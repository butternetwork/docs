---
cover: ../.gitbook/assets/omnichain message passing.jpg
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

# Butter Omnichain Service

### Intro

Butter Omnichain Service message enables projects built on one chain to easily synchronize some project information to other chains, and can also call contract methods on other connected chains.

Butter Omnichain Service uses a light client to verify the transaction of cross-chain messages to ensure that cross-chain messages are authentic and checkable on the chain.

With MOS you can achieve interoperation with two chains:

* Call a contract on chain B from chain A.
* Pack the message changes in chain A and write them into chain B to realize message synchronization

### The Workflow

<figure><img src="https://lh7-us.googleusercontent.com/XU67XChzTdGwH05bMV9NWfGig-IoAkBt-lSTqCxCAygBrkzBuy6RrDgQLJs4-4CCxdPosgG_TAjTAtQwdri4qA8EALQcRU2v5bixEbtiz8VmLSmIw9aAtulbM_LOr2Gj7xFqMEHYkDnot4hygf0olHA" alt=""><figcaption></figcaption></figure>

#### At the source chain

* The user (dApp) sorts out the messages that need to be cross-chained, and organizes the callData called by the target chain
* The dApp calls the transferOut method of MOS, and pays the gas fee for the cross-chain
* MOS sends a cross-chain transaction and pops up a cross-chain message log. You can view the details of the transaction on the browser of the source chain.

#### At map relay chain

* The interchain program detects the message log on the source chain, and builds proof data from the source chain, and calls the transferIn method to notify the MOS contract on the relay chain.
* The Butter Omnichain Service  relay contract confirms the message log of the source chain, verifies the authenticity of the source chain transaction through the light client, judges that it is going to another chain, sends the transaction, and continues to pop up the cross-chain message log.

#### At the destination chain

* The interchain program detects message log on the MAP Relay Chain, and builds proof data from the relay chain, and calls the transferIn method to notify the Butter Omnichain Service contract on the destination chain.
* The Butter Omnichain Service contract verifies the authenticity of the message log through the light client.
* The destination chain pops up the execution log, and completes the message cross-chain contract call.
