# Picture Management

This page covers how I am currently handling "merging" pictures between my Sony mirrorless camera(s) and personal phone (Pixel 7) with images already synced to my server via [nextcloud](./cloud).

Limitation, the symlinks do not maintain the original files date of creation/modification.

## Automated

Pre-requities:

- Create a temporary directory that contains a copy of the pictures desired. 
- Have explicit path of temporary directory with photos to be symlinked (e.g. `/mnt/user/backups/Adam/Phone\ Backup/2024/02`)
- Have explicit path of source location on the server (e.g. `/mnt/user/pictures/Gaming/FSX`)
- Have explicit path of destination location on the server (e.g. `/mnt/user/pictures/Gaming/Test_Destination`)

### Photo Symlink Script

There are two scripts that the photo symlink creation process use. One that is windows native (ends in `.bat`) and the other in shell. (ends in `.sh`)

Both scripts behave the same way natively when run on their respective operating environments.

On Windows:

- The script checks for the existence of plink, asks for the temporary directory, source directory, destination directory, and the root password for the server. Afterwards it will plink to the server to the hard-coded script location where the .sh file lives. [/mnt/user/DevRack/DevRack/scripts/photo_symlink.sh](https://github.com/adamzvolanek/DevRack/blob/main/scripts/photo_symlink.sh)

Common issues when running on windows:

- Command window quickly disappears after running
  - Check the destination directory the phone photos are added.
  - Verify the `.sh` script is executable. If not, PuTTY into Alexandria as root and issue `chmod u+x /mnt/user/DevRack/DevRack/scripts/photo_symlink.sh`

On Unraid:

- If the temporary, source, and destination directories are not provided as arguements, it prompts the user for input; the script also performs validation of paths existing prior to executing. It then generates a list of files in the temporary directory to loop over generating symlinks from the source directory to the destination directory. A touch command is run to preserve file modification time and the output is shown to the user.

## Manual Steps

- Start [Krusader](./unraid#once-booted).
- Once started navigate to `/mnt/user/pictures/...` on one side of the navigation tree, and navigate to `/mnt/user/backups/...` on the other side.
- Identify date range of Pixel images to by symlinked and "CTRL+Left-Click" all images from personal phone panel.
- "Left-Click" and drag images using the "Link Here" function.
