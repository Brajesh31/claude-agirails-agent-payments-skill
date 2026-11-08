# Wallet and Secret Handling Runbook

## Before setup
1. Decide whether a wallet is actually required for the chosen flow.
2. Begin in mock mode wherever possible.
3. Use a dedicated wallet for testnet and production activities.
4. Confirm the official SDK instructions and supported environment variables.

## Secret storage
- Store private keys, keystore passwords, and API credentials in a secrets manager or protected runtime environment.
- Never place real values in SKILL.md, README files, examples, source code, issue comments, or logs.
- Keep .env, keystore files, and exported secret material out of version control.
- Restrict access to the smallest set of people and workloads.
- Do not print environment variables to debug a configuration issue.

## Runtime controls
- Validate network, chain ID, token address, recipient, and amount before signing.
- Apply spending and transaction limits.
- Require explicit human approval for mainnet, high-value, or irreversible actions.
- Use dedicated test and production configurations.
- Alert on unexpected signing requests, state changes, or repeated failures.

## Rotation and incident response
1. Disable or revoke the affected credential where possible.
2. Rotate the key through the approved wallet process.
3. Review recent transactions and access logs.
4. Assess whether funds or other accounts are at risk.
5. Notify the appropriate security owner.
6. Record the incident and update controls.

## Release check
- [ ] No secrets are present in the repository.
- [ ] Runtime permissions are least-privilege.
- [ ] Network and recipient validation is implemented.
- [ ] Recovery and rotation steps are documented.
- [ ] Production release has a named approver.

Do not paste real secret values into this runbook.
