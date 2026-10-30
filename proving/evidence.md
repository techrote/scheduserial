# Native proving evidence ledger

**Status:** TASK CREATED / G0 PINNED — no self-edit or successive scheduled-run proof observed yet.

Only append or correct entries with evidence that can be traced to the saved task record or actual execution history. A task's internal statement of success without independently observing updated task state is **not** sufficient.

## Test identity

| Field | Observed value |
| --- | --- |
| Repository | `techrote/scheduserial` |
| Protocol | [protocol.md](protocol.md) |
| Test start date | 2026-10-30 (UTC) |
| Disposable task name | `Scheduserial Native Proof` |
| Task ID | `6ae4d7275c348191a5b4b70dbd0cd95b` |
| Schedule and timezone | `DTSTART:20261030T180000; RRULE:FREQ=HOURLY;COUNT=3` (Europe/London) |
| Baseline generation | 0 (planned) |
| Current saved generation | **0**, read back after interactive setup update |
| Current run status | No executions at setup readback; task reports `last_run=null` |
| Current verdict | NOT PROVEN |

## Execution records

| Gate | Trigger type | Run/time and evidence | Verdict |
| --- | --- | --- | --- |
| P0 task created/readback | Interactive setup | Task `6ae4d7275c348191a5b4b70dbd0cd95b`; latest setup readback `2026-10-30T17:43:42.294241+00:00`; `STAGE=0`, id pinned, `NONCE=NOT_GENERATED`; schedule unchanged | **PASS (setup only)** |
| P1 self-edit G0→G1 | Runner (manual or scheduled, label precisely) | Not yet observed | PENDING |
| P2 task readback G1 | Independent read | Not yet observed | PENDING |
| P3 second execution follows G1 | Runner (manual or scheduled) | Not yet observed | PENDING |
| P4 G2/pause/readback | Task runner / supervisor | Not yet observed | PENDING |

## Negative evidence and limitations

- No task execution exists yet in task readback at setup; `last_run=null` and `latest_result=null`. No self-edit proof.
- The creation prompt originally contained the placeholder `TASK_ID=PIN_AFTER_CREATION`; the supervising interactive chat replaced it with the actual returned ID and verified the post-setup prompt. **That supervised update is not the self-edit being tested.**
- The schedule includes a maximum of three hourly occurrences, intended for **18:00, 19:00, and 20:00 London time on 2026-10-30**; these are planned triggers, not evidence of execution. The task readback did not yet provide a concrete `next_run_time`.
- Task prompt editing in an **interactive** session does not establish that a **scheduled** execution has the same tool access.
- Two `run_now` calls, even if successful, do not independently prove automatic recurrence.

## Recovery / closeout

If the task is created but the test fails, record the task ID, last observed status and precise blocker. Pause the disposable task after it is no longer useful or after explicit failure, without altering unrelated tasks. Distinguish any supervisor intervention from actual autonomous self-editing.
