# Observation (navigation concept)

`Observation` **is not a technical entity** in BioMesh — it's the question
that guides someone from "I want to measure X" to the right
standard/protocol/hardware.

## Why it's not a schema

The original version of the project proposed `Observation`, `Specimen`,
`Device` as a custom schema. That was dropped: standards already exist
that cover this better than anything BioMesh could invent from scratch
(see `standards/mappings/`).

- Is it an organism found at a place/time? → Darwin Core (`Occurrence` +
  `Event`).
- Is it a measurement within a plant phenotyping experiment? → MIAPPE
  (`Observation Unit`).
- Is it an instrument measurement with an associated calibration/protocol?
  → ISA, or the candidate in `standards/calibration/` if ISA falls short
  (see `standards/gaps/`).

## How this concept is used

When someone (or BioMesh's future interface, phase 3-4) asks "what do you
want to measure?", the answer doesn't create an `Observation` record — it
directs the person to the right standard and, from there, to the protocol
(`protocols/`) and compatible hardware (`hardware/`) documented in this
repo.
