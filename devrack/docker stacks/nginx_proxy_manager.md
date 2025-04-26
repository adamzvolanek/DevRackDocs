This page covers the configuration of [Nginx Proxy Manager](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/core/npm.yaml) on DevRack.

## Setup

Follow these steps to setup Nginx Proxy Manager.

### General Setup Instructions

Most nginx proxy's will follow these general setup procedures. Upon login, select "Add Proxy Host".

- Details (Tab)
  - Provide `Domain Name` to field: `subdomain.domain.tld`.
  - Select http/https scheme based on port of docker.
  - Provide `container_name` as Forward Hostname / IP.
  - Provide the bolded value as the Forward Port, "${SERVER_IP}:**<Server_Port>**:<Docker_Port>".
  - [X] Cache Assets
  - [X] Websockets Support
  - [X] Block Common Exploits
- SSL (Tab)
  - Select "*your domain* CDN" certificate.
  - [X] Force SSL
  - [X] HSTS Enabled
  - [X] HTTP/2 Support
  - [X] HSTS Subdomains

### Certificate Installation

- [DuckDNS](https://youtu.be/qlcVx-k-02E?si=dRPaGsstvUQSuSkd)
- [CloudFlare](https://youtu.be/GarMdDTAZJo?si=I0haNsb_SYiNbOE5)
