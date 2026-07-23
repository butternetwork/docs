---
cover: ../../.gitbook/assets/Butter API for Routing.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 👩‍💻 Butter API for Analytics

Butter API for Analytics provides developers with statistical data.

## Endpoints

* [GET /api/statistics/dashboard](get-dashboard-by-unit.md)

## Authentication

Analytics API endpoints require signed requests.

Each request must include these headers:

| Header | Description |
| ------ | ----------- |
| `BS-ACCESS-KEY` | API key issued by Butter Network. |
| `BS-ACCESS-SIGN` | Base64 HMAC-SHA256 signature. |
| `BS-ACCESS-TIMESTAMP` | ISO 8601 UTC timestamp, for example `2026-07-23T08:00:00.000Z`. |
| `BS-ACCESS-PASSPHRASE` | Passphrase paired with the API key. |

Signature payload:

```text
timestamp + method + requestPath + body
```

For GET requests, `body` is an empty string and `requestPath` must include the query string.
