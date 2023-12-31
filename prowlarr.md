# Prowlarr

This page covers the setup of Prowlarr to deploy in my docker-compose stack(s). Likewise some investigation of configuration files to track and have deployable configuration on compose up.

Reference TRaSH Guide's for [Prowlarr](https://trash-guides.info/Prowlarr/) for additional more in-depth documentation.

## Automated

Pending.

## Manual Steps

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

### Indexers

Select Indexers and "Add New Indexer". Select the indexer desired to be added.

Modify the 'Download link' to be "magnet" and 'Download link (fallback) to be 'iTorrents.org'.

Repeat for additional indexers.
