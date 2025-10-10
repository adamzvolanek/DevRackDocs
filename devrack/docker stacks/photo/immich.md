This page covers the setup of Immich to deploy in my docker-compose stack(s). The Immich instance will be a private (family) photo library.

[Immich Site](https://immich.app/)

## Setup

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

## Importing Photos

Use [Immich-Go](https://github.com/simulot/immich-go).

- On windows, downloaded the `immich-go_Windows_x86_64.zip`, extracted the zip.
- Opened cmd and navigated to photo location.
- Ran the following command in cmd. `C:\Users\<PATH>\immich-go_Windows_x86_64\immich-go -server=https://subdomain.adamzvolanek.com -key=<API_KEY> upload .`
  - Note the uploading content is *relative*  in the same location. Hence the `.`
  - Alternative: `C:\Users\<PATH>\immich-go_Windows_x86_64\immich-go -server=https://subdomain.adamzvolanek.com -key=<API_KEY> upload C:\path\to\photos`

## Automated

Can follow the `immich-config.json` provided in Git.

## Nginx Security

By default, Immich via Cloudflare does not have strong security headers. For additional context see [this](https://github.com/immich-app/immich/discussions/13043) GitHub thread.

1. Navigate to Nginx Proxy Manager and select the photos proxy host.
2. Select the Custom locations tab.
3. Add a `/` for the location.
4. Scheme: http
5. Forward Hostname `immich_server` (or same as your Immich container name if on the same docker network)
6. Forward Poprt: `2283` (or your Immich container port)
7. Select the cog wheel to the right of location.
8. Copy paste the following
   1. Replace `domain.tld` with respective domain.

      ```bash  
      # Protect against cross-site scripting and clickjacking attacks
      add_header X-Frame-Options "SAMEORIGIN" always;
      add_header X-Content-Type-Options "nosniff" always;

      # Prevent referrer leakage to third parties
      add_header Referrer-Policy "no-referrer-when-downgrade" always;

      # Control access to browser features
      add_header Permissions-Policy "geolocation=(), microphone=(), camera=()" always;

      ## Self + Trusted Domains Only (no hashes)
      add_header Content-Security-Policy "default-src 'self'; script-src 'self' https://subdomain.domain.tld https://static.immich.cloud https://tiles.immich.cloud https://www.gstatic.com 'unsafe-inline'; style-src 'self' 'unsafe-inline'; img-src 'self' data: blob:; connect-src 'self' https://subdomain.domain.tld https://tiles.immich.cloud https://static.immich.cloud https://www.gstatic.com; frame-ancestors 'self'; worker-src 'self' blob:; " always;

      # Upcoming Headers Configuration
      add_header Cross-Origin-Embedder-Policy "require-corp" always;
      add_header Cross-Origin-Opener-Policy "same-origin" always;
      add_header Cross-Origin-Resource-Policy "same-origin" always;
      ```
