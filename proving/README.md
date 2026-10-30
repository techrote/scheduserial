# Serial Native — live proof experiment

This folder contains the **disposable, live two-execution proof** of Scheduserial's repository-free prompt handover.

**Purpose:** establish whether a scheduled task can replace **its own stored prompt** during execution, and whether a later *independent scheduled execution* actually uses that replacement. A successful manual edit from an interactive chat is a **setup/control check**, never evidence of self-editing.

## Scope and independence

The **scheduled task prompt is the only continuation state** for Serial Native. GitHub files here are an external, human-inspectable **audit record only**; the test agent is not required to read from this repository to know what to do. It must not derive its next instructions from `proving/`, create a replacement task, or depend on GitHub write access.

The disposable task has no permission to modify unrelated tasks, send external communications, or mutate other projects. Its only planned mutation is to its **own** saved prompt, followed by pausing itself after the proof (if the task-management interface permits). It should keep its schedule unchanged until termination.

## Evidence and files

- [Protocol and pass/fail rules](protocol.md): phases, strict proof gates, and treatment of run-now versus scheduled executions.
- [Experiment evidence ledger](evidence.md): **only actually observed** IDs, task metadata, transition results, and blockers.
- [Task prompt fixture](seed-prompt.md): canonical generation-0 prompt; the actual task ID is pinned after creation and must be verified against readback.

## Proof requirements

| Gate | Required observation |
| --- | --- |
| P0 — task created | Newly created disposable task with recorded exact ID, full prompt, and schedule |
| P1 — self-edit | Execution launched from **the task runner**, not interactive chat, updates **the same ID's** prompt from G0 to G1 |
| P2 — readback | After P1, task record independently shows G1, generated marker, unchanged fixed contract, and same schedule |
| P3 — successor execution | A **separate task execution** begins with G1 stored as its prompt and follows its new instructions, including exact marker |
| P4 — stop | Verification is recorded, task safely paused/finished; no unintended task created or modified |

A run requested via `run_now` may be useful to establish whether the task runner supports self-editing, but **is not evidence of an automatic clock-triggered recurrence**. If the strict claim is specifically two independently *scheduled* executions, retain status as **PARTIAL** until both are observed in the scheduled run history.

The agent should generate a fresh marker in execution 1; the marker must not already appear in the G0 prompt. Execution 2 must quote that marker from the G1 prompt and identify that it was taken from the task's saved successor instructions. The real test is a G0→G1 write by the task runner, and a G1→G2 response by a second run.

## Status

See [evidence.md](evidence.md). **Do not infer a PASS solely because the task was created, triggered, or because an interactive session edited its prompt.**

Related design: [Serial Native](../docs/serial-native.md), [qualification](../docs/verification.md).
