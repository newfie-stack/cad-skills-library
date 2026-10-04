# Execution protocol and templates

Read this before a Counsel run. This protocol works with actual worker/subagent tools; prose labels alone do not implement it.

## Shared brief template

- Decision / mode / decision deadline:
- Objective / success criteria:
- Options, including status quo:
- Facts with source IDs and verification dates:
- Inferences and their supporting facts:
- Assumptions:
- Unknowns and decision impact:
- Resources / constraints / dependencies:
- Authority already granted and actions requiring approval:
- Reversibility / safety boundaries:

Prepare the brief once. Store or otherwise retain the same brief for all five workers. Avoid inherited conversation that contains other first-pass outputs. All roles get the same essential facts; do not strip facts from the Outsider's copy.

## First-pass worker prompt

> Assess only the attached decision brief through the assigned lens: [one of the five lenses, with its instructions from SKILL.md]. You have not been given the other advisors' findings. Give a position, strongest decision-relevant finding, concise evidence-backed explanation with source IDs, uncertainty that could change it, and a proposed next action. Separate facts, inferences, assumptions, and unknowns. Do not invent disagreement, claim access to missing evidence, or perform consequential actions. Identify material evidence gaps and return findings for review.

Use five real isolated contexts. Record which workers actually completed. With limited capacity, collect isolated first passes sequentially without passing previous findings to subsequent workers. If separation cannot be achieved, use the limitation fallback in SKILL.md rather than representing a simulation as this protocol.

## Cross-review packet

1. Wait for all five first passes. Keep the originals and a private author map.
2. Create review copies. Remove role names, worker IDs, author headings, and stock role catchphrases. Preserve substantive arguments, caveats, and source IDs; do not sanitize away disagreement.
3. Shuffle copies and assign labels A–E. Keep the mapping out of reviewer inputs. Labels must not mechanically correspond to the fixed role order.
4. Give each advisor the four other labeled cases plus the common brief. The reviewer may retain its own first-pass context, so it may recognize its own perspective or infer another's role. Explicitly treat this as limited, label-anonymized peer review.
5. Collect all five reviews before synthesis. Do not feed earlier reviews to later reviewers as consensus cues.

Review prompt:

> Review these four labeled cases against the common decision brief. Their explicit author labels are withheld, but their lenses may be inferable. Evaluate evidence and reasoning, not guesses about authorship. Identify the strongest supported argument, the most consequential unsupported premise or blind spot, and the material disagreement or justified convergence. Cite response labels and source IDs. State whether any challenge changes your initial position and what correction or new evidence is needed. No vote counting or forced dissent.

After reviews, request concise corrections from affected advisors. Material new evidence must be shared equally; materially revised conclusions need another cross-review before a final ruling. Keep minor wording corrections separate from substantive changes. Report an incomplete stage as incomplete.

The coordinator can author the Chairman's synthesis after reviewing the actual outputs. It should cite decisive sources, identify shared-source dependence, and explain why stronger evidence defeats a weaker majority.

## User-facing output template

Adapt headings to the channel. Preserve the content rather than enforcing Markdown where the channel does not support it.

- Question counselled: [neutral decision]
- Material assumptions / unknowns: [only those that affect interpretation]
- Process: [five isolated first passes completed; label-anonymized cross-review completed; same-model/shared-evidence and role-inference limits as applicable]
- Five advisors: [one concise finding each: Contrarian, First Principles, Expansionist, Outsider, Executor]
- Cross-review: strongest argument; biggest blind spot; key disagreement or supported convergence
- Chairman's Verdict: agreement; clash; blind spots; recommendation and why; reversal evidence; next action with metric and justified timeframe; confidence with reason

Full mode can use the familiar `// QUESTION COUNCILLED`, `// THE FIVE ADVISORS`, `// PEER REVIEW HIGHLIGHTS`, and `// THE CHAIRMAN'S VERDICT` headings. Fast and pressure-test modes keep every role and the review, but compress the findings. Do not overwhelm the user with raw worker logs or private reasoning.

## Completion check

- All five actual first passes used the same brief and no peer outputs.
- All five actual cross-reviews evaluated the other cases with explicit author metadata withheld.
- Corrections, new facts, and incomplete stages are accurately represented.
- Sources support the claims; shared evidence has not become five votes of confidence.
- The Chairman has a decisive recommendation or clear blocker, a falsifiable next step, justified timing, and confidence with a reason.
- Advice is distinguished from authorization, implementation, testing, and acceptance.
