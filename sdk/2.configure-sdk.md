# Configure SDK

get started and set up Butter SDK .

### Setup SDK

To get started, you need to set up configuration for the Butter SDK.
This configuration contains the shared settings and data required for the proper functioning of other SDK features that
developers will use. Additionally, the configuration can be updated later as needed.

#### Config rpcs

```typescript
import { butterConfig, ChainType } from "@butternetwork/sdk";

butterConfig.setOptions({
  providers: [],
  rpcs: {
    [ChainType.NEAR]: ["https://near-example.node.com/"],
    [ChainType.SOLANA]: ["https://solana-example.node.com/"],
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

## Update SDK Configuration

To update the configuration, you need to import the global configuration object and use its methods.

```typescript
import { butterConfig } from "@butternetwork/sdk";

butterConfig.setOptions({
  // ...options
});
```

## Configure SDK Providers

The SDK offers **EVM** , **Solana** , **TRON** , **TON** and **NEAR** providers, all with similar configuration options
respective to their ecosystems.

#### Config EVM

The EVM provider execution logic is built based on the Viem library, using some of its types and terminology.

Options available for configuring the EVM provider:

- `walletClient`: a signer object that implements the `WalletClient` interface.

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

The Near provider execution logic is built based on the `@near-wallet-selector/core` library,
using some of its types and terminology.

Options available for configuring the Near provider:

- `getWallet` : a function that returns a wallet object.

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

The Solana provider execution logic is built based on the `@solana/web3.js` and `@solana/wallet-adapter-base` libraries,
using some of its types and terminology.

Options available for configuring the SOLANA provider:

- `getWalletAdapter`: a function that returns a wallet adapter object.

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

The Tron provider execution logic is built based on the `@tronweb3/tronwallet-adapters
` library,
using some of its types and terminology.

Options available for configuring the SOLANA provider:

- `getAdapter`: a function that returns a wallet adapter object.

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

The Ton provider execution logic is built based on the `@tonconnect/ui-react` library, using some of its types and
terminology.

Options available for configuring the TON provider:

- `getConnector`: a function that returns a `TonConnectUI` object.

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
