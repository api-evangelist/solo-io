# Solo.io

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
