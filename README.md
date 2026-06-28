# CAD Skills Library

A shareable library of **CAD drafting skills** for [Claude Code](https://claude.com/claude-code).
It packages domain conventions for Crown / cadastral land-survey toolchains — geometry
intelligence, DXF generation, layer/ObjectData standards, and package validation — as
installable Claude Code skills plus importable "instincts".

Distributed as a self-hosting Claude Code plugin marketplace, so installing is the same
flow as any other plugin.

## Install (co-workers)

```
/plugin marketplace add https://github.com/newfie-stack/cad-skills-library
/plugin install cad-drafting@cad-skills
/reload-plugins
```

Once installed, the skills auto-load and can be invoked by name (e.g. the model will pull
in `cad-toolchain-patterns` when working in a matching project).

### Optional: import the instincts

Skills are loaded automatically; **instincts** (lightweight, always-on behavioral nudges
for the continuous-learning system) are imported separately. They can be imported straight
from raw GitHub URLs:

```
/instinct-import https://raw.githubusercontent.com/newfie-stack/cad-skills-library/main/instincts/cad-surveyed-control-preferred.md --scope global
```

…or clone the repo and import the whole `instincts/` folder file-by-file.

## What's inside

```
.
├── .claude-plugin/
│   ├── marketplace.json   # makes this repo its own plugin marketplace
│   └── plugin.json        # the cad-drafting plugin manifest
├── skills/                # one folder per skill (auto-loaded when installed)
│   └── cad-toolchain-patterns/
│       ├── SKILL.md
│       └── instincts/     # instincts that pair with this skill
└── instincts/             # all instincts aggregated for easy URL import
```

## Skills

| Skill | What it covers |
|---|---|
| `cad-toolchain-patterns` | Crown cadastral toolchain conventions: schema-first layer/ObjectData definitions, geometry rules (townships→squares, pipelines→corridors, surveyed boundary control preferred), closed clockwise rings, and Python scaffold style. |

_More CAD drafting skills go here as the library grows — see [CONTRIBUTING.md](./CONTRIBUTING.md)._
