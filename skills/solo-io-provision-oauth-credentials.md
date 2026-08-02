---
name: solo-io-provision-oauth-credentials
description: Provision and revoke OAuth2 client credentials for a Gloo Portal app, both
  through the portal server API and through the IdP Connect SPI that creates the client in
  the OpenID Connect provider.
api: openapi/solo-io-portal-server-openapi.yml
operations:
  - GetCurrentUser
  - GetApplicationById
  - GenerateApplicationOAuthCredential
  - GetApplicationOAuthCredential
  - DeleteOAuthCredential
  - CreateOAuthApplication
  - DeleteOAuthApplication
generated: '2026-08-02'
method: generated
source: openapi/solo-io-portal-server-openapi.yml, openapi/solo-io-portal-idp-connect-openapi.yml
---

# Provision OAuth credentials for a Gloo Portal app

Two contracts are involved and they are deliberately separate:

- **`openapi/solo-io-portal-server-openapi.yml`** — the Gloo Portal Server API a portal
  user calls to generate credentials for their own app.
- **`openapi/solo-io-portal-idp-connect-openapi.yml`** — the IdP Connect SPI the portal
  server calls to actually create/delete the OAuth2 client in the OIDC provider. Operators
  implement or deploy this; portal end-users never call it directly.

## Authentication

Portal Server API: `identityToken` — the `id_token` cookie issued by the identity provider.
IdP Connect API: a `token` header carrying the token of the origin user invoking the request.

## Steps — portal user path

1. **Confirm the session.** `GetCurrentUser` (`GET /me`) → `200` with a `User`.
2. **Resolve the app.** `GetApplicationById` (`GET /apps/{appId}`) → `200` with an
   `Application`. `403` means the caller is not on the owning team.
3. **Check for an existing credential.** `GetApplicationOAuthCredential`
   (`GET /apps/{appId}/oauth-credentials`) → `200` with an `OAuthCredential`.
   Generating a second credential when one exists returns `409`.
4. **Generate.** `GenerateApplicationOAuthCredential`
   (`POST /apps/{appId}/oauth-credentials`) → `201` with an `OAuthCredentialWithSecret`.
   **The client secret is shown once at creation time and is not stored in the portal
   database.** Capture it in the same call; if it is lost, only the OIDC provider admin can
   retrieve it.
5. **Revoke.** `DeleteOAuthCredential` (`DELETE /oauth-credentials/{credentialId}`) → `204`.

## Steps — IdP Connect (operator/SPI) path

1. **Create the client.** `CreateOAuthApplication` (`POST /applications`) with the unique
   client identifier → `201` returning the `OAuthApplication`. Same one-time-secret rule.
2. **Delete the client.** `DeleteOAuthApplication` (`DELETE /applications/{id}`) → `204`.
   `404` means the client is already gone — treat that as success when reconciling.

## Rules

- Neither contract declares an idempotency key. Because `CreateOAuthApplication` mints a
  secret, never blind-retry it — read state first, and treat `409`/`404` as terminal
  reconciliation signals rather than retryable errors.
- The IdP Connect `Error` schema is the error envelope on that API; the Portal Server API
  returns its own error bodies. See `errors/solo-io-problem-types.yml`.
- Reference docs: https://docs.solo.io/gateway/latest/portal/guides/frontend-portal/credential-management/oauth/
