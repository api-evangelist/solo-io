---
name: solo-io-subscribe-app-to-api-product
description: Onboard a team onto a Gloo Portal API product — create the team, create an
  app, subscribe the app to an API product version, and issue the API key the app will
  call the gateway with.
api: openapi/solo-io-portal-backend-openapi.yml
operations:
  - GetCurrentUser
  - ListApiProducts
  - ListApiProductVersions
  - CreateTeam
  - CreateTeamApp
  - CreateAppSubscription
  - CreateAppApiKey
  - ListAppSubscriptions
generated: '2026-08-02'
method: generated
source: openapi/solo-io-portal-backend-openapi.yml
---

# Subscribe an app to a Gloo Portal API product

Use this skill against the **Gloo Portal Backend API** (`openapi/solo-io-portal-backend-openapi.yml`).
The portal is self-hosted, so the base URL is the portal backend deployed in the customer's
cluster, with `/v1` as the API base path.

## Authentication

The spec declares three schemes; pick the one the deployment uses:

- `identityToken` — `id_token` cookie set by the identity provider after OIDC login
- `accessToken` — `access_token` cookie set by the identity provider after OIDC login
- `bearerAuth` — bearer token in the `Authorization` header

Browser flows start at `LoginRedirect` (`GET /login`) and end at `LogoutRedirect`
(`GET /logout`). Every operation below returns `401` when the session is missing or expired.

## Steps

1. **Confirm the session.** Call `GetCurrentUser` (`GET /me`). A `200` returns the `User`
   object. If you get `401`, send the caller through `LoginRedirect` first.
2. **Find the product.** Call `ListApiProducts` (`GET /api-products`) and pick the
   `ApiProductSummary` the team needs. `503` here means the portal's backing catalog is
   not ready yet — retry rather than treating it as a hard failure.
3. **Pick the version.** Call `ListApiProductVersions` (`GET /api-products/{productID}/versions`)
   to get the `ApiProductVersion` the subscription should target.
4. **Create the team** (skip if it already exists). Call `CreateTeam` (`POST /teams`) with a
   `CreateTeamRequest`. A `409` means a team of that name already exists — resolve it with
   `ListTeams` instead of retrying the create.
5. **Create the app.** Call `CreateTeamApp` (`POST /teams/{teamID}/apps`) with a
   `CreateAppRequest`. Again, `409` means the app already exists.
6. **Subscribe.** Call `CreateAppSubscription` (`POST /apps/{appID}/subscriptions`) with a
   `CreateSubscriptionRequest` naming the API product. The response is a `Subscription`
   carrying a `SubscriptionStatus`; a subscription may require approval before it is usable.
7. **Issue the credential.** Call `CreateAppApiKey` (`POST /apps/{appID}/api-keys`) with a
   `CreateApiKeyRequest`. The `201` response is an `ApiKeyWithSecret` — **the secret is
   returned once and is not retrievable later.** Store it immediately; subsequent
   `ListAppApiKeys` calls return `ApiKey` without the secret.
8. **Verify.** Call `ListAppSubscriptions` (`GET /apps/{appID}/subscriptions`) and confirm the
   subscription status is the one you expect before telling the caller they are live.

## Rules

- **No idempotency keys.** The Portal Backend API declares no idempotency header, so a
  retried `POST` can create a duplicate. Guard creates by reading first
  (`ListTeams`, `ListTeamApps`, `ListAppSubscriptions`) and treat `409 Conflict` as
  "already exists", not as an error to retry.
- **No pagination parameters** are declared on the list operations — do not invent
  `limit`/`offset`/`cursor` query parameters.
- Error semantics: `400` bad request, `401` unauthenticated, `403` not permitted,
  `404` not found, `409` conflict, `500` server error, `503` catalog not ready.
  See `errors/solo-io-problem-types.yml`.
- Deletes return `204` with no body: `DeleteAppSubscription`, `DeleteAppApiKey`,
  `DeleteApp`, `DeleteTeam`, `RemoveTeamMember`.
