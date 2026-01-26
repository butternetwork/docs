# 🟢 Integration Guide

Welcome to the Butter Smart Router service! This document will guide developers on how to integrate our service into their applications to facilitate querying the best route from token1 on Chain A to token2 on Chain B and assembling transactions.

### API Interface Overview

Butter Smart Router service provides the following interfaces:

1. Query Supported Chain Info List
   * Interface: `/supportedChainInfo`
   * Description: Query the list of all supported chains by this service.
2. Find Token Information
   * Interface: `/findToken`
   * Description: Find the token information by the given address.
3. Query Best Routes
   * Interface: `/route`
   * Description: Query the best routes from token1 on Chain A to token2 on Chain B.
4. Assemble Transaction Data Based on Selected Route
   * Interface: `/swap`
   * Description: Assemble transaction data based on the selected route.
5. Query Best Routes and Assemble Transaction Data
   * Interface: `/routeAndSwap`
   * Description: Combination of querying best routes and assembling transaction data.

### Integration Steps

### 1.Query Supported Chain Info

Use the `/supportedChainInfo` interface to query the list of all supported chains by this service. You will receive a list of blockchains' information.

#### Request Url with **GET** method:

```json
https://bs-router-v3.chainservice.io/supportedChainInfo
```

#### Response:

```json
{
  "errno": 0,
  "message": "success",
  "data": [
     {
        "id": "1",
        "type": "EVM",
        "name": "Ethereum"
     },
     {
        "id": "137",
        "type": "EVM",
        "name": "Polygon"
     },
     {
        "id": "56",
        "type": "EVM",
        "name": "BSC"
     },
     {
        "id": "22776",
        "type": "EVM",
        "name": "MAP"
     },
     {
        "id": "728126428",
        "type": "EVM",
        "name": "Tron"
     },
     {
        "id": "2649",
        "type": "EVM",
        "name": "AILayer"
     },
     {
        "id": "8453",
        "type": "EVM",
        "name": "Base"
     },
     {
        "id": "59144",
        "type": "EVM",
        "name": "Linea"
     },
     {
        "id": "42161",
        "type": "EVM",
        "name": "Arbitrum"
     },
     {
        "id": "10",
        "type": "EVM",
        "name": "Optimism"
     },
     {
        "id": "8217",
        "type": "EVM",
        "name": "Kaia"
     },
     {
        "id": "196",
        "type": "EVM",
        "name": "XLayer"
     },
     {
        "id": "1360108768460801",
        "type": "Solana",
        "name": "Solana"
     },
     {
        "id": "1360095883558913",
        "type": "BTC",
        "name": "BTC"
     }
  ]
}
```

**Note**: the chain info list may change over time as new chains are added or removed from the Butter Router's support, please request this endpoint to get the latest supported chain info.


### 2. Find Token Information

Use the `/findToken` interface to find the token information by the given address. The result is a list of token information because same token address may exist on different blockchains.

E.g, find the token information by the address `0x55d398326f99059fF775485246999027B3197955`.

#### Request Url with **GET** method:

```url
https://bs-router-v3.chainservice.io/findToken?address=0x55d398326f99059fF775485246999027B3197955
```

#### Response:

```json
{
  "errno": 0,
  "message": "success",
  "data": [
    {
      "id": 56,
      "chainId": 56,
      "address": "0x55d398326f99059fF775485246999027B3197955",
      "blockchainNetwork": "56",
      "coingeckoId": "",
      "decimals": 18,
      "image": "https://files.mapprotocol.io/bridge/usdt.png",
      "name": "Tether USD",
      "rank": 0,
      "symbol": "USDT",
      "tokenSecurity": null,
      "usdprice": 0,
      "usedIniframe": 0
    }
  ]
}
```

### 3. Query Best Routes

Use the `/route` interface to query the best routes from token1 on Chain A to token2 on Chain B. These routes are sorted by **totalAmountOut** of token2 in descending order.

E.g. find the best swap route from 1 ETH on Ethereum to USDT on BSC with 1% slippage and Butter+ as the entrance.

#### Request URL with **GET** method:

