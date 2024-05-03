# FileBrowser

This page covers the setup of [filebrowser](https://github.com/filebrowser/filebrowser) to deploy in [my](https://github.com/adamzvolanek/DevRack/tree/main/docker-compose/cloud/filebrowser) filebrowser directory.

5/02/2024: FileBrowser use has been stopped.

## Manual Steps

Prerequisites:

- A `settings.json` file.
  - See [here](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/cloud/filebrowser/settings.json)
- Create the config directory per [line 19](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/cloud/filebrowser/filebrowser.yaml#L19)
- Create/paste the `settings.json` file into the config directory.

### Initial Setup of FileBrowser

Navigate to Settings --> Global Settings

- [ ] Allow users to signup
- [X] Auto create user home dir while adding new user
- Base path for user home directories: `/unraid/`
  - Using this path assumes "shares" of the same name as the user. Case-sensitive.

Under Chunked Uploads, update the file to read: 50 MB.

To Do:

- Rules?
- Branding
- Nginx
