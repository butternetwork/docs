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

    function getInputBeforeFee(
        address _inputToken,
        uint256 _afterFeeAmount,
        bytes calldata _feeData
    ) external view returns (address feeToken, uint256 inputAmount, uint256 nativeFee);
```

encode _swapData

```solidity
  enum DexType {
        AGG,
        UNIV2,
        UNIV3,
        CURVE,
        FILL,
        MIX
  }   
//for now only support FILL and MIX
 struct SwapParam {
        address dstToken;      // swap target token
        address receiver;      // recerver address
        address leftReceiver;  // input token left receiver address
        uint256 minAmount;     // min amount of target token
        SwapData[] swaps;  
    }

    struct SwapData {
        DexType dexType;  
        address callTo;       // excute contract address
        address approveTo;    // erc20 token spender
        uint256 fromAmount;   // swap input token amount
        bytes callData;       // swap function data
    }
```

example

```typescript
        let [wallet, other] = await ethers.getSigners();   
        let sushi_abi = [
            "function swapExactTokensForTokens(uint amountIn,uint amountOutMin,address[] calldata path,address to,uint deadline) external returns (uint[] memory amounts)",
        ];
        let deadline = Math.floor(Date.now() / 1000) + 600;
        let sushi = await ethers.getContractAt(sushi_abi, sushi_router_addr, wallet); 
        let sushi_swap0 = sushi.interface.encodeFunctionData("swapExactTokensForTokens", [
            ethers.utils.parseEther("0.0009"),
            0,
            [weth_addr, usdt_addr],
            butter_router_addr,
            deadline,
        ]);
        let callData0 = ethers.utils.defaultAbiCoder.encode(["uint256[]", "bytes"], [[0], sushi_swap0]);
        let Swap0 = {
            dexType: 4, // fill
            callTo: sushi_router_addr,
            approveTo: sushi_router_addr,
            fromAmount: ethers.utils.parseEther("0.0009"),
            callData: callData0,
        };
        let SwapParam = {
            dstToken: usdt_addr,
            receiver: wallet.address,
            leftReceiver: wallet.address,
            minAmount: 0,
            swaps: [Swap0],
        };
        let swapData = ethers.utils.defaultAbiCoder.encode(
            ["tuple(address,address,address,uint256,tuple(uint8,address,address,uint256,bytes)[])"],
            [
                [
                    SwapParam.dstToken,
                    SwapParam.receiver,
                    SwapParam.leftReceiver,
                    SwapParam.minAmount,
                    [
                        [Swap0.dexType, Swap0.callTo, Swap0.approveTo, Swap0.fromAmount, Swap0.callData]
                    ],
                ],
            ]
        );
```

encode butter bridge data

```solidity
    struct BridgeParam {
        uint256 toChain;    // target chain id
        uint256 nativeFee;  // butter bridge native fee
        bytes receiver;     // receiver address on target chain
        bytes data;         // bridge data 
    }
```

example

```typescript
        let butter_Bridge_Param = {
            gasLimit: gasLimit,             // gasLimit used for target chain call
            refundAddress: wallet.address,  //
            swapData: swapData,             // swapData on target chain
        };
        let b_data = ethers.utils.defaultAbiCoder.encode(
            ["tuple(uint256,bytes,bytes)"],
            [[butter_Bridge_Param.gasLimit, butter_Bridge_Param.refundAddress, butter_Bridge_Param.swapData]]
        );
        let bridgeData = ethers.utils.defaultAbiCoder.encode(
            ["tuple(uint256,uint256,bytes,bytes)"],
            [[target_chain_id, nativeFee, receiver, b_data]]
        );
```

encode callBackData

```solidity
    struct CallbackParam {
        address target;              // target address execute call back
        address approveTo;           // erc20 token spender
        uint256 offset;              // amount location in callBack data or 0
        uint256 extraNativeAmount;   // call back native value
        address receiver;            // receiver address
        bytes data;                  // call back function encode data
    }
```

example

```typescript
        let callBackData = ethers.utils.defaultAbiCoder.encode(
            ["tuple(address,address,uint256,uint256,address,bytes)"],
            [[target, approveTo, offset, extraNativeAmount, receiver, data]]
        ); 
```

encode feeData

```solidity
    enum FeeType {
        FIXED,
        PROPORTION
    }

    struct Fee {
        FeeType feeType;
        address referrer;
        uint256 rateOrNativeFee;
    }
```

example

```typescript
let feeData = ethers.utils.defaultAbiCoder.encode(["tuple(uint8,address,uint256)"], [[1, referrer, rateOrNativeFee]]);
```

encode permit data example

```typescript
let permitData = ethers.utils.defaultAbiCoder.encode(
                        ["address","address","address","uint256","uint256","uint8","bytes32","bytes32"],
                        [permitToken,tokenOwner,spender,amount,deadline,v,r,s]
                 );
```
