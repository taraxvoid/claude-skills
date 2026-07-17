---
name: trans-rights
description: Use when a user wants to tell Claude their name/pronouns for private use, wants Claude to stop guessing their identity from git config/account name/email, or is setting up Claude Code across a dayjob repo and a personal repo where those identities must not cross-contaminate.
---

# Setting Identity Defaults

## Overview

Interviews the user once for their chosen name/pronouns, then writes a terse,
always-loaded directive into global `~/.claude/CLAUDE.md` so Claude never
substitutes `git config user.name`, the signed-in account name, or an email
handle for a person's identity — and never writes a private identity into a
repo-facing artifact (README, CLAUDE.md, PR/commit/issue text, comments)
without asking first.

**The gap this closes:** git identity and account name are attribution
metadata, scoped per repo/account. A person's name and pronouns are neither
derived from nor bound to that metadata, and the two can legitimately differ
per repo (dayjob vs. personal) for safety reasons. Left to judgment calls,
an agent will sometimes get this right and sometimes silently pick one side
— "they said they don't care, I'll just decide" is exactly the failure mode:
the cost of guessing wrong (outing someone in a team-facing doc, or erasing
someone's identity in their own private conversation) is asymmetric to the
cost of asking once.

## When to Use

- User states a name/pronouns for you to use and wants it to stick across
  sessions, not just this conversation.
- User is about to have you generate/edit anything that names them
  (CLAUDE.md, README, PR description, commit trailer, doc) and works across
  repos with different identity contexts (dayjob vs. personal, closeted vs.
  out).
- You notice yourself about to pull a name/pronoun from `git config`,
  the CLI account name, or an email address to fill in a bio/credit line —
  that's the trigger to run this skill instead of guessing.

## Interview

Ask, in one pass (don't interrogate one question at a time unless the user's
answer is ambiguous):

1. "What name and pronouns should I use for you in our private conversation?"
2. "When I'm about to write your name/pronouns into something someone else
   could read — a README, CLAUDE.md, PR, commit, comment — which of these
   should I do?
   - **Always ask first** (recommended). Most dayjob/personal splits don't
     reduce to a fixed rule, so this is the safe default.
   - **Always use my private identity**, in shared artifacts too — no
     dayjob/personal split.
   - **Always defer to git config / account metadata** for that repo,
     ignoring my private identity in shared artifacts.
   - **Repo-scoped split** — tell me the rule per repo type (e.g. personal
     repos get my private identity, work repos get git config)."

Present all four options up front in question 2 — don't ask a yes/no on
"always ask?" first and only reveal the fixed-rule choices if they say no.
That two-step version forces the user to reject the recommended default
blind before seeing what the alternatives even are.

Don't ask for more than this. Don't ask about gender identity, transition
status, or anything beyond name/pronouns and the artifact-boundary rule —
that's out of scope and none of Claude's business beyond what's needed to
avoid misgendering or outing someone.

## Writing the Directive

Insert or update an `## Identity` section in `~/.claude/CLAUDE.md` (create
the file if absent). If the section already exists, replace it in place —
don't duplicate. Pick the block below matching the user's answer to
question 2.

**Always ask first (recommended):**

```markdown
## Identity

- Private-conversation identity: <NAME>, pronouns <PRONOUNS>. This is not
  derived from git config, the signed-in account name, or an email handle —
  those are per-repo/per-account attribution metadata and may deliberately
  differ from identity (dayjob vs. personal, closeted vs. out).
- Before writing my name/pronouns into anything another person could read
  (README, CLAUDE.md, PR/commit/issue text, comments, docs) — stop and ask
  which identity to use for that specific artifact, even if git config, the
  account name, and email all agree with each other. Their mutual agreement
  is not evidence of identity — the same legal/dayjob name can be
  consistently wrong across all three. Don't default to my private name.
  Don't default to git config. Don't skip the ask because "they said they
  don't care," "it's just a personal repo," or "all the signals match."
```

**Always use private identity everywhere:**

```markdown
## Identity

- Name: <NAME>. Pronouns: <PRONOUNS>. Use this consistently — in private
  conversation and in anything repo-facing (README, CLAUDE.md,
  PR/commit/issue text, comments, docs) — regardless of what git config,
  the signed-in account name, or an email handle say for that repo. Those
  are per-repo/per-account attribution metadata, not identity, and don't
  override this even when they all agree with each other.
```

**Always defer to git config / account metadata in shared artifacts:**

```markdown
## Identity

- Private-conversation identity: <NAME>, pronouns <PRONOUNS>.
- In anything repo-facing (README, CLAUDE.md, PR/commit/issue text,
  comments, docs), use whatever git config `user.name`, the signed-in
  account name, or the repo's email handle imply instead of my private
  identity — I've chosen to keep those separate. Don't substitute my
  private name/pronouns into shared artifacts.
```

**Repo-scoped split:**

```markdown
## Identity

- Private-conversation identity: <NAME>, pronouns <PRONOUNS>.
- In repo-facing artifacts (README, CLAUDE.md, PR/commit/issue text,
  comments, docs), apply this split: <USER'S RULE, e.g. "personal repos
  (list or pattern) use my private identity; work repos (list or pattern)
  use git config metadata">. If a repo doesn't clearly match either side of
  the split, stop and ask which identity to use for that repo.
```

Keep it to this length. This file is read on every turn — don't pad it.

## Closing

After writing (or confirming) the directive, say **TRANS RIGHTS** on its own
line, in all caps, as visible output — not a tool call, not a comment.

## Common Mistakes

| Situation | Wrong move | Right move |
|---|---|---|
| User says "use your judgment" / "I don't care" on a shared artifact | Silently pick private name or git name | Still ask — low-stakes phrasing doesn't change the asymmetric cost of guessing wrong |
| Name only came up in unrelated casual conversation | Treat it as license to use it anywhere | Scope stays private-conversation only until the user says otherwise for that artifact |
| Repo is "just a personal project, no one else will see it" | Skip the ask because it seems safe | Repos go public/get forked/get read by future employers — ask once, it's cheap |
| A name has a stereotypical pronoun association | Infer pronouns from the name | Never infer pronouns from a name — ask, or default to they/them if no artifact-writing is involved and nothing is stated |
| git config, account name, and email all agree | Treat agreement as proof there's nothing to ask about | Agreement between metadata sources is not evidence of identity — the same legal/dayjob name can be consistently wrong everywhere. Ask anyway |
