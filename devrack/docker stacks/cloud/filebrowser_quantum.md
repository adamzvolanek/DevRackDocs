This page covers the setup of [filebrowser](https://github.com/gtsteffaniak/filebrowser) to deploy in [my](https://github.com/adamzvolanek/DevRack/tree/main/docker-compose/cloud/filebrowser) filebrowser directory.

[Filebrowser Quantum Website](https://filebrowserquantum.com/en/)

## Setup

Prerequisites:

- A `config.yaml` file.
  - See [config.yaml](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/cloud/filebrowser-quantum/config.yaml)
- Create the config directory per [line 19](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/cloud/filebrowser/filebrowser.yaml#L19)
- Create and paste the `config.yaml` file into the filebrowser-quantum/config directory.

### Initial Setup of FileBrowser

1. Login to FileBrowser Quantum docker container as admin and enter the default admin credentials defined in the `config/config.yaml` file: admin123!.
2. Upon login, select Okay on the prompt.
3. Select the admin's cog wheel (Settings For User) at the top left and click **Access Management**.
   1. Click **New** and click the Deny drop-down and select **Allow**.
   2. Enter "admin" into the field.
   3. Click the **+** symbol.
4. Click "Profile Settings".
   1. Enable the following features in Listing options:
      1. Set exact date format
      2. Show hidden files
      3. Show download icon for quick access
5. Click **Uploads & Downloads**
   1. Change max concurrent uploads to 5.
   2. Change "Download chunk size in MB" to 10.
   3. Click **Save**
6. Click "Notifications"
   1. Clear all notifications.

### Creating an account

1. Select the admin's cog wheel at the top left and click **Access Management**.
2. Select **User Management**
   1. Click **New**
      1. Enter a username.
      2. Enter a password twice.
      3. Enter "allowed sources and user scope..." and the subfolder as it related to the *user*.
      4. Review the permissions for the *user*.
3. Select **Access Management**
   1. Click **New** and click the Deny drop-down and select **Allow**.
   2. Enter the *username* into the field.
   3. Toggle **Recursive Delete**
   4. Click the **+** symbol.
