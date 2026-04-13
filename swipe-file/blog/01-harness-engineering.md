# Swipe File: Harness Engineering Operator's Guide

Extracted from: `articles/published/2026-04-08-harness-engineering-operators-guide.md`

## Analysis

- **Hook pattern**: Bold claim ("Most people think better prompts fix broken AI agents. They don't.") + personal failure admission ("I spent weeks rewriting prompts before I realized...")
- **H2 structure**: 
  - The Three Layers (Context/Definitions) 
  - The Proof Point (Data-backed example)
  - Rule/Principle (Mitchell Hashimoto's Rule)
  - Primitives (The meat: 7 specific patterns)
  - Where to Start (Actionable advice)
- **Section rhythm**: ~100–200 words per section. Uses horizontal rules (`---`) as pacing between major concepts.
- **CTA style**: Direct question ("What's the one infrastructure constraint you could add this week to make your AI agents more reliable?")

## Content

Most people think better prompts fix broken AI agents.

They don't.

The system around the model matters more than the model itself.

I spent weeks rewriting prompts before I realized the agent was missing half the context it needed. The prompt wasn't the problem. The setup was.

There's a name for this now. It's called harness engineering. And it's the layer that determines whether your AI investments produce results or produce noise.

---

## The Three Layers of AI Agent Infrastructure

The industry is converging on a three-layer model. Each layer builds on the one below it.

**Prompt engineering** is what you ask.
This is what everyone focuses on because it's the most visible layer.

**Context engineering** is what the agent can see.
Files, prior decisions, active preferences. The agent can only work with what you give it access to.

**Harness engineering** is how the agent operates.
The harness is everything that isn't the model or the prompt.

And it's the layer almost nobody invests in.

---

## The Proof Point

LangChain was ranked outside the Top 30 on Terminal-Bench 2.0, an industry benchmark for AI agent performance.

Then they jumped to Top 5.

They didn't change the model. They didn't rewrite their prompts. They improved the harness — the infrastructure around the model. Structured verification loops. Better error recovery. Automated validation at each step.

Same model. Better system around it. Dramatically different results.

That's the entire thesis in one data point.

I made the same mistake. I thought my prompts weren't good enough. I rewrote them. I added more instructions. I specified formats and tone and output structure. The results got marginally better. Then I stopped tweaking the prompt and started building the system around it. The results jumped.

---

## Mitchell Hashimoto's Rule

Mitchell Hashimoto put it plainly in February 2026:

"Every time the agent makes a mistake, don't just hope it does better next time. Engineer the environment so it can't make that specific mistake the same way again."

This is the difference between coaching and system design.

Coaching says: try harder. Be more careful. Read the instructions again.

System design says: I changed the process so that error can't happen.

If you've ever added a checklist to your onboarding because new hires kept missing the same step, you already understand harness engineering. You just didn't know it had a name.

---

## Seven Harness Engineering Primitives

From research across the [OpenDev paper](https://arxiv.org/html/2603.05344v1), [Anthropic's context engineering guide](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents), and [Stanford's Meta-Harness project](https://github.com/stanford-iris-lab/meta-harness-tbench2-artifact), seven distinct infrastructure patterns emerge.

### 1. Scaffolding — Load What's Needed, Not Everything

Before asking an agent to analyze a quarterly report, I load the template, the prior quarter for comparison, and the scoring criteria. If I don't, it asks for them one at a time. Three turns wasted before it starts the actual work.

That's scaffolding. Everything the agent needs before it begins. The right instructions. The right tools. The right reference materials.

Most people launch their agent with a blank prompt and hope it figures out what it needs. Don't. Load the context upfront. Save the turns.

### 2. Context Management — External Memory Beats Internal Recall

AI agents have a context window. As conversations grow longer, early instructions get pushed out. The agent forgets what you told it in turn one.

This is why an agent that follows your formatting rules perfectly in the first response ignores them by the twentieth.

For longer projects, have the agent write progress notes to a file outside the conversation. Reference those notes when it needs to remember what was decided three hours ago. External memory beats internal recall every time.

### 3. System Reminders — Inject Rules at the Point of Decision

I added a rule to my workflow that fires right before the agent marks a task complete: re-read the original requirements, confirm each one was met. It catches errors that would've shipped.

That's a system reminder. Guidance injected at the exact moment it matters — not at the start of the conversation where it fades out, but at the point of decision.

Your mistakes file is useless if the agent reads it once and forgets it. Put the reminder where the mistake happens. If a specific tool routinely hallucinates formatting, inject a validation rule immediately after the tool call, not in the system prompt.

### 4. Environment Bootstrapping — Start on Turn One

When an agent starts a new project, it spends its first several turns exploring the file structure, reading documents, and figuring out what's going on. That's 2–5 turns of exploration burned before any real work begins.

I created a one-page project state document for each active project. Current status, last change, known issues, what's in progress. The agent reads it first and starts working immediately.

Saves time. Reduces confusion. Costs nothing.

### 5. Dual-Mode Operation — Plan Before You Touch Anything

Structure your AI workflows in two phases. Phase one: analyze the situation and propose a plan. Phase two: execute the plan.

During phase one, the agent reads and analyzes but cannot modify anything. Only after the plan is reviewed does it get permission to make changes.

The separation prevents the agent from making changes you didn't authorize. It also forces it to think before it acts. Which is exactly what you want.

### 6. Adaptive Memory — Build a Playbook, Not a Graveyard

Most teams have a lessons learned document. Most teams never look at it again.

At the end of every AI-assisted project, add a five-minute reflection step. What went wrong? Should we add a rule to prevent this next time? Over time, you build a playbook of what works in your specific context.

Good patterns get reinforced. Bad ones get flagged. The system learns. Instead of relying on a human to read the playbook, feed the adaptive memory file directly into the agent's initialization phase.

### 7. Verification Loops — The Gate That Ships or Stops

Build a mandatory verification step into every workflow. Not optional. Not "remember to check your work." A hard gate that must pass before the task is marked complete.

Run the checklist. Check the formatting. Confirm the numbers. Fix what's wrong.

LangChain's Terminal-Bench jump came from this alone. Same model. Better verification. If you don't have a systemic verification loop, you are accepting raw, unverified output as your baseline.

---

## Where to Start

You don't need to implement all seven primitives this week. Start with the ones that give you the most leverage for the least effort.

➡️ **Add a pre-completion checklist.** Before any AI-generated output goes out, force a verification step. Re-read the requirements. Confirm each item was addressed. Two minutes of checking saves twenty minutes of rework.

➡️ **Create project state documents.** One page per active project. Current status, last change, known issues. Your agent starts working immediately instead of spending turns figuring out where it is.

➡️ **Build reflection into your workflow.** After each project, ask what worked and what didn't. Capture the lesson. Use it next time.

➡️ **Separate planning from execution.** The separation costs nothing.

---

The question isn't whether your AI tools can do the work. The question is whether you've built the harness engineering to let them do it consistently.

What's the one infrastructure constraint you could add this week to make your AI agents more reliable?
