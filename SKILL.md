---
name: daydreaming
description: Public v1 continuity checkpoint skill for bounded recent context review. Use when the user wants a conservative restart-oriented judgment about what is worth carrying forward, what should stay visible but lighter, and what does not deserve stronger preservation—without hidden memory writes or broad scanning.
---

# DayDreaming

DayDreaming is a public v1 continuity checkpoint skill.

Use it to review bounded recent signal, decide what is worth carrying forward for the next restart, and produce a compact restart-oriented result through a small explicit command surface.

Treat it as:
- report-first
- conservative
- bounded
- restart-oriented
- explicit about persistence

Do not treat it as:
- an always-on memory engine
- a workspace-wide scanner
- a scheduler-driven system
- a hidden file mutation tool
- a generic saved checkpoint tool

## Public v1 command surface

The public v1 command surface is:
- `/skill daydreaming`
- `/skill daydreaming draft`
- `/skill daydreaming promote`
- `/skill daydreaming load`
- `/skill daydreaming view`
- `/skill daydreaming view draft`

## Core mental model

Public v1 DayDreaming should be understood simply as:
- run a continuity checkpoint
- judge what is worth carrying forward for the next restart
- keep lighter but still meaningful items visible when justified
- preserve valid restraint when stronger preservation is not warranted
- save or draft the result
- optionally promote draft to saved
- optionally view or load a prior result
- never rely on hidden background behavior

A normal saved checkpoint stores context.
DayDreaming decides what should meaningfully carry forward for the next restart, what should stay visible but lighter, and what does not deserve stronger preservation.

Default public behavior is:
- continuity checkpoint only
- no public exposure of broader internal family architecture
- no hidden memory writes by default
- no broad scanning
- no prior-run chaining by default

## Command meanings

## `/skill daydreaming`
- runs the default continuity checkpoint
- saves the result as the latest saved result
- returns the checkpoint result plus saved confirmation

Reads:
- current bounded run inputs only

Writes:
- latest saved result
- does **not** silently write to memory files by default

## `/skill daydreaming draft`
- runs the default continuity checkpoint
- saves the result as the latest draft result
- returns the checkpoint result plus draft confirmation

Reads:
- current bounded run inputs only

Writes:
- latest draft result
- does **not** silently update latest saved result
- does **not** silently write to memory files by default

## `/skill daydreaming promote`
- promotes the latest draft result into the latest saved result
- returns promotion confirmation when successful

Reads:
- latest draft result only

Writes:
- latest saved result from the latest draft
- does **not** silently fall back if no draft exists
- does **not** silently write to memory files by default

Required empty-state behavior:
- if no latest draft exists, return a clear `no draft to promote` style result

## `/skill daydreaming load`
- loads the latest saved result back into working context
- is not just display

Reads:
- latest saved result only

Writes:
- no new checkpoint result by itself
- no silent memory writes by default

Required empty-state behavior:
- if no latest saved result exists, return a clear no-saved-result result

## `/skill daydreaming view`
- displays the latest saved result only
- does not load it into working context
- does not create a new run

Reads:
- latest saved result only

Writes:
- none

Required empty-state behavior:
- if no latest saved result exists, return a clear no-saved-result result

## `/skill daydreaming view draft`
- displays the latest draft result only
- does not load it into working context
- does not create a new run

Reads:
- latest draft result only

Writes:
- none

Required empty-state behavior:
- if no latest draft result exists, return a clear no-draft-result result

## Persistence model

Public v1 DayDreaming uses only two persistence concepts:
- latest saved result
- latest draft result

Keep this simple.

Public v1 guarantees the semantics of these latest pointers.
It does **not** require a specific storage path, folder layout, or database design in the skill contract.

## Input contract

Require bounded inputs.

Good inputs include:
- a small set of recent notes
- a bounded transcript chunk
- a current scratch note plus one or two supporting files
- explicitly named sources the user wants reviewed

