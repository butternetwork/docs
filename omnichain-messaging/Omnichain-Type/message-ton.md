## Messaging with Ton Network

## Chain Id and Contract

Check [Contract](../deployed-omnichain-contracts.md) here.

### Ton Testnet contract

`EQBd_ou3bphIB0mcuxFmxqaEMsuHHzj3EipM-GejjWfcaeuu`

## Ton Network message out

### Call message out

```
slice bridge_addr = <bridge address>;
;; message out body
cell body = begin_cell()
        .store_uint(0x136a3529, 32) ;; op::message_out
        .store_uint(0, 64) ;; queryId
        .store_uint(0, 8) ;; relay, 0 or 1
        .store_uint(0, 8) ;; msgType, 0 for message or 1 for calldata
        .store_uint(56, 64) ;; toChain, eg. 56 for bnb
        .storeAddress(<initiator_address>) ;; initiator
        .store_slice(<target>) ;; target address
        .store_uint(200000000, 64) ;; gasLimit
        .store_ref(<payload>) ;; payload, custom data
    ).end_cell();

;; internal message
cell msg = begin_cell()
    .store_uint(0x18, 6)
    .store_slice(bridge_addr)
    .store_coins(50000000) ;; 0.05 TON for fees
    .store_uint(0, 1 + 4 + 4 + 64 + 32 + 1 + 1)
    .store_slice(body)
    .end_cell();
```

- `relay` indicates whether message processing is required on MAP Relay Chain (set to `1` if processed on MAP Relay Chain).
- `msgType` indicates different message, `MESSAGE` (set to `1`) or `CALLDATA` (set to `0`, deprecated, not supported on TON Network).
- `target` is the contract address where the message will be executed upon reaching the target chain
- `payload` is the data intended for cross-chain transmission.
- `gasLimit` is the maximum gas limit allowed for execution on the target chain.

### data example

| parameter | data                                                                   |                                                                          |
|-----------|------------------------------------------------------------------------|--------------------------------------------------------------------------|
| relay     | `0`                                                                    |                                                                          |
| msgType   | `1`                                                                    |                                                                          |
| toChain   | `11155111`                                                             | Sepolia chain id                                                         |
| initiator | `0x01f723e983d1cfc0da138b9046e03ca500dbe8a23e12b960c415ad423615180ecb` | The raw address of <br> `EQD3I-mD0c_A2hOLkEbgPKUA2-iiPhK5YMQVrUI2FRgOy4LB` |
| target    | `0x8c8afd3ff50c4D8e0323815b29E510a77D2c41fd`                           | Executor contract on Sepolia                                             |
| gasLimit  | 300000                                                                 |                                                                          |
| payload   | `0x96a296d224f285c6...`                                                |                                                                          |



## Message to Ton Network

Sending a omni-chain message to TON is the same as sending messages to other chains.
You can directly encode the assembled `MessageData` and then call `transferOut` to send the omni-chain message.
It is essential to ensure that the message data payload is a message that can be recognized by TON.
```
    bytes memory messageData = abi.encode(MessageData({}));
    
    function transferOut(
        uint256 toChain,
        bytes memory messageData,
        address feeToken
    ) external payable returns (bytes32);
```

Here, `toChain` is the TON Network chain id:
- mainnet: `1360104473493505`
- testnet: `1360104473493506`

And check [MessageData](../Butter-Omnichain-Service-explain.md) here.

### data example

| parameter | data                                                                   |                                                                          |
|-----------|------------------------------------------------------------------------|--------------------------------------------------------------------------|
| toChain   | `1360104473493506`                                                     | TON Testnet chain id                                                     |
| relay     | `0`                                                                    |                                                                          |
| msgType   | `1`                                                                    | Message                                                                  |
| target | `0x012bffbd154f9e738634d618e0c8f4928531e3f85c475fc934461f2ccf18bfe5e5` | The raw address of <br> `UQAr_70VT55zhjTWGODI9JKFMeP4XEdfyTRGHyzPGL_l5cHA` |
| gasLimit  | 300000                                                                 |                                                                          |
| payload   | `0x96a296d224f285c6...`                                                |                                                                          |


### Execute on Ton Network

On ton network, will send an `execute` message to the target contract.

```
begin_cell()
    .store_op(op::mapo_execute)
    .store_query_id(query_id)
    .store_uint(1, 64) ;; from chain id
    .store_uint(56, 64) ;; to chain id
    .store_slice(sender_address) ;; sender address
    .store_uint(2, 256) ;; order id
    .store_ref(begin_cell().end_cell()) ;; message
    .end_cell()
```




