# CopyMarket Devnet Runbook

This file explains how to produce the strongest proof for CopyMarket: a live Solana devnet escrow
settlement where the buyer funds escrow, the seller delivers `copyrescue`, and the arbiter releases
payment to the seller.

## Current Prepared Wallets

The local setup generated these public devnet addresses:

```text
buyer:   6WwdWJNYYFAthMJFP1gdM7xysGJv1GhwpBRSL2ch8Yhd
seller:  FeXKD6fYwGeBMeU5G9qF6HJk3Z9Wj5qFjFTopktFmJfD
arbiter: H5xAASAz21bhdtdRi73QSxa1bphXMTGCLXCwCbw2Ud9g
```

Only public addresses are shown here. The generated `.env` and `WALLETS.txt` contain private key
material and must stay local.

## Needed Before A Live Run

1. Fund the buyer address with devnet SOL from `https://faucet.solana.com`.
2. Use a working Solana devnet RPC in `SOLANA_RPC_URL`.
3. Optionally add an LLM key. Without one, the seller still returns deterministic structured output.

In this environment, public Solana devnet RPC requests timed out during preparation, so the live
Explorer proof was left ready-to-run rather than fabricated.

## Run Commands

From the repo root:

```sh
npm install --prefix scripts
node scripts/setup.js
```

Then add or confirm the following values in `.env`:

```ini
SOLANA_RPC_URL=https://api.devnet.solana.com
BUYER_SERVICE=copyrescue
BUYER_ARG=crypto wallet landing page needs a clearer hero and trust path
BUYER_MAX_SOL=0.001
SETTLEMENT_MODE=arbiter
```

Run the market stack:

```sh
docker compose up -d coral
bash build-agents.sh
cd examples/marketplace
npm install
npm start
```

Expected lifecycle:

```text
WANT copyrescue ...
BID ...
AWARD ...
ESCROW_REQUIRED ...
DEPOSITED ...
DELIVERED ...
ARBITER_RELEASED ...
```

The buyer logs print devnet Explorer links for the arbiter program, vault PDA, escrow PDA, open
transaction, and release transaction when `TRACE=1`.

## Reviewer Shortcut

If a reviewer does not want to run devnet, inspect:

- `coral-agents/seller-agent/src/service.ts`
- `coral-agents/buyer-agent/src/index.ts`
- `sample_copyrescue_delivery.json`
- `CopyMarket_Agent_Economy_Pitch.pptx`
- `CopyMarket_demo_video.avi`

These show the paid service, the market loop, and the escrow-gated delivery path.
