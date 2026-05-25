This page covers the configuration of [NPM Plus](https://github.com/ZoeyVid/NPMplus#) on DevRack.

## NPM Setup

Follow these steps to setup Nginx Proxy Manager Plus.

1. Navigate to the (host) IP of the server on port 81.
2. Enter name for (Admin) user, Email address, and Password.

### Certificate Installation

- [DuckDNS](https://youtu.be/qlcVx-k-02E?si=dRPaGsstvUQSuSkd)
- [CloudFlare](https://www.youtube.com/watch?v=pwK1LnbTitI)
  1. Login to [Cloudflare](https://www.cloudflare.com)
  2. Navigate to your domain.
  3. Select **SSL/TLS**
  4. Select **Origin Server**
     1. Select **Create Certificate**
     2. Verify hostnames are accurate.
     3. Edit the Certificate Validity as needed.
     4. Select **Create**
     5. Copy the first pem into Notepad++ and save as **domain.pem**.
     6. Copy the certificate key into Notepad++ and save as **domain.key**

#### Within NPM Plus

1. Click the **Certificates** button
2. Click **Add Certificate** and a drop-down appears.
3. Click **Custom Certificate**
   1. In "Names", enter your Domain Name desired. `*.domain.tld`
   2. For the "Certificate", select the `domain.pem` file saved from above.
   3. For the "Certificate Key" file select the `domain.key` file saved from above.

### Redirection Hosts

1. Select "Add Redirection Host"
2. Enter desired domain names.
   1. e.g. *.domain.tld, domain.tld
      1. Press the Enter key between entries.
3. Select https scheme
4. Enter Forward Domain without http/https scheme.
5. Select 307 Temporary redirect.
6. Options:
   1. Toggle On, Preserve Path
7. Select **TLS** tab.
   1. Select certificate created above.
   2. Enable all options except for "Make mTLS Optional".

### Hosts

1. Navigate to **Hosts**.
2. Enter domain name in the "Domain Names" field.
3. Select appropriate Scheme.
4. Enter Forward Hostname/IP/Path and Forward Port
5. For host options.
   1. **Enable**, Send noindex header and block some user agents
   2. Enable the following options for specific hosts:
      1. Jellyfin: Disable Response Buffering
         1. Video streaming works better when nginx streams directly rather than buffering large media responses. Benefits: Faster playback start, better seeking/scrubbing, lower latency, less disk buffering on proxy.
         2. **Note**, this may conflict or render Crowdsec as inoperative.
6. Select the **TLS** tab.
   1. Select the TLS Certificate created above.
   2. Enable all options: Force HTTPS, HTTP/3 Support, HSTS Enabled (2 Years), and HSTS Subdomains+Preload.

## CrowdSec Setup

Steps from NPMPlus CrowdSec section [link](https://github.com/ZoeyVid/NPMplus/blob/develop/README.md#crowdsec).

1. Install crowdsec and the ZoeyVid/npmplus collection for example by using crowdsec container at the end of the compose.yaml, you may also want to install [this](https://app.crowdsec.net/hub/author/crowdsecurity/collections/http-dos), but be warned of false positives
2. Set LOGROTATE to `true` in your `compose.yaml` and redeploy
3. Open `/opt/crowdsec/conf/acquis.d/npmplus.yaml` (path may be different depending how you installed crowdsec) and fill it with:

```yaml
filenames:
  - /opt/npmplus/nginx/logs/*.log
labels:
  type: npmplus
---
listen_addr: 0.0.0.0:7422
appsec_config: crowdsecurity/appsec-default
name: appsec
source: appsec
labels:
  type: appsec
```

4. Make sure to use `network_mode: host` in your compose file for the NPMplus container
5. Run `docker exec crowdsec cscli bouncers add npmplus`
   1. Save the api key of the output:
6. Open `/opt/npmplus/crowdsec/crowdsec.conf`
   1. Set `ENABLED` to `true`
   2. Use the output of step 5 as `API_KEY`
   3. Save the file
7. Redeploy the `compose.yaml`
8. Note that when using crowdsec requests will always be buffered, so setting `proxy_(request_)buffering` to off will not work

### Crowdsec Specifics

1. Navigate to `opt/crowdsec/conf` and open **config.yaml**.
   1. Add Server or LAN subnet into the trusted IP field.
      1. Note, this action will require restarting crowdsec.
2. Navigate to Crowdsec Website and login.
3. Navigate to engines via https://app.crowdsec.net/security-engines
4. Select the **Enroll Command** and enter the following into the crowdsec docker container.
5. Restart the crowdsec container: `docker restart crowdsec`
6. Perform the tests listed in: https://docs.crowdsec.net/u/getting_started/health_check
   1. Note, when running HTTP detection test and AppSec detection test, use URLs listed in the hosts in NPMPlus.

#### Whitelist IPs

1. Navigate to `opt\crowdsec\conf\parsers\s02-enrich`
2. Create `cloudflare-whistelist.yaml` and populate with the following content
3. IPs below should match cloudflares: https://www.cloudflare.com/ips-v4/#

   ```yaml
   name: CloudFlare
   description: "Cloudflare Hosted IPs"
   whitelist:
   reason: "CloudFlare"
   cidr:
      - "173.245.48.0/20"
      - "103.21.244.0/22"
      - "103.22.200.0/22"
      - "103.31.4.0/22"
      - "141.101.64.0/18"
      - "108.162.192.0/18"
      - "190.93.240.0/20"
      - "188.114.96.0/20"
      - "197.234.240.0/22"
      - "198.41.128.0/17"
      - "162.158.0.0/15"
      - "104.16.0.0/13"
      - "104.24.0.0/14"
      - "172.64.0.0/13"
      - "131.0.72.0/22"
   ```

4. Restart Crowdsec or the entire npmplus stack.
