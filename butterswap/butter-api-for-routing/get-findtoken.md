# GET /findToken

GET find the token information by the given address

#### Params

| Name    | Location | Type   | Required | Description |
| ------- | -------- | ------ | -------- | ----------- |
| address | query    | string | yes      | none        |

#### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

#### Request Example

```bash
GET /findToken?address=0x13CB04d4a5Dfb6398Fc5AB005a6c84337256eE23
```

#### Response Examples

> 200 Response

```json
{
  "errno": 0,
  "message": "string",
  "data": [
    {
      "id": 22776,
      "chainId": 22776,
      "address": "0x13CB04d4a5Dfb6398Fc5AB005a6c84337256eE23",
      "blockchainNetwork": "22776",
      "coingeckoId": "",
      "decimals": 18,
      "image": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png",
      "name": "Wrapped MAP",
      "rank": 0,
      "symbol": "WMAPO",
      "tokenSecurity": null,
      "usdprice": 0,
      "usedIniframe": 0
    }
  ]
}
```

\


\
