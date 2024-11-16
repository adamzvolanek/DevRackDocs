This page covers the setup of Photoprism to deploy in my docker-compose stack(s). This also includes some picture share directory setup and preparation. The Photoprism will be a public facing photo library as an alternate to my [Instagram](https://www.instagram.com/zvolanek.photography/). Family photos are hosted with an [immich](./immich) instance.

[Photoprism Site](https://www.photoprism.app/)

## Picture Share

Created a separate directory for "professional" photos. Images there are organized by Year and location. An Event folder is added if multiple photo "moments" occur at identical locations.

## Automated

Pending.

## Setup

These steps are a one-time setup and does require update of the docker environment variables after completion.

### Library Import

- Navigate to Library then select the "Index" tab.
  - Select "All Originals" and select "Start". This begins importing files from your additional media folders.

Once Photoprism is in 'public' mode, the following script will be needed to trigger a library scan for new image imports. More information in the [public ready](#public-ready) section.

### Settings

- Navigate to "Settings" and select the "Library" tab.
  - [X] Estimates
  - [ ] Quality Filter
  - [X] Preview Images
  - [X] Place & Time
  - [X] Unique ID
  - [X] Sequential Name
- Navigate to the "General" tab.
  - Set Theme to "Yellowstone".
  - [ ] People
  - [X] Moments
  - [X] Labels
  - [ ] Private
  - [ ] Upload
  - [ ] Download
  - [ ] Import
  - [ ] Share
  - [ ] Edit
  - [ ] Archive
  - [ ] Delete
  - [ ] Services
  - [ ] Library
  - [X] Originals
  - [ ] Logs
  - [ ] Account
  - [X] Places

### Public Ready

Once ready for public viewing, modify the `PUBLIC_READY` environment variable in the [photoprism docker environment file](https://github.com/adamzvolanek/DevRack/tree/main/docker-compose/photo/) from false to true.

Manual trigger for library update: `/usr/bin/docker exec -it <name_of_photo_prism_container> /opt/photoprism/bin/photoprism index`

This script should also be added to Unraid's User Scripts configuration as a cron job.

#### Editing `settings.yaml`

Edit the settings file and set albums to false, disabling the album feature.
