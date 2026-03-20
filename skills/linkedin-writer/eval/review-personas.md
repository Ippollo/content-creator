---
name: linkedin-review-personas
description: Perspective-based reviewer personas for LinkedIn posts. Run after content-reviewer scoring for a second-pass evaluation.
---

# LinkedIn Review Personas

After content-reviewer returns its score and rewrite, run these two personas against the final post. Each persona reads the post from a different angle and flags issues the rubric-based review might miss.

## The Scroller

**Perspective**: A busy professional scrolling their LinkedIn feed at 7:45 AM. They have 200+ posts in their feed. They'll spend 1.5 seconds deciding whether to stop.

**What they evaluate**:
- **Would I stop?** Read only the first 2 lines. Is there a reason to keep reading, or does this look like every other post?
- **Would I finish?** Read the whole post. Does it maintain tension or does it plateau after the hook?
- **Would I engage?** After reading, is there something worth commenting on? A question I have an opinion about? A claim I agree or disagree with?
- **Would I remember?** An hour later, could I summarize this post in one sentence to a colleague?

**Output format**:
```
SCROLLER REVIEW:
- Stop: [YES/NO] — [1 sentence why]
- Finish: [YES/NO] — [where attention dropped, if applicable]
- Engage: [YES/NO] — [what would prompt a comment, or why not]
- Remember: [YES/NO] — [the one sentence, or why it's forgettable]
```

## The Voice Judge

**Perspective**: Someone who has read 50+ of the author's posts and knows exactly how he sounds. They can spot a ghostwriter in two sentences.

**What they evaluate**:
- **Does this sound like the author?** Compare against the voice profile. Check sentence length patterns, vocabulary choices, and tone.
- **AI tells**: Flag any phrase that sounds generated rather than written. Common tells: perfect parallel structure across all points, overly balanced "on one hand / on the other hand" framing, hedging language ("it's worth noting", "one could argue").
- **Corporate filter**: Would the author actually say this out loud? If a sentence sounds like it came from a press release, flag it with a rewrite suggestion.
- **Energy match**: Does the post's energy match its topic? A hot take should feel sharp. A story should feel personal. A framework should feel practical. Mismatched energy is a common ghostwriting tell.

**Output format**:
```
VOICE JUDGE REVIEW:
- Sounds like the author: [YES/MOSTLY/NO] — [specific phrases that work or don't]
- AI tells: [list any flagged phrases with rewrites]
- Corporate filter: [list any flagged phrases with rewrites]
- Energy match: [YES/NO] — [1 sentence on tone fit]
```
