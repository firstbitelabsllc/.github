# Verification loop for agent work

A completed change needs evidence that the intended user path works. Start from
[Lauren Tan's verification loop](https://x.com/poteto/status/2109436202554372476):
run the product, interact with it as a user would, and return artifacts that are
easier to assess than the whole diff. Tests and reviews complement this proof.
Verification covers the paths exercised; it is not a guarantee of all behavior.

## Two reusable skills

The implementation adapts these MIT-licensed pstack skills at upstream commit
`11713c683fe4add4fd403ea880580abbc9e0875f`:

- [create-verification-skill](https://github.com/cursor/plugins/blob/11713c683fe4add4fd403ea880580abbc9e0875f/pstack/skills/create-verification-skill/SKILL.md)
  discovers the repo's real launch and interaction commands, writes a verification
  skill and feature map, and proves at least one feature end to end.
- [maintain-verification-skill](https://github.com/cursor/plugins/blob/11713c683fe4add4fd403ea880580abbc9e0875f/pstack/skills/maintain-verification-skill/SKILL.md)
  checks each mapped feature against source and live behavior, then repairs only
  the verification skill. A product regression is reported separately.

## Installation

The upstream links above are permanent source links. Download each complete
skill directory from that pinned revision, including the create skill's
`references/` directory and [pstack's MIT license](https://github.com/cursor/plugins/blob/11713c683fe4add4fd403ea880580abbc9e0875f/pstack/LICENSE).
The original skills target Cursor. To use them in another agent host, adapt the
output paths and invocation metadata to that host; preserve the launch, Doctor,
drive, evidence, cleanup, and feature-map requirements.

A portable adapted bundle is also supplied as an artifact with this setup task;
it includes both skills plus a `verify-voice-debug-harness` pilot. That bundle is
separate from this public repository. Access to this guide alone does not imply
access to the adapted package. The pinned upstream source is independently usable.

For either source, inspect the contents, then copy the complete desired skill
directories into the project's configured agent skill location. Use
`.agents/skills`, `.claude/skills`, or `.cursor/skills` only when supported by that
host. In the shared operator workspace, canonical adapted skills are staged
under `public/skills/` for its separate save step. Do not copy files into managed
runtime helper paths or assume a local edit has already been saved.

Invoke the skill by name when discovered, or ask the agent to read its `SKILL.md`.
For example:

> Use create-verification-skill for this active repository. Define the observable
> acceptance criteria, build the feature map, and run one real user path. Keep
> proof under outputs and report exactly what was and was not verified.

> Use maintain-verification-skill on verify-voice-debug-harness. Inspect and drive
> every mapped feature, retain evidence after cleanup, and prepare any corrections
> for review. Report clean, changed, or blocked with per-feature coverage.

These are agent instructions, not a background service or a CI gate. Copying
files does not activate T3, choose a model, install CodeRabbit, or enable merging.
An org `.github` repository does not automatically distribute skills into other
repositories. Adopt them in each selected host or through its supported shared
skill configuration.

## Goal and team ownership

Keep a short goal record: intended user outcome, acceptance criteria, unknowns,
next experiment, observed proof, and remaining gaps. New evidence changes the
next experiment; it does not justify weakening the requested outcome. Use managed
goal tools only when requested and available, otherwise track the checklist in
the task. A goal is complete when the acceptance criteria have supporting proof.

One task owner controls the branch and live application session. Parallel source
readers can inspect different features, but the coordinator drives them serially
and integrates their results. Respect T3/Shadow ownership and resource holds.
Record the models actually used; never claim an unavailable model ran. Run source
inspection serially if delegation is unavailable.

## Execution and evidence

1. Read repo instructions, establish the tested revision, and use declared tools.
2. Launch an isolated instance and run Doctor to establish readiness and ownership.
3. Drive the real UI, CLI, API, or library consumer. Check actions, resulting
   state, and relevant side effects. Capture screenshots or video for UI behavior,
   or structured output and exit status for CLI/API behavior.
4. If it fails, run Doctor again. Distinguish setup failure, harness drift, and
   product regression. Fix only authorized scope and re-run the affected path.
   Do not repeatedly retry unchanged failures or run recursive paid reviews.
5. Retain proof in `outputs/` before cleaning owned processes and scratch data.
   Confirm artifacts remain accessible after cleanup. Never kill by process name.
6. Reconcile the goal and report each criterion as pass, fail, or unverified.
   Maintenance is blocked if any mapped feature lacks live coverage.

Every receipt identifies the repository, full tested commit, dirty-tree state,
runtime, exact commands/interactions, expected and observed results, exit codes
where applicable, artifact paths, and limitations. For dirty trees retain a
sanitized diff or relevant content hashes. Re-run affected proof after edits;
old evidence does not automatically transfer to a new revision. Remove secrets
and private customer data before sharing artifacts.

Keep these claims separate: local tests, observed product behavior, CI, review
coverage of the current commit, merge state, and deployment. Zero checks is not
passing CI. A synthetic audio fixture proving microphone energy does not prove
speech recognition. UI copy promising typing at an exhausted shared limit must
be tested against the actual typing guard; a screenshot or passing copy test
alone cannot resolve that contradiction.

Copy the [evidence template](verification-evidence-template.md) into a PR body
or adopt it in a selected repository’s own template after review. It is an
opt-in document, not an organization-wide GitHub default. Reuse
an existing PR on the work branch; otherwise follow the current user's PR-opening
approval. Merge and deployment retain their own authorization and existing gates.
See [the review workflow](code-review.md) for CodeRabbit, local harness, and CI
integration. This change does not alter branch protection or auto-merge settings.
