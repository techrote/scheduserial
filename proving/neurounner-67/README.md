# Neurounner #67 — Serial Native production proof

**Owner-authorized continuation (31 Oct 2026, 01:05 UTC):** After the bounded two-run proof, the owner explicitly converted the **same existing task** to an **open-ended hourly Serial Native continuation** under the v2 operating contract. This does not retroactively extend the proof's observation count or change the historical G0/G1 evidence. See [open-ended continuation setup](open-ended-continuation.md). The task was enabled at its final saved STAGE=2, with first new planned trigger at 02:00 GMT, and no COUNT/UNTIL in its schedule.

**Final outcome (31 Oct 2026): PASS.** Two distinct clock-scheduled source/engineering runs (G0 and G1) advanced the *same* saved task prompt to G2 and verified the task disabled. Both Neurounner PRs remain draft/unmerged and all scientific/training gates remain closed. See the [source-linked execution ledger](evidence.md) and [draft #223](https://github.com/techrote/neurounner/pull/223)/[draft #224](https://github.com/techrote/neurounner/pull/224).\n\n**Historical status at setup (30 Oct 2026):** configured, **not yet executed**. This is a real-project continuation pilot, not a purely synthetic nonce test. The source of continuation instructions is exclusively the **saved prompt of one scheduled ChatGPT task**. This GitHub directory is a non-authoritative audit archive only.

## Test identity

| Field | Value |
| --- | --- |
| Target epic | [Neurounner NCR-001 #67](https://github.com/techrote/neurounner/issues/67) |
| Scheduled task | `Neurounner Serial Proof` |
| Exact task ID | `6ae51d0429e48191b27f6b540ab8a976` |
| Timezone | `Europe/London` |
| Schedule | `DTSTART:20261030T230000`; `RRULE:FREQ=HOURLY;COUNT=4` |
| Initial status | `STAGE=0`, `PROOF_PROGRESS_COUNT=0`, enabled |
| First planned trigger | 2026-10-30 23:00 GMT |
| Second planned trigger | 2026-10-31 00:00 GMT |
| Remaining safety triggers | 2026-10-31 01:00/02:00 GMT |
| First task observation | No run recorded at setup readback; no automatic execution proven yet |

A task may be dispatched slightly before or after the nominal time. Record **actual** run timestamps; do not infer that setup guarantees start to the minute.

## Live context at setup (historical checkpoint only)

- Main `techrote/neurounner` was `12f7bf0475aefb61227f676ea377134734fa5072` when audited; the agent must fetch current authority again at execution.
- [Issue #213](https://github.com/techrote/neurounner/issues/213) and `SCHEDUSWARM.md` v2 enforce coordination and budget: max 3 active lanes, concurrency budget 2, and no simultaneous shared integration writes. The explicit separately owned merge-down NCR-MERGEDOWN-4 concerns Sprocket Chat PRs #191/#192; the void.1 #220/#221/#222 source/physical/custody lane reported released.
- The four-model `#72` scientific admission and `#73` matched training compute remain unqualified. In particular `train_authorized=false`, `full_72_conformance_pass=false`, `actual_compute_budget_qualified=false`. Task is prohibited from elevating them.
- All earlier Neurounner continuation automations observed in the private task lookup were disabled; **this is a new, separately requested task**, not a reactivation.
- No source mutation, scientific admission or merge was performed by this setup.

## Core proof acceptance

1. **G0 work:** first real clock-scheduled run uses issue/PR/CI/source evidence, coordinates a non-colliding write set, makes one *substantive* source/test/provenance correction or bounded review, preserves exact evidence, generates a novel nonce, self-updates its own task prompt to G1 and independently reads it back.
2. **G1 work:** second **independent clock-triggered run** reads the G1 instructions (not this repo file), prints `CONSUMED_PRIOR_NONCE=...`, checks previous Git evidence against actual GitHub, performs a separate verifiable unit of work and advances to G2 on the SAME task with readback.
3. **Terminal state:** task marks `STATUS=COMPLETE`, pauses itself and independently verifies disabled status. A cap of four hourly occurrences bounds unexpected behavior but is not a substitute for verified pause.
4. **No invented progress:** a task record self-edit with no substantive project progress is a **continuation-mechanism-only** result, not a successful **production** proof. A GitHub green badge on an unrelated head, a source-only audit represented as a physical model run, or unapproved experimental gate promotion fails the acceptance.
5. **Safety:** if issue #213 reveals two active conflicting lanes or if mandatory scientific/review requirements cannot be honored, stop/record a concrete blocker rather than racing writers. Existing draft PRs are not automatically mergeable.

## Evidence and authority

- [Exact initial saved prompt](seed-prompt.md), archived **after interactive task-ID pinning**. This setup-only pinning is not an agent self-edit.
- [Execution ledger](evidence.md), initially pending. Do not fill it from intended outcomes.
- [Scheduserial design](../../docs/serial-native.md) and [earlier disposable proof](../post-restore-audit.md).

**Do not use this directory as a handover queue.** On each future run the agent must obtain its instructions from the scheduled task's own current saved prompt, reconcile Neurounner's live repository, then write the next instructions back into that same task.
