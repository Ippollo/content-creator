# Swipe File: Will Larson — Solving the Engineering Strategy Crisis

Source: [lethain.com/solving-the-engineering-strategy-crisis](https://lethain.com/solving-the-engineering-strategy-crisis/)

## Why This Is Here

Study Larson for **Constraint-First Framing** and **trade-off reasoning in prose**. His writing demonstrates how to make explicit constraints do the argumentative work — the reader evaluates every subsequent decision through the constraint lens. He also shows how to use real company case studies as progressive evidence without drifting into consultant-speak.

## Technique Map

### 1. Definition-as-Thesis (adapt for Bold Claim hook)

Larson opens by naming a universal frustration ("the company doesn't have an Engineering strategy") then immediately reframes it: the problem isn't missing strategy — it's missing *written* strategy. The definition becomes the thesis.

> "I've come to believe that: Most companies *do* have an engineering strategy. Awareness of that engineering strategy is often inconsistent. It's very rare for a company to have a *written* engineering strategy."

**What to learn**: The reframe is the hook. Larson doesn't open with a statistic or a question. He takes something the reader already believes ("we don't have a strategy") and says "actually, you do — you just haven't written it down." This forces the reader to reconsider their own organization while reading.

**How Chris would adapt**: "Your company has an AI strategy. It's just that nobody wrote it down, so everyone's following a different version of it." Same reframe structure, applied to the mid-market ops space.

### 2. Constraint-First Case Studies (core technique)

Larson presents three company case studies (Stripe, Calm, Uber). Each one follows the same structure:

1. **Diagnosis** — the real constraints (not the aspirational ones)
2. **Approach** — specific policies that acknowledge those constraints
3. **Impact** — what happened because of explicit trade-offs

The constraints do the argumentative work. "We have a meaningfully complex financial platform internally" explains why Stripe runs a monolith before Larson ever says they run a monolith. The reader arrives at the conclusion before the approach is stated.

**What to learn**: Don't lead with the solution. Lead with the constraint set. When Chris writes "Here's what bridging the gap looks like," the reader hasn't yet internalized *why* the gap exists in this specific context. Larson's pattern: constraint → approach → impact. Every time.

**Stripe example**: "We need our entire risk budget to respond to external changes" → "We reduce technology risk by running a Ruby monolith in a monorepo" → "Avoided the decade-long journey into microservices that distracted most contemporaneous technology companies."

**What makes this powerful**: The constraint ("entire risk budget for external changes") makes the approach ("monolith in a monorepo") feel *inevitable* rather than controversial. Remove the constraint and the approach sounds like laziness. Include it and it sounds like discipline.

### 3. The Negative Case as Proof

After three positive case studies, Larson adds a section: "Absence shows value as well." Three brief failure stories (Digg, Stripe's Java introduction, Uber's competing routing technologies) — each tagged to the *specific component of strategy* that was missing.

> "Digg's 3+ year migration to V4... Honest diagnosis about challenges, but highly impractical approaches."
> "Stripe's introduction of Java... Rooted in inaccurate diagnosis."
> "Uber's invested heavily in competing routing technologies... following conflicting approaches without aligning on approach."

**What to learn**: Positive examples prove a pattern works. Negative examples prove it's *necessary*. The negative cases are deliberately brief (one sentence each) — they don't need the full case study treatment because their purpose is contrast, not instruction. Chris's articles could benefit from a brief "what happens without this" section after the main framework.

### 4. Honest Parenthetical Asides

Larson drops small, self-aware asides that prevent the writing from feeling like a methodology deck:

> "(Aside – this was very painful, I don't recommend it)"
> "(Life is tradeoffs: even good strategies have undesirable consequences!)"
> "Disappointingly, this is the same list in both cases."

**What to learn**: These asides are the operator's voice breaking through the structure. They signal "I'm not presenting a theory — I lived this." Chris already does this well in case studies ("Fifteen hours of work. No conversation. An email rejection.") but could deploy it more in articles. One or two per article is the sweet spot — more becomes a tic.

### 5. The "Tragically Practical" Recurring Beat

Larson uses a recurring structural beat: setting up what the reader hopes for, then delivering something less exciting but more true.

> "This might not be what you were excited to do when you wrote about getting more strategic in your annual goals, but it's what actually works."

**What to learn**: The closing line lands because it *deflates* rather than inflates. No mic-drop reframe, no inspirational call to action. Just: this is unglamorous and it works. This is a valid closing style for Chris's more framework-oriented articles — not every piece needs a Pattern Interrupt ending.

## Anti-Patterns to Avoid

- Larson's talk-notes origin shows: some sections read as bullet-point outlines rather than prose. Don't adopt the outline structure — adopt the constraint-first *reasoning pattern* and render it in full prose.
- His personal stakes are professional, not personal. "I designed Stripe's approach to architecture" is credibility, not vulnerability. Chris's articles need both — operational credibility *and* personal stakes ("I built this for a company that rejected me").
- Larson's articles can run long (2,700+ words) without sufficient compression. His pacing is more patient than Chris's target. Extract the structural pattern, apply it at 1,500–2,000 words.

## Content

Over the course of my career, I've frequently heard from colleagues, team members and random internet strangers with the same frustration: the company doesn't have an Engineering strategy. I don't think this problem is unique to Engineering: it's also common to hear folks complain that they're missing a strategy for Product, Design or Business. But, whereas I don't feel particularly confident speaking to why so many companies are missing a clear Business or Product strategy, I've come to have some clear opinions about why so many engineering organizations don't have a written strategy.

## What is Engineering strategy?

Whenever I think about strategy, I start from Richard Rumelt's *Good Strategy, Bad Strategy*, which identifies three pillars of effective strategy:

1. **Diagnosis** - a theory describing the nature of the challenge. This is trying to identify the root cause(s) at play.
2. **Guiding policy** - a series of general policies which will be applied to grapple with the challenge. If a guiding policy doesn't imply a tradeoff, you should be suspicious of it.
3. **Coherent actions** - a set of specific actions directed by guiding policy to address challenge.

I believe that Engineering strategy comes down to two core components:

1. **Honest diagnosis** that engages with the reality your organization's current needs and challenges
2. **Practical approach** to move forward while addressing the circumstances raised in the diagnosis

### Stripe – "We run a monolith in a monorepo."

Diagnosis:
1. We work in a business with dynamic external forces that change frequently and unexpectedly
2. We integrate with thousands of external financial infrastructure that are filled with bad, inconsistent, buggy technology
3. We have a meaningfully complex financial platform internally that our other products are built on

Approach:
1. We need our entire risk budget to respond to external changes
2. We reduce technology risk by running a Ruby monolith in a monorepo
3. Our developer tooling team invests heavily in running Ruby and our monorepo at scale
4. Exceptions to the above are narrow and rare

Impact:
1. Innovation budget (mostly) went into product, not infrastructure
2. Avoided the decade-long journey into (micro)services that distracted most contemporaneous technology companies

### Calm – "We're a product engineering company."

Diagnosis:
1. We're spending a lot of time arguing about adopting new technologies
2. We seem to be adopting new technologies out of interest in using and learning about them
3. We have a long-running services migration, but only small components have been moved out
4. Our developer tooling team is split between supporting monolith and service workflows

Approach:
1. We are a product engineering company
2. We adopt new technologies to create valuable product capabilities
3. We do not adopt technologies for other reasons
4. We write all code in the monolith unless there is a functional requirement that makes it extremely difficult
5. Exceptions are granted exclusively by the CTO, who will approve in writing

Impact:
1. We stopped arguing about technology investments
2. We exited several engineers who didn't want to follow our strategy
3. We consolidated tooling investments into our TypeScript monolith
4. We started spending innovation chips on product enhancements

### Absence shows value as well

1. Digg's 3+ year migration to V4. Honest diagnosis about challenges, but highly impractical approaches.
2. Stripe's introduction of Java had unclear evaluation criteria, took years to assess. Rooted in inaccurate diagnosis.
3. Uber invested heavily in competing routing technologies, causing significant friction. Following conflicting approaches without aligning.

## Strategy is everywhere. *Written* strategy is rare.

Most companies *do* have an engineering strategy. Awareness of that engineering strategy is often inconsistent. It's very rare for a company to have a *written* engineering strategy.

You can solve half the engineering strategy crisis by just writing stuff down.

## Closing

This might not be what you were excited to do when you wrote about getting more strategic in your annual goals, but it's what actually works.
