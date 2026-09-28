# Experiment protocol

Canonical rules for the lab. The hub (`index.html`) renders a summary of this; this file is the source of truth.

## The problem under test

Every experiment in this lab is a candidate solution to one recurring problem:

> **A human cannot tell, at a glance, whether an agent's work is actually verified — only that it finished.**

`proto1`, `proto2`, `proto3` are different solutions to that same problem. Comparing them is the point of the lab.

## Addressing

Each experiment has a **semantic code**. The code is the address. Say the code and nothing else needs to be inferred.

| Code | Directory | Lifetime |
| --- | --- | --- |
| `proto<N>` | `lab/proto<N>/` | Permanent, monotonically increasing, never reused |

Rules:

- Codes are allocated when an experiment is **reserved**, not when it is built.
- A code is never reassigned, even if the experiment is retired or rejected.
- A revision of an existing experiment is a **new** code. History lives in git and in the experiment's log — not in a `v2` suffix.
- Instruction to the agent: *"improve `proto1`"* means **touch `lab/proto1/` and the registry entry for `proto1` only**. Do not modify other variants; they are the comparison baseline.

## The nine fields

Every experiment carries a log (`experiment.md`) with all nine, in order. Missing fields mean the experiment is not runnable.

1. **Problem** — which failure mode is this variant trying to make less likely?
2. **Hypothesis** — the predicted change in behavior, stated so it can be wrong.
3. **Baseline** — the current observable behavior, recorded before the change.
4. **Change** — what was made, kept to one variable.
5. **Protocol** — exact steps, runnable top to bottom, deterministic.
6. **Observation** — what was actually seen, raw. Not summarized into a conclusion.
7. **Verdict** — exactly one of `verified`, `not verified`, `uncertain`, `needs human judgment`. Never "pass".
8. **Boundary** — what the observation *does not* establish.
9. **Learning** — what becomes easier to prevent next time, and whether that is a skill, test, rule, or architecture change.

## Verdict vocabulary

Verdicts are borrowed from the PRD's *preserve uncertainty* principle. They are not interchangeable and must not be upgraded for convenience.

| Verdict | Means | Does not mean |
| --- | --- | --- |
| `verified` | The protocol was run and the observation matched the hypothesis | The product is correct overall |
| `not verified` | The protocol was run and the observation contradicted the hypothesis | The variant must be deleted |
| `uncertain` | The protocol was run but the observation is ambiguous | Re-running will help |
| `needs human judgment` | The question is not answerable by the protocol alone | The work was wasted |

## Registry statuses

| Status | Meaning |
| --- | --- |
| `current` | The solution in use. Exactly one at a time |
| `candidate` | Reserved, described, not built |
| `retired` | Superseded. Stays readable and linked |
| `rejected` | Evaluated and discarded. Reason recorded in its log |

## Rules of the lab

- **One variable per experiment.** If two things changed, that is two experiments.
- **The baseline is recorded before the change**, not reconstructed afterwards.
- **Raw observations are pasted, not paraphrased.** A summary is a different observation.
- **No variant is edited to make another variant look worse.**
- **The registry is append-only in spirit.** Retired variants stay linked so results remain comparable over time.
- **A longer report is not a better experiment.** If the verdict did not change behavior, the experiment failed regardless of length.

## Adding an experiment

1. Allocate the next `proto<N>`.
2. Create `lab/proto<N>/experiment.md` with fields 1–4 filled and 5–9 as placeholders.
3. Add a row to the registry in `index.html`.
4. Run the protocol. Fill 5–9 from what happened, not from what was hoped.
