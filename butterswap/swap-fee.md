# How is the swap fee calculated?

The swap fee is divided into two parts: one part is charged by the butterSwap, and the other part is charged by the access party. The access party can pass relevant parameters for collecting the fee to butterSwap, allowing butterSwap to collect the fee on their behalf.

The part of  butterSwap consists of two sections, one is the fixed native value,and the other is the input token amount multiply by fee rate;

For  access party they can choose to either use a fixed native value or input a percentage of the amount as the collection fee.

For ease of use, you can use the following interface to get the fee detail:

```solidity
    function getFee(
        address _inputToken,
        uint256 _inputAmount,
        bytes calldata _feeData
    ) external view returns (address feeToken, uint256 tokenFee, uint256 nativeFee, uint256 afterFeeAmount);

```
