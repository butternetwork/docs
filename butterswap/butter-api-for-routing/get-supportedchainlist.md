# GET /supportedChainList

*Note*: this endpoint is deprecated, please use `/supportedChainInfo` instead.

GET get chain id list that Butter Router supports

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
GET /supportedChainList
```

### Response Examples

> 200 Response

```
{
  "errno": 0,
  "message": "string",
  "data": [
     1,
     137,
     56,
     22776,
     728126428,
     2649,
     8453,
     59144,
     42161,
     10,
     8217,
     196,
     1360108768460801,
     1360095883558913
  ]
}
```

#### Butter Chain ID explanation

| Chain Id         | Blockchain Name         |
|------------------|-------------------------|
| 1                | Ethereum                |
| 137              | Polygon Mainnet         |
| 56               | BNB Smart Chain Mainnet |
| 22776            | MAP Protocol            |
| 728126428        | Tron                    |
| 8217             | Kaia                    |
| 2649             | AILayer                 |
| 8453             | Base                    |
| 59144            | Linea                   |
| 42161            | Arbitrum One            |
| 10               | OP Mainnet              |
| 196              | X Layer Mainnet         |
| 1360108768460801 | Solana Mainnet          |
| 1360095883558913 | BTC                     |


**Note**: the chain ID list may change over time as new chains are added or removed from the Butter Router's support, please request this endpoint to get the latest supported chain list.

**Please find all [ButterSwap API Reference](https://bs-router-v3.chainservice.io/docs#/) here.**