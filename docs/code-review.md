# First Bite Labs review workflow

Use one loop: Shadow/T3 tracks the task and its owner, the repository's local
harness produces deterministic proof, CodeRabbit reviews the change, and retained
CI verifies the checks that the repository actually requires. Blacksmith runs
existing opt-in Linux cloud lanes where configured. CodeRabbit review does not
replace a build, a test run, branch protection, or deployment approval.

## What this configuration does

The root `.coderabbit.yaml` is the reusable baseline and applies to this `.github`
repository. It enables assertive reviews, draft and incremental reviews, review
summaries with validation evidence, agent-ready fix prompts, code guideline
reading, and slop detection for all authors. Existing tool integrations retain
their schema defaults and run when applicable.

The request-changes workflow is enabled: CodeRabbit may approve after its feedback
is resolved, the latest commit has been reviewed, and pre-merge checks allow it.
Authors cannot use CodeRabbit's author-approval override. This is an AI review
signal, not human approval or an auto-merge rule. Repository branch protections
still govern merging. Review service errors fail CodeRabbit's outward status;
the status becomes a merge gate only if the repository requires it.

Title, description, linked-issue, and verification-evidence checks start in warning
mode. The evidence check inspects reported proof; it cannot certify that commands
ran. Generic docstring percentage checks are off to avoid unrelated churn across
Swift, JavaScript, documentation, and tool repositories.

Autofix, test generation, docstrings, simplification, CI repair, and conflict
resolution are enabled for deliberate use through CodeRabbit's available controls.
These settings expose capabilities, not blanket permission to change every PR.
Availability still depends on the installed app, permissions, current plan, and
repository support. Some documented finishing touches require Team or higher;
the trial screenshot alone does not establish their availability.

## Apply across repositories

**GitHub's `.github` convention does not make this a CodeRabbit org-wide config.**
CodeRabbit's automatic central configuration requires a repository named
`firstbitelabsllc/coderabbit` with a root `.coderabbit.yaml` and CodeRabbit App
access. No such repository was in the connected repository inventory during this
setup. This change does not create one or expand installation permissions.

Supported rollout paths:

1. Review this baseline, then import it into CodeRabbit's organization YAML
   settings. Inspect repository overrides before treating it as an org default.
2. Alternatively, put it in an authorized `coderabbit` central repository and
   verify app access. A repository config normally takes precedence; enable
   `inheritance: true` where lower-priority defaults should merge.
3. For an immediately reviewable pilot, apply the baseline directly in
   `voice-debug-harness/.coderabbit.yaml`. Keep its audio-specific instructions
   in that repository. This direct copy is an independent configuration; changes
   here do not automatically update it. Reconcile both until central rollout.

The baseline uses `inheritance: true` so compatible lower-priority settings can
fill gaps. Organization/workspace global overrides still win. Inspect the
resolved configuration instead of assuming a file is the only source.

On a pilot PR, request:

```text
@coderabbitai configuration
```

Confirm the source, path instructions, automatic review behavior, and offered
finishing touches. Record the PR URL, reviewed commit, checks, and unresolved
findings. Do not call a feature activated until the service demonstrates it.

## Agent and local harness loop

Use the repository's declared runtime, formatter, and verification commands.
Follow its `AGENTS.md` and saved ownership/admission rules before starting local
work. T3/Shadow coordinates ownership; it must not start another competing agent
on the same branch or bypass local resource holds.

With an installed and authenticated CodeRabbit CLI, the current documented
commands are:

```sh
# See included capacity before starting another review.
coderabbit usage --agent
# Replace VERIFIED_BASE with the target branch verified for this repository.
coderabbit review --agent --base VERIFIED_BASE
# Reuse an existing PR review's prompts without launching a new review.
coderabbit pullrequest PR_URL --show-prompts --agent
```

1. Implement a bounded change and run the repository's local proof commands.
2. Run one CLI review, or consume the existing PR review prompts.
3. Fix actionable findings, rerun affected checks, and run at most one follow-up
   CLI review. Escalate unresolved design issues to the task owner.
4. Batch fixes before pushing. Include the tested commit, exact commands, results,
   limitations, and changed behavior in the PR description.
5. Let incremental PR review assess the new commit. Automatic reviews pause after
   five reviewed commits; resume deliberately if more feedback is useful.

Do not add paid-credit flags or recursive review loops. Trial quotas and renewal
settings must be checked in the service. This repository change does not install
or authenticate the CLI on a developer's Mac, buy seats, or activate paid credits.

## CI and Blacksmith boundaries

The October 2026 connected-repository audit found these existing policies:

| Repository            | Existing policy to preserve                                                             |
| --------------------- | --------------------------------------------------------------------------------------- |
| `shadow`              | Scheduled/manual CI; owner-directed local-first proof.                                  |
| `resplit-web`         | Local-first tests; manual Blacksmith Testbox lane.                                      |
| `strongyes-web`       | Local-first proof; manual Blacksmith Testbox lane.                                      |
| `trysnowcubes-web`    | Manual Blacksmith Testbox lane.                                                         |
| `voice-debug-harness` | Node matrix and browser tests on PRs; pilot removes duplicate feature-branch push runs. |

Blacksmith is a runner provider used by GitHub Actions; adopting it does not
eliminate workflow orchestration. Use existing opt-in lanes and verify runner
access, architecture, image support, credentials, and budget before migrating
more jobs. In particular, Linux runners do not replace macOS/iOS build proof.

Keep required checks and their names stable. Deduplicate event triggers first;
then measure runs, runner minutes, queue time, and failure coverage before
consolidating jobs. Local proof remains required where repository policy says so.
Do not remove security or release checks because a review bot also scans code.

The voice pilot keeps PR jobs, pushes to `main`, all tag pushes, and adds manual
dispatch for pre-PR remote proof. Feature branches without a PR use local proof
or manual dispatch. This saves one duplicate four-job CI invocation per eligible
feature-branch push while preserving the PR's checks. Actual billable savings
must be measured; this document does not claim observed cost reduction.

## Merge and trial completion

Before enabling any automatic merge policy, confirm required tests, latest-commit
review, stale-approval dismissal, unresolved-thread policy, and deployment gates
in GitHub. CodeRabbit approval alone must not bypass those rules. This baseline
does not enable GitHub auto-merge or modify branch protection.

Use the trial to record useful findings, false positives, review latency, retained
CI minutes, and working finishing-touch actions on real PRs. Verify repository
coverage, remaining included usage, and renewal terms in CodeRabbit. Security
monitoring and triage activation must be checked in their service settings;
adding YAML does not establish account-level activation.

## Sources

- [Central configuration](https://docs.coderabbit.ai/configuration/central-configuration)
- [Configuration inheritance](https://docs.coderabbit.ai/configuration/configuration-inheritance)
- [Request changes workflow](https://docs.coderabbit.ai/pr-reviews/request-changes-workflow)
- [Pre-merge checks](https://docs.coderabbit.ai/pr-reviews/pre-merge-checks)
- [Finishing touches](https://docs.coderabbit.ai/finishing-touches/index)
- [CLI reference](https://docs.coderabbit.ai/cli/reference)
- [Configuration schema](https://coderabbit.ai/integrations/schema.v2.json)
