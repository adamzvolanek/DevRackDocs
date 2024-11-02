# Memos

This page covers the setup of [memos](https://www.usememos.com/).

## Manual Steps

### Administration

Initial splash page includes the sign-up page for the memo-admin account.

#### Settings

- Select Settings and System
  - Under Basic and click "Edit"
    - Server Name: `Memos - Alexandria`
    - Icon URL: None
    - Description: Self-Hosted Memos
    - Server Locale: English
    - Server Appearance: Follow system
  - [X] Disallow user registration
  - [ ] Disallow password auth
- Select Memo
  - [ ] Disable public memos
  - [X] Display with updated time
  - [X] Enable auto compact
  - [ ] Enable link preview
  - [x] Enable memo comments
  - [X] Enable double click to edit
  - Content length limit (Byte): 8192
  - Select "Save"
- Storage: Database
- Member
  - Create new users ad needed with appropriate user/admin roles.

## Automated

Put in as many environment variables to reduce manual setup.
