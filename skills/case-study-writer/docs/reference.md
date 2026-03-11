# Case Study Writer Reference

Supporting reference for the `case-study-writer` skill. The agent reads this during Steps 1–4 of the workflow.

## Intake Questionnaire

Use these questions to extract project details. Group into rounds — don't overwhelm the user.

### Round 1: Context

1. **What was the project?** (Brief description — one or two sentences)
2. **What was your role?** (Title, scope of responsibility)
3. **What was the environment?** (Company size, industry, team structure)
4. **What was broken or at risk?** (The core problem in plain language)

### Round 2: Action

5. **What did you do first?** (Discovery, assessment, listening phase)
6. **What was your approach?** (Methodology, framework, or strategy)
7. **What tools or systems did you use?** (Specific software, platforms, processes)
8. **What was the timeline?** (Duration from start to measurable result)
9. **Who else was involved?** (Team, stakeholders, cross-functional partners)
10. **What resistance or obstacles did you face?** (Political, technical, resource constraints)

### Round 3: Results

11. **What changed?** (The core outcome in one sentence)
12. **What metrics moved?** (Before/after numbers — even rough ones help)
13. **What's the ongoing impact?** (Is the change still in effect? Has it scaled?)
14. **What would you do differently?** (Honest reflection adds credibility)
15. **What's the one-line lesson?** (The generalizable takeaway)

## Case Study Archetypes

| Archetype | Description | Best For |
|---|---|---|
| **Process Transformation** | Fixing broken workflows, reducing cycle times, improving handoffs | Operations roles, consulting pitches |
| **Tool/System Implementation** | Selecting, deploying, or building a system that solved a problem | Technical roles, system integrators |
| **Revenue Impact** | Work that directly affected revenue, retention, or cost reduction | Business-facing roles, executive audience |
| **Team & Culture** | Building teams, changing behaviors, improving collaboration | Leadership roles, people management |
| **AI/Automation** | Implementing AI agents, automation, or intelligent workflows | AI-forward positioning, innovation narrative |

## Evidence Types

Strong case studies use multiple evidence types. Aim for at least 3 per case study.

| Evidence Type | Example | Strength |
|---|---|---|
| **Hard metrics** | "Reduced from 10 weeks to 4 weeks" | Highest — concrete and verifiable |
| **Directional ranges** | "Improved by roughly 40-60%" | Good — honest when exact numbers aren't available |
| **Before/after contrast** | "Before: 5 email threads. After: one dashboard" | Strong — visual and memorable |
| **Timeline markers** | "Within 3 weeks, stability replaced chaos" | Good — shows speed of impact |
| **Third-party validation** | "Client renewed for a second year" | Strong — external proof |
| **Specific actions** | "Implemented a Kanban board with three columns" | Good — proves you actually did the work |

### Metric Formatting

- Always pair a number with context: "Cut onboarding from 10 weeks to 4 weeks" (not just "60% improvement")
- Use the most concrete unit available: weeks > months, dollars > percentages
- If exact numbers aren't available, say so: "roughly," "approximately," "in the range of"
- Never fabricate or inflate metrics

## Confidentiality Guidelines

**Default posture: anonymize everything.** Only use real names/details with explicit permission.

| Detail Type | Anonymization Approach |
|---|---|
| Client/company name | "[a mid-market MSP]", "[a SaaS company with ~200 employees]" |
| Revenue/financial data | Percentage changes or ranges ("revenue grew 30-40%") |
| Proprietary tools | Generic description ("internal ticketing system") |
| Team member names | Role descriptions ("the operations lead") |
| Specific contract terms | Omit entirely |

**Safe to include by default:**
- Tools and platforms you used (Kanban, Teams, Power Automate — these are your skills)
- Your role and title
- General industry and company size range
- Timeline and duration of work
- Outcomes expressed as ratios or percentages

## SCAR Structure Rules

| Section | Purpose | Length Guide |
|---|---|---|
| **Situation** | Set the scene. Environment, team, business context | 150–250 words |
| **Challenge** | Name the pain. What was broken, inefficient, or at risk? | 150–250 words |
| **Action** | Show the work. Specific steps, tools, decisions, timeline | 400–600 words (largest section) |
| **Result** | Prove the impact. Metrics, before/after, ongoing effects | 200–350 words |
| **Takeaway** | Generalize. What principle does this illustrate beyond this project? | 100–200 words |

### Structure Notes

- **Situation and Challenge** can sometimes merge if the context is simple — don't pad
- **Action** is the heart — this is where the reader evaluates your capabilities
- **Result** must include at least one hard metric or directional range
- **Takeaway** should feel like advice, not self-congratulation

## Frontmatter Format

```yaml
---
title: "Case Study Title"
slug: case-study-slug
target_keyword: "primary keyword"
supporting_keywords: ["keyword 2", "keyword 3"]
meta_description: "145-155 char description"
pillar: "Content Pillar Name"
archetype: "Process Transformation"
project_role: "Operations Manager"
project_duration: "3 months"
project_industry: "Managed IT Services"
key_metric: "Reduced delivery time from 10+ weeks to under 4 weeks"
tools_used: ["Kanban", "Microsoft Teams", "Power BI"]
confidentiality: "anonymized"
status: draft
date: YYYY-MM-DD
word_count: NNNN
atoms: []
---
```
