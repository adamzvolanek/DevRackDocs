# Picture Management

This page covers how I am currently handling "merging" pictures between my Sony mirrorless camera(s) and personal phone (Pixel 7) with images already synced to my server via [nextcloud](./cloud).

Limitation, the symlinks do not maintain the original files date of creation/modification.

## Automated

This does not work as expected. Requires a *copy* of the photos wanted in a separate directory, defeating the purpose of using symlinks...

Future-work: Have user create a directory with the copy of phone pictures desired. Script will prompt for temporary directory with copies of photos, ask for source directory (where photos are backed up to), and destination directory. Have script run through list of photos in temporary directory (loop) and symlink matching file names from source to destination directory.

Pre-requities:

- Create directory that contains a copy of the pictures desired.
- Have explicit path of temporary directory with photos to be symlinked. (from source)
- Have explicit path of source location on the server (e.g. `/mnt/user/pictures/Gaming/FSX`)
- Have explicit path of destination location on the server (e.g. `/mnt/user/pictures/Gaming/Test_Destination`)

### `photo_symlink` script

There are two scripts that the photo symlink creation process use. One that is windows native (ends in `.bat`) and the other in shell. (ends in `.sh`)

Both scripts behave the same way natively when run on their respective operating environments.

On Windows:

- The script checks for the existence of plink, asks for the source directory, destination directory, and the root password for the server. Afterwards it will plink to the server to the hard-coded script location where the .sh file lives. [/mnt/user/DevRack/DevRack/scripts/photo_symlink.sh](https://github.com/adamzvolanek/DevRack/tree/main/scripts)

On Unraid:

- If the source and destination directories are not provided as arguements, it prompts the user for input; the script also performs validation of path existing prior to executing. It then generates a list of files in the source directory to loop over generating symlinks in the source directory. A touch command is run to preserve file modification time.

## Manual Steps

- Start [Krusader](./unraid#once-booted).
- Once started navigate to `/mnt/user/pictures/...` on one side of the navigation tree, and navigate to `/mnt/user/backups/...` on the other side.
- Identify date range of Pixel images to by symlinked and "CTRL+Left-Click" all images from personal phone panel.
- "Left-Click" and drag images using the "Link Here" function.
