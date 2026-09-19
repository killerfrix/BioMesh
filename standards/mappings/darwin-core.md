# Darwin Core (DwC)

**Status: pending full development — this is a starting point.**

## What it covers

Resolves `Occurrence` (an observation event of an organism) vs `Taxon` vs
`Event` (a site visit) vs `Location`. It's the base for everything related
to occurrences and taxonomy.

## When to use it

When the data to record is fundamentally "we found this organism at this
place at this time" — the natural unit for the Durango pilot
(botany/mycology). Gives direct compatibility with GBIF.

## Relationship to other standards

- TODO: how `Event`/`Occurrence` relates to MIAPPE's `Observation Unit`.
- TODO: where DwC's `Location` fits against the need for a reusable `Site`
  entity — repeated sampling events at the same physical location
  currently have no first-class way to share one.

## References

- TODO: link to the official Darwin Core specification.
