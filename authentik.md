# Authentik

This page covers the setup of Authenitk to deploy in my docker-compose stack(s).

## Manual Steps

Authentik [documentation](https://version-2023-5.goauthentik.io/docs/)

### Applications

Upon starting Authentik, enter the 'Admin' interface and select "Applications". 

#### Setup Providers

Create "Providers" under Applications and the blue "Create" button. Select "Proxy Provider" and fill the appropriate fields as needed:

- Provide a "Name" for the Proxy Provider
- Authorization Flow: use implicit
- Select the "Proxy" tab for non-auth'd end-points that do not utilize Traefik or Nginx or are internal.
- Select the "Forward Auth (single application)" for other services.
- If page uses basic authentication:
  - Follow [these](https://goauthentik.io/integrations/services/sonarr/) instructions. These are written specifically for the 'arr' family of applications.

Create applicable applications for each service desired to be found on the Authentik User Interface. Fill out the fields as needed with selecting the appropriate provider. Optionally setup the UI Settings for the Application by providing an Icon, Publisher, or Description.

Within the 'Outpost' tab, select the edit button on the right and verify in the 'Integration' drop-down shows the Docker network you have specified. If not click [here](#system) Select all the Applications for the embedded outpost. Update Line 3 of the configuration with your own `https://auth.domain.tld` site.

Additional application configurations can be found [here](https://goauthentik.io/integrations/).

#### Setup NextCloud OAuth2/OpenID Providers (1/3)

NextCloud:

- Click on the "Create" button
- For "Type" select "OAuth2/OIDC Provider"
- Provide recognizable name for NextCloud's OAuth2/OIDC Provider. e.g. `Nextcloud-oidc`
- For "Authentication flow" select appropriate default authentication flow e.g. `default-authentication-flow`
- Select `default-provider-authorization-implicit-consent` for "Authorization flow"
  - Otherwise your users need to confirm each login explicitly.
- Client type: "Confidential"
- Client ID: (leave auto-generated value as-is)
  - Copy this value for later
- For "Client Secret" trim the auto-generated value to 64 characters - there is currently a bug in NextClouds user_oidc that [prevents longer client secrets](https://github.com/nextcloud/user_oidc/issues/405).
  - Copy this value for later
- Modify the "Redirect URIs" to `https://<NEXTCLOUD-HOSTNAME>/apps/user_oidc/code`
- Under "Advanced protocol settings"
  - Modify "Access code validity", "Access token validity", and "Refresh Token validity" as appropriately
  - Under "Scopes" select the following:
    - `authentik default OAuth Mapping: OpenID 'email'`
    - `authentik default OAuth Mapping: OpenID 'openid'`
    - `authentik default OAuth Mapping: OpenID 'profile'`
  - For "Subject mode" select "Based on the User's username"
    - Ensures NextCloud’s federated cloud ID will have a human-readable value, like `username@nextcloud-hostname.com`
- Click on Finish

[Source](https://blog.cubieserver.de/2022/complete-guide-to-nextcloud-oidc-authentication-with-authentik/)

#### Setup Applications

Each of the Providers require an associated "Application".

- Click on "Applications" and click on "Applications"
- Click the blue "Create" button to create a Application.
  - Provide a "Name" for the application
  - Provide a "Slug" for the applications URL (note this is an all-lower string)
  - Enter a "Group" for various applications to be grouped together on the "User Interface" screen
  - Select the "Provider" by name created previously
  - Select "all" for "Policy Engine Mode"
  - Fill out "UI Settings" as appropriate

#### Setup NextCloud Application for OAuth2/OpenID (2/3)

- Create a new Application with the "Name" NextCloud
- Enter an appropriate "Slug"
- Select the previously created NextCloud OIDC provider (`Nextcloud-oidc`)
- Update any additional UI settings as needed

Steps continued on NextCloud page found [here](./cloud#setup-nextcloud-application-for-oauth2openid-33)

[Source](https://blog.cubieserver.de/2022/complete-guide-to-nextcloud-oidc-authentication-with-authentik/)

#### Setup Outposts

Upon creating both providers and applications, click on "Outposts" and edit the present outpost by clicking the pencil icon under "Actions".

- Provide a recognizable name for the Outpost's "Integration"
- Highlight/Select all Applications
- Update the "Configuration"
  - Edit line 3 but replacing the URL with your Authentik's domain
  - Edit line 4 with your docker network Name
- Click "Update" at the bottom when finished making changes

### Customization

Click on "Policies" to edit various settings.

#### Password Complexity

Edit and update the 'Password Complexity' fields under the Actions (icon) pencil on the right. Be sure to update the "Static rules" namely the "Error message" so users are aware of the password requirement minimums.

#### Local Network check

This will create a policy that checks if a user is accessing/authenticating on the local network to bypass MFA. *Assumes MFA stage exists as part of default authentication flow.*

- Click on the blue "Create" button at the top to create a new Policy.
- Select "Expression Policy".
  - Provide a "Name" to the policy.
  - In the "Expression" field paste, `return ak_client_ip.is_private`. You can also use `return ak_client_ip in ip_network('10.0.0.0/24')` to specify a subnet.
- Select "Flows & Stages" and click on "Flows"
  - Click on the `default-authentication-flow`
  - Click on "Stage Bindings"
  - Click on the default mfa validation stage
  - Select "Bind existing policy"
  - Select the previously named policy from the drop-down
  - Verify it is "Enabled"
  - Provide logical order and timeout values.

### Flows & Stages

This section covers modifications and improvements to the "Flows & Stages" section of Authentik.

Basic UI customization can be editing within each "Flow" within the "Appearance Settings". Commonly updated flows for UI updates include `default-authentication-flow` and `default-invitation-flow`. Likewise single prompts can be customized within "Flows & Stages" --> "Prompts" however these are currently set to defaults.

#### MFA validation

- Login to Authentik as Administrator
- Click on "Admin Interface"
- Click on "Flows & Stages"
  - Click on "Stages"
- Select "Create" to create a new stage
- For type of stage select "Authenticator Stage"
  - Name the stage e.g. `default-authentication-mfa-validation`
  - Under "Stage-specific settings" select/highlight desired "Device Classes"
  - Modify "Last validation threshold" to desired values
  - Modify "Not configuration action" to desired MFA enforcement
  - Select desired "WebAuthn User verification" Policy
  - Within "Configuration Stages" select setup stages that match the selected "Device classes"
- Click "Create"
- Return to "Flows" and click `default-authentication-flow`
  - Click on "Stage Bindings" and select "Bind existing stage"
  - Select the recently created MFA Stage
  - Select a logical order for the authentication-flow
  - Select "Evaluate when flow is planned" and "Evaluate when stage is run"
  - For "Invalid response error" select appropriate action desired
  - For "Policy engine mode" select "any"
  - CLick "Create"

#### CloudFlare Turnstile

- Login to CloudFlare and enter the Turnstile page using the left-side site menu.
- Click "Add Site"
- Enter the site name (domain) and select "managed".
- Login to Authentik as Administrator
- Click on "Admin Interface"
- Click on "Flows & Stages"
  - Click on "Stages"
- Select "Create" to create a new stage
- For type of stage select "Captcha Stage"
  - Name the stage e.g. `Cloudflare Turnstile`
  - Copy the site key into the "Public Key" field
  - Copy the "secret key" into the "Private Key" field
  - Expand "Advanced Settings"
    - Navigate to [Client-side render](https://developers.cloudflare.com/turnstile/get-started/client-side-rendering/#disable-implicit-rendering) and scroll to find the challenges endpoint. e.g. `https://challenges.cloudflare.com/turnstile/v0/api.js`
  - Paste the link into the "JS URL" field.
  - Navigate to [Server-side integration](https://developers.cloudflare.com/turnstile/get-started/server-side-validation/) and find the proper endpoint. e.g. `https://challenges.cloudflare.com/turnstile/v0/siteverify` and paste it into the "API URL" field.
- Click on "Flows" and primary authentication flow.
  - Click on "Stage Bindings" and "Bind Existing Stage"
  - Select the stage just created
  - Enter the order number desired; i.e. have CloudFlare Turnstile check prior to identification stage or after.

Supporting video can be found [here](https://www.youtube.com/watch?v=Fe5SttNa2lU).

### Directory

Setup Users and Groups as needed; Groups are allowed to be nested as expected.

### System

Modify/customize the 'authentik-default' Tenant by selecting the icon on the right.

Setup Outpost Integrations by selecting the Docker Service-Connection and filling out the Name, Local check, and Docker URL to `/var/run/docker.sock`.

## Automated setup

Possibly follow [this](https://goauthentik.io/docs/installation/automated-install) install guide?
