# Docker Backup

This page covers the backup procedure for my docker containers running on Unraid. This process acts as a last resort of restoration where all dockers are backed up at once and all restored at once.

Appdata backups that are 15 days or older are deleted, an output log file is created in `/mnt/user/backups/Unraid/CA_Backup/Appdata_Backup/` to verify run.

## Configuration

Install the [CA Appdata Backup v2.5](https://forums.unraid.net/topic/132721-plugin-ca-appdata-backup-restore-v25/) on Unraid.

- Appdata Share: `/mnt/user/appdata/`
- Destination Share: `/mnt/user/backups/Unraid/CA_Backup/Appdata_Backup`
- Excluded Folders: `/mnt/cache/appdata/.Recycle.Bin/,/mnt/cache/appdata/.Trash-99/,/mnt/cache/appdata/Downloads/,/mnt/cache/appdata/jellyfin/metadata,/mnt/cache/appdata/binhex-minecraftserver,/mnt/cache/Downloads,/mnt/cache/appdata/binhex-lidarr/MediaCover,/mnt/cache/appdata/Jellyfin/trancodes,/mnt/cache/appdata/Jellyfin/metadata,/mnt/cache/appdata/photoprism/cache/,/mnt/cache/appdata/photoprism_external/cache/`
- Use Compression: No
- Verify Backups? Yes
- Ignore errors during backup? No
- Create separate archives (one per folder): No
- USB Backup Destination: `/mnt/user/Backups/Unraid/CA_Backup/FlashDrive_Backup/`
- livirt.img Destination: `/mnt/user/Backups/Unraid/CA_Backup/libvirt_Backup/`
- Notification Settings: 'Errors Only'
- Path to Custom Stop Script: 
- Path to Custom Pre-start Script: `/mnt/user/DevRack/DevRack/scripts/clear_15day_appdata_logged.sh`
- Path to Custom Start Script:
- Update Applications On Restart? No
- Time to wait whenstopping app before killing: `60`
- Delete backups if they are this many days old: `180`
- Scheduled Backup Frequency: `Daily`
- Day of Week: Monday
- Day of Month: 13
- Hour: `2`
- Minute: `45`

Backups are placed daily to `backups/Unraid/CA_Backup/Appdata_Backup`

## Restoring

To restore via a backup, navigate to `alexandria/Settings/BackupMainV2/` and select the 'Restore Appdata' tab.

Verify the 'Source Directory' and 'Destination Directory' match the configuration above and options should appear as a drop-down to 'Select a Backup Set to Restore'.

Select a backup and click 'Restore'.
