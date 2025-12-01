This page covers the setup of Whisper on a Windows 11.

## Install Python

- Download Python **3.10 or 3.11**: https://www.python.org/downloads/
- Run the installer
- Check the box **"Add Python to PATH"**
- Click **Install**

**Verify Python installation (CMD):**

``` sh
    python --version
```

## Install FFmpeg

### Using Chocolatey

Install Chocolatey (PowerShell as Administrator):

``` powershell
Set-ExecutionPolicy Bypass -Scope Process -Force
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Install FFmpeg:

``` powershell
choco install ffmpeg -y
```

Verify FFmpeg:

``` sh
ffmpeg -version
```

### NVIDIA GPU Setup (Optional)

If you will be using GPU acceleration with NVIDIA:

``` sh
pip uninstall torch torchvision torchaudio
pip install --force-reinstall --index-url https://download.pytorch.org/whl/cu121 torch torchvision torchaudio
```

## Install Whisper

``` sh
pip install -U openai-whisper
```

**Verify installation:**

``` sh
whisper --help
```

## Usage

**Run Whisper on a media file:**

Change directory (or open a terminal) in the folder containing your media file, then run:

``` sh
whisper <MEDIA_FILE> --model medium --device cuda --output_dir subtitles --output_format srt --task transcribe --language English
```

``` sh
whisper <MEDIA_FILE> --model medium --device cuda --output_dir . --output_format srt --task translate --language Czech
```

This will generate an `.srt` subtitle file inside a folder named **subtitles** relative to the directory in the movie.

### Scripted

Location Pending.
