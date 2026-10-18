# Verify the changed user path

Start with the repository's existing launch commands and checks. Run the
changed UI, CLI, API, or library call, then inspect its resulting state and
relevant side effects. Tests and reviews complement this check.

1. Identify the tested revision, environment, and working-tree changes.
2. Run relevant formatting, compilation, lint, and behavior checks.
3. Exercise the changed action and inspect the result. For visual behavior,
   retain a captioned screenshot or short recording with synthetic data.
4. Name mocks and important unrun steps. A source test, local journey,
   production-data snapshot, merge, deployment, and live use prove different things.
5. Stop task-created processes and remove clean integrated temporary branches
   and worktrees. Preserve dirty, unmerged, and other-owned work.

Use [the shared PR guide](https://github.com/leojkwan/everything/blob/main/packages/host/references/pull-requests.md)
to explain the result and link long evidence. Use the
[default template](../pull_request_template.md) when opening a PR. A small
change needs no second evidence template, process record, or review gate.

The accepting source owner coordinates verification and integration. One
writer owns each shared scope. Optional memory is available for context and
does not replace the repository or block a checked merge.

When repeated verification needs a reusable skill, use pstack's existing
`create-verification-skill` or `maintain-verification-skill`. Verify that the
intended host discovers the skill before claiming it is installed or used.
