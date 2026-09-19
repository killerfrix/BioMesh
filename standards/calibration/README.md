# DIY hardware calibration (first gap candidate)

See the full process in [../gaps/README.md](../gaps/README.md).

**Status: Hypothesis.** This is currently the leading hypothesis under
investigation and is not a confirmed gap — neither Darwin Core, nor
MIAPPE, nor ISA (though ISA is the closest) address DIY environmental
sensor/hardware calibration in depth, but that hasn't been fully confirmed
against ISA yet. Don't create a schema yet — first confirm in
`standards/mappings/isa.md` how far ISA actually goes before inventing
something new.

## What it must eventually be able to answer

- Reference instrument used for calibration
- Calibration procedure
- Environmental conditions during calibration
- Date
- Operator
- Calibration data (curve, offset, etc.)
- Uncertainty
- Calibration ID (so a dataset can reference `calibration_id`)

## Why it matters

Without this, every BioMesh dataset has the typical DIY hardware problem:
"sensor plugged in → number," with no way to know if that number is
reliable or to reproduce the measurement. Any dataset schema that wants to
reference a `protocol_version` or `calibration_id` needs something for
those references to point to — neither currently has a schema of its own.
This is where that would get resolved, if the gap is confirmed.
