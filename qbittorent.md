# qBittorrent

This page covers the setup of [qBittorrent](https://github.com/binhex/arch-qbittorrentvpn) to deploy in [my](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/sparrow/qBittorrent.yaml) docker-compose stack(s).

## Manual Steps

### Temporarily Add Default WebGUI Password

Edit the following file, `...\appdata\sparrow\binhex-qbittorrentvpn\qBittorrent\config\qBitorrent.conf` and add the following line below preferences.

```md
[Preferences]
...
WebUI\Password_PBKDF2="@ByteArray(ARQ77eY1NUZaQsuDHbIMCA==:0WMRkYTUWVT9wVvdDtHAjU9b3b7uB8NR1Gur2hmQCvCDpm39Q+PsJRJPaCU51dEiz+dTzh8qbPsL8WkFljQYFQ==)"
```

### Initial Setup of qBittorrent

The default login for qBittorrent can be found to [here](https://github.com/binhex/arch-qbittorrentvpn/blob/master/README.md?plain=1#L59); `admin` and `adminadmin`.

