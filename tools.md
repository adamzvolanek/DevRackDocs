# Tools

This page covers the setup of tools & plugins used on the Alexandria (Unraid) server.

## Plugins

### Appdata Backup/Restore v2.5

Setup the Appdata Backup/Restore Plugin as follows.

- Appdata Share (Source): `/mnt/cache/appdata/`
- Destination Share: `/mnt/user/backups/Unraid/CA_Backup/Appdata _Backup`
- Excluded Folders: `/mnt/cache/appdata/.Recycle.Bin/,/mnt/cache/appdata/.Trash-99/,/mnt/cache/appdata/Downloads/,/mnt/cache/appdata/jellyfin/metadata,/mnt/cache/appdata/binhex-minecraftserver,/mnt/cache/Downloads,/mnt/cache/appdata/binhex-lidarr/MediaCover,/mnt/cache/appdata/Jellyfin/trancodes,/mnt/cache/appdata/Jellyfin/metadata
- Use Compression? No
- Verify Backups? Yes
- Ignore errors during backup? No
- Create separate archives (one per folder)? No

USB Backup Settings

- USB Backup Destination: `/mnt/user/backups/Unraid/CA_Backup/FlashDrive_Backup/`
- libvirt.img Destination: `/mnt/user/backups/Unraid/CA_Backup/libvirt_Backup/`
- Notifications Settings: Error Only
- Time to wait when stopping app before killing: 60
- Delete backups if they are this many days old: 180
- Scheduled Backup Frequency: Monthly
- Day of Week: Monday
- Day of Month: 13th
- Hour: 1
- Minute: 0

### Dynamix File Integrity

- Placement of file integrity control: Header menu
- Automatically protect new and modified files: Enabled
- Hashing method: MD5
- Save new hashing results to flash: Disabled
- Excluded folders and files: Scratch
  - Custom folders: `/mnt/disk2/system/libvirt/libvirt.img, /mnt/user/media`
  - Custom files: `.Recycle.Bin,*.nfo,*.log,*.xml`
- Disk verification schedule: Weekly
- Process priority: Low
- When parity operation is running: Don't start
- Day of the week: Sunday
- Time of the day: 01
- Send notifications: Yes
- Error Logging: Syslog & Output file

### Dynamix Schedules

- Verify you are comfortable with timing of fixed scheduled items.
  - Hourly: 0:20 of the hour
  - Daily: 3:30 am
  - Weekly: 4:00 am on a Sunday
  - Monthly: 4:30 am on the 1st of every month.

### Appdata Cleanup

No setup required.

### Community Applications

- Hide Deprecated Applications: Yes
- Hide Incompatible Applications: Yes
- Allow install of second instance: No
- Automatically open the sidebar: Yes
- Allow CA to check for updates to applications: Yes
- Allow CA to send any emergency notifications: Yes
- Save CA debugging information: No
- Enable developer mode: Yes

### Docker Compose Manager

- Compose Command Progress Display: Terminal
- Debug Logging: Disabled
- Patch unRAID WebUI: No

### Nvidia-Driver

The runtime settings:

- Vendor: NVIDIA
- Unit ID for Dashboard: 0:....
- Temperature Format: Celsius
- UI Automatic Refresh / Interval (Milliseconds): Yes, 1000

All remaining settings are setup as 'Yes'.

### Recycle Bin

- Enable Recycle Bin? Yes
- Update Recycle Bin Size in Background? Yes
- Enable on Unassigned Devices? No
- Recycle Bin permissions: `0777`
- Excluded Files: `*.tmp`
- Age Days: 30
- Remove Aged Files on Schedule? Weekly
- Remove Aged Files Notification? Yes
- Log Deleted Files? Yes

### Dynamix System Stats

- Placement of Stats menu: Header menu
- Opening page: System Stats
- Position of disk utilization percentage: Right
- Viewable system graphs: (All)
- CPU graph scaling: Automatic
- System graphs view per row: Pair
- Show disk size: Yes
- Ethernet interface: eth0
- Network graph display unit: Bits per second
- Initial graphing mode: Real-time
- Initial real-time sliding window: 1 hour

### Dynamix System Info

No setup required.

### File Activity

Enable for troubleshooting if needed.

### Network/GPU Stats

No setup required.

### rclone

Setup for B2, Google Drive, and Local pending instructions.

### Theme Engine

Truly preference in terms of setup.

### Tips and Tweaks

Pending

### Unassigned Devices / Plus (Add-on) / Preclear

Common Settings:

- Destructive Mode: Enabled
- Auto Mount USB Devices: Yes
- Mount SSDs with 'discord' option? Yes
- Legacy Mount Point Compatibility? No
- Specify SMB Version when Mounting Remote Shares? No
- NFS Version to use when Mounting Remote Shares: NFSv4
- Debug Log Level: None

SMB Settings:

- SMB Sharing: Disabled
- Case-sensitive names: Auto
- Add 'force user = nobody' to SMB share config: No

NFS Settings:

- Enable NFS export? No
- NFS Security: Public

### unBalance

Enable unBALANCE Server: Yes

### User Scripts

#### `delete_dangling_images`

Script deletes any 'dangling' images within your docker.img file.

- Scheduled Monthly

```bash
#!/bin/bash

docker rmi $(docker images --quiet --filter "dangling=true")

echo Finished
echo if an error shows above, no dangling images were found to delete
```

#### `delete.ds_store`

Deletes all .DS_Store files on array created by Apple's Finder.

- Scheduled Monthly

```bash
#!/bin/bash
echo "Searching for (and deleting) .DS_Store Files"
echo "This may take a awhile"
find /mnt/user -maxdepth 9999 -noleaf -type f -name ".DS_Store" -exec rm "{}" \;
```

#### `Network Routing`

Runs on boot to change default route.

Script location: `/boot/config/plugins/user.scripts/scripts/Networking`

```bash
#!/bin/bash
ip route add default via 192.168.1.1 dev br0
```
