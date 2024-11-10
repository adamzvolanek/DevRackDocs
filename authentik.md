# Authentik

This page covers the setup of Authenitk to deploy in my docker-compose stack(s).

## Manual Steps

Setup your admin user and upon starting Authentik, enter the 'Admin' interface and select "Applications".

Prior to starting docker-compose, un Unraid run `mkdir -p /mnt/user/appdata/authentik/authentik/media` and then `chmod -R 777 /mnt/user/appdata/authentik/authentik/media`.

### Create With Wizard

The next section is broken down by application to setup Authenitk for various services.

#### FileBrowser

Pending.

#### Immich

Follow [this page](https://immich.app/docs/administration/oauth/#example-configuration) for configuration.

### Customization

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
