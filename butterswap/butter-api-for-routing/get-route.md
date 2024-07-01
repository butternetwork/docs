# GET /route

GET get routes from 'tokenIn' to 'tokenOut', support both cross chain and same chain

### **Params**

<table data-header-hidden><thead><tr><th></th><th></th><th></th><th width="129"></th><th></th></tr></thead><tbody><tr><td>Name</td><td>Location</td><td>Type</td><td>Required</td><td>Description</td></tr><tr><td>fromChainId</td><td>query</td><td>string</td><td>yes</td><td>source chain id, the supported chain ID list can be get from endpiont /supportedChainList</td></tr><tr><td>toChainId</td><td>query</td><td>string</td><td>yes</td><td>destination chain id</td></tr><tr><td>amount</td><td>query</td><td>string</td><td>yes</td><td>amount of source token</td></tr><tr><td>tokenInAddress</td><td>query</td><td>string</td><td>yes</td><td>address of source token, use 0x0000000000000000000000000000000000000000 for native token on most blockchains, T9yD14Nj9j7xAB4dbGeiX9h8unkKHxuWwb for native token on Tron</td></tr><tr><td>tokenOutAddress</td><td>query</td><td>string</td><td>yes</td><td>address of destination token</td></tr><tr><td>type</td><td>query</td><td>string</td><td>yes</td><td>swap type, one of "exactIn" and "exactOut"</td></tr><tr><td>slippage</td><td>query</td><td>string</td><td>yes</td><td>slippage of swap, a integer in rang [0, 5000], e.g, 100 means 1%</td></tr><tr><td>entrance</td><td>query</td><td>string</td><td>yes</td><td>entrance of swap, please contact us for applying your dedicated entrance</td></tr></tbody></table>

\


#### Request Example

```bash
GET /route?fromChainId=56&toChainId=22776&amount=1&tokenInAddress=0x0000000000000000000000000000000000000000&tokenOutAddress=0x0000000000000000000000000000000000000000&type=exactIn&slippage=100&entrance=<entrance>
```

### **Responses**

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Sucess      | Inline      |

### **Responses Data Schema**

**Enum**

| Name      | Value              |
| --------- | ------------------ |
| tradeType | 0, means exact in  |
| tradeType | 1, means exact out |

#### Response Examples

1. get route successfully

> 200 Response

