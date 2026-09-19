# Standards mappings

This is the first real technical content in BioMesh.

For each relevant existing standard for biodiversity/phenotyping, a
document that answers:

- **What it covers** (which entities/concepts it models)
- **When to use it** (for what kind of data/observation it's the source of
  truth)
- **How it relates to the other standards** (where there's overlap, where
  the gaps are)

## Standards to document

| Standard | File | Status |
|---|---|---|
| Darwin Core | [darwin-core.md](darwin-core.md) | pending |
| MIAPPE | [miappe.md](miappe.md) | pending |
| BrAPI | [brapi.md](brapi.md) | pending |
| ISA (Investigation-Study-Assay) | [isa.md](isa.md) | pending |

## Rule

No custom BioMesh schema is created while an existing standard covers the
case. If nothing covers a real case, the gap is documented and confirmed
in `standards/gaps/` before proposing anything new.
