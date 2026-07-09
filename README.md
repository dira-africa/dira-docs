# dira-docs

**Dira — Public API Documentation, OpenAPI Specification, and Impact Reports**

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-teal.svg)](https://opensource.org/licenses/Apache-2.0)
[![OpenAPI](https://img.shields.io/badge/OpenAPI-3.0-6BA539.svg)](https://www.openapis.org/)
[![XION](https://img.shields.io/badge/XION-Mainnet-orange.svg)](https://xion.burnt.com/)
[![zkVerify](https://img.shields.io/badge/zkVerify-Mainnet-purple.svg)](https://zkverify.io/)
[![Code of Conduct](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](CODE_OF_CONDUCT.md)

The public documentation repository for the Dira platform. This is where insurers, banks, government partners, reviewers, and independent researchers find everything they need to understand, integrate with, and verify the Dira climate data network.

---

## What this repository contains

```
dira-docs/
├── openapi.yaml                        ← OpenAPI 3.0 specification (single source of truth)
├── guides/
│   ├── reviewer-guide.md               ← How to verify Dira data on XION independently
│   └── ...
├── architecture/
│   ├── system-overview.md              ← How all components fit together
│   ├── xion-zkverify-integration.md    ← XION and zkVerify blockchain integration design
│   └── ...
└── schemas/
    └── database/                       ← Database schema documentation
```

---

## Related repositories

* **[`dira-core`](https://github.com/dira-africa/dira-core)** — Telegram Mini App frontend. Next.js 14 App Router + @twa-dev/sdk. Onboarding, capture (with device barometer), reports, wallet/redeem, maps, dashboards, English/Swahili. Carries XION account abstraction to remove.
* **[`dira-api`](https://github.com/dira-africa/dira-api)** — the backend. Fastify + TypeScript, raw SQL migrations via pg, BullMQ + Redis, Zod env, pgcrypto PII. Services already cover AI verification, triangulation, tokens (internal ledger), airtime, Dira Circle, vouchers, B2B/partner, DPA and the public dashboard. Anchoring is zkVerify + XION and cash-out is Daraja M-Pesa — those are the parts we replace (Hedera for anchoring, Pretium for cash-out).
* **[`dira-docs`](https://github.com/dira-africa/dira-docs)** — docs & evidence room. Architecture, OpenAPI, reviewer guide. Currently XION/zkVerify-themed; rewritten to Hedera in P3.4.
* **`dira-contracts`** — DELETED. Held a CosmWasm/XION contract and a zkVerify circom circuit. Removed entirely in P0.2 (along with the Midnight .compact files inside dira-api) so there are no mix-ups.

---

## Licence

Apache 2.0 — see [LICENSE](LICENSE).

*Dira Africa Limited, 2026.*
