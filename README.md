# dira-docs

**Dira — Public API Documentation, OpenAPI Specification, and Impact Reports**

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-teal.svg)](https://opensource.org/licenses/Apache-2.0)
[![OpenAPI](https://img.shields.io/badge/OpenAPI-3.0-6BA539.svg)](https://www.openapis.org/)
[![Code of Conduct](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](CODE_OF_CONDUCT.md)

The public documentation repository for the Dira platform. This is where insurers, banks, government partners, reviewers, and independent researchers find everything they need to understand, integrate with, and verify the Dira climate data network.

If you are a reviewer verifying Dira's data independently on the Midnight blockchain, start with the [Reviewer Guide](guides/reviewer-guide.md).

If you are an insurer or bank integrating with the Dira Oracle API, start with the [API Quick Start](guides/api-quickstart.md).

---

## What this repository contains

```
dira-docs/
├── openapi.yaml                        ← OpenAPI 3.0 specification (single source of truth)
├── guides/
│   ├── reviewer-guide.md        ← How to verify Dira data on Midnight independently
│   ├── api-quickstart.md               ← Insurer / bank integration guide
│   ├── data-agent-onboarding.md        ← Data Agent training materials
│   ├── farmer-onboarding.md            ← Farmer onboarding guide (English + Swahili)
│   └── privacy-policy.md              ← Plain-language Privacy Policy (ODPC compliant)
├── impact-reports/
│   ├── 2025-Q3-impact-report.pdf       ← Quarterly impact reports
│   └── ...
├── api-reference/
│   └── endpoints/                      ← Auto-generated per-endpoint documentation
├── architecture/
│   ├── system-overview.md              ← How all components fit together
│   ├── circular-economy.md             ← The four-layer redemption model explained
│   ├── midnight-integration.md         ← Midnight blockchain integration design
│   └── ai-verification.md             ← Crop photo and atmospheric AI pipelines
└── schemas/
    └── database/                       ← Database schema documentation
```

---

## For reviewers

The Dira platform anchors a cryptographic hash of every week's verified data points to the Midnight public blockchain. This means any party — including potential investors — can independently verify that Dira's data has not been altered, without trusting Dira's word, and without needing a Dira account or API key.

**[Start here → Reviewer Guide](guides/reviewer-guide.md)**

The guide explains step by step:
1. How to find Dira's weekly batch hashes on the Midnight block explorer
2. How to verify that a specific data point was included in a specific week's batch
3. How to verify a ZK Data Certificate for a county-level climate condition
4. How to check the consecutive-week anchoring record (provenance chain)

---

## For API partners

The Dira Oracle API is a B2B data product for insurers, banks, and agricultural lenders. It provides:

- **Verified atmospheric data** — hyper-local barometric readings verified by triangulation against Open-Meteo and cross-validated by network consensus among Data Agents
- **Crop health assessments** — AI-verified health scores and issue detection for geo-tagged crop photos
- **ZK Data Certificates** — on-chain zero-knowledge proofs that a geographic area experienced a specific climate condition during a specific period, without revealing any individual farmer's data
- **Coverage density maps** — GeoJSON heatmaps of data density by county, updated in real time

**[Start here → API Quick Start](guides/api-quickstart.md)**

To request API access: api@dira.africa

---

## OpenAPI specification

The canonical API specification is `openapi.yaml`. It is the source of truth for all API behaviour — if there is a discrepancy between the spec and the running API, the spec is correct and the API has a bug.

View the rendered spec:

```bash
# Install Redoc CLI globally
npm install -g @redocly/cli

# Serve locally
redocly preview-docs openapi.yaml
# Opens at http://localhost:8080
```

Validate the spec:

```bash
redocly lint openapi.yaml
```

**All pull requests to `dira-api` that change any endpoint must include a corresponding update to `openapi.yaml` in this repository.** PRs that change the API without updating the spec will not be merged.

---

## Impact reports

Quarterly impact reports are published as PDFs in `/impact-reports/`. They cover:

- Total verified data points collected (by county and month)
- Active user counts (farmers and Data Agents)
- AI verification confidence rates
- Token economics — total tokens earned, redeemed, and in circulation
- KES disbursed across all four circular economy layers
- Case studies (with participant consent)
- Institutional partnerships (letters of support, LOIs)

Impact reports are open data. They may be cited, shared, and reproduced with attribution.

---

## Contributing

Documentation contributions are among the highest-impact work in the Dira project. Non-developers are especially welcome here. Areas where contributions are most needed:

- **Swahili translations** — all farmer-facing guides must exist in Swahili
- **OpenAPI examples** — worked request/response examples for every endpoint
- **Case study documentation** — field-collected farmer testimonials (with consent)
- **Architecture diagrams** — visual explanations of the system components

Before contributing, please read:

- **[CONTRIBUTING.md](CONTRIBUTING.md)** — contribution process, documentation standards, OpenAPI spec requirements, and the Swahili translation guide
- **[CODE\_OF\_CONDUCT.md](CODE_OF_CONDUCT.md)** — how we treat each other in this community

---

## Community and support

| Channel | Purpose |
|---|---|
| [GitHub Issues](https://github.com/dira-africa/dira-docs/issues) | Documentation errors, missing guides, API spec questions |
| [GitHub Discussions](https://github.com/dira-africa/dira-docs/discussions) | Questions about the API, data model, or Midnight integration |
| api@dira.africa | API access requests and partner inquiries |
| community@dira.africa | General inquiries |
| conduct@dira.africa | Code of Conduct reports (private) |

---

## Related repositories

| Repository | Description |
|---|---|
| [`dira-core`](https://github.com/dira-africa/dira-core) | Telegram Mini App frontend |
| [`dira-api`](https://github.com/dira-africa/dira-api) | Fastify backend API and AI verification engine |
| [`dira-contracts`](https://github.com/dira-africa/dira-contracts) | Compact smart contracts for Midnight blockchain |

---

## Licence

Apache 2.0 — see [LICENSE](LICENSE).

Impact reports are additionally licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — they may be cited, reproduced, and built upon with attribution.

*Dira Africa Limited, 2026.*
