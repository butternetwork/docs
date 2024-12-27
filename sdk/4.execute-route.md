# Execute Routes

We allow you to execute any on-chain or cross-chain swap and bridging transfer and a combination of both.

## Get Route Transactions

Before execute a route, we need to request Rotue Transactions by `generateSwapData`:

```typescript
const txn = await generateSwapData({
  hash: "0x123......", // hash from getRoutes
  slippage: "100",
  receiver: "0x123123...",
  from: "0x123123...",
});
```

Return data is

```typescript
export interface RouteTxData {
  to: string;
  data: string;
  value: string;
  method?: string;
  chainId: string;
  args: {
    type: string;
    value: any;
  }[];
}
```

## Execute Route

Then we can execure the route;

```typescript
import { executeRoute } from "@butternetwork/sdk";
// Near
const hash = await executeRoute(txn);
// Other Chain
// const hash = await executeRoute(txn[0]);
```

- Parameters
  - `route`: `RouteTxData` | `RouteTxData[]` the route transaction to be execure.
- Return
  - `Promise<string>`: Resolves when execution is done or halted and rejects when it is failed.
