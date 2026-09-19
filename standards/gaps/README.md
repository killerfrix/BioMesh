# Gaps

This is where a real gap gets confirmed (or ruled out) before any custom
schema is built on top of it. No candidate moves to `schemas/` without
going through this process first.

## Process

```
docs/ecosystem-map.md   (does a project already solve this?)
        ↓
standards/mappings/     (does an existing standard already model this?)
        ↓
protocols/              (does an existing protocol already cover this?)
        ↓
hardware/               (does existing hardware/an adapter already solve this?)
        ↓
software/ (once it exists) (does an existing tool already solve this?)
        ↓
Still unresolved? → documented here as a confirmed gap
```

Rule: **a specification is not created because it's convenient for
BioMesh. It's created only when the existing ecosystem proves it's
needed**, and that proof lives in this file (or the specific candidate's
file), not in the head of whoever proposes it.

## Candidates

| Candidate | File | Status |
|---|---|---|
| DIY environmental hardware calibration | [../calibration/README.md](../calibration/README.md) | Hypothesis — leading hypothesis under investigation, not a confirmed gap; pending a thorough review of ISA first |

## How to add a candidate

1. Verify it isn't already solved in `docs/ecosystem-map.md`.
2. Check it against every file in `standards/mappings/`.
3. If nothing covers it, document the candidate here with evidence (what
   was reviewed, what falls short, and why).
4. Only then open the gap's specific file/folder (like
   `standards/calibration/`).
