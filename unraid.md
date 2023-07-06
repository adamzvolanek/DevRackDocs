# Unraid

My server is based on Unraid and will transition to ZFS-based hard disks. Developement is done on a decade+ old laptop that runs Unraid purely for docker-compose develpoment.

This page covers the setup of my Unraid server.

## Prerequisite

Requires a USB Flash drive.

## Download

The free 30-day trail of Unraid can be found [here](https://unraid.net/download).

A flash drive ISO can be found in my DevRack repository. Link to the Unraid 6.9.2 ISO is pending.

- Select Unraid Version to run
- Define a server name (dev-laptop). Note: it defaults to Tower
- Select a network mode. I recommend setting a static IP
- Select USB Device
- Click Write

### Physical Action

Plug in flash drive to laptop and allow boot to flash-drive.

### Once Booted

Once the device is booted, navigate to your devices IP in a web-browser `http://dev-laptop.local` or `http://<Static_IP>` to reach the Unraid GUI.

You will be greeted by the registration screen, select trial.

Select your primary hard-drive as Disk 1 and start the array at the bottom of the page.

Install the community apps button by selecting 'Plugin' and . Refresh the page and select the newly created 'Apps' button. Click 'I Understand' on the Disclaimer and Plugins (appears after) window.

In the Unraid settings --> Disk Settings change 'Enable auto start' to Yes.

*If using an ssd in the array*, install 'Dynamix SSD Trim'. Have SSD Trim scheduled for daily.

### Setting up Docker network

Open the Unraid terminal and type `docker network create {DOCKER_NETWORK}`. Replacing the brackets and contents of DOCKER_NETWORK with the docker network name desired. The variable `${DOCKER_NETWORK}` is also referenced as part of the docker-compose configuration found [here](https://github.com/adamzvolanek/DevRack/tree/main/docker-compose#readme).

### Installing Docker Compose

Install docker-compose by going into Apps and searching 'docker compose'. Once installed, return to the docker tab and view the compose tab at the bottom of the page. You can add a new stack and test from here.

### Setting up Git

Create a deploy key as part of the DevRack repository, `https://github.com/<profile>/<repository>/settings/keys`. Unraid support git out of the box.

Create a share to house the git files and use the terminal or ssh to clone your repository.

## Tips

If this drive was previously used, it may read it is 'Unmountable: Unsupported partition layout':

- Install the 'Unassigned Devices' and the 'Unassigned Devices Plus' plugin.
- Navigate to Settings --> Unassigned Devices and enable Destructive Mode.
- Return to Main and begin deleting the partitions by selecting the red x.
- Once all partitions are deleted, a 'Format' button will appear. Select it and format the drive.
- Assign the disk and start the array.

If password is not working for root during SSH:

- Select the terminal button on the top-right and type `passwd`. Update your password.
