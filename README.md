# claude-agirails-agent-payments-skill

A Claude Code skill for building safe payment workflows between AI agents using AGIRAILS.

## What it helps with

- Provider agents that offer paid services.
- Requester agents that purchase services.
- Combined agents that both provide and request work.
- ACTP escrow workflows for deliverables that need review.
- x402 payment flows for supported immediate HTTP interactions.
- Wallet configuration, network selection, transaction review, and operational safety.

## Install

~~~bash
git clone https://github.com/Brajesh31/claude-agirails-agent-payments-skill.git ~/.claude/skills/agirails-agent-payments
~~~

Restart Claude Code if the skill directory was created while the session was already running.

## Use

Invoke:

~~~text
/agirails-agent-payments
~~~

Describe the agent's role, service, target network, payment model, amount limits, and runtime environment. The skill will clarify missing details before proposing an implementation.

## Recommended workflow

1. Design and test in mock mode.
2. Validate the service contract and error handling.
3. Test on Base Sepolia with a dedicated test wallet.
4. Verify balances, transaction states, recipient, and settlement.
5. Require explicit approval before moving to Base mainnet.

Never share private keys or seed phrases in chat. Mainnet payments and escrow releases are consequential operations and require independent verification.

## Supporting materials

| File | Purpose |
|---|---|
| [Payment integration readiness checklist](resources/payment-integration-readiness-checklist.md) | Review roles, network, wallet, spending controls, and launch approval. |
| [Transaction state review template](resources/transaction-state-review-template.md) | Record transaction history, delivery evidence, dispute status, and settlement verification. |
| [Wallet and secret handling runbook](resources/wallet-and-secret-handling-runbook.md) | Store, restrict, rotate, and respond to credential exposure. |
| [Provider and requester examples](resources/provider-requester-examples.md) | Starter patterns for both sides of a service transaction. |
| [Payment failure recovery playbook](resources/payment-failure-recovery-playbook.md) | Classify failed or uncertain operations and recover without duplicate payments. |

## Scope

The skill provides engineering workflow guidance. It does not replace security review, financial controls, or review of the active network and protocol configuration.

## License

MIT. See the root [LICENSE](LICENSE).