# SFTPGO

This page covers the setup of [SFTPGO](https://sftpgo.com/) to deploy in my docker-compose cloud stack.

## Manual Steps

Create the admin account and populate the account credentials. You can setup 2FA at a later point.

### Virtual folders

- Click "Add"
  - Name: Server
  - Description: Alexandria
  - File system
    - Storage: Local disk
    - Root directory: `/cloud`

### Users

- Click "Add"
  - Username: *username*
  - Password: *password*
  - [X] Require password change
  - Delete public keys
  - Delete TLS certificate
  - File System
    - Storage: Local disk
    - Root directory: `/cloud/short_username`
  - Profile
    - Status: Active
    - Expiration: None
    - Email: *populate*
    - Password strength: 40
      - Means: 1 captial, 1 lower, 1 special
    - Password expiration: 0
    - Default shares expiration: 30
    - Maximum shares expiration: 0
    - Description: Full name.
  - ACLs
    - Require 2FA for: HTTP, SSH, FTP
