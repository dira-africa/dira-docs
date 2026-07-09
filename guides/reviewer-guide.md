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

# Reviewer Guide: Verify Dira Climate Data on Hedera

Dira Africa anchors weekly weather telemetry and crop health certificate data on the **Hedera Consensus Service (HCS)** to establish tamper-proof data provenance.

This guide explains how independent reviewers and institutional partners can verify Dira's data integrity using a Hedera mirror node.

---

## The Verification Flow

```
+--------------------+        1. Submit SHA-256 Hash        +--------------------+
|   Dira API Node    | -----------------------------------> |    Hedera HCS      |
+--------------------+                                      +--------------------+
         |                                                            |
         |                                                            | 2. Fetch Messages
         v                                                            v
+--------------------+                                      +--------------------+
|  Anonymized CSV    | <----------------------------------- | Hedera Mirror Node |
|  Data Archive      |        3. Verify Hash Match          | (e.g. HashScan)    |
+--------------------+                                      +--------------------+
```

---

## Step 1: Fetch Anchored Hash from Hedera HCS

All verification hashes are published as messages to a dedicated Hedera Consensus Service (HCS) Topic. You can retrieve these messages from any public Hedera Mirror Node.

### Mirror Node API Query
Query the mirror node for messages on the Dira HCS Topic ID:

```bash
curl -X GET "https://mainnet-public.mirrornode.hedera.com/api/v1/topics/<HEDERA_TOPIC_ID>/messages"
```

Each message returned contains:
- `consensus_timestamp`: The exact timestamp when Hedera reached consensus.
- `message`: The base64-encoded payload containing the verified telemetry SHA-256 hash or Merkle root.
- `sequence_number`: The sequential message number.

Decode the `message` field from base64 to obtain the hex-encoded SHA-256 hash representing the data batch.

---

## Step 2: Generate the Data Hash Locally

1. Download the raw anonymized CSV batch for the targeted consensus period from Dira's open data archive.
2. Sort the telemetry records chronologically and calculate the SHA-256 hash (or Merkle root for larger batches) of the sorted data points.

---

## Step 3: Compare the Hashes

Compare your locally computed SHA-256 hash against the decoded HCS message retrieved from the Hedera mirror node:

- If they match exactly, the integrity and consensus timing of the telemetry data are verified.
- If they differ, the local dataset has been altered or does not match the anchored state.
