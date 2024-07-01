---
cover: ../.gitbook/assets/Understanding Light Client (1).jpg
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Understanding Light Client

### Backgroud

Light Clients function by downloading only the block headers of a blockchain rather than the full block data. Block headers contain a summary of the block, including its hash, the hash of the previous block, and a unique identifier called the Merkle root. By using this information, light clients can verify if a particular transaction is included in a block without needing the entire block data.

When a light client wants to confirm a transaction, it requests Merkle proofs from full nodes. These proofs can mathematically verify that a transaction is part of a block, using a tiny amount of data. This efficiency makes light clients ideal for devices with limited storage or bandwidth, such as smartphones or IoT devices.

<figure><img src="../.gitbook/assets/Understanding Light Client-Longest proof-of-work-chain (1).png" alt=""><figcaption></figcaption></figure>



### Issues with Light Client Verification&#x20;

Although light client verfication is more secure and decentralized than solutions such as Multi-Party Computation (MPC), the amount of gas fee consumption with light clients verification network is more costly, which will not be efficient and practical enough to serve for cross-chain purposes. To improve efficiency, light clients can instead validate a ZK-SNARK proof that a block header is valid.
