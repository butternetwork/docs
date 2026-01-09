# Omni Vault Liquidity Pool Introduction

## 1. Vault Basics

### 1.1 What is Omni Vault?

**Omni Vault** is a liquidity pool where users provide liquidity for the cross-chain bridge. Vaults are distributed across various External Chains (such as Ethereum, BSC, Polygon, etc.). Users deposit assets into the Vault to support cross-chain transactions and earn Vault Fee as rewards.

### 1.2 Key Features

| Feature | Description |
|---------|-------------|
| **Unified Asset Model** | Same assets on different chains are fully equivalent, Vaults share earnings equally |
| **Multi-chain Distribution** | Each asset has Vaults on multiple chains, forming a liquidity network |
| **Revenue Sharing** | Vault providers share cross-chain transaction fees (Vault Fee) |
| **Simple & Transparent** | Fixed fee rate, predictable earnings |

### 1.3 User Participation Flow

```
1. User selects chain and asset (e.g., USDC on Ethereum)
2. Deposit assets into the corresponding chain's Vault contract
3. Receive Vault Token (LP certificate)
4. Start earning Vault Fee share
5. Redeem Vault Token anytime to withdraw assets
```

---

## 2. Vault Fee Earnings

### 2.1 Fee Rate

| Item | Current Rate | Note |
|------|--------------|------|
| **Vault Fee** | **0.018%** | Adjustable via governance |

### 2.2 Earnings Calculation

```
User Earnings = Cross-chain Amount × Vault Fee × (User Vault Token / Total Vault Token)
```

### 2.3 Earnings Examples

Assuming user holds 10% share of a chain's USDC Vault (at current 0.018% rate):

| Daily Volume | Total Vault Fee | User Earnings (10% share) |
|--------------|-----------------|---------------------------|
| $1,000,000 | $180 | $18 |
| $10,000,000 | $1,800 | $180 |
| $100,000,000 | $18,000 | $1,800 |

### 2.4 Annualized Yield Estimation

Assuming Vault TVL is $1,000,000, user deposits $100,000 (10% share), at current 0.018% rate:

| Daily Volume | Annual Vault Fee | User Annual Earnings | APY |
|--------------|------------------|---------------------|-----|
| $1,000,000 | $65,700 | $6,570 | **6.57%** |
| $5,000,000 | $328,500 | $32,850 | **32.85%** |
| $10,000,000 | $657,000 | $65,700 | **65.7%** |

> Note: Actual earnings depend on trading volume, Vault TVL, and the Vault Fee rate at that time

---

## 3. Vault Operations

### 3.1 Deposit

```
1. Connect wallet to the corresponding chain
2. Select asset and amount to deposit
3. Approve and confirm deposit transaction
4. Receive Vault Token
```

### 3.2 Withdraw

```
1. Select amount of Vault Token to withdraw
2. Confirm withdrawal transaction
3. Receive original assets + accumulated Vault Fee earnings
```

### 3.3 Earnings Collection

- Vault Fee earnings automatically accumulate in Vault Token value
- Principal + earnings received upon withdrawal

---

## 4. Governance

### 4.1 Adjustable Parameters

| Parameter | Current Value | Note |
|-----------|---------------|------|
| Vault Fee | 0.018% | Adjustable via governance voting |

### 4.2 Future Plans

- **Incentive Programs**: Token incentive programs may be launched in the future, allowing Vault providers to earn additional rewards

---

## 5. Summary

| Item | Description |
|------|-------------|
| **Earnings Source** | Vault Fee (currently 0.018%, adjustable via governance) |
| **Earnings Method** | Pro-rata share distribution |
| **Lock-up Requirement** | None, deposit/withdraw anytime |
| **Expected Returns** | Depends on volume/TVL ratio and fee rate |

**Key Advantages**:
- Simple and transparent earnings model
- No lock-up period, high liquidity
- Fee rate adjustable via governance
- Multi-chain deployment, flexible options
