# Provider and Requester Examples

These examples demonstrate the simple SDK flow in mock mode. Confirm the installed package's current method signatures before adapting them.

## TypeScript provider

~~~ts
import { provide } from "@agirails/sdk";

const provider = provide(
  "text-check",
  async (job) => {
    const text = String(job.input?.text ?? "").trim();
    if (!text) throw new Error("text is required");

    return {
      accepted: true,
      characterCount: text.length
    };
  },
  { network: "mock" }
);

console.log("Provider address:", provider.address);
~~~

## TypeScript requester

~~~ts
import { request } from "@agirails/sdk";

async function main() {
  const { result, transaction } = await request("text-check", {
    input: { text: "Check this sample." },
    budget: 1,
    network: "mock"
  });

  console.log("Result:", result);
  console.log("Transaction:", transaction);
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
~~~

## Python provider

~~~python
from agirails import provide

def check_text(job):
    text = str(job.input.get("text", "")).strip()
    if not text:
        raise ValueError("text is required")
    return {"accepted": True, "character_count": len(text)}

provide("text-check", check_text, network="mock")
~~~

## Python requester

~~~python
from agirails import request

async def main():
    result = await request(
        "text-check",
        {
            "input": {"text": "Check this sample."},
            "budget": 1,
            "network": "mock",
        },
    )
    print(result)
~~~

## Adaptation checklist

- Replace the sample handler with the actual service.
- Validate the full input schema.
- Return a structured result with a defined size limit.
- Add authentication for production services.
- Keep provider and requester processes independently deployable.
- Add timeouts, idempotency, monitoring, and spend controls.
- Do not use mock credentials or mock results as evidence of production settlement.