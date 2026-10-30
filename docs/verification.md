# Qualification plan and acceptance criteria

**As of 2026-10-30:** The **Serial Native two-scheduled-run core test passed** on a disposable task, including verified prompt self-edit, successor consumption and self-pause. Task history now records the second scheduled run completed. See [post-restoration audit](../proving/post-restore-audit.md). Serial Git's scheduled-run test and Serial Native's negative/fault-injection cases remain open.

The core claim to test is **continuation across independent scheduled executions**, not merely an agent writing a plausible handover at the end of one chat.

## Test environments

- Use a **disposable** Git repository for Serial Git testing, not a production codebase.
- Use a **dedicated disposable scheduled task** for Serial Native. Do not edit an unrelated owner's active task.
- Give the agent only minimally necessary privileges; avoid irreversible actions.
- Pick an interval long enough to inspect completion and avoid plausible overlap. Eligible paid plans may support hourly scheduling; do not assume higher-frequency schedules.
- Capture task ID, exact saved prompt versions, scheduled execution time, actual run ID/time, and evidence sources.

## Serial Git acceptance

| ID | Scenario | Passing evidence |
| --- | --- | --- |
| G-01 | Initialization | Target repo contains valid `handover.md` and an unambiguous bootstrap task |
| G-02 | Scheduled run 1 reads baseline | Run 1 links the exact remote branch/head/handover it read |
| G-03 | Run 1 makes bounded progress | New artifact/test result is independently inspectable; failed checks are not hidden |
| G-04 | Run 1 writes successor | Commit with expected blob/ref state is visible remotely and content readback matches |
| G-05 | Independent run 2 continues | Run 2 reads the *new* handover and performs **different** specified work, not a replay of run 1 |
| G-06 | Concurrent modification test | Stale writer detects conflict and does not overwrite a newer handover |
| G-07 | Interrupted-run test | Next run reconciles side effects before resuming or replaying |
| G-08 | Completion | A verified COMPLETE stops work and the task is paused if supported; otherwise owner alerted |

**Git verdict:** two actual scheduled runs plus passing conflict/recovery behaviour and preserved repository policy. A successful manual write alone is insufficient.

## Serial Native acceptance

| ID | Scenario | Passing evidence |
| --- | --- | --- |
| N-01 | Identify existing task | Correct task ID, schedule and full baseline prompt observed |
| N-02 | Scheduled run 1 self-edit | The agent uses the authorized task-update action to replace only its own prompt |
| N-03 | Verify persistence | Same task ID; generation 0 -> 1; fixed contract and schedule unchanged; readback matches |
| N-04 | Independent scheduled run 2 | Run 2 executes **generation 1**, not generation 0, and advances to 2 |
| N-05 | Forbidden/wrong task test | An unknown or mismatched task ID results in refusal, no other task modified |
| N-06 | Update-failure injection | A denied or missing update is reported clearly, not claimed as successful |
| N-07 | Overlap/stale generation | Evidence demonstrates safe refusal or documents an unresolved race (no strict-serial claim) |
| N-08 | Completion behaviour | Verified goal completion pauses task with readback, or requests owner action if unsupported |

**Native verdict (observed 2026-10-30):** N-01, N-02, N-03, N-04 and N-08 **PASS** in the disposable task, with separate scheduled executions and exact prompt/readback evidence. N-05 (wrong-ID refusal), N-06 (denied update) and N-07 (overlap/stale-generation handling) **NOT TESTED**. A core proof is **not** a general resilience or strict-exclusive-execution claim. [Detailed audit](../proving/post-restore-audit.md).

## Evidence record for each execution

Record this minimal tuple:

    mode:
    date_time_utc:
    task_id:
    run_id_or_url:
    task_schedule_before_after:
    target_repo_and_ref:       # Git only
    observed_generation:
    observed_handover_or_prompt_digest:
    action_and_result:
    exact_test_evidence:
    persistence_operation:
    persisted_generation_and_digest:
    readback_location:
    failed_or_unverified_checks:
    next_action_or_stop_condition:

Where no digest or run ID can be obtained from the platform, say **not available** rather than fabricating one. Store redacted evidence without credentials.

## Negative tests and escalation

- Scheduled run denied access to repo/task management.
- A prior `RUNNING` owner is still active or status is ambiguous.
- A file SHA mismatch or an update targeting the wrong branch.
- Interrupted write followed by a retry.
- Already-completed objective and missing expected data.
- Required review or user approval is pending.
- Task changed externally between read and write.
- Native task prompt changes contract or schedule unintentionally.
- Inability to pause a finished task.

**Fail closed:** stop state-changing work and show the operator what was verified, what failed and the least risky recovery action. Do not automatically create a second scheduled task to compensate.

## Go/no-go

- **Serial Git:** documentation and manual Git writes may be proven separately from *scheduled* continuity; do not conflate them.
- **Serial Native:** the bounded two-run core handover is **functional in the tested configuration**; safe unattended production use remains gated on negative-path and operational-recovery qualification.
- **Strict exclusivity:** remains unproven without an appropriate scheduler guarantee or independently validated ownership mechanism, even when ordinary serial handover passes.

Keep this document updated with links and exact results from future trials; never replace pending states with assertions of success without cited evidence.
