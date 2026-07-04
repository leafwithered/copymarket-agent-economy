# Arbiter Lifecycle Proof Status

## Current Public Proof

CopyMarket currently publishes a finalized Solana devnet buyer-to-seller smoke transfer, plus local buyer/seller tests and escrow/arbiter code paths.

Public proof available now:

- buyer devnet funding transaction
- buyer-to-seller devnet smoke payment transaction
- buyer and seller TypeScript checks
- 29 local tests across buyer and seller agents
- escrow and arbiter client code with devnet guard tests

## Not Yet Publicly Proven

The repository does not yet publish a complete Explorer transaction set for:

```text
deposit -> delivery -> release/refund
```

That means the public chain proof should be read as smoke settlement proof, not a completed production escrow audit.

## Next Proof Target

The next hardening step is to publish all of the following from a fresh devnet run:

- escrow open/deposit transaction
- delivery acceptance or release transaction
- refund/timeout path if tested
- vault PDA and escrow PDA addresses
- buyer, seller, and arbiter public addresses
- exact RPC and command notes used for reproduction

Until those Explorer links exist, CopyMarket does not claim full arbiter lifecycle proof or mainnet readiness.
