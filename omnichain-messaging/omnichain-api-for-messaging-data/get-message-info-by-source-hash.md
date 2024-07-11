# GET Message Info By Source Hash

## GET /api/queryCrossInfoBySourceHash

#### Complete Query Example

[https://bn-api.chainservice.io/api/queryCrossInfoBySourceHash?txHash=0xdd15df0239d4b58cf419e2e4243555fe4d862fa4caf154086222dadd3d751013](https://bn-api.chainservice.io/api/queryCrossInfoBySourceHash?txHash=0xdd15df0239d4b58cf419e2e4243555fe4d862fa4caf154086222dadd3d751013)

#### Request Params

| Name      | Location | Type   | Required | Description                         |
| --------- | -------- | ------ | -------- | ----------------------------------- |
| txHash   | query    | string | yes       | Source chain transaction hash.   |

#### Responses

| HTTP Status Code | Meaning                                                 | Description | Data schema |
| ---------------- | ------------------------------------------------------- | ----------- | ----------- |
| 200              | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | Success     | Inline      |

#### Responses Data

| Name   | Type  | Description                |
| ------ | ----- | -------------------------- |
| list | Array | Result cross info list. |

#### Responses Params

| Name                | Type   | Description                               |
| ------------------- | ------ | ----------------------------------------- |
| sourceInfo          | object | Source chain info.                     |
| - address       | String | Source address.                           |
| - hash          | String | Source transfer hash.                     |
| - block        | BigInteger | Source chain block height.                  |
| - timestamp     | String | Transfer timestamp                         |
| - chainInfo     | Object | Source chain info.                            |
| -- chainId           | String | Chain id.                               |
| -- chainName         | String | Chain name.                             |
| -- scanUrl           | String | Scan url.                                 |
| -- chainImg          | String | Chain icon url.                          |
| -- chainName         | String | Chain name.                               |
| relayInfo          | object | Relay chain info.                     |
| - address       | String | Source address.                           |
| - hash          | String | Source transfer hash.                     |
| - block        | BigInteger | Source chain block height.                  |
| - timestamp     | String | Transfer timestamp                         |
| - chainInfo     | Object | Source chain info.                            |
| -- chainId           | String | Chain id.                               |
| -- chainName         | String | Chain name.                             |
| -- scanUrl           | String | Scan url.                                 |
| -- chainImg          | String | Chain icon url.                          |
| -- chainName         | String | Chain name.                               |
| destinationInfo          | object | Destination chain info.                     |
| - address       | String | Source address.                           |
| - hash          | String | Source transfer hash.                     |
| - block        | BigInteger | Source chain block height.                  |
| - timestamp     | String | Transfer timestamp                         |
| - chainInfo     | Object | Source chain info.                            |
| -- chainId           | String | Chain id.                               |
| -- chainName         | String | Chain name.                             |
| -- scanUrl           | String | Scan url.                                 |
| -- chainImg          | String | Chain icon url.                          |
| -- chainName         | String | Chain name.                               |
| state               | Integer | Cross transfer state, 0: crossing 1 completed 2 relaying 3 relay completed      |

> Response Examples

> 200 Response

```json
{
  "code": 200,
  "message": "success",
  "data": {
    "list": [
      {
        "sourceInfo": {
          "address": "0x14a5b11be1f996a2c662f8968d017328b4b80c3a",
          "chainInfo": {
            "id": 5,
            "chainId": "137",
            "chainName": "Polygon",
            "scanUrl": "https://polygonscan.com/",
            "chainImg": "https://get.celer.app/cbridge-icons/chain-icon/Polygon.png",
            "mosContract": "0xfeb2b97e4efce787c08086dc16ab69e063911380",
            "color": null
          },
          "contract": "0xbb21e441fb738f54e6ec244e435475096e179d66",
          "block": 59127917,
          "hash": "0xdd15df0239d4b58cf419e2e4243555fe4d862fa4caf154086222dadd3d751013",
          "timestamp": "2024-07-09T00:01:28.000+00:00"
        },
        "destinationInfo": {
          "address": "0xa97505a93bf036f87ff398d851c06946b6ffd849",
          "chainInfo": {
            "id": 1,
            "chainId": "22776",
            "chainName": "MAP Protocol",
            "scanUrl": "https://mapscan.io/",
            "chainImg": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png",
            "mosContract": "0xfeb2b97e4efce787c08086dc16ab69e063911380",
            "color": null
          },
          "contract": "0xfeb2b97e4efce787c08086dc16ab69e063911380",
          "block": 12663543,
          "hash": "0x8e48df42c3ae18f834da59867048d313c167a3149bac9bfa62c04b78d1df36d7",
          "timestamp": "2024-07-09T00:03:08.000+00:00"
        },
        "relyerInfo": {
          "address": "0xa97505a93bf036f87ff398d851c06946b6ffd849",
          "chainInfo": {
            "id": 1,
            "chainId": "22776",
            "chainName": "MAP Protocol",
            "scanUrl": "https://mapscan.io/",
            "chainImg": "https://cdn.befiwalletdao.com/image/icon_local_map_checked_3gfyyv.png",
            "mosContract": "0xfeb2b97e4efce787c08086dc16ab69e063911380",
            "color": null
          },
          "contract": "0xfeb2b97e4efce787c08086dc16ab69e063911380",
          "block": 12663543,
          "hash": "0x8e48df42c3ae18f834da59867048d313c167a3149bac9bfa62c04b78d1df36d7",
          "timestamp": "2024-07-09T00:03:08.000+00:00"
        },
        "state": 1
      }
    ]
  }
}
```
