# Immich

This page covers the setup of Immich to deploy in my docker-compose stack(s). The Immich instance will be a private (family) photo library.

[Immich Site](https://immich.app/)

This procedure has been **deprecated** and instead using [Photoprism](./photoprism) due to instability of Immich during testing.

## Automated

Pending.

## Manual Steps

Follow these steps if a config file is not provided.

### Getting Started

- Create Admin Profile
- Select Theme: Dark
- Storage Template: On
  - Configure to use "2022/02/IMAGE_56437". Template should be `{{y}}/{{MM}}/{{filename}}`.

### Admin Account Settings

- Select the profile icon at the top-right
- Select "Account Settings"
- Select "App Settings"
  - Change "Default Locale" to be "English (United Kingdom)"
  - [ ] "Display original photos"
  - [ ] "Play video thumbnail on hover"
  - [ ] "Loop videos"
  - [X] "Permanent deletion warning"
  - [ ] "People"
  - [X] "Sharing"
- Select "Memories"
  - Uncheck "Time-based memories"
- Select "Features"
  - Select "Folders"
    - [X] Enable
    - [X] Sidebar
  - [ ] Time-based memories
  - Select "People"
    - [ ] Enable
  - Select "Star rating"
    - [ ] Enable
  - Select "Tags"
    - [ ] Enable
- Select "Notifications"
  - [X] Enable email notifications
  - [X] Album added
  - [X] Album updated

### Administration Settings

- Select Settings
  - Select "Job Settings"
    - Set all concurrency threads to 1

### External Library Import

[Immich Link](https://immich.app/docs/guides/external-library/)

- Select Administration at the top-right
- Select "External Libraries" in Settings
- Select "Create Library"
  - Allow Immich Admin to maintain ownership
- Select three dots to the right of the "New External Library"
  - Rename to appropriate name
  - Select "Edit Import Paths"
    - Enter `/external_photos`
      - This matches immich's volume mounting in the docker-compose file
  - Select "Scan Settings"
    - Select "Add Exclusion Pattern"
      - Enter `**/Raw/**` to exclude photos in folders named "Raw"
      - Select "Save"
  - Select "Scan New Library Files"
- Select "Settings"
  - Select "External Library"
    - [X] "Watch filesystem"
  - Select "Periodic Scanning"
    - [X] "Enabled"
    - Edit the cron to read `10 23 4,20 * *` # At 23:10 on day-of-month 4 and 20.
  - Select "Logging"
    - [X] Enabled
    - Level: Log
  - Select "Machine Learning Settings"
    - [ ] "Enabled"
  - Skip "Map & GPS Settings"
  - Select "OAuth Authentication"
    - [ ] Enable
    - <details><summary>Authentik Setup</summary>

      - [X] "Enable"
      - Issuer URL:
      - Client ID:
      - Client Secret:
      - Scope:
      - Signing Algorithm:
      - Storage Label Claim:
      - Storage Quota Claim:
      - Default Storage Quota (GiB): 0
      - Button Text: Login with Adam's Authentik!
      - [X] "Auto Register"
      - [X] "Auto Launch"
      - [ ] "Mobile Redirect URI Override"

      </details>
  - Select "Server Settings"
    - Enter "External Domain": `https://subdomain.adamzvolanek.com`
    - Enter "Welcome Message": Zvolanek Photo Backup
  - Select "Trash Settings"
    - [ ] "Enabled"
  - Select "User Settings"
    - Delete Delay: 14
  - Select "Video Transcode Settings"
    - [X] "HEVC" under "Video Codec"
