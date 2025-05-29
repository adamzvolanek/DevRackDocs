This page covers the setup of BookStack to deploy in my docker-compose stack(s). Likewise some investigation of configuration files to track and have deployable configuration on compose up.

## Upon Start

Address the PHP TimeZone [fix](https://github.com/linuxserver/docker-bookstack/issues/178).

- Login using admin default credentials, as of writing: `admin@admin.com` and a password of `password`.
- Click the 'Settings' button and modify the settings as follows:
  - [X] Allow public access
  - [X] Enable higher security image uploads
  - [ ] Disable comments
  - Click Save Settings
- Select Customization on the left
  - Modify the application name to `DevRack BookStack`
  - Modify the Default Page Editor to 'Markdown'
  - Edit Application logo and Application Icon to Docs asset.
  - Footer Links
    - Enter `[WikiJS Version](https://wiki.adamzvolanek.com)`
    - Enter `[DevRack Docs Repo](https://github.com/adamzvolanek/DevRackDocs)`
    - Enter `[DevRack Repo](https://github.com/adamzvolanek/DevRack)`
    - Enter `[Photos](https://www.instagram.com/zvolanek.photography/)`
  - Click Save Settings
- Select Registration
  - [ ] Enable registration
    - Select 'Public' as the 'Default user role after registration'
  - Check 'Require email confirmation'
  - Click Save Settings

## Users

Select the Admin role.

Update the email from default, password, and user avatar. Setup both MFA methods.

## Roles

Select Public to teh following Asset Permissions.

- [X] (Create) Comments
- [X] (Edit) Own
- [ ] (Edit) All
- [X] (Delete) Own
- [ ] (Delete) All

## Setup with Authentik

Currently not setup. [Setup Link](https://docs.goauthentik.io/integrations/services/bookstack/)

## Webhooks

- [X] Webhook Active
- Webhook Name: `Alexandria Discord`
- Webhook Endpoint: https://discord.com/api/webhooks/...
- Webhook Request Timeout (Seconds): `5`
- Webhook Events
  - [X] page_create
  - [X] page_update
  - [X] chapter_update
  - [X] book_update
- Save Webhook.

## BookStack Hierarchy

Proposed structure of Alexandria BookStack:

| Shelf     | Book              | *Chapter(s)* and Page(s)          | Page(s)                  |
|---------- |------------------ |---------------------------------- | ------------------------ |
| DevRack   | Backups           | Alexandria, Authentik...          |                          |
| DevRack   | Docker Stacks     | Docker Stacks and *Docker Family* | Docker Stacks            |
| DevRack   | Windows           | Various Windows Related Pages     | Various Docker Stacks    |
| DevRack   | Unraid            | Various Unraid Related Pages      |                          |
| About Me  | Adam Zvolanek     | Various Pages                     |                          |
