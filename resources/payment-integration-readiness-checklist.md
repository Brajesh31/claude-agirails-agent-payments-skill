# Agent Payment Integration Readiness Checklist

Use this before enabling an AGIRAILS payment flow. Start with mock mode, then a test network. This checklist is not financial, legal, or security advice.

## Use case and roles
- [ ] Provider, requester, or both roles are defined.
- [ ] Service names match exactly on both sides.
- [ ] Pricing, budget, currency, and settlement expectations are documented.
- [ ] ACTP escrow versus x402 instant payment has been selected for a reason.
- [ ] The user understands that x402 is not an escrow or dispute-protected flow.

## Environment and identity
- [ ] SDK and CLI versions are recorded.
- [ ] Mock/testnet/mainnet mode is explicit.
- [ ] Chain/network identifiers are verified from current official documentation.
- [ ] Wallet ownership and required permissions are confirmed.
- [ ] Private keys and passwords are stored outside source control.
- [ ] .env, keystore, and secret files are ignored by Git.
- [ ] No secret values appear in logs, screenshots, or committed examples.

## Transaction safety
- [ ] Recipient address is independently checked.
- [ ] Amount, token, decimals, network, and fee are validated before signing.
- [ ] Duplicate requests and retries are idempotent or safely detected.
- [ ] Transaction IDs and state transitions are recorded.
- [ ] Escrow release is performed only after delivery is verified.
- [ ] Cancellation and dispute paths are understood.
- [ ] Mainnet operations require explicit human approval.

## Test plan
- [ ] Run end-to-end tests in mock mode.
- [ ] Test invalid recipient, insufficient funds, timeout, and duplicate request cases.
- [ ] Verify actual on-chain state independently on testnet.
- [ ] Confirm recovery steps before production.
- [ ] Review current contract, SDK, and network documentation before relying on any address or limit.

## Go-live decision
- Owner:
- Reviewer:
- Environment:
- Approved amount and limits:
- Outstanding risks:
- Explicit approval reference:
