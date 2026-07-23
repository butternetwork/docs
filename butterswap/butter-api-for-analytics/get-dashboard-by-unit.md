# GET Dashboard By Unit

## GET /api/statistics/dashboard

Returns analytics dashboard data for a selected time range.

#### Complete Query Example

```url
/api/statistics/dashboard?unit=30d&start=1784772000000
```

#### Authentication

This endpoint requires an API signature. See [Integration Guide](integration-guide.md#authentication).

#### Request Params

| Name | Location | Type | Required | Description |
| ---- | -------- | ---- | -------- | ----------- |
| `start` | query | string | yes | Millisecond timestamp. The API rounds it down to the start of the hour and uses it as the range end time. |
| `unit` | query | string | yes | Time range. Supported values: `24h`, `7d`, `30d`, `60d`, `liquidity`. |

#### Responses

| HTTP Status Code | Meaning | Description | Data schema |
| ---------------- | ------- | ----------- | ----------- |
| 200 | OK | Success | Inline |

#### Responses Data

| Name | Type | Description |
| ---- | ---- | ----------- |
| `summary.state.count` | Object | Summary count statistics. |
| `summary.state.volume` | Object | Summary volume statistics. |
| `items` | Array | Time-bucketed analytics items. |

#### Item Data

| Name | Type | Description |
| ---- | ---- | ----------- |
| `date` | string | Bucket date. |
| `data.time.startTime` | number | Bucket start timestamp in milliseconds. |
| `data.time.endTime` | number | Bucket end timestamp in milliseconds. |
| `data.count.complete` | number | Completed transaction count. |
| `data.count.address` | number | Address count. |
| `data.volume.complete` | number | Completed transaction volume. |
| `data.volume.swap` | number | Same-chain swap volume. |
| `data.chain.source[]` | Array | Source-chain statistics. Each item only contains `chainId`, `volume`, and `count`. |
| `data.chain.dest[]` | Array | Destination-chain statistics. Each item only contains `chainId`, `volume`, and `count`. |

> 200 Response

```json
{
  "errno": 0,
  "message": "success",
  "data": {
    "summary": {
      "state": {
        "count": {},
        "volume": {}
      }
    },
    "items": [
      {
        "date": "2026-06-23",
        "data": {
          "time": {
            "startTime": 1782144000000,
            "endTime": 1782230400000
          },
          "count": {
            "complete": 1134,
            "address": 1041
          },
          "volume": {
            "complete": 1246209016686,
            "swap": 0
          },
          "chain": {
            "source": [
              {
                "chainId": 56,
                "volume": {
                  "complete": 1000000,
                  "swap": 0
                },
                "count": {
                  "complete": 12,
                  "address": 10
                }
              }
            ],
            "dest": [
              {
                "chainId": 137,
                "volume": {
                  "complete": 900000,
                  "swap": 0
                },
                "count": {
                  "complete": 11,
                  "address": 9
                }
              }
            ]
          }
        }
      }
    ]
  }
}
```
