# CopyMarket

CopyMarket proves that AI agents can discover work, bid, transact, deliver structured output, and settle payment through Solana-backed escrow logic.

The demo market lets a buyer agent purchase a landing-page copy rescue from a seller agent. The buyer broadcasts a `WANT`, sellers compete with `BID`s, the buyer awards the best value, escrow funding is required before delivery, and settlement/release is tied to the delivered artifact.

```text
WANT -> BID -> AWARD -> ESCROW_REQUIRED -> DEPOSITED -> DELIVERED -> RELEASED
```

This is not a chatbot demo. It is a small agent-to-agent paid service market: agents sell useful work, negotiate terms, gate delivery on payment, and leave public verification artifacts for reviewers.

## Judge Quick Review

| Question | Answer |
| --- | --- |
| What is it? | An agent-to-agent service market for paid digital work. |
| Why is it Agent Economy? | Buyer agents define demand, seller agents compete, the winner delivers structured output, and payment is conditional on settlement state. |
| What does Solana do? | Solana devnet is the settlement/proof rail for escrow-style payment state and reviewer-visible transfer proof. |
| What can a judge verify quickly? | Code, tests, sample delivery JSON, devnet Explorer proofs, runbook, GitHub Pages demo, and the grant response. |
| What is honest scope? | Devnet only. The public Explorer proof includes a live buyer-to-seller smoke transfer; production-grade hardening is not claimed. |

## Agent Market State Machine

```text
WANT -> BID -> AWARD -> ESCROW_REQUIRED -> DEPOSITED -> DELIVERED -> RELEASED
                         \
                          -> TIMEOUT_OR_DISPUTE -> REFUND_PATH
```

Buyer responsibilities:

- publish the job, budget, and selection criteria
- collect bids and award the best seller
- deposit funds before expecting delivery
- release on valid delivery or use the refund path when the order expires

Seller responsibilities:

- bid with a price and service promise
- return `ESCROW_REQUIRED` terms before delivery
- verify funded escrow state before sending the final artifact
- deliver structured JSON another agent can consume

Arbiter/settlement responsibilities:

- bind the awarded seller to the payout wallet
- prevent delivery-before-payment behavior
- support release after delivery
- keep timeout/refund behavior explicit instead of hidden in chat text

## What Is Implemented vs. What Is Proven

Implemented in the repo:

- TypeScript buyer and seller agents for the market loop
- `copyrescue` seller service with deterministic fallback output
- escrow and arbiter-aware buyer/seller code paths for Solana devnet
- guard tests for payout binding and devnet settlement assumptions
- sample machine-readable delivery output
- reviewer page with an interactive state-machine demo

Public proof today:

- devnet funding proof for the buyer wallet
- finalized devnet buyer-to-seller smoke transfer
- local test record: 29 passing tests across buyer and seller packages
- sample `copyrescue` delivery artifact

Honest limitation:

The current public Explorer proof is a smoke settlement transfer, not a full captured arbiter escrow lifecycle. The code and runbook describe the escrow/arbiter path, and the next strongest proof target is a public transaction set for deposit, delivery, release, timeout, and refund. Real mainnet funds are out of scope.

## What The Agent Sells

The first service is `copyrescue`: a compact, structured landing-page rewrite that another agent can consume without scraping a chat transcript.

Each delivery includes:

- hero headline, subheadline, and CTA
- three section rewrites
- conversion notes
- compliance and risk controls
- deterministic fallback output when no LLM key is available

Example output is in `sample_copyrescue_delivery.json`.

## copyrescue Is The First Service, Not The Ceiling

`copyrescue` is deliberately small because it makes the market easy to judge: the buyer request, bid, escrow requirement, delivery JSON, and payment proof fit in one review flow.

The same protocol shape can support other agent services:

- research agents selling sourced market briefs
- code-review agents selling patch-risk reports
- compliance agents selling policy checks
- data-cleaning agents selling normalized CSV/JSON outputs
- design agents selling structured landing-page variants

In every case the service changes, but the commerce loop stays the same: demand, bid, award, escrow, delivery, release, refund path.

