# TakumiPay Backend API — Monad Metropolis Hackathon 2026

> **NestJS Payment Orchestration, EIP-712 Merchant Quoting & Monad Network Rails**  
> *Orchestrates cross-border remittance, merchant intent settlement, and dynamic blockchain configurations for TakumiPay.*

- **Team:** Planckify Labs
- **Track Entered:** Track 02 — Consumer Products & Payments
- **Framework:** NestJS, Prisma ORM, PostgreSQL, Redis / Valkey
- **License:** [GNU General Public License v3.0 (GPLv3)](./LICENSE)

---

## Overview

The TakumiPay Backend API acts as the central orchestration engine connecting consumer mobile clients to on-chain settlement rails, fiat gateways, and merchant acquirers.

For the **Monad Metropolis Hackathon**, the API provides:
1. **Dynamic Monad Blockchain Catalogue:** Serves Monad Mainnet (`143`) and Monad Testnet (`10143`) network configurations, RPC routes, and block explorer endpoints via `GET /blockchains`.
2. **Agora AUSD Stablecoin Management:** Seeds and governs AUSD token parameters (`0x00000000eFE302BEAA2b3e6e1b18d08D69a9012a`), decimals, and payment eligibility flags.
3. **EIP-712 Merchant Quote Signer (`QuoteSignerService`):** Deterministically computes and cryptographically signs payment quotes verified on-chain by `TakumiPay.sol`'s `processMerchantPayment`.
4. **Non-Blocking Settlement State Machine:** Asynchronously processes and tracks on-chain Monad transactions from broadcast to confirmation.

---

## Monad Configuration & Deployed Contract Integration

- **Monad Mainnet (Chain ID `143`):**
  - TakumiPay Proxy: `0x479B0843C3e0627f36551660506dEd5b349Fa968`
  - Agora AUSD: `0x00000000eFE302BEAA2b3e6e1b18d08D69a9012a` (6 decimals)
  - Native Gas: `MON` (18 decimals)
- **Monad Testnet (Chain ID `10143`):**
  - TakumiPay Proxy: `0x9EEC5aD4FC092fD468A8114007e541238F4Ba5ee`
  - MockAUSD Stand-In: `0x1aC593085Fa34c651E805085da4b2cabAC676F99` (6 decimals)

---

## Metropolis Hackathon Build & Originality Disclosure

*(Mandatory disclosure under Section 4.1 Clause 4 of Metropolis Hackathon Rules)*

- **Pre-Existing Foundation (Prior to September 1, 2026):**
  Core NestJS API architecture, Prisma schema, auth middleware, and multi-chain RPC proxy integration.
- **Hackathon Additions & Refinements (September 18 – September 26, 2026):**
  - Monad Mainnet (`143`) and Testnet (`10143`) network and token seeds (`src/scripts/prisma/seed.ts`).
  - Agora AUSD token integration with payment enable flags.
  - EIP-712 domain separator binding for Monad settlement validation in `intents.service.ts`.
  - Non-blocking payment verification polling endpoints.
- **AI Tools Disclosure:**
  Drafted and verified with assistance from Claude and Gemini.

---

## Getting Started

### Prerequisites
- Node.js 20+
- `pnpm`
- PostgreSQL & Redis (or Docker)

### Installation
```bash
# Install dependencies
pnpm install

# Run database migrations
pnpm prisma migrate deploy

# Seed blockchain and token catalogues (including Monad and AUSD)
pnpm prisma db seed
```

### Running the API
```bash
# Start development server
pnpm start:dev

# Run tests
pnpm test
```

---

## License

This project is licensed under the [GNU General Public License v3.0 (GPLv3)](./LICENSE).
