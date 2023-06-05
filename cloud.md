# Cloud

This page covers the setup of mariadb and nextcloud to deploy in my docker-compose cloud stack.

## Manual Steps

The manual steps require use of phpMyAdmin to setup the SQL database to be used with NextCloud. There is a development `cloud-dev` docker-compose stack that adds Redis and additional docker parameters added to allow NextCloud to setup and connect to MariaDB container on-boot.

### MariaDB

**Note**: The manual configuration may be unecessary with the updated configuration of `cloud-dev.yaml` in the cloud directory.

Login to phpMyAdmin and select the 'Databases' tab. Enter the database name with using the  `utf8mb4_general_ci` character set.

Once the database is created, select the 'Privileges' tab and create/add a new user by clicking the 'Add user account':

- Enter a username (Same entry as `${DB_USER_NC}` in the `cloud.env` file)
- Enter a password (Same entry as `${DB_PASSWORD_NC}` in the `cloud.env` file)
  - Re-type the password
- Check the following options:
  - 'Grant all privileges on wildcard name (username\_%).'
  - 'Grant all privileges on database testdb.'
- Select the 'Go' button at the bottom to create the user

### NextCloud

Follow [these](https://docs.nextcloud.com/server/latest/admin_manual/installation/installation_wizard.html) instructions once the nextcloud docker is up.

- Select 'MySQL/MariaDB'
  - Database user: `${DB_USER_NC}`
  - Database password: `${DB_PASSWORD_NC}`
  - Database name: `{$DB_NAME_NC}`
  - Enter the Servers IP
- Uncheck 'Install recommended apps'.

**Note**: Entering the Servers IP is a artifact of previous testing of the most reliable method of connecting to the MariaDB container. This should be 'readchable' via docker name (`mariadb_nc`) within the same docker-network.

There are additional items to configure *on* NextCloud itself, part of admin management like additional users, storage permissions, add-ons, etc.

## Redis

No setup is needed for Redis in conjunciton with the cloud docker-compose stack.

## Updating nextcloud

To update Nextcloud, open the docker terminal either using Unraid's console feature, or when in Unraid typing, `docker exec -it nextcloud bash`. To begin the console update process, type, `updater.phar` and follow the prompts.

The backup process takes time, allow it to complete.

## Automatic Setup

Testing has not been completed, however the `cloud-dev.yaml` docker-compose stack is the best method of setting up the cloud stack in an automated fashion.
