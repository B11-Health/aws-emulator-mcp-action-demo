# AWS Emulator MCP: external GitHub Action consumer demo

This is a **project-maintained, separate-repository integration test** for
[the AWS Emulator MCP architecture-review Action](https://github.com/B11-Health/aws-emulator-mcp).
It is **not** an independent third-party endorsement and it does not deploy real AWS infrastructure.

## Why this repo exists

This GitHub repository uses the **published Action pinned to an exact source
commit**, not an `uses: ./` action from the repository being tested.
Anyone can inspect the actual pull-request checks and downloaded artifacts,
then copy the minimal workflow into their own repository.

- The baseline checks in `.aws-emulator/architecture.json` declare a
  conceptual Checkout API, an S3 receipt bucket, and a DynamoDB orders table.
- An **add-only PR** proposes an SQS queue. The Action should show one added
  resource, zero high-priority flags, and a successful check.
- A **risky PR** changes the existing DynamoDB partition key. The Action
  should flag a possible replacement and fail the PR check because this
  demo deliberately selects `fail-on-risk: high`. That red check is
  **intentional test evidence**, not a broken build.

The Action compares source manifests and generates SVG/draw.io diagrams,
CloudFormation drafts, a structured report and a job summary. It is **not a
live AWS CloudFormation change set**. No AWS account or credentials are used.

## How to use

Copy [the workflow](.github/workflows/architecture-review.yml) and
[the blueprint](.aws-emulator/architecture.json) into your own repo. Change
the manifest in a pull request. The Action reads the base file from the
actual PR base commit using Git; `fetch-depth: 0` is required.

**Trust model:** the workflow uses only read-only `contents: read`
permissions, no AWS secrets, and an immutable 40-character SHA for the
upstream Action. The Action's compiler treats PR JSON as data, not code.

[Full feature documentation](https://github.com/B11-Health/aws-emulator-mcp/blob/v0.4.0-beta.12/docs/ARCHITECTURE_REVIEW.md) ·
[Download the v0.4.0-beta.12 artifacts](https://github.com/B11-Health/aws-emulator-mcp/releases/tag/v0.4.0-beta.12)

Independent developers are invited to reproduce the test in their own
repositories and report problems, not to treat this project-maintained
example as proof of general AWS fidelity.
