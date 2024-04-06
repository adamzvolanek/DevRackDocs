# Immich

This page covers the setup of Immich to deploy in my docker-compose stack(s). The Immich instance will be a private (family) photo library.

[Immich Site](https://immich.app/)

## Automated

Pending.

## Manual Steps

Follow these steps if a config file is not provided.

### Getting Started

- Create Admin Profile
- Select Theme: Dark
- Storage Template: Off

### External Library Import

- Select Administration at the top-right
- Select "External Libraries" in Settings
- Select "Create Library"
  - Allow Immich Admin to maintain ownership
- Select three dots to the right of the "New External Library"
  - Rename to appropriate name
  - Select "Edit Import Paths"
    - Enter `/external_photos`
      - This should match immich's volume
  - Select "Scan Settings"
    - Select "Add Exclusion Pattern"
      - Enter `**/Raw/**` to exclude photos in folders named "Raw"
  - Select "Scan New Library Files"
- Select "Settings"
  - Select "External Library"
    - Check "Watch filesystem"
  - Select "Periodic Scanning"
    - Check "Enabled"
    - Edit the cron to read `10 23 4,20 * *` # At 23:10 on day-of-month 4 and 20.
  - Select "Logging"
    - Check Enabled
    - Level: Log
  - Select "Machine Learning Settings"
    - Uncheck "Enabled"
  - Skip "Map & GPS Settings"
  - Select "OAuth Authentication"
    - Check "Enable"
      - Issuer URL:
      - Client ID:
      - Client Secret:
      - Scope:
      - Signing Algorithm:
      - Storage Label Claim:
      - Storage Quota Claim:
      - Default Storage Quota (GiB): 0
      - Button Text: Login with Adam's Authentik!
      - Check "Auto Register"
      - Check "Auto Launch"
      - Uncheck "Mobile Redirect URI Override"
  - Select "Server Settings"
    - Enter "External Domain": `https://sudomain.adamzvolanek.com`
    - Enter "Welcome Message": Zvolanek Photo Share
  - Select "Trash Settings"
    - Uncheck "Enabled"
  - Select "User Settings"
    - Delete Delay: 14
  - Select "Video Transcode Settings"
    - Check "HEVC" under "Video Codec"

### Admin Account Settings

- Select the profile icon at the top-right
- Select "Account Settings"
- Select "App Settings"
  - Change "Default Locale" to be "English (United Kingdom)"
  - Uncheck "Display original photos"
  - Uncheck "Play video thumbnail on hover"
  - Check "Permanent deletion warning"
  - Uncheck "People"
  - Check "Sharing"
- Select "Memories"
  - Uncheck "Time-based memories"
