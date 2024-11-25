This page covers the setup of sonarr v4 to deploy in my docker-compose stack(s). Likewise some investigation of configuration files to track and have deployable configuration on compose up.

Reference TRaSH Guide's for [Sonarr](https://trash-guides.info/Sonarr/) for additional more in-depth documentation.

## Setup

Follow these steps if a config file is not provided.

### Settings --> Custom Formats

Select the plus symbol and name it 'HEVC'. Select the plus symbol for "Conditions" and select "Presets" under 'Release Title' and select 'x265'.

Ensure "Required" is checked.

Select the plus symbol again under "Conditions" and name it "x265" with the regular expression of `x265`.

Repeat for creating a `x264` Custom format.

### Settings --> Profiles

#### Quality Profiles

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

#### Language Profiles

Create an profile named 'Anime' with only "Japanese" and "English" selected. Arrange "Japanese" to be above "English".

Create an profile named 'Czech' with only "Czech" and "English" selected. Arrange "Czech" to be above "English".

Create an profile named 'English' with only "English" selected.

### Settings --> Indexers

Under Indexers, add a new indexer named 'Torznab'. The instructions below will apply to all indexers added as part of the [jackett](jackett.md) instructions.

- Name the indexer to match the indexer URL in Jackett,
- Check 'Enable RSS'
- Check 'Enable Automatic Search'
- Check 'Enable Interactive Search'
- Add the 'Torznab Feed' (from Jackett) to the URL. Traditional structure of URL: `http://<SERVER_IP>:<JACKET_PORT>/api/v2.0/indexers/<INDEXER_NAME>/results/torznab/`
- Leave the API path as `/api`
- Add Jackett's API Key (found at the top right of Jackett's home screen)
- Select the appropriate category `TV (5000)`
- Select appropriate anime categories: `TV/Anime (5070)`, `Raw animes (134634)`, and `Anime (140679)`
- Minimum Seeders: 5
- Select an appropriate seed ratio. *This over-writes the download clients default*
- Select an appropriate seed time. *This over-writes the download clients default*

Repeat these steps for each Indexer.

### Settings --> Download Clients

Select 'qBittorrent' and name the Download Client. Fill in the remaining fields as follows:

- Name: qBittorrent VPN
- Host: Enter `qBittorrentvpn` (this is the same as the container_name in `qBittorrent.yaml`)
- Port: 8089
- Useranme: admin (change from defualt)
- Password: (change from default)
- Category: `tv`
- Recent Priority: 'Last' (leave as default)
- Older Priority: 'Last' (leave as default)
- Initial State: Start
- Remove Completed: Checked (leave as default)

### Settings --> Connections

**Prerequisite**: Requires API Key from Jellyfin.

Select 'Emby' and name the Connection. Fill in the fields as follows:

- Check 'On Health Issue' and check the subsequent 'Include Health Warnings'
- Host: Enter `jellyfin` (this is the same as the container_name in `jellyfin.yaml`)
- Port: 8096 (leave as default)
- Check 'Have MediaBrowser send notifications to configured providers'
- Check 'Update Library on Import, Rename or Delete?'

### Settings --> Metadata

An option to explore, to share meta-data between the *arr family of dockers and JellyFin. Select 'Kodi (XBMC) / Emby Metadata' and check all the boxes.

### Settings --> UI

Modify the 'Time Format' under 'Dates' to 17:00/17:30.

### Series --> Library Import

Select the 'Start Import' button, select the `media\tv` directory, and press Ok. Allow time for the tv shows to be imported and managed.

## Automated

Configuration file to be generated from 'blank' sonarr install and imported during compose or a part of local stack directory.

In-Work: Use of [Recyclarr](./recyclarr) to create default deployable configuration for both sonarr and radarr.
