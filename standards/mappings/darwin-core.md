# Darwin Core (DwC)

**Status: draft v1. Covers the core classes and a proposed mapping to MIAPPE's
Observation Unit. The mapping has not yet been tested against a real dataset
or reviewed by a Darwin Core/MIAPPE practitioner.**

## What it is

Darwin Core is a standard **vocabulary** for biodiversity data, maintained by
[TDWG](https://www.tdwg.org/) (Biodiversity Information Standards). It gives a
shared list of terms (like `scientificName`, `eventDate`, `decimalLatitude`),
grouped into classes, each with a clear definition and sometimes a recommended
format (e.g. ISO 8601 dates: `2026-10-05`).

If everyone labels their data with the same terms, datasets from different
people, CSVs or databases can be combined, for example in
[GBIF](https://www.gbif.org/).

Darwin Core does **not** define a database or run a project. It defines what to
call things and what each name means. Its main exchange format is the Darwin
Core Archive (CSV files plus a `meta.xml` descriptor).

## What it covers

The four main classes (others exist, like `Organism`, `Identification`,
`MaterialSample` and `MeasurementOrFact`):

| Class | Answers | Definition |
|---|---|---|
| `Occurrence` | *What was recorded?* | Evidence that an organism was present (or absent, via `occurrenceStatus`) at a place and time: an observation, a specimen, a photo, a sound recording. Dead organisms count. |
| `Event` | *What action was done, when and how?* | An action at a place and time, usually a sampling action (a survey, a transect, a trap check). Events can nest via `parentEventID`: a field trip → each sampling stop. |
| `Taxon` | *What is it?* | The named group the organism belongs to (species, genus…), with its `scientificName` and classification. Who identified it and when is recorded separately (`Identification`), because identifications can change. |
| `Location` | *Where?* | Coordinates with their uncertainty (`coordinateUncertaintyInMeters`), country, state, locality description, elevation. |

**How they connect:** an `Event` happens at a `Location` and produces zero or
more `Occurrence`s, each linked to a `Taxon`. In a flat CSV these classes are
not separate tables. One row can hold terms from all of them.

**Measurements are a small part of Darwin Core.** Most terms describe *what,
where, when and who*. Measured values (height, cap diameter, temperature) go in
the `MeasurementOrFact` class/extension. This matters for BioMesh, since sensor
data is where Darwin Core is weakest. Whether ISA covers instrument and
calibration metadata instead is the open question tracked in
[`standards/calibration/`](../calibration/README.md) (a hypothesis, see
[`standards/gaps/`](../gaps/README.md)).

### Required terms

Darwin Core itself makes **no term mandatory**. GBIF sets the minimum for
occurrence datasets: `occurrenceID`, `basisOfRecord` (e.g. `HumanObservation`,
`PreservedSpecimen`), `scientificName` and `eventDate`.

### Identifiers

Darwin Core does **not** assign identifiers. `eventID`, `occurrenceID`,
`organismID` and `locationID` are fields BioMesh must fill itself, with values
that are unique and stable (e.g. UUIDs, or a readable pattern such as the
`BM-...` IDs in the example below). The identifier scheme is a **proposal**,
not yet decided.

## When to use it

When the data to record is fundamentally *"we found this organism at this place
at this time"*: the natural unit for the
[Durango pilot](../../projects/durango-pilot/README.md) (botany/mycology). It
gives direct compatibility with GBIF.

## Relationship to other standards

### MIAPPE

[MIAPPE](https://www.miappe.org/) (Minimum Information About a Plant
Phenotyping Experiment, see [miappe.md](miappe.md)) is a standard for plant
phenotyping data, meaning measurements of observable plant traits like height,
leaf area or yield. It is a checklist of the minimum information needed to make
an experiment FAIR (Findable, Accessible, Interoperable, Reusable), plus a data
model: Investigation → Study → Observation Unit, with Biological Material,
Environment, Experimental Factors and Observed Variables (trait + method +
scale). It has no file format of its own; it is implemented through ISA-Tab,
BrAPI or JSON.

- **Darwin Core** records *that an organism occurred somewhere*.
- **MIAPPE** records *how plants were measured and under what conditions*.

They are complementary and overlap on *where, when and which organism*, so
MIAPPE data can be partially expressed in Darwin Core terms (see the gaps
below).

#### The Observation Unit

A MIAPPE **Observation Unit (OU)** is the entity on which Observed Variables
are measured: a plant, a pot or a plot. OUs have levels that can nest
(field → block → plot → plant), each with its own ID, and each is linked to its
Biological Material and Experimental Factor values. A **Sample** is a part taken
from an OU (e.g. a leaf for lab analysis).

**Key point:** an OU **persists over time** and is usually measured repeatedly.
A Darwin Core `Event` is tied to a single place and time. So the OU does
**not** map to an `Event`:

- a **plant** OU → `Organism` (`organismID`)
- a **plot** OU → `Location` (`locationID`)

Each measurement session is an `Event`. Each time the plant is recorded in a
session, that is an `Occurrence` carrying the same `organismID`, which links
all sessions back to the one OU.

#### Mapping table (proposed)

| MIAPPE | Darwin Core | Example |
|---|---|---|
| Study | Parent `Event` | "Growth study, Oct–Nov 2026" |
| OU (plant) | `Organism` (`organismID`) | Pine seedling #1, one ID for 2 months |
| OU (plot) | `Location` (`locationID`) | Plot A |
| Each measurement session | Child `Event` (`eventID`, `eventDate`, `parentEventID`) | 8 events, one per week |
| The plant recorded in a session | `Occurrence`, linked by `organismID` | 8 occurrences, all pointing to seedling #1 |
| Observed Variable + value (trait + method + scale) | `MeasurementOrFact` (`measurementType`, `measurementMethod`, `measurementUnit`, `measurementValue`), attached to each `Occurrence` | height, ruler soil-to-top, cm, 23 |
| Biological Material (species) | `Taxon` (`scientificName`) | *Pinus durangensis* |
| Sample | `MaterialSample` / `MaterialEntity` | a branch sent to the lab |
| Experimental Factors, genotype details | **No clean equivalent** | "low water" treatment: candidate gap |

For plot-level values (e.g. yield per plot, % ground cover), `MeasurementOrFact`
attaches to the `Event` instead of an `Occurrence`. Individual plants inside a
plot can still get their own `Occurrence`s.

**Archive layout caveat:** in a sampling-event Darwin Core Archive (Event core
with an Occurrence extension), the standard `MeasurementOrFact` extension can
only link to the core record, i.e. the `Event`, not to a specific
`Occurrence`. Attaching measurements to each `Occurrence` as above requires
either an Occurrence-core archive or the **Extended MeasurementOrFact (eMoF)**
extension, which carries an `occurrenceID` column.

#### Worked example (one week)

*Hypothetical example to illustrate the mapping. It is not the Durango pilot's
sampling design, which has not been defined yet.*

```
Event (parent)       eventID=BM-STUDY-2026-01   "Growth study, Oct–Nov 2026"
└─ Event (child)     eventID=BM-STUDY-2026-01-w1  eventDate=2026-10-05
                     parentEventID=BM-STUDY-2026-01  locationID=BM-PLOT-A
   └─ Occurrence     occurrenceID=BM-OCC-0001  organismID=BM-ORG-SEEDLING-01
                     scientificName=Pinus durangensis  basisOfRecord=HumanObservation
      └─ MeasurementOrFact  measurementType=height
                            measurementMethod=ruler, soil to top
                            measurementUnit=cm  measurementValue=23
```

Weeks 2–8 repeat the child `Event` → `Occurrence` → `MeasurementOrFact` chain
with new `eventID`/`occurrenceID` values and the **same** `organismID`.

#### Candidate gaps (lossy mapping)

These MIAPPE concepts have no clean home in core Darwin Core. They are
**candidates**, not confirmed gaps: each must go through the process in
[`standards/gaps/README.md`](../gaps/README.md) before anything new is
proposed.

- **Experimental Factors** (treatments like "low water"). TODO: check whether
  TDWG's Humboldt Extension (ecological inventories / sampling design) covers
  this before treating it as a gap.
- **Genotype / accession details** of the Biological Material.
- **Ontology-based trait definitions** (e.g. Crop Ontology trait IDs). Likely
  a partial gap at most: eMoF's `measurementTypeID` can hold an ontology URI.

### Location vs a reusable `Site`

Repeated sampling at the same physical place can share one `locationID`, so
events *can* point to the same site. However, in a standard Darwin Core Archive,
location terms are repeated on every event/occurrence row; there is no separate
Location table. Whether BioMesh needs a first-class `Site` entity on top of
this is an open question (hypothesis, not a decision).

- TODO: decide on `Site` handling once the Durango pilot's sampling design is known.

## References

- [Darwin Core home (TDWG)](https://dwc.tdwg.org/)
- [Darwin Core Quick Reference Guide](https://dwc.tdwg.org/terms/)
- [Darwin Core list of terms](https://dwc.tdwg.org/list/)
- [GBIF data quality requirements: occurrence datasets](https://www.gbif.org/data-quality-requirements-occurrences)
- [MIAPPE](https://www.miappe.org/)
- [MIAPPE specification (GitHub)](https://github.com/MIAPPE/MIAPPE)
