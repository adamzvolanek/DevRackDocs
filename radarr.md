# Radarr v4

This page covers the setup of radarr to deploy in my docker-compose stack(s). Likewise some investigation of configuration files to track and have deployable configuration on compose up.

Reference TRaSH Guide's for [Radarr](https://trash-guides.info/Radarr/) for additional more in-depth documentation.

## Automated

Configuration file to be generated from 'blank' radarr install and imported during compose or a part of local stack directory.

In-Work: Use of [Recyclarr](./recyclarr) to create default deployable configuration for both sonarr and radarr.

## Manual Steps

Follow these steps if a config file is not provided.

### Settings --> Custom Formats

Select the plus symbol and name it 'HEVC'. Select the plus symbol for conditions and enter the following information.

- Name: `x265`
- Regular Expression: `(((x|h)\.?265)|(HEVC))`
- Leave Negate unchecked. 'If checked, the custom format will not apply...'
- Check Required. 'This Release Title condition must match for the...'

### Settings --> Profiles

#### Quality Profiles

Modify 'HD-720p/1080p' by renaming it to 'Standard', check the "Upgrades Allowed" box, select "Upgrade Until Quality" to be 'Bluray-1080p', and select the "Language" to be 'English'. Verify the following qualifies are selected and de-selected:

- [ ] Raw-HD
- [ ] BR-DISK
- [ ] Remux-2160p
- [ ] Bluray-2160p
- [ ] WEB 2160p
- [ ] HDTV-2160p
- [X] Remux-1080p
- [X] Bluray-1080p
- [X] WEB 1080p
- [X] HDTV-1080p
- [X] Bluray-720p
- [X] WEB 720p
- [X] HDTV-720p
- [X] Bluray-576p
- [X] Bluray-480p
- [X] WEB 480p
- [ ] DVD-R
- [ ] DVD

Select 'Save'.

Modify 'SD' by renaming it to 'Ultra-HD', check the "Upgrades Allowed" box, select "Upgrade Until Quality" to be 'Bluray-2160p', and select the "Language" to be 'English'. Verify the following qualifies are selected and de-selected:

- [ ] Raw-HD
- [ ] BR-DISK
- [X] Remux-2160p
- [X] Bluray-2160p
- [X] WEB 2160p
- [X] HDTV-2160p
- [X] Remux-1080p
- [X] Bluray-1080p
- [ ] WEB 1080p
- [ ] HDTV-1080p
- [ ] Bluray-720p
- [ ] WEB 720p
- [ ] HDTV-720p
- [ ] Bluray-576p
- [ ] Bluray-480p
- [ ] WEB 480p
- [ ] DVD-R
- [ ] DVD

Select 'Save'.

Create a new "Quality Profile" and set it's name to 'Anime', check the "Upgrades Allowed" box, select "Upgrade Until Quality" to be 'Remux-1080p', and select the "Language" to be 'Original'. Verify the following qualifies are selected and de-selected:

- [ ] Raw-HD
- [ ] BR-DISK
- [ ] Remux-2160p
- [ ] Bluray-2160p
- [ ] WEB 2160p
- [ ] HDTV-2160p
- [X] Remux-1080p
- [X] Bluray-1080p
- [X] WEB 1080p
- [X] HDTV-1080p
- [X] Bluray-720p
- [X] WEB 720p
- [ ] HDTV-720p
- [ ] Bluray-576p
- [ ] Bluray-480p
- [ ] WEB 480p
- [ ] DVD-R
- [ ] DVD

Select 'Save'.

Create a new "Quality Profile" and set it's name to 'Standard Czech', check the "Upgrades Allowed" box, select "Upgrade Until Quality" to be 'Remux-1080p', and select the "Language" to be 'Czech'. Verify the following qualifies are selected and de-selected:

- [ ] Raw-HD
- [ ] BR-DISK
- [ ] Remux-2160p
- [ ] Bluray-2160p
- [ ] WEB 2160p
- [ ] HDTV-2160p
- [X] Remux-1080p
- [X] Bluray-1080p
- [X] WEB 1080p
- [X] HDTV-1080p
- [X] Bluray-720p
- [X] WEB 720p
- [X] HDTV-720p
- [X] Bluray-576p
- [X] Bluray-480p
- [X] WEB 480p
- [X] DVD-R
- [X] DVD

Select 'Save'.

Delete any remaining quality profiles.

### Settings --> Download Clients

Select 'Deluge' and name the Download Client. Fill in the remaining fields as follows:

- Host: Enter `delugevpn` (this is the same as the container_name in `delugevpn.yaml`)
- Port: 8112 (leave as default)
- Password: (change from default)
- Category: `radarr` (leave as default)
- Recent Priority: 'Last' (leave as default)
- Older Priority: 'Last' (leave as default)
- Add Paused: Remain unchecked (leave as default)
- Remove Completed: Checked (leave as default)

### Settings --> Connections

**Prerequisite**: Requires API Key from Jellyfin.

Select 'Emby / Jellyfin' and name the Connection. Fill in the fields as follows:

- Check 'On Health Issue' and check the subsequent 'Include Health Warnings'
- Host: Enter `jellyfin` (this is the same as the container_name in `jellyfin.yaml`)
- Port: 8096 (leave as default)
- Check 'Have MediaBrowser send notifications to configured providers'
- Check 'Update Library on Import, Rename or Delete?'

### Settings --> Metadata

An option to explore, to share meta-data between the *arr family of dockers and JellyFin. Select 'Kodi (XBMC) / Emby Metadata':

- Check 'Enable metadata file creation for this metadata type'
- Check Movie Metadata
- Leave 'English' as the Metadata Language
- Check Movie Images
- Uncheck 'Radarr will write metadata to movie.nfo...

### Settings --> UI

Modify the 'Time Format' under 'Dates' to 17:00/17:30.

### Movies --> Library Import

Select the 'Start Import' button, select the `media/movies` directory, and press Okay. Allow time for the movies to be imported and managed.
