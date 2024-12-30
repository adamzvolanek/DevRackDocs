This page covers the setup of [Beszel](https://beszel.dev/) to deploy in my docker-compose stack.

## Setup

### Setup of Admin Account

Enter valid (or invalid) email as the user email. Enter password to be utilized.

You can modify/update your email within PocketBase's System\superusers settings.

### Setting up Docker Agent

1. Select "Add System" and ensure "Docker" is selected on the "Add New System" prompt.
2. Name: `local` (name of the system)
3. Host/IP: `beszel-agent` (beszel docker container name)
4. Port: `45876` (matches beszel-agent docker port)
5. Public Key: copy the contents and populate the `KEY` environment variable with the `'ssh-ed25519...` value.

### Setup of Email Notifications

Select the cog wheel and press "configure an SMTP server". Login to PocketBase with same account created with Admin account.

1. Select Settings on the left-side bar.
2. Click Mail Settings
3. Edit sender name: `Alexandria Beszel`
4. Sender address: `admin@beszel.com`
5. Configure SMTP server host via app passwords.

### Setup of Backups

1. Select "Backups options"
2. Check "Enable auto backups"
3. Cron expression: `5 02 * * 6`
4. Max @auto backups to keep: `3`

### Setup of `local` notifications

1. Select the bell icon along the `local` system.
