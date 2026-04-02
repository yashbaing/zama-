# ⚡ ZKTrader — Private Trading on Midnight Network

**Trade crypto without exposing your portfolio, orders, or strategy to anyone.**

ZKTrader is a decentralized exchange where everything that matters stays private. Your balances, order prices, trade sizes, and investment strategies are protected using zero-knowledge proofs — powered by Midnight Network's programmable privacy infrastructure.

---

## 🧠 The Problem

On every existing DEX, your entire financial life is public:

- **Everyone sees your balance** — wallets are open books
- **Bots front-run your trades** — MEV extracts billions yearly
- **Your strategy is exposed** — competitors copy your moves in real-time

Blockchain transparency was meant to build trust. Instead, it became a surveillance tool.

## 🔐 The Solution

ZKTrader uses **Midnight Network** — a fourth-generation blockchain with built-in privacy — to keep your trading activity confidential:

| What's Private | How It Works |
|---|---|
| **Your balance** | Stored as encrypted values on-chain. Only you can decrypt. |
| **Your orders** | Price & amount are hidden using ZK proofs. No one sees your limit price. |
| **Trade execution** | Matching engine compares encrypted values. Prices never appear in plaintext. |
| **Your strategy** | Auto-invest and copy-trading allocations are fully shielded. |

The protocol itself **cannot** read your data. There are no admin backdoors.

## ⚙️ How It Works (Simple Version)

```
1. You type: "Buy 1 BTC at $67,000"
2. Your browser encrypts price + amount using ZK cryptography
3. Encrypted order goes on-chain — no one can read it
4. Matching engine checks: does any sell price ≤ your buy price?
   (This comparison happens on encrypted data — prices never revealed)
5. Trade settles. Your encrypted balance updates.
6. Only you can decrypt and see your new balance.
```

**Result:** You traded on a public blockchain, but no one — not validators, not other traders, not even the protocol — saw your order details.

## 🏗️ What's Inside

```
├── contracts/        Smart contracts (Solidity + ZK privacy)
│   ├── Vault.sol           Encrypted balance storage
│   ├── OrderBook.sol       Encrypted order book
│   ├── TradingEngine.sol   Privacy-preserving order matching
│   ├── CopyTrading.sol     Encrypted strategy copying
│   └── AutoInvestVault.sol Fear & Greed auto-invest
│
├── frontend/         Trading interface (Next.js)
│   ├── Dashboard          Portfolio overview (decrypted locally)
│   ├── Trade              Charts + encrypted order placement
│   ├── Vault              Deposit / withdraw
│   ├── Copy Trading       Follow encrypted strategies
│   └── History            Transaction log
│
├── backend/          API & services (Express)
│   ├── Price feeds        Public market data
│   ├── Event indexer      On-chain activity (metadata only)
│   ├── Matching keeper    Off-chain order matcher bot
│   └── WebSocket          Real-time streaming
│
└── docs/             Security audit & architecture
```

## 🔑 Privacy Model

**What's encrypted (private):**
- All user balances (`euint64` encrypted integers)
- Order prices and amounts
- Trade fill sizes
- Auto-invest allocation percentages
- Copy-trading strategy weights

**What's public (by design):**
- Order side (BUY/SELL) — needed for matching
- Trading pair (BTC/USDC, etc.)
- Order timestamps
- Market prices (from external feeds)

**Anti-front-running:** Since order prices are encrypted, MEV bots can't sandwich your trades, snipe your limit orders, or copy your strategy.

## 🚀 Quick Start

```bash
# One-command setup
chmod +x setup.sh && ./setup.sh

# Or step by step:
cd contracts && pnpm install && npx hardhat compile
cd ../backend && pnpm install && pnpm dev
cd ../frontend && pnpm install && pnpm dev

# Open http://localhost:3000
```

**With Docker:**
```bash
docker-compose up --build
```

## 🧪 Testing

```bash
# Smart contract tests (runs real ZK operations)
cd contracts && npx hardhat test --network localfhevm

# Frontend tests
cd frontend && pnpm test
```

## 🌐 Built With

- **[Midnight Network](https://midnight.network)** — Programmable privacy blockchain with ZK proofs, selective disclosure, and the Compact language
- **Zero-Knowledge Proofs** — Prove statements without revealing data
- **Next.js + TypeScript** — Modern frontend
- **Solidity** — Smart contract layer
- **Ethers.js** — Blockchain interaction

## 📊 Key Numbers

| Metric | Value |
|---|---|
| Smart contracts | 7 |
| Frontend pages | 6 |
| Backend services | 5 |
| Test cases | 50+ |
| Total code | 8,500+ lines |

## 🛡️ Security

Full security audit checklist and threat model available in [`docs/SECURITY_AUDIT.md`](docs/SECURITY_AUDIT.md).

Key guarantees:
- No plaintext sensitive data on-chain — ever
- Client-side key generation — keys never leave your browser
- No admin access to user funds or data
- Reencryption requires cryptographic proof of ownership

## 📄 License

MIT

---

*ZKTrader demonstrates that DeFi doesn't have to mean "public by default." With Midnight Network's privacy infrastructure, traders get the security of decentralization without sacrificing confidentiality.*
