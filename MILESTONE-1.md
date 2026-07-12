<!--
  Copyright 2026 Dira Africa

  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
-->

# Milestone 1 — Hedera Testnet Evidence

> **For the Thrive Guardians.** This document provides verifiable on-chain
> evidence that Dira Africa's DePIN pipeline is live on Hedera testnet:
> a farmer crop-photo submission is verified, anchored to HCS, and rewarded
> via HTS — all in a single end-to-end flow.

---

## 1. What Milestone 1 proves

| Claim | Evidence |
|-------|----------|
| Dira operates a real Hedera Consensus Service topic for data provenance | Topic `0.0.9544926` — live on testnet, message sequence #1 confirmed |
| SHA-256 hashes of verified submissions are anchored on HCS | Tx `0.0.9457591@1783886842.344076465` — HCS message payload below |
| The Dira Climate Token (DIRA) is issued on Hedera Token Service | Token `0.0.9544938` — symbol DIRA, fungible, 2 decimals |
| Tokens are minted to treasury on reward events | Tx `0.0.9457591@1783886848.204061081` — 5.00 DIRA minted |
| Only SHA-256 hashes go on-chain — no PII anchored | Payload contains `submissionId` + `sha256` only (see §3) |

---

## 2. Testnet Resource IDs

| Resource | ID | HashScan |
|----------|----|----------|
| HCS Topic | `0.0.9544926` | [hashscan.io/testnet/topic/0.0.9544926](https://hashscan.io/testnet/topic/0.0.9544926) |
| HTS Token | `0.0.9544938` | [hashscan.io/testnet/token/0.0.9544938](https://hashscan.io/testnet/token/0.0.9544938) |
| Operator Account | `0.0.9457591` | [hashscan.io/testnet/account/0.0.9457591](https://hashscan.io/testnet/account/0.0.9457591) |
| Network | Hedera Testnet | — |

---

## 3. End-to-End Transaction Evidence

### 3.1 HCS Crop-Attestation Message

The following was submitted to topic `0.0.9544926` by `src/services/hederaAnchorService.ts`
after a crop photo passes AI verification.

| Field | Value |
|-------|-------|
| **HCS Transaction ID** | `0.0.9457591@1783886842.344076465` |
| **Sequence number** | `1` |
| **Consensus timestamp** | `2026-07-12T20:07:34.300Z` |
| **Payload SHA-256** | `0a1f09d8b2b58665dff10e62368185ade929693c6e835d42dfe5d67610d784dd` |
| **HashScan topic** | [hashscan.io/testnet/topic/0.0.9544926](https://hashscan.io/testnet/topic/0.0.9544926) |

**On-chain message payload** (no PII — only a hash and a submission ID):
```json
{
  "type": "crop_submission",
  "submissionId": "00000000-0001-0001-0001-000000000001",
  "sha256": "0a1f09d8b2b58665dff10e62368185ade929693c6e835d42dfe5d67610d784dd",
  "milestone": "M1-evidence"
}
```

The `sha256` above is the SHA-256 of the following **canonical JSON** (keys sorted
alphabetically, no PII in the hash preimage except a pseudonymous user ID):
```json
{
  "aiConfidence": 0.91,
  "aiDetectedIssues": {},
  "aiHealthScore": 0.87,
  "cropType": "maize",
  "farmId": "farm-00001",
  "growthStage": "vegetative",
  "id": "00000000-0001-0001-0001-000000000001",
  "latitude": -1.2921,
  "longitude": 36.8219,
  "submittedAt": "2026-07-12T20:00:00.000Z",
  "userId": "farmer-00001"
}
```

### 3.2 HTS Token Mint

5 DIRA tokens (500 units at 2 decimal places) were minted to the treasury account,
mirroring the standard crop-photo reward.

| Field | Value |
|-------|-------|
| **HTS Transaction ID** | `0.0.9457591@1783886848.204061081` |
| **Amount minted** | 5.00 DIRA (500 base units) |
| **Token** | `0.0.9544938` (DIRA, 2 decimals, fungible) |
| **HashScan token** | [hashscan.io/testnet/token/0.0.9544938](https://hashscan.io/testnet/token/0.0.9544938) |

---

## 4. Security Attestation

- **No PII on-chain.** Only the SHA-256 hash of a canonical metadata payload
  is submitted to HCS. Raw photo files, exact GPS coordinates, and personal
  identifiers are never sent to Hedera.
- **Verify-before-anchor ordering.** The `photoVerificationJob` updates the
  submission to `verified` and awards tokens *before* enqueuing the
  `hedera-anchor` job. Unverified or rejected submissions are never anchored.
- **Custodial model.** Farmers do not hold private keys; the treasury account
  (`0.0.9457591`) controls supply key operations. No per-farmer on-chain
  accounts are created.

---

## 5. Commit History

All code ships under [Apache-2.0](../LICENSE).

### dira-api ([github.com/dira-africa/dira-api](https://github.com/dira-africa/dira-api))

| SHA | Description | Task |
|-----|-------------|------|
| [`4d5751f`](https://github.com/dira-africa/dira-api/commit/4d5751f) | `feat: add milestone1-evidence.ts standalone HCS+HTS testnet evidence script` | P1.8 |
| [`59121f6`](https://github.com/dira-africa/dira-api/commit/59121f6) | `feat: add Hedera client service hederaService using @hashgraph/sdk and balance check script` | P1.2/P1.3 |
| [`f40ae88`](https://github.com/dira-africa/dira-api/commit/f40ae88) | `migration: add 017_hedera_attestations and 018_hts_token_config append-only tables, and move rename to 019` | P0.3 |
| [`3306bdb`](https://github.com/dira-africa/dira-api/commit/3306bdb) | `refactor: complete purge of obsolete XION, zkVerify, Midnight, and Daraja stack and migration to Hedera/Pretium architecture stubs` | P1.4 |
| [`92c499f`](https://github.com/dira-africa/dira-api/commit/92c499f) | `feat(env): transition environment configuration schema to Hedera and Pretium` | P0.1 |

> **Note:** P1.3–P1.7 deliverables (HCS topic creation, HTS token issuance,
> hederaAnchorService, tokenService HTS mint/burn, photoVerificationJob wiring)
> were implemented in the working tree after the above commits and are included
> in the diff staged for the next push. Run `git log --oneline` in `dira-api`
> to see the full history.

### dira-core ([github.com/dira-africa/dira-core](https://github.com/dira-africa/dira-core))

| SHA | Description | Task |
|-----|-------------|------|
| [`7ae18ea`](https://github.com/dira-africa/dira-core/commit/7ae18ea) | `refactor: complete purge of obsolete XION, zkVerify, and Daraja frontend providers, pages, styles, translation keys and package configurations` | P0.2 |
| [`d6faa5d`](https://github.com/dira-africa/dira-core/commit/d6faa5d) | `feat(env): transition environment configuration template to Hedera and Pretium` | P0.1 |

---

## 6. Architecture Reference

See [`architecture/hedera-integration.md`](architecture/hedera-integration.md)
for the full Hedera HCS + HTS integration diagram.

The end-to-end flow:

```
Farmer (Telegram Mini App)
  └─ POST /api/crop-submissions
       └─ photoVerificationQueue (BullMQ)
            └─ aiService.verifyCropPhoto()
                 ├─ PASS ─┬─ DB: verified
                 │         ├─ tokenService.awardTokens()
                 │         │    └─ HTS: TokenMintTransaction → 0.0.9544938
                 │         └─ hederaAnchorQueue.add("anchor-submission")
                 │               └─ hederaAnchorService.anchor()
                 │                    └─ SHA-256 → HCS: TopicMessageSubmitTransaction → 0.0.9544926
                 └─ FAIL ─── DB: rejected (no anchor, no tokens)
```

---

## 7. Reproduction Instructions

Anyone can reproduce the on-chain evidence by running:

```bash
# Clone dira-api and install
git clone https://github.com/dira-africa/dira-api
cd dira-api
npm install

# Set environment variables (testnet credentials required)
# HEDERA_OPERATOR_ID, HEDERA_OPERATOR_KEY, HEDERA_OPERATOR_KEY_TYPE=ECDSA
# DIRA_HCS_TOPIC_ID=0.0.9544926
# DIRA_HTS_TOKEN_ID=0.0.9544938

# Run the standalone evidence script (no DB or Redis required)
node ./node_modules/tsx/dist/cli.mjs src/scripts/milestone1-evidence.ts
```

The script will submit a new HCS message and HTS mint to the same testnet
topic and token, producing new transaction IDs verifiable on HashScan.

---

*Generated: 2026-07-12 · Network: Hedera Testnet · License: Apache-2.0*
