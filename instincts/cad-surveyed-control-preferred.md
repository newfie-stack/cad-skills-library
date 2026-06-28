---
id: cad-toolchain-surveyed-control-preferred
trigger: "when generating pipeline or township geometry in cad-toolchain"
confidence: 0.9
domain: cad
source: local-codebase-analysis
---

# Prefer Surveyed Boundary Control; Centerline Is Fallback

## Action
Drive geometry from surveyed south/west boundary control when available. Use centerline
(or other approximate) inputs only as an explicit fallback, and mark the fallback path
with a `# legacy fallback` comment. For the same feature, the surveyed-boundary function
is canonical.

## Evidence
- Schema rules R005 and R006 state pipeline corridors and township geometry should prefer
  surveyed south/west boundary control, with centerline as fallback only.
- `geometry_intelligence.py` pairs `make_pipeline_from_surveyed_boundaries` (preferred)
  with `make_pipeline_rectangle` (commented "legacy fallback").
