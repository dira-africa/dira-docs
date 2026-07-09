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

Dira Africa leverages **Hedera** as the core decentralized trust layer to secure the provenance of climate data and reward contributors via a custodial climate-token economy.

---

## Architecture Overview

```
+--------------------------+
|  Farmers & Data Agents   | (Telegram Mini App)
+--------------------------+
             |
             |  1. Observations (Photos & Barometric pressure)
             v
+--------------------------+
|        Dira API          |
+--------------------------+
     |                  |
     | 2. Submit Hash   | 3. Mirror Earn / Redeem
     v                  v
+----------+      +----------+
|  Hedera  |      |  Hedera  |
|   HCS    |      |   HTS    |
+----------+      +----------+
(Consensus)        (Tokens)
```

### 1. Data Ingestion & Triangulation
- Data agents upload barometric syncs 4x daily.
- Farmers upload geotagged crop photos bi-weekly.
- Telemetry data is validated by Dira's backend engine (AI image verification and meteorological triangulation).

### 2. Provenance Anchoring (Hedera Consensus Service - HCS)
- Once a crop photo or pressure reading is verified, `dira-api` calculates its SHA-256 hash.
- This hash, along with minimum metadata, is submitted to a dedicated **Hedera Consensus Service (HCS)** topic.
- Only the cryptographic hash is anchored on-chain to verify provenance — **never** raw farmer PII (phone numbers, exact names, or un-triangulated coordinates).

### 3. Rewards & Ledger Mirroring (Hedera Token Service - HTS)
- The Climate Token runs on the **Hedera Token Service (HTS)**.
- `dira-api` manages the internal `token_transactions` SQL ledger as the primary source of truth for balances and performance.
- When tokens are earned or redeemed, the backend triggers corresponding HTS mint or burn operations on-chain.
- Farmers interact via a custodial model within the Telegram Mini App: they do not hold private keys, seed phrases, or manage raw accounts directly.
