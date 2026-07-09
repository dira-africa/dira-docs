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

# Obsolete Rails Retirement

As part of Dira Africa's architecture transition to Hedera-native services and a unified mobile-money rail, the following legacy blockchain and payment components have been retired and deleted from the codebase:

---

## 1. Midnight Smart Contract Integration
* **Retired Components**: `dira-contracts` repository (holding CosmWasm/XION smart contracts and zkVerify zero-knowledge proof circuits) and the `dira-api/contracts/` folder (holding `.compact` smart contracts for Midnight).
* **Reason for Retirement**: Transitioned to Hedera Consensus Service (HCS) for weather telemetry integrity proofs and Hedera Token Service (HTS) for Climate Token management. Because Hedera supports these capabilities out-of-the-box natively, Dira no longer needs custom, immutable on-chain smart contracts or complex off-chain zero-knowledge proof verification networks, greatly reducing operational and auditing overhead.

---

## 2. Safaricom Daraja M-Pesa Integration
* **Retired Components**: `dira-api/src/routes/payments/mpesa.ts` endpoint routes, the Safaricom IP whitelist and timeout/result callback webhooks in `webhooks.ts`, and the direct Daraja OAuth + B2C payment functions in `paymentService.ts`.
* **Reason for Retirement**: Replaced by **Pretium**, which serves as a single unified B2C mobile-money rail covering all major telecommunications providers across East Africa (including both Kenya and Uganda). Consolidating payment flows under Pretium eliminates the need to maintain, secure, and debug custom, direct integrations with individual telco APIs.
