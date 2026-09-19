# Hardware

Three categories, based on who designed it:

- [external/](external/) — third-party hardware, documented (not
  manufactured or sold by BioMesh).
- [adapters/](adapters/) — integrations built by the project between
  existing hardware and the rest of the system (wiring, firmware, adapter
  PCBs).
- [open-hardware/](open-hardware/) — hardware designed by BioMesh from
  scratch. Used only when `external/` and `adapters/` don't solve the
  case.

## Mandatory template per component

Every hardware component, regardless of category, documents:

- **WHAT** — what does it measure?
- **WHY** — why is that measurement needed?
- **HOW** — how is it used/integrated?
- **VALIDATION** — how do we know it works?
- **LICENSE** — what can someone else do with this?
