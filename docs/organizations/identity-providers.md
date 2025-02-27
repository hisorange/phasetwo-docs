---
id: identity-providers
title: Identity providers
---

Identity providers (IdPs) can be associated with an organization for the purpose of directing users to authenticate with the IdP via a verified email domain, and for automatically granting membership to users who authenticate with that IdP.

### Associating an identity provider

There are two ways that an IdP can be associated with an organization.

#### Admin portal

If you have activated the organizations and SSO portions of the admin portal, members of the organization with the appropriate roles can set up their IdPs on their own. When they create and manage IdPs this way, they will be automatcially associated with the user's organization.

#### Admin UI

The admin UI contains an **Identity providers** section where full details of all IdPs can be created and managed. Also, the IdP wizards that are available to your organization administrators through the admin portal are also available to site administrators by navigating to `https://{host}/auth/realms/{realm}/wizard/`.

Because IdPs created using the admin UI or wizards are done by a site administrator, there is no organization associated by default. To do so, you can navigate to the **Organizations** section, select the organization for assignment and select the **Identity providers** tab. Making the association here will create the necessary relationships with the organization.

![](/docs/organizations-idps-associate.png)

### Verified domains

The purpose of associating domains with an organization is to allow identity providers to be conditionally shown based on email domain of a user who is logging in. In the **Settings** tab of each organizations, you can add multiple domains. When an authentication flow is configured properly to allow for redirection based on email domain, these are the domains that will be used to look up the associating identity provider.

![](/docs/organizations-idps-domains.png)

### Adding IdP and organization information to the token

Following a successful login using an IdP associated with an organization, a few values will be set in what are called "User Session Notes".
- `org_id` - The ID of the organization associated with the IdP.
- `identity_provider` - The IdP alias of the broker used to perform the login.
- `identity_provider_identity` - The IdP username of the currently authenticated user. 

These are values that survive the duration of a user login session, and can be used in token mappers. In order to add such a mapper in the admin UI, navigate to the client you are using, select the **Client scopes** tab, select the `{client}-dedicated` scope link, select the *Mappers* tab and configure a new mapper of type `User Session Notes`. You can choose the *Token Claim Name* that you require, and configure which tokens it is included.

![](/docs/organizations-idps-mapper.png)

### API access

It is possible to manage all aspects of the identity provider and its relationship to the organization using the [API](/api/). You will notice that the method in the Phase Two API are similar to those in the Keycloak Admin API. If you are building software that is targeted at organization administrators, you should use the Phase Two API, as it uses the permission model for organizations, and is not compatible with the Keycloak Admin API.

