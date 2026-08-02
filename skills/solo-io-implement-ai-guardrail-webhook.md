---
name: solo-io-implement-ai-guardrail-webhook
description: Implement the Solo.io AI gateway guardrail webhook — the two endpoints
  agentgateway/kgateway call to inspect an LLM prompt on the way out and an LLM response on
  the way back, returning a pass, mask, or reject action.
api: openapi/solo-io-ai-gateway-guardrail-webhook-openapi.yml
operations:
  - process_prompts_request_post
  - process_responses_response_post
generated: '2026-08-02'
method: generated
source: openapi/solo-io-ai-gateway-guardrail-webhook-openapi.yml
---

# Implement the Solo.io AI guardrail webhook

This contract inverts the usual direction: **you** implement the server, and the Solo.io
gateway (kgateway, Agentgateway Enterprise, or Gloo Gateway) is the client. The spec is
`openapi/solo-io-ai-gateway-guardrail-webhook-openapi.yml` (OpenAPI 3.1.0, GuardRail Webhook
API 0.1.0). Docs: https://docs.solo.io/agentgateway/2.3.x/llm/guardrails/webhook/

## The two endpoints

1. `process_prompts_request_post` — `POST /request`
   Receives a `GuardrailsPromptRequest` (normalized `PromptMessages` / `Message` list, so
   the same shape arrives regardless of which LLM provider is behind the gateway).
   Returns a `GuardrailsPromptResponse` carrying one action.
2. `process_responses_response_post` — `POST /response`
   Receives a `GuardrailsResponseRequest` (`ResponseChoices` / `ResponseChoice`) and returns
   a `GuardrailsResponseResponse` carrying one action.

## The three actions

- `PassAction` — let the content through unchanged.
- `MaskAction` — return modified content with sensitive spans masked. The gateway forwards
  your rewritten body, so the mask must be complete; do not rely on the gateway to redact.
- `RejectAction` — block the content and return an error response to the caller.

## Rules

- **Only two response codes are declared:** `200` for a valid action and `422` for a
  validation error (`HTTPValidationError` / `ValidationError`). Do not invent other statuses —
  the gateway's failure handling is configured on its side, not signalled by new codes.
- The request bodies are **normalized** across providers. Write against the schemas in the
  spec, not against OpenAI/Anthropic/Bedrock wire formats.
- There is **no security scheme in the spec**. Authentication between the gateway and your
  webhook is deployment configuration (mTLS, network policy, a shared header) — decide it
  explicitly rather than assuming the endpoint is safe to expose.
- The webhook is on the request path of every LLM call routed through the gateway. Keep it
  fast and fail-closed or fail-open deliberately; there is no retry semantics in the contract.
- No idempotency key is declared, and none is meaningful here: each call is a fresh inspection
  of one prompt or one response.
