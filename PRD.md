# Bobastack PRD

> Reusable workflows for AI-assisted software development.

## Summary

Bobastack is a small, opinionated collection of agent skills and workflows designed to make AI-assisted development more reliable.

The goal is not to make agents autonomous.

The goal is to make common engineering practices **explicit, repeatable, observable, and progressively harder to get wrong**.

## Why Bobastack exists

AI coding agents are increasingly capable of writing code, navigating repositories, running tools, and fixing their own mistakes.

The remaining problems are often not:

> "Can the agent write the code?"

They are:

* Did it understand the task?
* Did it find the right part of the system?
* Did it make the smallest safe change?
* Did it actually verify the behavior?
* Did it verify the right thing?
* Did it repeat a known mistake?
* Did a local fix create a system-level problem?
* Did the workflow produce evidence that the work is actually correct?

Bobastack treats these as **workflow problems**, not primarily prompting problems.

## Core principle

Every workflow should answer:

> **What failure mode are we trying to prevent, and what concrete mechanism makes that failure less likely?**

A workflow should therefore contain more than instructions. It should define:

1. **Trigger** — when should this workflow be used?
2. **Goal** — what outcome are we trying to achieve?
3. **Procedure** — what should the agent actually do?
4. **Verification** — how can the result be checked?
5. **Stop condition** — when should the agent stop?
6. **Failure handling** — what happens when verification fails?
7. **Learning** — what should become easier to prevent next time?

## The basic loop

```text
Task
  ↓
Understand
  ↓
Act
  ↓
Observe
  ↓
Verify
  ↓
Evaluate
  ↓
Pass ─────────→ Done
  │
  └─ Fail → Investigate → Fix → Verify again
                         ↓
                    Capture learning
```

The important part is the feedback loop.

A failure should ideally improve the system rather than disappear when the current task ends.

## What Bobastack is

Bobastack is:

* a library of agent workflows
* a set of reusable engineering practices
* a place to encode recurring failure modes
* a lightweight alternative to large agent orchestration systems
* designed to work with existing coding agents
* intentionally inspectable and editable as Markdown

## What Bobastack is not

Bobastack is not:

* an autonomous coding agent
* a replacement for Claude Code, Codex, Cursor, or OpenCode
* a multi-agent framework
* a collection of prompts without verification
* a guarantee that generated code is correct
* a substitute for product or engineering judgment

## Design principles

### 1. Failure first

Start with a failure mode, not a feature.

Bad:

> Add a planning skill.

Better:

> Agents frequently start implementing before discovering important constraints.

Then design a workflow that addresses that failure.

### 2. Prefer mechanisms over instructions

Prefer:

```text
instruction
→ automated check
→ observable result
```

over:

```text
"Please remember to..."
```

When a rule matters repeatedly, look for a way to enforce it mechanically.

### 3. Observe the real system

Whenever possible, verify behavior in the environment where it actually occurs.

Prefer:

```text
change
→ run
→ interact
→ observe
→ verify
```

over:

```text
change
→ inspect diff
→ assume correctness
```

### 4. Verification must match the claim

Do not say:

> "The feature works."

when the evidence only establishes:

> "The test passed."

Every workflow should make its verification boundary explicit.

Ask:

```text
What did we observe?
What does that establish?
What does it not establish?
```

### 5. Keep workflows small

A workflow should solve one recognizable problem.

Prefer several composable workflows over one giant "do everything" workflow.

### 6. Minimize context

Only load the instructions needed for the current task.

More instructions do not automatically produce better behavior.

### 7. Make failure recoverable

Workflows should favor:

* small changes
* reversible operations
* checkpoints
* explicit state
* clear stop conditions

### 8. Turn repeated failures into system memory

If the same mistake happens repeatedly:

```text
failure
  ↓
understand cause
  ↓
choose intervention
  ↓
skill / test / rule / architecture
```

Do not merely add another warning to a prompt.

### 9. Preserve uncertainty

A workflow should be allowed to conclude:

```text
verified
not verified
uncertain
needs human judgment
```

"Pass" should not be the only useful outcome.

## Initial workflow set

Bobastack should start with a small set of high-value workflows.

### `/investigate`

For bugs and unexpected behavior.

```text
report
 ↓
reproduce
 ↓
map relevant system
 ↓
collect evidence
 ↓
identify cause
 ↓
propose fix
```

Do not modify the system until there is sufficient evidence about the cause.

### `/feature-map`

For vague feature or bug reports.

```text
human concept
 ↓
feature
 ↓
UI / API / runtime
 ↓
relevant code
 ↓
verification path
```

The goal is to connect human language to executable system locations.

### `/verify`

For validating an implemented change.

```text
expected behavior
 ↓
verification procedure
 ↓
runtime observation
 ↓
result
```

The workflow should distinguish implementation evidence from broader product judgment.

### `/review`

For detecting problems before shipping.

Review should prioritize:

1. correctness
2. regressions
3. architecture
4. security
5. maintainability
6. unnecessary complexity

It should produce actionable findings rather than a generic approval.

### `/retro`

For repeated failures.

Ask:

```text
What failed?
Why did it fail?
Was this preventable?
Could a workflow, test, rule, or architecture prevent recurrence?
```

The output should be a concrete system improvement where appropriate.

## Workflow quality

A workflow is successful when it changes agent behavior or outcomes.

It is not successful merely because:

* the Markdown is comprehensive
* the agent follows every step
* the output looks professional
* the workflow produces a long report

Measure the mechanism. For example:

```text
Before:
agent frequently changes code before reproducing bugs.

After:
agent reproduces the bug first.
```

That is meaningful improvement.

## Evolution

Bobastack should evolve through a loop:

```text
real task
   ↓
failure observed
   ↓
workflow created
   ↓
workflow used
   ↓
failure / success recorded
   ↓
workflow improved
   ↓
repeat
```

The repository itself becomes an experimental environment for agent workflows.

## Broader architecture

Bobastack intentionally starts at the workflow layer.

The broader agent system can eventually be understood as:

```text
┌─────────────────────────────┐
│       EPISTEMIC LAYER       │
│ evidence / claims /         │
│ uncertainty / decisions     │
├─────────────────────────────┤
│       DECISION LAYER        │
│ routing / classification /  │
│ System 1 / System 2         │
├─────────────────────────────┤
│         HARNESS             │
│ tools / state / permissions │
│ verification / environment  │
├─────────────────────────────┤
│       BOBSTACK              │
│ workflows / skills / rules  │
├─────────────────────────────┤
│          AGENT              │
└─────────────────────────────┘
```

Bobastack does not need to implement these other layers.

They provide the context for designing better workflows.

## Long-term direction

The long-term question is not:

> "How many skills can Bobastack have?"

It is:

> **Can repeated engineering experience be converted into increasingly reliable agent behavior?**

That means Bobastack should gradually move from:

```text
instructions
```

toward:

```text
instructions
+ verification
+ tests
+ system constraints
+ observability
+ reusable knowledge
```

without becoming unnecessarily complex.

## A simple rule

> **If a workflow cannot explain what failure it prevents and how we know it helped, it probably doesn't belong in Bobastack.**
