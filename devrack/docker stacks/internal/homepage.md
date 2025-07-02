This page covers the setup of [Homepage](https://github.com/gethomepage/homepage) to deploy in my server.

# Setup

Setup for homepage is primarily file based. Stepping through the files, *my* basic configuration is as follows.

For the majority of icon URLs, I leverage [selfh.st/icons](https://selfh.st/icons/).

### Bookmarks

For configuration options and examples, please visit [link](https://gethomepage.dev/configs/bookmarks).

### Docker and Kubernetes

I do not leverage the `docker.yaml` or `kubernetes.yaml`.

### Settings

Covering settings before services to understand the organization on the homepage. However can view the [example](https://gethomepage.dev/configs/settings/).

My summarized `settings.yaml` file, note the layout section. This is where the number of columns, header being visible, etc. can be set.

`settings.yaml`

```yaml
---
# For configuration options and examples, please see:
# https://gethomepage.dev/latest/configs/settings

# style
title: "Alexandria Internal Homepage"
background: 
  image: <SOME BACKGROUND IMAGE LINK>
  opacity: 40 # 0-100
favicon: <SOME FAVICON LINK>>
theme: dark
color: slate
target: _blank # Possible options include _blank, _self, and _top
headerStyle: clean
useEqualHeights: true
cardBlur: md
statusStyle: "dot"
quicklaunch:
  searchDescriptions: true
  hideInternetSearch: true
  hideVisitURL: false
  showSearchSuggestions: true

## layouts
layout:
  Core:
    style: row
    columns: 3
    header: True
  Home Assistant:
    style: row
    columns: 1
    header: false
  Photo:
    style: row
    columns: 2
    header: True
  Stream:
    style: row
    columns: 2
    header: true
  Arr:
    style: row
    columns: 4
    header: True
  Stuff:
    style: row
    columns: 4
    header: False
  Socials and Development:
    style: row
    header: true
    columns: 2
```

### Services

For configuration options and examples, please see the developers services [page](https://gethomepage.dev/configs/services/).

A summarized overview of my services file organization is as follows:

`services.yaml`

```yaml
---

- Arr:
    - Sonarr:
    ...
    - QBitTorrentVPN:
- Stream:
    - Jellyfin:
    - Requestarr:
- Core:
    - Unifi:
    - Nginx Proxy Manager:
    - UpTimeKuma:
- Home Assistant:
    - Home Assistant Power:
    - Home Assistant Temperature:
- Photo:
    - Photoprism:
    - Immich:
- Stuff:
    - Syncthing:
    - Alexandria File Upload:
    - Memos:
    - BookStack:
    - Jetlog:
    - AirTrail:
    - Dozzle:
    - Beszel:
    - Paperless-ngx:
    - Dawarich:
```

### Widgets

For configuration options and examples, please see [service-widgets](https://gethomepage.dev/configs/service-widgets).

`widgets.yaml`

```yaml
---
- logo:
    icon:  <ICON URL>

- greeting:
    text_size: xl
    text: Alexandria's Home Page!

- resources:
    cpu: true
    memory: true
    uptime: true
    cputemp: true

- openmeteo:
    label: <LOCATION> # optional
    latitude: <LAT>
    longitude: <LONG>
    timezone: America/Chicago # optional
    units: imperial # or imperial
    cache: 5 # Time in minutes to cache API responses, to stay within limits
    format: # optional, Intl.NumberFormat options
      maximumFractionDigits: 1

## Service widgets defined in services.yaml
```
