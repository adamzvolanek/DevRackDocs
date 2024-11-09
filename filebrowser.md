# FileBrowser

This page covers the setup of [filebrowser](https://github.com/filebrowser/filebrowser) to deploy in [my](https://github.com/adamzvolanek/DevRack/tree/main/docker-compose/cloud/filebrowser) filebrowser directory.

## Manual Steps

Prerequisites:

- A `settings.json` file.
  - See [here](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/cloud/filebrowser/settings.json)
- Create the config directory per [line 19](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/cloud/filebrowser/filebrowser.yaml#L19)
- Create/paste the `settings.json` file into the config directory. (`...cloud/filebrowser/config/`)

### Initial Setup of FileBrowser

- Settings
  - Profile Settings
    - [ ] Hide dotfiles
    - [ ] Use single clicks to open files and directories
    - [X] Set exact date format
    - Language: English
    - Change Password
      - Update your admin user password.
  - Global Settings
    - [X] Allow users to signup
    - [X] Auto create user home dir while adding new user
    - Base path for user home directories: `cloud/`
      - This reason for `cloud/` is due to the settings.json file including the root directory as `/unraid` already.
    - Branding
      - Instance name: {Server Name} File Browser
      - Branding directory path: `/branding`
      - [Docs for Custom Branding](https://filebrowser.org/configuration/custom-branding)
    - Chunked Uploads
      - Set to 75 MB
      - Number of retires... 5
  - User default settings
    - Scope: `.`
    - Language: English
    - Permissions:
      - [ ] Administrator
      - [X] Create files and directories
      - [X] Delete files and directories
      - [X] Download
      - [X] Edit files
      - [ ] Execute Commands
      - [X] Rename or move files and directories
      - [X] Share files
  - Command runner
    - Before Upload: `echo $USERNAME $FILE $SCOPE`
- User Management
  - Username: *UserName*
  - Password: *Password*
  - Scope: Leave empty.
  - [X] Create user home directory
  - Permissions leave default.

## Automated Setup

Leverage scripts using [FileBrowser CLI](https://filebrowser.org/cli).

Example script run in docker console: `filebrowser users ls --database=/database/filebrowser.db` however the database can only be accessed by a single resource at a time.

Possible work around when running on docker console:

```bash
#!/bin/bash

# Set the Docker container name for Filebrowser
CONTAINER_NAME="filebrowser"

# Define the paths to the filebrowser database inside the container
SOURCE_DB="/database/filebrowser.db"
TEMP_DB="/filebrowser-test.db"

# Step 1: Copy the filebrowser database to a temporary file
echo "Copying $SOURCE_DB to $TEMP_DB..."
docker exec "$CONTAINER_NAME" cp -rPp "$SOURCE_DB" "$TEMP_DB"

# Step 2: Run the `filebrowser users ls` command on the temporary database
echo "Listing users from $TEMP_DB..."
docker exec "$CONTAINER_NAME" filebrowser users ls --database="$TEMP_DB"

# Step 3: Clean up and delete the temporary database
echo "Deleting $TEMP_DB from the Docker container..."
docker exec "$CONTAINER_NAME" rm "$TEMP_DB"

# Optionally, you can remove the local copy of the temporary database if you no longer need it
# rm "$TEMP_DB"

echo "Script execution completed."
```
