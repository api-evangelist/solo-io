# Solo.io

Solo.io is a cloud-native application-networking company founded in 2017 that builds
enterprise and open-source API gateways, service mesh, and agentic-AI infrastructure —
Kgateway Enterprise (formerly Gloo Gateway), Solo Enterprise for Istio (formerly Gloo Mesh),
Agentgateway Enterprise, Kagent Enterprise, and Agentregistry Enterprise — plus the
kgateway, agentgateway, kagent, and Istio ambient-mesh open-source projects.

- Website: https://www.solo.io/
- Docs: https://docs.solo.io/
- GitHub: https://github.com/solo-io
- Pricing: https://www.solo.io/pricing
- Security: https://www.solo.io/security
- Trust center: https://trust.solo.io/

## APIs in this repo

| API | Spec | Operations |
|---|---|---|
| Gloo Portal Server API | `openapi/solo-io-portal-server-openapi.yml` | 28 |
| Gloo Portal Backend API | `openapi/solo-io-portal-backend-openapi.yml` | 39 |
| Gloo Platform Portal API | `openapi/solo-io-gloo-platform-portal-openapi.yml` | 7 |
| Gloo Portal IdP Connect API | `openapi/solo-io-portal-idp-connect-openapi.yml` | 2 |
| AI Gateway Guardrail Webhook API | `openapi/solo-io-ai-gateway-guardrail-webhook-openapi.yml` | 2 |

All five specs were harvested verbatim from the `solo-io` GitHub organization.

## Artifacts

`openapi/` `overlays/` `grpc/` `llms/` `packages/` `cli/` `mcp/` `skills/` `asyncapi/`
`authentication/` `conventions/` `errors/` `lifecycle/` `changelog/` `conformance/`
`data-model/` `security/` `well-known/`

Notable recorded absences (probed, not assumed): no `/.well-known/*` documents on any
Solo.io host, no A2A agent card, no AsyncAPI, no public status page, no idempotency or
pagination contract on the portal APIs.
