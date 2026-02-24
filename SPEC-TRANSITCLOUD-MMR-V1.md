# SPEC-TRANSITCLOUD-MMR-V1

## Purpose
Maintain an **append-only** global audit root for DocumentCurrency artifacts.
Instead of anchoring every document on-chain, anchor a periodic root (e.g. daily) that can attest to large sets of documents.

## Inputs
A sequence of leaves, each derived deterministically from a MetaByte manifest.

### Leaf derivation (recommended)
```
leaf = sha256("METABYTE|" + package_id + "|" + document.sha256 + "|" + content_address.ipfs_cid)
```

## Files
- `proof/mmr/leaves.jsonl` (append-only)
  - each line: `{"t":"ISO8601","package_id":"...","leaf":"0x..."}`
- `proof/mmr/roots/YYYY-MM-DD.root.json` (periodic root)
  - contains leaf_count + root + timestamp

## Root artifact format (minimum)
```json
{
  "date_utc": "YYYY-MM-DD",
  "spec": "SPEC-TRANSITCLOUD-MMR-V1",
  "leaf_count": 1234,
  "root": "0x...",
  "updated_utc": "ISO8601"
}
```

## Upgrade path
This bundle starts with a simple Merkle root for operational reliability.
Next upgrade: full MMR peaks + inclusion proofs.
