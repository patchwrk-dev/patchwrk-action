# Security — PatchWRK Free Scanner Action

This local distribution candidate has not been published or hosted-qualified at
patchwrk-dev/patchwrk-action. Previous qualification applies to the original pinned
Action repository path. Support is best effort, no guaranteed response/backport/SLA.

Use the existing [confidential reporting process](https://github.com/patchwrk-dev/patchwrk-scanner/blob/main/SECURITY.md)
and [private vulnerability reporting](https://github.com/patchwrk-dev/patchwrk-scanner/security/advisories/new)
in the Scanner repository, or security@patchwrk.dev. Do not report vulnerabilities
in public Issues. This candidate does not establish private reporting settings in a
new repository or verify current email forwarding. Agree secure transfer before
sensitive details; never attach credentials, private source or raw sensitive reports.

Report full Action reference/hash, runner/runtime, impact and a synthetic reproduction.
The intended support scope is public GitHub.com / standard Ubuntu24.04 Linux x64 /
Node24. Do not execute scanned code, install target dependencies or configure
privileged PR events/secrets/writes. Preserve read-only permissions and fork approval
policy. Workflows must consume trusted remote immutable code and only trusted-base
verification helpers. Public workflow logs and profile identities are visible.

Scanning is offline/read-only with bounded parsing/traversal and a worker deadline.
Empty/partial/unknown reports and exit 0 do not prove compatibility or production
health. Scan stable checkouts: portable filesystem checks do not sandbox hostile
concurrent mutation. Command-file writes are not transactional and output from a
failed step must not be treated as valid. Worker environment isolation does not
remove tokens/permissions from the entire GitHub job.

The initial response to suspected defects is disable/remove the job. Changes,
withdrawal and new releases require owner approval; no automatic repair, retag or
revocation of cached copies. No certification, complete network audit or universal
fork-safety claim is made. Third-party advisories need fresh review before release.
