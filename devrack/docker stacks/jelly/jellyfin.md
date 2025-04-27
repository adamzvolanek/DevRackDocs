This page covers the setup of [JellyFin](https://github.com/jellyfin/jellyfin) to deploy in [my](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/jelly/jellyfin.yaml) docker-compose stack(s).

# Setup

Prerequisites:

- Hardware Transcoding Solution
  - See [NVIDIA Plugin](./unraid#nvidia-gpu-plugin)

## Initial Setup of JellyFin

placeholder text

### Notification Setup

Under Plugins select "Catalog" and install the "Webhook" plugin. Restart Jellyfin.

#### Webhook Plugin Configuration

A webhook is created per action desired to account for different template uses.

- Server Url: `https://subdomain.domain.tld`.
- Click "Add Discord Destination"

For Added Media:

- Webhook Name: `Jellyfin Added`
- Webhook URL: `https://discord.com/api/webhooks/...`
  - Generated via Discord Server Settings, Apps, Integrations.
- [X] Enable
- Notification Type:
  - [X] Item Added
- Item Type:
  - [X] Movies
  - [X] Episodes
  - [X] Season
  - [X] Series
  - [X] Albums
  - [X] Songs
  - [X] Videos
  - [ ] Send All Properties (ignores template)
  - [X] Trim leading and trailing whitespace from message body before sending
  - [X] Do not send when message body is empty
- Template:
  - [ItemAdded Template](https://github.com/jellyfin/jellyfin-plugin-webhook/blob/master/Jellyfin.Plugin.Webhook/Templates/Discord/ItemAdded.handlebars)
- Avatar URL: `https://cdn.jsdelivr.net/gh/selfhst/icons/webp/jellyfin.webp`
- Webhook Username: `Jellyfin Added`
- Mention Type: None

For User Lockouts:

- Webhook Name: `Jellyfin Lockout`
- Webhook URL: `https://discord.com/api/webhooks/...`
- [X] Enable
- Notification Type:
  - [X] User Locked Out
- Item Type:
  - [ ] Movies
  - [ ] Episodes
  - [ ] Season
  - [ ] Series
  - [ ] Albums
  - [ ] Songs
  - [ ] Videos
  - [ ] Send All Properties (ignores template)
  - [X] Trim leading and trailing whitespace from message body before sending
  - [X] Do not send when message body is empty
  - Generated via Discord Server Settings, Apps, Integrations.
- Template:
  - [UserLockedOut Template](https://github.com/jellyfin/jellyfin-plugin-webhook/blob/master/Jellyfin.Plugin.Webhook/Templates/Discord/UserLockedOut.handlebars)
- Avatar URL: `https://cdn.jsdelivr.net/gh/selfhst/icons/webp/jellyfin.webp`
- Webhook Username: `Jellyfin Added`
- Mention Type: None