## Main Changed Files

| Path | Why it matters |
| --- | --- |
| `docs/index.html` | Public reviewer page with quick review, state machine, demo, and verification links. |
| `AGENTIC_ENGINEERING_GRANT_RESPONSE.md` | Grant response text used to explain the project to Superteam reviewers. |
| `coral-agents/buyer-agent/src/index.ts` | Buyer market loop: WANT, bid collection, award, deposit, delivery wait, release. |
| `coral-agents/buyer-agent/src/arbiter.ts` | Arbiter wrapper for release/refund authority. |
| `coral-agents/buyer-agent/src/guard.ts` | Payout binding guard so the awarded seller matches escrow payout. |
| `coral-agents/seller-agent/src/index.ts` | Seller loop: bid, require escrow, verify funding, deliver. |
| `coral-agents/seller-agent/src/service.ts` | `copyrescue` artifact generation and deterministic fallback. |
| `sample_copyrescue_delivery.json` | Machine-readable delivery example. |
| `DEVNET_RUNBOOK.md` | Steps for reproducing a live devnet run. |
| `DEVNET_PAYMENT_PROOF.json` | Public smoke payment proof metadata. |

## What To Verify

Start with the reviewer page:

```text
https://leafwithered.github.io/copymarket-agent-economy/
```

Then inspect these repo artifacts:

- Buyer agent: `coral-agents/buyer-agent/src/index.ts`
- Seller agent: `coral-agents/seller-agent/src/index.ts`
- Arbiter wrapper: `coral-agents/buyer-agent/src/arbiter.ts`
- Delivery example: `sample_copyrescue_delivery.json`
- Devnet runbook: `DEVNET_RUNBOOK.md`
- Smoke payment proof: `DEVNET_PAYMENT_PROOF.json`
- Grant response: `AGENTIC_ENGINEERING_GRANT_RESPONSE.md`
- Submission package: `CopyMarket_submission_package.zip`

External proof links:

```text
Funding proof:
https://explorer.solana.com/tx/4CMqLmrU6zLTaCFse1NP6F4WTeDjj1hbFcRagV8T8rNEQ8ZBziieaE2W8khwRree3iVnjrUTTBkyC497u6vAUoBe?cluster=devnet

Buyer-to-seller smoke transfer:
https://explorer.solana.com/tx/49V7wedjpa66Rzk87qhCzjshWVx4uw2zhBL4WhKzN7kTEfshickWW9dcwbUS11adb33LkhEFEiE9hFdQbcV1s7zo?cluster=devnet

Public X launch thread:
https://x.com/leafmyx/status/2072747881883369696
```

## Review Artifacts

- Pitch deck: `CopyMarket_Agent_Economy_Pitch.pptx`
- Demo video: `CopyMarket_demo_video.avi` inside `CopyMarket_submission_package.zip`
- Demo preview: `CopyMarket_demo_preview.gif`
- Demo script: `demo_video_script.md`
- Submission notes: `SUBMISSION.md`
- Public submission package: `CopyMarket_submission_package.zip`
- Devnet airdrop proof: `devnet_airdrop_proof.json`
- Devnet buyer-to-seller payment proof: `DEVNET_PAYMENT_PROOF.json`

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
- a live Solana devnet RPC, verified with `https://api.devnet.solana.com`
- a funded buyer devnet wallet
- optional LLM key; the seller service has a deterministic fallback

## Submission Links

Superteam listing:

```text
Imperial AI Agent Hackathon: Build the Agent Economy
```

Public repo:

```text
https://github.com/leafwithered/copymarket-agent-economy
```

Reviewer page source:

```text
https://github.com/leafwithered/copymarket-agent-economy/blob/main/docs/index.html
```

GitHub Pages:

```text
https://leafwithered.github.io/copymarket-agent-economy/
```

Contact:

```text
Telegram: http://t.me/hierachleafleaf
X: https://x.com/leafmyx
```

## Security Notes

This repo must not include private keys, `.env`, `WALLETS.txt`, or the Superteam agent API key. The project is configured for devnet settlement only. Do not use a funded mainnet wallet.
