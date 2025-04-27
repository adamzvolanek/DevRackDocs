This page covers the setup of Prowlarr to deploy in my docker-compose stack(s). Likewise some investigation of configuration files to track and have deployable configuration on compose up.

Reference TRaSH Guide's for [Prowlarr](https://trash-guides.info/Prowlarr/) for additional more in-depth documentation.

## Setup

Follow these steps if a config file is not provided.

## Settings --> General

Security Settings

- Authentication: Basic (Browser Popup)
- Authentication Required: Enabled
- Username:
- Password:
- API Key:
- Certificate Validation: "Disabled for Local Addresses"

### Settings --> Apps

Within "Applications", add connected arrs.

Radarr/Sonarr

- Name: Leave default
- Sync Level: Full Sync
- Prowlarr Server: `http://prowlarr:<prowlarr_port>`
- Radarr Server: `http://radarr:<radarr_port>`
- API Key: <Key from Radarr>
- Sync Categories: Leave default

Within "Sync Profiles" modify "Minimum Seeders" to 5.

### Settings --> Indexers

Follow TRaSH Guides page on [FlareSolverr](https://trash-guides.info/Prowlarr/prowlarr-setup-flaresolverr/) to configure.

If site is down, follow these instructions.

- Select the + symbol and select 'FlareSolverr'.
- Name the Indexer Proxy
- Add the `flaresolverr` tag
- Configure the host. e.g. `http://flaresolverr:8191`
- Select "Test" and click "Save".

Adding FlareSolverr will be done in the [Indexer](#indexers) section of the doc.

### Indexers

Select Indexers and "Add New Indexer". Select the indexer desired to be added.

Modify the 'Download link' to be "magnet" and 'Download link (fallback) to be 'iTorrents.org'.

Repeat for additional indexers.

**Adding FlareSolverr**

- Select the indexer needed to use with FlareSolverr
- Select the wrench icon
- Scroll towards the bottom of the indexer's Tags and add the tag used for flaresolverr above. e.g. `flaresolverr`
- Click "Test" and "Save"

### Notifications

Navigate to Prowlarr Settings, Connect, Plus Symbol, and select Discord.

- Name: `Alexandria Discord`
- Notification Triggers:
  - [X] On Release Grab
  - [ ] Include Manual Grabs made within Prowlarr
  - [ ] On Health Issue
  - [ ] On Health Restored
  - [ ] On Application Upgrade
- Tags: Empty
- Webhook URL: https://discord.com/api/webhooks/...
- Username: `Prowlarr`
- Avatar: `https://cdn.jsdelivr.net/gh/selfhst/icons/webp/prowlarr.webp`
