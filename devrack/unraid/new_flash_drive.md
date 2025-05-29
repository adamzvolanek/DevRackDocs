Creating a new flash drive for Unraid.

1. Download Unraid USB Creator Tool
   1. [Link](https://docs.unraid.net/unraid-os/manual/changing-the-flash-device/#replace-the-usb-flash-device)
2. Download Flash Drive Backup
   1. Navigate to `http://{SERVER_IP}/Main/Flash?name=flash`
   2. Press the "Flash Backup"
3. Run the Unraid USB Creator Tool
4. Under Operating System select "Choose OS" and scroll to the bottom to 'Use custom'.
   1. Select your downloaded flash backup
5. Under Storage select your microSD card.
6. Select "Next", Settings window appears.
   1. Server Name: `Alexandria`
   2. Network Mode: Static IP
   3. IP Address: {SERVER_IP}
   4. Gateway: Router IP
   5. DNS Server: Recommend Router IP
   6. Select "Continue"
7. Select "Yes" for all existing data warning.

Note Windows Defender may generate a warning about fat32 format. It is safe to allow on device re-run the setup process above starting at Step 3.
