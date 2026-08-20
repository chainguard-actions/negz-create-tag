<!-- markdownlint-disable -->

# Hardening Report: negz--create-tag/v1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **negz--create-tag/v1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file references actions/checkout@v2 (a mutable tag) in two steps. These should be pinned to a full 40-character commit SHA to prevent supply-chain attacks. Failing references: 'uses: actions/checkout@v2' (line 11, build job) and 'uses: actions/checkout@v2' (line 19, test job).

Locations:

- `.github/workflows/test.yml:11`
- `.github/workflows/test.yml:19`

### missing-permissions (severity: medium)

The workflow file has no top-level 'permissions:' key, and neither the 'build' job nor the 'test' job defines its own 'permissions:' block. Without explicit permissions, the workflow inherits the default (often write-all) token permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned both `actions/checkout@v2` references to full SHA `0717577d45739eb3c851188b29f50ed6c0b2194e # v2` at lines 11 and 19 of .github/workflows/test.yml. 2. Added top-level `permissions: contents: read` for least-privilege defaults, and a job-level `permissions: contents: write` override on the `test` job since it creates tags via GITHUB_TOKEN.

