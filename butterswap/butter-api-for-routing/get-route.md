# GET /route

GET get routes from 'tokenIn' to 'tokenOut', support both cross chain and same chain


### Request Parameters

| Name            |Location|Type| Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|-----------------|---|---|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| fromChainId     |query|string| yes      | source chain id, the supported chain ID list can be get from endpiont /supportedChainList                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | 
| toChainId       |query|string| yes      | destination chain id                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| amount          |query|string| yes      | amount of source token                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | 1.0                                                                  |
| tokenInAddress  |query|string| yes      | address of source token, use 0x0000000000000000000000000000000000000000 for native token on most blockchains, T9yD14Nj9j7xAB4dbGeiX9h8unkKHxuWwb for native token on Tron                                                                                                                                                                                                                                                                                                                                                                                                       |
| tokenOutAddress |query|string| yes      | address of destination token                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| type            |query|string| yes      | swap type, one of "exactIn" and "exactOut"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| slippage        |query|string| yes      | slippage of swap, a integer in range [0, 5000], e.g, 100 means 1%. For cross chain swap, the min slippage is 150， for cross chain from/to TON/BTC, min slippage is 300                                                                                                                                                                                                                                                                                                                                                                                                          |
| receiver        |query|string| no       | receiver on destination chain, it is required when source chain is Solana                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| entrance        | query          | string | yes      | entrance of swap, please contact us for applying your dedicated entrance.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| caller          | query          | string | no       | caller of butter router contract, e.g., the smart contract address who calls butter rotuer, or the user account who directly calls butter router                                                                                                                                                                                                                                                                                                                                                                                                                                |
| affiliate       | query          | string | no       | affiliate nickname and fee rate, the format is '\<nickname\>[:rate]'. If fee rate is not provided, the default base rate (aka source rate) will be used, note that the rate could not be greater than max rate (aka target rate). E.g., for nickname 'butter' which has configured base rate to 0.1% and max rate to 1%, affiliate=butter means the affiliate charges 0.1% affiliate fee and affiliate=butter:50 means it charges 0.5% affiliate fee. For cross chain swap, you can specify multiple affiliates, but for same chain swap, at most one affilate can be accepted. |
| referrer        | query          | string | no       | referrer address to receive the referrer(affiliate) fee in same chain swap. It is required for Solana same chain swap, and optional for EVM same chain swap. If not provided in EVM same chain swap, the default affiliate wallet will be used.                                                                                                                                                                                                                                                                                                                                 |

### Request Example

```bash
GET /route?fromChainId=56&toChainId=137&amount=1&tokenInAddress=0x0000000000000000000000000000000000000000&tokenOutAddress=0x0000000000000000000000000000000000000000&type=exactIn&slippage=150&entrance=<entrance>
```

### Responses Structure

The response contains the following fields:

