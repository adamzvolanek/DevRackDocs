This page covers the setup of [syncthing](https://github.com/linuxserver/docker-syncthing) to deploy in my docker-compose stack(s). Syncthing is setup as a (conceptually) different approach to a "cloud" server, replacing NextCloud in favor for local storage.

Syncthing can be deployed on mobile phones and laptops.

# Setup

## Settings

Navigate to the Actions at the top right and select "Settings".

- Change device name to server name, "Alexandria".
- Under Default Configuration select "Edit Folder Defaults"
  - Under Folder Path, enter `/storage/`
    - (If on Windows) Under Folder Path, enter `C:\Syncthing`
- Navigate to the GUI Tab
  - Replace GUI Listen Address with server IP
  - Create GUI Authentication User and Password
- Navigate to the Advanced tab
  - [X] "Sync Ownership"
    - [ ] (If on Windows) "Sync Ownship"
  - [X] "Ignore permissions"
    - [ ] (If on Windows) "Ignore Permissions"
  - Select "Save"
- Select "Actions" then "Advanced"
  - Select "Default Ignore Patterns"
    - Add `.Recycle.Bin`

These steps need to be repeated for each new device added.

### Adding Folder(s)

On the main page, select "Add Folder".

Under the General tab add the following:

- Folder Label: (mounted volumes within the `/storage/`|`C:\Syncthing` directory)
- Folder ID: (mounted sub-directory volume)
- Folder Path: `/storage/`(mounted volume name)
  - (If on Windows) Folder Path: `C:\Syncthing\`(Folder Name)
- Select "Save"

### Connecting Devices

Select Actions and then "Show ID". Copy the ID Hash to use on Device. Local Discovery may show other devices if adding a n+1 device.

(On Android) Select the + symbol at the top-right and paste in the copied DeviceID. Provide a Name for the device on the phone and once done tap the check-mark at the top-right. Allow a few minutes to pass monitoring original device. (Alexandria)

Click "Add Device" once new device name appears at the top. Once added, additional confirmation of DeviceName is provided and will begin to appear under "Remote Devices".

### Sharing Folders

Select "Edit" on the Remote Device. Under the Sharing tab, check the box for the "Unshared Folders" you want to share.

- [X] Auto Accept
  - Use this setting with caution. Only "Auto Accept" for devices you expect Folders should be created *from*.

A notification will appear to Accept or Ignore a shared folder. The prompt will ask you to designate a folder on the device to use. Best practice is to label the folder the same as the folder on Alexandria. Create a Syncthing folder on the Android device, within *it* create the shared folder. Select the checkmark at the top-right to confirm all settings.
