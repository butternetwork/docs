# Request and Response

the detail of all the request\&response types needed while using the SDK.

### Request Types[​](https://docs.butternetwork.io/SDK/types#request-types) <a href="#request-types" id="request-types"></a>

All the request data structure needed to interact with the SDK

**`BridgeRequestParam`**[**​**](https://docs.butternetwork.io/SDK/types#bridgerequestparam)

The request parameter data structure for bridge action.

```javascript
export type BridgeRequestParam = {
  fromAddress: string;
  fromToken: BaseCurrency;
  fromChainId: string;
  toChainId: string;
  toAddress: string;
  amount: string; // in minimal uint
  options: ButterTransactionOption;
};
```

**`SwapRequestParam`**[**​**](https://docs.butternetwork.io/SDK/types#swaprequestparam)

The request parameter data structure for swap action.

```javascript
export type SwapRequestParam = {
  fromAddress: string;
  fromToken: BaseCurrency;
  toAddress: string;
  toToken: BaseCurrency;
  amountIn: string; // in minimal uint
  swapRouteStr: string; // cross-chain swap route, in string format.
  slippage?: number; // in bps, e.g. 100 = 1%
  options: ButterTransactionOption;
};
```

**`PaymentRequestParam`**[**​**](https://docs.butternetwork.io/SDK/types#paymentrequestparam)

The request parameter data structure for omnichain payment.

```javascript
export type PaymentRequestParam = {
    fromAddress: string;
    paidToken: BaseCurrency; // token user paid
    paidAmount: string; // in minimal uint
    toAddress: string; // seller's receiving address 
    requiredToken: BaseCurrency; // required token by seller
    requiredAmount: string; // required amount
    swapRouteStr: string;
    options: ButterTransactionOption;
};
```

**`ButterTransactionOption`**[**​**](https://docs.butternetwork.io/SDK/types#buttertransactionoption)

options needed to do a cross-chain swap

```javascript
export type ButterTransactionOption = {
  signerOrProvider?: Signer | Provider | Eth; // When source chain is EVM provide Ethers.js Signer/Provider or Web3.js Eth info
  nearProvider?: NearProviderType; // mandatory when src chain is near
  gas?: string;
  gasPrice?: string;
};
```

`signerOrProvider`: Butter supports both _ethers.js_ and _web3.js_. If you are using ethers.js, provider the [`Signer`](https://docs.ethers.org/v5/api/signer/) object. If your application choose to use web3.js, please provide [`Eth`](https://web3js.readthedocs.io/en/v1.2.11/web3-eth.html) object in order to send a transaction.

`nearProvider`: Whenever send a transaction from Near Protocol, you have to provide [`NearNetworkConfig`](https://near.github.io/near-api-js/interfaces/connect.ConnectConfig) with keystore provided or [`WalletConnection`](https://near.github.io/near-api-js/classes/walletAccount.WalletConnection/) object

```
export type NearProviderType = NearNetworkConfig | WalletConnection;
```

### Response Types[​](https://docs.butternetwork.io/SDK/types#response-types) <a href="#response-types" id="response-types"></a>

All the response data structure when interacting the SDK

**Vault**[**​**](https://docs.butternetwork.io/SDK/types#vault)

**`VaultBalance`**[**​**](https://docs.butternetwork.io/SDK/types#vaultbalance)

```javascript
interface VaultBalance {
  token: BaseCurrency; // token in vault
  balance: string; // amount of token in vault on target chain
  isMintable: boolean; // if token is mintable by Butter
}
```

**Fee Related**[**​**](https://docs.butternetwork.io/SDK/types#fee-related)

**`ButterFee`**[**​**](https://docs.butternetwork.io/SDK/types#butterfee)

```javascript
export interface ButterFee {
  feeToken: BaseCurrency; // the token that to be charged
  amount: string; // in minimal unit
  feeRate: ButterFeeRate; // fee rate inforamtion
  feeDistribution?: ButterFeeDistribution; // fee distribution inforamtion
}
```

**`ButterFeeRate`**[**​**](https://docs.butternetwork.io/SDK/types#butterfeerate)

Fee rate

```javascript
export type ButterFeeRate = {
  lowest: string; // lowest AMOUNT of fee token to be charged
  highest: string; // highest AMOUNT of fee token to be charged
  rate: string; // fee rate in bps
};
```

**`ButterFeeDistribution`**[**​**](https://docs.butternetwork.io/SDK/types#butterfeedistribution)

Fee distribution

```javascript
export type ButterFeeDistribution = {
    protocol: string; // protocol rate in bps
    relayer: string; // relayer rate in bps, prepaid destination gas fee
    lp: string; // lp fee rate in bps
};
```

**Best Route**[**​**](https://docs.butternetwork.io/SDK/types#best-route)

**`RouterResponse`**[**​**](https://docs.butternetwork.io/SDK/types#routerresponse)

```javascript
export type RouteResponse = {
  data?: string; // json string
  msg: string;
  status: number;
};
```

**Transaction Response**[**​**](https://docs.butternetwork.io/SDK/types#transaction-response)

**`ButterTransactionResponse`**[**​**](https://docs.butternetwork.io/SDK/types#buttertransactionresponse)

Response datatype when invoke cross-chain transaction

```javascript
export interface ButterTransactionResponse {
  hash: string;
  wait?: () => Promise<ButterTransactionReceipt>;
  promiReceipt?: PromiEvent<Web3TransactionReceipt>; // only when use web3.js
}
```

[`promiReceipt`](https://web3js.readthedocs.io/en/v1.2.11/callbacks-promises-events.html) is only available when you are using web.js.

**`ButterTransactionReceipt`**[**​**](https://docs.butternetwork.io/SDK/types#buttertransactionreceipt)

Transaction receipt

```javascript
export interface ButterTransactionReceipt {
  to: string;
  from: string;
  gasUsed: string;
  transactionHash: string;
  logs: Array<Log> | string[]; // string[] for Near logs
  blockHash?: string;
  blockNumber?: number;
  success?: boolean; // 1 success, 0 failed
}
```
