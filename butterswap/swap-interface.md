# Use butter router to swap an asset across blockchains.

## interface

```solidity
interface IButterRouterV3 {
    enum FeeType {
        FIXED,       // fixed native fee
        PROPORTION   // the proportion of the input token amount
    }

    struct Fee {
        FeeType feeType;
        address referrer;         //address of referrer
        uint256 rateOrNativeFee;  // the proportion or the value of native
    }

    struct BridgeParam {
        uint256 toChain;          // destination chain id
        uint256 nativeFee;        // bridge native fee
        bytes receiver;           // receiver address on destination chain
        bytes data;               // call data on destination chain
    }

    event SwapAndBridge(
        address indexed referrer, // fee referrer
        address indexed initiator,// user who make this swap
        address indexed from,     // msg.sender of function swapAndBridge
        bytes32 transferId,       // a custom unique id
        bytes32 orderId,          // butter cross chain unique id
        address originToken,      // input token address(zero address for native token)
        address bridgeToken,      // token bridged of butter bridge 
        uint256 originAmount,     // input token amount
        uint256 bridgeAmount,     // bridge token amount
        uint256 toChain,          // destination chain id
        bytes to                  // receiver address on destination chain
    );

    event SwapAndCall(
        address indexed referrer, // fee referrer
        address indexed initiator,// user who make this swap
        address indexed from,     // msg.sender of function  swapAndCall
        bytes32 transferId,       // a custom unique id
        address originToken,      // input token address(zero address for native token)
        address swapToken,        // swapped token address
        uint256 originAmount,     // input token amount
        uint256 swapAmount,       // swapped token amount
        address receiver,         // receiver address  
        address target,           // call target address
        uint256 callAmount        // call token used
    );

    event RemoteSwapAndCall(
        bytes32 indexed orderId,  // butter cross chain unique id
        address indexed receiver, // destination chain target token receiver
        address indexed target,   // call target address
        address originToken,      // butter bridge token 
        address swapToken,        // destination chain swap target token
        uint256 originAmount,     // butter bridge token amount
        uint256 swapAmount,       // destination chain swap target token amount
        uint256 callAmount,       // call token used
        uint256 fromChain,        // from chain id
        uint256 toChain,          // destination chain id
        bytes from                // from user address
    );

    // 1. swap: _swapData.length > 0 and _bridgeData.length == 0
    // 2. swap and call: _swapData.length > 0 and _callbackData.length > 0
    function swapAndCall(
        bytes32 _transferId,         // a custom unique id
        address _initiator,          // user who make this swap
        address _srcToken,           // input token
        uint256 _amount,             // input token amount
        bytes calldata _swapData,    // encode data for swap 
        bytes calldata _callbackData,// encode data for call back
        bytes calldata _permitData,  // encode data for erc20 token permit approve
        bytes calldata _feeData      // encode data for fee parameter
    ) external payable;

    // 1. bridge:  _swapData.length == 0 and _bridgeData.length > 0
    // 2. swap and bridge: _swapData.length > 0 and _bridgeData.length > 0
    function swapAndBridge(
        bytes32 _transferId,        // a custom unique id
        address _initiator,         // user who make this swap
        address _srcToken,          // input token
        uint256 _amount,            // input token amount
        bytes calldata _swapData,   // encode data for swap 
        bytes calldata _bridgeData, // encode bridge data
        bytes calldata _permitData, // encode data for erc20 token permit approve
        bytes calldata _feeData     // encode data for fee parameter
    ) external payable returns(bytes32 orderId);

    function getFee(
        address _inputToken,       // input token
        uint256 _inputAmount,      // input token amount
        bytes calldata _feeData    // encode data for fee parameter
    ) external view returns (address feeToken, uint256 tokenFee, uint256 nativeFee, uint256 afterFeeAmount);
//returned value
//feeToken fee token address
//tokenFee fee amount of fee token
//nativeFee native fee amount
//afterFeeAmount _inputAmount minus tokenFee  

```
