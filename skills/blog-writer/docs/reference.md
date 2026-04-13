# Blog Writer Reference

Supporting reference for the `blog-writer` skill. The agent reads this during Steps 2–4 of the workflow.

## Search Intent Types

Identify the reader's intent before outlining. This shapes the article's structure and depth.

| Intent | Reader wants to... | Article approach |
|---|---|---|
| **Informational** | Learn or understand something | Explain clearly, use examples, define terms |
| **Commercial** | Compare options before deciding | Pros/cons, comparison tables, recommendations |
| **Transactional** | Take action (hire, buy, sign up) | Clear value prop, social proof, strong CTA |
| **Navigational** | Find a specific resource | Direct answers, link to the resource |

Most personal branding articles are **informational** or **commercial**. Transactional intent maps to service/consulting pages.

## Article Archetypes

| Archetype | Description | Best For |
|---|---|---|
| **Deep Dive** | Comprehensive analysis of one topic | Building authority, cornerstone content |
| **How-To / Guide** | Step-by-step walkthrough | Search traffic, practical value |
| **Framework / Model** | Original or adapted framework | Thought leadership, shareability |
| **Case Study** | Behind-the-scenes of a project or result | Credibility, consulting leads |
| **Comparison** | A vs B analysis with recommendation | Search traffic, decision-making value |
| **The Reframe** | Challenges a common assumption by presenting familiar expertise through a new lens | Positioning, career narrative, contrarian thought leadership |
| **Lessons Learned** | Personal experience distilled into principles | Authenticity, career narrative |
| **Trend Analysis** | Industry trend with expert interpretation | Timeliness, positioning |
| **Anti-Patterns** | What NOT to do and why | Contrarian angle, engagement |

## Voice Rules

- Match the user's natural sentence patterns, vocabulary, and tone from the voice profile
- The voice can breathe more in long-form. Longer sentences and deeper explanations are appropriate, but maintain the directness and specificity
- Use the user's actual experiences and domain expertise as raw material
- Sound like a real expert, not a content mill or an AI

## Structure Rules

- **Title**: Include target keyword, be specific and compelling. No clickbait. SEO title: 60–65 characters.
- **Intro** (100–200 words): Hook the reader with a specific problem, bold claim, or scenario. State what the article will cover and why it matters. Include target keyword naturally.
- **Body**: 3–6 H2 sections, each covering one clear sub-topic. Each section: 150–300 words. Use H3s within sections when there are distinct sub-points.
- **FAQ section** (optional): When relevant, add 2–3 FAQ-style H3s targeting common long-tail queries. Write direct answers (40–60 words) to target featured snippets.
- **Conclusion** (100–150 words): Summarize the key takeaways without repeating the intro. End with a clear CTA (contact, comment, apply the framework, read a related article).
- **Total length**: 1,500–2,500 words unless the user specifies otherwise
- **Paragraph length**: 2–4 sentences max. Use whitespace generously.
- **Lists and formatting**: Use bullet lists, numbered steps, and bold key phrases for scanability
- Do NOT use em dashes. Use a period, comma, or rewrite instead.

## SEO Rules

- **Target keyword**: Include in the title, first 100 words, at least 2 H2s, and the conclusion
- **Supporting keywords**: Distribute naturally through body sections
- **Meta description**: 145–155 characters, includes target keyword, compelling enough to click
- **Heading hierarchy**: Single H1 (the title), logical H2/H3 structure, no skipped levels
- **Internal links**: When `internal_links` are provided, suggest 3–7 placements with descriptive anchor text. Otherwise, note where links could go.
- **External sources**: When referencing third-party data or frameworks, suggest 2–4 authoritative sources. Never fabricate citations.
- **Readability**: Short paragraphs, sub-300 word sections, varied sentence length

## Swipe File Rules

- Learn PATTERNS from swipe examples: structure, section rhythm, intro hooks, depth of analysis
- NEVER copy or closely paraphrase content from swipe examples
- Blend patterns from multiple examples rather than mimicking one
- If the user's voice conflicts with a swipe pattern, prioritize voice

## Frontmatter Format

```yaml
---
title: "Article Title"
slug: article-title
target_keyword: "primary keyword"
supporting_keywords: ["keyword 2", "keyword 3"]
meta_description: "145-155 char description"
pillar: "Content Pillar Name"
archetype: "Deep Dive"
search_intent: "informational"
status: draft
date: YYYY-MM-DD
word_count: NNNN
atoms: []
---
```
