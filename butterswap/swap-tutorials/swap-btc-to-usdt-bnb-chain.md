# BTC (Native Bitcoin) to USDT on BNB Chain Step by Step (No CEX Account)

This guide shows how to swap native BTC on Bitcoin mainnet into USDT on BNB Chain using ButterSwap. If you are looking to convert BTC to USDT on BNB Chain without a centralized exchange account, follow the steps below.

## Pre-filled BTC to USDT (BNB Chain) swap link

[Pre-filled BTC to USDT on BNB Chain swap link](https://www.butterswap.io/en/swap?referrer=&to=56%3AUSDT&from=1360095883558913%3ABTC)

Note: This link defaults to USDT on BNB Chain. If you want a different token on BNB Chain, change the To token before confirming.

Important: This page is for native BTC on Bitcoin mainnet only. It is not WBTC, BTCB, or BTC on BNB Chain.

## Quick checklist (30 seconds)

✅ BTC on Bitcoin mainnet (native BTC)  
✅ A BNB Chain receiving address (EVM address starting with 0x)  
✅ Extra BTC for the Bitcoin network fee (miner fee)  
✅ If you plan to move funds later on BNB Chain, have a small amount of BNB for gas (not required just to receive)

## What you will get (in one sentence)

You will send native BTC on Bitcoin mainnet and receive USDT on BNB Chain to an EVM address (0x).

## Before you start

### 1) BNB Chain address format (do not mix networks)
Your Received Address must be an EVM address:

✅ 0x... (BNB Chain / EVM wallet address)  
❌ Not bc1... / 1... / 3... (Bitcoin address)  
❌ Not T... (TRON address)

### 2) BTC fees are paid on Bitcoin (in BTC)
Bitcoin sends require a miner fee. Keep extra BTC available so your wallet can broadcast the transaction.

### 3) USDT on BNB Chain vs other USDT versions
This guide is for USDT on BNB Chain (often called BEP20 USDT). Always confirm the To network shows BNB Chain.

### 4) Generic wallet connection help
For general ButterSwap steps, see the [Butter Swap User Guide](/butterswap/user-guide.md).

## Step by step BTC (Native Bitcoin) to USDT (BNB Chain)

### Step 1) Open ButterSwap
Go to the pre-filled swap page (recommended) or open the app:

- Prefilled: [BTC to USDT on BNB Chain](https://www.butterswap.io/en/swap?referrer=&to=56%3AUSDT&from=1360095883558913%3ABTC)
- App: [dApp](https://www.butterswap.io/en/swap)

You should see:
- From: BTC on Bitcoin
- To: USDT on BNB Chain

<img src="/.gitbook/assets/BTC-to-BNB-main.png" width="768" alt="BTC to USDT on BNB Chain main screen">
<p><em>From BTC (Bitcoin mainnet) to USDT (BNB Chain)</em></p>

### Step 2) Connect your BTC wallet first (From)
Click Connect BTC Wallet on the swap card and connect the wallet that holds your native BTC on Bitcoin mainnet.

If your BTC balance shows as 0, confirm you are using a Bitcoin wallet that holds native BTC on Bitcoin mainnet.

<img src="/.gitbook/assets/BTC-to-BNB-connect-btc-wallet.png" width="768" alt="Connect BTC Wallet">
<p><em>Connect BTC Wallet for the From side</em></p>

### Step 3) Optional change the destination token on BNB Chain
This guide defaults to USDT on BNB Chain.

If you want a different token on BNB Chain, change the To token before continuing. Keep the To network as BNB Chain.

<img src="/.gitbook/assets/BTC-to-BNB-to-token-selector.png" width="768" alt="BNB Chain token selector">
<p><em>To token selector on BNB Chain (USDT default)</em></p>

### Step 4) Set your BNB Chain receiving address (two valid paths)
In Received Address, you will see two options:

Option A: Connect wallet (same wallet flow)  
Click Connect Wallet under Received Address to connect the wallet that will receive your USDT on BNB Chain.

Option B: Enter Address (different wallet)  
Click Enter Address and paste your BNB Chain EVM address.

✅ Valid BNB Chain address format: 0x...  
❌ Do not use: bc1... / 1... / 3... (Bitcoin), T... (TRON)

<img src="/.gitbook/assets/BTC-to-BNB-received-address-options.png" width="768" alt="Received Address options">
<p><em>Received Address options (Connect Wallet or Enter Address)</em></p>

### Step 5) Enter amount and review route and fees
Enter the amount of BTC you want to swap.

Review the Best Route panel on the right (route steps and estimated receive). Check the fee and ETA area.

<img src="/.gitbook/assets/BTC-to-BNB-route-and-fees.png" width="768" alt="Route and fees">
<p><em>Best Route and fee or ETA area</em></p>

### Step 6) Confirm and complete the flow (UI dependent)
Click Confirm to open the swap summary popup. Then follow the exact flow you see in the ButterSwap UI.

Valid path A: In wallet confirmation  
If your BTC wallet supports in app signing, you may be asked to approve or sign in your wallet.

Valid path B: On screen instructions inside ButterSwap  
If ButterSwap shows BTC send or deposit instructions inside the swap flow, follow the exact instructions shown. Do not send BTC anywhere unless ButterSwap shows it in the swap confirmation flow.

After submitting, you can monitor progress via:
- History in the swap UI (if shown)
- [ButterSwap Explorer](https://explorer.butterswap.io/en) (if linked from the swap details screen)

<img src="/.gitbook/assets/BTC-to-BNB-confirm-swap.png" width="768" alt="Confirm swap popup">
<p><em>Confirm swap popup</em></p>

## Fees and timing

### Do I need BNB?
To receive USDT on BNB Chain, usually no. To move or swap on BNB Chain later, yes, you will need a small amount of BNB for gas.

### What BTC do I send?
Native BTC on Bitcoin mainnet, not wrapped BTC like WBTC or BTCB.

### How long does it take?
Timing varies based on Bitcoin confirmations (miner fee affects this) and route liquidity or network conditions. Track progress in History and verify via [ButterSwap Explorer](https://explorer.butterswap.io/en) if available.

## Common issues (quick fixes)

### Wrong receiving address format (most common)
Your Received Address must be an EVM address (0x) for BNB Chain. Do not use bc1 addresses (Bitcoin) or T addresses (TRON).

### I selected the wrong USDT network
Make sure the To token is USDT on BNB Chain, not USDT on TRON or Ethereum.

### Not enough BTC to cover miner fee
If your BTC send fails or you cannot proceed, reduce the BTC amount slightly and retry.

### Confusing wallet connect vs Received Address
Connecting a wallet is not always the same as setting the destination. Always verify the Received Address field before confirming.

## FAQ (BTC to BNB Chain USDT)

### Can I swap BTC to USDT on BNB Chain without using a centralized exchange?
Yes. This is a wallet based cross chain swap flow on ButterSwap with no CEX account required.

### What address do I use to receive USDT on BNB Chain?
Use an EVM address starting with 0x (your BNB Chain wallet address).

### Is BTC to USDT (BEP20) the same as BTC to USDT on BNB Chain?
Most users mean the same thing. USDT on BNB Chain is commonly called BEP20 USDT and uses an 0x address format.

### Do I need BNB to receive USDT on BNB Chain?
Usually no for receiving. You will need BNB for gas if you want to move the USDT later.

### Is this native BTC on Bitcoin mainnet (not WBTC or BTCB)?
Yes. This tutorial is specifically for native BTC on Bitcoin mainnet only.

### Can I send BTC directly to a 0x address to convert it?
No. BTC and BNB Chain are different networks. You need a cross chain swap route to receive USDT on BNB Chain.

### How do I swap BTC to a different token on BNB Chain?
Open the swap page and change the To token. Keep the To network as BNB Chain before confirming.

## Start your BTC to BNB Chain swap

Open the pre-filled page:
- [BTC to USDT on BNB Chain](https://www.butterswap.io/en/swap?referrer=&to=56%3AUSDT&from=1360095883558913%3ABTC)

Or open the [dApp](https://www.butterswap.io/en/swap) and set:
- From: BTC (Bitcoin mainnet)
- To: BNB Chain (select token)

## Related guides

- [USDT (TRC20) to BTC (Native Bitcoin) Step by Step](/butterswap/swap-tutorials/swap-usdt-trc20-to-btc.md)
