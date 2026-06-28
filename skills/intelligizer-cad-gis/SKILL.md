---
name: intelligizer-cad-gis
description: Alberta survey CAD-to-GIS drafting automation guidance for converting unintelligent DWG linework into intelligent features/object-data-ready outputs. Use when tasks involve section evidence labeling, bearings/distances, road allowances/plans, land-status labels, hydrology, low areas, radius circles, and shapefile prep from AutoCAD Map 3D/Civil 3D workflows.
---

Use this skill to produce practical, standards-aligned CAD/GIS automation plans.

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
- Restore baseline from `Projects/customgpt-migration/optimizer/runs/iteration-018-config.json` baseline block or prior VCS snapshot.

## Workflow
1. Ask for objective, input artifacts, and target outputs.
2. Confirm assumptions and unknowns before giving rules.
3. Produce a rule-based feature classification plan.
4. Produce object data mapping and labeling logic.
5. Provide QA checklist for export readiness.

## Output format
- Assumptions
- Feature rules
- Object-data schema mapping
- Labeling logic
- QA checks
- Next action

## Guardrails
- Do not invent legal/survey facts.
- Separate confirmed facts from inferred suggestions.
- Use uploaded files only for extraction; do not mention file names.

Read `references/evidence-rules.md` when evidence symbol mapping is required.
