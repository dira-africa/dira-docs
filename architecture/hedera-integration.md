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

# Hedera-Native Blockchain Integration Architecture

Dira Africa leverages the **Hedera network** as its core decentralized trust layer to secure the provenance of climate data and run a custodial Climate Token economy.

---

## 1. End-to-End System Flow

```
+---------------------------------------+
|          Telegram Mini App            | <--- User Interface (EN / SW)
|  - Crop captures (Farmer)              |
|  - Barometric sync (Data Agent)       |
+---------------------------------------+
                   |
                   | 1. Submit Readings & Photos
                   v
+---------------------------------------+
|              Dira API                 |
|  - AI Crop Verification               |
|  - Meteorological Triangulation       |
|  - Custodial Wallet Ledger            |
+---------------------------------------+
         /         |         \
        /          |          \
 2. Anchor   3. Mint/Burn   4. Disburse
    Hash        Tokens         Funds
   /               |            \
  v                v             v
+------+       +------+       +------------------------------------+
| HCS  |       | HTS  |       | Redemption Layers                  |
| Topic|       | Token|       | - Pretium Mobile Money             |
+------+       +------+       | - Africa's Talking Airtime         |
                              | - Dira Circle Community Pools      |
                              | - Agro-Dealer Input Vouchers       |
                              +------------------------------------+
```

---

## 2. Component Architecture

### A. Telegram Mini App (`dira-core`)
- **Farmer Interface**: Enables farmers to onboarding, photograph crops bi-weekly, review performance history, and request token redemptions.
- **Data Agent Interface**: Runs passive background synchronization of device barometric pressure readings 4x daily.
- **Custodial UX**: Farmers and agents do not manage public/private keys or pay transaction gas fees. All actions are authorized via regular JWT sessions secured by Telegram authentication.

### B. Verification Backend (`dira-api`)
- **Atmospheric Triangulation**: Cross-references barometric readings against neighboring agent devices and reference weather stations to calculate an anomaly score.
- **AI Crop Verification**: Analyzes uploaded photos to verify crop presence and growth stage using Gemini Vision.
- **Custodial Ledger**: Maintains an internal PostgreSQL database ledger (`token_transactions` & `token_ledger`) as the fast caching layer and account coordinator.

### C. Hedera Consensus Service (HCS)
- **Data Provenance**: Every verified crop photo and barometric reading has its cryptographic SHA-256 hash calculated.
- **Weekly Batch Anchoring**: These hashes are aggregated weekly into a Merkle root and written to a dedicated Hedera HCS Topic ID (`DIRA_HCS_TOPIC_ID`).
- **PII Protection**: Raw data and user identifiers (phone numbers, names, precise coordinates) are **never** published on-chain. Reviewers can only match an off-chain data archive hash against the HCS topic message.

### D. Hedera Token Service (HTS)
- **Climate Token (`DIRA`)**: Minted and burned on-chain representing the platform's Climate Token asset (`DIRA_HTS_TOKEN_ID`).
- **Custodial Treasury Model**: `dira-api` holds the operator key for the HTS token treasury.
  - **Minting**: When a user's data submission passes verification, the backend executes an HTS `TokenMintTransaction` to mint tokens to the treasury, while updating the user's internal SQL balance.
  - **Burning**: When a user initiates a redemption, the backend performs a database transaction deducting their balance, followed by a `TokenBurnTransaction` on HTS to permanently take those tokens out of circulation.

---

## 3. Redemption & Integration Rails

- **Pretium Mobile Money**: The primary cashout layer, serving as a unified B2C mobile-money gateway for Safaricom M-Pesa across Kenya and mobile providers in Uganda.
- **Africa's Talking**: The airtime disbursement channel, delivering immediate top-ups to the user's registered phone number upon burning `DIRA` tokens.
- **Dira Circle**: Community-led cash pools managed by local coordinators who disburse cash payouts and verify agent listings.
- **Agro-Dealer Input Vouchers**: Farmers can burn `DIRA` tokens in exchange for signed, expiring QR codes redeemable at certified agro-dealer partners for high-yield seeds and fertilizers. The redemption records a 3-5% transaction take-rate to fund network operations.
