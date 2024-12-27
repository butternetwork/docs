# Install Butter SDK

###### Integrate Butter SDK to your dApp/Swap UI

## Installation

To get started, install the latest version of Butter SDK

### yarn

```bash
yarn add @butternetwork/sdk
```

### npm

```bash
npm i @butternetwork/sdk
```

Check out our complete examples in the SDK repository, and feel free to file an issue if you encounter any problems.

## Quick Start

### Setup SDK

#### Config rpcs

```typescript
import { butterConfig, ChainType } from "@butternetwork/sdk";

butterConfig.setOptions({
  providers: [],
  rpcs: {
    [ChainType.NEAR]: [],
    [ChainType.SOLANA]: [],
    [ChainType.TRON]: {
      urls: ["https://api.trongrid.io"],
      headers: {
        "TRON-PRO-API-KEY": "your-api-key",
      },
    },
    [ChainType.TON]: [],
  },
});
```

#### Config EVM

```typescript
import { useWalletClient } from "wagmi";

const { data: signer } = useWalletClient();

useEffect(() => {
  butterConfig.setOptions({
    providers: [
      createEvmProvider({
        walletClient: signer as any,
      }),
    ],
  });
}, [signer]);
```

#### Config Near

```typescript
import { setupWalletSelector } from "@near-wallet-selector/core";

const selector = await setupWalletSelector({
  network: nearConfig.networkId as NetworkId,
  debug: true,
  modules: [
    // ...modules
  ],
});

useEffect(() => {
  selector.wallet().then((wallet) => {
    butterConfig.setOptions({
      providers: [
        createNearProvider({
          getWallet: async () => wallet as any,
        }),
      ],
    });
  });
}, [selector]);
```

#### Config Solana

```typescript
import { useWallet } from "@solana/wallet-adapter-react";

const { wallet } = useWallet();

useEffect(() => {
  butterConfig.setOptions({
    providers: [
      createSolanaProvider({
        getWalletAdapter: async () => wallet?.adapter as any,
      }),
    ],
  });
}, [wallet]);
```

#### Config Tron

```typescript
import { useWallet as useTronWallet } from "@tronweb3/tronwallet-adapter-react-hooks";

const { wallet: tronWallet } = useTronWallet();

useEffect(() => {
  butterConfig.setOptions({
    providers: [
      createTronProvider({
        getAdapter: async () => tronWallet?.adapter as any,
      }),
    ],
  });
}, [tronWallet]);
```

#### Config Ton

```typescript
import { useTonConnectUI } from "@tonconnect/ui-react";

const [tonConnectUI, setOptions] = useTonConnectUI();
useEffect(() => {
  if (!tonConnectUI) {
    return;
  }
  butterConfig.setOptions({
    providers: [
      createTonProvider({
        getConnector: async () => tonConnectUI as any,
      }),
    ],
  });
}, [tonConnectUI]);
```

### Usage

#### Request Routes

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
  abortSignal: signal,
});
```

#### Request Txn

```typescript
import { generateSwapData } from "@butternetwork/sdk";

const txn = await generateSwapData({
  hash: "0x123......", // hash from getRoutes
  slippage: "100",
  receiver: "0x123123...",
  from: "0x123123...",
});
```

#### Execute Route

```typescript
import { executeRoute } from "@butternetwork/sdk";
// Near
const hash = await executeRoute(txn);
// Other Chain
// const hash = await executeRoute(txn[0]);
```
