# Native proving evidence ledger

**Status:** **CORE TWO-SCHEDULED-RUN PROOF PASSED:** G0→G1→G2, successor marker consumption, independent readbacks and task self-pause. See [second-run acceptance](second-run-evidence.md).

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
| Current saved generation | **2**, independently read back after the second scheduled execution |
| Current run status | First execution completed; second run `be50fba6-6310-8330-a848-d0fd4f3d111b` **completed at `2026-10-30T19:05:45.421572Z`**; final stored prompt **STAGE=2**, task **disabled** (verified after repository restoration) |
| Current verdict | **PASS — core two-run scheduled continuation; broader fault-injection/overlap qualification outstanding** |

## Execution records

| Gate | Trigger type | Run/time and evidence | Verdict |
| --- | --- | --- | --- |
| P0 task created/readback | Interactive setup | Task `6ae4d7275c348191a5b4b70dbd0cd95b`; latest setup readback `2026-10-30T17:43:42.294241+00:00`; `STAGE=0`, id pinned, `NONCE=NOT_GENERATED`; schedule unchanged | **PASS (setup only)** |
| P1 self-edit G0→G1 | Scheduled execution | Run `d747258d-ff84-8325-ae99-5fdf6a3c522e` started `2026-10-30T17:57:26.276165Z`; runner executed task prompt mutation on same ID, tool confirmed update; G1 prompt readback `2026-10-30T17:58:18.279237+00:00`; nonce `G1TBRTUHZX3ZRXXXK0IW7JZNEAQCJQB8OR2MGR` | **PASS (first run, runner self-edit)** |
| P2 task readback G1 | Independent task-manager read | `STAGE=1`, exact nonce, same task/title, byte-identical fixed contract and unchanged schedule/timezone/enabled; second read after mutation reconfirmed it | **PASS** |
| P3 second execution follows G1 | Independent scheduled execution | Run `be50fba6-6310-8330-a848-d0fd4f3d111b`, scheduled `2026-10-30T19:00:00Z`, consumed `CONSUMED_G1=G1TBRTUHZX3ZRXXXK0IW7JZNEAQCJQB8OR2MGR` from G1 | **PASS** |
| P4 G2/pause/readback | Second scheduled task execution | G2 update at `19:00:55Z`; readback verified G2, exact fixed-contract equality with G0, task ID/title/schedule/timezone; self-disabled and readback verified at `19:01:08Z`. [Full acceptance](second-run-evidence.md) | **PASS** |

## Negative evidence and limitations

- At the **original contemporaneous audit**, the second run had already advanced G1→G2 and disabled the task but its history entry remained `in_progress` pending completion bookkeeping. At the **post-restoration audit on 2026-10-30**, its task-history entry was **completed**, scheduled for `19:00:00Z`, started `19:00:24.958881Z`, completed `19:05:45.421572Z`; its saved G2 prompt and disabled state still matched the original evidence. See [post-restoration readback](post-restore-audit.md).
- First-run marker was generated during the scheduled execution and was absent from G0. Runner updated **only** the saved prompt; a separate task-management readback verified the exact G1 replacement and unchanged fixed contract, ID, schedule, title, timezone and enabled state.
- First run was scheduled for 18:00 UTC and observed as started at 17:57:26 UTC, slightly before the nominal scheduled time; record actual timestamps rather than claiming it ran precisely at 18:00.
- The creation prompt originally contained the placeholder `TASK_ID=PIN_AFTER_CREATION`; the supervising interactive chat replaced it with the actual returned ID and verified the post-setup prompt. **That supervised update is not the self-edit being tested.**
- The schedule includes a maximum of three hourly occurrences, intended for **18:00, 19:00, and 20:00 London time on 2026-10-30**; these are planned triggers, not evidence of execution. The task readback did not yet provide a concrete `next_run_time`.
- Both observed prompt changes occurred inside distinct scheduled task executions, not the interactive setup session. This proves this bounded self-edit/successor scenario, not platform-wide availability or safe concurrent updates.
- Two `run_now` calls, even if successful, do not independently prove automatic recurrence.

## Recovery / closeout

The task was disabled by its second scheduled execution and independently read back disabled. The first-run and second-run IDs, prompt-generation progression and remaining qualification limitations are recorded in [second-run-evidence.md](second-run-evidence.md). No further test execution is required for this bounded proof.