```json
{
    "errno": 0,
    "message": "success",
    "data": [
        {
            "diff": "0",
            "bridgeFee": {
                "amount": "0.0002",
                "symbol": "WETH"
            },
            "tradeType": 0,
            "gasFee": {
                "amount": "0.000405",
                "symbol": "BNB"
            },
            "gasEstimated": "135000",
            "timeEstimated": 120,
            "hash": "0x286081342b93d276381a8cf4b43990e3a522fb25d0c50c3467dce7ff4543c92c",
            "timestamp": 1710825324995,
            "srcChain": {
                "chainId": "56",
                "tokenIn": {
                    "address": "0x0000000000000000000000000000000000000000",
                    "name": "BNB",
                    "decimals": 18,
                    "symbol": "BNB",
                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/binance-smart-chain/0x0000000000000000000000000000000000000000/logo.png"
                },
                "tokenOut": {
                    "address": "0x2170Ed0880ac9A755fd29B2688956BD959F933F8",
                    "name": "Wrapped ETH",
                    "decimals": 18,
                    "symbol": "WETH",
                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
                },
                "totalAmountIn": "1.0",
                "totalAmountOut": "0.155833181339839686",
                "route": [
                    {
                        "amountIn": "0.6",
                        "amountOut": "0.093491860635897614",
                        "dexName": "PancakeswapV3",
                        "path": [
                            {
                                "id": "0xD0e226f674bBf064f54aB47F42473fF80DB98CBA",
                                "tokenIn": {
                                    "address": "0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c",
                                    "name": "Wrapped BNB",
                                    "decimals": 18,
                                    "symbol": "WBNB",
                                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/binance-smart-chain/0xbb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c/logo.png"
                                },
                                "tokenOut": {
                                    "address": "0x2170Ed0880ac9A755fd29B2688956BD959F933F8",
                                    "name": "Wrapped ETH",
                                    "decimals": 18,
                                    "symbol": "WETH",
                                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
                                },
                                "fee": "500"
                            }
                        ],
                        "priceImpact": "0.050987"
                    },
                    {
                        "amountIn": "0.4",
                        "amountOut": "0.062341320703942072",
                        "dexName": "UniswapV3",
                        "path": [
                            {
                                "id": "0x47a90A2d92A8367A91EfA1906bFc8c1E05bf10c4",
                                "tokenIn": {
                                    "address": "0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c",
                                    "name": "Wrapped BNB",
                                    "decimals": 18,
                                    "symbol": "WBNB",
                                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/binance-smart-chain/0xbb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c/logo.png"
                                },
                                "tokenOut": {
                                    "address": "0x55d398326f99059fF775485246999027B3197955",
                                    "name": "Tether USD",
                                    "decimals": 18,
                                    "symbol": "USDT",
                                    "icon": "https://files.mapprotocol.io/bridge/usdt.png"
                                },
                                "fee": "100"
                            },
                            {
                                "id": "0xb125aa15Ad943D96e813E4A06d0c34716F897e26",
                                "tokenIn": {
                                    "address": "0x55d398326f99059fF775485246999027B3197955",
                                    "name": "Tether USD",
                                    "decimals": 18,
                                    "symbol": "USDT",
                                    "icon": "https://files.mapprotocol.io/bridge/usdt.png"
                                },
                                "tokenOut": {
                                    "address": "0x2170Ed0880ac9A755fd29B2688956BD959F933F8",
                                    "name": "Wrapped ETH",
                                    "decimals": 18,
                                    "symbol": "WETH",
                                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
                                },
                                "fee": "100"
                            }
                        ],
                        "priceImpact": "0.0389769"
                    }
                ],
                "bridge": "Butter"
            },
            "bridgeChain": {
                "chainId": "22776",
                "tokenIn": {
                    "address": "0x05aB928d446d8ce6761e368c8e7bE03C3168A9ec",
                    "name": "Mapped Wrapped Ether",
                    "decimals": 18,
                    "symbol": "WETH",
                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
                },
                "tokenOut": {
                    "address": "0x05aB928d446d8ce6761e368c8e7bE03C3168A9ec",
                    "name": "Mapped Wrapped Ether",
                    "decimals": 18,
                    "symbol": "WETH",
                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
                },
                "totalAmountIn": "0.155833181339839686",
                "totalAmountOut": "0.155633181339839686",
                "route": [
                    {
                        "amountIn": "0.155833181339839686",
                        "amountOut": "0.155633181339839686",
                        "dexName": "",
                        "path": []
                    }
                ],
                "bridge": "Butter"
            },
            "dstChain": {
                "chainId": "22776",
                "tokenIn": {
                    "address": "0x05aB928d446d8ce6761e368c8e7bE03C3168A9ec",
                    "name": "Mapped Wrapped Ether",
                    "decimals": 18,
                    "symbol": "WETH",
                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
                },
                "tokenOut": {
                    "address": "0x0000000000000000000000000000000000000000",
                    "name": "MAPO",
                    "decimals": 18,
                    "symbol": "MAPO",
                    "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
                },
                "totalAmountIn": "0.155633181339839686",
                "totalAmountOut": "17641.735743500668930946",
                "route": [
                    {
                        "amountIn": "0.155633181339839686",
                        "amountOut": "17641.735743500668930946",
                        "dexName": "HiveswapV3",
                        "path": [
                            {
                                "id": "0x53545E3500958BEF1728f701bCF96AB078498017",
                                "tokenIn": {
                                    "address": "0x05aB928d446d8ce6761e368c8e7bE03C3168A9ec",
                                    "name": "Mapped Wrapped Ether",
                                    "decimals": 18,
                                    "symbol": "WETH",
                                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
                                },
                                "tokenOut": {
                                    "address": "0x13CB04d4a5Dfb6398Fc5AB005a6c84337256eE23",
                                    "name": "Wrapped MAP",
                                    "decimals": 18,
                                    "symbol": "WMAPO",
                                    "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
                                },
                                "fee": "10000"
                            }
                        ],
                        "priceImpact": "1.02419"
                    }
                ],
                "bridge": "Butter"
            },
            "minAmountOut": {
                "amount": "17288.901028630655552328",
                "symbol": "MAPO"
            }
        },
        {
            "diff": "2.11227045810555416126",
            "bridgeFee": {
                "amount": "1.0",
                "symbol": "USDT"
            },
            "tradeType": 0,
            "gasFee": {
                "amount": "0.000405",
                "symbol": "BNB"
            },
            "gasEstimated": "135000",
            "timeEstimated": 120,
            "hash": "0x34d1fbd9a296eabc2847a22011ffb6796d6a898a1a1207b8beb7fd9e28419b7c",
            "timestamp": 1710825324996,
            "srcChain": {
                "chainId": "56",
                "tokenIn": {
                    "address": "0x0000000000000000000000000000000000000000",
                    "name": "BNB",
                    "decimals": 18,
                    "symbol": "BNB",
                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/binance-smart-chain/0x0000000000000000000000000000000000000000/logo.png"
                },
                "tokenOut": {
                    "address": "0x55d398326f99059fF775485246999027B3197955",
                    "name": "Tether USD",
                    "decimals": 18,
                    "symbol": "USDT",
                    "icon": "https://files.mapprotocol.io/bridge/usdt.png"
                },
                "totalAmountIn": "1.0",
                "totalAmountOut": "526.094556583077351061",
                "route": [
                    {
                        "amountIn": "1.0",
                        "amountOut": "526.094556583077351061",
                        "dexName": "UniswapV3",
                        "path": [
                            {
                                "id": "0x47a90A2d92A8367A91EfA1906bFc8c1E05bf10c4",
                                "tokenIn": {
                                    "address": "0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c",
                                    "name": "Wrapped BNB",
                                    "decimals": 18,
                                    "symbol": "WBNB",
                                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/binance-smart-chain/0xbb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c/logo.png"
                                },
                                "tokenOut": {
                                    "address": "0x55d398326f99059fF775485246999027B3197955",
                                    "name": "Tether USD",
                                    "decimals": 18,
                                    "symbol": "USDT",
                                    "icon": "https://files.mapprotocol.io/bridge/usdt.png"
                                },
                                "fee": "100"
                            }
                        ],
                        "priceImpact": "0.0204261"
                    }
                ],
                "bridge": "Butter"
            },
            "bridgeChain": {
                "chainId": "22776",
                "tokenIn": {
                    "address": "0x33DAba9618a75a7AFf103e53AfE530FbAcF4A3DD",
                    "name": "Mapped USDT",
                    "decimals": 18,
                    "symbol": "USDT",
                    "icon": "https://files.mapprotocol.io/bridge/usdt.png"
                },
                "tokenOut": {
                    "address": "0x33DAba9618a75a7AFf103e53AfE530FbAcF4A3DD",
                    "name": "Mapped USDT",
                    "decimals": 18,
                    "symbol": "USDT",
                    "icon": "https://files.mapprotocol.io/bridge/usdt.png"
                },
                "totalAmountIn": "526.094556583077351061",
                "totalAmountOut": "525.094556583077351061",
                "route": [
                    {
                        "amountIn": "526.094556583077351061",
                        "amountOut": "525.094556583077351061",
                        "dexName": "",
                        "path": []
                    }
                ],
                "bridge": "Butter"
            },
            "dstChain": {
                "chainId": "22776",
                "tokenIn": {
                    "address": "0x33DAba9618a75a7AFf103e53AfE530FbAcF4A3DD",
                    "name": "Mapped USDT",
                    "decimals": 18,
                    "symbol": "USDT",
                    "icon": "https://files.mapprotocol.io/bridge/usdt.png"
                },
                "tokenOut": {
                    "address": "0x0000000000000000000000000000000000000000",
                    "name": "MAPO",
                    "decimals": 18,
                    "symbol": "MAPO",
                    "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
                },
                "totalAmountIn": "525.094556583077351061",
                "totalAmountOut": "17269.094571093656059889",
                "route": [
                    {
                        "amountIn": "525.094556583077351061",
                        "amountOut": "17269.094571093656059889",
                        "dexName": "HiveswapV3",
                        "path": [
                            {
                                "id": "0x45e428dFF59008Fa24E11C8d21f82611BE4968Bc",
                                "tokenIn": {
                                    "address": "0x33DAba9618a75a7AFf103e53AfE530FbAcF4A3DD",
                                    "name": "Mapped USDT",
                                    "decimals": 18,
                                    "symbol": "USDT",
                                    "icon": "https://files.mapprotocol.io/bridge/usdt.png"
                                },
                                "tokenOut": {
                                    "address": "0x13CB04d4a5Dfb6398Fc5AB005a6c84337256eE23",
                                    "name": "Wrapped MAP",
                                    "decimals": 18,
                                    "symbol": "WMAPO",
                                    "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
                                },
                                "fee": "10000"
                            }
                        ],
                        "priceImpact": "1.03382"
                    }
                ],
                "bridge": "Butter"
            },
            "minAmountOut": {
                "amount": "16923.712679671782938692",
                "symbol": "MAPO"
            }
        }
    ]
}
```

2. no route found or other error

> 200 Response

```
{
    "errno": <error code>,
    "message": <detailed error message>
}
```

**Note**: error code can be found in [here](error-code-list.md)