```url
https://bs-router-v3.chainservice.io/route?fromChainId=1&toChainId=56&amount=1&tokenInAddress=0x0000000000000000000000000000000000000000&tokenOutAddress=0x55d398326f99059fF775485246999027B3197955&type=exactIn&slippage=100&entrance=Butter%2B
```

#### Success Response:

```json
{
  "errno": 0,
  "message": "success",
  "data": [
    {
      "diff": "0",
      "bridgeFee": {
        "amount": "0.003",
        "symbol": "WETH"
      },
      "tradeType": 0,
      "gasFee": {
        "amount": "0.001356760233135",
        "symbol": "ETH"
      },
      "gasEstimated": "135000",
      "timeEstimated": 1080,
      "hash": "0x4cae26ffe044267ffa39f5885259c104abd67bec07a1452169dbc4fff5d0319c",
      "timestamp": 1713521277918,
      "srcChain": {
        "chainId": "1",
       ...
      },
      "bridgeChain": {
        "chainId": "22776",
        ...
        "bridge": "Butter"
      },
      "dstChain": {
        "chainId": "56",
        ...
        "totalAmountIn": "3099.354635",
        "totalAmountOut": "3097.435380206588564864",
       ...
      }
    },
    {
      "diff": "0.01031423702686832168",
      "bridgeFee": {
        "amount": "8.0",
        "symbol": "USDT"
      },
      "tradeType": 0,
      "gasFee": {
        "amount": "0.001356760233135",
        "symbol": "ETH"
      },
      "gasEstimated": "135000",
      "timeEstimated": 1080,
      "hash": "0xc13ebfadb392251d093cd8efdbca23ed1e886211c72ef239b04d3496c165a61a",
      "timestamp": 1713521277918,
      "srcChain": {
        "chainId": "1",
       ...
      },
      "bridgeChain": {
        "chainId": "22776",
       ...
        "bridge": "Butter"
      },
      "dstChain": {
        "chainId": "56",
        ...
        "totalAmountIn": "3097.127755",
        "totalAmountOut": "3097.127755",
       ...
    }
  ]
}
```

#### Failure Response:

```json
{
  "errno": 2003,
  "message": "No Route Found"
}
```

### 4. Assemble Transaction Data Based on Selected Route

Use the `/swap` interface to assemble transaction data based on the selected route hash from the `/route` response.

E.g. assemble the transaction data based on the route hash `0x4cae26ffe044267ffa39f5885259c104abd67bec07a1452169dbc4fff5d0319c` with the slippage of 1% and the sender address `0x2D4C407BBe49438ED859fe965b140dcF1aaB71a9` and the receiver address `0x2D4C407BBe49438ED859fe965b140dcF1aaB71a9`.

#### Request URL with **GET** method:

```
https://bs-router-v3.chainservice.io/swap?hash=0x4cae26ffe044267ffa39f5885259c104abd67bec07a1452169dbc4fff5d0319c&slippage=100&from=0x2D4C407BBe49438ED859fe965b140dcF1aaB71a9&receiver=0x2D4C407BBe49438ED859fe965b140dcF1aaB71a9
```

#### Success Response:

