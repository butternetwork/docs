# USDT (TRC20) → BTC (Native Bitcoin): Step-by-Step (No CEX Account)

This guide shows how to swap USDT on TRON (TRC20) into native BTC on the Bitcoin network using ButterSwap’s cross-chain swap flow (no centralized exchange account required).

## Pre-filled USDT → BTC swap link
[Pre-filled USDT → BTC swap link](https://www.butterswap.io/en/swap?from=728126428%3AUSDT&to=1360095883558913%3ABTC)

**Important:** If you are receiving native BTC on Bitcoin, your **Received Address must be a Bitcoin address** (e.g., `bc1...`, `1...`, `3...`).  
Do **not** paste a TRON address (often starts with `T...`) or an EVM address (`0x...`).

Need the opposite direction? See: **BTC (Native Bitcoin) → TRON (TRX / USDT-TRC20): Step-by-Step (No CEX Account)** (link once published).

---

## Quick checklist (30 seconds)

Before you start, make sure you have:

✅ USDT (TRC20) on TRON  
✅ A small amount of TRX (TRON network fees)  
✅ A Bitcoin receiving address (native BTC on Bitcoin mainnet)  
✅ A supported wallet connection (WalletConnect works if your wallet isn’t listed)

---

## What you’ll get (in one sentence)

You’ll send **USDT (TRC20) on TRON** and receive **native BTC on Bitcoin mainnet** to a **Bitcoin address**.

---

## Before you start

### Address format check (BTC receiving)
✅ Valid BTC formats: `bc1...`, `1...`, `3...`  
❌ Do not use: `T...` (TRON), `0x...` (EVM)

### Gas / fees (TRON)
TRON transaction fees are paid in **TRX** (bandwidth/energy). Keep a small amount of TRX available.

For generic wallet connection help: [Click Here](/butterswap/user-guide.md)

---

## Step-by-step: USDT (TRC20) → BTC (native)

### Step 1 — Open ButterSwap
Go to the pre-filled swap page (recommended) or go to the app:

- **Prefilled:** [Pre-filled USDT → BTC swap link](https://www.butterswap.io/en/swap?from=728126428%3AUSDT&to=1360095883558913%3ABTC)
- **dApp:** [dApp](https://www.butterswap.io/en/swap)

Set:
- **From:** USDT on TRON (TRC20)
- **To:** BTC on Bitcoin (native BTC)

<img src="/.gitbook/assets/02-usdt-tron-to-btc.png" width="768" alt="USDT TRON to BTC">
<p><em>From=USDT (TRON) and To=BTC (Bitcoin)</em></p>

### Step 2 — Connect your TRON wallet (From)
Click **Connect Tron Wallet** (the big button on the swap card) and connect the wallet that holds your USDT (TRC20).

> If you connected the wrong wallet type and your TRON USDT balance shows as 0, switch to a wallet that supports TRON assets (TRC20).  
> Note: The wallet button in the top-right is not the same as setting your BTC receiving address. You’ll set the BTC destination in **Received Address** next.
 
<img src="/.gitbook/assets/03-connect-tron-wallet.png" width="768" alt="Connect Tron Wallet">
<p><em>Connect Tron Wallet</em></p>

### Step 3 — Set your BTC receiving address on Bitcoin mainnet (two valid paths)
In **Received Address**, you’ll see two options:

- **Option A — Connect wallet (same-wallet flow):**  
Click **Connect Wallet** under Received Address to connect to the same wallet holding your TRON USDT. (If it doesn’t provide a Bitcoin address, use Option B.)

- **Option B — Enter a BTC address (send to another wallet):**  
Click **Enter Address** and paste your Bitcoin address.

✅ Valid BTC formats: `bc1...`, `1...`, `3...`  
❌ Do not use: `T...` (TRON), `0x...` (EVM)

<img src="/.gitbook/assets/04-received-address-options.png" width="768" alt="Received Address options">
<p><em>Received Address options (Connect Wallet / Enter Address)</em></p>  

### Step 4 — Enter amount and review route + fees
- Enter the amount of USDT you want to swap  
- Review the **Best Route** panel on the right (route steps + estimated receive)  
- Check the fee/ETA area (example fields you may see):
  - Fee
  - Original chain gas fee estimate (TRON fees paid in TRX — bandwidth/energy)
  - Estimated time of arrival
  
<img src="/.gitbook/assets/05-route-and-fees.png" width="768" alt="Best Route and fees">
<p><em>Best Route + fee/ETA area</em></p>

### Step 5 — Click Confirm (popup) and sign in your wallet
Click **Confirm**. A popup will show the swap summary. Confirm, then follow your wallet prompts:

- If prompted, **approve USDT** (first time only)
- Final transaction confirmation signature(s)

After submitting, you can monitor progress via:
- History in the swap UI
- [ButterSwap Explorer](https://explorer.butterswap.io/en) 

<img src="/.gitbook/assets/06-confirm-swap.png" width="768" alt="Confirm swap popup">
<p><em>Confirm swap popup</em></p>  

---

## Fees & timing (USDT TRC20 → BTC)

### Do I need TRX?
Yes. On TRON, transaction fees are paid in TRX (bandwidth/energy). Keep a small amount of TRX available.

### What BTC do I receive?
Native BTC on Bitcoin mainnet (not wrapped BTC like WBTC/BTCB).

### How long does it take?
Timing varies based on network conditions and routing/liquidity. Track progress in History and verify via [ButterSwap Explorer](https://explorer.butterswap.io/en).

---

## Common issues (quick fixes)

### Wrong receiving address format (most common)
Your Received Address must be a Bitcoin address: `bc1…`, `1…`, or `3…`.  
Don’t use `T…` (TRON) or `0x…` (EVM).

### Not enough TRX for fees (bandwidth/energy)
If you can’t proceed or the wallet errors, top up a small amount of TRX and retry.

### Expecting “BTC on TRON” instead of BTC on Bitcoin
This guide swaps TRON USDT (TRC20) → BTC on Bitcoin mainnet, not “BTC” on another chain.

### Confusing wallet connect vs Received Address
Connecting a wallet ≠ setting a BTC destination address. Always double-check the **Received Address** field before confirming.

---

## FAQ (USDT TRC20 → BTC)

### Can I swap USDT (TRC20) to BTC without using a centralized exchange?
Yes. This is a wallet-based cross-chain swap flow (no CEX account required).

### Can I send USDT (TRC20) directly to a Bitcoin (BTC) address?
No. They’re on different networks. You need a cross-chain swap route to receive native BTC on Bitcoin.

### Do I need TRX to swap USDT on TRON (TRC20)?
Usually yes, TRON fees are paid in TRX (bandwidth/energy).

### What Bitcoin address format should I use to receive BTC?
Use a Bitcoin mainnet address like `bc1…`, `1…`, or `3…`.

### What’s the difference between TRC20 and the Bitcoin network?
TRC20 is a token standard on TRON. BTC is native to Bitcoin mainnet. They aren’t interchangeable without a cross-chain swap.

### Is “convert USDT TRC20 to Bitcoin” the same as “swap USDT TRC20 to BTC”?
Most of the time, yes! Users mean exchanging TRON USDT into native BTC on Bitcoin.

---

## Start your USDT (TRC20) → BTC swap

Open ButterSwap [dApp](https://www.butterswap.io/en/swap) and set:
- **From:** USDT (TRC20) on TRON  
- **To:** BTC (Native Bitcoin) on Bitcoin mainnet

---

## Related guides

- BTC (Native Bitcoin) → TRON (TRX / USDT-TRC20): Step-by-Step (No CEX Account) (link once published)
- BTC (Native Bitcoin) → USDT on BNB Chain: Step-by-Step (No CEX Account) (link once published)
- BTC (Native Bitcoin) → SOL on Solana: Step-by-Step (No CEX Account) (link once published)