| Field             | Type    | Description                                                                                                      |
|-------------------|---------|------------------------------------------------------------------------------------------------------------------|
| errno             | number  | Error code. `0` means success, other values indicate errors, see [error code list](#errors).                     |
| message           | string  | Response message. If the request was successful it is `success`, otherwise it gives corresponding error message. |
| data              | array   | Contains data on the swap route path, fees, etc.                                                                 |


#### `data` Field

The `data` field contains an array with one or more routes. Each route has the following fields:

| Field             | Type    | Description                                                                                          |
|-------------------|---------|------------------------------------------------------------------------------------------------------|
| diff              | string  | The percentage difference of the amount out compare to the best route.                               |
| bridgeFee         | object  | Details of the bridge fee which is charged by butter protocol.                                       |
| tradeType         | number  | Trade type. `0` means 'exactIn', `1` means 'exactOut'.                                               |
| gasFee            | object  | Estimated gas fee that the user pays for the transaciton on source blockchain.                       |
| swapFee           | object  | The referral fee payed to referrer.                                                                  |
| feeConfig         | object  | Configuration for fees, including referrer and fee type.                                             |
| gasEstimated      | string  | Estimated gas of the source chain transaction (in gas).                                              |
| gasEstimatedTarget| string  | Estimated gas of the destination chain transaction (in gas).                                         |
| timeEstimated     | number  | Estimated time for the cross chain transaction (in seconds).                                         |
| hash              | string  | Route hash.                                                                                          |
| entrance          | string  | Indicates where the request is from.                                                                 |
| timestamp         | number  | The time at which the request occurred                                                               |
| hasLiquidity      | boolean | Whether liquidity is available for the route path.                                                   |
| srcChain          | object  | Route information on source chain.                                                                   |
| bridgeChain       | object  | Route information on bridge chain. The field is not returned if it's a same chain swap route.        |
| dstChain          | object  | Route information on destination chain. The field is not returned if it's a same chain swap route. |
| totalAmountInUSD  | string  | Total input amount in USD.  This is an optional field.                                               |
| totalAmountOutUSD | string  | Total output amount in USD. This is an optional field.                                               |
| contract          | string  | The contract which the user interacts with on source chain.   This is an optional field.             |
| minAmountOut      | object  | Minimum output amount considering the slippage, with the amount and symbol of the destination token. |

#### Detailed Explanation of Key Fields

##### `bridgeFee` Field

- `amount`: The fee amount for using the bridge.
- `symbol`: The symbol of the fee token (e.g., `USDT`).
- `address`: The contract address for the fee token.
- `chainId`: The chain ID where the fee is paid.
- `in`: The input token details (contract address, name, symbol, etc.).
- `out`: The output token details (contract address, name, symbol, etc.).
- `affiliate`: The affiliate fee details, including the amount and token details.

##### `gasFee` Field

- `amount`: The estimated gas fee in native token.
- `symbol`: The symbol of the gas fee token (e.g., `BNB`).
- `inUSD`: The gas fee in USD.

##### `swapFee` Field

- `nativeFee`: The native fee for the transaction.
- `tokenFee`: The fee in the token being exchanged.

##### `feeConfig` Field

- `feeType`: The fee type, 0 for fixed, 1 for proportional.
- `referrer`: The referrer address.
- `rateOrNativeFee`: The fee percentage if feeType is proportional or amount if fixed.

##### `srcChain`, `bridgeChain`, and `dstChain` Fields

- `chainId`: The ID of the source, bridge, or destination chain.
- `tokenIn` and `tokenOut`: Token details, including contract address, symbol, name, decimals, and icon.
- `totalAmountIn` and `totalAmountOut`: The total amount of tokens being exchanged.
- `route`: The trade route details, including the exchange and token path used.

##### `minAmountOut` Field

- `amount`: The minimum amount of the output token you can expect from the transaction considering the slippage.
- `symbol`: The symbol of the output token.


### Response Examples

1.  get route successfully
> 200 Response

```json
{
  "errno": 0,
  "message": "success",
  "data": [
    {
      "diff": "0",
      "bridgeFee": {
        "amount": "0.000710663038874504",
        "symbol": "WETH",
        "address": "0x05aB928d446d8ce6761e368c8e7bE03C3168A9ec",
        "chainId": 22776,
        "in": {
          "amount": "0.0",
          "token": {
            "address": "0x05aB928d446d8ce6761e368c8e7bE03C3168A9ec",
            "name": "Mapped Wrapped Ether",
            "decimals": 18,
            "symbol": "WETH",
            "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
          }
        },
        "out": {
          "amount": "0.000710663038874504",
          "token": {
            "address": "0x05aB928d446d8ce6761e368c8e7bE03C3168A9ec",
            "name": "Mapped Wrapped Ether",
            "decimals": 18,
            "symbol": "WETH",
            "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
          }
        },
        "affiliate": {
          "amount": "0.0",
          "token": {
            "address": "0x05aB928d446d8ce6761e368c8e7bE03C3168A9ec",
            "decimals": 18,
            "symbol": "ETH",
            "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
          },
          "list": [],
          "data": "0x00"
        }
      },
      "tradeType": 0,
      "gasFee": {
        "amount": "0.000569294",
        "symbol": "BNB",
        "inUSD": "0.3999949723560408"
      },
      "swapFee": {
        "nativeFee": "0.0",
        "tokenFee": "0.0"
      },
      "feeConfig": {
        "feeType": 1,
        "referrer": "0x200AEe9ba7040d778922A763CE8A50948d61AFF5",
        "rateOrNativeFee": 0
      },
      "gasEstimated": "569294",
      "gasEstimatedTarget": "655900",
      "timeEstimated": 120,
      "hash": "0x33123abbfa81d40de9ef349696ad286736c8795ca3abde25e1b84f827813052d",
      "entrance": "<entrance>",
      "timestamp": 1735101377557,
      "hasLiquidity": true,
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
        "totalAmountOut": "0.20145719964828254",
        "route": [
          {
            "amountIn": "1.0",
            "amountOut": "0.20145719964828254",
            "dexName": "OpenOcean",
            "path": [],
            "extra": "0x90411a3200000000000000000000000055877bd7f2ee37bde55ca4b271a3631f3a7ef121000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000001c0000000000000000000000000eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee0000000000000000000000002170ed0880ac9a755fd29b2688956bd959f933f800000000000000000000000055877bd7f2ee37bde55ca4b271a3631f3a7ef121000000000000000000000000aa301070448385cfaac5913a67b16c4392944a8f0000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000002a7ef0afd5b567d00000000000000000000000000000000000000000000000002cbb841767b17ac0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000200aee9ba7040d778922a763ce8a50948d61aff50000000000000000000000000000000000000000000000000000000000000140000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000014000000000000000000000000000000000000000000000000000000000000003000000000000000000000000000000000000000000000000000000000000000420000000000000000000000000bb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000004d0e30db00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000104e5b07cdb00000000000000000000000062fcb3c1794fb95bd8b1a97f6ad5d8a7e4943a1e00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000055877bd7f2ee37bde55ca4b271a3631f3a7ef12100000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000000000000000000000000000000000000000002ebb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c0000642170ed0880ac9a755fd29b2688956bd959f933f800000300000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000000000000000000648a6a1e850000000000000000000000002170ed0880ac9a755fd29b2688956bd959f933f8000000000000000000000000922164bbbd36acf9e854acbbf32facc949fcaeef00000000000000000000000000000000000000000000000002cbb841767b17ac00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000000000000000001a49f8654220000000000000000000000002170ed0880ac9a755fd29b2688956bd959f933f800000000000000000000000000000001000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000004400000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000064d1660f990000000000000000000000002170ed0880ac9a755fd29b2688956bd959f933f8000000000000000000000000aa301070448385cfaac5913a67b16c4392944a8f00000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"
          }
        ],
        "totalAmountOutUSD": "702.8322029367731",
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
        "totalAmountIn": "0.20145719964828254",
        "totalAmountOut": "0.200746536609408036",
        "route": [
          {
            "amountIn": "0.20145719964828254",
            "amountOut": "0.200746536609408036",
            "dexName": "",
            "path": []
          }
        ],
        "bridge": "Butter"
      },
      "dstChain": {
        "chainId": "137",
        "tokenIn": {
          "address": "0x7ceB23fD6bC0adD59E62ac25578270cFf1b9f619",
          "name": "Wrapped Ether",
          "decimals": 18,
          "symbol": "WETH",
          "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
        },
        "tokenOut": {
          "address": "0x0000000000000000000000000000000000000000",
          "name": "POL",
          "decimals": 18,
          "symbol": "POL",
          "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/polygon/0x0000000000000000000000000000000000000000/logo.png"
        },
        "totalAmountIn": "0.200746536609408036",
        "totalAmountOut": "1342.527362693619495308",
        "route": [
          {
            "amountIn": "0.200746536609408036",
            "amountOut": "1342.527362693619495308",
            "dexName": "UniswapV3",
            "path": [
              {
                "id": "0x86f1d8390222A3691C28938eC7404A1661E618e0",
                "tokenIn": {
                  "address": "0x7ceB23fD6bC0adD59E62ac25578270cFf1b9f619",
                  "name": "Wrapped Ether",
                  "decimals": 18,
                  "symbol": "WETH",
                  "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2/logo.png"
                },
                "tokenOut": {
                  "address": "0x0d500B1d8E8eF31E21C99d1Db9A6444d3ADf1270",
                  "name": "Wrapped MATIC",
                  "decimals": 18,
                  "symbol": "WMATIC",
                  "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/polygon/0x0d500b1d8e8ef31e21c99d1db9a6444d3adf1270/logo.png"
                },
                "fee": "500"
              }
            ],
            "priceImpact": "0.0662491"
          }
        ],
        "totalAmountOutUSD": "699.5920155951671",
        "bridge": "Butter"
      },
      "totalAmountInUSD": "702.61582303",
      "totalAmountOutUSD": "699.5920155951671",
      "contract": "0xEE030ec6F4307411607E55aCD08e628Ae6655B86",
      "minAmountOut": {
        "amount": "1322.389452253215202879",
        "symbol": "POL"
      }
    },
    {
      "diff": "0.04449357251697017337",
      "bridgeFee": {
        "amount": "2.359389574856292229",
        "symbol": "USDT",
        "address": "0x33DAba9618a75a7AFf103e53AfE530FbAcF4A3DD",
        "chainId": 22776,
        "in": {
          "amount": "0.0",
          "token": {
            "address": "0x33DAba9618a75a7AFf103e53AfE530FbAcF4A3DD",
            "name": "Mapped USDT",
            "decimals": 18,
            "symbol": "USDT",
            "icon": "https://files.mapprotocol.io/bridge/usdt.png"
          }
        },
        "out": {
          "amount": "2.359389574856292229",
          "token": {
            "address": "0x33DAba9618a75a7AFf103e53AfE530FbAcF4A3DD",
            "name": "Mapped USDT",
            "decimals": 18,
            "symbol": "USDT",
            "icon": "https://files.mapprotocol.io/bridge/usdt.png"
          }
        }
      },
      "tradeType": 0,
      "gasFee": {
        "amount": "0.000568858",
        "symbol": "BNB",
        "inUSD": "0.3996886318571997"
      },
      "swapFee": {
        "nativeFee": "0.0",
        "tokenFee": "0.0"
      },
      "feeConfig": {
        "feeType": 1,
        "referrer": "0x200AEe9ba7040d778922A763CE8A50948d61AFF5",
        "rateOrNativeFee": 0
      },
      "gasEstimated": "568858",
      "gasEstimatedTarget": "1389337",
      "timeEstimated": 120,
      "hash": "0xd5514b5358aed4ebfc99d4f73cde5a11413ec50ba42c83c155678d84a791e913",
      "entrance": "<entrance>",
      "timestamp": 1735101377558,
      "hasLiquidity": true,
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
        "totalAmountOut": "703.129858285430743024",
        "route": [
          {
            "amountIn": "1.0",
            "amountOut": "703.129858285430743024",
            "dexName": "OpenOcean",
            "path": [],
            "extra": "0x90411a3200000000000000000000000055877bd7f2ee37bde55ca4b271a3631f3a7ef121000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000001c0000000000000000000000000eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee00000000000000000000000055d398326f99059ff775485246999027b319795500000000000000000000000055877bd7f2ee37bde55ca4b271a3631f3a7ef121000000000000000000000000aa301070448385cfaac5913a67b16c4392944a8f0000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000002435fe1cbb022857f00000000000000000000000000000000000000000000000261de310c4d9d99ff00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000200aee9ba7040d778922a763ce8a50948d61aff50000000000000000000000000000000000000000000000000000000000000140000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000040000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000014000000000000000000000000000000000000000000000000000000000000003000000000000000000000000000000000000000000000000000000000000000420000000000000000000000000bb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000004d0e30db00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000104e5b07cdb00000000000000000000000047a90a2d92a8367a91efa1906bfc8c1e05bf10c400000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000055877bd7f2ee37bde55ca4b271a3631f3a7ef12100000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000000000000000000000000000000000000000002ebb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c00006455d398326f99059ff775485246999027b319795500000100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000000000000000000648a6a1e8500000000000000000000000055d398326f99059ff775485246999027b3197955000000000000000000000000922164bbbd36acf9e854acbbf32facc949fcaeef0000000000000000000000000000000000000000000000261de310c4d9d99ff000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000000000000000001a49f86542200000000000000000000000055d398326f99059ff775485246999027b319795500000000000000000000000000000001000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000004400000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000064d1660f9900000000000000000000000055d398326f99059ff775485246999027b3197955000000000000000000000000aa301070448385cfaac5913a67b16c4392944a8f00000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000"
          }
        ],
        "totalAmountOutUSD": "702.5940733334173",
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
        "totalAmountIn": "703.129858285430743024",
        "totalAmountOut": "700.770468710574450795",
        "route": [
          {
            "amountIn": "703.129858285430743024",
            "amountOut": "700.770468710574450795",
            "dexName": "",
            "path": []
          }
        ],
        "bridge": "Butter"
      },
      "dstChain": {
        "chainId": "137",
        "tokenIn": {
          "address": "0xc2132D05D31c914a87C6611C10748AEb04B58e8F",
          "name": "Tether USD",
          "decimals": 6,
          "symbol": "USDT",
          "icon": "https://files.mapprotocol.io/bridge/usdt.png"
        },
        "tokenOut": {
          "address": "0x0000000000000000000000000000000000000000",
          "name": "POL",
          "decimals": 18,
          "symbol": "POL",
          "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/polygon/0x0000000000000000000000000000000000000000/logo.png"
        },
        "totalAmountIn": "700.770468",
        "totalAmountOut": "1341.930024307939242544",
        "route": [
          {
            "amountIn": "700.770468",
            "amountOut": "1341.930024307939242544",
            "dexName": "1inch",
            "path": [],
            "extra": "0x07ed2379000000000000000000000000e37e799d5077682fa0a244d46e5649f71457bd09000000000000000000000000c2132d05d31c914a87c6611c10748aeb04b58e8f000000000000000000000000eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee000000000000000000000000e37e799d5077682fa0a244d46e5649f71457bd09000000000000000000000000aa301070448385cfaac5913a67b16c4392944a8f0000000000000000000000000000000000000000000000000000000029c4e8a40000000000000000000000000000000000000000000000451bde7ee52ab952e00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000012000000000000000000000000000000000000000000000000000000000000003e20000000000000000000000000000000000000000000003c40003ae00036400a007e5c0d20000000000000000000000000000000003400001b400019a0000ca0000b05120445fe580ef8d70ff569ab36e80c647af338db351c2132d05d31c914a87c6611c10748aeb04b58e8f0044a6417ed600000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002410f95d3550b62bb80020d6bdbf788f3cf7ad23cd3cadbd9735aff958023239c6a06351201d8b86e3d88cdb2d34688e87e72f388cb541b7c88f3cf7ad23cd3cadbd9735aff958023239c6a0630044e2ad025a00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002a5526fe10b2203000000000000000000000000e37e799d5077682fa0a244d46e5649f71457bd090020d6bdbf787ceb23fd6bc0add59e62ac25578270cff1b9f61900a0c9e75c4800000000000000002d0500000000000000000000000000000000000000000000000000015e0000af00a007e5c0d200000000000000000000000000000000000000000000000000008b00004f02a0000000000000000000000000000000000000000000000006e931b154cd38d5aaee63c1e5001a34eabbe928bf431b679959379b2225d60d9cda7ceb23fd6bc0add59e62ac25578270cff1b9f61941010d500b1d8e8ef31e21c99d1db9a6444d3adf127000042e1a7d4d000000000000000000000000000000000000000000000000000000000000000000a007e5c0d200000000000000000000000000000000000000000000000000008b00004f02a000000000000000000000000000000000000000000000003e32accd905d807d36ee63c1e50086f1d8390222a3691c28938ec7404a1661e618e07ceb23fd6bc0add59e62ac25578270cff1b9f61941010d500b1d8e8ef31e21c99d1db9a6444d3adf127000042e1a7d4d000000000000000000000000000000000000000000000000000000000000000000a0f2fa6b66eeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeee000000000000000000000000000000000000000000000048bf05274212067230000000000000000085220ebb76bd8e70c061111111125421ca6dc452d289314280a0f8842a6500000000000000000000000000000000000000000000000000000000000052fd304d"
          }
        ],
        "totalAmountOutUSD": "699.2807421143855",
        "bridge": "Butter"
      },
      "totalAmountInUSD": "702.61582303",
      "totalAmountOutUSD": "699.2807421143855",
      "contract": "0xEE030ec6F4307411607E55aCD08e628Ae6655B86",
      "minAmountOut": {
        "amount": "1321.801073943320153906",
        "symbol": "POL"
      }
    }
  ]
}
```

2. no route found
> 200 Response

```json
{
    "errno": 2003,
    "message": "No Route Found"
}
```

**Note**: error code can be found in [here](error-code-list.md)
