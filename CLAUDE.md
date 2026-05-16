# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

`sabu` is a personal harness — a collection of **skills** (capability-shaped prompts) that local AI agents can use. It is not an application. There is no build step, no test suite, no linter, no package manager — do not invent commands that don't exist here.

Currently, installation is manual: clone the repo, then run the setup script to link the skills into the expected locations. In the future, this may be automated or integrated with npm or a package manager.

```sh
./setup.sh
```

It is idempotent. Run it after adding, removing, or renaming a skill.

## Skill shape

Every skill lives at `skills/<name>/` and must contain a `SKILL.md` file. SKILL.md uses YAML frontmatter:

```yaml
---
name: <kebab-case-name> # must match the directory name
description: <one-line summary> # used by agents to decide when to load it
disable-model-invocation: true # optional; prevents auto-trigger
---
```

Supporting files live alongside `SKILL.md` in the same directory (e.g. `marshal/triage-labels.md`, `tdd/refactoring.md`). The skill body references them by relative path; agents only read them when the skill instructs them to.

Skills cross-reference each other by name (e.g. `marshal` mentions `to-issues`, `triage`, `tdd`, `diagnose`). Renaming a skill silently breaks those references — grep before renaming.

## Distribution model (what setup.sh does)

Two destinations, two patterns:

1. **`~/.agents/skills`** — a single parent symlink pointing at this repo's `skills/`. Tools that follow the AGENTS.md convention pick up everything under `skills/` automatically. If `~/.agents` is itself a symlink (e.g. managed by stow), setup bails so the user can decide.
2. **`~/.claude/skills/<name>`** — one symlink per skill. Claude Code discovers user-level skills by enumerating this directory, so each skill needs its own entry.

`setup.sh` reports new symlinks, replaced symlinks (target moved), skipped real directories (won't clobber), and dangling symlinks (point at non-existent paths — usually leftovers from a renamed/removed skill; remove manually).

## Adding a new skill

1. Create `skills/<name>/SKILL.md` with the frontmatter above.
2. Add any supporting files in the same directory.
3. Run `./setup.sh` — it will print `linked   ~/.claude/skills/<name>`.
