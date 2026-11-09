# Payment Integration Readiness Checklist

Complete this review before enabling an AGIRAILS payment workflow. Use mock mode first, then a test network.

## Use case

- [ ] Provider, requester, or combined role is defined.
- [ ] Service labels are identical on both sides.
- [ ] Input and output schemas are documented.
- [ ] Pricing, budget, token, and currency units are explicit.
- [ ] ACTP escrow or x402 immediate settlement is selected for a clear reason.
- [ ] The team understands the protection and dispute limits of the selected flow.

## Environment and identity

- [ ] SDK and CLI versions are recorded.
- [ ] Network is explicitly configured.
- [ ] Base Sepolia is selected for testnet work.
- [ ] Base mainnet is selected only for approved production use.
- [ ] Wallet ownership and signing permissions are confirmed.
- [ ] Credentials are stored outside the repository.
- [ ] Local keystores and environment files are excluded from version control.
- [ ] Logs and diagnostics contain no private credentials.

## Transaction controls

- [ ] Recipient and network are checked before signing.
- [ ] Amount, token decimals, and fee estimate are validated.
- [ ] Duplicate submissions are detected.
- [ ] Retries check transaction status before submitting again.
- [ ] Spending caps are configured.
- [ ] Escrow delivery and dispute handling are understood.
- [ ] Irreversible actions require a named approver.

## Test plan

- [ ] Mock success path passes.
- [ ] Invalid payload is rejected.
- [ ] Missing service handler is handled.
- [ ] Insufficient balance is handled.
- [ ] Timeout and retry behavior is tested.
- [ ] Duplicate request does not create an unintended second payment.
- [ ] Cancellation and dispute paths are tested where applicable.
- [ ] Testnet transaction and final state are independently checked.

## Production decision

- Responsible owner:
- Reviewer:
- Network:
- Maximum transaction amount:
- Aggregate spending limit:
- Monitoring and pause procedure:
- Known gaps:
- Approval reference:
- Decision: Approved / Limited test / Blocked