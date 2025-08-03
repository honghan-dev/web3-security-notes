# 🧱 What’s Inside a Bitcoin Block?

Every 10 minutes, a new Bitcoin block is born — the heartbeat of the Bitcoin network. But what exactly is inside one of these blocks? Let’s crack it open and explore both the **header** and the **payload**.

---

## 🔗 The Block Header — The DNA of Bitcoin

The block header is like a block’s ID card. It's just **80 bytes**, but it contains everything needed to:

- Link the block to its parent
- Prove its legitimacy
- Enable mining and consensus

### 🧩 Block Header Structure

| Field                 | Size      | Description |
|----------------------|-----------|-------------|
| `version`            | 4 bytes   | Signals block validation rules |
| `previous_block_hash`| 32 bytes  | Hash of the parent block (ensures chaining) |
| `merkle_root`        | 32 bytes  | Root hash of all transactions in the block |
| `timestamp`          | 4 bytes   | Time when block was mined |
| `bits`               | 4 bytes   | Current network difficulty (compact format) |
| `nonce`              | 4 bytes   | Value miners adjust to solve the proof-of-work puzzle |

🔐 **Fun Fact**: Miners repeatedly change the nonce to find a block hash that's below the difficulty target defined by `bits`.

---

## 📦 The Block Body — Where the Real Action Happens

The body contains what matters most: **transactions**. These define who sent how much BTC to whom.

### 📝 Transaction Count

- A variable-length integer (`varint`) that tells how many transactions are inside.

### 🔄 Transactions (txs)

Each transaction is a mini-program that transfers BTC. It contains:

- **Inputs**: Where the BTC is coming from (referencing earlier outputs)
- **Outputs**: Where the BTC is going (and how it can be spent)
- **Signatures**: To prove the sender owns the funds

---

### 🧨 OP_RETURN — Hiding Messages in the Blockchain

One unique type of transaction output uses `OP_RETURN`.

**OP_RETURN formatting**

```rust
<OP_RETURN (0x6a)> <PUSHDATA opcode> <data>
```

**Example 1:**

```text
OP_RETURN <36 bytes>
6a24aa21a9ed + witness_root + witness_nonce
└─┘└─┘└──────┘
│  │     │
│  │     └─ Magic number Witness commitment prefix  
│  └─ Push 36 bytes
└─ OP_RETURN (unspendable output)

`6a 24 aa21a9ed <32-byte SHA256 hash>`
```

#### ✳️ What’s OP_RETURN?

- A special script opcode used in an output’s `scriptPubKey`
- Makes the output **provably unspendable**
- Used to embed data (like hashes, messages, NFTs, timestamps)
- 🛑 OP_RETURN outputs do not transfer BTC. They're used to carry metadata, not money.

#### 🧠 Example

```text
Output = {
  value: 0,
  scriptPubKey: "OP_RETURN 48656c6c6f20576f726c64"
}
```

That hex string? It says `Hello World` — forever etched into the blockchain.

Sure! Here's your explanation converted into well-structured Markdown format for easier reading and sharing:

---

# 🔁 The Coinbase Transaction — Paying the Miners

The first transaction in every Bitcoin block is special — it’s the **coinbase transaction**.

---

## 💰 What makes it different?

- It has **no inputs** (it doesn’t spend any existing UTXO).
- It **mints new BTC** (the block subsidy + total transaction fees).
- It **pays the block reward to the miner**.
- It can include **arbitrary data** (e.g., a message or SegWit commitment).

### 🧱 Example Structure (Rust-style pseudocode)

```rust
CoinbaseTx {
    inputs: [
        {
            previous_output: null,
            scriptSig: arbitrary data (e.g., block height, miner tag),
            sequence: 0xffffffff
        }
    ],
    outputs: [
        {
            value: <block reward + tx fees>,
            scriptPubKey: <payout address or script>
        },
        ...
        optional OP_RETURN (e.g., witness commitment)
    ]
}
```

---

## 🧠 Can a coinbase tx have multiple outputs?

Yes!
While there is usually **one main output** that pays the miner, **additional outputs** can:

- Include **metadata**
- Split rewards among **pools**
- Contain **OP\_RETURN** data

---

# 🧨 OP\_RETURN — Hiding Messages in the Blockchain

One unique type of transaction output uses `OP_RETURN`.

### 🧾 Format

```text
<OP_RETURN (0x6a)> <PUSHDATA opcode> <data>
```

#### Example 1: SegWit Commitment (36 bytes)

```text
OP_RETURN <36 bytes>
6a24aa21a9ed + witness_root + witness_nonce
```

Used for embedding:

- Messages
- Hashes
- SegWit commitment

❗ This output is **provably unspendable** by design.

---

# 🧬 SegWit (Segregated Witness)

Introduced in **[BIP141](https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki)** to:

- Solve **transaction malleability**
- **Increase block capacity**

---

## 🪓 How does SegWit work?

- **Separates witness data** (signatures & scripts) from the main transaction body
- Signatures are moved to a **new “witness” section**
- Keeps txids **stable**
- Reduces overall weight (enabling more txs per block)

---

## 📛 Witness Commitment — Where does it go?

SegWit-enabled blocks **commit to all witness data** using an **OP\_RETURN output** in the **coinbase transaction**.

### Format

```text
OP_RETURN 6a24aa21a9ed<witness_merkle_root>
```

- `aa21a9ed`: Magic prefix signaling a **witness commitment**
- 32-byte hash: **Merkle root** of all witness data

🔐 Ensures full nodes can **verify** the integrity of the witness data, even though it’s stored separately.

---

## 📦 Block Weight Math (BIP141 rules)

| Data Type        | Weight Units per Byte |
| ---------------- | --------------------- |
| Non-witness data | 4                     |
| Witness data     | 1                     |

🔧 This **scales block size** up to \~4MB *effective* weight, without raising the original 1MB block size limit.

---

Let me know if you'd like this converted into HTML or Notion format as well.

### 🧠 TL;DR — Anatomy of a Bitcoin Block

```rust
Block
├── Header (80 bytes)
│   ├── Version
│   ├── Previous Block Hash
│   ├── Merkle Root
│   ├── Timestamp
│   ├── Difficulty (bits)
│   └── Nonce
└── Body
    ├── Transaction Count
    └── Transactions
        ├── Coinbase Tx (reward)
        ├── Standard Tx(s)
        └── Optional OP_RETURN data
```

## 👁 Final Thoughts

A Bitcoin block isn't just a chunk of data — it’s a cryptographically linked, timestamped container of financial truth. Every transaction tells a story, and every block is a chapter in the open, immutable ledger we call the blockchain.

Whether you're a miner, developer, or just a curious explorer — understanding the internals of a block brings you one step closer to the foundations of Bitcoin.
