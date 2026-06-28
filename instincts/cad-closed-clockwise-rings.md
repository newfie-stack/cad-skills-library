---
id: cad-toolchain-closed-clockwise-rings
trigger: "when returning polygon geometry from a cad-toolchain geometry function"
confidence: 0.85
domain: cad
source: local-codebase-analysis
---

# Return Closed, Clockwise Rings; Reject Degenerate Input

## Action
Return polygon vertices as a closed clockwise ring — repeat the first vertex as the last
element so closure is explicit. Use the right-hand normal `(-dy/length, dx/length)` of the
SW→SE south boundary to define the north side. Raise `ValueError` on degenerate input
(identical points / zero length) instead of returning a malformed ring.

## Evidence
- `make_square`, `make_pipeline_rectangle`, and `make_pipeline_from_surveyed_boundaries`
  all return rings whose last point equals the first.
- The pipeline functions raise `ValueError` when boundary length is zero.
- Schema rule R001 requires boundary polygons to be closed and non-self-intersecting.
