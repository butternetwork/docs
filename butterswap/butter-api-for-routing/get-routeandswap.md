# GET /routeAndSwap

GET get best routes and generate swap transaction calldata to swap in Butter router

### **Params**Params

<table data-header-hidden><thead><tr><th width="210"></th><th></th><th width="94"></th><th width="124"></th><th></th></tr></thead><tbody><tr><td>Name</td><td>Location</td><td>Type</td><td>Required</td><td>Description</td></tr><tr><td>fromChainId</td><td>query</td><td>string</td><td>yes</td><td>source chain id, the supported chain ID list can be get from endpiont /supportedChainList</td></tr><tr><td>toChainId</td><td>query</td><td>string</td><td>yes</td><td>destination chain id</td></tr><tr><td>amount</td><td>query</td><td>string</td><td>yes</td><td>amount of source token</td></tr><tr><td>tokenInAddress</td><td>query</td><td>string</td><td>yes</td><td>address of source token, use 0x0000000000000000000000000000000000000000 for native token on most blockchains, T9yD14Nj9j7xAB4dbGeiX9h8unkKHxuWwb for native token on Tron</td></tr><tr><td>tokenOutAddress</td><td>query</td><td>string</td><td>yes</td><td>address of destination token</td></tr><tr><td>type</td><td>query</td><td>string</td><td>yes</td><td>swap type, one of "exactIn" and "exactOut"</td></tr><tr><td>slippage</td><td>query</td><td>string</td><td>yes</td><td>slippage of swap, a integer in rang [0, 5000], e.g, 100 means 1%</td></tr><tr><td>entrance</td><td>query</td><td>string</td><td>yes</td><td>entrance of swap, please contact us for applying your dedicated entrance</td></tr><tr><td>from</td><td>query</td><td>string</td><td>yes</td><td>sender address on source chain</td></tr><tr><td>receiver</td><td>query</td><td>string</td><td>yes</td><td>receiver address on destination chain</td></tr><tr><td>callData</td><td>query</td><td>string</td><td>no</td><td>encoded call data if receiver is a contract</td></tr></tbody></table>

### Request Example

```bash
GET /routeAndSwap?fromChainId=56&toChainId=22776&amount=1&tokenInAddress=0x0000000000000000000000000000000000000000&tokenOutAddress=0x0000000000000000000000000000000000000000&type=exactIn&slippage=100&entrance=<entrance>&from=0x2D4C407BBe49438ED859fe965b140dcF1aaB71a9&receiver=0x2D4C407BBe49438ED859fe965b140dcF1aaB71a9
```

### **Responses**

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

**Responses Data Schema**

**Enum**

| Name      | Value |
| --------- | ----- |
| tradeType | 0     |
| tradeType | 1     |

#### Response Examples

1. get best routes and swap transaction calldata successfully

> 200 Response

