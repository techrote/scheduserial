# Neurounner older-PR merge-down — Serial Native

**Setup:** 31 October 2026, approximately 04:43 GMT. **Status at setup: PENDING FIRST RUN.**

This folder is a human-readable audit archive for a separate, scheduled, **single-logical-worker** task that evaluates older Neurounner PRs and performs guarded merges of those that genuinely qualify. The **same task's saved prompt** is the ONLY authority for continuation; do not read a successor prompt from this GitHub folder or mistake source-audit notes for task state.

## Identity and scope

| Item | Value |
| --- | --- |
| Target | [techrote/neurounner](https://github.com/techrote/neurounner) — 45 open PRs at initial audit |
| Task name | `Neurounner PR Merge-Down` |
| Task ID | `6ae571c1f6ac8191a767bbbafa3c3bcd` |
| Initial stage | `0`, READY |
| Initial task state | Enabled, no execution yet recorded |
| Schedule | `DTSTART:20261031T053000; RRULE:FREQ=HOURLY` |
| Timezone | `Europe/London` |
| First planned run | 2026-10-31 **05:30 GMT**, not an observed run |
| Other ongoing task | `Neurounner Serial Proof` `6ae51d0429e48191b27f6b540ab8a976`, hourly at :00; leave its task and its active PRs #223/#224 unchanged |
| Initial main SHA | `12f7bf0475aefb61227f676ea377134734fa5072` (historical setup snapshot, **reverify** before any merge) |
| Owner coordination | [Neurounner issue #213 notice](https://github.com/techrote/neurounner/issues/213#issuecomment-6539153028) |

This is not Scheduswarm v2 automatic dispatch. Each actual scheduled execution must respect the project concurrency budget, live issue #213 claims, source/issue authority and the independent NCR-001 experimental gates.

## Merge acceptance

**The owner's request authorizes guarded merges only after substantive evidence-based eligibility review.** A stored draft is not automatically merge-ready and source-only green CI is not model-scientific admission. For each old PR: reconstruct source and stack ancestry, check current `main`, preserve original raw receipt/archive/negative evidence, inspect reviews and unresolved threads, validate the complete current-main integration composition, and merge only with an exact expected PR head and postmerge verification. No force-push of historic source refs. Work through dependent stages in order where safe.

Some old PRs are held for independent scientific review, and all four frozen NCR model lanes remain separate. Preserve `train_authorized=false`, `full_72_conformance_pass=false`, `actual_compute_budget_qualified=false`, sealed held-outs and original pin/fixture/hash authority. Never infer that a same-account COMMENTED review equals an APPROVED review or a distinct scientist.

The previous historical NCR-MERGEDOWN-4 #191/#192 claim lacks a release note, but the original declared PRs were found **merged** by GitHub API: #191 merge `06e2e69ec1014c35731388f25fe1d105eae4212e`, #192 merge `12f7bf0475aefb61227f676ea377134734fa5072`. This is a factual checkpoint, not a fabricated release or proof that no other integration worker is active. Each run must reconcile again.

## Audit material

- [Exact generation-0 saved task prompt](seed-prompt.md) — copy after initial task-ID pinning and before first execution; **not continuation authority**.
- [Execution ledger](evidence.md) — append actual scheduled runs, reviewed candidates, guard/review/CI outcomes, merges, safe holds and task updates.
- [Neurounner coordination issue](https://github.com/techrote/neurounner/issues/213) — live ownership claims, release and merge decisions.

When no safe merge exists, prefer a detailed backlog classification and actionable owner decision over a false-positive merge. A task may pause after genuinely clearing the eligible backlog or when a hard safety issue prevents unattended continuation. Owner can pause at any time.

**No merge, code edit, PR readiness transition or task execution has occurred as part of this setup archive.**
