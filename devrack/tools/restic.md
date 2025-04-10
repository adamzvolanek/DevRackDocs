This page covers the setup of [backrest](https://github.com/garethgeorge/backrest).

The idea of this restic implementation is to have daily backups (via backup plan) of various "respositories" shares for up to 30 days prior.

Can have mulitple paths per repository.

## Setup

[Page referenced](https://garethgeorge.github.io/backrest/introduction/getting-started)

- Instance ID: `serverName-backrest`
- Disable authentication
  - Local only tool

BackBlaze B2 bucket should be named, `restic-shareName-serverName-serverOS-region`.

### Repository Setup

Verify a B2 bucket has the following setup:

- Lifecycle: "Keep only the last version of the file".
- Backblaze Account ID and Account Key generated using [these](https://www.backblaze.com/docs/cloud-storage-s3-compatible-api) instructions.

- Repo Name: `function-shareName`
  - e.g. restic-backups
- Repo URI: `b2:bucketName`
- Enter password to encrypt upload: `password`
- Environment Variables:
  - B2_ACCOUNT_ID=someAccountValue
  - B2_ACCOUNT_KEY=someKeyValue
- Prune policy: 10%
  - Cron: Every month on 6th and * at 10 (`0 10 6 * *`)
- Check policy: 25%
  - Cron: Every week on TUE at 13 (`0 13 * * 2`)
- Command Modifiers: IO_DEFAULT AND CPU_DEFAULT
- [X] Auto Unlock

### Backup Plan Setup

- Plan Name: `function-shareName-b2-bucketName`
- Repository: Select from above
- Paths: `/userdata/shareName`
  - Can have multiple paths per backup plan.
- Excludes: `*.Recycle.Bin`
- Schedule: Every day at 0830 (`30 8 * * *`)
- Backup Flags: `--skip-if-unchanged`
- Retention Policy: By Count. 30
  - Keeps the last 30 days of snapshots.
