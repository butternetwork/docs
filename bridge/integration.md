# How to bridge

To perform a cross chain `swapOutToken()` in solidity, here is an example:

For the native gas fee required for `swapOutToken()` you need to call  `getNativeFee()` to get the amount you should send as msg.value.

`getNativeFee()` interface;

```solidity
    function getNativeFee(
        address _token,     //bridge token
        uint256 _gasLimit,  // call gas limit on target chain
        uint256 _toChain    // target chain id
    ) external view returns (uint256);
```

` swapOutToken()` interface

```solidity
    function swapOutToken(
        address _sender,   // user account send this transation
        address _token,    // src token
        bytes memory _to,  // receiver account (if _swapData not empty _to must contract who implement IButterReceiver)
        uint256 _amount,   // token amount
        uint256 _toChain,  // target chain id
        bytes calldata _swapData
    ) external payable returns (bytes32 orderId);
```

First determine the swap fee by call `getNativeFee()`, then call `swapOutToken()` to transfer the asset to the destination chain.

```solidity
// get native fee
uint256 value = IButterBridgeV3(bridgeAddress).getNativeFee(token，gasLimit，toChain);

// perform a butter swapOutToken() in a solidity smart contract function
IButterBridgeV3(bridgeAddress).swapOutToken{value:value}(
    msg.sender,                           // user account send this transatio
    token,                                // bridge token (zero address for native token)
    toAddress,                            // target chain receiver address   
    amount,                               // bridge token amount
    toChain,                               // target chain id
    swapDat                               // encode swap Data
);
```

To perform a `swapOutToken()` using ethers via a frontend, use the abi and call `swapOutToken()` on the Router contract instance:

```typescript
  let [wallet] = await ethers.getSigners();
  let nativeFee = await bridge.getNativeFee(token.address,gasLimit,tochain);
  // if token if ERC20 token
  await(await token.approve(bridge.address,amount)).wait()

 let BridgeParam = {
        gasLimit: gasLimit, // gas limit called by IButterReceiver
        refundAddress: wallet.address, // for src token is OmniToken to receiver refund native fee on target chain
        swapData: swapData, // IButterReceiver -> onReceived -> _payload
    };
let swapData = ethers.utils.defaultAbiCoder.encode(
        ["tuple(uint256,bytes,bytes)"],
        [[BridgeParam.gasLimit, BridgeParam.refundAddress, BridgeParam.swapData]]
    );
   let tx = await bridge.swapOutToken(wallet.address,token.address,to,amount,swapData,{value:nativeFee})
```

`BridgeParam.swapData` if need call contract on target chain  otherwise set `'0x'` for it

need call contract on target chain ? must make sure parameter `_to` is a contract  and implement IButterReceiver.

IButterReceiver

```solidity
interface IButterReceiver {
    //_srcToken received token (wtoken or erc20 token)
    function onReceived(
        bytes32 _orderId,       // order Id
        address _srcToken,      // received token
        uint256 _amount,        // received token amount
        uint256 _fromChain,     // from chain
        bytes calldata _from,   // from account
        bytes calldata _payload // call data
    ) external;
}
```