```json
{
  "errno": 0,
  "message": "success",
  "data": [
    {
      "route": {
        "diff": "0",
        "bridgeFee": {
          "amount": "200.0",
          "symbol": "MAP"
        },
        "tradeType": 0,
        "gasFee": {
          "amount": "0.002809357862805",
          "symbol": "ETH"
        },
        "gasEstimated": "135000",
        "timeEstimated": 1080,
        "hash": "0xc2b702c23f1451684d76b5bdcdaeba639da60ea900f794e45a59d8f8de7c1918",
        "timestamp": 1710825890374,
        "srcChain": {
          "chainId": "1",
          "tokenIn": {
            "address": "0x0000000000000000000000000000000000000000",
            "name": "ETH",
            "decimals": 18,
            "symbol": "ETH",
            "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0x0000000000000000000000000000000000000000/logo.png"
          },
          "tokenOut": {
            "address": "0x9E976F211daea0D652912AB99b0Dc21a7fD728e4",
            "name": "MAP Protocol",
            "decimals": 18,
            "symbol": "MAP",
            "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
          },
          "totalAmountIn": "1.0",
          "totalAmountOut": "113505.546596669069242755",
          "route": [
            {
              "amountIn": "0.8",
              "amountOut": "90672.418897207863894269",
              "dexName": "UniswapV3",
              "path": [
                {
                  "id": "0xd43E4955B5ea62a87386631B01200dD4dC82283c",
                  "tokenIn": {
                    "address": "0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2",
                    "name": "Wrapped Ether",
                    "decimals": 18,
                    "symbol": "WETH",
                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
                  },
                  "tokenOut": {
                    "address": "0x9E976F211daea0D652912AB99b0Dc21a7fD728e4",
                    "decimals": 18,
                    "symbol": "MAP",
                    "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
                  },
                  "fee": "10000"
                }
              ],
              "priceImpact": "1.0777"
            },
            {
              "amountIn": "0.2",
              "amountOut": "22833.127699461205348486",
              "dexName": "UniswapV3",
              "path": [
                {
                  "id": "0x11b815efB8f581194ae79006d24E0d814B7697F6",
                  "tokenIn": {
                    "address": "0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2",
                    "name": "Wrapped Ether",
                    "decimals": 18,
                    "symbol": "WETH",
                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
                  },
                  "tokenOut": {
                    "address": "0xdAC17F958D2ee523a2206206994597C13D831ec7",
                    "name": "Tether USD",
                    "decimals": 6,
                    "symbol": "USDT",
                    "icon": "https://files.mapprotocol.io/bridge/usdt.png"
                  },
                  "fee": "500"
                },
                {
                  "id": "0x84D9B06b335C5270A76dDC4Bf4674D238A5b5F8A",
                  "tokenIn": {
                    "address": "0xdAC17F958D2ee523a2206206994597C13D831ec7",
                    "name": "Tether USD",
                    "decimals": 6,
                    "symbol": "USDT",
                    "icon": "https://files.mapprotocol.io/bridge/usdt.png"
                  },
                  "tokenOut": {
                    "address": "0x9E976F211daea0D652912AB99b0Dc21a7fD728e4",
                    "decimals": 18,
                    "symbol": "MAP",
                    "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
                  },
                  "fee": "3000"
                }
              ],
              "priceImpact": "1.23832"
            }
          ],
          "bridge": "Butter"
        },
        "bridgeChain": {
          "chainId": "22776",
          "tokenIn": {
            "address": "0x13CB04d4a5Dfb6398Fc5AB005a6c84337256eE23",
            "name": "Wrapped MAP",
            "decimals": 18,
            "symbol": "WMAPO",
            "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
          },
          "tokenOut": {
            "address": "0x13CB04d4a5Dfb6398Fc5AB005a6c84337256eE23",
            "name": "Wrapped MAP",
            "decimals": 18,
            "symbol": "WMAPO",
            "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
          },
          "totalAmountIn": "113505.546596669069242755",
          "totalAmountOut": "113305.546596669069242755",
          "route": [
            {
              "amountIn": "113505.546596669069242755",
              "amountOut": "113305.546596669069242755",
              "dexName": "",
              "path": []
            }
          ],
          "bridge": "Butter"
        },
        "dstChain": {
          "chainId": "56",
          "tokenIn": {
            "address": "0x8105ECe4ce08B6B6449539A5db23e23b973DfA8f",
            "name": "wrapped MAP",
            "decimals": 18,
            "symbol": "MAPO",
            "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
          },
          "tokenOut": {
            "address": "0x0000000000000000000000000000000000000000",
            "name": "BNB",
            "decimals": 18,
            "symbol": "BNB",
            "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/binance-smart-chain/0x0000000000000000000000000000000000000000/logo.png"
          },
          "totalAmountIn": "113305.546596669069242755",
          "totalAmountOut": "6.441341217947751802",
          "route": [
            {
              "amountIn": "113305.546596669069242755",
              "amountOut": "6.441341217947751802",
              "dexName": "1inch",
              "path": [],
              "extra": "0x12aa3caf000000000000000000000000e37e799d5077682fa0a244d46e5649f71457bd090000000000000000000000008105ece4ce08b6b6449539a5db23e23b973dfa8f000000000000000000000000eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee000000000000000000000000e37e799d5077682fa0a244d46e5649f71457bd09000000000000000000000000002162b2aee2dd657fb131b28cc34dee6797b66f0000000000000000000000000000000000000000000017fe4e554727fa0cb18300000000000000000000000000000000000000000000000054ec076cae370133000000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000001400000000000000000000000000000000000000000000000000000000000000160000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000bf0000000000000000000000000000000000000000000000a100008b00004f02a000000000000000000000000000000000000000000000000054ec076cae370133ee63c1e501532931fe9160070fb1f07c0a9952c953a89612fd8105ece4ce08b6b6449539a5db23e23b973dfa8f4101bb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c00042e1a7d4d0000000000000000000000000000000000000000000000000000000000000000c0611111111254eeb25477b68fb85ed929f73a96058200b5bd87e5"
            }
          ],
          "bridge": "Butter"
        },
        "minAmountOut": {
          "amount": "6.376927805768274284",
          "symbol": "BNB"
        }
      },
      "txParam": {
        "errno": 0,
        "message": "success",
        "data": [
          {
            "to": "0xbB21e441fb738F54e6eC244e435475096E179d66",
            "data": "0x480a341100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000006200000000000000000000000000000000000000000000000000000000000000d80000000000000000000000000000000000000000000000000000000000000056000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002162b2aee2dd657fb131b28cc34dee6797b66f000000000000000000000000002162b2aee2dd657fb131b28cc34dee6797b66f0000000000000000000000002d4c407bbe49438ed859fe965b140dcf1aab71a90000000000000000000000009e976f211daea0d652912ab99b0dc21a7fd728e40000000000000000000000000000000000000000000017cb9dd4eefee217c43900000000000000000000000000000000000000000000000000000000000000e00000000000000000000000000000000000000000000000000000000000000424efa06465000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000000000000000000000000000009e976f211daea0d652912ab99b0dc21a7fd728e400000000000000000000000000000000000000000000000000000000000000000000000000000000000000002d4c407bbe49438ed859fe965b140dcf1aab71a90000000000000000000000000000000000000000000017cb9dd4eefee217c43900000000000000000000000000000000000000000000000000000000000000c00000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000001a0000000000000000000000000000000000000000000000000000000000000000200000000000000000000000068b3465833fb72a70ecdf485e0e4c7bd8665fc4500000000000000000000000068b3465833fb72a70ecdf485e0e4c7bd8665fc450000000000000000000000000000000000000000000000000b1a2bc2ec50000000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000130235437a1b4bf8b99f0000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000002bc02aaa39b223fe8d0a0e5c4f27ead9083c756cc20027109e976f211daea0d652912ab99b0dc21a7fd728e4000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000200000000000000000000000068b3465833fb72a70ecdf485e0e4c7bd8665fc4500000000000000000000000068b3465833fb72a70ecdf485e0e4c7bd8665fc4500000000000000000000000000000000000000000000000002c68af0bb14000000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000c00000000000000000000000000000000000000000000004c9689174e3961f0a9a00000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000000042c02aaa39b223fe8d0a0e5c4f27ead9083c756cc20001f4dac17f958d2ee523a2206206994597c13d831ec7000bb89e976f211daea0d652912ab99b0dc21a7fd728e400000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000074000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000038000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000014bb21e441fb738f54e6ec244e435475096e179d6600000000000000000000000000000000000000000000000000000000000000000000000000000000000006600000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000064000000000000000000000000000000000000000000000000000000000000005e000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002162b2aee2dd657fb131b28cc34dee6797b66f000000000000000000000000002162b2aee2dd657fb131b28cc34dee6797b66f0000000000000000000000002d4c407bbe49438ed859fe965b140dcf1aab71a90000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000587f660d8d21116c00000000000000000000000000000000000000000000000000000000000000e000000000000000000000000000000000000000000000000000000000000004a4efa0646500000000000000000000000000000000000000000000000000000000000000200000000000000000000000008105ece4ce08b6b6449539a5db23e23b973dfa8f000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002d4c407bbe49438ed859fe965b140dcf1aab71a9000000000000000000000000000000000000000000000000587f660d8d21116c00000000000000000000000000000000000000000000000000000000000000c00000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000040000000000000000000000001111111254eeb25477b68fb85ed929f73a9605820000000000000000000000001111111254eeb25477b68fb85ed929f73a9605820000000000000000000000000000000000000000000017fe4e554727fa0cb18300000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000002c000000000000000000000000000000000000000000000000000000000000000c40000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000024812aa3caf000000000000000000000000e37e799d5077682fa0a244d46e5649f71457bd090000000000000000000000008105ece4ce08b6b6449539a5db23e23b973dfa8f000000000000000000000000eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee000000000000000000000000e37e799d5077682fa0a244d46e5649f71457bd09000000000000000000000000002162b2aee2dd657fb131b28cc34dee6797b66f0000000000000000000000000000000000000000000017fe4e554727fa0cb18300000000000000000000000000000000000000000000000054ec076cae370133000000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000001400000000000000000000000000000000000000000000000000000000000000160000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000bf0000000000000000000000000000000000000000000000a100008b00004f02a000000000000000000000000000000000000000000000000054ec076cae370133ee63c1e501532931fe9160070fb1f07c0a9952c953a89612fd8105ece4ce08b6b6449539a5db23e23b973dfa8f4101bb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c00042e1a7d4d0000000000000000000000000000000000000000000000000000000000000000c0611111111254eeb25477b68fb85ed929f73a96058200b5bd87e50000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
            "value": "0x0de0b6b3a7640000",
            "chainId": "1"
          }
        ]
      }
    }
  ]
}
```

