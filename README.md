# PatchWRK Free Scanner — GitHub Action

Find supported API SDK integrations in JavaScript/TypeScript and review potential
compatibility risks against a limited historical catalog. Scanner reads code without
executing or changing it, fetching provider updates or uploading source to PatchWRK.
No PatchWRK account or API credential is needed.

**Available by immutable SHA from `patchwrk-dev/patchwrk-action`.** Hosted
qualification passed on November 3, 2026 for the supported scope below.
[GitHub Marketplace](https://github.com/marketplace/actions/patchwrk-free-scanner)
and the [v0.1.0 release](https://github.com/patchwrk-dev/patchwrk-action/releases/tag/v0.1.0)
are available.

## Install with the qualified commit

Create `.github/workflows/patchwrk.yml` in your authorized public repository.
The example pins the exact hosted-qualified Action commit. Review the workflow,
commit it to default `main`, then run it manually or push to main. GitHub account
permissions and repository-owner approval are required for workflow changes/runs.

```yaml
name: PatchWRK Free Scanner
on:
  workflow_dispatch:
  push:
    branches: [main]
permissions:
  contents: read
concurrency:
  group: patchwrk-${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: false
jobs:
  scan:
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-24.04
    timeout-minutes: 5
    steps:
      - uses: actions/checkout@11d5960a326750d5838078e36cf38b85af677262
        with:
          ref: ${{ github.sha }}
          persist-credentials: false
          fetch-depth: 1
          submodules: false
          lfs: false
      - id: patchwrk
        uses: patchwrk-dev/patchwrk-action@4f7aa523e0bd9038f0d1a6144cbda50b571f25e3
        with:
          path: '.'
```

No source clone, project dependency installation, npm package, Docker image or build
is required by Scanner. GitHub retrieves the bundled Action. `runs.using: node24`
selects the Action runtime; system Node is not an alternative to this runtime.
This exact repository/commit was qualified on standard GitHub-hosted **ubuntu-24.04 /
Linux x64 / Node24** (observed 24.22.1), in public GitHub.com repositories. Producer
contracts and consumer push, default-main manual dispatch, same-repository PR opened
and founder-owned fork PR opened all passed. [Qualification provenance](PROVENANCE.json).

Private repos, GHES, self-hosted/container/macOS/Windows/ARM runners and additional
PR events remain unqualified. Main push, default-main manual dispatch and PR opened
are the qualified event scope. The fork run used a founder-owned fork; it does
not prove every first-time/outside-contributor approval policy. GitHub-hosted scans
process your checkout and logs on GitHub infrastructure; installation and checkout
use network. GitHub runner costs depend on your account allowance and policy.

## Inputs, results and first use

Only optional `path` is accepted: a relative subdirectory inside GITHUB_WORKSPACE,
default `.`. Absolute/escaping/symlink inputs fail closed. Begin with a stable,
authorized synthetic JS/TS folder. Do not install or execute the target project.
After a successful scan, read the job summary and step outputs `status` and `result`:

- `status`: complete or partial; operational errors fail the step.
- `result`: minimized aggregate schema 1 JSON, provider counts, change IDs/statuses,
  catalog identity and coverage flags; no source paths or rich editor report.
- Exit 0: complete, including findings; exit 2: partial and failing step; exit 1:
  execution/validation error. Never interpret residual outputs after failure as valid.

Findings, unknowns and no findings are not a production-health guarantee. SDK version
declarations do not prove installed/deployed versions; SDK and remote API versions
stay separate. Discovery covers Stripe, OpenAI, Anthropic, Shopify and Twilio.
Compatibility coverage contains **four historical Stripe/OpenAI records**, not
comprehensive or current provider monitoring. No live provider checks, autonomous
repairs, automated migrations, automatic PRs, SARIF/comments or cloud history.

## Fork PRs and untrusted content

Use the separate [PR-opened example](examples/pull-request.yml.example) only after
reviewing repository/fork policy. It uses unprivileged pull_request, the event's merge
SHA, read-only checkout and immutable remote implementation. Do not use
pull_request_target or privileged workflow chains. Never run PR-local helpers,
Actions, package managers, target scripts or arbitrary user commands in this scan job.
No secret inputs, deployments, write scopes, caches or artifact uploads. Do not weaken
fork approval controls. Keep verification helpers in trusted base code, not the PR.

The Action cannot remove permissions granted by a caller. GitHub platform tokens
can exist even though Scanner needs none. The worker uses an empty environment and
no inherited Node arguments; stable-checkout, bounded scan/AST limits, a 75-second
worker deadline and 512 MiB old-generation heap cap remain. Portable filesystem
checks do not sandbox hostile concurrent ancestor replacement or guarantee a hard
process-wide memory/CPU boundary. Command-file writes are not transactional; fail
closed on errors and do not trust stale outputs. Do not share private source or raw
logs/reports in public Issues.

## Versions, source, updates and rollback

Recommended usage is a full immutable destination commit SHA. The first release
is **v0.1.0 in this dedicated repository**, separate from the original action-v0.1.0.
The published tag points to `09f384666781fc53839aecbffa927ba21a8db103`;
workflow examples retain the directly hosted-qualified `4f7aa523e0bd9038f0d1a6144cbda50b571f25e3` pin.
Version tags are convenient labels and can be mutable; never overwrite/reuse published tags or assets. No floating v1 alias is
planned. Updates require a reviewed new SHA, byte/source/license mapping, focused
checks and an explicit workflow pin change. No silent or automatic update promise.

Runtime bytes come unchanged from the [qualified original Action snapshot](https://github.com/patchwrk-dev/patchwrk-scanner/tree/542affc4913b5c3ee55b506470f36dc0304b17fb/action).
[PROVENANCE.json](PROVENANCE.json) and [dist/manifest.json](dist/manifest.json) identify
source, engine and hashes. This is a distribution repository; editable source and
build recipe live at immutable public source links. Rebuilding is a separate reviewed
change and is not required to consume this Action. Dependencies TypeScript 5.9.3 and
semver 7.8.5 are bundled with their notices; no runtime package install occurs.

For an incident, disable/remove the scan job while preserving relevant private
evidence. If appropriate after review, use the prior qualified original reference:
`patchwrk-dev/patchwrk-scanner/action@542affc4913b5c3ee55b506470f36dc0304b17fb`.
That old SHA belongs to the old repo path; it is not a destination SHA. No previous
release in this dedicated repository is established as a rollback. A corrective
release or listing withdrawal needs owner review; removing a listing cannot retract
cached/downloaded code.

## Support, licensing and security

MIT © 2026 Jovan Simon; [LICENSE](LICENSE), [dependency notices](THIRD_PARTY_NOTICES.txt)
and bundled license files apply. Engine open source does not imply private editor
adapter source is included. Maintainer Jovan Simon provides best-effort support,
without guaranteed response, backports, SLA or backup responder.

Use existing [Issues](https://github.com/patchwrk-dev/patchwrk-scanner/issues/new/choose)
for sanitized bugs and [Discussions](https://github.com/patchwrk-dev/patchwrk-scanner/discussions)
for questions. Include channel/version or SHA, OS/runner, expected/actual result,
change ID and a minimal invented reproduction. Never request repository access,
credentials, private source or unreviewed logs. For confidential vulnerabilities,
use [SECURITY.md](SECURITY.md). Marketplace presence/branding is not a third-party audit
or a verified-creator claim.
