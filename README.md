# CopyMarket Agent Economy

CopyMarket is an escrow-settled agent service market for paid B2B growth work. This fork adapts the Solana CoralOS "agent economy" starter kit into a concrete commercial workflow: a buyer agent purchases a landing-page copy rescue from a seller agent, with delivery gated by devnet escrow settlement.

## What It Does

The buyer agent broadcasts a WANT for the `copyrescue` service, evaluates seller bids, awards the best-value seller, opens arbiter-gated devnet escrow, and waits for delivery.

The seller agent only delivers after escrow funding is verified. The sold artifact is intentionally practical: a hero rewrite, CTA, three offer-section rewrites, conversion notes, and compliance-aware risk controls.

## Why This Fits The Agent Economy

Most agent demos stop at chat. CopyMarket shows an agent-to-agent service transaction with:

- a real service SKU: `copyrescue`
- buyer/seller negotiation
- escrow-first settlement logic
- structured JSON delivery that another agent can consume
- fallback deterministic output when no LLM key is configured
- compliance controls for crypto, fintech, SaaS, and cross-border businesses

## Main Changed Areas

- `coral-agents/seller-agent/src/service.ts`: CopyMarket delivery logic and LLM/deterministic normalization.
- `coral-agents/seller-agent/src/bidder.ts`: seller defaults moved from TxODDS to `copyrescue`.
- `coral-agents/buyer-agent/src/index.ts`: buyer defaults request a copy rescue.
- `coral-agents/buyer-agent/src/llm_buyer.ts`: Anthropic integration switched to direct HTTP to reduce dependency friction.
- `SUBMISSION.md`: Superteam submission notes and verification results.

## Example Delivery Shape

```json
{
  "service": "copyrescue",
  "request": "crypto wallet landing page needs a clearer hero and trust path",
  "audience": "crypto",
  "currentIssue": "The first screen asks visitors to decode the product before they see the outcome, proof, and next step.",
  "hero": {
    "headline": "Turn crypto visitors into qualified actions faster",
    "subheadline": "Clarify the offer, remove trust friction, and show exactly what happens after the first click.",
    "cta": "Get the 48h copy rescue"
  },
  "sections": [
    { "title": "Outcome first", "copy": "Lead with the result visitors can understand in five seconds." },
    { "title": "Trust path", "copy": "Explain user control, safety, and proof before asking for action." },
    { "title": "Action flow", "copy": "Use one primary CTA and expectation-setting copy beside it." }
  ],
  "conversionNotes": [
    "Move the strongest proof above the first scroll.",
    "Replace abstract category language with a concrete user action.",
    "Put risk-reducing copy next to the primary CTA."
  ],
  "riskControls": [
    "No guaranteed revenue, ranking, token-price, or investment claims.",
    "Keep compliance-sensitive wording factual and verifiable.",
    "Use user-control language around wallets, payments, or personal data."
  ]
}
```

## Local Verification Completed

Seller agent:

```text
pnpm run typecheck
pnpm test
```

Result: typecheck passed; 5 test files and 16 tests passed.

Buyer agent:

```text
tsc --noEmit
vitest run
```

Result: typecheck passed; 2 test files and 13 tests passed.

Pitch deck QA: overflow check passed.

## Submission Assets

Prepared locally for the Imperial AI Agent Hackathon: Build the Agent Economy.

- Pitch deck: `CopyMarket_Agent_Economy_Pitch.pptx`
- Demo video: `CopyMarket_demo_video.avi`
- Demo preview: `CopyMarket_demo_preview.gif`
- Sample delivery: `sample_copyrescue_delivery.json`
- Final submission text: `SUPERTEAM_FINAL_SUBMISSION_TEXT.md`

## Contact

Telegram: http://t.me/hierachleafleaf
