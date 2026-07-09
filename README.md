# dira-docs

**Dira — Public API Documentation, OpenAPI Specification, and Impact Reports**

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-teal.svg)](https://opensource.org/licenses/Apache-2.0)
[![OpenAPI](https://img.shields.io/badge/OpenAPI-3.0-6BA539.svg)](https://www.openapis.org/)
[![Hedera](https://img.shields.io/badge/Hedera-HCS%20%26%20HTS-green.svg)](https://hedera.com/)
[![Code of Conduct](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](CODE_OF_CONDUCT.md)

The public documentation repository for the Dira platform. This is where insurers, banks, government partners, reviewers, and independent researchers find everything they need to understand, integrate with, and verify the Dira climate data network.

---

## What this repository contains

```
dira-docs/
├── openapi.yaml                        ← OpenAPI 3.0 specification (single source of truth)
├── guides/
│   ├── reviewer-guide.md               ← How to verify Dira data independently
│   └── ...
├── architecture/
│   ├── system-overview.md              ← How all components fit together
│   ├── hedera-integration.md           ← Hedera (HCS & HTS) integration design
│   └── ...
└── schemas/
    └── database/                       ← Database schema documentation
```

---

## Related repositories

* **[`dira-core`](https://github.com/dira-africa/dira-core)** — Telegram Mini App frontend. Next.js 14 App Router + @twa-dev/sdk. Onboarding, capture (with device barometer), reports, custodial wallet/redeem (no user wallets), maps, dashboards, English/Swahili.
* **[`dira-api`](https://github.com/dira-africa/dira-api)** — the backend. Fastify + TypeScript, raw SQL migrations via pg, BullMQ + Redis, Zod env, pgcrypto PII. Services cover AI verification, triangulation, tokens (internal ledger), airtime via Africa's Talking, Dira Circle, vouchers, B2B/partner, and the public dashboard. Anchoring is Hedera Consensus Service (HCS) and Hedera Token Service (HTS); cash-out is Pretium (single mobile-money rail, all Kenyan & Ugandan telcos).
* **[`dira-docs`](https://github.com/dira-africa/dira-docs)** — docs & evidence room. Architecture, OpenAPI, reviewer guide.
* **`dira-contracts`** — DELETED. Held a CosmWasm/XION contract and a zkVerify circom circuit. Removed entirely (along with the Midnight .compact files inside dira-api) so there are no mix-ups.

---

## Licence

Apache 2.0 — see [LICENSE](LICENSE).

*Dira Africa Limited, 2026.*
