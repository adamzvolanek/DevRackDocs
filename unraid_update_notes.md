# Updating Unraid

Covering the process of updating my Unraid from 6.11.5 to 6.12.8.

## Steps

- Update all the plugins to the latest version
- Update all docker containers to their latest image

Prompted to wait for download to complete in the background:

> Plugin Update Helper: 08-03-2024 20:10. Notification. unRAID version change detected, please don't reboot just yet! Download from plugin(s) for new unRAID v6.12.8 started in background! You will be notified when the download(s) is/are finished!

Follow up 6 minutes later:

> Nvidia Driver v550.40.07 download successful! Everything done, please reboot to install unRAID v6.12.8!

Rebooting.

## Post Reboot

My AdGuard environment [file](https://github.com/adamzvolanek/DevRack/blob/main/docker-compose/core/adguard.env) immediately threw a bug with the change in networking naming in Unraid's update.

Be aware of user-scripts.

Common Applications Backup update *does* import settings from previous version, **so long as** previous version remains installed.

Docker Start Order:

1. Cloudflare-DDNS
2. AdGuard
3. NginxProxyManager
4. postgres_authentik
5. redis
6. authentik-worker
7. authentik
8. nextcloud_db
9. nextcloud
10. delugevpn
11. Jellyfin
12. jellyseerr
13. wikijs_db
14. wikijs
15. UniFi-Protect-Backup
16. radarr
17. sonarr
18. flaresolverr
19. prowlarr
20. homeassistant
21. scrutiny
22. qbittorrentvpn
23. recyclarr
24. sqlitebrowser
25. phpmyadmin
26. luckyBackup
27. lidarr
28. Krusader
29. AllTheMods8
30. DiskSpeed
31. Czkawka

Added the backblaze backup script as a post-run script. Start a manual backup to test.
