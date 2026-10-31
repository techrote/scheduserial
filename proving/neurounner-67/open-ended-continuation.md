# Neurounner #67 — owner-authorized open-ended Serial Native continuation

**Recorded:** 31 October 2026, 01:05 UTC.  
**Current intent:** indefinite **hourly scheduled** single logical agent, with owner review roughly every 4–12 hours.  
**Note:** This is a **setup/readback record**, not evidence that any post-proof execution has yet occurred.

## Owner decision and historical transition

The owner clarified that the earlier finite `Neurounner Serial Proof` was intended as a genuine ongoing Neurounner #67 continuation. Instead of creating another task, the original scheduled task was explicitly reconfigured **in place** after the successful G0/G1 production proof. The original complete [two-run archive](evidence.md), draft PRs #223/#224 and Git/CI claims remain historical evidence.

| Field | Verified immediately after update |
| --- | --- |
| Existing task ID | `6ae51d0429e48191b27f6b540ab8a976` |
| Display title | `Neurounner Serial Proof` (unchanged) |
| Fixed contract | `SCHEDUSERIAL / NEUROUNNER-67 — OPEN-ENDED SERIAL CONTRACT v2` |
| Owner-authorized contract migration | v1 terminal G2 → v2 ready G2 (setup edit, **not** a model-initiated handover) |
| Task status | **Enabled** (`is_enabled=true`) |
| Schedule | `BEGIN:VEVENT\nDTSTART:20261031T020000\nRRULE:FREQ=HOURLY\nEND:VEVENT` |
| Timezone | `Europe/London` |
| Finite end | **None**: `COUNT=4` removed; no `UNTIL` |
| Initial resumed state | `STAGE=2`, `STATUS=READY__OWNER_PROMOTED_TO_OPEN_ENDED`, 2 preceding verified substantive runs |
| Last completed run before restart | `1c3c2cbd-b7ec-8321-88ee-f245143488fd`, G1 completed at 2026-10-31 00:08:12.646001Z |
| Last observed task update | `2026-10-31T01:05:13.155379+00:00` |
| V2 prompt length | 7,062 characters, including 1,269-character initial mutable continuation (1,243 excluding its delimiter) |
| First new planned trigger | 2026-10-31 **02:00 GMT** — planned, **not observed** at this record's creation |

The task manager returned a successful update and a subsequent **independent readback** matched the new fixed-contract header, task identity, STAGE=2 state, unchanged title/timezone, enabled status, and unbounded hourly recurrence. Its `next_run_time` field was null at that inspection; **the schedule**, not a returned estimated next-run timestamp, is the basis of the planned 02:00 trigger.

**The saved task prompt remains the sole authoritative next-instruction state.** Do **not** treat this audit file as a handover or overwrite the task based on a stale copy of it. For recovery, inspect the actual task by exact ID and reconcile current GitHub source and issue authority.

## Changes from the bounded proof

- Replaced the obsolete two-run terminal rule with an **open-ended** contract. There is no predetermined stop after two or four generations; human pause, verified #67 completion or a hard unsafe state are terminal conditions.
- New v2 contract is shorter and requires **compact mutable checkpoints** (target at most 1,500 characters), source-linked GitHub evidence and idempotent recovery after interruptions.
- Previous task-created draft PRs [#223](https://github.com/techrote/neurounner/pull/223) and [#224](https://github.com/techrote/neurounner/pull/224) remain **draft/unmerged**. A soft limit of **four task-created open draft PRs** pushes future executions toward review, repair and integration-readiness evidence rather than generating indefinite PR backlog.
- Every run checks owner claims and coordinates through [Neurounner #213](https://github.com/techrote/neurounner/issues/213) before writing project source; one logical worker is **not a concurrency lock**.
- If no safe progress exists: record a meaningful WAITING/RETRY state rather than fabricating a new PR or declaring the whole project complete. Pause the task only for hard safety/state failures or verified owner-authorized completion.
- The existing scientific restrictions remain **closed**: `train_authorized=false`, `full_72_conformance_pass=false`, `actual_compute_budget_qualified=false`. No comparative NCA/MLP training, sealed heldouts, unapproved physical host jobs, protocol/pin/fixture modification, or merges to `main` without separately established authorization.
- No new scheduled tasks, other task edits, Scheduswarm queue mutations, Neurounner code edits or manual run-now dispatch occurred during this conversion.

## Monitoring and recovery guidance

The owner expects to check results at intervals of around 4–12 hours. When auditing, read the **live task record** first: `is_enabled`, current STAGE, run history, fixed-contract continuity, last result, and scheduled recurrence. Independently recheck Neurounner #67/#72/#73/#213, new draft PRs and exact-head CI.

If the task becomes disabled unexpectedly, a prior execution is still active, the prompt is corrupted or the last Git side effect is ambiguous, **do not blindly re-enable or replay**. Reconcile the exact last commit/branch/PR first. The task's new contract explicitly permits refusing unsafe work and owner intervention.

No long-horizon uptime or recovery claim is made here. The two-run proof remains valid but does not establish weeks-long reliability.
