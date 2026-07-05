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

1. Fund the buyer address with devnet SOL from `https://faucet.solana.com` or `requestAirdrop`.
2. Use a working Solana devnet RPC in `SOLANA_RPC_URL`; `https://api.devnet.solana.com` was verified.
3. Optionally add an LLM key. Without one, the seller still returns deterministic structured output.

## Live Devnet Proofs

Buyer funding proof:

```text
https://explorer.solana.com/tx/4CMqLmrU6zLTaCFse1NP6F4WTeDjj1hbFcRagV8T8rNEQ8ZBziieaE2W8khwRree3iVnjrUTTBkyC497u6vAUoBe?cluster=devnet
```

Buyer-to-seller payment smoke proof:

```text
https://explorer.solana.com/tx/49V7wedjpa66Rzk87qhCzjshWVx4uw2zhBL4WhKzN7kTEfshickWW9dcwbUS11adb33LkhEFEiE9hFdQbcV1s7zo?cluster=devnet
```

The second transaction transfers 0.001 devnet SOL from the prepared buyer wallet to the prepared seller
wallet. It is a live payment smoke proof, not the full arbiter escrow lifecycle. The full arbiter escrow
run remains the strongest next reproduction step below.

## Runnable Local Checks

The public repository includes the buyer package, seller package, and the local `@pay/agent-runtime`
dependency required by both agents. A reviewer can run the local verification without the older
Docker/example workspace commands.

From the repo root, use Node 20+ and pnpm:

```sh
pnpm run verify
```

Equivalent package-level commands:

```sh
cd coral-agents/buyer-agent
pnpm install --lockfile=false --ignore-scripts
pnpm exec tsc --noEmit
pnpm exec vitest run

cd ../seller-agent
pnpm install --lockfile=false --ignore-scripts
pnpm exec tsc --noEmit
pnpm exec vitest run
```

Expected local verification:

```text
buyer-agent: 2 test files, 13 tests passed
seller-agent: 5 test files, 16 tests passed
```

## Live Arbiter Lifecycle Status

The current public Explorer proof is a finalized buyer-to-seller devnet smoke transfer. The repo
contains the escrow/arbiter code path and devnet guard tests, but it does not yet publish a complete
Explorer transaction set for `deposit -> delivery -> release/refund`.

The next hardening target is to run the arbiter flow with funded devnet wallets and publish the
open/release/refund Explorer links alongside `DEVNET_PAYMENT_PROOF.json`. Until then, this runbook
should be read as runnable local checks plus public smoke transfer proof, not a completed production
escrow audit.

Required private inputs for that run:

- `BUYER_KEYPAIR_B58`
- `ARBITER_KEYPAIR_B58`
- `SELLER_WALLET`
- funded devnet buyer balance

Do not publish those private key values. Only publish public addresses, Explorer links, and PDA values.

## Reviewer Shortcut

If a reviewer does not want to run devnet, inspect:

- `coral-agents/seller-agent/src/service.ts`
- `coral-agents/buyer-agent/src/index.ts`
- `sample_copyrescue_delivery.json`
- `CopyMarket_Agent_Economy_Pitch.pptx`
- `CopyMarket_demo_video.mp4`
- `CopyMarket_demo_video.avi`
- `devnet_airdrop_proof.json`
- `DEVNET_PAYMENT_PROOF.json`

These show the paid service, the market loop, and the escrow-gated delivery path.
