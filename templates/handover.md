# [PROJECT] — serial handover

> **Template only.** Copy this file to `handover.md` in the **target project repository**. Replace all bracketed placeholders. This file is not a live handover for Scheduserial itself.

## Control

| Field | Value |
| --- | --- |
| Mode | Serial Git |
| Target repository | [owner/repo] |
| Authoritative branch | [main or approved dedicated handover ref] |
| Status | READY |
| Generation | 0 |
| Last run ID and timestamp (UTC) | [none yet] |
| Current owner / RUNNING claim | [none; if claimed, identify run and UTC claim time] |
| Last project source HEAD inspected | [exact commit SHA, or initial state] |
| Last handover **blob** SHA read | [record externally at start/readback; do not assume this text can contain its own commit SHA] |
| Next authorized write path | [direct commit / PR + required merge gate / other approved path] |

Statuses: **READY** / **RUNNING** / **BLOCKED** / **NEEDS_ATTENTION** / **COMPLETE**.

A RUNNING marker by itself is **not** an exclusive lock. If a different run may be active, halt modifications and reconcile before changing ownership.

## Goal and scope

**Owner objective:** [What outcome is wanted, with clear bounds.]

**Acceptance / completion criteria:** [Evidence required to declare done.]

**Non-goals / prohibitions:** [Actions and scope explicitly excluded.]

**Applicable instructions:** [AGENTS.md, specification, release policy, issue URLs and relevant pinned versions.]

## Current verified state

**Observed as of:** [UTC timestamp and run ID]

**Latest source/ref:** [Actual head SHA, branch and remote fetch context.]

**Completed and independently checkable:**
- [Result, exact artifact/commit/PR/issue URL, test/evidence reference and qualification level.]

**Pending/in progress:**
- [Named dependency, linked PR/issue, owner, next gate.]

**Negative evidence / failures:**
- [Failed test, mismatch, uncertainty, missing artifact; leave historical material visible if still relevant.]

**Access, permissions and review gates:**
- [Current known constraints; state what has *not* been authorized.]

## Next execution — authoritative instructions

**Objective:** [One highest-value bounded, dependency-ready task.]

**First live checks:**
- Fetch repository's current authoritative branch and this handover; verify exact SHAs.
- Read relevant repository instructions and current issue/PR/test state.
- Reconcile side effects from the previous execution before replaying any write.

**Proposed implementation / investigation:**
- [Concrete sequence with filenames/areas if known, avoiding guessed state.]
- [Specific evidence to collect and source-matched tests to run.]

**Done when:**
- [Measurable stop point; identify any review/approval necessary before merging or completing.]

**On blocker:**
- [What to preserve, what must not be overwritten, and the decision needed from the owner.]

**On completion:**
- Record verified results and next instructions here; use a guarded write; re-fetch the remote handover to verify persistence.
- If the project's overall acceptance criteria are met, set COMPLETE and pause its recurring task where supported/authorized.

## Compact execution history

### Generation 0 — [UTC date] — [run identifier / bootstrap]

- **Read:** [exact source ref or created initial file].
- **Worked:** [initialization or actual action].
- **Verified:** [artifact/test evidence or 'not yet run'].
- **Persisted:** [where handover is stored; include remote commit in run output because a commit cannot embed its own SHA in itself].
- **Residual risk:** [clear, bounded risk].

Keep only the most recent useful entries here. Link older full audit and CI evidence rather than growing this file indefinitely. Never include access tokens, credentials, sensitive data, or hidden chain-of-thought.
