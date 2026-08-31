This page covers the setup of [JellyFin](https://github.com/jellyfin/jellyfin) to deploy in [my](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/jelly/jellyfin.yaml) docker-compose stack(s).

## Setup

Prerequisites:

- Hardware Transcoding Solution
  - See [NVIDIA Plugin](./unraid#nvidia-gpu-plugin)

### Initial Setup of JellyFin

### Playback

#### Transcoding

- Hardware Acceleration: Intel QSV
- QSV device: `/dev/dri/renderD128`

#### Hardware decoding

Enable all available:

- [x] H264
- [x] HEVC
- [x] MPEG2
- [x] VC1
- [x] VP8
- [x] VP9
- [x] AV1
- [x] HEVC 10bit
- [x] VP9 10bit
- [x] HEVC RExt 8/10bit
- [x] HEVC RExt 12bit
- [X] Prefer OS native DXVA or VA-API hardware decoders

#### Hardware encoding

- [x] Enable hardware encoding
- [x] Enable Intel Low-Power H.264 hardware encoder
- [x] Enable Intel Low-Power HEVC hardware encoder

#### Encoding formats

- [x] Allow encoding in HEVC format
- [x] Allow encoding in AV1 format

#### VPP Tone Mapping

- [x] Enable VPP Tone mapping
- Brightness gain: `16`
- Contrast gain: `1`

#### Tone Mapping

- [x] Enable Tone mapping
- Tone mapping mode: `BT.2390`
- Output color range: `Auto`
- Desaturation: `0`
- Peak: `100`
- Tone mapping param: Blank/default

#### Transcoding

- Maximum number of threads: Auto/default
- FFmpeg path: Blank/default
- Custom transcode path: Blank/default

  Docker mapping:
  `/config/data/transcodes` → `/mnt/user/scratch/jellyfin_transcodes`

#### Fonts

- [x] Enable fallback fonts
- [ ] Enable custom alternate fonts

#### Audio

- [x] Enable VBR audio encoding
- Boost audio when downmixing: `1`
- Downmix algorithm: Default

#### FFmpeg

- Maximum packets buffered: `2048`
- Encoder preset: Default
- x264 CRF: `23`
- x265 CRF: `28`

> CRF settings only apply to software video encoding.

#### Deinterlacing

- Deinterlacing method: Default
- [ ] Double the frame rate when deinterlacing

#### Subtitles

- [x] Allow subtitle extraction on the fly

#### Transcode management

- [x] Throttle Transcodes
- [x] Delete segments
- Throttle time: Default
- Segment retention time: Default

### Trickplay

#### Hardware acceleration

- [x] Enable hardware decoding
- [x] Enable hardware accelerated MJPEG encoding
- [ ] Only generate images from key frames

#### Generation

- Processing mode: Non-blocking
- Process priority: Below Normal

#### Image generation

| Setting | Recommended value |
|---|---|
| Interval | `10000 ms` |
| Image widths | `320` |
| Maximum images per tile — X | `10` |
| Maximum images per tile — Y | `10` |
| JPEG compression quality | `80` |
| FFmpeg image quality (`-q:v`) | `10` |

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
