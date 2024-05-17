## OAuth v2.0 - Authorization

#### Authorization Code flow

1. The **CLIENT** Application on **RESOURCE OWNER'S** consent to get access to their resources calls the **AUTHORIZATION SERVER** (FRONT CHANNEL CALL)

In the case of Microsoft Entra, the AUTHORIZATION SERVER's Authorize endpoint is *https://login.microsoftonline.com/[tenant-id]/oauth2/v2.0/authorize*

This endpoint can be obtained from any Application Registration instance in Azure Portal.

2. When the **CLIENT** calls the **AUTHORIZATION SERVER**, it provides the **REDIRECT URI** (callback),**SCOPE**, **CLIENT ID (1)** and the type of AUTHORIZATION GRANT (i.e) **RESPONSE TYPE**. (FRONT CHANNEL CALL)

Example :

1. RESPONSE TYPE: code for Authorization Code flow
2. SCOPE: profile contacts

The **scope** will be used by the **authorization server** to build the consent screen. Basically **scope** represent the resources to which the **client** needs access from the **resource server**.

3. The **AUTHORIZATION SERVER** redirects to **REDIRECT URI** (ie. callback) and provides the **AUTHORIZATION CODE** (FRONT CHANNEL CALL)

4. The Callback service (of **CLIENT**) calls the **AUTHORIZATION SERVER**'s token endpoint with the **AUTHORIZATION CODE** (obtained from previous steps) and its SECRET (**CLIENT ID (1?) AND CLIENT SECRET**) to get the **ACCESS TOKEN**. (BACK CHANNEL CALL)

5. The **AUTHORIZATION SERVER** validates the **AUTHORIZATION CODE**, (checks whether the code is from valid client) and returns the **ACCESS TOKEN** to the callback. ( Note!: **Access Token**)

In the case of Microsoft Entra, the AUTHORIZATION SERVER's Token endpoint is

*https://login.microsoftonline.com/[tenant-id]/oauth2/v2.0/token*

6. The **CLIENT** after getting the **ACCESS TOKEN** calls the **RESOURCE SERVER** with the **ACCESS TOKEN** and access the scoped resources. (BACK CHANNEL CALL)

## Other Flows

1. Client Credentials Flow (Back channel only)

2. Implicit Flow (Front Channel only) - Here the response type is Token and not the Code as in Authorization Code flow

3. Resource Owner Password Credentials Flow (Back channel only)

## Open ID Connect - Authentication

What Open ID Connect adds on top of OAuth?

1. ID Token (contains some of the users information)

2. User endpoint (to fetch more user information from AuthZ server)(called with access token)

3. Standard Set of Scopes

   scope: **openid** profile => this returns id token

---

Example Request

---

[Reference](https://learn.microsoft.com/en-us/entra/identity-platform/v2-oauth2-client-creds-grant-flow#application-permissions)

```
https://login.microsoftonline.com/a4e846c2-72d3-43ca-8473-e7311c75b073/oauth2/v2.0/token

method: POST
Content-Type: application/x-www-form-urlencoded

---------------------------------------------------------------

body :

grant_type : client_credentials
client_id: a5e19417-3551-4d19-9c36-86d275092f07
client_secret: <secret>
scope: https://graph.microsoft.com/.default

```

Reference

---

1. [Authorization Code flow + Refresh Token => (Delegated Permissions)](https://learn.microsoft.com/en-us/graph/auth-v2-user?tabs=http)

2. [Auth Concepts](https://learn.microsoft.com/en-us/graph/auth/auth-concepts)

3. [Application Permissions](https://learn.microsoft.com/en-us/graph/auth-v2-service?tabs=http)
