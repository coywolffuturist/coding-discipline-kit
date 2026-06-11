# Coding Discipline Kit

*Rigor skills, independent-reviewer agents, and deterministic guard hooks that
make an AI coding agent trustworthy.*

> Working title — rename freely.

AI coding agents are fast, confident, and occasionally confidently wrong. This
kit installs **habits of rigor** (skills), **independent reviewers** (agents),
and **hard guardrails** (hooks) so your agent earns trust: it reproduces a bug
before fixing it, checks what already exists before building, refuses to ship
unverified, gets a second opinion before "done," and is structurally prevented
from leaking secrets.

This is the **coding-focused** kit. There's a sibling for non-technical
knowledge work — see *Companion kit* below.

## What's inside

**Skills** (habits the agent applies to its own work):

| Skill | What it does |
|---|---|
| `95-percent-rule` | Don't claim "done/works" until evidence supports it; report the honest probability. |
| `substrate-search` | Before building anything new, find what already exists and why it's insufficient. |
| `root-cause` | Fix the lowest broken layer, not the symptom; reproduce the failure as a test first. |
| `karsholto` | Smallest brick that proves the wall — and build the trusted eval *first*. |
| `think-3x` | Best idea → red-team it → synthesize → build the synthesis, not the first idea. |
| `nomess` | Before "done": lint, no orphans, no doc-drift, no half-states (runs `nomess.sh`). |
| `vizcheck` | Verify any UI/visual change in its *rendered* form — read the pixels, not the code. |
| `adversarial-pass` | Independent review before claiming done; spawn the `refuter` agent for high-stakes. |
| `adversarial-inverse` | Before locking any value-bearing mechanism, find how it's exploited. |
| `self-correcting-substrate` | Build monitors/crons that *act* on what they find, not just alert. |
| `discipline` | The conductor — fires the right gate at the right phase for high-stakes work. |
| `grill-me` | Interrogate a plan until every branch is resolved. |

**Agents** (independent reviewers you spawn in a fresh context):

| Agent | Role |
|---|---|
| `refuter` | A hostile, independent reviewer that reproduces and refutes a claim/fix before it's accepted. |
| `mechanism-auditor` | An independent auditor for value-bearing mechanisms (tokenomics, fees, auctions): how is it exploited? |

**Hooks & scripts** (deterministic — they enforce, they don't just advise):

| File | What it does |
|---|---|
| `scripts/guard_secrets.sh` | PreToolUse[Bash] — blocks `gh repo create` without `--private`, blocks visibility flips to public, and scans outgoing commits for secrets before any `git push`. |
| `scripts/guard_modals.sh` | PreToolUse[Write\|Edit] — blocks browser modals (`alert`/`confirm`/`prompt`) in frontend files. |
| `scripts/nomess.sh` | Repo-hygiene scan (lint, untracked, stale branches, dead symlinks, unpushed). Used by the `nomess` skill. |
| `scripts/secret-patterns.txt` | The secret regexes `guard_secrets.sh` uses (or install `gitleaks` instead). |

## Install

**Skills and agents** (the always-on disciplines):

```
mkdir -p ~/.claude/skills ~/.claude/agents
cp -r skills/* ~/.claude/skills/
cp -r agents/* ~/.claude/agents/
```

**Scripts** (make them runnable; the secret-patterns file is read from `~/.git-hooks/`):

```
mkdir -p ~/.claude/scripts ~/.git-hooks
cp scripts/nomess.sh scripts/guard_secrets.sh scripts/guard_modals.sh ~/.claude/scripts/
chmod +x ~/.claude/scripts/*.sh
cp scripts/secret-patterns.txt ~/.git-hooks/        # or install gitleaks instead
```

**Hooks** (turn the guards on) — add to `~/.claude/settings.json`:

```json
{
  "hooks": {
    "PreToolUse": [
      { "matcher": "Bash",
        "hooks": [{ "type": "command", "command": "~/.claude/scripts/guard_secrets.sh", "timeout": 30 }] },
      { "matcher": "Write|Edit",
        "hooks": [{ "type": "command", "command": "~/.claude/scripts/guard_modals.sh", "timeout": 15 }] }
    ]
  }
}
```

Start a new session. Skills auto-fire when their moment arrives (and you can
invoke any by name); the hooks run on every matching tool call.

> Requires `jq` for the guard hooks. The secret scan uses `gitleaks` if present,
> otherwise the bundled `secret-patterns.txt`.

## Companion kit (for non-coding work)

There's a sibling kit, **agent-discipline-kit**, with the same disciplines
generalized for non-technical knowledge work (decks, legal, accounting,
marketing, research). Every skill name differs between the two kits **on
purpose** — so you can install both on one machine with **zero collisions**.
Copy both into `~/.claude/` and they coexist cleanly.

## The one idea behind all of it

**Evidence beats assertion.** Every piece here replaces "it should work / looks
right" with "I ran it, and here's the proof" — and the hooks make the
unforgivable mistakes (a leaked secret, a public repo) structurally hard to make.
