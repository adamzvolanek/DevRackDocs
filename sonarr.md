# Sonarr

This page covers the setup of sonarr to deploy in my docker-compose stack(s). Likewise some investigation of configuration files to track and have deployable configuration on compose up.

This document supports Sonarr version 3.

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

Under Release Profiles, create a new profile named 'HEVC'. Check 'Enable Profile' and in 'Preferred' enter `x265` wiht a score of 10 and `x264` with a score 5.

### Settings --> Indexers

Under Indexers, add a new indexer named 'Torznab'. The instructions below will apply to all indexers added as part of the [jackett](jackett.md) instructions.

- Name the indexer to match the indexer URL in Jackett,
- Check 'Enable RSS'
- Check 'Enable Automatic Search'
- Check 'Enable Interactive Search'
- Add the 'Torznab Feed' (from Jackett) to the URL. Traditional structure of URL: `http://<SERVER_IP>:<JACKET_PORT>/api/v2.0/indexers/<INDEXER_NAME>/results/torznab/`
- Leave the API path as `/api`
- Add Jackett's API Key (found at the top right of Jackett's home screen)
- Select the appropriate categoriey `TV (5000)`
- Select appropriate anime categories: `TV/Anime (5070)`, `Raw animes (134634)`, and `Anime (140679)`
- Minimum Seeders: 5
- Select an appropriate seed ratio. *This over-writes the download clients default*
- Select an appropriate seed time. *This over-writes the download clients default*

Repeat these steps for each Indexer.

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