```json
{
  "errno": 0,
  "message": "success",
  "data": [
    {
      "to": "0xbB21e441fb738F54e6eC244e435475096E179d66",
      "data": "0x480a341100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000014000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc20000000000000000000000002d4c407bbe49438ed859fe965b140dcf1aab71a9000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc20000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000000000000000000e00000000000000000000000000000000000000000000000000000000000000004d0e30db00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000007e000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000038000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000a00000000000000000000000000000000000000000000000000000000000000014bb21e441fb738f54e6ec244e435475096e179d660000000000000000000000000000000000000000000000000000000000000000000000000000000000000700000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000006e0000000000000000000000000000000000000000000000000000000000000068000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002162b2aee2dd657fb131b28cc34dee6797b66f000000000000000000000000002162b2aee2dd657fb131b28cc34dee6797b66f0000000000000000000000002d4c407bbe49438ed859fe965b140dcf1aab71a900000000000000000000000055d398326f99059ff775485246999027b31979550000000000000000000000000000000000000000000000a5ed65c00189cca20000000000000000000000000000000000000000000000000000000000000000e00000000000000000000000000000000000000000000000000000000000000544efa0646500000000000000000000000000000000000000000000000000000000000000200000000000000000000000002170ed0880ac9a755fd29b2688956bd959f933f800000000000000000000000055d398326f99059ff775485246999027b319795500000000000000000000000000000000000000000000000000000000000000000000000000000000000000002d4c407bbe49438ed859fe965b140dcf1aab71a90000000000000000000000000000000000000000000000a5ed65c00189cca20000000000000000000000000000000000000000000000000000000000000000c00000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000040000000000000000000000001111111254eeb25477b68fb85ed929f73a9605820000000000000000000000001111111254eeb25477b68fb85ed929f73a9605820000000000000000000000000000000000000000000000000dd60e37b910800000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000000000000000000000000000000000000000036000000000000000000000000000000000000000000000000000000000000000c4000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000002e812aa3caf000000000000000000000000e37e799d5077682fa0a244d46e5649f71457bd090000000000000000000000002170ed0880ac9a755fd29b2688956bd959f933f800000000000000000000000055d398326f99059ff775485246999027b3197955000000000000000000000000e37e799d5077682fa0a244d46e5649f71457bd09000000000000000000000000002162b2aee2dd657fb131b28cc34dee6797b66f0000000000000000000000000000000000000000000000000dd60e37b910800000000000000000000000000000000000000000000000009f3923940bd1ceb54f0000000000000000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000000000000000000000000014000000000000000000000000000000000000000000000000000000000000001600000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000015800000000000000000000000000000000000000000000013a00010c0000c200a007e5c0d200000000000000000000000000000000000000000000000000009e00004f02a000000000000000000000000000000000000000000000000048b16c7d7669cdecee63c1e501d0e226f674bbf064f54ab47f42473ff80db98cba2170ed0880ac9a755fd29b2688956bd959f933f802a000000000000000000000000000000000000000000000009f3923940bd1ceb54fee63c1e500172fcd41e0913e95784454622d1c3724f546f849bb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c00a0f2fa6b6655d398326f99059ff775485246999027b31979550000000000000000000000000000000000000000000000a79a764afef7cc1d2b00000000000000004553f3402a35c68080a06c4eca2755d398326f99059ff775485246999027b31979551111111254eeb25477b68fb85ed929f73a960582000000000000000052fd304d0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
      "value": "0x0de0b6b3a7640000",
      "chainId": "1"
    }
  ]
}
```

#### Failure Response:

```json
{
  "errno": 2004,
  "message": "Insufficient Liquidity"
}
```

#### Note:

1. the route data will be expired after 5 minutes, so it is recommended to request the `/route` interface periodically to get the best route and then assemble the transaction data.
2. if the source token is an ERC20 token, the user needs to approve the router contract to spend the token before calling the swap function. The router contract address is the **to** field in the swap response.

### 5. Query Best Routes and Assemble Transaction Data

You can also use the `/routeAndSwap` interface to combine querying the best routes and assembling transaction data in one step.

E.g. find the best swap route from 1 ETH on Ethereum to USDT on BSC with 1% slippage and Butter+ as the entrance, and assemble the transaction data for each route. You need to specify the sender address and the receiver address.

#### Request URL with **GET** method:

```url
https://bs-router-v3.chainservice.io/routeAndSwap?fromChainId=1&toChainId=56&amount=1&tokenInAddress=0x0000000000000000000000000000000000000000&tokenOutAddress=0x55d398326f99059fF775485246999027B3197955&type=exactIn&slippage=100&entrance=Butter%2B&from=0x2D4C407BBe49438ED859fe965b140dcF1aaB71a9&receiver=0x2D4C407BBe49438ED859fe965b140dcF1aaB71a9
```

#### Response:

