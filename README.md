# BlockShop — Ethereum E-Commerce Platform

A full-stack decentralized marketplace built on Ethereum smart contracts, powered by **Ganache Local** for development.

---

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- [Ganache](https://trufflesuite.com/ganache/) (GUI) or `npm install -g ganache` (CLI)
- [MetaMask](https://metamask.io/) browser extension

---

## 1. Start Ganache

**Option A — Ganache GUI**
1. Open Ganache
2. Create a new Workspace (or Quickstart)
3. Ensure settings: **Port: 7545 | Network ID / Chain ID: 1337**

**Option B — Ganache CLI**
```bash
npx ganache --port 7545 --chain.chainId 1337
```

---

## 2. Deploy Smart Contracts

```bash
cd blockchain
npm install
cp .env.example .env
# Paste one of Ganache's account private keys into .env → PRIVATE_KEY=0x...
npx hardhat run scripts/deploy.js --network ganache
```

This writes `deployment.json` to both `backend/config/` and `frontend/src/contracts/`.

---

## 3. Start Backend

```bash
cd backend
npm install
# ETH_RPC_URL=http://127.0.0.1:7545 is already set in .env
npm start
```

Backend runs on **http://localhost:5001**

---

## 4. Start Frontend

```bash
cd frontend
npm install
npm start
```

Frontend runs on **http://localhost:3000**

---

## 5. Configure MetaMask

Add Ganache network to MetaMask:
| Field | Value |
|---|---|
| Network Name | Ganache Local |
| RPC URL | http://127.0.0.1:7545 |
| Chain ID | 1337 |
| Currency Symbol | ETH |

> **Tip:** The app auto-prompts MetaMask to switch/add Ganache when you click "Connect Wallet".

Import a Ganache account private key into MetaMask to see your test ETH balance.

---

## Project Structure

```
blockshop/
├── blockchain/          # Hardhat project — Solidity contracts
│   ├── contracts/       # BlockShopMarketplace.sol, BlockShopToken.sol
│   ├── scripts/         # deploy.js
│   └── hardhat.config.js
├── backend/             # Express API
│   ├── config/
│   │   ├── blockchain.js   # Ethers.js provider (Ganache: 127.0.0.1:7545)
│   │   └── .env            # ETH_RPC_URL=http://127.0.0.1:7545
│   └── routes/
├── frontend/            # React app
│   └── src/
│       └── context/
│           └── Web3Context.js  # Ganache chainId 1337, port 7545
└── README.md
```

---

## Network Configuration Summary

| Setting | Value |
|---|---|
| Network | Ganache Local |
| RPC URL | http://127.0.0.1:7545 |
| Chain ID | 1337 (0x539) |
| MetaMask hex | 0x539 |

---

## Wallet Balance Fix

The wallet balance is fetched directly from the Ganache node via `ethers.BrowserProvider` on every connect, and **auto-refreshes every 5 seconds** so it always stays accurate. No more 0 ETH display.

# BLOCKCHAIN_ECOMMERCE
