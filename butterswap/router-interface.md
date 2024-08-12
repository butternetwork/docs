# Contract Interface

You will need the butter [router interface](broken-reference).

To perform a swap cross chain `swapAndBridge()` in solidity, here is an example:

```solidity
(,,uint256 nativeFee,) = IButterRouterV3(routerAddress).getFee(inputToken,inputAmount,feeData);
IButterRouterV3(routerAddress).swapAndBridge(
                                 transferId,     // custom unique i
                                 initiator       // user who make this swap
                                 inputToke       // input token
                                 inputAmoun      // input token amount
                                 swapData        // encode data for swap 
                                 bridgeData      // encode bridge data
                                 permitData      // encode data for erc20 token permit approve
                                 feeData         // encode data for fee parameter
                               );
```

To perform a `swapAndBridge()` using ethers via a frontend, use the abi and call `swapAndBridge()` on the Router contract instance:

```typescript
let [wallet] = await ethers.getSigners();
let sushi_abi = [
            "function swapExactTokensForTokens(uint amountIn,uint amountOutMin,address[] calldata path,address to,uint deadline) external returns (uint[] memory amounts)"
            ]

let deadline = Math.floor(Date.now() / 1000) + 600;
let sushi = await ethers.getContractAt(sushi_abi, sushi_addr, wallet);

let sushi_swap1 = sushi.interface.encodeFunctionData("swapExactTokensForTokens", [
            amount,
            0,
            [weth_addr, usdt_addr],
            router.address,
            deadline,
        ]);

let ERC20 = [
    "function approve(address spender, uint256 amount) external returns (bool)",
];

let token = await ethers.getContractAt(ERC20, weth_addr, wallet);
await (await token.approve(router.address, amount)).wait();

let bridge_abi = [
            "function getNativeFee(address _token, uint256 _gasLimit, uint256 _toChain) external view returns (uint256)",
        ];

let bridge = await ethers.getContractAt(bridge_abi, bridge_addr, wallet);
let bridgeFee = await bridge.getNativeFee(usdt_addr, gasLimit, toCahin);

// encode fee data(if no refer fee  can set to '0x') 
//FeeType 0 - FIXED native 1 - PROPORTION   token amount
let feeData = ethers.utils.defaultAbiCoder.encode(["tuple(uint8,address,uint256)"], [[1, wallet.address, 50]]);
let routerFee = await router.getFee(usdt_addr,usdt_amount,feeData)
let native = routerFee.nativeFee.add(bridgeFee);

// offsets  the swap amount location - set it to adjust the swap input amount,or empty list
let callData = ethers.utils.defaultAbiCoder.encode(["uint256[]", "bytes"], [[0], sushi_swap1]);
// dexType
//  enum DexType {
//        AGG,
//        UNIV2,
//        UNIV3,
//        CURVE,
//        FILL,
//       MIX
//  }  
//for now only support FILL and MIX 
let Swap1 = {
            dexType: 4,
            callTo: sushi.address,
            approveTo: sushi.address,
            fromAmount: amount,
            callData: callData,
        };

let SwapParam = {
            dstToken: usdt_addr,
            receiver: wallet.address,
            leftReceiver: wallet.address,
            minAmount: 0,
            swaps: [Swap1],
        };

// encode swap data 
let swapData = ethers.utils.defaultAbiCoder.encode(
            ["tuple(address,address,address,uint256,tuple(uint8,address,address,uint256,bytes)[])"],
            [
                [
                    SwapParam.dstToken,
                    SwapParam.receiver,
                    SwapParam.leftReceiver,
                    SwapParam.minAmount,
                    [
                        [Swap0.dexType, Swap0.callTo, Swap0.approveTo, Swap0.fromAmount, Swap0.callData],
                        [Swap1.dexType, Swap1.callTo, Swap1.approveTo, Swap1.fromAmount, Swap1.callData],
                    ],
                ],
            ]
        );

// encode bridgeData
let target_swapData = "0x";
let BridgeParam = {
            gasLimit: gasLimit,
            refundAddress: wallet.address,
            swapData: target_swapData,
        };
let b_data = ethers.utils.defaultAbiCoder.encode(
            ["tuple(uint256,bytes,bytes)"],
            [[BridgeParam.gasLimit, BridgeParam.refundAddress, BridgeParam.swapData]]
        );

let bridgeData = ethers.utils.defaultAbiCoder.encode(
            ["tuple(uint256,uint256,bytes,bytes)"],
            [[tochain, bridgeFee, to, b_data]]
        );

let permitData = "0x"
let tx = await router.swapAndBridge(transferId,initiator,weth_addr,amount,swapData,bridgeData,permitData,feeData)
```

encode permit data example

```typescript
let permitData = ethers.utils.defaultAbiCoder.encode(
                        ["address","address","address","uint256","uint256","uint8","bytes32","bytes32"],
                        [permitToken,tokenOwner,spender,amount,deadline,v,r,s]
                 );
```
