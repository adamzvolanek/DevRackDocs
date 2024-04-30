# Nginx Proxy Manager

This page covers the configuration of [Nginx Proxy Manager](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/core/npm.yaml) on DevRack.

## Manual Setup

Follow these steps to setup Nginx Proxy Manager.

### Cloud Setup

These steps are for [NextCloud AIO](./cloud-aio.md)!

#### Details

- Domain Names: `subdomain.domain.tld`
- Scheme: http
- Forward Hostname/IP: ${SERVER_IP}
- Forward Port: 11000 (Apache Port defined in [cloud-aio.yam](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/cloud-aio/cloud-aio.yaml))

#### Proxy Host

- [X] Cache Assets
- [X] Websockets Support
- [X] Block Common Exploits

#### SSL

- [X] Check all options.

#### Advanced

```bash
client_body_buffer_size 512k;
proxy_read_timeout 86400s;
client_max_body_size 0;
```

## Automated Setup
