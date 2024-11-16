# NextCloud AIO

This page covers the setup of [NextCloud AIO](https://github.com/nextcloud/all-in-one) to deploy in my docker-compose cloud stack.

This procedure has been **deprecated** and instead using [NextCloud](./cloud).

## Setup

Steps taken from [here](https://myunraid-ru.translate.goog/nextcloud-aio/?_x_tr_sl=auto&_x_tr_tl=en&_x_tr_hl=de&_x_tr_pto=wapp)

### WebUI

Navigate to `https://${SERVER_IP}:8089/`. The 8089 port should be what is listed on [line 16](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/cloud-aio/cloud-aio.yaml).

The initial window will show the authorization password of the NextCloud AIO master container. Save the password somewhere locally. Select "Open Nextcloud AIO Login" and paste the received password into the login form and click "Login".

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
