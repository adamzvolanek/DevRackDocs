# Tools

This page covers the setup of tools used on the Alexandria server.

# Plugins

## Appdata Backup/Restore v2.5

Setup the Appdata Backup/Restore Plugin as follows.

- Appdata Share (Source): `/mnt/cache/appdata/`
- Destinatinon Share: `/mnt/user/Backups/Unraid/CA_Backup/Appdata _Backup`
- Excluded Folders: `/mnt/cache/appdata/.Recycle.Bin/,/mnt/cache/appdata/.Trash-99/,/mnt/cache/appdata/Downloads/,/mnt/cache/appdata/jellyfin/metadata,/mnt/cache/appdata/binhex-minecraftserver,/mnt/cache/Downloads,/mnt/cache/appdata/binhex-lidarr/MediaCover,/mnt/cache/appdata/Jellyfin/trancodes,/mnt/cache/appdata/Jellyfin/metadata,/mnt/cache/appdata/photoprism/cache/,/mnt/cache/appdata/photoprism_external/cache/`
- Use Compression? No
- Verify Backups? Yes
- Ignore errors during backup? No
- Create separate archives (one per folder)? No

USB Backup Settings

- USB Backup Destination: `/mnt/user/Backups/Unraid/CA_Backup/FlashDrive_Backup/`
- libvirt.img Destination: `/mnt/user/Backups/Unraid/CA_Backup/libvirt_Backup/`
- Notifications Settings: Error Only
- Time to wait when stopping app before killing: 60
- Delete backups if they are this many days old: 180
- Scheduled Backup Frequency: Monthly
- Day of Week: Monday
- Day of Month: 13th
- Hour: 1
- Minute: 0

## Dynamix File Integrity

- Placement of file integrity control: Header menu
- Automatically protect new and modified files: Enabled
- Hashing method: MD5
- Save new hashing results to fhash: Disabled
- Excluded folders and files: Scratch
  - Custom folders: `/mnt/disk2/system/libvirt/libvirt.img, /mnt/user/Movies, /mnt/user/TV_Shows`
  - Custom files: `.Recycle.Bin,*.nfo,*.log,*.xml`
- Disk verification schedule: Weekly
- Process priority: Low
- When parity operation is running: Don't start
- Day of the week: Sunday
- Time of the day: 01
- Send notifications: Yes
- Error Logging: Syslog & Output file

## Appdata Cleanup

No setup requried.

## Community Applications

- Hide Deprecated Applications: Yes
- Hide Incompatible Applications: Yes
- Allow install of second instance: No
- Automatically open the sidebar: Yes
- Allow CA to check for updates to applications: Yes
- Allow CA to send any emergency notifications: Yes
- Save CA debugging information: No
- Enable developer mode: Yes

## Docker Compose Manager

- Compose Command Porgress Display: Terminal
- Debug Logging: Disabled
- Patch unRAID WebUI: No

## Nvidia-Driver

The runtime settings:

- Vendor: NVIDIA
- Unit ID for Dashboard: 0:....
- Temperature Format: Celcius
- UI Automatic Refresh / Interval (Milliseconds): Yes, 1000

All remaning settings are seupt as 'Yes'.

## Recycle Bin

- Enable Recycle Bin? Yes
- Update Recycle Bin Size in Background? Yes
- Enable on Unassigned Devices? No
- Recycle Bin permissions: `0777`
- Excluded Files: `*.tmp`
- Age Days: 30
- Remove Aged Files on Schedule? Weekly
- Remove Aged Files Notification? Yes
- Log Deleted Files? Yes

## Dynamix System Stats

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

## Dynamix System Info

No setup required.

## Dynamix WireGuard

Pending.

## File Activity

Enable for troubleshooting if needed.

## Network/GPU Stats

No setup requried.

## rclone

No setup requried. Installed as support for dockers.

## Theme Engine

Truly preference in terms of setup.

## Tips and Tweaks

Pending

## Unassigned Devices / Plus (Addon) / Preclear

Pending

## unBalance

Enable unBALANCE Server: Yes

## User Scripts

No setup require.
