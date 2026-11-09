# Transaction State Review

Use this template to inspect a transaction. Completing this record does not authorize a payment, cancellation, or release.

## Transaction details

- Internal reference:
- Protocol transaction ID:
- Network:
- Requester:
- Provider:
- Service:
- Amount and token:
- Created time:

## State history

| Time | Previous state | New state | Transaction hash or evidence | Reviewer |
|---|---|---|---|---|
| | | | | |

## Delivery assessment

- Expected deliverable:
- Delivered result:
- Acceptance criteria:
- Gaps or defects:
- Applicable review deadline:
- Decision: Accepted / Rejected / Pending

## Settlement assessment

- Current state checked independently:
- Escrow involved:
- Settlement action required:
- Authorized operator:
- Settlement transaction hash:
- Final recipient and amount:
- Dispute or cancellation notes:

## Review outcome

- Status: In progress / Delivered / Disputed / Settled / Cancelled
- Follow-up action:
- Responsible owner:
- Review date:

**Control:** Never infer settlement from a success message alone. Verify the final state on the correct network. Require separate approval before an irreversible action.