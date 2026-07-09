<div align="center">

# dira-docs

**Architecture, API specification, and verification guides for Dira Africa**

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-0A6E56.svg)](../LICENSE)
[![Built on Hedera](https://img.shields.io/badge/Built_on-Hedera-1A1A6E.svg)](https://hedera.com)

</div>

---

## Overview

`dira-docs` is the documentation home for the [Dira Africa](https://github.com/dira-africa) platform — a decentralized climate-data verification network for African smallholder agriculture. It holds the system architecture, the API specification, and the guides an external reviewer or partner uses to independently verify Dira's data on-chain.

## Contents

```
architecture/     System design — Telegram frontend, Hedera (HCS + HTS), and the
                  circular-economy redemption rails (Pretium, Africa's Talking, vouchers).
guides/           Reviewer guide — how to independently verify Dira attestations on
                  Hedera via HashScan and the mirror node.
openapi.yaml      OpenAPI specification for the dira-api REST API.
```

## How Dira works (summary)

Verified climate observations are hashed and anchored to the **Hedera Consensus Service** for tamper-proof provenance, while contributor rewards are issued as a **Hedera Token Service** Climate Token. Anyone can independently verify a given attestation on [HashScan](https://hashscan.io) using the topic ID and sequence number — no trust in Dira required. Raw farmer data is never placed on-chain; only cryptographic hashes are.

## The platform

| Repository | Description |
| --- | --- |
| [`dira-core`](https://github.com/dira-africa/dira-core) | Telegram Mini App frontend |
| [`dira-api`](https://github.com/dira-africa/dira-api) | Backend REST API |
| [`dira-docs`](https://github.com/dira-africa/dira-docs) | This repository |

## Project status

Documentation is maintained alongside the platform's testnet-first rollout to Hedera. Architecture and API references are updated as milestones ship.

## License

[Apache License 2.0](./LICENSE) © Dira Africa.
