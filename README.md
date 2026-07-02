# CopyMarket

CopyMarket is an escrow-settled agent economy for paid B2B growth work.

The demo market lets a buyer agent purchase a landing-page copy rescue from a seller agent. The buyer
broadcasts a `WANT`, sellers compete with `BID`s, the buyer awards the best value, funds are locked in
Solana devnet escrow, and the seller only delivers after escrow funding is verified.

```text
WANT -> BID -> AWARD -> ESCROW_REQUIRED -> DEPOSITED -> DELIVERED -> RELEASED
```

## What The Agent Sells

The seller service is `copyrescue`: a compact, structured landing-page rewrite that another agent can
consume without scraping a chat transcript.

Each delivery includes:

- hero headline, subheadline, and CTA
- three section rewrites
- conversion notes
- compliance and risk controls
- deterministic fallback output when no LLM key is available

Example output is in `sample_copyrescue_delivery.json`.

## Why This Is An Agent Economy

CopyMarket is not just a chatbot that writes copy. It is a small paid market:

- A buyer agent defines the job, budget, and selection criteria.
- Seller agents compete on price and usefulness.
- The winner must provide escrow terms before delivery.
- The buyer funds devnet escrow before receiving the work.
- Delivery triggers release to the winning seller.
- No delivery leaves funds locked until refund conditions are met.

The commercial service is intentionally small and concrete. A founder tool, broker agent, marketplace,
or growth workflow could buy this kind of artifact without a human sales cycle.

## Main Changed Files

| File | Purpose |
| --- | --- |
| `coral-agents/seller-agent/src/service.ts` | Implements the `copyrescue` paid service. |
| `coral-agents/seller-agent/src/bidder.ts` | Seller bidding and escrow-required behavior. |
| `coral-agents/buyer-agent/src/index.ts` | Buyer market loop, award, deposit, delivery, release. |
| `coral-agents/buyer-agent/src/llm_buyer.ts` | Direct HTTP LLM buyer integration without SDK lock-in. |
| `sample_copyrescue_delivery.json` | Reviewable deterministic delivery artifact. |
| `DEVNET_RUNBOOK.md` | How to reproduce a live devnet settlement proof. |

## Review Artifacts

- Pitch deck: `CopyMarket_Agent_Economy_Pitch.pptx`
- Demo video: `CopyMarket_demo_video.avi` inside `CopyMarket_submission_package.zip`
- Demo preview: `CopyMarket_demo_preview.gif`
- Demo script: `demo_video_script.md`
- Submission notes: `SUBMISSION.md`
- Public submission package: `CopyMarket_submission_package.zip`

## Local Verification

Seller agent:

```sh
cd coral-agents/seller-agent
pnpm run typecheck
pnpm test
```

Verified result:

- typecheck passed
- 5 test files passed
- 16 tests passed

Buyer agent:

```sh
cd coral-agents/buyer-agent
tsc --noEmit
vitest run
```

Verified result:

- typecheck passed
- 2 test files passed
- 13 tests passed

Pitch deck:

```sh
slides_test.py CopyMarket_Agent_Economy_Pitch.pptx
```

Verified result:

- no slide overflow detected

## Quick Start

Install dependencies for the relevant agent packages, then run the seller and buyer tests above.

For a live escrow run, use `DEVNET_RUNBOOK.md`. The run needs:

- Node 20+
- a live Solana devnet RPC
- a funded buyer devnet wallet
- optional LLM key; the seller service has a deterministic fallback

## Submission

Superteam listing:

```text
Imperial AI Agent Hackathon: Build the Agent Economy
```

Public repo:

```text
https://github.com/leafwithered/copymarket-agent-economy
```

Contact:

```text
Telegram: http://t.me/hierachleafleaf
X: https://x.com/leafmyx
```

## Security Notes

This repo must not include private keys, `.env`, `WALLETS.txt`, or the Superteam agent API key. The
project is configured for devnet settlement only. Do not use a funded mainnet wallet.
