# Solo.io

Cloud-native API management and service connectivity to automate security, observability, resiliency, and traffic control for any API or workload in any environment.

**URL:** [https://raw.githubusercontent.com/api-evangelist/solo-io/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/solo-io/refs/heads/main/apis.yml)

## Scope

- **Type:** Contract
- **Position:** Consuming
- **Access:** 3rd-Party

## Tags

AI Gateway, Analytics, Automation, Gateways, Management, Monetization, Observability, Platform, Resiliency, Security, Service Mesh, Traffic Control

## APIs

### Gloo Portal Server API

REST endpoints to manage user access to the Gloo developer portal and API resources. Enables API key management, usage plan discovery, and API catalog browsing.

- **Documentation:** [https://docs.solo.io/gloo-mesh-gateway/latest/portal/openapi/](https://docs.solo.io/gloo-mesh-gateway/latest/portal/openapi/)
- **OpenAPI:** [openapi/solo-io-gloo-portal-server-api-openapi.yml](openapi/solo-io-gloo-portal-server-api-openapi.yml)

**Operations:** Get Current User, List Available Apis, Get Api Details, Get Api Schema, List Usage Plans, List Api Keys, Create Api Key, Delete Api Key, Login To Developer Portal, Logout From Developer Portal

### Gloo Gateway Management API

Administrative REST endpoints for managing Gloo Gateway deployments built on Envoy Proxy. Manages upstreams, virtual services, route tables, proxies, and gateways.

- **Documentation:** [https://docs.solo.io/gloo-edge/latest/reference/api/](https://docs.solo.io/gloo-edge/latest/reference/api/)
- **OpenAPI:** [openapi/solo-io-gloo-gateway-management-api-openapi.yml](openapi/solo-io-gloo-gateway-management-api-openapi.yml)

**Operations:** List Upstreams, Get Upstream Details, List Virtual Services, Get Virtual Service Details, List Proxies, Get Proxy Details, List Route Tables, Get Route Table Details, List Gateways, Get Gateway Details, Health Check

## Artifacts

### JSON Schemas

- [json-schema/user.json](json-schema/user.json)
- [json-schema/api-product.json](json-schema/api-product.json)
- [json-schema/api-version.json](json-schema/api-version.json)
- [json-schema/usage-plan.json](json-schema/usage-plan.json)
- [json-schema/api-key.json](json-schema/api-key.json)
- [json-schema/upstream.json](json-schema/upstream.json)
- [json-schema/virtual-service.json](json-schema/virtual-service.json)
- [json-schema/route.json](json-schema/route.json)
- [json-schema/route-table.json](json-schema/route-table.json)
- [json-schema/gateway.json](json-schema/gateway.json)
- [json-schema/proxy.json](json-schema/proxy.json)
- [json-schema/resource-metadata.json](json-schema/resource-metadata.json)
- [json-schema/resource-status.json](json-schema/resource-status.json)

### JSON Structures

- [json-structure/gloo-portal-structure.json](json-structure/gloo-portal-structure.json) — Portal API resource structures
- [json-structure/gloo-gateway-management-structure.json](json-structure/gloo-gateway-management-structure.json) — Gateway Management API resource structures

### JSON-LD

- [json-ld/solo-io-context.jsonld](json-ld/solo-io-context.jsonld) — Linked data context for Solo.io resources

### Spectral Rules

- [rules/solo-io-rules.yml](rules/solo-io-rules.yml) — API governance rules for Solo.io OpenAPI specs

### Naftiko Capabilities

| Capability | Description |
|---|---|
| [capabilities/gateway-operations.yaml](capabilities/gateway-operations.yaml) | Unified workflow: Gateway Management + Portal APIs (17 tools) |
| [capabilities/shared/gloo-portal.yaml](capabilities/shared/gloo-portal.yaml) | Shared: Gloo Portal Server API (8 tools) |
| [capabilities/shared/gloo-gateway-management.yaml](capabilities/shared/gloo-gateway-management.yaml) | Shared: Gloo Gateway Management API (11 tools) |

### Examples

- [examples/gloo-portal-list-apis-example.json](examples/gloo-portal-list-apis-example.json) — List available APIs response
- [examples/gloo-portal-create-api-key-example.json](examples/gloo-portal-create-api-key-example.json) — Create API key request/response
- [examples/gloo-gateway-list-upstreams-example.json](examples/gloo-gateway-list-upstreams-example.json) — List upstreams response
- [examples/gloo-gateway-get-virtual-service-example.json](examples/gloo-gateway-get-virtual-service-example.json) — Get virtual service response

### Vocabulary

- [vocabulary/solo-io-vocabulary.yml](vocabulary/solo-io-vocabulary.yml) — Domain vocabulary for Solo.io cloud-native API management

## Common Properties

- [Customers](https://www.solo.io/customers)
- [Case Studies](https://www.solo.io/resources/case-study)
- [Blog](https://www.solo.io/blog)
- [Documentation](https://www.solo.io/docs)
- [White Papers](https://www.solo.io/resources/white-paper)
- [Videos](https://www.solo.io/resources/video)
- [Webinars](https://www.solo.io/resources/webinar)
- [eBooks](https://www.solo.io/resources/ebook)
- [Partners](https://www.solo.io/partners)
- [Support](https://www.solo.io/company/get-support)
- [Pricing](https://www.solo.io/pricing)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
