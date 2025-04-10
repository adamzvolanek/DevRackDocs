This page covers the setup of [jellyseerr](https://github.com/fallenbagel/jellyseerr) to deploy in my docker-compose stack(s).

## Setup

### Server Type and Sign In

1. Select "Configure Jellyfin" as the server type.
2. Check "Use SSL"
3. Enter (internal) JellyFin URL, `http://IP:[PORT]`
   1. Verify port, default is 443.
4. Leave URL Base blank.
5. Enter email.
6. Enter JellyFin account username.
   1. Ensure user has permissions to generate API Keys on JellyFin.
7. Enter JellyFin account password.

### Configure Media Server

1. Select "Sync Libraries" and turn on your respective libraries for scanning.
2. Take note of the API key, it should match one generated on JellyFin.
3. Populate External URL with `https://subdomain.domain.tld`
4. Optionally provide a Forgot Password URL.

### Configure Services

For Radarr

1. Select "Add Radar Server"
2. Check "Default Server"
3. Leave 4K un-checked.
   1. Separate profile will be created later.
4. Server Name: "Radarr"
5. Hostname or IP address: `radarr`
   1. For docker deployments of dockers in the same network
6. Port: Verify the port is correct.
7. **Uncheck** Use SSL
8. Populate a Radarr API key.
9. URL Base: blank
10. Quality Profile: Standard
    1. Select one to associate for standard movie requests.
11. Root Folder: `/media/movies`
12. Minimum Availability: "Released"
13. External URL: blank
14. Check "Enable Scan"
15. Check "Enable Automatic Search"
16. Check "Tag Requests"
17. Select "Test"

Repeat the steps above for 4K with the following changes:

1. Check "4K Server"
2. Update Server Name "Radarr 4K"
3. Update Quality Profile to "Ultra-HD"

For Sonarr

1. Select "Add Radar Server"
2. Check "Default Server"
3. Leave 4K un-checked.
   1. Separate profile will be created later.
4. Server Name: "Sonarr"
5. Hostname or IP address: `sonarr`
   1. For docker deployments of dockers in the same network
6. Port: Verify the port is correct.
7. **Uncheck** Use SSL
8. Populate a Sonarr API key.
9. URL Base: blank
10. Quality Profile: Standard
    1. Select one to associate for standard movie requests.
11. Root Folder: `/media/tv`
12. Anime Series Type: "Standard"
13. Anime quality Profile: "Standard"
14. Anime Root Folder: `/media/tv`
15. External URL: blank
16. Check "Enable Scan"
17. Check "Enable Automatic Search"
18. Check "Tag Requests"
19. Select "Test"

Repeat the steps above for 4K with the following changes:

1. Check "4K Server"
2. Update Server Name "Sonarr 4K"
3. Update Quality Profile to "Ultra-HD"

## General Setup

### General Tab

1. Application Title: `Jellyseerr`.
2. Application URL: `https://subdomain.domain.tld`.
3. Check "Enable Proxy Support"
4. Check "Enable CSRF Protection"
5. Uncheck "Enable Image Caching"
6. Display Language: English
7. Discover Region: All Regions
8. Discover Language: All Languages
9. Streaming Region: United States
10. Uncheck "Hide Available Media"
11. Check "Allow Partial Series Requests"
12. Uncheck "Allow Special Episodes Requests"
13. Check "IPv4 Resolution First"
14. Custom DNS Servers: Populate with DNS Server IP

### Users Tab

1. Check "Enable local Sign-In"
2. Check "Enable New Jellyfin Sign-in"
3. Global Movie Request Limit: 3 movies per 14 days
4. Global Series Request Limit: 1 season per 14 days
5. Default Permissions:
   - [ ] Manage Users
   - [ ] Manage Requests
     - [ ] Advanced Requests
     - [X] View Requests
     - [X] View Recently Added
     - [ ] View Jellyfin Watchlists
   - [X] Request
   - [X] Auto-Approve
   - [ ] Auto-Request
   - [X] Request 4K
   - [ ] Auto-Approve 4K
   - [ ] Manage Issues
     - [ ] Report Issues
     - [X] View Issues
   - [ ] Manage Blacklist
     - [ ] View blacklisted media.

## Users

This section covers the Users section above the large Settings of Jellyseerr.

1. Select "Import Jellyfin Users"
2. Select the slider at the top to import all Users.
