# Neurounner #67 Serial Native execution ledger

**Status:** SETUP VERIFIED — **production proof NOT YET PASSED**. Created 2026-10-30T22:41:40.410571+00:00. The initial task record had no recorded run.

| Phase | Required independent evidence | Status |
| --- | --- | --- |
| P0 | One finite scheduled task, exact ID, correct full G0 prompt and schedule read back | **PASS (interactive setup)** |
| P1 | Clock-scheduled G0 does useful source-bound #67 work, claims/releases safe ownership, persists G1 with new nonce and exact readback | **PENDING** |
| P2 | Separate clock-scheduled G1 consumes previous nonce **from saved prompt**, rechecks actual previous artifact and does new substantive work | **PENDING** |
| P3 | Same task updated to G2 COMPLETE, fixed contract/schedule preserved, task paused/readback disabled | **PENDING** |
| Scientific policy | No training/heldouts/admission or main merge, no conflict with another owner | **TO VERIFY EACH RUN** |

## Baseline

- Task ID: `6ae51d0429e48191b27f6b540ab8a976`
- Initial stored generation: `0`; progress count `0`
- Initial scheduled RRULE: `FREQ=HOURLY;COUNT=4`
- No run ID or work artifact existed at setup. **Do not fabricate either.**
- Setup Neurounner `main`: `12f7bf0475aefb61227f676ea377134734fa5072` (historical, refresh).
- Original fixed contract and full initial prompt: [seed-prompt.md](seed-prompt.md).
- Existing manually-owned Sprocket Chat #191/#192 lane was recorded in [issue #213](https://github.com/techrote/neurounner/issues/213); avoid collision.

## Run 1 — PENDING

Run ID/time: **Not yet observed.**  
Substantive source/test/PR/CI evidence: **Not yet observed.**  
New nonce and independent G1 readback: **Not yet observed.**  
Owned lane claim/release: **Not yet observed.**

## Run 2 — PENDING

Run ID/time: **Not yet observed.**  
Consumed prior nonce: **Not yet observed.**  
Second substantive result and G2 readback: **Not yet observed.**  
Task pause/disabled readback: **Not yet observed.**

## Failure and recovery record

No test failures observed at setup. Later agents/auditors should preserve raw negative facts, exact tool errors and source-matched run URLs rather than overwriting this ledger with a generic PASS.

If all scheduled occurrences expire before a two-generation production proof, mark PARTIAL or FAIL with exact observed evidence. Do not automatically create a replacement scheduled task.


## G0 source-linked completion — 30 Oct 2026 (23:02 UTC task readback)

**P1 PASS: one substantive project run and self-persisted successor.** This is **not P2** and not a completed two-trigger Serial Native production proof.

- Scheduled task ID `6ae51d0429e48191b27f6b540ab8a976` original clock-triggered first run was observed as `7954f600-67a0-832c-886e-f5f53c403951`; that same task, not a successor task, now saves `STAGE=1`, `PROOF_PROGRESS_COUNT=1`, a new one-time alphanumeric continuation nonce, and the next independently executable objective. Readback at `2026-10-30T23:02:20.043408+00:00` confirmed the exact updated full prompt, unchanged fixed operating contract, original schedule/timezone/title and enabled status. **The nonce is retained in the task prompt, not this repository; this file is never continuation authority.**
- Freshly audited Neurounner `main` `12f7bf0475aefb61227f676ea377134734fa5072`; existing [#213 Scheduswarm coordination](https://github.com/techrote/neurounner/issues/213) showed one remaining claimed NCR-MERGEDOWN-4 integration lane and an explicitly released void.1 physical lane. New G0 exact source-only write-set [claimed #6535268757](https://github.com/techrote/neurounner/issues/213#issuecomment-6535268757) and [released #6535323761](https://github.com/techrote/neurounner/issues/213#issuecomment-6535323761).
- Substantive four-file implementation on **new, nonshared, unmerged draft** [Neurounner PR #223](https://github.com/techrote/neurounner/pull/223): original eight removable Python `assert` checks for nine preregistered NCA/optimizer/bottleneck invariants were replaced by type-strict unconditional runtime refusal; new ten temporary-protocol adversarial sentinels; dedicated CI in ordinary and `python3 -O` modes; source-only explanatory note. Exact final PR/commit `d1b86e1c20cf6079f8e2bc3463e4ebc34f48f6b7`, original intermediate implementation commit `b46686d912610f93c67f77249c07f625fb4404af`. Original main, source/fixture pins, weights, raw ZIP/logs and held-outs unchanged.
- [Final exact-head GitHub Actions run #41141734057](https://github.com/techrote/neurounner/actions/runs/41141734057), job `124357383922` **SUCCESS**: 11/11 ordinary + 11/11 optimized unittest methods, including all ten tampered protocol refusals; compiled source; original 7,204-byte plan SHA-256 reproduced unchanged `f906206cfde550625512efe4c5af2f2add1a281a17c9cd3fff16991d95f17ed0`. Transient derived artifact `#13019340544` digest `sha256:735e1c43b8084238325f588bacffdff0ba8528db5d28c1bcaec88b8c523616cb`; raw full log held by Actions, and one nonfatal NumPy import warning remains visible. Previous implementation-head [#41141655669](https://github.com/techrote/neurounner/actions/runs/41141655669) likewise **SUCCESS**, not substituted for final CI.
- Exact-head [same-account COMMENTED review #5719591351](https://github.com/techrote/neurounner/pull/223#pullrequestreview-5719591351) and durable [#73 comment #6535321327](https://github.com/techrote/neurounner/issues/73#issuecomment-6535321327). No GitHub APPROVED review and no independent-person scientific admission is claimed.
- **Strict scientific status:** Source-only planner integrity improved; `train_authorized=false`, `full_72_conformance_pass=false`, `actual_compute_budget_qualified=false` remain, with no model inference/training/heldouts/merges. #223 intentionally remains DRAFT and open.

**Next needed independent proof:** a distinct later clock-scheduled G1 execution must consume the nonce from the task's own prompt, reverify these actual source/CI links, do a second genuinely substantive unowned #67 task, update the same task prompt to G2 and self-pause with readback. No G1 continuation consumption, completion or disabled-state evidence exists at this archive point.
