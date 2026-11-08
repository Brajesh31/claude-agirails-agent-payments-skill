# claude-agirails-agent-payments-skill

A Claude Code skill for integrating AI agents with payment workflows using escrow, instant payment, and settlement patterns.

## Overview

This skill guides agent payment onboarding and integration. It covers provider and requester roles, payment routing, escrow lifecycle, instant payment flows, pricing, disputes, and identity configuration.

Payment integrations require careful handling of credentials, state transitions, and irreversible operations. Follow the onboarding workflow and verify each step before enabling live transactions.

## Main Capabilities

- Onboard an agent to the payment workflow.
- Select provider or requester behavior.
- Configure payment adapters and routing.
- Work with escrow-based payment flows.
- Work with instant payment flows where supported.
- Understand settlement on the configured network.
- Manage pricing and payment metadata.
- Handle dispute and release workflows.
- Configure agent identity and key management.
- Verify setup before enabling real payments.

## Payment Workflow Concepts

### Provider

An agent that offers a service and receives payment after the required conditions are satisfied.

### Requester

An agent that requests a service and initiates payment according to the configured flow.

### Escrow

A payment state that holds funds until the agreed release conditions are met. State transitions and release operations must be handled carefully.

### Instant Payment

A direct payment flow for cases where escrow is not required and the supported payment protocol allows immediate settlement.

## Installation

The skill can be installed in the Claude Code skills directory:

```bash
git clone https://github.com/Brajesh31/claude-agirails-agent-payments-skill.git ~/.claude/skills/agirails-agent-payments
```

The payment SDK and network configuration are separate runtime requirements. Review the current onboarding instructions in `SKILL.md` before installing packages or configuring keys.

## Usage

Invoke the skill when integrating an agent with the payment system:

```text
/agirails-agent-payments
```

Provide the agent role, service or task description, pricing model, payment preference, settlement environment, and required identity configuration.

## Onboarding Workflow

1. Clarify the agent's role and payment use case.
2. Select the appropriate payment flow.
3. Define service pricing and settlement requirements.
4. Configure identity and credentials securely.
5. Generate integration code for the selected role.
6. Review state transitions and error handling.
7. Test using a safe non-production environment.
8. Verify payment status and settlement behavior.
9. Enable live use only after explicit confirmation.
10. Monitor transactions and handle disputes through the documented process.

## Security Checklist

- Private keys are never committed.
- Credentials are stored securely.
- Payment amounts and recipients are validated.
- Escrow state transitions are checked.
- Release operations require the correct conditions.
- Duplicate requests are handled safely.
- Network and chain configuration are verified.
- Transaction status is independently checked.
- Test and production environments are separated.

## Repository Contents

- `SKILL.md`: Main onboarding and payment integration instructions.
- `README.md`: Payment concepts, workflow, and security checklist.

## Important Note

This skill provides technical integration guidance, not financial or legal advice. Payment operations can be irreversible. Verify network details, transaction state, and permissions before moving real funds.
