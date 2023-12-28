# AdGuard

This page covers the setup of [AdGuard](https://github.com/AdguardTeam/AdGuardHome/wiki/Docker) to deploy in [my](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/core/adguard.yaml) docker-compose stack(s).

## Manual Steps

### Settings/General Settings

Navigate to "Settings/General settings" (`http://<server_ip>/#settings`). These settings can be edited per your desired configuration, however current settings include:

- [X] "Block domains using filters and hosts files"
  - "Filter update interval" to 24 Hours
- [ ] "Use AdGuard browsing security web service"
- [ ] "Use AdGuard parental control web service"
- [ ] "Use Safe Search"

Within **Logs configuration**

- [X] "Enable log"
- [ ] Anonymize client IP
- Query log rotation
  - 30 days

Within **Statics configuration**

- [X] Enable statistics
- Statics retention
  - 30 days

Ensure you click "Save" at the bottom of the page.

### Settings/DNS Settings

Current "Upstream DNS servers" include,

```bash
https://dns.cloudflare.com/dns-query
1.1.1.1
https://dns.google/dns-query
8.8.8.8
```

Select your preferred method of querying out DNS requests: "Load-balancing", "Parallel requests", "Fastest IP address". Currently have "Load-balancing" selected.

The remainder of the settings are set to default.

### Settings/Client Settings

Populate the "Persistent clients" table with known devices and their IP addresses associating appropriate tags to each. This helps in identifying traffic on the AdGuard homepage.

### Settings/DHCP Settings

Disable DHCP by selecting "Disable DHCP Server".

### Filters/DNS blocklists

Current filters applied to AdGuard and enabled.

| Name | List URL |
| ----------- | ----------- |
| AdGuard DNS Filter | https://adguardteam.github.io/HostlistsRegistry/assets/filter_1.txt       |
| AdAway Default Blocklist  | https://adguardteam.github.io/HostlistsRegistry/assets/filter_2.txt        |
| NoCoin Filter List | https://adguardteam.github.io/HostlistsRegistry/assets/filter_8.txt |
| Advertising Filter  1 | https://adaway.org/hosts.txt        |
| Advertising Filter 1   | https://v.firebog.net/hosts/AdguardDNS.txt       |
| Tracking & Telemetry Filter 1  | https://v.firebog.net/hosts/Easyprivacy.txt       |
| Malicious Filter 1 | https://v.firebog.net/hosts/RPiList-Malware.txt |
| Malicious Filter 2 | https://v.firebog.net/hosts/RPiList-Phishing.txt |

### Filters/Custom filtering rules

Currently have the following custom filtering rules in place after some usability issues with various services, sites, apps.

```bash
@@||vortex.data.microsoft.com^$important
@@||tr.www.cloudflare.com^$important
@@||static.cloudflareinsights.com^$important
@@||links.h6.hilton.com^$important
@@||alb.reddit.com^$important
```

## Automated Steps

placeholder text
