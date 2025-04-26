My server is based on Unraid. Developement is done on a decade+ old laptop that runs Unraid purely for docker-compose develpoment.

This page covers the setup of my Unraid server.

## Prerequisite

Requires a USB Flash drive.

An alternative to using an USB Flash drive is leveraging an microSD card and a microSD to USB converter. Similar to [MobileMate USB 3.0 Reader](https://shop.sandisk.com/en-ie/products/accessories/memory-card-readers/sandisk-mobilemate-uhs-i-usb-3-0-microsd-reader-writer?sku=SDDR-B531-GN6NN) and a [high-endurance microSD card](https://shop.sandisk.com/products/memory-cards/microsd-cards/sandisk-high-endurance-uhs-i-microsd?sku=SDSQQNR-032G-GN6IA).

## Download

A 30-day trail of Unraid is offered [here](https://unraid.net/getting-started).

- Select Unraid Version to run
- Define a server name . Using "dev-laptop" going forward.
- Select a network mode. Recommend setting a static IP.
- Select USB Device
- Click Write

### Physical Action

Plug in flash drive to device and allow boot to flash-drive.

### Once Booted

Once the device is booted, navigate to your devices IP in a web-browser `http://dev-laptop.local` or `http://<Static_IP>` to reach the Unraid GUI.

You will be greeted by the registration screen, select trial.

Select your primary hard-drive as Disk 1 and start the array at the bottom of the page.

Install the community apps button by selecting 'Plugin' and . Refresh the page and select the newly created 'Apps' button. Click 'I Understand' on the Disclaimer and Plugins (appears after) window.

In the Unraid settings --> Disk Settings change 'Enable auto start' to Yes.

*If using an ssd as disk share*, install 'Dynamix SSD Trim'. Have SSD Trim scheduled for daily.

Setup any additional Unraid shares as desired.

#### Secure Shares

Create a user within Unraid's "Users" tab. Upon creation of a user, verify permission of any shares that set as "Secure" and your user has Read/Write permissions.

For my own deployment, I use powershell to mount network drives, [network_drive_mounts](https://github.com/adamzvolanek/DevRack/blob/main/scripts/windows_11).

Note: You may need to allow PowerShells to be run on your Windows PC. Open Powershell as administrator and type `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` than select 'Y'.

### Setting up Docker network

Open the Unraid terminal and type `docker network create {DOCKER_NETWORK}`. Replacing the brackets and contents of DOCKER_NETWORK with the docker network name desired. The variable `${DOCKER_NETWORK}` is also referenced as part of the docker-compose configuration found [here](https://github.com/adamzvolanek/DevRack/tree/main/docker-compose#readme).

### Installing Docker Compose

Install docker-compose by going into Apps and searching 'docker compose' by dcflachs. Once installed, return to the docker tab and view the compose tab at the bottom of the page. Instructions for setting up docker-compose can be found [here](./installs#creating-a-docker-compose-stack)

Optionally, create a share to house the git files and use the terminal or ssh to clone your repository. Then set the Compose Project Directory to the backup repo. e.g. `/mnt/user/share/repo/docker-compose-backups/server_name`. Having the docker compose project directory point to a Git repo allows the user to backup their configs to GitHub and maintain source control all docker compose files. Likewise one *can* update their docker compose files from GitHub rather than directly on Unraid itself.

### Setting up Git

Optionally, create a deploy key as part of the DevRack repository, `https://github.com/<profile>/<repository>/settings/keys`. Unraid includes git.

To begin installing dockers continue to [pre-docker and plugin setup](../page/pre-docker-and-plugin-setup)

---

## Tips + Odds & Ends

If this drive was previously used, it may read it is 'Unmountable: Unsupported partition layout':

- Install the 'Unassigned Devices' and the 'Unassigned Devices Plus' plugin via Community Apps.
- Navigate to Settings --> Unassigned Devices and enable Destructive Mode.
- Return to Main and begin deleting the partitions by selecting the red x.
- Once all partitions are deleted, a 'Format' button will appear. Select it and format the drive.
- Assign the disk and start the array.

If password is not working for root during SSH:

- Select the terminal button on the top-right and type `passwd`. Update your password.

### Creating GMail SMTP Relay

Navigate to your Google Accounts [app passwords](https://myaccount.google.com/apppasswords) and create a new app specific password.

### Nvidia GPU Plugin

[Link](https://forums.unraid.net/topic/98978-plugin-nvidia-driver/) to forum post.