```json
{
  "errno": 0,
  "message": "success",
  "data": [
    {
      "route": {
        "diff": "0",
        "bridgeFee": {
          "amount": "8.0",
          "symbol": "USDT"
        },
       ...
        "hash": "0x536ca56a24c05fb5820826fb5e1fd2052fa393d1423cd588f37e6dcf333f3af9",
        "timestamp": 1713529145811,
        "srcChain": {
          "chainId": "1",
          ...
        },
        "bridgeChain": {
          "chainId": "22776",
          ...
          "bridge": "Butter"
        },
        "dstChain": {
          "chainId": "56",
          ...
          "totalAmountIn": "3103.310596",
          "totalAmountOut": "3103.310596",
          ...
        },
        ...
      },
      "txParam": {
        "errno": 0,
        "message": "success",
        "data": [
          {
            "to": "0xbB21e441fb738F54e6eC244e435475096E179d66",
            "data": "0x480a341100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000004a000000000000000000000000000000000000000000000000000000000000005a000000000000000000000000000000000000000000000000000000000000003e000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002162b2aee2dd657fb131b28cc34dee6797b66f000000000000000000000000002162b2aee2dd657fb131b28cc34dee6797b66f0000000000000000000000002d4c407bbe49438ed859fe965b140dcf1aab71a9000000000000000000000000dac17f958d2ee523a2206206994597c13d831ec700000000000000000000000000000000000000000000000000000000b798157300000000000000000000000000000000000000000000000000000000000000e000000000000000000000000000000000000000000000000000000000000002a4efa0646500000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000dac17f958d2ee523a2206206994597c13d831ec700000000000000000000000000000000000000000000000000000000000000000000000000000000000000002d4c407bbe49438ed859fe965b140dcf1aab71a900000000000000000000000000000000000000000000000000000000b798157300000000000000000000000000000000000000000000000000000000000000c00000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001111111254eeb25477b68fb85ed929f73a9605820000000000000000000000001111111254eeb25477b68fb85ed929f73a9605820000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000a8e449022e0000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000000000000b02d172a00000000000000000000000000000000000000000000000000000000000000600000000000000000000000000000000000000000000000000000000000000001400000000000000000000000c7bbec68d12a0d1830360f8ec58fa599ba1b0e9b52fd304d0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000e000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000038000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000a000000000000000000000000000000000000000000000000000000000000000142d4c407bbe49438ed859fe965b140dcf1aab71a900000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
            "value": "0x0de0b6b3a7640000",
            "chainId": "1"
          }
        ]
      }
    },
    {
      "route": {
        "diff": "0.06040927566755252048",
        "bridgeFee": {
          "amount": "8.0",
          "symbol": "USDC"
        },
        ...
        "hash": "0x26cc63276da4db7e5a361e27db242b9e402d2085b9eff0760507c78f181bc4d4",
        "timestamp": 1713529145812,
        "srcChain": {
          "chainId": "1",
          ...
        },
        "bridgeChain": {
          "chainId": "22776",
          ...
          "bridge": "Butter"
        },
        "dstChain": {
          "chainId": "56",
         ...
          "totalAmountIn": "3103.685172",
          "totalAmountOut": "3101.435908547241992898",
          ...
      },
      "error": {
        "response": {
          "errno": 2004,
          "message": "Insufficient Liquidity"
        },
        "status": 200,
        "message": "Insufficient Liquidity",
        "name": "HttpException"
      }
    }
  ]
}
```

### 6. Send swap transaction

To send the swap transaction to source blockchain, you can use the information from the `/swap` or `/routeAndSwap` response. Here are some examples for different blockchain networks.

#### Common EVM Chains (Ethereum, BSC, Polygon, etc.)

```typescript
   const rpcUrl = '...';
   const senderPrivateKey = '....'; // Private key in hex format
   const receiver = '...'; // Receiver address on destination chain
   const wallet = new ethers.Wallet(senderPrivateKey, provider);
   const sender = wallet.address;

   const response = await axios.get(`https://bs-router-v3.chainservice.io/swap?hash=0x4cae26ffe044267ffa39f5885259c104abd67bec07a1452169dbc4fff5d0319c&slippage=300&from=${sender}&receiver=${receiver}`)
   /*
   ....
   asset the request is successful and get the swapData
    */
   const swapData = response.data.data[0];

   const provider = new ethers.providers.JsonRpcProvider(rpcUrl);
   const gasPrice = await provider.getGasPrice();
   const tx = {
      to: swapData.to,
      value: swapData.value,
      data: swapData.data,
      gasPrice: gasPrice,
   };
   
   const estimatedGas = await wallet.estimateGas(tx);
   const txWithGas = {
      ...tx,
      gasLimit: estimatedGas.mul(110).div(100),
   };
   const receipt = await wallet.sendTransaction(txWithGas);
   console.log('tx hash', receipt.hash);
