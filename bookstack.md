# BookStack

This page covers the setup of BookStack to deploy in my docker-compose stack(s). Likewise some investigation of configuration files to track and have deployable configuration on compose up. This procedure has been **deprecated** and instead using WikiJS.

## Upon Start

- Login using admin default credentials, as of writing: `admin@admin.com` and a password of `password`.
- Click Admin drop-down and select 'Edit Profile'
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

Proposed structure of Adam's BookStack:

| Shelf     | Book              | Chapter/Page              | Page              |
|---------  |---------------    |-------------------------  |-----------------  |
| HomeLab   | Alexandria        | Installation Procedures   | Specific Stacks   |
| HomeLab   | Alexandria        | Backup Procedures         | Specific Stacks   |
| AboutMe   | Adam Zvolanek     | Hobbies                   |                   |

### Creation of Skeleton Structure

Select the 'Shelves' button and click 'Create one now'.

- HomeLab
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
