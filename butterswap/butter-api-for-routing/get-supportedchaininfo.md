# GET /supportedChainInfo

GET get blockchains' information that Butter Router supports

### Request Parameters
None

### Responses Structure
The response contains the following fields:

| Field             | Type    | Description                                                                                                      |
|-------------------|---------|------------------------------------------------------------------------------------------------------------------|
| errno             | number  | Error code. `0` means success, other values indicate errors, see [error code list](#errors).                     |
| message           | string  | Response message. If the request was successful it is `success`, otherwise it gives corresponding error message. |
| data              | array   | An array of the supported blockchain Ids.                                                                        |


### Request Example

```
GET /supportedChainInfo
```

### Response Examples

> 200 Response

```
{
  "errno": 0,
  "message": "string",
  "data": [
     {
      "id": "1",
      "type": "EVM",
      "name": "Ethereum"
    },
    {
      "id": "137",
      "type": "EVM",
      "name": "Polygon"
    },
    {
      "id": "56",
      "type": "EVM",
      "name": "BSC"
    },
    {
      "id": "22776",
      "type": "EVM",
      "name": "MAP"
    },
    {
      "id": "728126428",
      "type": "EVM",
      "name": "Tron"
    },
    {
      "id": "2649",
      "type": "EVM",
      "name": "AILayer"
    },
    {
      "id": "8453",
      "type": "EVM",
      "name": "Base"
    },
    {
      "id": "59144",
      "type": "EVM",
      "name": "Linea"
    },
    {
      "id": "42161",
      "type": "EVM",
      "name": "Arbitrum"
    },
    {
      "id": "10",
      "type": "EVM",
      "name": "Optimism"
    },
    {
      "id": "8217",
      "type": "EVM",
      "name": "Kaia"
    },
    {
      "id": "196",
      "type": "EVM",
      "name": "XLayer"
    },
    {
      "id": "130",
      "type": "EVM",
      "name": "UniChain"
    },
    {
      "id": "43114",
      "type": "EVM",
      "name": "Avalanche"
    },
    {
      "id": "1360108768460801",
      "type": "Solana",
      "name": "Solana"
    },
    {
      "id": "1360095883558913",
      "type": "BTC",
      "name": "BTC"
    }
  ]
}
```

**Note**: the chain info list may change over time as new chains are added or removed from the Butter Router's support, please request this endpoint to get the latest supported chain info.

**Please find all [ButterSwap API Reference](https://bs-router-v3.chainservice.io/docs#/) here.**