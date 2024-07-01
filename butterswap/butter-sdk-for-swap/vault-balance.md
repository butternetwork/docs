# Vault Balance

On each connected blockchain, Butter has a 'Vault' that holds certain amount of token assets that is available to bridge/swap

### Return Type[​](https://docs.butternetwork.io/SDK/vault#return-type) <a href="#return-type" id="return-type"></a>

```javascript
interface VaultBalance {
  token: BaseCurrency; // token in vault
  balance: string; // amount of token in vault on target chain
  isMintable: boolean; // if token is mintable by Butter
}
```

### Vault Balance[​](https://docs.butternetwork.io/SDK/vault#vault-balance-1) <a href="#vault-balance-1" id="vault-balance-1"></a>

To get the vault balance, use the following provided method:

```javascript
const mapRpcProvider = {
    url: 'https://poc2-rpc.maplabs.io',
    chainId: 22776,
}

async function getVaultBalance(
  fromChainId: string, // from chain id
  fromToken: BaseCurrency, // from token
  toChainId: string, // to chain id
  mapRpcProvider: ButterJsonRpcProvider // map relay chain rpc provider
): Promise<VaultBalance>;
```

**Example: get how many USDC tokens in our vault is available to transfer from Ethereum to BSC**[**​**](https://docs.butternetwork.io/SDK/vault#example-get-how-many-usdc-tokens-in-our-vault-is-available-to-transfer-from-ethereum-to-bsc)

```javascript
  const balance: VaultBalance = await getVaultBalance(
    ChainId.ETH_MAINNET,
    ETH_MAINNET_USDC,
    ChainId.BSC_MAINNET,
    mapProvider
  );
  console.log('vault balance', balance);
```

**Output:**[**​**](https://docs.butternetwork.io/SDK/vault#output)

```json
vault balance {
  feeToken: Token {
    address: '0x8AC76a51cc950d9822D68b83fE1Ad97B32Cd580d',
    chainId: '56',
    decimals: 18,
    symbol: 'USDC',
    name: 'Binance-Peg USD Coin',
    logo: 'https://files.maplabs.io/bridge/usdc.png',
    isNative: false,
    isToken: true
  },
  balance: '100000000000000000000',
  isMintable: false
}
```
