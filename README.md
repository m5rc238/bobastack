# Bobastack

> Reusable workflows for AI-assisted software development.

Bobastack is a small, opinionated collection of agent skills and workflows designed to make AI-assisted development more reliable.

The goal is not to make agents autonomous. The goal is to make common engineering practices **explicit, repeatable, observable, and progressively harder to get wrong**.

Every workflow declares a trigger, goal, procedure, verification step, stop condition, failure handling, and learning capture — so a mistake improves the system instead of disappearing when the task ends.

## What's here

| Path | Purpose |
| --- | --- |
| [PRD.md](PRD.md) | Full product definition: rationale, design principles, initial workflow set, evolution loop |

## Initial workflow set

| Workflow | For |
| --- | --- |
| `/investigate` | Bugs and unexpected behavior — reproduce before modifying |
| `/feature-map` | Vague reports — map human language to executable code and a verification path |
| `/verify` | Implemented changes — observe real behavior, state the verification boundary |
| `/review` | Pre-ship checks — correctness, regressions, architecture, security, complexity |
| `/retro` | Repeated failures — turn them into a skill, test, rule, or architecture change |

## Design principles

Failure first. Mechanisms over instructions. Observe the real system. Verification must match the claim. Keep workflows small. Minimize context. Make failure recoverable. Turn repeated failures into system memory. Preserve uncertainty.

## A simple rule

> **If a workflow cannot explain what failure it prevents and how we know it helped, it probably doesn't belong in Bobastack.**

## License

To be decided.