2. get route successfully but fail to get swap transaction calldata

> 200 Response

```json
{
  "errno": 0,
  "message": "success",
  "data": [
    {
      "route": {
        "diff": "0",
        "bridgeFee": {
          "amount": "200.0",
          "symbol": "MAP"
        },
        "tradeType": 0,
        "gasFee": {
          "amount": "0.002809357862805",
          "symbol": "ETH"
        },
        "gasEstimated": "135000",
        "timeEstimated": 1080,
        "hash": "0xc2b702c23f1451684d76b5bdcdaeba639da60ea900f794e45a59d8f8de7c1918",
        "timestamp": 1710825890374,
        "srcChain": {
          "chainId": "1",
          "tokenIn": {
            "address": "0x0000000000000000000000000000000000000000",
            "name": "ETH",
            "decimals": 18,
            "symbol": "ETH",
            "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0x0000000000000000000000000000000000000000/logo.png"
          },
          "tokenOut": {
            "address": "0x9E976F211daea0D652912AB99b0Dc21a7fD728e4",
            "name": "MAP Protocol",
            "decimals": 18,
            "symbol": "MAP",
            "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
          },
          "totalAmountIn": "1.0",
          "totalAmountOut": "113505.546596669069242755",
          "route": [
            {
              "amountIn": "1",
              "amountOut": "113505.546596669069242755",
              "dexName": "UniswapV3",
              "path": [
                {
                  "id": "0xd43E4955B5ea62a87386631B01200dD4dC82283c",
                  "tokenIn": {
                    "address": "0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2",
                    "name": "Wrapped Ether",
                    "decimals": 18,
                    "symbol": "WETH",
                    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
                  },
                  "tokenOut": {
                    "address": "0x9E976F211daea0D652912AB99b0Dc21a7fD728e4",
                    "decimals": 18,
                    "symbol": "MAP",
                    "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
                  },
                  "fee": "10000"
                }
              ],
              "priceImpact": "1.0777"
            }
          ],
          "bridge": "Butter"
        },
        "bridgeChain": {
          "chainId": "22776",
          "tokenIn": {
            "address": "0x13CB04d4a5Dfb6398Fc5AB005a6c84337256eE23",
            "name": "Wrapped MAP",
            "decimals": 18,
            "symbol": "WMAPO",
            "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
          },
          "tokenOut": {
            "address": "0x13CB04d4a5Dfb6398Fc5AB005a6c84337256eE23",
            "name": "Wrapped MAP",
            "decimals": 18,
            "symbol": "WMAPO",
            "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
          },
          "totalAmountIn": "113505.546596669069242755",
          "totalAmountOut": "113305.546596669069242755",
          "route": [
            {
              "amountIn": "113505.546596669069242755",
              "amountOut": "113305.546596669069242755",
              "dexName": "",
              "path": []
            }
          ],
          "bridge": "Butter"
        },
        "dstChain": {
          "chainId": "56",
          "tokenIn": {
            "address": "0x8105ECe4ce08B6B6449539A5db23e23b973DfA8f",
            "name": "wrapped MAP",
            "decimals": 18,
            "symbol": "MAPO",
            "icon": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
          },
          "tokenOut": {
            "address": "0x0000000000000000000000000000000000000000",
            "name": "BNB",
            "decimals": 18,
            "symbol": "BNB",
            "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/binance-smart-chain/0x0000000000000000000000000000000000000000/logo.png"
          },
          "totalAmountIn": "113305.546596669069242755",
          "totalAmountOut": "6.441341217947751802",
          "route": [
            {
              "amountIn": "113305.546596669069242755",
              "amountOut": "6.441341217947751802",
              "dexName": "1inch",
              "path": [],
              "extra": "0x12aa3caf000000000000000000000000e37e799d5077682fa0a244d46e5649f71457bd090000000000000000000000008105ece4ce08b6b6449539a5db23e23b973dfa8f000000000000000000000000eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee000000000000000000000000e37e799d5077682fa0a244d46e5649f71457bd09000000000000000000000000002162b2aee2dd657fb131b28cc34dee6797b66f0000000000000000000000000000000000000000000017fe4e554727fa0cb18300000000000000000000000000000000000000000000000054ec076cae370133000000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000001400000000000000000000000000000000000000000000000000000000000000160000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000bf0000000000000000000000000000000000000000000000a100008b00004f02a000000000000000000000000000000000000000000000000054ec076cae370133ee63c1e501532931fe9160070fb1f07c0a9952c953a89612fd8105ece4ce08b6b6449539a5db23e23b973dfa8f4101bb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c00042e1a7d4d0000000000000000000000000000000000000000000000000000000000000000c0611111111254eeb25477b68fb85ed929f73a96058200b5bd87e5"
            }
          ],
          "bridge": "Butter"
        },
        "minAmountOut": {
          "amount": "6.376927805768274284",
          "symbol": "BNB"
        }
      },
      "txParam": {
        "errno": 2004,
        "message": "Insufficient Liquidity"
      }
    }
  ]
}
```

3. fail to get route

> 200 Response

```
{
    "errno": <error code>,
    "message": <detailed error message>
}
```

**Note**: error code can be found in [here](error-code-list.md)
