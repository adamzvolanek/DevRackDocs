This page covers the setup of [filebrowser](https://github.com/gtsteffaniak/filebrowser) to deploy in [my](https://github.com/adamzvolanek/DevRack/tree/main/docker-compose/cloud/filebrowser) filebrowser directory.

[Filebrowser Quantum Website](https://filebrowserquantum.com/en/)

## Setup

Prerequisites:

- A `config.yaml` file.
  - See [config.yaml](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/cloud/filebrowser-quantum/config.yaml)
- Create the config directory per [line 19](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/cloud/filebrowser/filebrowser.yaml#L19)
- Create and paste the `config.yaml` file into the filebrowser-quantum/config directory.
- Create and modify the permissions of the filebrowser-quantum/data and filebrowser-quantum/tmp directories to 755 with uid:gid of 1000.

### Initial Setup of FileBrowser

1. Login to FileBrowser Quantum docker container and enter the default admin credentials defined in the `config/config.yaml` file: admin123!.
   1. **Remember to change the admin password after instance creation**
2. Upon login, select 'Login to Alexandria' on the prompt.
3. Select **Acknowledge** on the "Welcome to FileBrowwer Quantum" popup that describes a new database was created on startup...
4. Select the admin's cog wheel (Settings For User) at the top left and click **Access Management**.
   1. Click **New** at the bottom right and click the Deny drop-down and select **Allow**.
   2. Enter "admin" into the field.
   3. Click the **+** symbol.
   4. Close the window and select the **x** at the top left.
5. Click "Profile Settings".
   1. Enable the following features in Listing options:
      1. Set exact date format.
      2. Show hidden files.
      3. Show download icon for quick access.
   2. Disable the following features in Thumbnail Options:
      1. Motion previews.
      2. Select "Save".
6. Click **Uploads & Downloads**
   1. Change max concurrent uploads to 5.
   2. Change "Download chunk size in MB" to 10.
   3. Click **Save**
7. Click "Notifications"
   1. Clear all notifications.

### Creating an account

1. Create the (new) user's folder in the `/cloud`.
2. Select the admin's cog wheel at the top left and click **User Management**.
   1. Click **New** at the bottom right.
      1. Enter a username.
      2. Enter a password twice.
      3. Under "Defined allowed sources and user scope within them", ensure "Alexandria Cloud" is selected and select the users directory in `/`.
      4. Review the permissions for the *user*.
      5. Select "Save".
      6. Enter *admin password* and click **Confirm**.
3. Select **Access Management**
   1. Click **New**.
   2. Click on **Path: /** and select the users respective directory. Click "OK".
   3. Click the Deny drop-down and select **Allow**.
   4. Enter the *username* into the field.
   5. Click the **+** symbol.
4. User can now sign in to Alexandria Cloud.
