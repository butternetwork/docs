# GET Token Detail

## GET /api/token/detail

Returns a single token, looked up by contract address or by symbol.

#### Complete Query Example

```url
/api/token/detail?chainId=56&address=0x55d398326f99059ff775485246999027b3197955
```

```url
/api/token/detail?chainId=56&symbol=USDT
```

#### Authentication

This endpoint requires an API signature. See [Integration Guide](integration-guide.md#authentication).

#### Request Params

| Name | Location | Type | Required | Description |
| ---- | -------- | ---- | -------- | ----------- |
| `address` | query | string | one of the two | Token contract address. Takes precedence when both `address` and `symbol` are supplied. |
| `symbol` | query | string | one of the two | Token symbol, such as `USDT`. Used only when `address` is absent. |
| `chainId` | query | string | no | Chain ID, such as `56`. When omitted, the first matching token across all chains is returned. |

Supply either `address` or `symbol`. Requests with neither are rejected with `errno` `2021`.

#### Responses

| HTTP Status Code | Meaning | Description | Data schema |
| ---------------- | ------- | ----------- | ----------- |
| 200 | OK | Success | Inline |

#### Responses Data

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

`data` is `null` when no token matches the query.

> 200 Response

```json
{
  "errno": 0,
  "message": "success",
  "data": {
    "id": "12053",
    "chainId": "56",
    "address": "0x55d398326f99059ff775485246999027b3197955",
    "decimals": 18,
    "name": "Tether USD",
    "symbol": "USDT",
    "icon": "https://s3.amazonaws.com/map-static-file/mapSwap/binance-smart-chain/0x55d398326f99059ff775485246999027b3197955/logo.png",
    "rank": 0
  }
}
```

> 200 Response, no match

```json
{
  "errno": 0,
  "message": "success",
  "data": null
}
```

#### Errors

| Code | Description |
| ---- | ----------- |
| `2021` | Neither `address` nor `symbol` was supplied. |

Signature errors are listed in the [Integration Guide](integration-guide.md#error-response).

#### Notes

* `address` and `symbol` are matched exactly, not as a prefix or substring. EVM addresses are stored in lowercase, so send them in lowercase.
* Omitting `chainId` is only safe for tokens whose `symbol` or `address` is unique across chains. Symbols such as `USDT` exist on many chains, so pass `chainId` to get a deterministic result.
* To page through every token instead of looking one up, use [GET Token List](get-token-list.md).
