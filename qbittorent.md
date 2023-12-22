# qBittorrent

This page covers the setup of [qBittorrent](https://github.com/binhex/arch-qbittorrentvpn) to deploy in [my](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/sparrow/qBittorrent.yaml) docker-compose stack(s).

Note, qBittorrent and [delugeVPN](https://github.com/binhex/arch-delugevpn) cannot run simultaneously. Not seeing port conflict, cause unknown.

## Manual Steps

Create the docker compose stack following the [instructions](./installs#creating-a-docker-compose-stack) on the Installs page. Select "Compose Up" and allow docker-compose to pull down the docker image.

It is expected for qBittorrent to fail on first run due to missing openVPN files.

### Populate the openvpn Directory

In the qbittorrent config volume (`binhex-qbittorrentvpn/openvpn/`) add VPNs OpenVPN configuration files.

- Certificate file (`ca....crt`)
- OVPN file (`*.ovpn`)
- Credentials file (`credentials.conf`)
- CMS (S/MIME) file (`crl...pem`)

Start the stack again by selecting "Compose Up" and allow container to load. You can monitor the logs to view when the container is ready to view the WebUI.

```bash
2023-12-22 22:47:31,586 DEBG 'watchdog-script' stdout output:
[info] qBittorrent process listening on port <WEBUI_PORT>
```

### Temporarily Add Default WebGUI Password

Stop the container by selecting "Compose Down". Edit the following file, `...\binhex-qbittorrentvpn\qBittorrent\config\qBitorrent.conf` and add the following line below preferences.

```md
[Preferences]
...
WebUI\Password_PBKDF2="@ByteArray(ARQ77eY1NUZaQsuDHbIMCA==:0WMRkYTUWVT9wVvdDtHAjU9b3b7uB8NR1Gur2hmQCvCDpm39Q+PsJRJPaCU51dEiz+dTzh8qbPsL8WkFljQYFQ==)"
```

### Initial Setup of qBittorrent

The default login for qBittorrent can be found to [here](https://github.com/binhex/arch-qbittorrentvpn/blob/master/README.md?plain=1#L59); `admin` and `adminadmin`.

Pending further instructions, notes for later: https://trash-guides.info/Downloaders/qBittorrent/Basic-Setup/
