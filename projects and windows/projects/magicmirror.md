This page covers the setup of MagicMirror (Client) on Raspberry Pi Zero 2 W

## Install DietPi

- Install [DietPi](https://dietpi.com/)
- Flash using [Balenda Etcher](https://etcher.balena.io/)

### Configure DietPi

- Re-plug into the (Linux) PC, open the main partition and the boot directory.

1. As root modify `dietpi-wifi.txt` file with Wifi name and password.
2. Open `dietpi.txt`
  3. Update `AUTO_SETUP_KEYBOARD_LAYOUT` to be `us`
  4. Update `AUTO_SETUP_TIMEZONE` to be `America/Chicago`
  5. Modify `AUTO_SETUP_NET_WIFI_ENABLED` to 1
  6. Modify `AUTO_SETUP_DHCP_TO_STATIC` to 1
  7. Modify `AUTO_SETUP_NET_HOSTNAME` to `MagicMirrorClient`
  8.
