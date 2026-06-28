---
id: cad-toolchain-schema-first
trigger: "when adding or changing a CAD layer, attribute, or validation rule in cad-toolchain"
confidence: 0.85
domain: cad
source: local-codebase-analysis
---

# Edit the Schema Before the Code

## Action
Add or modify the layer, required attribute, or rule in
`specs/layer-objectdata-schema-v1.yaml` first, then make scripts conform to it.
Never hard-code a layer list or attribute set in Python that can drift from the schema.

## Evidence
- The YAML schema enumerates all 5 layers, their geometry types, required attributes,
  and rules R001–R006 — it is structured as the single source of truth.
- `generate_dxf_stub.py` duplicates the layer list inline; that duplication is the kind
  of drift to drive out by reading from the schema.
