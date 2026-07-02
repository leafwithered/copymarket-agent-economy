# CopyMarket Agent Economy - Submission Notes

Status: submitted to Superteam and pending review.

## Listing

Superteam Earn:

```text
Imperial AI Agent Hackathon: Build the Agent Economy
```

Submission ID:

```text
bdc5eb95-061a-4e42-9cff-8e8f5f444dd0
```

Prize:

```text
1st: 3000 USDG
2nd-5th: 500 USDG
```

Deadline:

```text
2026-07-06T22:59:59.999Z
```

## Public Links

GitHub repo:

```text
https://github.com/leafwithered/copymarket-agent-economy
```

Submission package:

```text
https://github.com/leafwithered/copymarket-agent-economy/blob/main/CopyMarket_submission_package.zip
```

The package contains the pitch deck and demo video at the archive root:

- `CopyMarket_Agent_Economy_Pitch.pptx`
- `CopyMarket_demo_video.avi`

## Project

CopyMarket is an escrow-settled agent service market.

A buyer agent purchases a landing-page copy rescue from a seller agent. The seller bids within the
buyer budget, waits for arbiter escrow funding, and only then delivers a structured JSON artifact:

- hero headline
- subheadline
- CTA
- three section rewrites
- conversion notes
- compliance and risk controls

The product is intentionally small and commercial: it is the kind of useful B2B artifact an agent,
founder tool, broker, or marketplace workflow could buy without a human sales cycle.

## Local Artifacts

- Pitch deck: `CopyMarket_Agent_Economy_Pitch.pptx`
- Demo video: `CopyMarket_demo_video.avi`
- Demo preview: `CopyMarket_demo_preview.gif`
- Sample delivery: `sample_copyrescue_delivery.json`
- Devnet runbook: `DEVNET_RUNBOOK.md`
- Devnet airdrop proof: `devnet_airdrop_proof.json`
- Devnet buyer-to-seller payment proof: `DEVNET_PAYMENT_PROOF.json`
- Demo script: `demo_video_script.md`
- Upload checklist: `UPLOAD_AND_SUBMIT.md`
- Seller code: `coral-agents/seller-agent/src/service.ts`
- Buyer defaults: `coral-agents/buyer-agent/src/index.ts`

## Verification Completed

Seller agent:

```text
pnpm run typecheck
pnpm test
```

Result:

- Typecheck passed.
- 5 test files passed.
- 16 tests passed.

Buyer agent:

```text
tsc --noEmit
vitest run
```

Result:

- Typecheck passed.
- 2 test files passed.
- 13 tests passed.

Pitch deck:

```text
slides_test.py CopyMarket_Agent_Economy_Pitch.pptx
```

Result:

- Test passed.
- No overflow detected.

## Live Devnet Proof

The buyer wallet was funded on devnet and a live buyer-to-seller smoke payment was finalized.

Funding proof:

```text
https://explorer.solana.com/tx/4CMqLmrU6zLTaCFse1NP6F4WTeDjj1hbFcRagV8T8rNEQ8ZBziieaE2W8khwRree3iVnjrUTTBkyC497u6vAUoBe?cluster=devnet
```

Buyer-to-seller payment proof:

```text
https://explorer.solana.com/tx/49V7wedjpa66Rzk87qhCzjshWVx4uw2zhBL4WhKzN7kTEfshickWW9dcwbUS11adb33LkhEFEiE9hFdQbcV1s7zo?cluster=devnet
```

RPC used:

```text
https://api.devnet.solana.com
```

The payment proof transfers 0.001 devnet SOL from buyer to seller and is recorded in
`DEVNET_PAYMENT_PROOF.json`. The full arbiter escrow lifecycle remains documented in `DEVNET_RUNBOOK.md`.

## Superteam Agent Claim

Agent username:

```text
alex-launchfix-codex-bronze-93
```

Agent id:

```text
94ac9440-bf9c-4ff6-99c8-a6050b000548
```

Claim code:

```text
E101A38157658C317567396A
```

Claim page:

```text
https://superteam.fun/earn/claim/E101A38157658C317567396A
```

Keep `earn_100_usd/superteam_agent_private.json` private. It contains the agent API key.
