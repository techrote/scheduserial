# Serial Native — independent post-restoration audit

**Audit date:** 2026-10-30 UTC  
**Verdict:** **PASS for bounded two-scheduled-execution self-edit/continuation.** No claim of conflict safety, exactly-once execution or long-term reliability.

## Recovery and repository identity

The owner deleted and then restored `techrote/scheduserial`. An authenticated repository read confirmed the original **repository ID `1440030988`**, `main`, and original proof history. The readback before documentation reconciliation observed `main` at [`e081000d0a8146bf10a21eece27959dcbd3ded69`](https://github.com/techrote/scheduserial/commit/e081000d0a8146bf10a21eece27959dcbd3ded69). The earlier [G0 self-edit evidence commit](https://github.com/techrote/scheduserial/commit/9a8caa620f484d3ca2c1e4e56009075e0c2b9386) and [G0 setup commit](https://github.com/techrote/scheduserial/commit/ddcf7bb2401575cf565ab318510ab7b34b4f5967) remained accessible. No open PRs or issues were found; the repository had no GitHub Actions workflow runs. GitHub CI is **not** evidence of scheduled-task execution.

## Independent task-manager readback

| Property | Observed state |
| --- | --- |
| Disposable task | `6ae4d7275c348191a5b4b70dbd0cd95b` (`Scheduserial Native Proof`) |
| Enabled | `false` — disabled; **not reactivated** |
| Final saved prompt | `STAGE=2`, `STATUS=COMPLETE` |
| Generated marker | `G1TBRTUHZX3ZRXXXK0IW7JZNEAQCJQB8OR2MGR` |
| Consumed marker in G2 | `CONSUMED_G1=G1TBRTUHZX3ZRXXXK0IW7JZNEAQCJQB8OR2MGR` |
| Fixed contract | Saved G2 fixed contract matched the [G0 seed](seed-prompt.md) **exactly** in an independent text comparison |
| Fresh marker check | The generated G1 marker was **absent** from the G0 seed prompt |
| Schedule | Unchanged `DTSTART:20261030T180000; RRULE:FREQ=HOURLY;COUNT=3`; `Europe/London` |
| Last task update timestamp | `2026-10-30T19:06:52.879787+00:00` |
| Second scheduled run ID | `be50fba6-6310-8330-a848-d0fd4f3d111b` |
| Scheduled for | `2026-10-30T19:00:00Z` |
| Started | `2026-10-30T19:00:24.958881Z` |
| Completed | `2026-10-30T19:05:45.421572Z` |
| Recorded status | **`completed`** (previous contemporaneous audit had observed `in_progress`) |

The second run's saved result explicitly reported consuming the G1 marker, advancing to G2, readback and self-pause. This was a **different** scheduled execution from the first G0→G1 run, which is recorded with its own run ID and observed start/readback times in [the original ledger](evidence.md).

## Scientific interpretation

- **Proved within the tested configuration:** a clock-scheduled execution replaced **its own** task's stored prompt; a later independently scheduled execution followed the new instructions, reproduced the first-run nonce, advanced the same task to G2 and disabled it. Task history now also confirms second-run completion.
- **Historical reconciliation:** the contemporaneous [second-run evidence](second-run-evidence.md) said its run history was still `in_progress`. That was true **at that time** but is superseded by the fresh completed-run readback. The original observation remains preserved.
- **Unproven:** scheduler-exclusive execution, update compare-and-swap, denied-write recovery, interrupted-run idempotence, prompt truncation or corruption handling, arbitrary-account portability and long-duration reliability.
- **No new proof run or task was created.** The original disposable task remains disabled. The repository is an audit archive, not the Serial Native continuation state.

## Next actions

Do **not** reactivate the finished proof task. Follow [next qualification priorities](../docs/next-qualification.md) for a distinct Serial Git end-to-end test and bounded negative-path qualification.
