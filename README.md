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

| Repository | Description |
|---|---|
| [`dira-core`](https://github.com/dira-africa/dira-core) | Telegram Mini App frontend |
| [`dira-api`](https://github.com/dira-africa/dira-api) | Fastify backend API and AI verification engine |
| [`dira-contracts`](https://github.com/dira-africa/dira-contracts) | CosmWasm smart contracts for XION & zkVerify ZK circuits |

---

## Licence

Apache 2.0 — see [LICENSE](LICENSE).

*Dira Africa Limited, 2026.*
