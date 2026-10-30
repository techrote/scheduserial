# Native proving evidence ledger

**Status:** G0→G1 SELF-EDIT VERIFIED — successor execution and G1→G2 still pending.

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
| Current saved generation | **1**, read back after self-edit from scheduled task execution |
| Current run status | First task execution `d747258d-ff84-8325-ae99-5fdf6a3c522e`, status `in_progress` at evidence write; started `2026-10-30T17:57:26.276165Z`, scheduled for `2026-10-30T18:00:00Z` |
| Current verdict | NOT PROVEN |

## Execution records

| Gate | Trigger type | Run/time and evidence | Verdict |
| --- | --- | --- | --- |
| P0 task created/readback | Interactive setup | Task `6ae4d7275c348191a5b4b70dbd0cd95b`; latest setup readback `2026-10-30T17:43:42.294241+00:00`; `STAGE=0`, id pinned, `NONCE=NOT_GENERATED`; schedule unchanged | **PASS (setup only)** |
| P1 self-edit G0→G1 | Scheduled execution | Run `d747258d-ff84-8325-ae99-5fdf6a3c522e` started `2026-10-30T17:57:26.276165Z`; runner executed task prompt mutation on same ID, tool confirmed update; G1 prompt readback `2026-10-30T17:58:18.279237+00:00`; nonce `G1TBRTUHZX3ZRXXXK0IW7JZNEAQCJQB8OR2MGR` | **PASS (first run, runner self-edit)** |
| P2 task readback G1 | Independent task-manager read | `STAGE=1`, exact nonce, same task/title, byte-identical fixed contract and unchanged schedule/timezone/enabled; second read after mutation reconfirmed it | **PASS** |
| P3 second execution follows G1 | Runner (manual or scheduled) | Not yet observed | PENDING |
| P4 G2/pause/readback | Task runner / supervisor | Not yet observed | PENDING |

## Negative evidence and limitations

- Initial setup had `last_run=null`. First task-run execution is now recorded; task history still reports its run as `in_progress` at evidence write. The separate successor run is not yet observed.
- First-run marker was generated during the scheduled execution and was absent from G0. Runner updated **only** the saved prompt; a separate task-management readback verified the exact G1 replacement and unchanged fixed contract, ID, schedule, title, timezone and enabled state.
- First run was scheduled for 18:00 UTC and observed as started at 17:57:26 UTC, slightly before the nominal scheduled time; record actual timestamps rather than claiming it ran precisely at 18:00.
- The creation prompt originally contained the placeholder `TASK_ID=PIN_AFTER_CREATION`; the supervising interactive chat replaced it with the actual returned ID and verified the post-setup prompt. **That supervised update is not the self-edit being tested.**
- The schedule includes a maximum of three hourly occurrences, intended for **18:00, 19:00, and 20:00 London time on 2026-10-30**; these are planned triggers, not evidence of execution. The task readback did not yet provide a concrete `next_run_time`.
- Task prompt editing in an **interactive** session does not establish that a **scheduled** execution has the same tool access.
- Two `run_now` calls, even if successful, do not independently prove automatic recurrence.

## Recovery / closeout

If the task is created but the test fails, record the task ID, last observed status and precise blocker. Pause the disposable task after it is no longer useful or after explicit failure, without altering unrelated tasks. Distinguish any supervisor intervention from actual autonomous self-editing.
