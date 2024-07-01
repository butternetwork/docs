# GET Swap History by Source Hash

## GET /api/queryBridgeInfoBySourceHash

#### Complete Query Example

[https://bs-app-api.chainservice.io/api/queryBridgeInfoBySourceHash?hash=0x5141a62e5cb24e57f99f0208d34470a4d1043ce089b8b7db8a4a5c8d3fabe49b](https://bs-app-api.chainservice.io/api/queryBridgeInfoBySourceHash?hash=0x5141a62e5cb24e57f99f0208d34470a4d1043ce089b8b7db8a4a5c8d3fabe49b)

#### Request Params

| Name | Location | Type   | Required | Description                    |
| ---- | -------- | ------ | -------- | ------------------------------ |
| hash | query    | string | yes      | Source Chain Transaction Hash. |

#### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

#### Responses Data

| Name | Type       | Description       |
| ---- | ---------- | ----------------- |
| info | JSONObject | Result data info. |

#### Responses Params

| Name             | Type       | Description                                                                                |
| ---------------- | ---------- | ------------------------------------------------------------------------------------------ |
| fromChain        | JSONObject | Source Chain Info.                                                                         |
| - chainId        | String     | Chain Id.                                                                                  |
| - chainName      | String     | Chain name.                                                                                |
| - scanUrl        | String     | Explorer Url.                                                                              |
| - chainImg       | String     | Chain Icon Url.                                                                            |
| relayerChain     | JSONObject | Relayer Chain Info.                                                                        |
| - chainId        | String     | Chain Id.                                                                                  |
| - chainName      | String     | Chain name.                                                                                |
| - scanUrl        | String     | Explorer Url.                                                                              |
| - chainImg       | String     | Chain Icon Url.                                                                            |
| toChain          | JSONObject | Destination Chain Info.                                                                    |
| - chainId        | String     | Chain Id.                                                                                  |
| - chainName      | String     | Chain name.                                                                                |
| - scanUrl        | String     | Explorer Url.                                                                              |
| - chainImg       | String     | Chain Icon Url.                                                                            |
| tokenAddress     | String     | Source Token Address.                                                                      |
| tokenSymbol      | String     | Source Token Symbol.                                                                       |
| timestamp        | String     | Source Transfer Time.                                                                      |
| completeTime     | String     | Cross chain completion time.                                                               |
| amount           | decimal    | Cross amount.                                                                              |
| inAmount         | decimal    | Receive amount.                                                                            |
| fee              | decimal    | Fee amount.                                                                                |
| state            | Integer    | Cross state, 0: crossing, 1: completed                                                     |
| sourceHash       | String     | Source Chain Transaction Hash.                                                             |
| relayerHash      | String     | Relayer Chain Transaction Hash, null if no relay chain is required                         |
| toHash           | String     | Destination Chain Transaction Hash，When not completed, the destination chain hash is null. |
| sourceAddress    | String     | Cross address.                                                                             |
| toAddress        | String     | Receive address.                                                                           |
| sourceToken      | JSONObject | Source Token Info.                                                                         |
| - chainId        | BigInteger | Chain Id.                                                                                  |
| - address        | String     | Token address.                                                                             |
| - name           | String     | Token name.                                                                                |
| - symbol         | String     | Token symbol.                                                                              |
| - decimal        | Integer    | Token decimal.                                                                             |
| - icon           | String     | Token icon url.                                                                            |
| destinationToken | JSONObject | Destination Token Info.                                                                    |
| - chainId        | BigInteger | Chain Id.                                                                                  |
| - address        | String     | Token address.                                                                             |
| - name           | String     | Token name.                                                                                |
| - symbol         | String     | Token symbol.                                                                              |
| - decimal        | Integer    | Token decimal.                                                                             |
| - icon           | String     | Token icon url.                                                                            |
| feeToken         | JSONObject | Fee Token Info.                                                                            |
| - chainId        | BigInteger | Chain Id.                                                                                  |
| - address        | String     | Token address.                                                                             |
| - name           | String     | Token name.                                                                                |
| - symbol         | String     | Token symbol.                                                                              |
| - decimal        | Integer    | Token decimal.                                                                             |
| - icon           | String     | Token icon url.                                                                            |

> Response Examples

> 200 Response

```json5
{
  "code": 200,
  "message": "success",
  "data": {
    "info": {
      "fromChain": {
        "id": 3,
        "chainId": "56",
        "chainName": "BNB Chain",
        "scanUrl": "https://bscscan.com/",
        "chainImg": "https://files.maplabs.io/bridge/bsc.png"
      },
      "relayerChain": {
        "id": 1,
        "chainId": "22776",
        "chainName": "MAP Relayer Chain",
        "scanUrl": "https://mapscan.io/",
        "chainImg": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
      },
      "toChain": {
        "id": 1,
        "chainId": "22776",
        "chainName": "MAP Relayer Chain",
        "scanUrl": "https://mapscan.io/",
        "chainImg": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
      },
      "tokenAddress": "0x55d398326f99059fF775485246999027B3197955",
      "tokenSymbol": "USDT",
      "timestamp": "2023-07-27T12:21:22.000+00:00",
      "completeTime": "2023-07-27T12:23:58.000+00:00",
      "amount": 793.9679079533888,
      "inAmount": 793.1739400454354,
      "fee": "0.793967907953388772USDT",
      "state": 1,
      "sourceHash": "0xfa26d7abef03d57a938b675a46e9fb2edc15003cf50c99c73eeac2de0183d166",
      "relayerHash": null,
      "toHash": "0xf56080d26a008eaecba32e3f99ee38016554cc0ba2a20127b24b81b33dc0d36a",
      "sourceAddress": "0xecef0d873d909730da0f446d3afac15ef19b45b1",
      "toAddress": "0xa06e0f8851438115628c5780480c53017d405e4e",
      "fromTokenDecimal": 18,
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
      "feeToken": {
        "id": 36,
        "chainId": 22776,
        "address": "0x33daba9618a75a7aff103e53afe530fbacf4a3dd",
        "name": "USDT",
        "symbol": "USDT",
        "icon": null,
        "decimal": 18,
        "isMainCurrency": 0
      }
    }
  }
}
```

\


| Name | Location | Type   | Required | Description                    |
| ---- | -------- | ------ | -------- | ------------------------------ |
| hash | query    | string | yes      | Source Chain Transaction Hash. |

#### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

> Response Examples

> 200 Response

```json
{
  "code": 200,
  "message": "success",
  "data": {
    "info": {
      "fromChain": {
        "id": 3,
        "chainId": "56",
        "chainName": "BNB Chain",
        "scanUrl": "https://bscscan.com/",
        "chainImg": "https://files.maplabs.io/bridge/bsc.png"
      },
      "relayerChain": {
        "id": 1,
        "chainId": "22776",
        "chainName": "MAP Relayer Chain",
        "scanUrl": "https://mapscan.io/",
        "chainImg": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
      },
      "toChain": {
        "id": 1,
        "chainId": "22776",
        "chainName": "MAP Relayer Chain",
        "scanUrl": "https://mapscan.io/",
        "chainImg": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png"
      },
      "tokenAddress": "0x55d398326f99059fF775485246999027B3197955",
      "tokenSymbol": "USDT",
      "timestamp": "2023-07-27T12:21:22.000+00:00",
      "completeTime": "2023-07-27T12:23:58.000+00:00",
      "amount": 793.9679079533888,
      "inAmount": 793.1739400454354,
      "fee": "0.793967907953388772USDT",
      "state": 1,
      "sourceHash": "0xfa26d7abef03d57a938b675a46e9fb2edc15003cf50c99c73eeac2de0183d166",
      "relayerHash": null,
      "toHash": "0xf56080d26a008eaecba32e3f99ee38016554cc0ba2a20127b24b81b33dc0d36a",
      "sourceAddress": "0xecef0d873d909730da0f446d3afac15ef19b45b1",
      "toAddress": "0xa06e0f8851438115628c5780480c53017d405e4e",
      "fromTokenDecimal": 18,
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
      "feeToken": {
        "id": 36,
        "chainId": 22776,
        "address": "0x33daba9618a75a7aff103e53afe530fbacf4a3dd",
        "name": "USDT",
        "symbol": "USDT",
        "icon": null,
        "decimal": 18,
        "isMainCurrency": 0
      }
    }
  }
}
```

\
