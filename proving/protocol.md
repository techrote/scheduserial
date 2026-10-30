# Serial Native scheduled-task proof protocol

Recorded: 2026-10-30. Test is intentionally small, bounded, and non-destructive.

## Phase A — setup

1. Inspect current `techrote/scheduserial` head, instructions and existing `proving/` files. Avoid overwriting concurrent work.
2. Create exactly **one new disposable scheduled task** named `Scheduserial Native Proof`. Use an hourly schedule with a limited recurrence count where supported; no subhour recurrence. The first real scheduled run must occur after creation.
3. The G0 prompt contains two named regions: `FIXED CONTRACT` and `MUTABLE CONTINUATION`. Its initial stage is 0. Use a placeholder for task ID at creation only; after creation, an interactive **setup-only** update may pin the returned task ID. A setup edit is not a proof result.
4. Read back the resulting ID, saved full prompt and schedule. Record them in [evidence](evidence.md) with timestamps and an exact generation-0 snapshot in [seed-prompt](seed-prompt.md).

## Phase B — run 1 (self-edit)

1. A task execution (scheduled or runner-invoked, explicitly label which) identifies its own pinned ID.
2. Read the existing saved prompt and schedule via task management if available; require `stage=0`.
3. Generate a **new, unique marker** not present in G0, for example a random alphanumeric nonce; do not use a prewritten phrase.
4. Use the **task-update** interface to replace **only the prompt** of the same task ID, preserving full fixed contract verbatim and schedule/timezone/title.
5. The G1 prompt must contain `stage=1`, the new marker, and an instruction that execution 2 echo exactly that marker and record it as coming from the new saved instructions. It must also instruct execution 2 to mark G2 and pause the disposable task if supported.
6. Read back. Report success only if task ID, G1 marker, unchanged fixed contract and unchanged schedule match. Otherwise report BLOCKED, retain exact error, and stop.

## Phase C — run 2 (successor)

1. Execute **the same** task again only after run 1 is definitively complete and G1 is present.
2. Confirm the **task runner actually received G1**, not G0. Quote the G1 nonce exactly; do not invent or recover it from a repository file or other memory.
3. Update the same task prompt to `stage=2` with PASS/FAIL evidence (and optionally a compact run summary) and verify readback; where permitted, pause the task and verify disabled state.
4. Record exact task/run IDs and task-history links where available.

## Phase D — independent audit

Read task details and last-run record without altering them. Compare observed stored prompt, run output, schedule, task ID, prompt generation and marker with the acceptance table in README. Link the run evidence in [evidence.md](evidence.md). Never claim a scheduler-triggered proof from `run_now` alone.

## Guardrails

- The experiment's continuation state is **only the task prompt**, not the repository.
- There is no hypothetical success: unavailable tool, denied edit, missing readback, wrong task ID or stale stage is a recorded **FAIL/BLOCKED**.
- Never modify an existing unrelated task or create additional tasks to disguise failure.
- Do not run a second execution while the first is still active; avoid overwrites.
- If scheduled-run tools are insufficient, stop and mark the capability gap; no external UI scripting or API key workarounds.
- On proven completion, pause the disposable task; if the agent cannot, the supervising interactive session should pause it after verifying both runs.
- Limit total recurring executions to avoid a runaway test. Do not silently let the task keep posting proof messages forever.

## Evidence classification

- **SETUP:** external interactive task update, trigger setup, or tool-discovery result.
- **P1-RUNNER:** run 1 launched through task runner, which self-edits its prompt and verifies readback.
- **P2-RUNNER:** separate task runner execution follows stored G1, quotes nonce and records G2.
- **P1-SCHEDULED / P2-SCHEDULED:** run history explicitly shows automatic scheduled trigger rather than a manual run-now request.
- **PASS (task-runner):** both P1-RUNNER and P2-RUNNER.
- **PASS (strict scheduled):** both executions were independently clock-triggered and gates P0–P4 pass.
- **PARTIAL/BLOCKED:** any missing gate, with exact evidence.
