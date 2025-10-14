## Using Raspberry Pi Zero 2 W

Overall a success apart from the lack of a touchscreen and an extra cable purchased that I didn't need. If I was to do it again, I would either purchase a larger PI or smaller/compatible display for the Pi Zero 2 W.

Instructions updated with Immich release v2.X.X!

### Purchases List and Notes

Immich Kiosk Version 2

- 15.6 inch 1920x1080 display [Amazon Link](https://www.amazon.com/dp/B0CN771QHZ)
- Raspberry Pi Zero 2 W
  - [Raspberry PI Zero 2 W Heatsink](https://www.amazon.com/dp/B09VFHJF85)
  - [MicroSD Card](https://www.amazon.com/dp/B07P3D6Y5B)
- [Micro USB to C](https://www.amazon.com/dp/B0744BKDRD) for power from display.
- [Mini HDMI Cable](https://www.amazon.com/dp/B0FDB9WCYZ)
- USB-C Power Brick to power display and PI.

</details>

<details><summary>Immich Kiosk Version 1</summary>

- Raspberry Pi Zero 2 W
- 10.1 inch 1280x800 display [Amazon Link](https://www.amazon.com/dp/B0BPM9VTY6)
  - Note: Touchscreen will not work without driver install. In-op for Raspberry Pi Zero 2 W.
  - Comes with posts to screw Pi Zero 2 at two points.
- [Micro USB to C](https://www.amazon.com/dp/B0746NHSCZ) for touchscreen, not used.
- [Mini HDMI to HDMI Adapter](https://www.amazon.com/dp/B09MD23K4X)
  - Would recommend a traditional mini-HDMI to HDMI cable over adapter cable combo.
- [Short HDMI Cable](https://www.amazon.com/dp/B0B5KN6853)
  - Would recommend buying shortest HDMI to mini-HDMI rather than adapter cable combo.
- [Anker 2 Pack Dual Port Charger](https://www.amazon.com/Charger-Anker-Foldable-PowerPort-Samsung/dp/B07DFWKBF7)
  - Powers both display and Pi Zero 2.
- [Micro USB to USB](https://www.amazon.com/YOKIVE-Switch-Extension-Reduced-6-56-Feet/dp/B0BGSKFLS5) or something similar to power Raspberry PI.

</details>

***

### Downloads

1. Download [DietPi](https://dietpi.com/#download).
2. Download [etcher](https://etcher.balena.io/).

### Immich Setup

1. Create Immich Kiosk User
2. Select **New API Key**
   1. Name the API Key. e.g. `Acer15Mom`
      1. `<DisplayType><Size><UsersName>`
   2. Under Permission, check **album.read**.
   3. Select **Create**.
   4. Take note of the API Key.
   5. For instructions using Hoppscotch to generate API Key, see bottom of page prior to photos.

For **each** ImmichKiosk Picture Frame.

1. Have user create an Album, populate with pictures.
2. Have user share Album with the Immich Kiosk User.
3. Login and navigate to album as Immich Kiosk User and note the UID after albums in the URL. This will be `album` for the Album_ID in the config.yaml file.
   1. Alternatively, you can use Hoppscotch to GET the album ID using the `immich_api_key` by having the parameters set to key:`shared` and value: `true`.

### Steps for Windows

1. Locate DietPi OS once downloaded.
2. Flash DietPi to microSD card via Etcher.
3. Re-mount the microSD card and edit `dietpi-wifi.txt`.
   1. In dietpi-wifi.txt enter WIFI_SSID and WIFI_KEY. e.g.
      1. `WIFI_SSID`='Name of SSID'
      2. `WIFI_KEY[0]`='Password of SSID'
4. Replace the `dietpi.txt` with the following file: [dietpi.txt](https://github.com/adamzvolanek/DevRack/blob/main/immich-kiosk-project/dietpi.txt)
5. Boot
   1. Monitor assigned IP via DHCP
   2. Chromium RAM warning expected on first boot.
      1. This will go away once the `Automation_Custom_Script` is run.
6. Login as **dietpi** to PI via SSH.
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

These steps are **untested**!

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

## Photos

[![Front of the Digital Photo Frame](https://docs.adamzvolanek.com/uploads/images/gallery/2025-02/scaled-1680-/epf0vZFEU8j0XD0C-pxl-20250205-023059383.jpg)](https://docs.adamzvolanek.com/uploads/images/gallery/2025-02/epf0vZFEU8j0XD0C-pxl-20250205-023059383.jpg)

[![Rear of the Digital Photo Frame](https://docs.adamzvolanek.com/uploads/images/gallery/2025-02/scaled-1680-/dp3HZIy5ZVwGBLr1-pxl-20250205-022739548.jpg)](https://docs.adamzvolanek.com/uploads/images/gallery/2025-02/dp3HZIy5ZVwGBLr1-pxl-20250205-022739548.jpg)
