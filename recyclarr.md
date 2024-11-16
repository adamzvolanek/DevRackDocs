This page covers the setup of [recyclarr](https://github.com/recyclarr/recyclarr) to deploy in my docker-compose stack(s). Recyclarr is setup to configure quality profiles with HEVC preference **not** language support.

## Setup

Manual [Radarr configuration](./radarr#manual-steps) and manual [Sonarr configuration](./sonarr#manual-steps).

## Configuration

Replace `radarr_url` and `radarr_apikey` within the `docker-compose\arrs\secrets.yml` file. Resources used to create the configuration file can be found in the [YAML Reference](https://recyclarr.dev/wiki/yaml/config-reference/) section.

<details>
<summary>Click to show/hide</summary>

```yml reference title="Copy this configuration into your own configuration file:"
<Pending Link>
```

</details>
