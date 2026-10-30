# Serial Native: self-editing scheduled-task handover

**Primary use:** lightweight serial work where storing the successor prompt inside the **same scheduled task** is more convenient than maintaining a repository.

**Qualification status (2026-10-30): CORE CONTINUATION PROVEN, FAULT TOLERANCE EXPERIMENTAL.** A disposable task rewrote its own prompt during one clock-scheduled execution; a second independent clock-scheduled execution read the replacement instructions, consumed an unpredictable first-run marker, updated the same prompt again and disabled itself. A post-restoration readback verified **STAGE=2**, `is_enabled=false`, the unchanged fixed contract and a **completed** second run. See [evidence](../proving/evidence.md) and [independent audit](../proving/post-restore-audit.md). This does **not** prove exclusivity under overlap, denied-write recovery, portability to every configuration or long-term reliability.

## Model

A single existing task holds two logically distinct regions:

1. **Fixed operating contract:** scope, task identity, work policy, verification, update/readback procedure, failure handling and stop conditions. Keep this text stable across generations.
2. **Mutable continuation:** generation number, last verified result, current blockers, next bounded objective, acceptance criteria and evidence links.

The agent does not create a new task every run. It should update **the same task ID** without changing schedule, timezone, title or enabled state unless the goal is explicitly completed or the owner authorizes a change.

See [the example prompt](../templates/serial-native-task.md).

## Execution protocol

1. Identify the task from authoritative tool context or inspect the existing task record. **Never guess an ID.**
2. Read the saved prompt and schedule where available; confirm it is the same task as the one executing.
3. Reconcile the mutable continuation with live evidence and any explicit owner revisions. Do not assume old statements are true.
4. Check for a prior active run or conflicting ownership. Prompt generations alone do not guarantee non-overlap.
5. Perform one bounded action. Collect exact results, including failures and effects on external systems.
6. Construct a **complete replacement prompt** preserving the fixed contract verbatim and updating only the mutable region to generation N+1.
7. Invoke the authorized task-update tool against the **same ID**. Update only the prompt field, or pause the task if completion is genuinely verified and stopping is authorized.
8. Read back the task. Verify the ID, full prompt, new generation, unchanged fixed contract and unchanged schedule.
9. Only then claim a successful handover. If the update/readback failed, report `NEEDS_ATTENTION` and avoid pretending the successor will see the new objective.

The task update has no documented general-purpose transactional lock for coordinated prompt generations. Two overlapping runs may both try to write and the later result could overwrite the earlier. This is a limitation to test, not a solved problem.

## Controlled trial, before real work

Use a harmless two-run experiment:

- **Run 1:** identify its own task, observe generation 0, record a harmless unique nonce/test result, and replace just the mutable section with generation 1 instructions.
- **Run 2:** verify that the same scheduled task now actually executes the generation 1 instructions, references the previous marker, and progresses to generation 2 without schedule or contract drift.
- After both runs, inspect the saved task record, history and any notifications. Failure to access the update tool, missing readback, stale instructions, wrong task ID, or changed schedule is a failed trial.

This experiment **was performed** on 2026-10-30 using task `6ae4d7275c348191a5b4b70dbd0cd95b`: G0→G1 and G1→G2 ran as separate scheduled executions and the task was disabled after successful readbacks. The proof task is historical and **must not be restarted for another project**. Details: [acceptance](../proving/second-run-evidence.md) and [final reconciliation](../proving/post-restore-audit.md).

## Failure handling

| Failure | Safe response |
| --- | --- |
| Task-management tool absent inside scheduled execution | Record the capability gap in the run output; do not claim self-edit is supported there |
| Cannot identify the exact task | Stop; never modify a similarly named task |
| Update denied / approval needed | Stop and request authorized action |
| Update succeeded but readback disagrees | Treat as unverified; investigate rather than issuing blind repeated overwrites |
| Previous run still active / no reliable exclusivity | Stop mutations; notify the owner |
| Prompt contract inadvertently changed | Restore from a reviewed, owner-controlled copy; do not bootstrap from the corrupted text |
| Goal completed | Pause or disable the task if permitted and verify; otherwise request owner action |

## Advantages and limitations

**Advantages:** no repository, file hosting or Git permissions needed for persistence; one schedule and one editable prompt; straightforward operator inspection.

**Limitations:** weaker historical audit, more difficult rollback, prompt size/drift risk, task self-edit demonstrated only in the tested configuration, and no established compare-and-swap semantics for prompt updates. Retaining a human-readable copy of the fixed contract outside the task improves recovery, but doing so is optional and weakens the strict 'no external state' ideal.

Do not store credentials or sensitive personal information in a task prompt; sharing an eligible task can expose its saved instructions. See [OpenAI Scheduled Tasks guidance](references.md).

## Status

The minimal **self-edit + successor scheduled run** mechanism is empirically demonstrated; it remains a **prototype** for real engineering workloads until the guarded-retry, stale-generation, interrupted-execution and operational recovery tests in [next qualification priorities](next-qualification.md) pass. Do not imply exactly-once delivery or a scheduler-level exclusive lock.
