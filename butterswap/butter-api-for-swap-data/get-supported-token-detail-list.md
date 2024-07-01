# GET Supported Token Detail List

## GET /api/queryTokenList

#### Complete Query Example

[https://bs-tokens-api.chainservice.io/api/queryTokenList?network=binance-smart-chain\&page=1\&size=10](https://bs-tokens-api.chainservice.io/api/queryTokenList?network=binance-smart-chain\&page=1\&size=10)

#### Request Params

| Name     | Location | Type    | Required | Description                                     |
| -------- | -------- | ------- | -------- | ----------------------------------------------- |
| pageNo   | query    | Integer | no       | Integer of page number, default is 1            |
| pageSize | query    | Integer | no       | Integer of page size, default is 10, max is 100 |
| network  | query    | string  | yes      | Key field in chain list                         |
| symbol   | query    | string  | no       | Token symbol，Support fuzzy query                |

#### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

#### Responses Data

| Name    | Type      | Description             |
| ------- | --------- | ----------------------- |
| results | JSONArray | List of token list.     |
| count   | Integer   | Total number of tokens. |

#### Responses Params

| Name              | Type       | Description     |
| ----------------- | ---------- | --------------- |
| chainId           | String     | Chain id.       |
| address           | String     | Token address.  |
| blockchainNetwork | String     | Chain key.      |
| decimals          | Integer    | Token decimal.  |
| image             | String     | Token icon url. |
| name              | Biginteger | Token name.     |
| symbol            | String     | Token symbol.   |
| usdprice          | decimal    | Token price.    |

> Response Examples

> 200 Response

```
{
  "code": 200,
  "message": "success",
  "data": {
    "count": 12,
    "results": [
      {
        "id": 34744,
        "chainId": "1030",
        "address": "0x0000000000000000000000000000000000000000",
        "blockchainNetwork": "conflux",
        "coingeckoId": null,
        "decimals": 18,
        "image": "https://map-static-file.s3.amazonaws.com/mapSwap/conflux/0x0000000000000000000000000000000000000000.png",
        "name": "Conflux",
        "rank": 0,
        "symbol": "CFX",
        "tokenSecurity": null,
        "usdprice": 0,
        "usedIniframe": 0
      }
......
    ]
  }
}
```

\
