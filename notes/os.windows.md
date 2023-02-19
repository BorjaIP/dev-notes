---
id: uy66ufz0pc9831r2tbm2wmu
title: Windows
desc: ''
updated: 1676813026917
created: 1655320512824
---

- [Shorcuts](#shorcuts)
- [Variables](#variables)
- [Startup Programs](#startup-programs)
- [Programs](#programs)
  - [Dev](#dev)
- [Folders](#folders)
- [Powershell](#powershell)
- [Winget](#winget)
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
- [Handbraker](https://handbrake.fr/) --> Video transcoder
- [ShareX](https://getsharex.com/) --> Screen capture

## Dev

- [OpenLens](https://github.com/MuhammedKalkan/OpenLens) --> Kubernetes IDE
- [mRemoteNG](https://github.com/mRemoteNG/mRemoteNG) --> Remote connections
- Putty

    Steps for Putty

    For colors

    https://github.com/AlexAkulov/putty-color-themes

    Teerb.reg

    1. Install MRemoteNG
    2. Go to install directory (default C:\Program Files (x86)\mRemoteNG )
    3. Rename PuTTYNG.exe to PuTTYNG.exe.bak
    4. Copy the Putty portable executable and sessions folder to the installation location of MRemoteNG
    5. Rename Putty.exe with PuTTYNG.exe


# Folders

User config is in `C:\Users\Borja`, for example `.ssh`

```bash
# hosts
C:\Windows\System32\drivers\etc
# temporal
C:\Users\Borja\AppData\Local\Temp
# ssh
C:\Users\Borja\.ssh
```

# Powershell

Personalize Windows Terminal.

1. Install windows [terminal](https://github.com/microsoft/terminal).
2. Install Powershell from Windows Store.
3. Install [Nerd Fonts](https://www.nerdfonts.com/font-downloads) for active Icons in particular [Inconsolata](https://github.com/ryanoasis/nerd-fonts/releases) from the releases and select `Inconsolata Regular Nerd Font Complete Windows Compatible.ttf`.
   - Be careful with the [issue 509](https://github.com/ryanoasis/nerd-fonts/issues/509).
4. Change color scheme to [Base 16](https://github.com/ShiromMakkad/base16-windows-terminal) Ocean.
5. Install [Startship](https://github.com/starship/starship) for custom prompt.
6. Edit Powershell profile with VScode. 
    ```bash
    code $PROFILE
    . $env:USERPROFILE\.config\powershell\profile.ps1
    ```
7. Create `profile.ps1` file in .config for custom configuration.
8. Install [Terminal Icons](https://github.com/devblackops/Terminal-Icons).
9.  Install [PSReadLine](https://github.com/PowerShell/PSReadLine).
10. Install [z Directory Jumper](https://github.com/jethrokuan/z).
11. Install [fzf](https://github.com/junegunn/fzf) y [PSfzf](https://github.com/kelleyma49/PSFzf).


Install icons

```bash
Install-Module -Name Terminal-Icons -Repository PSGallery
Install-Module -Name PSReadLine -Force
Install-Module -Name PSFzf -Force
Install-Module -Name z -Force
```

# Winget

List of [packages](https://winget.run/) for install in Windows.

```bash
# install git
winget install -d --id Git.Git
# install gcc
winget install -e --id libjpeg-turbo.libjpeg-turbo.GCC
# install Neovim
winget install -e --id Neovim.Neovim
# install sudo
winget install -e --id gerardog.gsudo
# install jq
winget install -e --id stedolan.jq
```

# Key

For show windows key open `regedit` and see the key:

```bash
Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SoftwareProtectionPlatform
```

# Drivers

Uninstall all GPU drivers

[DDU](https://www.guru3d.com/files-details/display-driver-uninstaller-download.html)

