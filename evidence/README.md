# Permanent synthetic GitHub Action evidence

This **project-maintained** repository runs the released AWS Emulator MCP
Architecture Review from a separate GitHub repository. The checks below
verify that the GitHub Action can be installed and used elsewhere. They are
**not independent developer endorsements** and do not test a real AWS
CloudFormation change set.

| Scenario | GitHub PR | Verified workflow run | Outcome | Permanent report |
| --- | --- | --- | --- | --- |
| Add SQS queue only | [#1](https://github.com/B11-Health/aws-emulator-mcp-action-demo/pull/1) | [43761515041](https://github.com/B11-Health/aws-emulator-mcp-action-demo/actions/runs/43761515041) | PASS — 1 added, 2 unchanged, no high-risk flags | [Report](safe-queue-addition/report.json) |
| DynamoDB partition-key change | [#2](https://github.com/B11-Health/aws-emulator-mcp-action-demo/pull/2) | [43763159579](https://github.com/B11-Health/aws-emulator-mcp-action-demo/actions/runs/43763159579) | **EXPECTED BLOCK** — 1 high-risk flag, exit code 2 | [Report](blocked-dynamodb-key/report.json) |
| Diagram-only label change | [#3](https://github.com/B11-Health/aws-emulator-mcp-action-demo/pull/3) | [43762959649](https://github.com/B11-Health/aws-emulator-mcp-action-demo/actions/runs/43762959649) | PASS — 1 conceptual change, no CloudFormation property change | [Report](safe-diagram-only/report.json) |

Each scenario has a generated [before/after SVG](safe-queue-addition/architecture-diff.svg)
(or choose another scenario directory), a machine-readable `report.json`,
a Markdown summary, before/after CloudFormation YAML **drafts**, and a
`SHA256SUMS.txt` file for the checked-in subset. The original hosted jobs
produced 11 files per run. Those GitHub Actions artifacts expire after seven
days; these five selected evidence outputs remain in Git.

The root Action was pinned to the exact reviewed source commit
`b14fb52e6c69b661e7d0a8dd2d2dd2aa38c851be` (beta.13) in #2/#3.
The first (safe addition) example used the prior pinned beta.12 nested Action.
Both versions use the same bounded, synthetic blueprint comparison.

The expected-block PR #2 **remains open and intentionally red**.
It should **not** be merged. A red check there demonstrates policy behavior,
not a failed production release.

**Safety boundary:** no real AWS account, credentials, deployment, IAM policy
or CloudFormation change set was accessed. Review flags are conservative
human prompts, not guaranteed AWS replacement/deletion predictions.
