This page covers the setup of sonarr v4 to deploy in my docker-compose stack(s). Likewise some investigation of configuration files to track and have deployable configuration on compose up.

Reference TRaSH Guide's for [Sonarr](https://trash-guides.info/Sonarr/) for additional more in-depth documentation.

## Setup

Follow these steps if a config file is not provided. If various settings do not appear, be sure to select the "Show Advanced" cog wheel at the top.

### Settings

These settings may already be set by default.

### Settings --> Media Management

Under the Folders section,

- [X] Create empty movie folders.
- [X] Delete Empty Folders.

#### Episode Naming

- [X] Rename Episodes
- [X] Replace Illegal Characters
- Color Replacement: Smart Replacement
- Standard Episode Format: `{Series Title} - S{season:00}E{episode:00} - {Episode Title} {Quality Full}`
- Daily Episode Format: `{Series Title} - {Air-Date} - {Episode Title} {Quality Full}`
- Anime Episode Format: `{Series Title} - S{season:00}E{episode:00} - {Episode Title} {Quality Full}`
- Series Folder Format: `{Series TitleYear}`
- Season Folders Format: `Season {season}`
- Specials Folder Format: `Specials`
- Multi Episode Style: Extend

#### Folders

- [X] Create empty movie folders.
- [X] Delete Empty Folders.

#### Importing

- Episode Title Required: Always
- [X] Skip Free Space Check
- Minimum Free Space: 3000 MB
- [X] Use Hardlinks instead of Copy
- [ ] Import Using Script
- [X] Import Extra Files
- Import Extra Files: `srt`

#### File Management

- [X] Unmonitor Deleted Episodes
- Propers and Repacks: Prefer and Upgrade
- [X] Analyse video files
- Rescan Series Folder after Refresh: Always
- Change File Date: None
- Recycling Bin: <Blank>
- Recycling Bin Cleanup: 7

#### Permissions

- [X] Set Permissions
- chmod Folder: `775`
- chown Group: <blank>

#### Root Folders

- `/media/tv`

#### Profiles

Modify 'HD-720p/1080p' by renaming it to 'Standard', check the "Upgrades Allowed" box, and Upgrade Until 'Bluray-1080p'. Verify the following qualifies are selected and de-selected:

- [ ] Bluray-2160p Remux
- [ ] Bluray-2160p
- [ ] WEB 2160p
- [ ] HDTV-2160p
- [X] Bluray-1080p Remux
- [X] Bluray-1080p
- [X] WEB 1080p
- [X] Bluray-720p
- [X] WEB 720p
- [ ] Raw-HD
- [X] HDTV-1080p
- [X] HDTV-720p
- [X] DVD
- [X] WEB 480p
- [ ] SDTV
- [ ] Unknown

Give HEVC a score of +10, x264 a score of +5, and select 'Save'.

Modify 'Ultra-HD', check the "Upgrades Allowed" box, and Upgrade Until 'Bluray-2160p'. Verify the following qualifies are selected and de-selected:

- [X] Bluray-2160p Remux
- [X] Bluray-2160p
- [X] WEB 2160p
- [X] HDTV-2160p
- [X] Bluray-1080p Remux
- [X] Bluray-1080p
- [x] WEB 1080p
- [ ] Bluray-720p
- [ ] WEB 720p
- [ ] Raw-HD
- [ ] HDTV-1080p
- [ ] HDTV-720p
- [ ] DVD
- [ ] WEB 480p
- [ ] SDTV
- [ ] Unknown

Give HEVC a score of +10, x264 a score of +5, and select 'Save'.

Delete the any remaining quality profiles.

#### Custom Formats

Select the plus symbol and name it 'HEVC'. Select the plus symbol for "Conditions" and select "Presets" under 'Release Title' and select 'x265'.

Ensure "Required" is checked.

Select the plus symbol again under "Conditions" and name it "x265" with the regular expression of `x265`.

Repeat creating an additional custom format for a `x264` Custom format.

Background info, these regex will match: x265, x.265, h265, h.265, and HEVC.

#### Indexers

These should be setup whence [Prowlarr](./prowlarr) is connected to the respective arr.

#### Download Clients

Select 'qBittorrent' and name the Download Client. Fill in the remaining fields as follows:

- Name: qBittorrent
- [X] Enable
- Host: `qBittorrentvpn` (this is the same as the container_name in `qBittorrent.yaml`)
- Port: `9519`
- [ ] Use SSL
- URL Base
- Username: admin (change from default)
- Password: (change from default)
- Category: `tv`
- Post-Import Category: blank
- Recent Priority: 'Last'
- Older Priority: 'Last'
- Initial State: Started
- [ ] Sequential Order
- [ ] First and Last First
- Content Layout: Default
- Client Priority: 1
- Tags: blank
- [X] Remove Completed

