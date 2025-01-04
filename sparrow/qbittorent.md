This page covers the setup of [qBittorrent](https://github.com/binhex/arch-qbittorrentvpn) to deploy in [my](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/sparrow/qbittorrentvpn.yaml) docker-compose stack(s).

Note, qBittorrent and [delugeVPN](https://github.com/binhex/arch-delugevpn) cannot run simultaneously. Not seeing port conflict, cause unknown.

## Setup

Create the docker compose stack following the [instructions](./installs#creating-a-docker-compose-stack) on the Installs page. Select "Compose Up" and allow docker-compose to pull down the docker image.

It is expected for qBittorrent to fail on first run due to missing openVPN files.

### Populate the openvpn Directory

In the qbittorrent config volume (`qbittorrentvpn\config\openvpn`) add VPNs OpenVPN configuration files.

- Certificate file (`ca....crt`)
- OVPN file (`*.ovpn`) for the region to be used
- CMS (S/MIME) file (`crl...pem`)

Start the stack again by selecting "Compose Up" and allow container to load. You can monitor the logs to view when the container is ready to view the WebUI.

```bash
2023-12-22 22:47:31,586 DEBG 'watchdog-script' stdout output:
[info] qBittorrent process listening on port <WEBUI_PORT>
```

### QBitTorrent Configuration File

Bring qbittorrent down again and import the following [qBittorrent.conf]() file into `sparrow\qbittorrentvpn\config\qBittorrent\config\`. It should loosely follow the [basic setup](https://trash-guides.info/Downloaders/qBittorrent/Basic-Setup/). Likewise import the `categories.json` to `sparrow\qbittorrentvpn\config\qBittorrent\config\`.

Continue with setting up Sonarr and Radarr following the respective docs: [sonarr](./sonarr) and [radarr](./radarr).
