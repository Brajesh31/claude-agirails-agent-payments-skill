# Wallet and Secret Handling Runbook

## Setup

1. Determine whether the selected workflow needs a wallet.
2. Use mock mode when exploring the integration.
3. Use separate wallets for test and production work.
4. Record the active network and wallet owner.
5. Follow the installed SDK's supported credential configuration.

## Credential storage

- Keep private keys, recovery phrases, keystore passwords, and API credentials in a secrets manager or protected runtime environment.
- Never place real credentials in skill files, documentation, examples, tickets, logs, or screenshots.
- Exclude environment files and wallet stores from version control.
- Limit secret access to the smallest number of services and operators.
- Do not print environment variables to diagnose a configuration problem.
- Rotate credentials when an operator leaves or exposure is suspected.

## Transaction controls

- Verify chain, token, recipient, amount, and fee before signing.
- Use a separate signer identity for each environment.
- Restrict the agent's spend and transaction permissions.
- Require a human approval step for mainnet and high-value transfers.
- Keep signing events and transaction identifiers in an auditable log.
- Alert on unexpected signing requests and repeated payment failures.

## Incident response

1. Pause the affected agent or signing workload.
2. Revoke or disable exposed credentials where possible.
3. Rotate the affected key through the approved wallet process.
4. Review recent transactions and access records.
5. Determine whether assets or connected accounts may be affected.
6. Notify the responsible security operator.
7. Record the incident and improve the control that failed.

## Release review

- [ ] No real credentials are present in the repository.
- [ ] Signing permissions are least-privilege.
- [ ] Spend limits are active.
- [ ] Network and recipient checks are enforced.
- [ ] Rotation and recovery owners are named.
- [ ] Production use has explicit approval.

Never paste a real secret into this document.