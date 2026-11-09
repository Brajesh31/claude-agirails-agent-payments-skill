# Payment Failure and Recovery Playbook

Use this playbook when a payment request fails, times out, or returns an uncertain result.

## First response

1. Stop automatic retries until the transaction status is known.
2. Capture the internal request ID, protocol transaction ID, network, timestamp, and error category.
3. Check the transaction on the configured network.
4. Determine whether funds moved, remain escrowed, were returned, or were never committed.
5. Do not create a replacement request until duplicate risk is resolved.

## Failure classes

| Failure | Safe response |
|---|---|
| Invalid input or service label | Correct the request and validate before resubmission. |
| Provider unavailable | Check provider status and transaction state before retrying. |
| Insufficient balance | Reconcile the wallet balance and approved budget. |
| Network timeout | Query the transaction state; do not assume the operation failed. |
| Duplicate request | Compare transaction IDs and idempotency keys; keep one canonical operation. |
| Delivery rejected | Preserve evidence and follow the configured dispute process. |
| Credential exposure | Pause signing, rotate credentials, and review activity. |
| Unexpected terminal state | Stop the agent and escalate to the payment operator. |

## Recovery record

- Incident ID:
- Related transaction:
- Network:
- Time discovered:
- Failure category:
- Funds movement confirmed:
- Current protocol state:
- Duplicate risk:
- Action taken:
- Approver:
- Follow-up owner:

## Restart criteria

Resume only after the transaction state is known, duplicate risk is eliminated, credentials are safe, and the responsible operator approves the next action. For unresolved settlement or dispute cases, escalate instead of improvising a manual transfer.