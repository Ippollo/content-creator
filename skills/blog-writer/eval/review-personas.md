---
name: blog-review-personas
description: Perspective-based reviewer personas for blog articles. Run after content-reviewer scoring for a second-pass evaluation.
---

# Blog Article Review Personas

After content-reviewer returns its score and rewrite, run these two personas against the final article. Each persona reads the article from a different angle and flags issues the rubric-based review might miss.

## The Skeptical Reader

**Perspective**: A mid-market business owner or operations leader who has read too many AI thought leadership pieces that say nothing. They clicked because the title promised something specific. They'll give you about 90 seconds before deciding whether to keep reading or close the tab.

**What they evaluate**:
- **Does this article prove its thesis?** Identify the thesis. Then check: does each section provide evidence (named source, specific metric, personal proof point), or does it just restate the thesis from a different angle? An article that asserts its thesis in five different ways without proving it once fails this check.
- **Would I believe the author knows what they're talking about?** Credibility comes from specificity — named tools, named research, specific timelines and numbers. Vague claims ("most companies struggle with...") without evidence erode trust.
- **Did I learn something I couldn't get from the headline?** If the article's value is fully captured by its title and H2 headers, the body sections aren't earning their space. Each section should reveal something the reader didn't already know.
- **Is the evidence real?** Check that every cited source is named, that statistics are attributed, and that no claim sounds like a plausible fabrication. One fake-sounding stat poisons the entire article's credibility.

**Output format**:
```
SKEPTICAL READER REVIEW:
- Thesis proven: [YES/PARTIALLY/NO] — [which sections prove vs. assert]
- Credibility: [HIGH/MEDIUM/LOW] — [specific evidence of expertise, or what's missing]
- Value beyond headline: [YES/NO] — [what new insight the body provides]
- Evidence verified: [PASS/FLAG] — [any stats or claims that need verification]
```

## The Skim Reader

**Perspective**: A professional who found this article via search or a social link. They have 30 seconds to decide if it's worth their time. They'll read the title, scan the H2 headers, read the first sentence of each section, glance at the conclusion, and decide.

**What they evaluate**:
- **H2 headers tell a story**: Read only the H2 headers in order. Do they create a logical progression? Could someone get the core argument just from the headers? Generic headers ("Background," "Implementation," "Conclusion") fail this test.
- **First sentences carry weight**: Read only the first sentence of each H2 section. Does each one make a specific claim or observation that pulls the reader into the section? Opening a section with context or history is weak — lead with the point.
- **Closing lands**: Read the last paragraph. Does it leave the reader with something to think about, or does it summarize what they already read?
- **Scanability**: Is the article visually scannable on a screen? Are there enough subheaders, bold key phrases, and whitespace to guide the eye? Or does it look like a wall of same-shaped paragraphs?

**Output format**:
```
SKIM READER REVIEW:
- Headers tell a story: [YES/NO] — [the story they tell, or what's missing]
- First sentences pull: [YES/NO] — [weakest section opening, if any]
- Closing lands: [YES/NO] — [1 sentence on why]
- Scanability: [GOOD/NEEDS WORK] — [specific formatting suggestions]
```
