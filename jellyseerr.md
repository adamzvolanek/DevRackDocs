# Jellyseerr

This page covers the setup of [Jellyseer](https://github.com/Fallenbagel/jellyseerr) to deploy in [my](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/external/jellyseerr.yaml) docker-compose stack(s).

## Manual Steps

Prerequisites:

- A Jellyfin instance running with [Nginx configured](./nginx_proxy_manager)
- Radarr instance running and configured per [radarr](./radarr)
- Sonarr instance running and configured per [sonarr](./sonarr)

### Initial Setup Connect to JellyFin

On connecting to docker container, select the "Use your Jellyfin account", and input your Jellyfin's information:

- "Jellyfin URL" : `https://<Jellyfin_Domain>.tld`
- "Email Address" : `email@domain.tld` (As noted, does not have to be associated with server)
- "Username" : `JellyFin Admin Username`
  - Utilize a JellyFin admin account username here on creation
- "Password" : `JellyFin Admin Password`

### Initial Setup Jellyseerr

On step 2 of "Configure Media Server" click on "Sync Libraries" and select your applicable libraries. Upon selecting the libraries select "Next".

### Initial Setup Services

#### Radarr

For Radarr configuration select "Add Radarr Server". Treat the "Default Server" as the [Standard](./radarr#quality-profiles) quality profile.

- "Default Server" : Check box "Standard" Quality Profile.
- "4K Server" : Only checked for ["Ultra-HD"](./radarr#quality-profiles) quality profile.
- "Server Name" : [`<Radarr_Container_Name>`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/arrs/arrs.yaml#L5)
- "Hostname or IP Address" : `<Radarr_Container_Name>`.
- "Port" : [`<Radarr_Port>`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/arrs/arrs.yaml#L12)
- "Use SSL" : Uncheck
- "API Key" : [`<Radarr_API_Key>`](./arr_family#generating-arr-api-keys)
- "URL Base" : Leave blank.
- "Quality Profile" : Select "Standard" when configuring "Default Server", else configure a Radarr Server for each "Quality Profile".
- "Root Folder" : [`/media`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/arrs/arrs.yaml#L15)`/movies`
- "Minimum Availability" : "Released"
- "Tags" : Empty.
- "External URL" : `https://<Jellyfin_Domain>.tld`
- "Enable Scan" : Check
- "Enable Automated Search" : Check
- "Tag Requests" : Check

- "Default Server" : Check box "Ultra-HD" Quality Profile.
- "4K Server" : Only checked for ["Ultra-HD"](./radarr#quality-profiles) quality profile.
- "Server Name" : [`<Radarr_Container_Name>`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/arrs/arrs.yaml#L5)
- "Hostname or IP Address" : `<Radarr_Container_Name>`.
- "Port" : [`<Radarr_Port>`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/arrs/arrs.yaml#L12)
- "Use SSL" : Uncheck
- "API Key" : [`<Radarr_API_Key>`](./arr_family#generating-arr-api-keys)
- "URL Base" : Leave blank.
- "Quality Profile" : Select "Standard" when configuring "Default Server", else configure a Radarr Server for each "Quality Profile".
- "Root Folder" : [`/media`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/arrs/arrs.yaml#L15)`/movies`
- "Minimum Availability" : "Released"
- "Tags" : Empty.
- "External URL" : `https://<Jellyfin_Domain>.tld`
- "Enable Scan" : Check
- "Enable Automated Search" : Check
- "Tag Requests" : Check

**Sonarr**

For Sonarr configuration select "Add Sonarr Server". Treat the "Default Server" as the [Standard](./sonarr#quality-profiles) quality profile.

- "Default Server" : Check box "Standard" Quality Profile.
- "4K Server" : Only checked for ["Ultra-HD"](./sonarr#quality-profiles) quality profile.
- "Server Name" : [`<Sonarr_Container_Name>`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/arrs/arrs.yaml#L22)
- "Hostname or IP Address" : `<Sonarr_Container_Name>`.
- "Port" : [`<Sonarr_Port>`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/arrs/arrs.yaml#L29)
- "Use SSL" : Uncheck
- "API Key" : [`<Sonarr_API_Key>`](./arr_family#generating-arr-api-keys)
- "URL Base" : Leave blank.
- "Quality Profile" : Select "Standard" when configuring "Default Server", else configure a Radarr Server for each "Quality Profile".
- "Root Folder" : [`/media`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/arrs/arrs.yaml#L33)`/tv`
- "Minimum Availability" : "Released"
- "Tags" : Empty.
- "External URL" : `https://<Jellyfin_Domain>.tld`
- "Enable Scan" : Check
- "Enable Automated Search" : Check
- "Tag Requests" : Check

- "Default Server" : Check box "Ultra-HD" Quality Profile.
- "4K Server" : Only checked for ["Ultra-HD"](./sonarr#quality-profiles) quality profile.
- "Server Name" : [`<Sonarr_Container_Name>`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/arrs/arrs.yaml#L22)
- "Hostname or IP Address" : `<Sonarr_Container_Name>`.
- "Port" : [`<Sonarr_Port>`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/arrs/arrs.yaml#L29)
- "Use SSL" : Uncheck
- "API Key" : [`<Sonarr_API_Key>`](./arr_family#generating-arr-api-keys)
- "URL Base" : Leave blank.
- "Quality Profile" : Select "Standard" when configuring "Default Server", else configure a Radarr Server for each "Quality Profile".
- "Root Folder" : [`/media`](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/arrs/arrs.yaml#L33)`/tv`
- "Minimum Availability" : "Released"
- "Tags" : Empty.
- "External URL" : `https://<Jellyfin_Domain>.tld`
- "Enable Scan" : Check
- "Enable Automated Search" : Check
- "Tag Requests" : Check

### Settings

These settings are available after initial configuration.

#### General

#### Users

#### Emby

See [above](#initial-setup-connect-to-jellyfin)

#### Services

See [above](#initial-setup-services)

#### Notifications

Not setup.

#### Jobs & Cache

Verify job execution times do not overlap with UnRaids [backup schedule](./tools#dynamix-schedules)

## Automated Install

Jellyseerr does not include any automated install methods out of the box.
