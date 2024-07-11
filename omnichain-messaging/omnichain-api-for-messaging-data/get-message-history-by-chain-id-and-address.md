# GET Message History By Chain Id And Address

## GET /api/queryHistoryByChainIdAddress

#### Complete Query Example

[https://bn-api.chainservice.io/api/queryHistoryByChainIdAddress?chainId=137&address=0x14a5b11be1f996a2c662f8968d017328b4b80c3a&page=1&size=10](https://bn-api.chainservice.io/api/queryHistoryByChainIdAddress?chainId=137&address=0x14a5b11be1f996a2c662f8968d017328b4b80c3a&page=1&size=10)

#### Request Params

| Name      | Location | Type   | Required | Description                         |
| --------- | -------- | ------ | -------- | ----------------------------------- |
| page      | query    | integer | no      | Integer of page number, default is 1.   |
| size      | query    | integer | no      | Integer of size number, default is 10.  |
| chainId   | query    | string | yes      | Source Chain id.   |
| address   | query    | string | yes      | Source Address. |

#### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

#### Responses Data

| Name   | Type  | Description                |
| ------ | ----- | -------------------------- |
| list   | Array | Result cross info history list. |
| total   | Integer | Total number of cross history. |

#### Responses Params

| Name                | Type   | Description                               |
| ------------------- | ------ | ----------------------------------------- |
| id                  | Integer | Cross id.                           |
| sourceAddress       | String | Source address.                           |
| sourceHash          | String | Source transfer hash.                     |
| sourceHeight        | BigInteger | Source chain block height.                  |
| sourceTimestamp     | String | Transfer timestamp                         |
| sourceChainInfo     | Object | Source chain info.                            |
| - chainId           | String | Chain id.                               |
| - chainName         | String | Chain name.                             |
| - scanUrl           | String | Scan url.                                 |
| - chainImg          | String | Chain icon url.                          |
| relayHash          | String | Relay transfer hash.                     |
| relayHeight        | BigInteger | Relay chain block height.                  |
| relayChainInfo     | Object | Relay chain info.                            |
| - chainId           | String | Chain id.                               |
| - chainName         | String | Chain name.                             |
| - scanUrl           | String | Scan url.                                 |
| - chainImg          | String | Chain icon url.                          |
| destinationHash     | String | Destination chain transfer hash.                     |
| destinationHeight   | BigInteger | Destination chain block height.    |
| destinationChainInfo| Object | Destination chain info.                            |
| - chainId           | String | Chain id.                               |
| - chainName         | String | Chain name.                             |
| - scanUrl           | String | Scan url.                                 |
| - chainImg          | String | Chain icon url.                          |
| state               | Integer | Cross transfer state, 0: crossing 1 completed 2 relaying 3 relay completed                           |
> Response Examples

> 200 Response

```json
{
  "code": 200,
  "message": "success",
  "data": {
    "list": [
      {
        "id": 322111,
        "sourceAddress": "0x14a5b11be1f996a2c662f8968d017328b4b80c3a",
        "sourceHash": "0xdd15df0239d4b58cf419e2e4243555fe4d862fa4caf154086222dadd3d751013",
        "sourceHeight": 59127917,
        "sourceTimestamp": "2024-07-09T00:01:28.000+00:00",
        "sourceChainInfo": {},
        "relayHash": null,
        "relayHeight": null,
        "relayChainInfo": null,
        "destinationHash": "0x8e48df42c3ae18f834da59867048d313c167a3149bac9bfa62c04b78d1df36d7",
        "destinationHeight": 12663543,
        "destinationChainInfo": {
          "id": 1,
          "chainId": "22776",
          "chainName": "MAP Protocol",
          "scanUrl": "https://mapscan.io/",
          "chainImg": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png",
          "mosContract": "0xfeb2b97e4efce787c08086dc16ab69e063911380",
          "color": null
        },
        "state": 1
      }
    ],
    "total": 2
  }
}
```
