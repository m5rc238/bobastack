# Lab

The lab exists to make one question answerable by comparison rather than argument:

> A human cannot tell, at a glance, whether an agent's work is actually verified — only that it finished.

Every `proto<N>` is a different candidate solution to that question. Exactly one is `current`. The rest stay linked so results remain comparable over time.

## Addressing

| Code | Directory | Lifetime |
| --- | --- | --- |
| `proto<N>` | `lab/proto<N>/` | Permanent, never reused |

Name the code to direct work. `improve proto1` means edit `lab/proto1/` and its registry row in `index.html` — nothing else, because the other variants are the comparison baseline.

Codes are allocated on reservation, never reassigned, and never versioned with suffixes. A revision is a new code; history lives in git.

## Layout

```
lab/
  index.html          hub — registry, protocol summary, rules
  protocol.md         canonical protocol: nine fields, verdicts, statuses
  proto<N>/
    index.html        the variant itself
    experiment.md     its log: problem → learning
```

Open `index.html` in a browser. No build, no dependencies.

## Run it properly

`index.html` is a specimen, not a result. The protocol is in `protocol.md`; the interesting failures are in fields 6 through 9, and those can only be filled by an actual run.
