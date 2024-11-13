This page covers the setup of [crowdsec](https://www.crowdsec.net/) to deploy in my docker-compose stack(s).

## Manual Steps

- Setup the docker compose stack in Unraid.
- Paste the current `crowdsec-npm.yaml` contents.
- Paste the `server.env` contents and the `crowdsec-npm.evn` file contents.
- Create the [`acquis.yaml`](https://github.com/crowdsecurity/example-docker-compose/blob/main/npm/crowdsec/acquis.yaml) file.
- Start up the docker stack
- Sign into the new NginxProxyManager using default credentials. Update Admin email and password.
- In the crowdsec terminal run, `cscli bouncers add NginxBouncer` and copy the received API key.
- Paste the API key into the environment variable named "CROWDSEC_BOUNCER_APIKEY".
- In the crowdsec terminal run, `cscli collections install crowdsecurity/nginx-proxy-manager`
- Restart the docker stack
- Run `cscli bouncers list` to verify the bouncer is running.
  - Each field should be populated.
