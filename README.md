# BioMesh

**Open, modular infrastructure for reproducible biodiversity measurement.**

Initial domains: botany, mycology, and ecology.

## The problem

Someone who wants to measure a biological trait — a plant's height, soil
moisture, a mushroom's morphology — has to figure out on their own which
data standard to use, what hardware is appropriate, how to calibrate it,
and what protocol to follow. Excellent solutions exist for parts of the
problem (FieldKit, ROMI, PlantCV, Darwin Core, MIAPPE, BrAPI, ISA...) but
they're fragmented: nobody connects them.

BioMesh doesn't solve this by replacing those pieces. It **indexes,
documents, and connects** them.

> BioMesh is like Linux, not a new standard. Linux didn't replace POSIX or
> TCP/IP — it integrated them under one roof, letting each standard remain
> the source of truth in its own domain.

BioMesh does not replace existing standards. BioMesh:

- **discovers** them (`docs/ecosystem-map.md`)
- **documents** them (`standards/mappings/`)
- **maps** them against each other (where they overlap, where the gaps are)
- **connects** them to real protocols and hardware (`protocols/`, `hardware/`)
- provides **practical examples** (`schemas/examples/`, illustrative,
  never a source of truth)
- **identifies gaps** explicitly before acting on them (`standards/gaps/`)
- develops **extensions only when the existing ecosystem proves they're
  needed**

## Philosophy

> Reuse → Integrate → Standardize → Validate → Improve → Invent only when necessary.

- Don't reinvent sensors, standards, or datasets that already exist.
- Don't create a new solution without first proving existing ones aren't
  enough.
- Don't create custom hardware before exhausting the option of integrating
  existing hardware.
- Don't create a custom data standard before proving existing ones can't
  represent the needed information.
- The first deliverable is not a PCB, a web app, or AI. **It's the map.**

## What BioMesh is NOT (yet)

- Not a web application.
- Not a final PCB.
- Not an AI/ML system.
- Not a general-purpose custom data schema (`Observation` / `Specimen` /
  `Device` are not implemented as technical entities — see
  [docs/concepts/observation.md](docs/concepts/observation.md)).
- Has no schema of its own as a source of truth. `schemas/` exists, but
  only as illustrative examples of how already-documented mappings connect
  — never as a "BioMesh Standard v1."

## Conceptual architecture

```
                    BIOMESH
                       │
        ┌──────────────┼──────────────┐
        │              │              │
    KNOWLEDGE       HARDWARE         DATA
        │              │              │
   protocols       external/       existing
   mappings        adapters/       standards
   calibration     open-hardware/  (DwC, MIAPPE,
        │              │            BrAPI, ISA)
        └──────────────┼──────────────┘
                       │
             BOTANY · MYCOLOGY · ECOLOGY
```

No gap is confirmed yet to justify a schema of its own. `standards/gaps/`
documents the process that confirms (or rules out) a gap before anything
is built on top of it. The first **candidate** — not a decision already
made — is **DIY environmental hardware calibration**
(`standards/calibration/`), because neither Darwin Core, MIAPPE, nor ISA
cover it in depth.

## Repository structure

```
BioMesh/
├── standards/
│   ├── mappings/         # DwC / MIAPPE / BrAPI / ISA — what each covers, when to use it
│   ├── gaps/             # process that confirms (or rules out) a gap before creating a schema
│   └── calibration/      # first gap candidate: DIY sensor/hardware calibration
├── schemas/               # illustrative examples only, never a source of truth
├── docs/
│   ├── ecosystem-map.md  # table of existing projects (FieldKit, ROMI, PlantCV...)
│   └── concepts/
│       └── observation.md
├── research/              # background research behind ecosystem-map and gaps/
├── protocols/
│   ├── botany/
│   ├── mycology/
│   ├── ecology/
│   └── general/
├── hardware/
│   ├── external/          # third-party hardware, documented
│   ├── adapters/          # integrations built by the project
│   └── open-hardware/     # hardware designed by the project
├── projects/
│   └── durango-pilot/     # first scientific project
└── .github/                # issue and PR templates
```

Deliberately **not created yet**: `firmware/`, `software/`, `datasets/` —
`CLAUDE.md` explicitly places them after protocols, hardware, calibration,
and templates; they get created when there's something real to put there,
not before.

## Roadmap

- **Phase 1 — the map** (where we are now): standard mappings, ecosystem
  map, protocols, documented hardware catalog.
- **Phase 2 — first hardware**: ESP32 + microclimate sensor → CSV/JSON, no
  PCB.
- **Phase 3 — dataset**: Durango Biodiversity Pilot, first reproducible
  dataset.
- **Phase 4 — interoperability**: exposure via BrAPI or other APIs,
  conversion/validation tools.
- **Phase 5+**: custom hardware only for proven gaps, commercial services
  (kits, calibration, support).

## First scientific project: Durango Biodiversity Pilot

See [projects/durango-pilot/README.md](projects/durango-pilot/README.md).

## Model

Everything open stays open: documentation, protocols, designs, firmware,
software, open datasets. The commercial layer is the service (assembled
kits, calibration, installation, support, analysis) — a FieldKit-type
model.

## Licenses

- Code: [MIT](LICENSE)
- Documentation, protocols, and mappings: [CC BY 4.0](LICENSE-DOCS.md)
- Custom hardware: decided per component once the first design exists
  (candidate: CERN-OHL family)
- Third-party hardware/software referenced in `hardware/external/`: keeps
  its own license, documented in each entry.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) and [GOVERNANCE.md](GOVERNANCE.md).
