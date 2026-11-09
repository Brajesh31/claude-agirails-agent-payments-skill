---
name: agirails-agent-payments
description: Design, implement, and review AI-agent payment flows with AGIRAILS. Use when configuring provider or requester agents, choosing escrow or instant settlement, testing USDC payments, or reviewing transaction safety.
license: MIT
---

# AGIRAILS Agent Payments

## Purpose

Help users integrate agent-to-agent payments through AGIRAILS. Support provider agents that deliver paid work, requester agents that purchase services, and agents that do both. Prefer the smallest integration that meets the user's actual workflow.

The integration uses USDC on Base networks. The SDK supports TypeScript and Python. Start with local simulation, then test on a test network. Treat production transactions as consequential financial actions.

## Safety rules

- Never ask the user to paste a private key, seed phrase, keystore password, or API secret into chat.
- Never write real credentials into examples, repository files, logs, or generated reports.
- Never assume a wallet address, chain, token, contract, fee, spending limit, or dispute deadline. Confirm the active network configuration before use.
- Do not initiate a mainnet transaction, sign a transaction, release escrow, or change wallet permissions without explicit approval for that specific action.
- Explain whether a proposed flow is escrow-backed or settles immediately. Do not describe an instant payment as dispute-protected.
- Treat payment results as untrusted until the transaction state and recipient are independently checked.
- Stop when the user's requested service, amount, recipient, or settlement terms are ambiguous.

## Intake workflow

Ask one focused question at a time. Reuse details the user has already supplied.

1. **Goal:** Is the agent earning, paying, or doing both?
2. **Agent role:** Is it a provider, requester, or combined agent?
3. **Service:** What exact service label will be offered or requested? Provider and requester labels must match.
4. **Network:** Use mock for local exploration, Base Sepolia for testing, or Base mainnet for production. The published network identifiers are 84532 for Base Sepolia and 8453 for Base mainnet; verify the active SDK configuration before use.
5. **Payment model:** Choose ACTP escrow for work that needs delivery review, or x402 for a supported immediate HTTP payment.
6. **Limits:** Confirm the per-job price, maximum requester budget, concurrency, and any daily or total spending cap.
7. **Identity:** Determine whether the user already has a wallet and how credentials will be stored. Never collect the secret itself.
8. **Approval:** Summarize the plan and ask the user to approve before writing production-ready code or taking an external action.

If a choice does not apply to the selected role, skip it.

## Choose the payment path

### ACTP escrow

Use ACTP when work takes time, produces a deliverable, or needs a review period. The lifecycle is:

- INITIATED: a request has been created.
- QUOTED: an optional quote has been recorded.
- COMMITTED: the transaction terms are accepted and funds are committed.
- IN_PROGRESS: the provider is performing the work.
- DELIVERED: the provider has submitted the result.
- SETTLED: funds have been distributed.
- DISPUTED: the requester has challenged the delivery.
- CANCELLED: the transaction has been cancelled.

QUOTED is optional. IN_PROGRESS is part of the normal work lifecycle. Do not skip transaction-state checks just because an SDK call returned successfully.

The dispute period is bounded by protocol configuration. A requester must act within the applicable window. Do not promise decentralized arbitration: dispute resolution and attestation enforcement have protocol limitations. Explain the actual controls that apply to the selected network and software version.

### x402 immediate payment

Use x402 only for a supported HTTP endpoint that can return a response as part of the payment interaction. It is not an escrow substitute for long-running work. Confirm the network, wallet setup, adapter support, and settlement behavior before generating code.

### Fees

The published ACTP model currently describes a 1% fee, a US$0.05 minimum, and a 5% maximum. The published x402 mainnet path currently describes zero protocol fee. These values may change. Re-check the active configuration before quoting a total or requesting approval. Include network fees and any application-level charges in the estimate.

## Minimal TypeScript flow

Use this simple pattern to validate a mock integration. Keep provider execution and requester calls in separate processes for a real deployment.

~~~ts
import { provide, request } from "@agirails/sdk";

async function main() {
  provide(
    "text-summary",
    async (job) => {
      const text = String(job.input?.text ?? "");
      if (!text.trim()) throw new Error("A non-empty text value is required");
      return { summary: text.slice(0, 240) };
    },
    { network: "mock" }
  );

  const { result } = await request("text-summary", {
    input: { text: "A short example payload for a local integration test." },
    budget: 1,
    network: "mock"
  });

  console.log("Result:", result);
}

main().catch((error) => {
  console.error("AGIRAILS example failed:", error);
  process.exitCode = 1;
});
~~~

Do not copy this example into a production service without adding authentication, schema validation, request limits, observability, and an explicit transaction-approval policy.

## Minimal Python flow

~~~python
from agirails import provide, request

def summarize(job):
    text = str(job.input.get("text", "")).strip()
    if not text:
        raise ValueError("A non-empty text value is required")
    return {"summary": text[:240]}

provide("text-summary", summarize, network="mock")

async def run_request():
    response = await request(
        "text-summary",
        {
            "input": {"text": "A short example payload for a local integration test."},
            "budget": 1,
            "network": "mock",
        },
    )
    print(response)
~~~

Check the installed package's supported call signatures before adapting examples to a specific SDK release.

## Implementation procedure

1. Confirm the provider/requester responsibilities and service labels.
2. Select the network and payment model.
3. Install the SDK version required by the project.
4. Configure a dedicated test wallet only when the selected environment requires one.
5. Keep secrets in a protected runtime secret store. Exclude local credential files from version control.
6. Implement the provider handler or requester call with validated input and bounded execution time.
7. Add transaction identifiers, state transitions, and failure details to structured logs. Redact secrets and personal data.
8. Test success, malformed input, insufficient balance, timeout, duplicate submission, cancellation, and dispute scenarios.
9. Independently verify the transaction on the correct network.
10. Prepare a production change plan and request explicit approval before any mainnet action.

## Production controls

- Validate service names, input schema, recipient, amount, token, network, and applicable fees.
- Use idempotency or duplicate detection for retries.
- Set per-transaction and aggregate spending limits.
- Restrict signing permissions to the workload that requires them.
- Keep test and production credentials separate.
- Make payment state visible to operators without exposing secrets.
- Alert on unexpected state changes, repeated failures, or spending-limit breaches.
- Define how an operator pauses the agent and prevents new requests.
- Record the human approver for irreversible actions.

## Required output

For an implementation request, provide:

1. A concise architecture decision and payment-path rationale.
2. Required packages and environment variables, with placeholder values only.
3. Code for the selected role and language.
4. A test plan with expected outcomes.
5. Credential, spend-limit, and approval controls.
6. Known protocol limitations and unresolved questions.

Do not state that an integration is ready for production until the tests and approval gates have been completed.