# Slack bot instructions

## Code and documentation

Write code that can be understood on its own. Use descriptive names and consistent
patterns, because agents reproduce the structures they find.

Keep documentation only when it adds significant information beyond the code,
such as business objectives, non-obvious design decisions, agent instructions or
external operational procedures. Remove duplicated schemas, endpoint catalogs,
file inventories, implementation reports and historical records. Git and PRs
retain the history.

Type checking and linting do not verify the accuracy of prose. When editing
documentation, check its owning source and remove redundant or obsolete material
within the scope of the change.

## Implementation and verification

Use functions and Maps and keep TypeScript ESM imports compatible with the build.
Preserve the existing Slack formatting and conversation isolation.

Run `npm run build` and `git diff --check` before each commit or push. The repository
defines no separate tests or lint script.

Follow Red → Green → Refactor for non-trivial code and reproduce a bug before
fixing it. Prefer existing integration clients over additional protocol code.

## Operation

Keep the SDK and its CLI installation consistent when upgrading. Restart the
service after updating the installed SDK so the running wrapper and spawned
binary use the same package version.

Use [the operations guide](README.md) for deployment and credential renewal.
Keep credentials out of logs and Git. Slack actions that need user notification
must use a new message, because editing an existing message does not notify them.
