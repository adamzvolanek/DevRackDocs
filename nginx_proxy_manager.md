# Nginx Proxy Manager

This page covers the configuration of [Nginx Proxy Manager](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/core/npm.yaml) on DevRack.

## Manual Setup

Follow these steps to setup Nginx Proxy Manager.

### General Setup Instructions

All nginx proxy's will follow these general setup procedures. Upon login, select "Add Proxy Host".

1. Details (Tab)
   1. Provide `Domain Name` to field: `subdomain.domain.tld`.
   2. Select http/https scheme based on port of docker.
   3. Provide `container_name` as Forward Hostname / IP.
   4. Provide the bolded value as the Forward Port, "${SERVER_IP}:**<Server_Port>**:<Docker_Port>".
   5. [X] Cache Assets
   6. [X] Websockets Support
   7. [X] Block Common Exploits
2. SSL (Tab)
   1. Select "domain CDN" certificate.
   2. [X] Force SSL
   3. [X] HSTS Enabled
   4. [X] HTTP/2 Support
   5. [X] HSTS Subdomains

#### NextCloud AIO Setup

These steps are for [NextCloud AIO](./cloud-aio)!

1. Advanced (Tab)

```bash
client_body_buffer_size 512k;
proxy_read_timeout 86400s;
client_max_body_size 0;
```
