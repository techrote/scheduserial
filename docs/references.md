# References, provenance and evidence boundary

**Recorded / checked:** 30 October 2026.

## Origin of this proposal

Owner's design proposal in the Scheduserial discussion on 30 October 2026:

> A scheduled agent prompt reads `handover.md` from the project repository; on completing its turn it writes a successor prompt into the same file. Alternatively, the scheduled agent updates its **own scheduled-task prompt** with the successor instructions. Both approaches are deliberately **serial**, not parallel multi-agent orchestration.

The core reason for this design is **reducing orchestration to a stable trigger plus a durable continuation**, while retaining actual source checks and verification gates. It is a separate minimal design from [techrote/scheduswarm](https://github.com/techrote/scheduswarm).

## External platform references

1. **OpenAI Help Center — [Scheduled tasks in ChatGPT](https://help.openai.com/en/articles/10291617-scheduled-tasks-in-chatgpt).** Documents recurring tasks, task management and editing, pausing, task availability and plan-dependent limits. Eligible paid scheduling is no more frequent than hourly; task prompts and task sharing need appropriate privacy care. **It does not establish that a scheduled execution can programmatically rewrite its own future prompt.**
2. **OpenAI Help Center — [ChatGPT Work and Codex](https://help.openai.com/en/articles/20001275-chatgpt-work-and-codex).** Describes Work tasks capable of running on a schedule or supported trigger. Tool and service availability depend on user permissions and configuration.
3. **GitHub Docs — [Repository contents API](https://docs.github.com/en/rest/repos/contents).** Describes creating/updating a repository file and requiring the existing file's blob `sha` for updates, plus conflicts from concurrent file operations. This is the basis for SHA-aware `handover.md` update guidance.
4. **GitHub Docs — [Git references API](https://docs.github.com/en/rest/git/refs).** Reference read/update and fast-forward semantics. Repository policy and branch protection still govern what is authorized.
5. **GitHub Docs — [Git trees API](https://docs.github.com/en/rest/git/trees) and [Git commits API](https://docs.github.com/en/rest/git/commits).** Illustrate a multi-file Git commit path when appropriate. This is **not** a requirement for Scheduserial end users.

## Observed tool capabilities vs empirical proof

At design time, the available interactive task management interface included an **update-existing-task** operation supporting prompt replacement while omitted schedule fields remain unchanged, plus an existing-task read operation. The linked GitHub connection supported reading files and writing content with expected blob SHAs.

Those are **interface observations**, not recorded successful end-to-end test results for Scheduserial. In particular:

- **Documented:** a person can edit a scheduled task; compatible authorized tool interfaces may expose task updates.
- **Unverified:** whether a task can edit **itself while executing on a schedule**, and whether a later independent scheduled execution sees and obeys that new prompt.
- **Unverified:** a strict no-overlap execution guarantee for either mode.
- **Unverified:** a two-execution Git continuation using this design.

See [qualification plan](verification.md). Any future claims of success must identify task ID, run IDs/timestamps, old/new prompt or Git SHAs, readback evidence, and the result of the next invocation. Avoid claiming a passing experiment solely from documentation, hypothetical workflows or manual edits.

## Citation and revision policy

External help pages can change. Check current task capabilities, account limits and API permissions before deploying; record the checked date in subsequent evaluations. A handover must cite **live, exact** project state for high-impact actions, rather than treating a prior summary as authoritative.
