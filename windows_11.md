# Windows 11

This page covers the manual setup of Windows 11 for my personal use.

## Quick-Links

- [System File Checker](https://winbindex.m417z.com/)

## Manual Setup

If setup via Microsoft Account, create an additional **local** user with the name "Adam". Run through sign-in process again. Sign into Microsoft account this time.

Set Network & internet setting to "Private network". Download and setup your Security tools first!

### Settings / Removing Items

- Via Control Panel, uninstall the OneDrive.
- Via Settings --> Apps --> Installed Apps, Uninstall the following
  - Clipchamp - Video Editor
  - Cortana
  - Maps
  - Microsoft News
  - Microsoft To Do
  - Movies & TV
  - Office
  - People
  - Solitaire Collection
  - Sticky Notes
  - Xbox Live

### Settings / System

- Verify your displays are in the correct position.
- Night light, set to On, schedule night light: Sunset to Sunrise
- Use HDR: Off
- Within Scale & layout
  - Advanced display
    - Choose highest refresh rate
- Within Sound
  - Verify correct microphone is selected and verify level of 90 for the AT2020 USB microphone.
- Within System -> Power
  - Screen and sleep, set "When plugged in, turn off my screen after **30 minutes**" and "When plugged in, put my device to sleep after **3 hours**.
- Select the "Best performance" power mode in Control Panel
- Within For developers
  - [X] Enable Developer Mode
  - [X] Enable Device discovery
  - [X] Enable End Task
  - File Explorer
    - [X] Show file extensions
    - [X] Show hidden and system files
    - [X] Show full path in title bar
    - [X] Show empty drives
- Enable Remote Desktop
- Terminal: Windows Terminal

### Settings / Bluetooth & Devices

- Turn off Bluetooth
- Printers & scanners:
  - [ ] Let Windows manage my default printer
    - Set it to Brother printer/scanner
- AutoPlay set to Off
- Choose AutoPlay defaults
  - Removable drive: Open folder to view files (File Explorer)
  - Memory card: Download and setup your Security tools first!

### Settings / Network & internet

- Ethernet set to Private Network

### Settings / Personalization

- Personalize your lock screen: Windows Spotlight
- Lock screen status: Weather

### Settings / Apps

- Apps for websites, remove Maps pointer to `maps.windows.com` and `*.maps.windows.com`.

### Settings / Accounts

- Within Windows backup, turn off Remember my apps.

### Settings / Time & language

- Set to English (United States), Region format: Update short-date to include first month digit, short/long-time to 24-hour

### Settings / Accessibility

- Visual effects:
  - [X] Always show scrollbars
  - [ ] Transparency effects
  - [ ] Animation effects

### Settings / Privacy & security

- Within General
  - [ ] Let apps show me personalized ads by using my advertising ID
  - [ ] Let websites show me locally relevant content by accessing my langauge list
  - [ ] Let Windows improve Start and search results by tracking app launches
  - [ ] SHow my suggested content in the Settings app

### Settings / Windows Update

- [ ] Get the latest updates as soon as they're available

### Registry Edits

Run in cmd with admin-mode:

- Force File Explorer to open to This PC instead of Quick Access
  -     reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" /v LaunchTo /t REG_DWORD /d 1 /f
- Disable Promotional Apps
  -     reg add "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\ContentDeliveryManager" /v PreInstalledAppsEnabled /t REG_DWORD /d 0 /f
- Disable Cloud Search
  -     reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Windows Search" /v AllowCloudSearch /t REG_DWORD /d 0 /f
- Disable Cortana
  -     reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Windows Search" /v AllowCortana /t REG_DWORD /d 0 /f
  -     reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Search" /v CortanaEnabled /t REG_DWORD /d 0 /f
  -     reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Search" /v CortanaConsent /t REG_DWORD /d 0 /f
- Disable Cortana LockScreen
  -     reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Windows Search" /v AllowCortanaAboveLock /t REG_DWORD /d 0 /f
- Old Context Menu
  -     reg.exe add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f
  - To restore
    -     reg.exe delete "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}" /f

## Ninite

Select the following:

- Web Browsers
  - Chrome
  - Firefox
- Messaging
  - Discord
- Media
  - VLC
  - Spotify
- Developer Tools
  - Notepad++
  - PuTTY
  - Visual Studio Code
- Other
  - Steam
- Compression
  - 7-Zip

## Network Drive Mounting

Script located [here](https://github.com/adamzvolanek/DevRack/blob/main/scripts/windows_11/network_drive_mounts.bat)
