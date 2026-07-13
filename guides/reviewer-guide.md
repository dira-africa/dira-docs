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

Independent reviewers, insurance partners, and institutional stakeholders can verify Dira's data integrity using two methods:
1. **Direct Verification** via public Hedera Mirror Nodes (HashScan).
2. **B2B Verification** via the Dira Partner API.

---

## Method 1: Direct Verification via Hedera Mirror Node

This method is recommended for independent audits of historical telemetry archives.

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

### Step 1: Fetch Anchored Hash from HCS
Query a public Hedera Mirror Node for messages written to the Dira HCS Topic ID (`DIRA_HCS_TOPIC_ID`):

```bash
# Example for testnet topic messages
curl -X GET "https://testnet.mirrornode.hedera.com/api/v1/topics/0.0.9556970/messages"
```

Each response message contains:
- `consensus_timestamp`: The exact consensus time.
- `message`: The base64-encoded payload containing the verified telemetry SHA-256 batch hash.
- `sequence_number`: The sequential message number.

Decode the `message` field from base64 to obtain the hex-encoded SHA-256 hash.

### Step 2: Generate the Local Data Hash
1. Download the anonymized CSV data archive corresponding to the target week.
2. Sort the telemetry records chronologically.
3. Calculate the SHA-256 hash of the sorted dataset.

### Step 3: Compare Hashes
Verify that your locally calculated SHA-256 hash matches the decoded HCS message retrieved from the mirror node. An exact match guarantees the dataset has not been modified since consensus was reached.

---

## Method 2: B2B API Verification (For Partners & Insurers)

For automated or programmatic verification of specific readings or photo submissions, Dira provides a structured partner endpoint: `GET /api/partner/verify`.

### 1. Verify by SHA-256 Data Hash
If you have the SHA-256 hash of a crop certificate or telemetry point, query the API:

```bash
curl -X GET "https://api.dira.africa/api/partner/verify?hash=d5e786ef789ab3cd89a12e345f67abcd123e456789abcde0123456789abcdef0" \
  -H "X-API-Key: YOUR_API_KEY"
```

### 2. Verify by HCS Topic and Sequence Number
If you know the HCS topic and sequence number:

```bash
curl -X GET "https://api.dira.africa/api/partner/verify?topic=0.0.9556970&seq=42" \
  -H "X-API-Key: YOUR_API_KEY"
```

### Example Verification Response
A successful verification returns the consensus metadata directly verified against Hedera records:

```json
{
  "success": true,
  "verified": true,
  "attestation": {
    "consensusTimestamp": "1783886848.204061081",
    "sequenceNumber": 42,
    "network": "testnet",
    "topicId": "0.0.9556970",
    "hashscanLink": "https://hashscan.io/testnet/topic/0.0.9556970"
  }
}
```

*Note: All partner queries are tracked in the database usage logs and audit trails to maintain security and enforce rate limits.*
