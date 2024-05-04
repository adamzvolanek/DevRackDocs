# BookStack

This page covers the setup of BookStack to deploy in my docker-compose stack(s). Likewise some investigation of configuration files to track and have deployable configuration on compose up.

Currently my primary page is using [WikiJS](./wikijs) due to its ability to leverage Git on the backend. However a BookStack version of my page can be viewed at [docs.adamzvolanek.com](https://docs.adamzvolanek.com).

## Upon Start

Address the PHP TimeZone [fix](https://github.com/linuxserver/docker-bookstack/issues/178).

- Login using admin default credentials, as of writing: `admin@admin.com` and a password of `password`.
- Click Admin drop-down and select 'My Profile'
  - Change the Name, Email, and update the Password.
    - Setup MFA
- Click the 'Settings' button and modify the settings as follows:
  - Check 'Allow public access'
  - Check 'Enable higher security image uploads'
  - Check 'Disable comments'
  - Click Save Settings
- Select Customization on the left
  - Modify the application name to `DevHub BookStack`
  - Modify the Default Page Editor to 'Markdown'
  - Click Save Settings
- Select Registration
  - Check 'Enable registration'
    - Select 'Public' as the 'Default user role after registration'
  - Check 'Require email confirmation'
  - Click Save Settings
- Select 'Users' and click 'Add New User'
  - Create your own user account (Name and Email)
  - Check 'Admin' and 'Editor'
  - Click Save

## BookStack Hierarchy

Proposed structure of Alexandria BookStack:

| Shelf     | Book              | Page                      | Page   |
|---------  |---------------    |-------------------------  |------- |
| DevRack   | Alexandria        | Installation Procedures   |        |
| DevRack   | Alexandria        | Backups                   | Various Backup Solutions |
| DevRack   | Alexandria        | Dockers                   | Various Docker Stacks |
| DevRack   | Alexandria        | Photopraphy               |        |
| DevRack   | Windows           | Windows 10 to 11 Upgrade  |        |
| Adam Zvolanek | About Me      | Hobbies                    | Photopraphy |

### Creation of Skeleton Structure

Select the 'Shelves' button and click 'Create one now'.

- DevRack
  - Description: Information about my primary server Alexandria.

Click 'Create New Book'

- Alexandria
  - Description: All things installation, backup, and other procedures as they relate to my server after the great library of Alexandria.

Note, at the book level you can create both chapters and pages.

Click 'Add a chapter'

- Installation Procedures
  - Description: A manually maintained repository of markdown installation procedures for Alexandria.

Click 'Create a new page' and copy/paste the various markdown files from [DevRackDocs](https://github.com/adamzvolanek/DevRackDocs) repository. Be sure to edit the Page name to align.

## Automated

Configuration likely to be sourced from skeleton structure of BookStack's database.
