# GET /supportedChainList

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
    8217,
    4200,
    2649,
    8453,
    81457,
    324,
    5000,
    59144,
    42161,
    10,
    1360108768460801,
    1360104473493505,
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
| 4200             | Merlin Mainnet          |
| 2649             | AILayer                 |
| 8453             | Base                    |
| 81457            | Blast                   |
| 324              | zkSync Mainnet          |
| 5000             | Mantle                  |
| 59144            | Linea                   |
| 42161            | Arbitrum One            |
| 10               | OP Mainnet              |
| 1360108768460801 | Solana Mainnet          |
| 1360104473493505 | TON                     |
| 1360095883558913 | BTC                     |




**Please find all [ButterSwap API Reference](https://bs-router-v3.chainservice.io/docs#/) here.**