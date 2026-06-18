# Reviewer Guide: Verify Dira Climate Data on XION & zkVerify

Dira Africa anchors weekly weather telemetry and crop health certificate data on the XION public blockchain, verified cryptographically using zero-knowledge proofs via zkVerify.

This guide explains how independent reviewers and institutional partners can verify Dira's data integrity without relying on Dira's backend.

---

## The Verification Flow

```
+------------------+     1. Generate Proof      +------------------+
| Dira Data Node   | -------------------------> |     zkVerify     |
+------------------+                            +------------------+
         |                                                |
         | 3. Submit Anchor & Proof ID                    | 2. Attestation
         v                                                v
+------------------+                            +------------------+
|  XION CosmWasm   | <------------------------- | zkVerify Bridge  |
+------------------+                            +------------------+
```

## Step 1: Query XION CosmWasm Smart Contract

You can query the `dira-anchor` smart contract on XION directly to fetch the Merkle root of any anchored week.

### Command Line Verification
Use `xiond` or standard Cosmos CLI to query contract state:

```bash
xiond query wasm contract-state smart <CONTRACT_ADDRESS> '{"get_week_anchor":{"week_number":202620}}' --node <XION_RPC_URL>
```

This returns the `merkle_root` and `xion_tx_hash` for that week.

---

## Step 2: Verify ZK Proof on zkVerify

When Dira registers a compliance certificate, it submits a ZK proof to zkVerify. zkVerify validates the proof and registers it.

You can check the proof validation status on zkVerify using the `zkverify_proof_id`:

```bash
curl -X GET "https://api.zkverify.io/proofs/verify/<ZKVERIFY_PROOF_ID>"
```

This returns:
- `status`: Verified
- `attestation_tx_hash`: Transaction hash on the zkVerify network.

---

## Step 3: Match locally generated Merkle Root

1. Download the raw anonymized CSV batch for the targeted Week Number from Dira's open data archive.
2. Compute the double SHA-256 Merkle Root of the reading UUIDs sorted alphabetically.
3. Compare your calculated Merkle Root hash against the `merkle_root` returned from XION CosmWasm contract.
