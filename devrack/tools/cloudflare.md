This page covers the setup of Cloudflare as related to Alexandria. These steps apply to all CloudFlare domains hosted by Alexandria.

## CloudFlare Domain

Select Cloudflare domain.

### AI Crawl Control

- In Security Tab Block all Crawlers.
- In Signals, enable "Managed robots.txt".

### DNS

Configure DNS A-Records and CNAMES as needed. For each, ensure they are proxied per Cloudflare policy.

- Enable DNSSEC

### SSL/TLS

- Configured *.domain.tld, domain.tld of Universal Type is active.
- [X] Always Use HTTPS
- HSTS Settings:
  - [X] Enable HSTS (Strict-Transport-Security)
  - Max Age Header (max-age): 6 months
  - [X] Apply HSTS policy to subdomains (includeSubDomains)
  - [X] Preload
  - [X] No-Sniff Header
- Minimum TLS Version: TLS 1.2
- [X] Opportunistic Encryption
- [X] TLS 1.3
- [X] Automatic HTTPS Rewrites
- [X] Certificate Transparency Monitoring

### Client Certificates

- If needing to crate one, select "Cloudflare Managed CA", Generate private ky and CSR with Cloudflare of at least RSA (2048), select a validity period for your certificate.

### Origin Server

- Includes single Origin Certificate

## Security

### Security Rules

Within Custom Rules: 

1. Bot Protect
   1. "When incoming requests match..." (Known Bots) equals true.
   2. Then take action: Block
   3. Execution Order: First
   4. Status: Active
2. AND AI Scrapers and Crawlers rule
3. AND Country Block
4. AND Outside Country Challenge

Within Rate limiting rules:

1. Leaked credential check
  2. Field: Password Leaked, equals, an enabled value.
3. When rate exceeds...: 3 at 10 seconds
4. Then take action...: Block
5. For duration...: 10 seconds
6. Select Save.

### Settings

- [X] AI Labyrinth
- [X] Bot fight mode
- [X] Browser integrity check
- [X] Challenge passage.
  - Timeout: 1 day
- [X] Cloudflare managed ruleset
- Configure AI bot policies
  - Search: Block
  - Agent: Block
  - Training: Block
- [ ] Continous script monitoring
- [X] Email Address Obfuscation
- [X] Hotlink Protection
- [X] HTTP DDoS attack protection
- [X] Leaked credentials detection
- Manage your robots.txt
  - Instruct AI bots to not scrape content
- [X] Network-layer DDoS attack protection
- [X] Replace insecure JavaScript libraries
- [ ] Schema validation
- [ ] Security.txt
- [X] SSL/TLS DDoS attack portection
- [X] Web asset discovery

## Speed

### Settings

Under Site Recommendations, select **Enable all available settings**. Select Content Optimization tab and configure as follows:

- [X] Speed brain
- [ ] Cloudflare Fonts
- [X] Early Hints
- [ ] Rocket Loader
- Shared Dictionary Compression set to Off

Select "Protocol Optimization" as follows:

- [X] HTTP/2 to Origin
- [X] HTTP/3 (with QUIC)
- [X] 0-RTT Connection Resumption

### Smart Shield

- [X] Smart Tiered Cache

## Caching

### Configuration

- Caching Level: Standard
- Browser Cache TTL: 5 hours
- [ ] Crawler Hints
- [ ] Always Online
- [ ] Development Mode

### Cache Rules

- Create cache rule named "Bypass".
- If incoming request match... "Custom filter expression".
- When incoming reuqests match...
  - Field: Hostname
  - Operator: equals
  - Value: subdomain.domain.tld
    - OR
  - Field: Hostname
  - Operator: equals
  - Value: subdomain.domain.tld
  - Expression preview: `(http.host eq "subdomain.domain.tld") or (http.host eq "subdomain.domain.tld")`
- Then...
  - Cache eligibility: Bypass cache
- Select **Save** at the bottom of the page.

## Rules

### Page rules

Create one page rule.

- URL: subdomain.domain.tld
- Then the settings are: Cache Level
  - Bypass

### Settings

Within Managed Transforms

- [X] Add visitor location headers

Within URL Normalization

- Normalization type: RFC-3986
- [X] Normalize incoming URLs
- [ ] Normalize URLs to origin

## Network

- [X] IPv6 Compatibility
- [ ] gRPC
- [X] WebSockets
- [ ] Pseudo IPv4
- [X] IP Geolocation
- Maximum Upload Size: 100 MB
- [X] Network Error Logging
- [X] Onion Routing
