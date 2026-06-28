---
id: cad-toolchain-python-scaffold-style
trigger: "when writing or extending a Python script in cad-toolchain"
confidence: 0.8
domain: python
source: local-codebase-analysis
---

# Match the Toolchain's Script Scaffold Style

## Action
- Start with `#!/usr/bin/env python3` and a module docstring; for stubs, include a
  `Next step:` line describing the intended `ezdxf` + rule-engine integration.
- Type geometry as `Point = Tuple[float, float]`; model inputs as `@dataclass` with
  unit comments (`# map units`, `# corridor width`).
- Add an `if __name__ == "__main__":` block that demos each function with labeled prints,
  and keep the matching `tests/*.txt` fixture in sync with that output.
- Write generated artifacts to `outputs/` resolved via
  `Path(__file__).resolve().parents[1] / "outputs"` with `mkdir(parents=True, exist_ok=True)`
  — never write in place.

## Evidence
- All three scripts share the shebang + docstring pattern; stubs carry "Next step:" notes
  and emit `{"status": "stub"}` payloads.
- `generate_dxf_stub.py` resolves output via `parents[1] / "outputs"` and `mkdir(exist_ok=True)`.
- `tests/geometry_intelligence_sample.txt` mirrors the `__main__` printed output.
