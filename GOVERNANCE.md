# Governance

## Current state

BioMesh is at an early stage, with a single maintainer. This document
describes how decisions are made today and how it's expected to evolve as
more contributors join.

## Decision-making

- Architecture decisions (which standard to use, when a custom schema is
  justified, what goes into the monorepo) are documented as an explicit
  decision in `CLAUDE.md` — they don't stay implicit in the code.
- Any decision that contradicts a previously documented decision must
  explain why, not just silently replace it (real example: the revision
  that dropped `Observation`/`Specimen`/`Device` as a custom schema in
  favor of `standards/mappings/`, and the later refinement that demoted
  `schemas/` to a secondary tool instead of removing it).
- While there's a single maintainer, the maintainer decides. Once regular
  contributors join, architecture decisions move to being discussed in an
  issue/RFC before being implemented.
- Gap confirmation follows the process defined in
  `standards/gaps/README.md` — no gap becomes a custom schema without
  going through it.

## Versioning

- Software and firmware (once they exist): [Semantic Versioning](https://semver.org/)
  (`MAJOR.MINOR.PATCH`).
- Custom protocols and standards (`standards/calibration/` and any future
  schema): explicit version in the document itself (`v1.0`, `v1.1`...),
  with a note on what changed and why.
- Hardware: explicit version per design (`soil-module-v1`, `v0.3`...).

## Licensing

Each type of content may have a different license — see the "Licenses"
section in the [README](README.md). Before reusing or commercializing any
third-party component, follow the flow:

```
Identify license → check permissions → check attribution
→ check modification restrictions → check patents/trademarks
→ document provenance → commercialize if permitted
```

## Roles (future)

For now there are no formal roles beyond "maintainer." These will be
documented here once they exist (reviewers per area: hardware, protocols,
standards, data).
