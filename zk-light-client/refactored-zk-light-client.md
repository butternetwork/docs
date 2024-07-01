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

# Refactored ZK Light Client

### Understand ZK-Proof

Zero-knowledge proofs (ZKPs) are a form of cryptographic protocol that allows one party, the prover, to prove to another party, the verifier, that a certain statement is true without revealing any information beyond the validity of the statement itself. In other words, zero-knowledge proofs enable the sharing of proof of knowledge without sharing the knowledge itself.

<figure><img src="../.gitbook/assets/Understand ZK-Proof (1).png" alt=""><figcaption></figcaption></figure>

### Refactored ZK Light Client

In the original light clients verification network, clients need to store the public keys of all current validators along with their respective weights. Verifying the validity of a block requires accessing all the public keys of the validator set and aggregating the public keys of the validators participating in block signing (MAPO Relay Chain uses aggregated BLS signatures). By employing zero-knowledge proofs, however, the process above can be expressed through arithmetic circuits, generating the corresponding zero-knowledge proofs;

In this design, the light client no longer needs to store the public keys and weights of all validators in the current validator set. Instead, it only stores the commitment value (hashed values of the industrial and weight information of all validators encoded) of the public keys and weights of the current validator set. The calculations for aggregating public keys and verifying the validity of the aggregated BLS signature are both expressed through arithmetic circuits and computed using the[ Groth16 protocol](https://codeocean.com/explore/3d07dc79-69aa-47bd-98d8-e319575f9a8a) to generate zero-knowledge proofs.

This now simplifies verifying the legitimacy of a constant-sized zkSNARK proof, thus improving the efficiency of the light clients verification network while maintaining its decentralization.
