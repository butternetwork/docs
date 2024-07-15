# Use butter bridge to transfer an asset across blockchains.

## interface

#### IButterBridgeV3

```solidity

interface IButterBridgeV3 {

    struct BridgeParam {
        uint256 gasLimit;
        bytes refundAddress;
        bytes swapData;
    }

    function swapOutToken(
        address _sender,   // user account send this transation
        address _token,    // src token
        bytes memory _to,  // receiver account (if _swapData not empty _to must contract who implement IButterReceiver)
        uint256 _amount,   // token amount
        uint256 _toChain,  // target chain id
        bytes calldata _swapData
    ) external payable returns (bytes32 orderId);


    function getNativeFee(
        address _token,
        uint256 _gasLimit,
        uint256 _toChain
    ) external view returns (uint256);


    event CollectFee(bytes32 indexed orderId, address indexed token, uint256 value);

    event SwapOut(
        bytes32 indexed orderId, // orderId
        uint256 indexed tochain, // to chain
        address indexed token,   // token to across chain 
        uint256 amount,          // amount to transfer
        address from,            // account send this transation
        address caller,          // msg.sender call swapOutToken
        bytes to,                // account receiver on target chain
        bytes outToken,          // token bridge to target chain(token is native this maybe wtoken)
        uint256 gasLimit,        // gasLimit for call on target chain 
        uint256 messageFee       // native amount for pass message  
    );
}

```

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
