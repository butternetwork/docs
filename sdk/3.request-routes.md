# Request Routes

To executing any swap or bridging, you need to request the best route from our smart routing API.

The Butter SDK provides functionality to request routes and quotes, as well as to execute them.
This guide will walk you through the process of making a request using `getRoutes` function.

## How to

Here is a example to request a route to bridge 1000 MAPO from Map protocol to Binance Smart Chain.

```typescript
import { getRoutes } from "@butternetwork/sdk";

const routes = await getRoutes({
  fromChainId: "22776",
  toChainId: "56",
  amount: "1000",
  tokenInAddress: "0x0000000000000000000000000000000000000000",
  tokenOutAddress: "0x55d398326f99059ff775485246999027b3197955",
  type: "exactIn",
  slippage: "200",
  entrance: "Butter+",
});
```

When you request routes, you receive an array of route objects containing the essential information to determine which
route to take for a swap or bridging transfer. At this stage, transaction data is not included and must be requested
separately. Read more _Execute Routes/Quotes_.

## Routes request parameters

Below are the parameters for the RoutesRequest interface along with their descriptions:

`fromChainId` **(string, required)**

The Chain Id of the source chain.

`toChainId` **(string, required)**
The Chain Id of the destination chain.

`amount` **(string, required)**
The amount of tokens to be swapped or bridged.

`tokenInAddress` **(string, required)**
The address of the token to be swapped or bridged.

`tokenOutAddress` **(string, required)**
The address of the token to be received.

`type` **(string, required)**
The type of swap or bridging. Possible values are `exactIn` and `exactOut`.

`slippage` **(string, required)**
The slippage tolerance percentage.

`entrance` **(string, required)**
The entrance of the swap or bridging. Default value is `Butter+`.

`abortSignal` **(AbortSignal, optional)**
The signal to abort the request.

## Response

The response is an array of route objects. Each route object contains the following fields:

```typescript
export interface Route {
  // The difference between current route and the best route
  diff: string;
  bridgeFee: {
    amount: string;
    symbol: string;
  };
  // 0 for exactIn / 1 for exactOut
  tradeType: number;
  gasFee: {
    amount: string;
    symbol: string;
  };
  gasEstimated: string;
  // hash for reqeust route tx
  hash: string;
  srcChain: ChainInRoute;
  bridgeChain: ChainInRoute;
  dstChain: ChainInRoute;
  minAmountOut: {
    amount: string;
    symbol: string;
  };
  timeEstimated: number;
}
```
