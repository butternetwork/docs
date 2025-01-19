# GET /findToken

GET find the token information by the given address


### Request Parameters

|Name|Location|Type|Required| Description         |
|---|---|---|---|---------------------|
|address|query|string| yes | token address       |

### Responses Structure

| Field             | Type    | Description                                                                                                      |
|-------------------|---------|------------------------------------------------------------------------------------------------------------------|
| errno             | number  | Error code. `0` means success, other values indicate errors, see [error code list](#errors).                     |
| message           | string  | Response message. If the request was successful it is `success`, otherwise it gives corresponding error message. |
| data              | array   | An array of token information with the requested address on supported blockchains.                               |


### Request Example

```bash
GET /findToken?address=0x13CB04d4a5Dfb6398Fc5AB005a6c84337256eE23
```

### Response Examples

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


**Please find all [ButterSwap API Reference](https://bs-router-v3.chainservice.io/docs#/) here.**
