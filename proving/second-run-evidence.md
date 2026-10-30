# Serial Native — second scheduled execution acceptance

**Observed 30 October 2026 UTC. Core two-run proof: PASS.** This is an audit record only; the saved task prompt, not GitHub, was the continuation state.

- **Disposable task:** `6ae4d7275c348191a5b4b70dbd0cd95b` (`Scheduserial Native Proof`).
- **First execution:** run `d747258d-ff84-8325-ae99-5fdf6a3c522e`, scheduled for `18:00:00Z`. Its G0→G1 self-edit and readback were already recorded in [evidence.md](evidence.md); the task-history API later exposed a completed first-run result.
- **Second independent execution:** run `be50fba6-6310-8330-a848-d0fd4f3d111b`, scheduled for `19:00:00Z`, started at `19:00:24.958881Z`. At audit time, this run's history status was still `in_progress`; its mutation and readbacks had completed.
- **G1 instruction actually received and consumed:** `CONSUMED_G1=G1TBRTUHZX3ZRXXXK0IW7JZNEAQCJQB8OR2MGR`. The marker came from the second run's received G1 prompt, independently matched to live task readback before mutation; it was not sourced from a GitHub file or prior conversation.
- **G1→G2 prompt-only update:** task management confirmed success; saved task update timestamp `2026-10-30T19:00:55.933817+00:00`. Independent readback confirmed `STAGE=2`, `STATUS=COMPLETE`, same marker and consumed marker, same task ID, title, fixed contract, schedule, timezone and initially enabled state.
- **Fixed contract equality:** the entire G2 fixed contract compared byte-for-byte equal to the G0 prompt in [seed-prompt.md](seed-prompt.md); equality check returned true.
- **Termination:** second execution disabled the same task. Independent post-pause readback confirmed `is_enabled=false`, `STAGE=2` and exact marker, with update timestamp `2026-10-30T19:01:08.047965+00:00`.

**Qualification boundary:** P0–P4 of [protocol.md](protocol.md) passed for this two-scheduled-execution test; no manual run-now trigger was used. This demonstrates prompt self-editing and successor consumption in this bounded experiment, **not** transactional exclusivity, safe overlapping runs, stale-generation refusal, denied-update handling or long-term reliability. The second run's final delivery/completion status had not yet been recorded when audited.

The first execution's observed start time (`17:57:26Z`) precedes its nominal scheduled time (`18:00:00Z`); the schedule record, rather than a claim of exact wall-clock start, is cited.
