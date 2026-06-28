---
name: cad-toolchain-patterns
description: Conventions for the Crown cadastral CAD toolchain — layer/ObjectData schema, geometry intelligence rules, and Python scaffold style. Use when editing or extending Projects/cad-toolchain (DXF generation, package validation, geometry helpers).
version: 1.0.0
source: local-codebase-analysis
analyzed_path: Projects/cad-toolchain
---

# CAD Toolchain Patterns

A small Python toolchain that turns survey specs into validated CAD packages for
Crown / cadastral land drafting. Most modules are intentionally **stubs** scaffolded
toward an `ezdxf` + rule-engine implementation — match the existing conventions when
filling them in.

> Note: extracted from the codebase itself (not git history — the project is tracked
> under the parent workspace with no per-project commits). Treat the rules below as the
> source of truth, and keep `specs/layer-objectdata-schema-v1.yaml` authoritative when
> they ever disagree.

## Project Layout

```
Projects/cad-toolchain/
├── specs/      # YAML schema = source of truth for layers, attributes, rules
├── scripts/    # Python: geometry helpers + DXF/validation generators
├── outputs/    # Generated artifacts (e.g. draft-scaffold.json)
└── tests/      # Sample expected-output fixtures (plain .txt for now)
```

## Schema Is the Source of Truth

`specs/layer-objectdata-schema-v1.yaml` defines every layer, its geometry type, its
required attributes, and the validation rules. **Add a layer/attribute/rule here first,**
then make code conform — never hard-code a layer set that drifts from the schema.

- Layer names are `UPPERCASE` (`BOUNDARY`, `EVIDENCE`, `ROAD`, `HYDRO`, `LAND_STATUS`).
- Attribute names are `UPPER_SNAKE` (`DISP_TYPE`, `WIDTH_M`, `UNIQUE_ID`).
- Each layer declares one `geometry`: `polygon` | `line` | `point`.
- Rules are `R0NN` with a one-line `description`. Current rules:
  - **R001** boundary polygons must be closed and non-self-intersecting
  - **R002** all required attributes present per layer
  - **R003** labels generated for evidence/road metrics where applicable
  - **R004** township footprints normalized to square geometry
  - **R005** pipeline corridors **prefer surveyed south/west boundary control**; centerline is fallback only
  - **R006** township geometry should honor surveyed south/west boundary control where available

## Geometry Intelligence Conventions

In `scripts/geometry_intelligence.py`. The domain rules matter as much as the math:

- **Surveyed boundary control is preferred; centerline is a fallback.** Where a function
  has both a surveyed-boundary form and a centerline form (e.g.
  `make_pipeline_from_surveyed_boundaries` vs `make_pipeline_rectangle`), the surveyed
  one is canonical — flag the legacy form with a `# legacy fallback` comment, as the
  existing `PipelineSpec` does.
- **Townships → squares** (`make_square`), **pipelines → rectangular corridors**.
- **Rings are closed and clockwise**: return the first vertex again as the last element
  so the polygon is explicitly closed.
- **Right-hand normal convention**: the unit normal `(-dy/length, dx/length)` of the
  SW→SE south boundary points to the north side. Keep this orientation when adding
  offset geometry.
- **Reject degenerate input** with `raise ValueError(...)` (e.g. identical/zero-length
  boundary points) rather than returning a malformed ring.

## Python Style

Match the existing scripts:

- `#!/usr/bin/env python3` shebang + a module docstring stating what the script does
  (and, for stubs, the **"Next step:"** toward real implementation).
- Typed geometry primitives: `Point = Tuple[float, float]`; specs as `@dataclass` with
  unit comments (`# map units`, `# corridor width`).
- Type-hinted signatures returning `List[Point]`.
- A `if __name__ == "__main__":` block that demos each function with printed,
  labeled output — these double as the fixtures checked into `tests/*.txt`.
- File outputs go to `outputs/` resolved via
  `Path(__file__).resolve().parents[1] / "outputs"` with `mkdir(parents=True, exist_ok=True)`.

## Stub → Implementation Workflow

Scaffolds carry their own roadmap; honor it instead of rewriting wholesale:

- Generators emit a payload with `"status": "stub"` and a `"note"` describing the next
  integration step (e.g. *"integrate ezdxf + rule engine"*).
- `ezdxf` is the intended DXF backend (currently optional/not wired).
- `validate_package_stub.py` is the home for: closed-polygon checks (R001), required-attr
  enforcement (R002), and naming-convention checks — implement geometry + schema
  validation there, driven by the YAML schema.

## When Extending

1. Edit `specs/layer-objectdata-schema-v1.yaml` first for any new layer/attribute/rule.
2. Implement against the schema; keep geometry closed/clockwise and prefer surveyed control.
3. Update the `__main__` demo and refresh the matching `tests/*.txt` fixture.
4. Write generated artifacts to `outputs/`, not in-place.
