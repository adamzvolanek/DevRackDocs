Immich Kiosk Setup

## Using Raspberry Pi Zero 2 W

### Downloads

1. Download [DietPi](https://dietpi.com/#download).
2. Download [etcher](https://etcher.balena.io/).

### Steps for Windows

1. Extract DietPi OS whence downloaded.
2. Flash DietPi to microSD card via Etcher.
3. Re-mount the microSD card and edit `dietpi-wifi.txt`.
   1. In dietpi-wifi.txt enter WIFI_SSID and WIFI_KEY. e.g.
      1. `WIFI_SSID`='Name of SSID'
      2. `WIFI_KEY[0]`='Password of SSID'
4. Replace the `dietpi.txt` with the following file: [dietpi.txt](https://github.com/adamzvolanek/DevRack/blob/main/immich-kiosk-project/dietpi.txt)
5. Boot
   1. Monitor assigned IP via DHCP
   2. Chromium RAM warning expected.
6. Login as dietpi to PI via SSH.
7. Type, `cd /home/dietpi/` to change directories to dietpi's home.
8. Type, `touch setup_script.sh` to create the setup script file.
9. Type, `nano setup_script.sh` to open and edit the setup script file.
10. Paste in contents of [Automation_Custom_Script.sh](https://github.com/adamzvolanek/DevRack/blob/main/immich-kiosk-project/Automation_Custom_Script.sh)
11. Edit the immich values:
    1. `immich_api_key` with a dedicated API key from respective Immich account
    2. `immich_url` with Immich server web address.
    3. `album` with the album ID. e.g. 12345678-1234-1234-1234-12345678
12. Type, `sudo sh setup_script.sh` to run the script.
13. Type, `sudo init 6`.

### Steps for Linux

These are **untested**!

1. Extract DietPi OS whence downloaded.
2. Flash DietPi to microSD card via Etcher.
3. Re-mount the microSD card and edit `dietpi-wifi.txt`.
   1. In dietpi-wifi.txt enter WIFI_SSID and WIFI_KEY. e.g.
      1. `WIFI_SSID`='Name of SSID'
      2. `WIFI_KEY[0]`='Password of SSID'
4. Replace the `dietpi.txt` with the following file: [dietpi.txt](https://github.com/adamzvolanek/DevRack/blob/main/immich-kiosk-project/dietpi.txt)
5. **If on windows skip to step 8!** <br/> Download the [Automation_Custom_Script.sh](https://github.com/adamzvolanek/DevRack/blob/main/immich-kiosk-project/Automation_Custom_Script.sh) script to your desktop
6. Edit the immich values
    1. `immich_api_key` with a dedicated API key from respective Immich account
    2. `immich_url` with Immich server web address.
    3. `album` with the album ID. e.g. 12345678-1234-1234-1234-12345678
7. Paste the `Automation_Custom_Script.sh` into the /boot/ partition of the microSD card.
8. Boot
