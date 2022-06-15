---
id: uy66ufz0pc9831r2tbm2wmu
title: Windows
desc: ''
updated: 1655320524971
created: 1655320512824
---

- [Shorcuts](#shorcuts)
- [Variables](#variables)
- [Startup Programs](#startup-programs)
- [Programs](#programs)
- [User](#user)
- [Powershell](#powershell)
- [Key](#key)
- [Drivers](#drivers)

# Shorcuts

```bash
# Clipboard history
Win+v
```

# Variables

```bash
# Env variables
%PROGRAMFILES%
%APPDATA%
%LocalAppData%
%USERPROFILE%
```

# Startup Programs

Open execute window `Win+R`:

```bash
# delete all unnecesary
shell:startup
# delete all unnecesary
shell:common startup
```
Open `regedit` and delete all unnecesary:

```bash
# For User
Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
# For Local Machine
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
```

Open `Task scheduler` and DISABLE all unnecesary.

- Disable all Edge.
- Disable all Nvidia reports and updates in background.

# Programs

All config programs are in `%APPDATA%\`

    cd $env:APPDATA
    - Alacritty --> %APPDATA%\alacritty

- [Scoop](https://scoop.sh/) --> Package manager
  
    ```bash
    Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
    scoop install starship
    ```

- [Winget](https://github.com/microsoft/winget-cli) --> Windows Package manager

    ```bash
    winget install 7zip alacritty git
    ```

- [OpenRGB](https://openrgb.org/) --> Light control

    ```bash
    E:\Programs\OpenRGB\OpenRGB.exe --gui --startminimized --server
    ```
    See for startup: https://gitlab.com/CalcProgrammer1/OpenRGB/-/wikis/Frequently-Asked-Questions#can-i-have-openrgb-start-automatically-when-i-log-in

- [NVcleanstall](https://www.techpowerup.com/nvcleanstall/) --> Install NVIDIA Drivers
- [Debloater](https://github.com/Sycnex/Windows10Debloater) --> Remove all unnecesary windows applications
- [Autohotkey](https://www.autohotkey.com/) --> Hotkey software
- [HotkeyD](https://github.com/HikariKnight/hotkeyD) --> Hotkey software
- [Trakt](https://github.com/iamkroot/trakt-scrobbler) --> Trakt app
- [VIA](https://caniusevia.com/) --> Keyboard mapping
- [Vial](https://get.vial.today/) --> Keyboard mapping
- [QMK Fimeware](https://docs.qmk.fm/#/) --> Keyboard fimewares
- [PowerToys](https://github.com/microsoft/PowerToys) --> System utilities
- [O&O ShutUp](https://www.oo-software.com/en/shutup10) --> AntySpy
- [SumatraPDF](https://www.sumatrapdfreader.org/free-pdf-reader)
- [CoreTemp](https://www.alcpu.com/CoreTemp/)
- [OpenHardware](https://openhardwaremonitor.org/)
- [PowerUP](https://www.techpowerup.com/gpuz/)
- [NZXT](https://nzxt.com/software/cam)
- [AMD Wraith Prism](https://landing.coolermaster.com/pages/amd-ryzen-wraith-prism-rgb-software/)
- [Trident Z RGB](https://www.gskill.com/download/1502180912/1551690847/Trident-Z-Family-(RGB,-Royal,-Neo))
- [RGB Fusion](https://www.gigabyte.com/MicroSite/512/download.html)
- [Armor](https://rog.asus.com/armoury-crate/)
- [Handbraker](https://handbrake.fr/) --> Video transcoder

# User

User config is in `C:\Users\Borja`, for example `.ssh`

- Install Inconsolata Nerd Fonts --> https://www.nerdfonts.com/
- Keyboard layout --> https://github.com/thomasfaingnaert/win-us-intl-altgr/releases
- Edit profile in Powershell --> code $PROFILE

# Powershell

Install icons

```bash
Install-Module -Name Terminal-Icons -Repository PSGallery
```
# Key

For show windows key open `regedit` and see the key:

```bash
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SoftwareProtectionPlatform
```

# Drivers

Uninstall all GPU drivers

[ddu](https://www.guru3d.com/files-details/display-driver-uninstaller-download.html)

