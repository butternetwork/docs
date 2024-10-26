## Messaging with Ton Network

## Chain Id and Contract

Check [Contract](../deployed-omnichain-contracts.md) here.

## Ton Network message out

### Call message out

```
slice bridge_addr = <bridge address>;
;; message out body
cell body = begin_cell()
    .store_uint(0x136a3529, 32) ;; op::message_out
    .store_uint(0, 64) ;; queryId
    .store_ref(
        begin_cell()
            .store_uint(0, 8) ;; relay, 0 or 1
            .store_uint(0, 8) ;; msgType, 0 for message or 1 for calldata
            .store_uint(56, 64) ;; toChain, eg. 56 for bnb
            .store_slice(begin_cell().store_uint(0x70997970c51812dc3a010c7d01b50e0d17dc79c8, 512).end_cell().begin_parse()) ;; targetAddress
            .store_ref(begin_cell().store_uint(1, 8).end_cell()) ;; payload, custom data
            .store_uint(200000000, 64) ;; gasLimit
            .end_cell()
    )
    .end_cell();

;; internal message
cell msg = begin_cell()
    .store_uint(0x18, 6)
    .store_slice(bridge_addr)
    .store_coins(50000000) ;; 0.05 TON for fees
    .store_uint(0, 1 + 4 + 4 + 64 + 32 + 1 + 1)
    .store_slice(body)
    .end_cell();
```

- `relay` indicates whether message processing is required on MAP Relay Chain.
- `msgType` indicates different message, `MESSAGE` or `CALLDATA`.
- `target` is the contract address where the message will be executed upon reaching the target chain
- `payload` is the data intended for cross-chain transmission.
- `gasLimit` is the maximum gas limit allowed for execution on the target chain.


### External out message
If the omni-chain message is sent successfully, an external out message will be generated, similar to an EVM event.
```
begin_cell()
    .store_uint(ton_chainId, 64)
    .store_uint(to_chain, 64)
    .store_uint(order_id, 64)
    .store_slice(sender_address)
    .store_ref(args)
.end_cell()
```

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

