# XION & zkVerify Blockchain Integration Architecture

Dira Africa leverages **XION** as the primary smart contract layer and **zkVerify** as the zero-knowledge verification engine to secure the provenance of Kenya's climate data network.

---

## Architecture Overview

```
+--------------------------+
|  Farmers & Data Agents   |
+--------------------------+
             |
             |  1. Submissions
             v
+--------------------------+
|        Dira API          |
+--------------------------+
    |                  |
    | 2. Submit Proof  | 3. Submit Anchor & Proof ID
    v                  v
+----------+      +----------+
| zkVerify |      |   XION   |
+----------+      +----------+
```

### 1. Data Ingestion & Triangulation
- Data agents upload barometric syncs 4x daily.
- Farmers upload geotagged crop photos.
- Telemetry data is validated by Dira's backend engine.

### 2. ZK Proof Submission (zkVerify)
- Dira generates ZK proofs certifying that the data points meet the required thresholds without revealing coordinates or raw data.
- The proofs are sent to `zkVerify` for high-throughput, low-cost verification.
- zkVerify returns a verification receipt (`proof_id` and transaction hash).

### 3. State Anchoring (XION)
- Every week, the Merkle root of all telemetry data points is calculated.
- The Merkle root, along with the zkVerify receipt, is committed to the CosmWasm `dira-anchor` contract deployed on XION.
- The CosmWasm contract stores this state publicly so that it can be audited by third parties.
