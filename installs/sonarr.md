# Sonarr

This page covers the setup of my development version of sonarr to deploy my docker-compose stack(s). Likewise some investigation of configuration files to track and have deployable configuration on compose up.

**TO COMPLETE LATER** Will need to adjust and reform mounts/media library to follow the structure outlined [here](https://trash-guides.info/Hardlinks/How-to-setup-for/Docker/). This will occur during ZFS transition.

## Manual Steps

Follow these steps if a config file is not provided.

### Settings --> Profiles

Delete the following quality profiles:

- 'SD'
- 'HD-1080p'
- 'HD-720p'

Modify 'Any' by renaming it to 'Any(Czech)' and change the Language to Czech. Also modify it by excluding these Qualities:

- BR-DISK, Remux-2160p, Bluray-2160p, WEB 2160p, HDTV-2160p, and Remux-1080p.
- Exclude all qualities below 'WEB 480p'

Modify 'HD-720p/1080p' by renaming it to 'Any'.

### Settings --> Custom Formats

Select the plus symbol and name it 'HEVC'. Select the plus symbol for conditions and enter the following information.

- Name: `x265`
- Regular Expression: `(((x|h)\.?265)|(HEVC))`
- Leave Negate unchecked. 'If checked, the custom format will not apply...'
- Check Required. 'This Release Title condition must match for the...'

### Settings --> Download Clients

Select 'Deluge' and name the Download Client. Fill in the remaining fields as follows:

- Host: Enter `delugevpn` (this is the same as the container_name in `delugevpn.yaml`)
- Port: 8112 (leave as default)
- Password: (change from default)
- Category: `sonarr` (leave as default)
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

An option to explore, to share meta-data between the *arr family of dockers and JellyFin. Select 'Kodi (XBMC) / Emby Metadata' and check all the boxes.

### Settings --> UI

Modify the 'Time Format' under 'Dates' to 17:00/17:30.

### Movies --> Library Import

Select the 'Start Import' button, select the 'movies' directory, and press Okay. Allow time for the movies to be imported and managed.

## Automated

Configuration file to be generated from 'blank' sonarr install and imported during compose or a part of local stack directory.
