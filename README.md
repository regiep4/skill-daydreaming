# daydreaming

Public v1 continuity checkpoint skill for bounded recent context review.

DayDreaming helps an agent decide what should meaningfully carry forward into the next restart, what should stay visible but lighter, and what should remain restrained. It is report-first, conservative, bounded, and explicit about persistence.

## Install

```bash
npx skills add regiep4/skill-daydreaming@daydreaming
```

## What this skill does

DayDreaming runs a bounded continuity checkpoint over recent, explicitly selected context. Instead of treating all recent context as equally worth saving, it applies restart-oriented judgment and produces a compact result that says:

- what was reviewed
- what matters for the next restart
- what should carry forward
- what should stay visible but lighter
- what outcome was chosen
- why that outcome was correct

## DayDreaming vs a normal checkpoint

| Aspect | Normal checkpoint | DayDreaming |
|---|---|---|
| Main job | Store context | Judge what should meaningfully carry forward for the next restart |
| Core question | What should be saved? | What should carry forward, stay visible but lighter, or stay restrained? |
| Input posture | Capture what is there | Review bounded recent signal conservatively |
| Output posture | Stored snapshot | Restart-oriented judgment result |
| Treatment of quiet outcomes | Can feel empty or underpowered | Explicitly valid governed results |
| Restart usefulness | Depends on raw context quality | Optimized for restart usefulness |
| Scope control | Varies by implementation | Bounded by default; no broad scanning |

A normal checkpoint stores context. DayDreaming decides what deserves stronger carry-forward judgment.

## What it is not

This skill is not:

- a broad autonomous memory engine
- a workspace-wide scanner
- a hidden file mutation tool
- a background scheduler-driven system
- a generic journaling skill

By default it does **not**:

- scan the whole workspace
- chain through prior runs automatically
- silently write to `MEMORY.md`
- silently write to `memory/YYYY-MM-DD.md`
- silently mutate unrelated user files

## Supported commands

The public v1 command surface is:

- `/skill daydreaming`
- `/skill daydreaming draft`
- `/skill daydreaming promote`
- `/skill daydreaming load`
- `/skill daydreaming view`
- `/skill daydreaming view draft`

## Expected inputs

DayDreaming expects **bounded** inputs, such as:

- a recent transcript chunk
- a scratch note plus one or two supporting files
- explicitly named sources the user wants reviewed

If the request is too vague or too broad, the correct behavior is to ask for tighter bounds before proceeding.

## Expected output shape

A good DayDreaming result is compact and restart-oriented. Typical sections are:

- Reviewed
- Restart from here
- Carry forward
- Keep visible / watch
- Outcome
- Rationale
- Proposals (if any)
- Watch / unresolved (if any)

## Valid outcomes

Quiet outcomes are valid. Public v1 treats all of these as legitimate results:

- `successful-with-updates`
- `successful-no-op`
- `deferred`
- `proposal-only`
- `watch-unresolved-captured`

That means a good run does **not** need to force stronger preservation when the signal is weak, local, or badly timed.

## Design principles

DayDreaming is designed to be:

- **report-first**
- **conservative**
- **bounded**
- **restart-oriented**
- **explicit about persistence**

## Example usage

```text
/skill daydreaming
```
Run a continuity checkpoint and save the latest saved result.

```text
/skill daydreaming draft
```
Run a continuity checkpoint and save the latest draft result.

```text
/skill daydreaming view
```
Display the latest saved result without creating a new run.

## Repo contents

- `SKILL.md` — the skill contract and operating instructions used by the agent runtime

If you want the shortest description: DayDreaming is a bounded, conservative continuity checkpoint skill that helps an agent restart better without pretending every recent signal deserves long-term preservation.
