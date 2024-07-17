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
    1030,
    1360100178526209,
    22776,
    728126428,
    8217,
    1501,
    4200,
    2649,
    8453,
    81457,
    324,
    223,
    810180,
    5000,
    59144,
    534352,
    42161,
    10
  ]
}
```

#### Butter Chain ID explanation

| Chain Id         | Blockchain Name         |
| ---------------- | ----------------------- |
| 1                | Ethereum                |
| 137              | Polygon Mainnet         |
| 56               | BNB Smart Chain Mainnet |
| 1030             | Conflux eSpace          |
| 1360100178526209 | Near Protocol           |
| 22776            | MAP Protocol            |
| 728126428        | Tron                    |
| 8217             | Klaytn Mainnet Cypress  |
| 1501             | BEVM Canary             |
| 4200             | Merlin Mainnet          |
| 2649             | AILayer                 |
| 8453             | Base                    |
| 81457            | Blast                   |
| 324              | zkSync Mainnet          |
| 223              | B2 Mainnet              |
| 810180           | zkLink Nova Mainnet     |
| 5000             | Mantle                  |
| 59144            | Linea                   |
| 534352           | Scroll                  |
| 42161            | Arbitrum One            |
| 10               | OP Mainnet              |




**Please find all [ButterSwap API Reference](https://bs-router-v3.chainservice.io/docs#/) here.**