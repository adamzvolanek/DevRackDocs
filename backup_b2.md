# BackBlaze B2 Backup

This page covers the backing up of my server to BackBlaze B2 using RClone.

## Bucket Setup

Name the buckets using the following nomenclature: `shareName-serverName-os-region`. I am not including an environment portion due to the cloud backup only applying to the main server.

Create buckets to match the Unraid User Shares using the nomenclature.

Review the Lifecycle settings for each bucket to have appropriate settings, by default buckets should utilize the "Keep only the last version of the file:". If data needs to be kept, use "Keep prior versions for this number of days:" and enter the number of appropriate days. Entering the number of days utilizes the `daysFromHidingToDeleting`: `30` as noted [here](https://www.backblaze.com/docs/cloud-storage-lifecycle-rules).

## RClone Setup

Ensure you have Waseh's rclone plugin installed.

Create a local remote using `rclone config` in the terminal and follow the prompts. Name the remote as `local_backup`. 

Create a remote for backblaze with an application key.

- After typing `rclone config`, enter `n` for new remote
- Enter the name of the new remote, `b2_buckets`.
- Select the option for BackBlaze, option 6 for version when written.
- Enter the Application Key ID
- Enter the Application Key
- Select no for 'hard_delete'
- Select n for 'advanced config'

## Backup Scripts

Ensure you have Squid's 'User Scripts' installed prior to continuing.

During testing, the following script was created to rclone to a temporary bucket:

```bash
https://github.com/adamzvolanek/DevRack/blob/main/scripts/backblaze_scripts/backup-shareName-b2-bucketName.sh
```

Create a script for each share's backup following the script nomenclature, `function-shareName-destination-bucketName`. This results in a script name like, `backup-b2-{bucketName}'.

Review the rclone global flags [here](https://rclone.org/flags/).

Add a description to the script putting in words what the script is doing.

Repeat the creation of scripts for each Unraid share.

Setup scripts cadence to run to your desired liking. Currently personal shares are running daily with others running weekly. One share includes a custom cron job to run daily to align with other backup processes. The current setup of hourly, daily, weekly, and monthly cadence can be viewed in the [tools](./tools.md) file under 'Dynamix Scheduler'. At time of writing cadence is outlined as follows:

- Hourly: 0:20 of the hour
- Daily: 3:30 am
- Weekly: 4:00 am on a Sunday
- Monthly: 4:30 am on the 1st of every month.

Backups for user shares, critical data, and designated backups are scheduled daily. Backups of other users is weekly. Recall Community Applications Appdata (v2.5) occurs at 02:45 am daily allowing backups to pickup changes there after.

## Cloud Drive Sync

Uses Bisync [docs](https://rclone.org/bisync/) and runs on a custom cron schedule of `*/15 * * * *`.
