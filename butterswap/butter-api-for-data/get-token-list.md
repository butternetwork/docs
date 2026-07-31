# GET Token List

## GET /api/token/list

Returns a paginated list of tokens supported by Butter Network, optionally filtered by chain.

#### Complete Query Example

```url
/api/token/list?page=1&size=20&chainId=56
```

#### Authentication

This endpoint requires an API signature. See [Integration Guide](integration-guide.md#authentication).

#### Request Params

| Name | Location | Type | Required | Description |
| ---- | -------- | ---- | -------- | ----------- |
| `page` | query | string | no | Page number, starting at `1`. Defaults to `1`. Non-numeric values fall back to the default. |
| `size` | query | string | no | Items per page. Defaults to `20`. Non-numeric values fall back to the default. |
| `chainId` | query | string | no | Filter by chain ID, such as `56`. When omitted, tokens from all supported chains are returned. |

#### Responses

| HTTP Status Code | Meaning | Description | Data schema |
| ---------------- | ------- | ----------- | ----------- |
| 200 | OK | Success | Inline |

#### Responses Data

| Name | Type | Description |
| ---- | ---- | ----------- |
| `total` | number | Total number of tokens matching the query. |
| `page` | number | Current page number. |
| `size` | number | Items per page. |
| `pages` | number | Total number of pages. |
| `items` | Array | Token list. |

#### Item Data

| Name | Type | Description |
| ---- | ---- | ----------- |
| `id` | string | Internal token record ID. Serialized as a decimal string. |
| `chainId` | string | Chain ID the token belongs to. Serialized as a decimal string. |
| `address` | string | Token contract address, lowercase for EVM chains. The native token uses the zero address. |
| `decimals` | number | Token decimals. |
| `name` | string | Token name. |
| `symbol` | string | Token symbol. |
| `icon` | string | Token logo URL. May be an empty string when no logo is available. |
| `rank` | number | Sorting weight used by Butter clients. |

> 200 Response

```json
{
  "errno": 0,
  "message": "success",
  "data": {
    "total": 10423,
    "page": 1,
    "size": 20,
    "pages": 522,
    "items": [
      {
        "id": "12027",
        "chainId": "56",
        "address": "0x0000000000000000000000000000000000000000",
        "decimals": 18,
        "name": "Binance Coin",
        "symbol": "BNB",
        "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/binance-smart-chain/0x0000000000000000000000000000000000000000/logo.png",
        "rank": 0
      },
      {
        "id": "12044",
        "chainId": "56",
        "address": "0xbb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c",
        "decimals": 18,
        "name": "Wrapped BNB",
        "symbol": "WBNB",
        "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/binance-smart-chain/0xbb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c/logo.png",
        "rank": 0
      }
    ]
  }
}
```

#### Notes

* `page` is 1-based. Requesting a page beyond `pages` returns an empty `items` array with the same `total`.
* This endpoint does not support filtering by token `address` or `symbol`. Contact Butter Network if you need address-level or symbol-level lookups.
