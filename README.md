# claude-skills

Tara's skillz which won't ever pay the billz (but do important things anyway)

## Install

```
/plugin marketplace add taraxvoid/claude-skills
/plugin install trans-rights@claude-skills
```

## Skills

- **trans-rights** — interviews you once for your chosen
  name/pronouns, then writes a directive into global `~/.claude/CLAUDE.md`
  so Claude stops treating `git config`, account name(s), and
  email addy as evidence of identity, and asks before writing your name/pronouns
  into anything potentially dayjob-facing (README, CLAUDE.md, PR/commit text, comments).

## Adding a new skill

1. `skills/<name>/SKILL.md` (+ optional `.claude-plugin/plugin.json` if it
   should be independently installable/versioned).
2. Add an entry to `.claude-plugin/marketplace.json` under `plugins`.
3. Commit, push to `main`.
