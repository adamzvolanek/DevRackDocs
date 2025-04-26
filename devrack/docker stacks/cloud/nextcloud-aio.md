# NextCloud AIO

This page covers the setup of [NextCloud AIO](https://github.com/nextcloud/all-in-one) to deploy in my docker-compose cloud stack.

## Setup

Steps taken from [here](https://www.youtube.com/watch?v=U47nvwXrAOo)

### WebUI

Navigate to nextcloud-aio webUI via Unraid.

### Domain

After authorization, the system will prompt us to enter the domain through which our cloud will be available. Enter `subdomain.domain.tld`.

Launch NPM on another window/tab and configure per [cloud setup](./nginx_proxy_manager#cloud-setup).

Click on "Submit" and verify check passes.

In the next window, we select the additional options that we want to install along with the cloud and the time zone, and also carefully read the requirements for the required space, required ports, and the amount of RAM for deploying. Leave all options unchecked, update Timezone to: `America/Chicago`.

Click the Save changes button.

### Starting NextCloud

Select "Start containers".

After launch (depending on the selection of components), the downloading and deployment process itself will begin, it will take some time.

Once installed page will show the nextcloud username: `admin` and password to use. Click "Open your Nextcloud". Login using previously mentioned credentials.

## Configuration Updates

### App Removal

- Calendar
- Contacts
- Tasks
- Notes

### Chunked Uploads

Run `sudo docker exec --user www-data -it nextcloud-aio-nextcloud php occ config:app:set files max_chunk_size --value 52428800` to set it to 50 MB upload chunks.
