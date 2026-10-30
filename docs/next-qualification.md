# Next qualification priorities

**Status:** Serial Native core continuation **PROVEN** in one bounded configuration; Serial Git two-scheduled-run continuation **UNVERIFIED**; crash/overlap recovery **UNVERIFIED**. See [post-restoration audit](../proving/post-restore-audit.md).

This remains deliberately a **single-agent serial** design. There is no multi-agent coordinator, automatic task spawning or browser extension. Do not reuse or reactivate the finished `Scheduserial Native Proof` task.

## Priority 1 — Prove Serial Git across scheduled executions

Use a **new disposable Git target** or a clearly isolated test branch with an initialized `handover.md`. The live continuation state must be Git, not the archived `proving/` evidence. Use one new, dedicated task and the [Serial Git bootstrap](../templates/serial-git-task.md).

- **First scheduled run:** fetch exact target source HEAD and handover blob SHA, do a harmless observable change, publish a successor handover to its **authoritative ref** using optimistic concurrency and verify remote readback.
- **Second scheduled run:** receive its instructions from that saved handover, consume a fresh marker generated in the first run, perform new bounded work and mark completion; disable and verify the disposable task.
- **Recovery test:** with a disposable file, deliberately attempt a stale-SHA update and demonstrate refusal rather than clobbering a newer handover.
- **Acceptance:** check G-01–G-08 in [verification](verification.md). Distinguish interactive setup, two independently scheduled executions and the actual remote Git publication step.

## Priority 2 — Serial Native negative-path qualification

Use **other disposable tasks**, not the original proof task. No external services or risky mutations are required for most failure-path scenarios.

- Wrong task ID or unexpected generation: refuse without editing any task.
- Missing task-management capability, denied update or absent readback: report `NEEDS_ATTENTION` and don't claim successful persistence.
- Truncated or corrupted continuation: preserve the fixed contract and stop rather than inventing state.
- Update succeeded but readback differs: stop; don't blindly overwrite.
- Stale generation or potential overlapping run: document a safe refusal path using isolated fixtures. **Do not deliberately race real scheduled workers** without a separate justified and controlled test plan.

**Until true exclusivity is established, a single task implies a logical serial worker, not a guaranteed mutex or exactly-once processing.**

## Priority 3 — Bounded soak and recovery usability

After negative paths are qualified, consider a separate capped **5–10-generation** Serial Native trial to check contract preservation, exact generation progression, schedule stability, complete run records and final self-disable. Keep the recurring schedule conservative and the goal harmless.

Produce a concise operating playbook: task-ID recovery, saved-prompt inspection, failed-run diagnosis, owner intervention for stuck tasks, and safe disable/pause. No secrets or private source data in handover prompts.

## Promotion gate

| Capability | Evidence required | Present status |
| --- | --- | --- |
| Serial Native core G0→G2 | Two independent scheduled executions, same-ID prompt updates/readback and self-pause | **PASS** |
| Serial Git scheduled continuation | Two separate scheduled runs, remote handover commits/readback, successor evidence | **PENDING** |
| Serial Native rejected-update / stale state | Real or isolated negative tests with fail-closed results | **PENDING** |
| Guaranteed single active execution | Platform guarantee or verified coordinated ownership primitive | **NOT ESTABLISHED** |
| Production-grade reliability | Recovery, long-run behaviour and clear owner controls | **NOT ESTABLISHED** |