```

#### Tron

```typescript
   const senderPrivateKey = '....';  // Private key in hex format
   const sender = TronWeb.address.fromPrivateKey(senderPrivateKey) as string;
   const receiver = '0x...'; // Receiver address on destination chain
   
   const response = await axios.get(`https://bs-router-v3.chainservice.io/swap?hash=0x4cae26ffe044267ffa39f5885259c104abd67bec07a1452169dbc4fff5d0319c&slippage=300&from=${sender}&receiver=${receiver}`)
   /*
   ....
   asset the request is successful and get the swapData
    */
   const swapData = response.data.data[0];
   
   const tronWeb = new TronWeb({
      fullHost: 'https://api.trongrid.io',
   });
   const triggerResult = await tronWeb.transactionBuilder.triggerConstantContract(
           swapData.to,
           '',
           {
              callValue: Number(swapData.value),
              input: swapData.data,
           },
           [],
           sender
   );
   
   const estimatedEnergy = Number(triggerResult.energy_used) * 1.2;
   const energyPrices = await tronWeb.trx.getEnergyPrices();
   const energyPricesList = energyPrices.split(',');
   const energyPrice = energyPricesList[energyPricesList.length - 1].split(':')[1];
   const feeLimit = Math.ceil(estimatedEnergy * Number(energyPrice));
   
   const tx = await tronWeb.transactionBuilder.triggerSmartContract(
           swapData.to,
           '',
           {
              callValue: Number(swapData.value),
              input: swapData.data,
              feeLimit: feeLimit,
           },
           [],
           sender
   );
   const signedTx = await tronWeb.trx.sign(tx.transaction, evmPrivateKey);
   const receipt = await tronWeb.trx.sendRawTransaction(signedTx);
   console.log('tx hash', receipt.txid);
```

#### Solana

```typescript
   const solanaRpcUrl = '...';   
   const senderPrivateKey = '...'; // Base58 encoded private key
   const sender = ''; // Sender address on Solana chain
   const receiver = ''; // Receiver address on destination chain
   const response = await axios.get(`https://bs-router-v3.chainservice.io/swap?hash=0x4cae26ffe044267ffa39f5885259c104abd67bec07a1452169dbc4fff5d0319c&slippage=300&from=${sender}&receiver=${receiver}`)
   /*
   ....
   asset the request is successful and get the swapData
    */
   const swapData = response.data.data[0];
   
   const connection = new Connection(solanaRpcUrl);
   const latestBlockHash = await connection.getLatestBlockhash();
   const wallet = new Wallet(Keypair.fromSecretKey(bs58.decode(senderPrivateKey)));
   const transaction = VersionedTransaction.deserialize(Buffer.from(swapData.data, 'hex'));
   transaction.message.recentBlockhash = latestBlockHash.blockhash;
   
   // Usually, the Solana wallet will add 2 instructions to set Compute Unit Price and set Compute Unit Limit.
   // If necessary, you can run simulation transaction and add them by yourself.

   transaction.sign([wallet.payer]);
   const rawTransaction = transaction.serialize();
   const txSig = await connection.sendRawTransaction(rawTransaction, {
      skipPreflight: false,
      maxRetries: 2,
   });;
   
   console.log('tx signature', txSig);
```

#### Bitcoin

Here is the example using OKX injected provider.

```typescript
   const rpcUrl = '...';
   const sender = '....'; // Sender address on BTC chain
   const receiver = '...'; // Receiver address on destination chain

   const response = await axios.get(`https://bs-router-v3.chainservice.io/swap?hash=0x4cae26ffe044267ffa39f5885259c104abd67bec07a1452169dbc4fff5d0319c&slippage=300&from=${sender}&receiver=${receiver}`)
   /*
      ....
      asset the request is successful and get the swapData
       */
   const swapData = response.data.data[0];
   
   const result = await window.okxwallet.bitcoin.send({
      from: sender,
      to: swapData.to,
      value: swapData.value,
      memo: swapData.memo,
   });
   
   console.log('tx hash', receipt.txHash);
```