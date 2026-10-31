# Neurounner PR merge-down — execution evidence

**Status: READY / awaiting first scheduled execution.** No accepted PR merges or scheduled execution results recorded at setup.

| Stage | Source of truth | Evidence | Verdict |
| --- | --- | --- | --- |
| G0 setup | The saved `Neurounner PR Merge-Down` automation | Exact ID `6ae571c1f6ac8191a767bbbafa3c3bcd`, G0 prompt and hourly 05:30 schedule independently read back; enabled, `last_run=null` | **PASS — setup only** |
| G0 scheduled run | Actual task history and Neurounner issue/PR/CI | Not yet observed | PENDING |
| G1 self-handover | Same task's prompt update/readback and nonce | Not yet observed | PENDING |
| First guarded merge | Fresh PR head/current main/CI and GitHub merge response | Not yet observed | PENDING |
| Post-merge verification | GitHub main commit/tree and relevant required CI | Not yet observed | PENDING |

## Initial factual baseline

- Neurounner `main` at setup: `12f7bf0475aefb61227f676ea377134734fa5072`.
- 45 open PRs; candidates include older stacked #97/#98/#99 and later evidence/custody descendants. None preapproved.
- Existing separate development automation at `6ae51d0429e48191b27f6b540ab8a976` must not be altered.
- Historical PRs #191/#192 already merged, but their issue #213 claim has no visible explicit release; reconciling current ownership is the first integration safety check.
- Recorded planning notice: [#213 comment 6539153028](https://github.com/techrote/neurounner/issues/213#issuecomment-6539153028).
- Initial scheduled task prompt is in [seed-prompt.md](seed-prompt.md); its saved mutable section is the live next-instruction authority.

## Future stage record template

For each actual execution, add only facts supported by tool/CI/GitHub evidence:

```text
task_run_id:
scheduled_for_utc:
actual_start_finish_utc:
stage_input_output:
consumed_nonce_verified:
main_before_after:
ownership_claim_release:
reviewed_prs_and_exact_heads:
source_and_evidence_verification:
CI_ids_head_events_conclusions:
review_outcome_threads:
merge_response_and_real_main_sha:
preserved_negative_evidence:
remaining_owner_or_scientific_holds:
saved_prompt_readback:
next_decision:
```

Failed or unverified operations remain failed/unverified; no synthetic PASS. GitHub audit is external evidence, not a Git-backed continuation queue.
