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
