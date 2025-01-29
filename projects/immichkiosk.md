Immich Kiosk Setup

Recall, SHIFT+INSERT allows paste into PuTTY via VIM.

## Raspberry Pi Zero 2 W Setup

### Downloads

1. Download [DietPi](https://dietpi.com/#download).
2. Download [etcher](https://etcher.balena.io/).

### Pre-Boot Setup

1. Extract DietPi OS whence downloaded.
2. Load to microSD card via Etcher.
3. Re-mount the microSD card and edit `dietpi-wifi.txt`.
   1. In dietpi-wifi.txt enter WIFI_SSID and WIFI_KEY. e.g.
      1. `WIFI_SSID`='Name of SSID'
      2. `WIFI_KEY[0]`='Password of SSID'
4. Replace the `dietpi.txt` with the following file: [Broken Link]()
5. Download the [Automation_Custom_Script.sh]() script to your desktop
6. Edit the immich values
    1. `immich_api_key` with a dedicated API key from respective Immich account
    2. `immich_url` with Immich server web address.
    3. `album` with the album ID. e.g. 12345678-1234-1234-1234-12345678
7. Paste the `Automation_Custom_Script.sh` into the /boot (ext4 format) partition of the microSD card.
8. Boot PI

### Immich Kiosk Install and Setup

1. Login as dietpi and navigate to home directory, `cd ~`.
2. Create immichkiosk folder, `mkdir immichkiosk`.
3. Download the example config file, `wget -O immichkiosk/config.yaml https://raw.githubusercontent.com/damongolding/immich-kiosk/refs/heads/main/config.example.yaml`.
4. Download the Linux arm64 package, `wget -O immich-kiosk_Linux_arm64.tar.gz https://github.com/damongolding/immich-kiosk/releases/download/v0.15.1/immich-kiosk_Linux_arm64.tar.gz`.
5. Unpack the archive, `tar -zxvf immich-kiosk_Linux_arm64.tar.gz`.
6. Populate `config.yaml` with the following:

## AutoStart Setup

Section covers the auto start configuration of Immich Kiosk.

### Immich Kiosk System Service

1. Navigate to system services, `cd /etc/systemd/system`
2. Create immich-kiosk service, `sudo touch immich-kiosk.service`
3. Populate with the following:
   1.  

       [Unit]
       Description=Immich Kiosk
       After=network.target
       StartLimitIntervalSec=0

       [Service]
       Type=simple
       Restart=always
       RestartSec=1
       User=dietpi
       WorkingDirectory=/home/dietpi/immichkiosk
       ExecStart=/home/dietpi/immichkiosk/immich-kiosk

       [Install]
       WantedBy=multi-user.target

4. Enable and auto-start the service using the following:
   1. `sudo systemctl daemon-reload`
   2. `sudo systemctl enable immich-kiosk`
   3. `sudo systemctl start immich-kiosk`

### DietPi Kiosk Mode

1. Navigate to here, `cd /var/lib/dietpi/dietpi-software/installed/`
2. Modify the `chromium-autostart.sh` file with the example below:
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
        CHROMIUM_OPTS="--kiosk --no-memcheck --window-size=${RES_X:-1280},${RES_Y:-800} --window-position=0,0"

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

        exec "$STARTX" /tmp/xinitrc.tmp "$FP_CHROMIUM" $CHROMIUM_OPTS "${URL:-https://localhost:3000}"
