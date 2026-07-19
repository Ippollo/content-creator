# X Algorithm & Dynamics (2026)

This document captures the operating mechanics of the X "For You" feed algorithm. Updated May 2026 from the [open-source X recommendation algorithm](https://github.com/xai-org/x-algorithm) released by xAI.

> **Source confidence**: Derived from actual production code (Rust + Python), not secondhand reporting. Weight constants are loaded via server-side feature switches, so exact magnitudes can change without code deploys. The *structure and relative signals* are reliable.

## System Architecture

The "For You" feed runs a multi-stage pipeline:

1. **Candidate Sourcing** — Posts from accounts you follow (Thunder/in-network) + ML-discovered posts from a global corpus (Phoenix retrieval/out-of-network)
2. **Hydration** — Enrich candidates with author info, media data, engagement counts, mutual follow graphs
3. **Filtering** — Remove duplicates, old posts, self-posts, blocked/muted authors, muted keywords, previously seen posts
4. **Scoring** — Phoenix (Grok-based transformer) predicts engagement probabilities per post
5. **Weighted Combination** — Final score = weighted sum of predicted engagement probabilities
6. **Author Diversity** — Exponential decay applied to repeated posts from the same author
7. **OON Adjustment** — Out-of-network content scaled by a multiplier (< 1.0 by default)
8. **Selection** — Sort by final score, select top K

## The Scoring Model: Phoenix

Phoenix is a Grok-based transformer that predicts engagement probabilities. Key properties:

- **No hand-engineered features.** The model learns entirely from user engagement history sequences — what you liked, replied to, shared, dwelled on. No manual feature engineering for content relevance.
- **Candidate isolation.** During inference, candidates cannot attend to each other — only to user context. A post's score doesn't depend on what other posts are in the batch.
- **Continuous training.** Production Phoenix trains continuously on real-time data. The open-source release is a frozen checkpoint.

## Engagement Actions Tracked

The algorithm predicts probabilities for 19 action types. Each gets its own weight in the final score formula:

```
Final Score = Σ (weight_i × P(action_i))
```

### Positive-Weight Actions

| Action | Code Field | Signal |
|---|---|---|
| **Like** | `favorite_score` | User taps heart |
| **Reply** | `reply_score` | User writes a reply |
| **Repost** | `retweet_score` | User reposts to timeline |
| **Quote** | `quote_score` | User quotes with commentary |
| **Share** | `share_score` | Native share action |
| **Share via DM** | `share_via_dm_score` | User sends post to someone |
| **Share via Copy Link** | `share_via_copy_link_score` | User copies the URL |
| **Click** | `click_score` | User clicks to expand |
| **Profile Click** | `profile_click_score` | User clicks author's profile |
| **Photo Expand** | `photo_expand_score` | User expands an image |
| **Video Quality View** | `vqv_score` | User watches video past minimum duration threshold |
| **Dwell** | `dwell_score` | User paused on the post (binary) |
| **Dwell Time** | `dwell_time` | How long user stayed on the post (continuous) |
| **Follow Author** | `follow_author_score` | User follows author after seeing post |

### Negative-Weight Actions

| Action | Code Field | Signal |
|---|---|---|
| **Not Interested** | `not_interested_score` | User marks "not interested" |
| **Block Author** | `block_author_score` | User blocks the author |
| **Mute Author** | `mute_author_score` | User mutes the author |
| **Report** | `report_score` | User reports the post |
| **Not Dwelled** | `not_dwelled_score` | User scrolled past without pausing |

### Notable Absences

- **Bookmarks** are not listed as a separate scoring signal in the open-source code. Previous guidance treated bookmarks as "high value" — this may have been inaccurate, or bookmarks may be folded into another signal internally.
- **Impressions** are not a scoring input. The model predicts engagement given that a post is shown, not whether to show it based on past impressions.

## Author Diversity Decay

The `AuthorDiversityScorer` applies an exponential decay to repeated appearances of the same author in a single feed response:

```
multiplier = (1 - floor) × decay_factor^position + floor
```

Where `position` is how many times this author has already appeared (0-indexed). First appearance = full score. Subsequent appearances decay toward the floor. Practical effect: your 3rd post in someone's feed today is worth significantly less than your 1st.

## Out-of-Network (OON) Scaling

Out-of-network content (posts shown to non-followers via "For You") gets multiplied by `OON_WEIGHT_FACTOR` (< 1.0). Special cases:
- **New users** with enough follows get `NEW_USER_OON_WEIGHT_FACTOR` (likely higher)
- **Topic feeds** use `TopicOonWeightFactor`

To reach beyond your follower base, content must score high enough to overcome this discount.

## Content Understanding: Grox

Before scoring, the Grox pipeline runs content understanding:
- Spam detection classifiers
- Post-category classification
- PTOS (policy/trust/safety) enforcement
- Content embedding for similarity search

Content flagged by these classifiers may be filtered before it reaches the scorer.

## Filtering Rules

Posts are removed at two stages:

**Pre-Scoring**: Duplicates, posts too old, self-posts, repost deduplication, paywalled content user can't access, previously seen posts, previously served posts, muted keywords, blocked/muted authors.

**Post-Selection**: Deleted/spam/violence/gore via visibility filtering, conversation thread deduplication.

Key implication: recycling identical content has zero algorithmic value — previously seen posts are filtered out.

## Post Mechanics & Constraints

These are empirical best practices, not derived from the open-source code:

### Character Limits & Lengths
- **Sweet spot (71-140 chars)**: Maximum baseline engagement for singles
- **Full singles (up to 280 chars)**: Allowed if every word earns its place
- **Threads**: Sparingly. Standalone hook tweet, numbered insights, hard ceiling of 10 posts

### The Penalty Box
- **External links in body**: X penalizes off-platform links (pushes users off the platform)
- **Hashtag stuffing**: Degrades quality. Zero or one targeted hashtag max
- **Corporate speak**: "Excited to announce" is filtered by users and likely by content classifiers
