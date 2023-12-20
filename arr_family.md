# Arr Guides

Contents here will include setup and configuration of various arr tools: Radarr, Sonarr, and Jackett. In the future Jackett will be replaced by Prowlarr.

## UnRaid Setup

Follow the steps outlined by [TRaSH Guide for unRAID](https://trash-guides.info/Hardlinks/How-to-setup-for/Unraid/#unraid) for configuring the Unraid OS and file structure.

My documentation differs in that I omit top level folder `data`. Instead of `/mnt/user/data/media/` I use `/mnt/user/media/`.

Many of the arr tool installation and configuration can be accompanied by [TRaSH Guides](https://trash-guides.info/).

## Generating Arr API Keys

_In Radarr Version 4_, navigate to Settings --> General (`<radarr_instance>`/settings/general) and under the "Security" section. An API key exists in place, if it is your first time using the API key, rotate the (API) key by clicking the Red button and copying the key to your clipboard.

Store the key in a password manager if needed for future use.

_In Sonarr Version 3_, navigate to Settings --> General (`<sonarr_instance>`/settings/general) and under the "Security" section. An API key exists in place, if it is your first time using the API key, rotate the (API) key by clicking the Red button and copying the key to your clipboard.

Store the key in a password manager if needed for future use.
