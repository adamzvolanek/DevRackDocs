This page covers the setup of Cloudflare as related to Alexandria.

## CloudFlare Domain

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

1. Bot Protect
   1. "When incoming requests match..." (Known Bots) equals true.
   2. Then take action: Block
   3. Execution Order: First
   4. Status: Active
2. AND AI Scrapers and Crawlers rule
3. 
4. AND Country Block
5. AND Outside Country Challenge
