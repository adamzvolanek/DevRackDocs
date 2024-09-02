# Cloud

This page covers the setup of mariadb and NextCloud to deploy in my docker-compose cloud stack. Currently there is no method to "stop and move" the mariaDb and NextCloud instances without re-setting up the manual steps section.

**NextCloud and it's MariaDB have been stopped in favor of Syncthing.**

## Manual Steps

The manual steps require use of phpMyAdmin to setup the SQL database to be used with NextCloud. There is a development `cloud-dev` docker-compose stack that adds Redis and additional docker parameters added to allow NextCloud to setup and connect to MariaDB container on-boot.

Pre-requisite: [phpMyAdmin](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/tools/phpmyadmin.yml) installed and the `/mnt/user/NextCloud` share is empty.

### Create and Start the Stack

Use the [installs](./installs#creating-a-docker-compose-stack) section and start the stack.

### MariaDB

Login to phpMyAdmin and select the 'Databases' tab. Enter the database name `${DB_NAME_NC}` with using the  `utf8mb4_general_ci` character set.

Once the database is created, select the 'Privileges' tab and create/add a new user by clicking the 'Add user account':

- Enter a username (Same entry as `${DB_USER_NC}` in the `cloud.env` file)
- Skip the Host name field
- Enter a password (Same entry as `${DB_PASSWORD_NC}` in the `cloud.env` file)
  - Re-type the password
- Skip Authentication Plugin
- Verify the following settings are checked (and unchecked):
  - [ ] Create database with same name and grant all privileges.
  - [X] 'Grant all privileges on wildcard name (username\_%).'
  - [X] 'Grant all privileges on database `${DB_NAME_NC}`'
- Select the 'Go' button at the bottom to create the user

### NextCloud

Follow [these](https://docs.nextcloud.com/server/latest/admin_manual/installation/installation_wizard.html) instructions once the nextcloud docker is up.

- Select 'MySQL/MariaDB'
  - Database user: `${DB_USER_NC}`
  - Database password: `${DB_PASSWORD_NC}`
  - Database name: `{$DB_NAME_NC}`
  - Enter the Servers IP and port, `${SERVER_IP}`:`${MARIADB_PORT}`
- Uncheck 'Install recommended apps'.

**Note**: Entering the `${SERVER_IP}` is a artifact of previous testing of the most reliable method of connecting to the MariaDB container. This should be 'reachable' via docker name (`mariadb_nc`) within the same docker-network, but is not.

There are additional items to configure *on* NextCloud itself, part of admin management like additional users, storage permissions, add-ons, etc.

Upon completion of initial setup wizard, NextCloud will prompt for recommended apps. Skip this screen and navigate to your nextcloud instance. Or press "Skip".

## Updating NextCloud

To update Nextcloud, open the docker terminal either using Unraid's console feature, or when in Unraid typing, `docker exec -it nextcloud bash`. To begin the console update process, type, `updater.phar` and follow the prompts.

The backup process takes time, allow it to complete.

### Setup NextCloud Application for OAuth2/OpenID (3/3)

These steps are to be completed after completing the [Authentik install](./authentik) and the previous [steps](./authentik#setup-nextcloud-oauth2openid-providers-13).

- Login to NextCloud as the Administrator and navigate to "Apps" on the top-right.
- Select "Security" and then search for `OpenID Connect user backend` in NextCloud app search. (At time of writing, version 1.3.5)
  - Click on "Download and enable"
- Navigate to "Administration settings" and find "OpenID Connect"
  - Click on the "+" button under "Registered Providers" and fill in the fields
    - For "Identifier" provide an recognizable value like `Authentik`
      - Note, the selection here will be shown to your users in the form of a Login with <IDENTIFIER> button
    - Copy the "Client ID" value from Authentik [nextcloud-OpenID](./authentik#setup-nextcloud-oauth2openid-providers-13)
    - Copy the "Client Secret" value copied from Authentik
      - This is the shortened value from the NextCloud open issue. (Missing link)
    - Enter the "Discovery endpoint" with the "OpenID Configuration URL" copied from Authentik
      - Should end with `.well-known/openid-configuration`. e.g. `https://Authentik_DOMAIN/application/o/cloud/.well-known/openid-configuration`
    - Uncheck "Use unique user ID"
      - When this option is enabled, NextCloud will use the hash (checksum) of the provider identifier + user identifier as the internal user ID. Unfortunately, this creates rather ugly and long federated cloud IDs.
  - Leave the remainder as defaults
  - Click on "Submit"

Upon clicking "Submit" the "Backchannel Logout URL" should populate with the proper URL for when a user performs a logout from NextCloud they are presented with the option of logging out of Authentik as well.

Ensure the "Redirect URI (to be authorized in the provider client configuration)" in NextCloud matches what is in Authentik NextCloud OAuth2 Provider's "Redirect URIs/Origins (RegEx)". e.g. `https://<domain>.<tld>/apps/user_oidc/code`

In the future, the NextCloud setup can be completed using [automation](#automatic-setup). (Pending)

Additional configuration can be made to disable the built-in login form by setting `hide_login_form` => `false` in the `...appdata\nextcloud\www\nextcloud\config\config.php` however can still be accessed manually by entering `https://<NEXTCLOUD-HOSTNAME>/login?direct=1`. This is **not** implemented.

[Source](https://blog.cubieserver.de/2022/complete-guide-to-nextcloud-oidc-authentication-with-authentik/)

### Additional Setup

- Disable the Dashboard App.

Setup External Storage. Fill out the External Storage under Administration settings with the following fields

| Folder Name | External Storage | Authentication | Configuration | Available for |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| Adam        | Local       | None        | `/data/alexandria/Adam` | Adam (User) and Admin (Group) |
| backups     | local       | None        | `/data/alexandria/backups` | Adam (User) and Admin (Group) |

On the three-dots select the following:

- [X] Enable previews
- [X] Enable sharing
- Check for changes "Once every direct access"
- [ ] Compatibility with Mac NFD encoding (slow)
- [ ] Read only

Select the check mark and ensure a green check mark appears on the left side.

Administration --> Basic settings.

- Setup your email server to relay SMTP.

Review and verify additional Administration settings: Sharing, Security, etc.

Configure theming.

Configure read-only photo group with external storage.

### WorkFlow of New Users

This assumes Authentik is setup and user exists in Authentik.

Have user navigate to `https://subdomain.domain.tld` for your NextCloud instance and select the "Login with Authentik" button.

## Automatic Setup

Testing has not been completed, however the `cloud-dev.yaml` docker-compose stack is the best method of setting up the cloud stack in an automated fashion.

### NextCloud OAuth2/OpenID

Assuming that your are in the root of the NextCloud folder `(...appdata\cloud\nextcloud\config\www\nextcloud)` and running this as the `www-data` user:

```bash
php ./occ app:install user_oidc
php ./occ user_oidc:provider "Authentik" \
    --clientid="<CLIENT-ID>" \
    --clientsecret="<CLIENT-SECRET>" \
    --discoveryuri="<AUTHENTIK-OPENID-CONFIGURATION-URL>" \
    --unique-uid=0

# for help, refer to:
php ./occ user_oidc:provider -h
php ./occ user_oidc:provider:delete -h
php ./occ app -h
```
