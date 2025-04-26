This page covers the setup of [Uptime-Kuma](https://uptime.kuma.pet/) in my docker-compose cloud stack.

## Setup

### Account Setup

Upon start of Uptime-Kuma, setup an account with a password to get started. After setup, head over to your account "Settings" at the top-right and select "Security". 2FA setup will be completed later.

### Status Pages

1. Select "New Status Page"
2. Name: Alexandria
3. Slug: alexandria

### Settings

Sections skipped are to be left blank.

1. General
   1. Search Engine Visibility
      - [X] Discourage search engines from indexing site.
   2. Entry Page
      - [X] Status Page - Alexandria
   3. Select save.
2. Notifications
   1. Setup Notifications
      - Notification Type: Email (SMTP)
      - Friendly Name: <Fillout appropriately>
      - Hostname: smtp.domain.tld
      - Port: 465
      - Security: TLS (465)
      - SMTP username: Your email address
      - SMTP password: Application specific email password
      - From email: Must match SMTP username
      - To Email: <Email to be sent to>
      - Custom Subject: Leave blank
3. Reverse Proxy
   1. If using Cloudflare Tunnel, setup accordingly.
4. Security
   1. Setup 2FA.
5. API Keys
   1. Add API Key
      1. Name: Homepage
      - [X] Don't expire

### Adding Monitors

1. Add New Monitor
   1. Monitor Type: https
   2. Friendly Name: Service Name
   3. URL: https://{Service Name}.domain.tld
   4. Heartbeat Interval: 300
   5. Retires: 2
   6. Monitor Group: Dockers
2. Save

### Maintenance Windows

1. Title: Regular Maintenance
2. Description: Limited serviec is available at 0315 CST.
3. Add all affected monitors.
4. Status Pages: Check all
5. Date and Time
   1. Cron Expression
   2. `30 2 * * *`
   3. Duration: 120 (Minutes)
   4. Timezone: UTC-06:00
6. Save

### Networking Setup

Leverage [CloudFlare ZeroTrust Tunnels](https://github.com/louislam/uptime-kuma/wiki/Reverse-Proxy-with-Cloudflare-Tunnel)
