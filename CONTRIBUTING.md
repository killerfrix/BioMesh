# Contributing to BioMesh

Thanks for your interest. The project is in phase 1 (the map) — the most
useful way to contribute right now is research and documentation, not code.

## Before proposing something new

Any contribution that adds a protocol, hardware, or standard must first
answer:

1. Does a solution for this already exist? (check `docs/ecosystem-map.md`
   and `standards/mappings/`)
2. If it exists, why isn't it enough to integrate or adapt it?
3. If you're proposing that something is a real gap, follow the process in
   `standards/gaps/` before creating a schema.

## Checklist for a new protocol

- What variable does it measure?
- Why is that measurement necessary?
- What unit and what precision/uncertainty does it have?
- What instrument is required?
- How is it calibrated?
- Under what environmental conditions is it valid?
- What's the step-by-step procedure?
- What common errors need to be avoided?
- What existing standard frames it (DwC / MIAPPE / ISA / none)?

## Checklist for new hardware

Every component in `hardware/` must document:

- **WHAT** — what does it measure?
- **WHY** — why is that measurement needed?
- **HOW** — how is it used/integrated?
- **VALIDATION** — how do we know it works? (comparison against a
  reference, repeatability, etc.)
- **LICENSE** — what can someone else do with this?

Before documenting third-party hardware (`hardware/external/`), make sure
you're not copying protected material (datasheets, images) without
permission — link to the source instead of copying it if in doubt.

## Issue types

Use the matching template: Bug, Hardware, Protocol, Calibration, Dataset,
Feature, Research, Documentation.

## Pull requests

Every PR must answer in its description:

- What changed?
- Why?
- Scientific justification (if applicable)?
- Does it affect existing hardware?
- Does it affect any data schema/mapping?
- Does it affect calibration?
- What license applies to the added content?
- How was it tested/verified?

## Language

All documentation is in English, to reach the widest possible audience of
contributors and to match the language used by the standards BioMesh
integrates (Darwin Core, MIAPPE, BrAPI, ISA).
