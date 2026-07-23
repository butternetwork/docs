# 🟢 Integration Guide

Butter API for Analytics provides dashboard statistics for Butter Swap activity.

## Base URL

```text
https://butterapi.chainservice.io
```

## API Interface Overview

| Interface | Description |
| --------- | ----------- |
| [`GET /api/statistics/dashboard`](get-dashboard-by-unit.md) | Query dashboard analytics by time range. |

## Authentication

Analytics endpoints require signed requests.

Each request must include these headers:

| Header | Value | Description |
| ------ | ----- | ----------- |
| `BS-ACCESS-KEY` | `<your-api-key>` | API key issued by Butter Network. |
| `BS-ACCESS-SIGN` | `<signature>` | Base64 HMAC-SHA256 signature. |
| `BS-ACCESS-TIMESTAMP` | `<timestamp>` | ISO 8601 UTC timestamp, for example `2026-07-23T08:00:00.000Z`. It must be within 30 seconds of server time. |
| `BS-ACCESS-PASSPHRASE` | `<your-passphrase>` | Passphrase paired with the API key. |

Signature formula:

```text
BS-ACCESS-SIGN = Base64(HMAC-SHA256(secretKey, timestamp + method + requestPath + body))
```

| Part | Description |
| ---- | ----------- |
| `timestamp` | Same value as `BS-ACCESS-TIMESTAMP`. |
| `method` | HTTP method in uppercase, such as `GET`. |
| `requestPath` | Path plus query string, such as `/api/statistics/dashboard?unit=30d&start=1784772000000`. |
| `body` | Raw request body. GET requests use an empty string. |

> Query parameters are part of `requestPath`, not `body`.

## Signing Example

```typescript
import { createHmac } from 'crypto';

const method = 'GET';
const requestPath =
  '/api/statistics/dashboard?unit=30d&start=1784772000000';
const timestamp = new Date().toISOString();
const body = '';

const sign = createHmac('sha256', process.env.BS_SECRET_KEY!)
  .update(`${timestamp}${method}${requestPath}${body}`)
  .digest('base64');

const res = await fetch(`${BASE_URL}${requestPath}`, {
  headers: {
    'BS-ACCESS-KEY': process.env.BS_ACCESS_KEY!,
    'BS-ACCESS-SIGN': sign,
    'BS-ACCESS-TIMESTAMP': timestamp,
    'BS-ACCESS-PASSPHRASE': process.env.BS_ACCESS_PASSPHRASE!,
  },
});

const bodyJson = await res.json();
if (!res.ok || bodyJson.errno !== 0) {
  throw new Error(`Request failed (${res.status}) errno=${bodyJson.errno} ${bodyJson.message}`);
}
```

For endpoint parameters and response fields, see [GET Dashboard By Unit](get-dashboard-by-unit.md).

## Error Response

```json
{
  "errno": 50103,
  "message": "Invalid signature"
}
```

| Code | Description |
| ---- | ----------- |
| `50100` | Missing signature headers. |
| `50101` | Invalid API key. |
| `50102` | Timestamp is invalid or outside the allowed time window. |
| `50103` | Invalid signature. |
| `50104` | Invalid passphrase. |
| `50105` | API key is disabled. |
| `50106` | API key is expired. |
| `50107` | Rate limit exceeded. |
