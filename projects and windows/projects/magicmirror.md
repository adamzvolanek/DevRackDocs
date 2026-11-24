This page covers the setup of MagicMirror (Client) on Raspberry Pi Zero 2 W

## Install DietPi

- Install [DietPi](https://dietpi.com/)
- Flash using [Balenda Etcher](https://etcher.balena.io/)

### Configure DietPi

- Re-plug into the (Linux) PC, open the main partition and the boot directory.

1. As root modify `dietpi-wifi.txt` file with Wifi name and password.
2. Open `dietpi.txt`
    1. Update `AUTO_SETUP_KEYBOARD_LAYOUT` to be `us`
    2. Update `AUTO_SETUP_TIMEZONE` to be `America/Chicago`
    3. Modify `AUTO_SETUP_NET_WIFI_ENABLED` to 1
    4. Modify `AUTO_SETUP_DHCP_TO_STATIC` to 1
    5. Modify `AUTO_SETUP_NET_HOSTNAME` to `MagicMirrorClient`
    6. Modify `AUTO_SETUP_BROWSER_INDEX` to -2
    7. Modify `AUTO_SETUP_AUTOMATED` to 1
    8. Modify `AUTO_SETUP_INSTALL_SOFTWARE_ID` to 9
       1. Latest NodeJS
    9. Add `AUTO_SETUP_INSTALL_SOFTWARE_ID` to 17
       1. Latest Git
    10. Modify `AUTO_SETUP_AUTOMATED` to 1.
3. Boot dietpi and login as root
4. Follow boot prompts

## MagicMirror Client Installation

1. Follow steps for client only installation [here](https://docs.magicmirror.builders/getting-started/installation.html#manual-installation).
