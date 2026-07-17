# claude-skills

Personal Claude Code plugin marketplace. Private, single-owner — skills here
are dogfooded on my own machines before (maybe) graduating anywhere public.

## Install

```
/plugin marketplace add taraxvoid/claude-skills
/plugin install setting-identity-defaults@claude-skills
```

This repo is **private**. `/plugin marketplace add` clones it under the hood,
so the machine running Claude Code needs git/`gh` credentials with read
access to `taraxvoid/claude-skills` already configured (SSH key or the `gh`
credential helper) — if the add fails, that's the first thing to check.

## Skills

- **setting-identity-defaults** — interviews you once for your chosen
  name/pronouns, then writes a terse directive into global `~/.claude/CLAUDE.md`
  so Claude stops treating agreement between `git config`, account name, and
  email as evidence of identity, and asks before writing your name/pronouns
  into anything repo-facing (README, CLAUDE.md, PR/commit text, comments).

## Adding a new skill

1. `skills/<name>/SKILL.md` (+ optional `.claude-plugin/plugin.json` if it
   should be independently installable/versioned).
2. Add an entry to `.claude-plugin/marketplace.json` under `plugins`.
3. Commit, push to `main`.
