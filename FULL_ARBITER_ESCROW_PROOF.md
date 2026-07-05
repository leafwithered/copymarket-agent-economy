# Full Arbiter Escrow Proof

## Current Proof Status

The current public Solana devnet proof demonstrates a buyer-to-seller settlement smoke transfer.

It proves that CopyMarket can attach a verifiable Solana devnet transaction to the agent workflow, but it is not yet a full captured arbiter escrow lifecycle.

## Target Full Escrow Lifecycle

The intended full proof should capture:

1. Buyer creates or initializes escrow.
2. Buyer funds escrow or vault.
3. Seller verifies funded state before delivery.
4. Seller submits structured delivery artifact.
5. Arbiter releases funds to seller.
6. Optional timeout/refund path is tested.

## Proof Fields To Add

- Network: Solana devnet
- Escrow program:
- Arbiter program:
- Buyer wallet:
- Seller wallet:
- Arbiter wallet:
- Escrow PDA:
- Vault PDA:
- Order/reference ID:
- Init/open escrow transaction:
- Deposit/fund transaction:
- Release transaction:
- Refund transaction, if available:
- Delivery artifact: `sample_copyrescue_delivery.json`

Until these Explorer links are filled in, CopyMarket does not claim a complete public arbiter escrow lifecycle proof.
