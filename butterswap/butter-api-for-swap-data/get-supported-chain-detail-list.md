# GET Supported Chain Detail List

## GET /api/queryChainList

#### Complete Query Example

[https://bs-tokens-api.chainservice.io/api/queryChainList](https://bs-tokens-api.chainservice.io/api/queryChainList)

#### Request Params

| Name      | Location | Type   | Required | Description                         |
| --------- | -------- | ------ | -------- | ----------------------------------- |
| chainId   | query    | string | no       | Chain id, if not set, return all.   |
| chainName | query    | string | no       | Chain name, if not set, return all. |

#### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

#### Responses Data

| Name   | Type  | Description                |
| ------ | ----- | -------------------------- |
| chains | Array | Result support chain list. |

#### Responses Params

| Name                | Type   | Description                               |
| ------------------- | ------ | ----------------------------------------- |
| chainId             | String | Chain id.                                 |
| chainType           | String | Chain type.                               |
| coin                | String | Mainnet coin.                             |
| key                 | String | Query token key                           |
| logoUri             | String | Logo Uri.                                 |
| metamask            | String | Metamask info.                            |
| - chainName         | String | Chain name.                               |
| - blockExplorerUrls | String | Explorer Url.                             |
| - chainId           | String | Chain Id.                                 |
| - nativeCurrency    | String | Mainnet coin info.                        |
| - rpcUrls           | String | Rpc Url.                                  |
| name                | String | Chain name.                               |
| nativeToken         | String | Mainnet coin info.                        |
| - symbol            | String | Token symbol.                             |
| - address           | String | Token address.                            |
| - coinKey           | String | Token key.                                |
| - priceUSD          | String | Token price.                              |
| - chainId           | String | Chain id.                                 |
| - decimals          | String | Token decimal.                            |
| - name              | String | Token name.                               |
| - logoURI           | String | Token icon url.                           |
| isBlock             | String | Whether it is a blacklist, 0, no, 1, yes. |

> Response Examples

> 200 Response

```json
{
  "code": 200,
  "message": "success",
  "data": {
    "chains": [
      {
        "id": 1,
        "chainId": "1",
        "chainType": "EVM",
        "coin": "ETH",
        "key": "ethereum",
        "logoUri": "https://s3.amazonaws.com/map-static-file/mapSwap/ethereum.svg",
        "mainnet": 1,
        "metamask": "{\"chainName\":\"Ethereum Mainnet\",\"blockExplorerUrls\":[\"https://etherscan.io/\"],\"chainId\":\"0x1\",\"nativeCurrency\":{\"symbol\":\"ETH\",\"decimals\":18,\"name\":\"ETH\"},\"rpcUrls\":[\"https://mainnet.infura.io/v3/9aa3d95b3bc440fa88ea12eaa4456161\"]}",
        "multicallAddress": "0xcA11bde05977b3631167028862bE2a173976CA11",
        "name": "Ethereum",
        "nativeToken": "{\"symbol\":\"ETH\",\"address\":\"0x0000000000000000000000000000000000000000\",\"coinKey\":\"ETH\",\"priceUSD\":\"1885.39\",\"chainId\":1,\"decimals\":18,\"name\":\"ETH\",\"logoURI\":\"https://static.debank.com/image/token/logo_url/eth/935ae4e4d1d12d59a99717a24f2540b5.png\"}",
        "tokenlistUrl": "https://gateway.ipfs.io/ipns/tokens.uniswap.org",
        "isBlock": 0
      }
      ......
    ]
  }
}
```

\
