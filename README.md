# Scheduserial

**A minimal, single-agent continuation protocol for scheduled AI work.**

Scheduserial makes an ordinary recurring task useful across many independent executions. Every run reads the latest handover, does bounded substantive work, verifies its result, and leaves a precise continuation for the next run. **Serial only:** one project, one intended writer, one scheduled task. No multi-agent queue, orchestration service, browser extension or polling worker is required.

## Two persistence modes

| Mode | Source of next instructions | Best for | Maturity |
| --- | --- | --- | --- |
| **Serial Git** | A version-controlled `handover.md` in the target repository | Code, research and auditable projects | Design documented; end-to-end scheduled-run trial pending |
| **Serial Native** | The scheduled task's *own prompt*, replaced after each run | Repo-free, lightweight recurring work | **Two-run core proven:** separately scheduled executions completed G0→G1→G2 and verified pause; concurrency/fault handling remain untested |

Neither mode guarantees that the platform prevents overlapping executions. A single scheduled task is a *single logical writer*, not automatically a distributed lock. Use bounded work, explicit ownership checks and a sufficient interval; see the validation plan before unattended reliance.

## How it works

1. The scheduled task activates the agent.
2. The agent reads the current instructions, checks actual state and any repo/task policy, and selects bounded work.
3. The agent implements or investigates, tests what can be tested, and records precise evidence and unresolved risks.
4. The agent **persists and verifies** the next handover: a Git commit in Serial Git, or an update to the *same scheduled task* in Serial Native.
5. The next scheduled execution repeats from the verified state. On completion or unrecoverable blockage, the task pauses or requests human intervention rather than looping aimlessly.

**The handover is a continuation instruction, not a substitute for live reconciliation.** Existing commits, issues, PRs, checks and tool availability may have changed since it was written.

## Start here

- [Design and decision rationale](docs/design.md)
- [Serial Git protocol](docs/serial-git.md) and [handover template](templates/handover.md)
- [Serial Native protocol](docs/serial-native.md)
- [Trial plan, success criteria and failure injection](docs/verification.md)
- [Copyable Serial Git scheduled-task prompt](templates/serial-git-task.md)
- [Copyable Serial Native scheduled-task prompt](templates/serial-native-task.md)
- [External references and evidence status](docs/references.md)
- [Serial Native live proving experiment and evidence ledger](proving/README.md)

## Guardrails

- Preserve an immutable-in-spirit operating contract: permissions, scope, verification, stop conditions and handover procedure.
- Recheck live reality each run. Do not promote an intended action into a verified result.
- Never overwrite another active writer's work or bypass repository branch protection, code-review or release gates.
- Preserve evidence such as commit SHAs, PRs, CI run links, and exact blockers. Do not put secrets into Git or task prompts.
- A failed handover write is **not** a successful continuation. Report the failure and do not claim the next run was prepared.
- Human approval remains mandatory where required; scheduled execution does not grant additional permissions.
- Stop when the goal is complete. Avoid self-generating meaningless new work.

## Status

**30 October 2026:** A disposable Serial Native task passed the core two-execution scheduled proof: G0→G1 self-edit, G1 consumed by a separate execution, G1→G2 edit and verified self-pause. [Evidence](proving/evidence.md). Fault handling and exclusive execution remain unqualified. Serial Git is not yet verified.

## Scope

This project is deliberately separate from [Scheduswarm](https://github.com/techrote/scheduswarm), which explores more complex orchestration. Multi-agent concurrency, lane assignment and browser automation are **out of scope** for Scheduserial's minimal design.

## References

See [references](docs/references.md) for current OpenAI Scheduled Tasks guidance and GitHub's documented file update semantics.
