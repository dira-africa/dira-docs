# AGENTS.md — dira-docs

> Read this before doing anything in this repo. Pair it with `GUARDRAILS.md`.

## What this repo is
`dira-docs` is the documentation and **evidence room** for Dira Africa: the
architecture, API spec, reviewer/reviewer guides, runbooks, and the milestone
evidence used to unlock Hedera Thrive grant tranches.

## Current job — migrate docs to Hedera
The docs currently describe a XION + zkVerify design and must be rewritten to the
Hedera-native architecture:
- Replace `architecture/xion-zkverify-integration.md` with a Hedera
  (HCS + HTS) architecture doc: Telegram frontend → dira-api → HCS provenance +
  HTS Climate Token → Pretium / Africa's Talking / Dira Circle / vouchers.
- Update `openapi.yaml` to match the real `dira-api` routes (remove XION/zkVerify
  anchoring endpoints; add Hedera attestation + verification fields).
- Keep `guides/reviewer-guide.md` accurate to the shipped system.

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
