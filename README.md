# dira-docs

**API Documentation, OpenAPI Specifications & Impact Reports — Dira Climate Verification Infrastructure**

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![OpenAPI](https://img.shields.io/badge/OpenAPI-3.1-green)](https://spec.openapis.org/oas/v3.1.0)
[![Midnight Mainnet](https://img.shields.io/badge/Midnight-Mainnet-1A1A6E)](https://midnight.network)

> *Your data earns your airtime. Your data grows your crops. Your data builds your safety net.*

---

## What Is Dira?

Dira (دائرة — Arabic for "circle") is a Decentralised Physical Infrastructure Network (DePIN) that turns the existing smartphone network into the most granular agricultural weather sensing layer in Sub-Saharan Africa. Verified data points are anchored as zero-knowledge proofs on the [Midnight blockchain](https://midnight.network). The Climate Token circular economy rewards contributors with airtime, farm inputs, and cash — from Day 1, without requiring Daraja production credentials.

---

## This Repository

`dira-docs` is the **public documentation and evidence layer** for Dira. Everything in this repository is open, citable, and reproducible. If Dira ever ceases to operate, this repository remains as an independent record of what was built and what it proved.

**Contents:**

| Directory | Contents |
|---|---|
| `api/` | OpenAPI 3.1 specifications for the Dira Oracle API |
| `guides/` | Integration guides for insurers, banks, and NGOs |
| `reports/` | Impact reports (published each quarter, open PDF) |
| `midnight/` | ZK architecture documentation and Compact contract ABIs |
| `circular-economy/` | Token redemption documentation and agro-dealer onboarding |
| `data-dictionary/` | Field definitions for all public API response objects |
| `postman/` | Postman collection for all public and B2B API endpoints |

---

## Repository Structure

```
dira-docs/
├── api/
│   ├── openapi.yaml                    # Master OpenAPI 3.1 specification
│   ├── paths/
│   │   ├── atmospheric.yaml            # Barometric sync endpoints
│   │   ├── crop-submissions.yaml       # Farmer photo submission endpoints
│   │   ├── tokens.yaml                 # Token balance and redemption endpoints
│   │   ├── public.yaml                 # Unauthenticated dashboard endpoints
│   │   └── partner.yaml                # Agro-dealer scan endpoint
│   └── schemas/
│       ├── AtmosphericReading.yaml
│       ├── CropSubmission.yaml
│       ├── AIHealthReport.yaml
│       ├── TokenTransaction.yaml
│       ├── ZKDataCertificate.yaml      # Midnight certificate schema
│       └── CircularEconomyRedemption.yaml
├── guides/
│   ├── insurer-integration.md          # How insurers connect to the Dira Oracle API
│   ├── zk-certificate-verification.md # How to verify a Dira ZK proof on Midnight without an account
│   ├── agro-dealer-onboarding.md      # Dira Partner App setup and MOU template
│   └── reviewer-guide.md        # reviewer: how to verify Dira data independently
├── midnight/
│   ├── DiraDataAnchor-ABI.json        # DiraDataAnchor.compact interface
│   ├── DiraDataCertificate-ABI.json   # DiraDataCertificate.compact interface
│   ├── zk-architecture.md             # How the three-contract Midnight suite works
│   └── verify-on-explorer.md          # Step-by-step: verify any Dira data point on Midnight
├── circular-economy/
│   ├── token-economics.md             # Earning rules, rates, and upgrade timeline
│   ├── agro-dealer-mou-template.md    # Standard MOU template for partner agro-dealers
│   ├── dira-circle-coordinator.md     # County coordinator selection and distribution model
│   └── redemption-api-reference.md    # All four redemption API endpoints documented
├── reports/
│   ├── impact-report-q1-2026.pdf      # First published impact report
│   └── token-economic-activity.csv    # Anonymised token velocity data (Annex A)
├── postman/
│   └── Dira-API-Collection.json       # Postman collection — all endpoints
└── data-dictionary/
    └── field-definitions.md            # Every field in every public API response
```

---

## The Dira Oracle API

The Dira Oracle API provides verified agricultural climate data to insurers, banks, governments, and NGOs. From Phase 2 (Month 4–5), all data feeds include Midnight ZK proof certificates.

### Authentication

B2B API access requires an API key obtained from [dira.africa/api-access](https://dira.africa/api-access).

```http
GET /api/v1/atmospheric/coverage
Authorization: Bearer dk_live_your_api_key_here
```

### Base URL

```
Production: https://api.dira.africa/v1
Sandbox:    https://sandbox.dira.africa/v1
```

### Key Endpoints

```yaml
# Climate data feed
GET /atmospheric/coverage?county=nakuru&from=2026-01-01&to=2026-01-31
GET /atmospheric/readings?lat=-0.303&lon=36.080&radius_km=5&hours=24

# ZK-verified data certificates (from Month 6–7)
GET /certificates?county=nakuru&month=2026-01
GET /certificates/:id/verify    # Independent verification without trusting Dira

# Public endpoints (no authentication)
GET /public/stats
GET /public/coverage-map
GET /public/activity-feed
```

---

## For Reviewers

This directory contains everything needed to independently verify Dira's claims without trusting Dira's word on anything.

**`guides/reviewer-guide.md`** explains, step by step, how to:

1. Open [Midnight's block explorer](https://explorer.midnight.network) and find Dira's weekly batch hashes without any Dira account
2. Verify that a specific batch hash corresponds to real data in Dira's public API
3. Read a ZK Data Certificate and confirm it proves a drought condition for a specific county and period
4. Cross-reference Dira's public dashboard data with the Midnight block explorer

No API key. No Dira account. No trust in Dira required.

---

## Impact Reports

Impact reports are published quarterly as open PDFs. They are written for non-technical readers — reviewers, insurance regulators, government partners — and contain:

- Network growth (active users, counties, verified data points)
- AI verification accuracy and confidence distribution
- Token economic velocity (tokens earned, airtime disbursed in KES, inputs redeemed, cash distributed)
- Family case studies (with written consent)
- Basis risk reduction calculation vs nearest Kenya Met station
- Midnight on-chain provenance statistics

Reports are permanently archived here. They are not updated retroactively.

---

## Circular Economy Documentation

**`circular-economy/agro-dealer-mou-template.md`** — the standard MOU template used when onboarding a new agro-dealer partner. It covers token acceptance terms, weekly reconciliation schedule, the 3–5% transaction fee structure, and the QR scan process. Agro-dealers may modify this template; the terms are a starting point, not a take-it-or-leave-it requirement.

**`circular-economy/dira-circle-coordinator.md`** — explains how county coordinators are selected (community consensus, not Dira appointment), how the monthly cash pool is calculated, and what the coordinator is and is not responsible for.

---

## Contributing

Documentation contributions are the most accessible way to improve Dira. You do not need to be a developer.

- **Swahili translations**: all guides should be available in Swahili — contributions welcome
- **Agro-dealer guide corrections**: if you work with cooperatives and something in the onboarding guide is wrong, please open an issue
- **Impact report data**: if you are a researcher using Dira data, open an issue to discuss citation and data access

1. Fork the repository
2. Create a branch: `git checkout -b docs/your-improvement`
3. Submit a Pull Request against `main`

All contributions are accepted under the Apache 2.0 license.

---

## Related Repositories

| Repository | Contents |
|---|---|
| [dira-core](https://github.com/dira-africa/dira-core) | Next.js 14 Telegram Mini App frontend |
| [dira-api](https://github.com/dira-africa/dira-api) | Fastify backend API, AI engine, circular economy payments |
| [dira-contracts](https://github.com/dira-africa/dira-contracts) | Compact smart contracts for Midnight blockchain |

---

## License

Copyright 2025 Dira Africa

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE) for the full text.

Documentation and reports in this repository are additionally released under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) — you may use, adapt, and republish any report or guide with attribution.

The code is a gift to the world. The data, verified on Midnight, is the moat.
