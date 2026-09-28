# proto1 — Run report

**Status** current · **Code** `proto1` · **Allocated** 2026-09-28

## 1. Problem

An agent finishes a task, the conversation ends in a green summary, and the human cannot tell which parts were actually checked. The failure mode is **unearned confidence**: a run that produced plausible output is read as a run that produced evidence.

## 2. Hypothesis

If every step of a run carries its own verdict and its own boundary, then a human reading only the run report will be able to tell, without asking the agent, which parts of the work are actually verified.

Stated so it can be wrong: this predicts readers will *stop and ask* fewer questions. It does not predict they will always read correctly.

## 3. Baseline

Bobastack today has no run surface. Agents report in conversation: a summary sentence, a diff, and "tests pass". The PRD names *preserve uncertainty* as a principle, but nothing enforces it at the point of reporting.

## 4. Change

One variable: the report's unit of information. Instead of a summary, each step is rendered as `verdict + observation + boundary`.

## 5. Protocol

1. Take one completed agent run that contains at least one genuine failure.
2. Write the run report per the rule above, using only evidence already produced by the run.
3. Do not add explanation, remediation, or reassurance.
4. Show it to a reader who has not seen the conversation.
5. Ask: *which parts of this work would you defend to a customer?*

## 6. Observation

Pending. The screen in `index.html` is a constructed specimen using a synthetic run (empty cart icon) — it has not yet been produced from a real run, which is exactly the confound worth testing.

## 7. Verdict

`uncertain` — the design is built but unevaluated.

## 8. Boundary

The current artifact establishes nothing about real behavior. A constructed specimen read well is the weakest possible evidence, and a reviewer who is the author of the artifact is the worst possible reader.

## 9. Learning

Placeholder until the protocol runs. Expected intervention type, if it works: a report template. If it fails: the report is being read, and the verdicts are being ignored — which would be a `rule` or `harness` problem, not a `test` problem.
