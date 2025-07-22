# 🌐 What is libp2p?

libp2p is a modular peer-to-peer (P2P) networking stack originally developed by Protocol Labs (creators of IPFS and Filecoin). It provides the infrastructure to build decentralized and distributed applications by enabling secure, scalable, and resilient communication between peers.

Think of it as a toolkit for building your own custom P2P network – instead of relying on centralized servers, each node talks directly to others.

The Rust implementation of libp2p is highly performant, async-ready, and widely used in projects like Polkadot, Substrate, and IPFS.

🧱 Core Components of libp2p (Rust crate)
Here are the key components/modules you’ll encounter in the Rust crate:

## Component Description

| Component               | Description                                                                                               |
| ----------------------- | --------------------------------------------------------------------------------------------------------- |
| **Transport**           | Handles how data is physically transmitted (TCP, WebSockets, QUIC, etc.)                                  |
| **Swarm**               | Local network engine that connects your node to others. It manages all peer-to-peer connections, handles I/O, and routes protocol messages.       |
| **Behaviour**           | Describes the logic of your node (e.g. how to respond to messages, send requests, etc.). You define this. |
| **Identity**            | Handles cryptographic identities (usually using ed25519 keys) for secure peer IDs.                        |
| **PeerId**              | A unique identifier for each node, derived from its public key.                                           |
| **Multiaddr**           | A flexible format for describing network addresses (IP, port, protocol).                                  |
| **Protocols**           | Define how nodes talk to each other (e.g. ping, Kademlia DHT, Gossipsub pubsub).                          |
| **Connection Handling** | Supports NAT traversal, encryption (via Noise or TLS), and stream multiplexing (via Yamux or Mplex).      |

## 🔧 How is libp2p used?

General Workflow
Create a keypair and PeerId

Define network behaviour (custom logic or use built-in protocols like Gossipsub or Kademlia)

Build a Swarm using:

- Transport (e.g. TCP + Noise + Yamux)
- Behaviour
- PeerId

Run the event loop, polling for events and handling network interactions.

## 🪙 Using libp2p to Create a Blockchain

To create a blockchain, you need to enable:

1. Peer discovery – find other nodes (via Kademlia DHT or bootstrap list)

2. Block propagation – share new blocks (via Gossipsub or floodsub)

3. Consensus coordination – submit votes or proposals

4. Transaction gossiping – broadcast and receive txs

5. State sync – ask peers for block data or chain state

### High-Level Architecture

```rust
libp2p (P2P layer)
│
├── Gossipsub (broadcast blocks & txs)
├── Kademlia DHT (peer discovery)
├── Ping/Identify (network liveness)
├── Custom Protocol (e.g. block request/response)
│
└── Blockchain Logic (consensus, execution, storage)
```

#### Address Format Explanation

```rust
/ip4/10.10.0.21/udp/49590/quic-v1
│    │          │   │     │
│    │          │   │     └─ Protocol: QUIC version 1
│    │          │   └─ Port: 49590  
│    │          └─ Transport: UDP
│    └─ IP Address: 10.10.0.21 (Docker container IP)
└─ Protocol: IPv4
```
