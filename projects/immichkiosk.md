Immich Kiosk Setup

Recall, SHIFT+INSERT allows paste into PuTTY via VIM.

## Raspberry Pi Zero 2 W Setup

1. Download [DietPi](https://dietpi.com/#download).
2. Download [etcher](https://etcher.balena.io/).
3. Extract DietPi OS whence downloaded.
4. Load to microSD card via Etcher.
5. Re-mount the microSD card and edit `dietpi-wifi.txt` and `dietpi.txt`
   1. In dietpi-wifi.txt enter WIFI_SSID and WIFI_KEY. e.g.
      1. `WIFI_SSID`='Name of SSID'
      2. `WIFI_KEY[0]`='Password of SSID'
   2. In dietpi.txt edit the following:
      1. `AUTO_SETUP_TIMEZONE`=`America/Chicago`
      2. `AUTO_SETUP_NET_ETHERNET`=`0`
      3. `AUTO_SETUP_NET_WIFI`=`1`
      4. `AUTO_SETUP_NET_HOSTNAME`=`ImmichKiosk-DietPi`
      5. `CONFIG_ENABLE_IPV6`=`0`
      6. `SOFTWARE_DISABLE_SSH_PASSWORD_LOGINS`=`0`

### Once Booted

1. Verify IP address of the DietPI PC and SSH in as root. Enter default password `dietpi`.
2. Select Chromium and VIM software to be installed.
3. Reboot using `init 6`.

### Immich Kiosk Install and Setup

1. Login as root and navigate to home directory, `cd ~`.
2. Create immich folder, `mkdir immichkiosk`.
3. Download the example config file, `wget -O immichkiosk/config.yaml https://raw.githubusercontent.com/damongolding/immich-kiosk/refs/heads/main/config.example.yaml`.
4. Download the Linux arm64 package, `wget -O immich-kiosk_Linux_arm64.tar.gz https://github.com/damongolding/immich-kiosk/releases/download/v0.15.1/immich-kiosk_Linux_arm64.tar.gz`.
5. Unpack the archive, `tar -zxvf immich-kiosk_Linux_arm64.tar.gz`.
6. Populate `config.yaml` with the following:
    1. `immich_api_key` with a dedicated API key from respective Immich account
    2. `immich_url` with Immich server web address.
    3. `album` with the album ID. e.g. 12345678-1234-1234-1234-12345678
    4. More items coming.

## AutoStart Setup

### Immich Kiosk System Service

1. Enter `dietpi-autostart` and select Option 11.
   1. Enter the local URL and port
2. Navigate to system services, `cd /etc/systemd/system`
3. Create immich-kiosk service, `touch immich-kiosk.service`
4. Populate with the following:
   1.  

        [Unit]
        Description=Immich Kiosk
        After=network.target
        StartLimitIntervalSec=0

        [Service]
        Type=simple
        Restart=always
        RestartSec=1
        User={your_user}
        WorkingDirectory=/home/{your_user}/immichkiosk
        ExecStart=/home/{your_user}/immichkiosk/immich-kiosk

       [Install]
       WantedBy=multi-user.target
5. Enable and auto-start the service using the following:
   1. `systemctl daemon-reload`
   2. `systemctl enable immich-kiosk`
   3. `systemctl start immich-kiosk`

### DietPi Kiosk Mode

1. Navigate to here, `cd /var/lib/dietpi/dietpi-software/installed/`
2. Modify the chromium-autostart.sh file with the example below:
   1.  

        #!/bin/dash
        # Autostart script for kiosk mode, based on @AYapejian: https://github.com/MichaIng/DietPi/issues/1737#issue-318697621

        # Resolution to use for kiosk mode, should ideally match current system resolution
        RES_X=$(sed -n '/^[[:blank:]]*SOFTWARE_CHROMIUM_RES_X=/{s/^[^=]*=//p;q}' /boot/dietpi.txt)
        RES_Y=$(sed -n '/^[[:blank:]]*SOFTWARE_CHROMIUM_RES_Y=/{s/^[^=]*=//p;q}' /boot/dietpi.txt)

        # Create a temporary xinitrc file to launch unclutter before chromium
        cat > /tmp/xinitrc.tmp << 'EOF'
        #!/bin/dash
        # Hide cursor
        unclutter -idle 0 -root &

        # Launch Chromium with provided arguments
        exec "$@"
        EOF
        chmod +x /tmp/xinitrc.tmp

        # Command line switches: https://peter.sh/experiments/chromium-command-line-switches/
        # - Review and add custom flags in: /etc/chromium.d
        CHROMIUM_OPTS="--kiosk --no-memcheck --window-size=${RES_X:-1280},${RES_Y:-720} --window-position=0,0"

        # If you want tablet mode, uncomment the next line.
        #CHROMIUM_OPTS+=' --force-tablet-mode --tablet-ui'

        # Home page
        URL=$(sed -n '/^[[:blank:]]*SOFTWARE_CHROMIUM_AUTOSTART_URL=/{s/^[^=]*=//p;q}' /boot/dietpi.txt)

        # RPi or Debian Chromium package
        FP_CHROMIUM=$(command -v chromium-browser)
        [ "$FP_CHROMIUM" ] || FP_CHROMIUM=$(command -v chromium)

        # Use "startx" as non-root user to get required permissions via systemd-logind
        STARTX='xinit'
        [ "$USER" = 'root' ] || STARTX='startx'

        exec "$STARTX" /tmp/xinitrc.tmp "$FP_CHROMIUM" $CHROMIUM_OPTS "${URL:-https://dietpi.com/}"

# Potentially Fully Scripted Upon Boot

```bash
#!/bin/bash

# Variables
immich_api_key="api_key"
immich_url="https://immich.example.com"
album_id="guid"

# Step 1: Create /opt/kiosk directory
mkdir -p /opt/kiosk

# Step 2: Download and extract immich-kiosk
wget -qO- https://github.com/damongolding/immich-kiosk/releases/download/v0.14.7/immich-kiosk_Linux_arm64.tar.gz | tar xz -C /opt/kiosk

# Step 3: Download config.example.yaml and save as config.yaml
wget -q https://raw.githubusercontent.com/damongolding/immich-kiosk/main/config.example.yaml -O /opt/kiosk/config.yaml

# Step 4: Update the keys in the config file
sed -i "s|api_key:.*|api_key: \"$immich_api_key\"|" /opt/kiosk/config.yaml
sed -i "s|url:.*|url: \"$immich_url\"|" /opt/kiosk/config.yaml
sed -i "s|hide_cursor:.*|hide_cursor: true|" /opt/kiosk/config.yaml
sed -i "s|show_time:.*|show_time: true|" /opt/kiosk/config.yaml
sed -i "s|time_format:.*|time_format: 12|" /opt/kiosk/config.yaml
sed -i "s|show_date:.*|show_date: true|" /opt/kiosk/config.yaml
sed -i "s|date_format:.*|date_format: MM/DD/YYYY|" /opt/kiosk/config.yaml
sed -i "s|disable_screensaver:.*|disable_screensaver: true|" /opt/kiosk/config.yaml
sed -i "s|album:.*|album:\n  - \"$album_id\"|" /opt/kiosk/config.yaml

# Step 5: Create systemd service file
cat <<EOL > /etc/systemd/system/kiosk.service
[Unit]
Description=Immich Kiosk
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
ExecStart=/opt/kiosk/immich-kiosk
WorkingDirectory=/opt/kiosk
Restart=always
RestartSec=1
User=root

[Install]
WantedBy=multi-user.target
EOL

# Reload systemd, enable
systemctl daemon-reload
systemctl enable kiosk.service
systemctl start kiosk.service

# Step 6: Fix Memory warning in chromium
sed -i 's|^CHROMIUM_OPTS="|CHROMIUM_OPTS="--no-memcheck |' /var/lib/dietpi/dietpi-software/installed/chromium-autostart.sh

echo "Installation and setup complete!"
```
