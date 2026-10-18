# Review and merge a pull request

Use the [shared PR guide](https://github.com/leojkwan/everything/blob/main/packages/host/references/pull-requests.md)
for the author brief, before-and-after evidence, review replies, and merge flow.
The product repository owns its behavior, checks, and release rules.

CodeRabbit is advisory. Its organization configuration and
[review guidance](https://github.com/firstbitelabsllc/coderabbit/blob/main/docs/code-review.md)
live in `firstbitelabsllc/coderabbit`. Repository overrides can change the
effective settings. This `.github` repository supplies the default PR template;
its own `.coderabbit.yaml` does not configure other repositories.

Run the relevant local checks, fix reproducible defects, and explain false
positives with the exact PR file list or diff. Check covered commits before
claiming bot review. Skipped, paused, or incomplete reviews are not passes.
Checked work can merge under the repository's rules without bot approval.

Source changes and fixes stay with the accepting source owner. Preserve
unfinished work and its last useful check before an authorized host handoff.
Optional Shadow plans or Honcho memory do not gate shipping.

See [verification](verification-loop.md) for the evidence boundary.
