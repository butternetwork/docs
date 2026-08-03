# GET /supportedTokenList

GET the supported token list for every supported chain or for one specified chain.

### Request Parameters

| Name      | Location | Type   | Required | Description                                                                                           |
|-----------|----------|--------|----------|-------------------------------------------------------------------------------------------------------|
| `chainId` | query    | string | no       | Chain ID to filter by. Omit it to return token groups for every chain supported by the Butter Router. |

> **Authentication**: this endpoint supports API Key authentication. See [Integration Guide - Authentication](integration-guide.md#authentication) for details.

### Request Examples

Get token groups for every supported chain:

```bash
GET /supportedTokenList
```

Get the token group for Ethereum only:

```bash
GET /supportedTokenList?chainId=1
```

### Response Structure

| Field     | Type   | Description                                                                                                       |
|-----------|--------|-------------------------------------------------------------------------------------------------------------------|
| `errno`   | number | Error code. `0` means success; other values indicate errors. See the [error code list](error-code-list.md).        |
| `message` | string | Response message. A successful request returns `success`; otherwise it contains the corresponding error message. |
| `data`    | array  | Supported tokens grouped by chain.                                                                                |

Each item in `data` contains:

| Field     | Type   | Description                                                     |
|-----------|--------|-----------------------------------------------------------------|
| `chainId` | number | Supported chain ID.                                             |
| `tokens`  | array  | Complete configured token list for the chain. May be an empty array. |

Each item in `tokens` contains:

| Field               | Type           | Description                                      |
|---------------------|----------------|--------------------------------------------------|
| `id`                | number         | Chain identifier used by the token record; currently matches `chainId`. |
| `chainId`           | number         | Chain ID for the token.                          |
| `address`           | string         | Token address in the chain's address format.     |
| `blockchainNetwork` | string         | Chain ID represented as a string.                |
| `coingeckoId`       | string         | CoinGecko identifier field; currently an empty string. |
| `decimals`          | number         | Number of token decimals.                        |
| `image`             | string         | Token icon URL.                                  |
| `name`              | string         | Token name.                                      |
| `rank`              | number         | Client sorting rank; currently `0`.              |
| `symbol`            | string         | Token symbol.                                    |
| `tokenSecurity`     | string or null | Token security metadata field; currently `null`. |
| `usdprice`          | number         | Token USD price field; currently `0`.            |
| `usedIniframe`      | number         | Embedded-client usage flag; currently `0`.       |

When `chainId` is omitted, `data` contains one group for every supported chain in router configuration order, including groups whose `tokens` array is empty. When `chainId` is provided, `data` is still an array and contains exactly one chain group.

### Response Examples

> 200 Response

```json
{
  "errno": 0,
  "message": "success",
  "data": [
    {
      "chainId": 1,
      "tokens": [
        {
          "id": 1,
          "chainId": 1,
          "address": "0x0000000000000000000000000000000000000000",
          "blockchainNetwork": "1",
          "coingeckoId": "",
          "decimals": 18,
          "image": "https://files.mapprotocol.io/bridge/butter64_64.png",
          "name": "Ether",
          "rank": 0,
          "symbol": "ETH",
          "tokenSecurity": null,
          "usdprice": 0,
          "usedIniframe": 0
        }
      ]
    }
  ]
}
```

An unsupported or unrecognized `chainId` returns an application error with HTTP status 200:

```json
{
  "errno": 2001,
  "message": "The Chain not Support"
}
```

Use [`GET /supportedChainInfo`](get-supportedchaininfo.md) to discover the current supported chain IDs. Token and chain configuration may change over time, so query this endpoint instead of maintaining a static list.

**Please find all [ButterSwap API Reference](https://bs-router-v3.chainservice.io/docs#/) here.**
