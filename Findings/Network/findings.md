# Blockchain / Network Findings

A curated list of interesting blockchain/network protocol issues for learning and reference.

## Consensus / Chain Integrity Issues

### **Movement Full Node – Permanent Chain Split**

Missing block-height check allowed two blocks at the same height, causing a permanent fork and requiring a hard fork. [Read More](https://medium.com/@yemresaritoprak/permanent-chain-split-in-movement-full-node-anatomy-of-a-6-710-critical-vulnerability-that-fa75fe66a0c7)

### **Story Network – Double Burn Bug**  

Delegating and withdrawing multiple times in the same block could over-burn tokens, causing validator panic. [Read More](https://www.story.foundation/blog/story-network-postmortem)

## Denial of Service

### **Sui Network – Temporary Total Network Shutdown**

A vulnerability in Narwhal’s `GetCertificates` handler allowed a single request with a large number of digests to crash validator nodes, causing a temporary total network shutdown. [Read More](https://immunefi.com/blog/bug-fix-reviews/sui-network-shutdown/)
