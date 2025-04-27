This page covers the setup of [Jellyseer](https://github.com/Fallenbagel/jellyseerr) to deploy in [my](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/external/jellyseerr.yaml) docker-compose stack(s).

# Setup

Prerequisites:

- A Jellyfin instance running with [Nginx configured](./nginx_proxy_manager)
- Radarr instance running and configured per [radarr](./radarr)
- Sonarr instance running and configured per [sonarr](./sonarr)

## Initial Setup Connect to JellyFin

On connecting to docker container, select the "Use your Jellyfin account", and input your Jellyfin's information:

- "Jellyfin URL" : `https://<Jellyfin_Domain>.tld`
- "Email Address" : `email@domain.tld` (As noted, does not have to be associated with server)
- "Username" : `JellyFin Admin Username`
  - Utilize a JellyFin admin account username here on creation
- "Password" : `JellyFin Admin Password`

## Initial Setup Jellyseerr

On step 2 of "Configure Media Server" click on "Sync Libraries" and select your applicable libraries. Upon selecting the libraries select "Next".

## Initial Setup Services

### Arrs

**Radarr**

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

## Settings

These settings are available after initial configuration. They can be found by navigating to `<jellyseer_instance/settings/main>`.

### General

- "Application URL" : Populate with instance URL if desired, `subdomain.domain.tld`
- "Enable Proxy Support" : Check
- "Enable CSRF Protection" : Unchecked
- "Enable Image Caching" : Unchecked
- "Display Language" : "English"
- "Discover Region" : "All Regions"
- "Discover Language" : "All Languages"
- "Hide Available Media" : Unchecked
- "Allow Partial Series Requests" : Check

### Users

This view depends on the user currently logged in, instructions are written under the assumption you are logged in as the Jellyseer admin.

<details><summary>Settings/Users Settings</summary>

- "Enable Local Sign-in" : Checked
- "Enable New Emby Sign-In" : Unchecked
- "Global Movie Request Limit" : "Unlimited"
- "Global Series Request Limit" : "Unlimited"
- "Default Permissions" :
  - [ ] Manage Users
  - [ ] Manage Requests
    - [ ] Advanced Requests
    - [X] View Requests
    - [ ] View Recently Added
    - [ ] View Plex Watchlists
- [X] Request
- [ ] Auto-approve
  - [ ] Auto-Approve Movies
  - [ ] Auto-Approve Series
- [ ] Auto-Request
  - [ ] Auto-Request Movies
  - [ ] Auto-Request Series
- [X] Request 4K
  - [X] Request 4K Movies
  - [X] Request 4K Series
- [ ] Auto-Approve 4K
  - [ ] Auto-Approve 4K Movies
  - [ ] Auto-Approve 4K Series
- [X] Manage Issues
  - [X] Report Issues
  - [X] View Issues

</details>

### Jellyfin

See [above](#initial-setup-connect-to-jellyfin) additional Jellyfin Settings.

- "Internal URL" : `<subdomain.domain.tld>` (External JellyFin URL)
- "External URL" : `<subdomain.domain.tld>` (External JellyFin URL)

### Services

See [above](#initial-setup-services)

### Network

- [X] Enable Proxy Support
- [X] Enable CSRF Protection
- [ ] HTTP(S) Proxy

Advanced Network Settings

- [X] Force IPv4 Resolution First

### Notifications

Select Discord

- [X] Enable Agent
- Webhook URL: `https://discord.com/api/webhooks...`
- Bot Username: Jellyseerr
- Bot Avatar URL: jellyseerr-logo
- Notification Role ID: User "User" role ID to notify.
- [ ] Enable Mentions
- [X] Request Pending Approval
- [ ] Request Automatically Approved
- [X] Request Approved
- [ ] Request Denied
- [X] Request Available
- [X] Request Processing Failed
- [X] Issue Reported
- [ ] Issue Comment
- [X] Issue Resolved
- [ ] Issue Reopened

Select "Test" to verify Webhook is working; Select "Save Changes".

### Jobs & Cache

Verify job execution times do not overlap with UnRaids [backup schedule](./tools#dynamix-schedules)

## Tips & Fixes

- Access Denied Error
  - Turn off Overseer instance so DB is not in use
  - Installed a SQLite DB editor on my local system. For me I used DB Browser for SQLite on my mac
  - Copied just the main db.sqlite3 file to my local system. This might not be necessary, but it did it
  - Opened db.sqlite3 in my SQLite editor
  - Navigated to the user db table
  - Found my user and updated the missing plexId with the correct ID (I personally found this value in my tautulli database. I assume there are other places to find this Id as well
  - Saved my change to the row. When I did this, 2 other files were generated in the location I had copied the db.sqlite3 file, they were db.sqlite3-shm and db.sqlite3-wal.
  - I backed up all 3 of these files in the overseer db folder (into a new backup directory outside of the db folder)
  - I then replaced all 3 of these files with my new copies
  - I started overseer again and the problem was resolved.”
