# GET Swap History by Source Address

## GET /api/queryBridgeHistoryByAddress

#### Complete Query Example

[https://bs-app-api.chainservice.io/api/queryBridgeHistoryByAddress?page=1\&size=50\&address=0xbf2b8bf2f05222bedde1f3330bd421fb6a0fb375](https://bs-app-api.chainservice.io/api/queryBridgeHistoryByAddress?page=1\&size=50\&address=0xbf2b8bf2f05222bedde1f3330bd421fb6a0fb375)

#### Request Params

| Name    | Location | Type    | Required | Description                                     |
| ------- | -------- | ------- | -------- | ----------------------------------------------- |
| page    | query    | Integer | no       | Integer of page number, default is 1            |
| size    | query    | Integer | no       | Integer of page size, default is 10, max is 100 |
| address | query    | string  | yes      | source address                                  |
| chainId | query    | string  | no       | source chain id                                 |

#### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

#### Responses Data

| Name  | Type      | Description                   |
| ----- | --------- | ----------------------------- |
| list  | JSONArray | List of swap history.         |
| total | Integer   | Total number of swap history. |

#### Responses Params

| Name                    | Type       | Description                                 |
| ----------------------- | ---------- | ------------------------------------------- |
| sourceAddress           | String     | Source address.                             |
| destinationAddress      | String     | Receive address.                            |
| fromChainId             | String     | Source Chain Id.                            |
| toChainId               | String     | Destination Chain Id.                       |
| sourceHash              | String     | Source Chain Transaction Hash.              |
| sourceHeight            | Biginteger | Source Chain Transaction Block Height.      |
| destinationHash         | String     | Destination Chain Transaction Hash.         |
| destinationHeight       | Biginteger | Destination Chain Transaction Block Height. |
| orderId                 | String     | Cross Order Id.                             |
| sourceTokenAddress      | String     | Source Chain Token Address.                 |
| destinationTokenAddress | String     | Destination Chain Token Address.            |
| amount                  | decimal    | Cross amount.                               |
| state                   | Integer    | Cross state, 0: crossing, 1: completed      |
| timestamp               | String     | Cross Transfer Time.                        |
| completeTime            | String     | Cross Complete Time.                        |
| inAmount                | decimal    | Receive Amount.                             |
| sourceChain             | JSONObject | Source Chain Info.                          |
| - chainId               | String     | Chain Id.                                   |
| - chainName             | String     | Chain name.                                 |
| - scanUrl               | String     | Explorer Url.                               |
| - chainImg              | String     | Chain Icon Url.                             |
| destinationChain        | JSONObject | Destination Chain Info.                     |
| - chainId               | String     | Chain Id.                                   |
| - chainName             | String     | Chain name.                                 |
| - scanUrl               | String     | Explorer Url.                               |
| - chainImg              | String     | Chain Icon Url.                             |
| sourceToken             | JSONObject | Source Token Info.                          |
| - chainId               | BigInteger | Chain Id.                                   |
| - address               | String     | Token address.                              |
| - name                  | String     | Token name.                                 |
| - symbol                | String     | Token symbol.                               |
| - decimal               | Integer    | Token decimal.                              |
| - icon                  | String     | Token icon url.                             |
| destinationToken        | JSONObject | Destination Token Info.                     |
| - chainId               | BigInteger | Chain Id.                                   |
| - address               | String     | Token address.                              |
| - name                  | String     | Token name.                                 |
| - symbol                | String     | Token symbol.                               |
| - decimal               | Integer    | Token decimal.                              |
| - icon                  | String     | Token icon url.                             |

> Response Examples

> 200 Response

```json
{
  "code": 200,
  "message": "success",
  "data": {
    "list": [
      {
        "id": 85510,
        "sourceAddress": "0xecef0d873d909730da0f446d3afac15ef19b45b1",
        "destinationAddress": "0xa06e0f8851438115628c5780480c53017d405e4e",
        "fromChainId": "56",
        "toChainId": "22776",
        "sourceHash": "0xfa26d7abef03d57a938b675a46e9fb2edc15003cf50c99c73eeac2de0183d166",
        "sourceHeight": 30328761,
        "destinationHash": "0xf56080d26a008eaecba32e3f99ee38016554cc0ba2a20127b24b81b33dc0d36a",
        "destinationHeight": 6736439,
        "orderId": "0x06c55c661a44abaf1089ea7285926e03d741effd09d2d932916cf99af5a3a7f0",
        "sourceTokenAddress": "0x55d398326f99059ff775485246999027b3197955",
        "destinationTokenAddress": "0x33daba9618a75a7aff103e53afe530fbacf4a3dd",
        "amount": 793967907953388800000,
        "type": 0,
        "state": 1,
        "timestamp": "2023-07-27 12:21:22",
        "sourceChain": {
          "id": 3,
          "chainId": "56",
          "chainName": "BNB Chain",
          "scanUrl": "https://bscscan.com/",
          "chainImg": "https://files.maplabs.io/bridge/bsc.png"
        },
        "destinationChain": {
          "id": 1,
          "chainId": "22776",
          "chainName": "MAP Relayer Chain",
          "scanUrl": "https://mapscan.io/",
          "chainImg": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
        },
        "sourceToken": {
          "id": 37,
          "chainId": 56,
          "address": "0x55d398326f99059fF775485246999027B3197955",
          "name": "USDT",
          "symbol": "USDT",
          "icon": null,
          "decimal": 18,
          "isMainCurrency": 0
        },
        "destinationToken": {
          "id": 36,
          "chainId": 22776,
          "address": "0x33daba9618a75a7aff103e53afe530fbacf4a3dd",
          "name": "USDT",
          "symbol": "USDT",
          "icon": null,
          "decimal": 18,
          "isMainCurrency": 0
        },
        "inAmount": 793173940045435400000,
        "completeTime": "2023-07-27 12:23:58"
      }
      ......
    ],
    "total": 29
  }
}
```

\


\
