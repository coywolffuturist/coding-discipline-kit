---
name: discipline
description: Full-rigor mode for a high-stakes workstream — a PHASE-AWARE conductor over the discipline stack. It does NOT recite every gate at once; it fires the right one at each phase and lets none be skipped. DESIGN: substrate-search → compile-it → think-3x (carrying karsholto + adversarial-inverse-for-mechanisms as lenses). VERIFY: the triad (.95 + root-cause + karsholto) → completer → nomess → cold-read → vizcheck (UI only) → adversarial pass. Trigger: "discipline" / "full rigor", or proactively for any high-stakes build (money movement, irreversible/outward-facing change, new substrate).
---

# Discipline — the full-rigor conductor

"Discipline" is not a checklist to recite. It is a standing commitment
that for THIS workstream the correct gate fires at each phase —
automatically, without the user naming each one — and **none is skipped
when its phase arrives.** Reciting all of them at once is the failure
mode, not the goal.

## How to run it

Identify the current PHASE, fire that phase's gates, carry the
commitment to the other phase. Most work passes through both in order.

### DESIGN — before building anything non-trivial

1. **substrate-search** — proposing new substrate (table / module /
   endpoint / daemon / abstraction / layer)? Answer in writing FIRST:
   *"what existing piece is insufficient?"* Prefer reusing a validated
   component.
2. **compile-it** — before designing an LLM build, ask: should this be
   deterministic CODE instead? If it repeats + is mechanical + stable +
   checkable, write the hard code (agents think, code does). Crystallize on
   the 2nd–3rd repeat, not the 1st.
3. **think-3x** — Think 1 (best idea) → Think 2 (red-team) → Think 3
   (synthesis); build the synthesis, not Think 1. Show all three before
   code. Think 2 carries two lenses:
   - **karsholto** — smallest brick that proves the wall; eval-driven;
     no N-layers-ahead-of-evidence.
   - **adversarial-inverse** — REQUIRED only when building a
     cooperative-economic mechanism (treasuries, fees, slashing, jury
     triggers, eligibility): how does a participant exploit it for +EV
     harm? Close every exploit or name the trade-off. For non-mechanism
     builds, Think 2 runs the design-failure lenses instead.

### VERIFY — before claiming "done / ready / deployed / clean / it works"

4. **The triad — .95 + root-cause + karsholto** (always fire together):
   - **.95** — define the user-outcome ONCE, set a prior, update the
     posterior with real cycles; don't claim ready below P≥0.95; answer
     "are you sure?" with posterior + evidence, not a feeling.
   - **root-cause** — fix the root, not the symptom; a verified
     symptom-patch is still a symptom-patch.
5. **completer** — about to claim done-with-residue, or write
   "follow-up / next session / separate pass / deferred"? Classify the
   remaining work: a GENUINE blocker (data/decision/access you lack, or a
   distinct NEW build) → name it + what unblocks it; or stopping-short
   ("it's big" / "end of session" — cop-outs) → finish it now. The user
   outcome is the WHOLE job.
6. **nomess** — semantic orphans, dead symlinks, untracked files, stale
   gates, doc-vs-runtime drift, end-to-end smoke gap.
7. **cold-read** — about to ship or retire an artifact? Cold-read it as a
   context-free future agent would: does anything dead/deprecated read as
   live, could it be mistaken for current, is the intent legible? When
   retiring something, tombstone-or-remove and eliminate the whole CLASS
   (sweep every occurrence), not the instance you tripped over.
8. **vizcheck** — UI/CSS/layout change? Verify the visual achieved its
   intent in its rendered form — read the pixels, escalate to coordinate
   readback for exact placement. Syntax checks don't substitute.
9. **adversarial-pass** — the author can't be the only reviewer.
   Live-fire the user-outcome path (repeatedly for nondeterministic
   surfaces); for high-stakes work, spawn the `refuter` agent to
   REFUTE the claim, not bless it. This EARNS the .95 posterior rather
   than asserting it.

## Rules

- **Phase-match, don't dump.** Don't run nomess before anything is
  built; don't run think-3x while verifying a finished artifact.
- **Anti-ritual.** No "I will now apply the disciplines." Apply the
  one(s) whose phase is live, genuinely — depth over recitation.
- **None skipped.** "Discipline" is a promise across the whole
  workstream, not a one-time incantation.
- **Auto-fires already exist.** Most sub-skills self-trigger (.95 on
  "are you sure", nomess on "done", vizcheck on UI, think-3x on
  "build"). Discipline is the umbrella guaranteeing the *full* sequence
  so nothing relies on a single trigger firing.

## Composition map

```
DESIGN:  substrate-search → compile-it → think-3x ─┬─ karsholto (lens)
                                      └─ adversarial-inverse (lens; mechanisms only)
                   │  build the synthesis
                   ▼
VERIFY:  triad(.95 + root-cause + karsholto) → completer → nomess → cold-read → vizcheck(UI) → adversarial-pass(→ refuter agent)
```

## One-line summary

**Discipline = full-rigor mode: the right gate at the right phase, none
skipped, none recited for show.**