Completed Download Handling

- [X] Enable
- [X] Redownload Failed
- [X] Redownload Failed from Interactive Search

#### Language Profiles

Create an profile named 'Anime' with only "Japanese" and "English" selected. Arrange "Japanese" to be above "English".

Create an profile named 'Czech' with only "Czech" and "English" selected. Arrange "Czech" to be above "English".

Create an profile named 'English' with only "English" selected.

#### Connect

**Prerequisite**: Requires API Key from Jellyfin and Discord.

Select 'Emby/Jellyfin' and name the Connection. Fill in the fields as follows:

- [X] On Grab
- [X] On File Import
- [X] On File Upgrade
- [ ] On Import Complete
- [X] On Rename
- [X] On Series Add
- [X] On Series Delete
- [X] On Episode File Delete
- [X] On Episode File Delete For Upgrade
- [X] On Health Issue
- [X] On Health Restored
- [X] Include Health Warning
- [X] On Application Update
- Tags: blank
- Host: Enter `jellyfin` (this is the same as the container_name in `jellyfin.yaml`)
- Port: 8096
- [ ] Use SSL
- URL Base: blank
- API Key: <JellyFin API Key>
- [ ] Send Notifications
- [X] Update Library
- Map Paths From: blank
- Map Paths To: blank

Select 'Discord' and name the Connection: Alexandria Discord.

- [ ] On Grab
- [ ] On File Import
- [X] On Import Complete
- [ ] On Rename
- [X] On Series Add
- [X] On Series Delete
- [X] On Episode File Delete
- [X] On Episode File Delete For Upgrade
- [ ] On Health Issue
- [ ] On Health Restored
- [ ] On Application Update
- [ ] On Manual Interaction Required
- Tags: blank
- Webhook URL: https://discord.com/api/webhooks/...
- Username: Sonarr
- Avatar: `https://cdn.jsdelivr.net/gh/selfhst/icons/webp/sonarr.webp`
- Author: blank
- On Grab Fields: All selected.
- On Import Fields: All selected except for CustomFormats CustomFormatScore
- On Manual Interaction Fields: All selected.

#### Metadata

An option to explore, to share meta-data between the *arr family of dockers and JellyFin. Select 'Kodi (XBMC) / Emby Metadata' and check all the white text boxes.

#### General

Under Host

- Bind Address: *
- Port Number: 8989 (matching dockercompose file)
- URL Base: blank
- Instance Name: Sonarr
- Application URL: blank
- [ ] Enable SSL

Security

- Authentication: Basic (Browser Popup)
- Authentication Required: Disabled for Local Addresses
- Username: pick a name
- Password: pick a password
- Password Confirmation: repeat above
- API Key: leave alone
- Certificate Validation: Disabled for Local Addresses

Proxy

- [ ] Use Proxy

Logging

- Log Level: Info
- Log Size Limit: 1

Analytics

- [ ] Send Anonymous Usage Data

Updates

- Branch: develop
- [ ] Automatic
- Mechanism: Docker

Backups

- Folder: Backups
- Interval: 7 days
- Retention: 21 days

#### UI

Calendar

- First Day of the Week: Sunday
- Week Column Header: Tue 3/25

Dates

- Short Date Format: 03/25/2014
- Long Date Format: Tuesday, March 25, 2014
- Time Format: 17:00/17:30
- [X] Show Relative Dates

Style

- Theme: Auto
- [ ] Enable Color-Impaired Mode

Language

### Notifications

Navigate to Sonarr Settings, Connect, Plus Symbol, and select Discord.

- Name: `Alexandria Discord`
- Notification Triggers:
  - [X] On Grab
  - [ ] On File Import
  - [X] On File Upgrade
  - [X] On Import Complete
  - [ ] On Rename
  - [X] On Series Add
  - [X] On Series Delete
  - [X] On Episode File Delete
  - [X] On Episode File Delete For Upgrade
  - [ ] On Health Issue
  - [ ] On Health Restored
  - [ ] On Application Upgrade
  - [ ] On Manual Interaction Required
- Tags: Empty
- Webhook URL: https://discord.com/api/webhooks/...
- Username: `Sonarr`
- Avatar: `https://cdn.jsdelivr.net/gh/selfhst/icons/webp/sonarr.webp`

### Library Import

If you already have media, select the 'Start Import' button, select the `media\tv` directory, and press Ok. Allow time for the tv shows to be imported and managed.
