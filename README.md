# Sabu

Sabu is the harness — a collection of skills, rules, and conventions I use with AI coding agents (primarily Claude Code) so they understand how I work and what I expect.

The name is from Chacha Chaudhary, the Indian comic series. Chacha is the brain ("Chacha Chaudhary ka dimaag computer se bhi tez chalta hai" — Chacha's brain works faster than a computer); Sabu is the loyal, super-strong sidekick from Jupiter who handles the heavy lifting once Chacha decides what to do. That's the model: I'm the thinker, Sabu is the agent that executes.

## What's in here

- **`skills/`** — a collection of skills (capability-shaped prompts) the agent can pick up and run. Each one is a SKILL.md plus optional supporting files. The skills live by themselves so they can be invoked individually (`/marshal`, `/triage`, etc.) and read each other for cross-reference.

The skills currently cover, roughly:

- **Project setup** — `marshal` (lays the rails: CLAUDE.md/AGENTS.md coherence, issue tracker, triage labels, domain doc layout, code style, version control conventions).
- **Issue workflow** — `triage` (state machine for incoming issues), `to-issues` (break a plan into tickets), `to-prd` (turn a conversation into a PRD).
- **Implementation discipline** — `tdd` (red-green-refactor), `diagnose` (disciplined debugging loop), `improve-codebase-architecture` (find deepening opportunities).
- **Design / collaboration** — `rubber-duck` (interview the user about a plan), `rubber-duck-with-docs` (challenge a plan against project domain language), `zoom-out` (step back from current work).
- **Stack-specific helpers** — `gitbutler`, `shadcn`, `shadcn-ui`, `supabase-postgres-best-practices`, `migrate-oxlint`.

## Getting started

```sh
git clone git@github.com:vidluther/sabu.git ~/work/personal/sabu
cd ~/work/personal/sabu
./setup.sh
```

`setup.sh` symlinks each `skills/<name>/` into `~/.claude/skills/<name>` (the location Claude Code reads user-level skills from), so the skills become invokable via `/<name>` in any session. Idempotent — safe to re-run after adding skills.

## Provenance

Most of the skills are forks or evolutions of public sets — Matt Pocock's skill collection and others — adapted to my workflow. Some are bespoke. The `marshal` skill (and the broader state/provenance label model in `triage`) were rewritten from scratch in May 2026 as part of a redesign aimed at making the harness work for any new or existing repo.

## Security 

I highly recommend you view the skills here, and elsewhere, before you decide to start using them yourself. Take a look at [Skillspector](https://github.com/nvidia/skillspector) and see ifthe skills you have do anything dangerous, and decide if you want to risk it or not. 

