# AGENTS.md — dira-docs

> Read this before doing anything in this repo. Pair it with `GUARDRAILS.md`.

## What this repo is
`dira-docs` is the documentation and **evidence room** for Dira Africa: the
architecture, API spec, reviewer/reviewer guides, runbooks, and the milestone
evidence used to unlock Hedera Thrive grant tranches.

## Migration status — XION/zkVerify → Hedera (COMPLETED)
The documentation has been updated to the Hedera-native architecture. The
Hedera integration architecture doc is at `architecture/hedera-integration.md`.
The OpenAPI spec and reviewer guide have been updated. If you encounter any
residual XION/zkVerify/Midnight references, remove them.

## Evidence room (keep current as milestones ship)
Maintain milestone evidence files that the Thrive Guardians verify:
- Testnet + mainnet **HCS topic IDs** and **HTS token IDs** with HashScan links.
- GitHub links / commit history for each milestone.
- Demo recordings and public dashboard links.
- On-chain metric snapshots (transactions, unique farmers) from the mirror node.

## Conventions
- Markdown + OpenAPI (`openapi.yaml`). No application code runs here.
- Use real, verifiable IDs and links only — never invent a topic id, token id,
  transaction hash, or metric.
- Preserve Apache-2.0 licensing notices.

## How to work here
1. Produce a PLAN artifact and wait for approval before large rewrites.
2. Stay inside this repo. Do not modify `dira-core` or `dira-api` from here.
3. Cross-check every documented endpoint against the actual `dira-api` code.
