This page covers the configuration of [Nginx Proxy Manager](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/core/npm.yaml) on DevRack.

## Setup

Follow these steps to setup Nginx Proxy Manager.

### General Setup Instructions

### Certificate Installation

- [DuckDNS](https://youtu.be/qlcVx-k-02E?si=dRPaGsstvUQSuSkd)
- [CloudFlare](https://youtu.be/GarMdDTAZJo?si=I0haNsb_SYiNbOE5)

### Hosts

Most nginx proxy's will follow these general setup procedures. Upon login, select "Add Proxy Host".

- Details (Tab)
  - Provide `Domain Name` to field: `subdomain.domain.tld`.
  - Select http/https scheme based on port of docker.
  - Provide `container_name` as Forward Hostname / IP.
  - Provide the bolded value as the Forward Port, "${SERVER_IP}:**<Server_Port>**:<Docker_Port>".
  - [ ] Cache Assets
  - [X] Websockets Support
  - [X] Block Common Exploits
- SSL (Tab)
  - Select "*your domain* CDN" certificate.
  - [X] Force SSL
  - [X] HSTS Enabled
  - [X] HTTP/2 Support
  - [X] HSTS Subdomains

### Redirection Hosts

1. Select "Add Redirection Host"
2. Enter desired domain names.
   1. e.g. *.domain.tld, domain.tld
      1. Press the Enter key between entries.
3. Select https scheme
4. Enter Forward Domain.
5. Select 307 Temporary redirect.
6. Options:
   1. Toggle On, Preserve Path
   2. Toggle On, Block Common Exploits
7. Follow general setup instructions above.

## Custom Nginx Configuration for Stacks

### BookStack

```
# By default indexes are disabled on Nginx but if you have them enabled
# add this to your BookStack server block
location /uploads {
       autoindex off;
}
```

### Jellyfin

```
proxy_buffering off;
proxy_request_buffering off;
proxy_max_temp_file_size 0;
client_max_body_size 20M;
```
