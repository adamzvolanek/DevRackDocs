# Cheat Sheet of Useful Commands

## docker-compose

- List all running containers: `docker-compose ps`
- Create and start all containers in the background using a docker-compose.yml file from the current directory: `docker-compose up -d`
- Start all containers, rebuild if necessary: `docker-compose up --build`
- Start all containers using an alternate compose file: `docker-compose --file path/to/file up`
- Stop all running containers: `docker-compose stop`
- Stop and remove all containers, networks, images, and volumes: `docker-compose down --rmi all --volumes`
- Follow logs for all containers: `docker-compose logs --follow`

## Git

- Global Git config lives in: `C:/Users/<username>/.gitconfig`
- Change git gpg.program to use above location: `git config --global gpg.program "C:/Users/<username>/.gitconfig"`

## Unraid Commands

- Shut-down/Reboot: `/sbin/<command>`
  - Can replace `<command>` with reboot, poweroff, and shutdown
- Run diagnostics: `diagnostics`
- Tail the syslog: `tail -f /var/log/syslog`
- See Config file: `vi /boot/syslinux.cfg`
- Create backup of usb and store on disk: `dd if=/dev/sda of=/mnt/disk1/unraid.img`
- Check power on hours for all drives: `for drive in $(ls -la /dev | grep -Ev 'sda|sd[a-z][0-9]' | grep sd[a-z] | awk '{print $10}'); do hours=$(smartctl --all /dev/${drive} | grep Power_On_Hours | awk '{print $10}'); echo "Power on Hours for ${drive}: ${hours}"; echo ''; done`
