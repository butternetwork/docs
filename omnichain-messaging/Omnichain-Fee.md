# Omnichain Fee
When initiating a cross-chain message, a fee is charged to cover the gas consumption of transactions on other chains. We support payment using various tokens or the source chain token.

Below, we will explain our calculation method in detail:

- Users can choose the gas limit for executing messages on the target chain.
- During the cross-chain message process, we will go through the relay chain, which also incurs some gas consumption. To avoid affecting the execution of messages on the target chain, we also have a base gas limit.
- The gas consumed on the target chain and the diversity of payment methods on the source chain will have different gas prices for calculation.

Finally, we can calculate the exact amount of tokens needed to be paid using the following formula:

```
(gasLimit + baseGasLimit) * gasPrice
```

For ease of use, you can use the following interface to get the base gas limit and gas price for the target chain:

```
function getFeeInfo(
uint256 _chainId,
address _feeToken
) external view override returns (uint256 _base, uint256 _gasPrice, address _receiverAddress);
```
