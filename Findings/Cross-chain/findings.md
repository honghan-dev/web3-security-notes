# Cross-chain findings

### **Across V3 – Cross Chain Action Exploit**

A bug in the early return logic allowed a relayer to mark a user’s cross-chain action as completed without actually transferring funds. The relayer could then claim the full refund from LP funds, effectively stealing the user’s assets. [Read More](https://paragraph.com/@zachobront/across-v3-cross-chain-action-vulnerability-disclosure)
