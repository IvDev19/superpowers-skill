# superpowers-skill

Installable personal skill for [Claude Code AI](https://claude.ai/code) that bootstraps the [superpowers skill library](https://github.com/IvDev19/superpowers-IvDev19).

## What this is

This repo is a single installable skill — the bootstrap entry point for IvDev19's superpowers library (v5.1.1). Installing it makes Claude aware of 14 workflow skills (TDD, debugging, brainstorming, code review, planning, and more) and teaches it when and how to invoke them.

The 14 skill implementations live in the canonical library: [IvDev19/superpowers-IvDev19](https://github.com/IvDev19/superpowers-IvDev19). This repo does not duplicate them.

## Installation

In Claude Code AI: **Settings → Skills → Add from GitHub**, then paste:

`https://github.com/IvDev19/superpowers-skill`

## Usage modes

**With the full plugin installed** (`IvDev19/superpowers-IvDev19`): The bootstrap skill triggers automatically, and all 14 library skills are available via the Skill tool.

**Standalone**: The bootstrap loads on its own. When a skill is needed, Claude fetches its content on demand from `superpowers-IvDev19` via WebFetch. See `references/skill-library.md` for the full URL index.

## Contents

| File | Purpose |
|------|---------|
| `SKILL.md` | Root bootstrap — triggers at session start, routes to the right skill |
| `references/copilot-tools.md` | Tool name mapping for non-Claude-Code environments |
| `references/skill-library.md` | 14 skill names and direct GitHub raw URLs for standalone fetch |

## License

MIT — see [LICENSE](LICENSE).
