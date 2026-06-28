# Adding a CAD drafting skill

This library holds many skills; each is a self-contained folder under `skills/`.

## 1. Create the skill folder

```
skills/<skill-name>/
├── SKILL.md          # required
└── instincts/        # optional — paired behavioral nudges
    └── <id>.md
```

## 2. Write SKILL.md

Start with YAML frontmatter, then the body:

```markdown
---
name: <skill-name>            # kebab-case, must match the folder name
description: <one line — when Claude should reach for this skill>
version: 1.0.0
---

# Title

Body: the conventions, rules, and workflows the skill teaches.
```

Keep `description` trigger-oriented ("Use when …") — that's what the model matches on.

## 3. (Optional) Add instincts

Instincts are tiny, always-on nudges for the continuous-learning system. One per file:

```markdown
---
id: <unique-id>
trigger: "when <situation>"
confidence: 0.8            # 0.0–1.0; back higher numbers with stronger evidence
domain: cad
source: <where it came from>
---

# Title

## Action
What to do.

## Evidence
Why — cite the file/spec/rule it came from so it's auditable.
```

Put a copy in both `skills/<skill-name>/instincts/` (ships with the skill) and the
top-level `instincts/` folder (so it's importable by raw URL).

## 4. Register it in the README

Add a row to the **Skills** table in `README.md`.

## 5. Bump the version

Increment `version` in `.claude-plugin/plugin.json` so co-workers' `/plugin update`
picks up the change.
