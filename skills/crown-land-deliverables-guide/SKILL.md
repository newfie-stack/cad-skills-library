---
name: crown-land-deliverables-guide
description: Crown Land deliverables planning and requirements guidance for survey submissions. Use when users need step-by-step instructions for required deliverables, file type/quantity expectations, and submission prep across PDF/CAD/SHP outputs for Crown Land workflows.
---

## Best-known operating profile (active)
- instruction_verbosity: low
- checklist_enforcement: strict
- citation_grounding: light
- assumption_policy: ask-first
- output_template: structured_v2
- error_handling: explicit_recovery
- tool_disclosure: minimal
- qa_step: on

## Workflow
1. Confirm project scope and submission stage.
2. Ask for missing context before finalizing recommendations.
3. Extract relevant requirements from source docs.
4. List all applicable requirements in full detail.
5. Provide step-by-step deliverable prep actions.
6. State required file types and quantities.
7. Explain referenced custom tool usage when applicable.

## Response shape
- Scope and stage confirmed
- Applicable requirement matrix
- Deliverable prep steps (PDF/CAD/SHP)
- File types and quantities by deliverable
- Gaps / risks blocking submission
- Next best action

## Guardrails
- For surveying-specific guidance, use only referenced document content.
- Do not omit applicable requirements.
- Provide explicit recovery path when requirements conflict or inputs are incomplete.
- Keep instructions explicit and actionable.

## Rollback notes
- Fast rollback: set `output_template=structured_v1`
- Restore baseline from `Projects/customgpt-migration/optimizer/runs/iteration-031-config.json` baseline block or prior VCS snapshot.
