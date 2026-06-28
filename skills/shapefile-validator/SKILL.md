---
name: shapefile-validator
description: Validate and assemble Alberta Crown land submission packages (MSL renewals, wellsites, pipelines, access roads). Use when cross-checking DWG/PDF/shapefile consistency, schema/projection/topology validation, controlled auto-corrections, and submission ZIP readiness for AER/AEP OneStop workflows.
---

Run compliance-first validation with explicit pass/fail and correction options.

## Active optimization profile (best-known)
- instruction_verbosity: low
- checklist_enforcement: strict
- citation_grounding: strict
- assumption_policy: ask-first
- output_template: structured_v2
- error_handling: explicit_recovery
- tool_disclosure: minimal
- qa_step: on

## Rollback notes
- Fast rollback: set `citation_grounding=light`
- Restore baseline from `Projects/customgpt-migration/optimizer/runs/iteration-017-config.json` baseline block or prior VCS snapshot.

## Workflow
1. Collect available inputs (DWG, PDF, SHP set, optional ATS grid).
2. Validate geometry/topology/projection/schema requirements.
3. Cross-verify key metadata across DWG/PDF/SHP.
4. Propose corrections and request user approval before applying.
5. Produce final checklist and packaging recommendation.

## Validation targets
- Required fields (example): DISP_TYPE, SCALE_FAC, CAP_METHOD, UNIQUE_ID
- Projection: UTM NAD83 (CSRS)
- Topology: closed polygons, clean geometry

## Guardrails
- Never silently fix data.
- Pause when inputs are missing.
- Do not claim compliance when critical checks fail.

Read `references/validation-checklist.md` for standard output checklist format.
