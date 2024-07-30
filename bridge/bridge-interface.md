# Butter Bridge Interface

## import

Directly import the bridge interface using the following code.
```solidity
import "@butternetwork/bridge/contracts/interface/IButterMosV2.sol";
```
Make sure to install the package with 'npm install @butternetwork/bridge before usage.

## swapOutToken

```solidity
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

```

## getNativeFee

```solidity

    function getNativeFee(
        address _token,
        uint256 _gasLimit,
        uint256 _toChain
    ) external view returns (uint256);

}

```

## IButterReceiver

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