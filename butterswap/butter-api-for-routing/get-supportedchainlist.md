# GET /supportedChainList

GET get chain id list that Butter Router supports

#### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

#### Request Example

```
GET /supportedChainList
```

#### Response Examples

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
    "313230561203979757"
  ]
}
```

#### Butter Chain ID explanation

| Chain Id        | Blockchain Name         |
|-----------------|-------------------------|
| 1        | Ethereum                |
| 137      | Polygon Mainnet         |
| 56       | BNB Smart Chain Mainnet |
| 22776    | MAP Protocol            |
| 728126428| Tron                    |
| 4200     | Merlin Mainnet          |
| 2649     | AILayer                 |
| 8453     | Base                    |
| 81457    | Blast                   |
| 324      | zkSync Mainnet          |
| 5000     | Mantle                  |
| 59144    | Linea                   |
| 42161    | Arbitrum One            |
| 10       | OP Mainnet              |
| 1360108768460801       | Solana Mainnet          |
| 1360104473493505       | TON                     |
| 313230561203979757       | BTC                     |




**Please find all [ButterSwap API Reference](https://bs-router-v3.chainservice.io/docs#/) here.**