Avoid:
- broad workspace fishing
- “look through everything”
- hidden source-surface guessing
- ambient scanning
- automatic prior-run chaining by default

If bounds are unclear, ask for tighter source selection before proceeding.

## Read/write posture

Allowed reads:
- current bounded run inputs for a new run
- latest saved result for `view` or `load`
- latest draft result for `view draft` or `promote`

Not allowed by default:
- broad workspace scanning
- automatic memory folder reading
- automatic prior-run chaining
- hidden consultation of unrelated artifacts

Allowed writes:
- saved DayDreaming result state
- draft DayDreaming result state
- latest pointer updates

Not allowed by default:
- silent writes to `MEMORY.md`
- silent writes to `memory/YYYY-MM-DD.md`
- silent writes to other user files

## Expected output

Produce a compact continuity checkpoint result that explicitly answers:
- what was reviewed
- what matters for the next restart
- what should carry forward
- what should remain visible but lighter
- what outcome was chosen
- why that outcome was correct
- whether any proposals or watch items are justified

Keep the output:
- compact
- practical
- restart-oriented
- honest about uncertainty and restraint

Recommended output shape:
- Reviewed
- Restart from here
- Carry forward
- Keep visible / watch
- Outcome
- Rationale
- Proposals (if any)
- Watch/unresolved (if any)

## Valid outcomes

Treat all of these as valid public v1 results:
- `successful-with-updates`
- `successful-no-op`
- `deferred`
- `proposal-only`
- `watch-unresolved-captured`

Important:
- a good run does **not** have to produce stronger carry-forward
- quiet outcomes remain valid governed results
- no-op is not failure
- deferred is not indecision if timing is the real issue
- proposal-only is a valid light result
- watch/unresolved capture is valid when visibility matters more than stronger preservation

## Carry-forward judgment guidance

Carry forward when the signal is:
- meaningful enough to matter later
- useful for restart
- durable enough to deserve explicit preservation
- clearer after bounded review than in raw form

Keep visible / watch when the signal:
- matters
- but is not yet strong enough, stable enough, or clear enough for stronger carry-forward
- deserves visibility more than stronger preservation

Do not force stronger carry-forward when the signal is:
- thin
- badly timed
- mostly local noise
- better handled by no-op, defer, or watch visibility

## Public examples

- `/skill daydreaming` -> run checkpoint and save latest saved result
- `/skill daydreaming draft` -> run checkpoint and save latest draft result
- `/skill daydreaming promote` -> promote latest draft into latest saved result
- `/skill daydreaming view` -> display latest saved result only
- `/skill daydreaming view draft` -> display latest draft result only
- `/skill daydreaming load` -> reuse latest saved result as working context

## Normal checkpoint vs DayDreaming

| aspect | normal checkpoint | DayDreaming |
|---|---|---|
| main job | store context | judge what should meaningfully carry forward for the next restart |
| input posture | capture what is there | review bounded signal conservatively |
| core question | what should be saved? | what should carry forward, stay visible but lighter, or stay restrained? |
| output posture | stored snapshot | restart-oriented judgment result |
| treatment of quiet outcomes | may feel empty | explicitly valid governed results |
| restart usefulness | depends on raw context quality | explicitly optimized for restart usefulness |
| scope control | varies by implementation | bounded by default, no broad scanning |

A normal checkpoint stores context. DayDreaming decides what should meaningfully carry forward for the next restart.

## What this skill is not

This skill is not:
- a broad autonomous memory system
- a workspace-wide scanner
- an always-on reflection engine
- a generic journaling skill
- a scheduler-driven background runner
- the broader companion product

This v1 skill is only the public continuity checkpoint slice with explicit save/draft/view/load/promote behavior.

## Output style

Write like a calm operator-facing checkpoint:
- concise
- clear
- non-theatrical
- practical
- restart-useful

Do not inflate the result.
Do not pretend quiet outcomes are weak.
Do not turn the result into a broad plan unless the user explicitly asks.
