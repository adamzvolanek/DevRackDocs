# Authentik

This page covers the setup of authenitk to deploy in my docker-compose stack(s). Likewise some investigation of configuration files to track and have deployable configuration on compose up.

## Manual Steps

Authentik [documentation](https://version-2023-5.goauthentik.io/docs/)

### Applications

Upon starting Authentik, enter the 'Admin' interface and select 'Applications'. Create 'Providers' under Applications and click 'Create'. Select 'Proxy Provider' and fill the appropriate fileds as needed:
  - Name: For the Proxy Provider
  - Authorization Flow: use implicit
  - Select the 'Proxy' tab for non-auth end-points that do not utilize Traefik or Nginx or are internal.
  - Select the 'Forward Auth (single application)' for other services.
  - If page uses basic authentication:
    - Follow [these](https://goauthentik.io/integrations/services/sonarr/) instructions. These are written specifically for the 'arr' family of applications.

Create applicable applications for each service desired to be found on the Authentik User Interface. Fill out the fields as needed wiht selecting the appropriate provider. Optionally setup the UI Settings for the Application by providing an Icon, Publisher, or Description.

Within the 'Outpost' tab, select the edit button on the right and verify in the 'Integration' drop-down shows the Docker network you have specified. If not click [here](#system) Select all the Applications for the embedded outpost. Update Line 3 of the configuration with your own `https://auth.domain.tld` site.

Additional application configurations can be found [here](https://goauthentik.io/integrations/).

### Customisation

Edit and updateh the 'Password Complexity' fields under the Actions (icon) pencil on the right.

### Flows & Stages

Setup CloudFlare turnstile following [this](https://www.youtube.com/watch?v=Fe5SttNa2lU) video.

### Directory

Setup Users and Groups as needed.

### System

Modify/customize the 'authentik-defualt' Tenant by selecting the icon on the right.

Setup Outpost Integrations by selecting the Docker Service-Connection and filling out the Name, Local check, and Docker URL to `/var/run/docker.sock`.

## Automated setup

Possibly follow [this](https://goauthentik.io/docs/installation/automated-install) install guide?
