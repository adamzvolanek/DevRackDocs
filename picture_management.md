# Picture Management

This page covers how I am currently handling "merging" pictures between my Sony mirrorless camera(s) and personal phone (Pixel 7) with images already synced to my server via [nextcloud](./cloud).

Limitation, the symlinks do not maintain the original files date of creation/modification.

## Automated

Pending.

## Manual Steps

- Start [Krusader](./unraid#once-booted).
- Once started navigate to `/mnt/user/pictures/...` on one side of the navigation tree, and navigate to `/mnt/user/backups/...` on the other side.
- Identify date range of Pixel images to by symlinked and "CTRL+Left-Click" all images from personal phone panel.
- "Left-Click" and drag images using the "Link Here" function.
