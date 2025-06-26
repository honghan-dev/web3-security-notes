# 🛡️ Cryptography in Modern Blockchains

## 1. BLS (Boneh–Lynn–Shacham) Signatures

A pairing-based signature scheme that supports signature aggregation — allowing multiple signatures to be combined into one.

This is especially useful in Proof-of-Stake (PoS) blockchains, where many validators sign the same message (e.g., block attestations).

BLS is typically used with the BLS12-381 elliptic curve, which offers strong 128-bit security and efficient pairing operations.

### Used in

BLS12-381 + BLS — Ethereum 2.0 (validators), Chia, Filecoin

## 2. User Transaction Signatures

Most user-level (EOA) transactions prioritize speed, simplicity, and wide compatibility.

**ECDSA (secp256k1)**

- Used in Bitcoin, Ethereum (Layer 1), and many EVM-compatible chains.
- Known for efficiency and broad hardware/software support.

**Ed25519**

- A modern signature scheme based on twisted Edwards curves.
- Deterministic and faster to verify, with smaller keys and signatures.
- Popular in networks like Solana, Polkadot, Cosmos, and Tezos.

### Used in

ECDSA (secp256k1) — Bitcoin, Ethereum (EOAs)

Ed25519 — Solana, Cosmos, Polkadot, Tezos
