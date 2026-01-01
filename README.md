<p align=center>
    <img src="https://github.com/pinkSakoora/sakoora.hyprlock/blob/33a5ec211ace6b2f63b92a0fc6545cf3ad6828b4/lockbanner.png" alt="Banner" width="1000">
</p>
<p align=center style="bold">A repository containing my hyprlock theme(s), along with an installation script to set it up according to screen size.  </p>

<p align=center>
    <img src="https://github.com/pinkSakoora/sakoora.hyprlock/blob/33a5ec211ace6b2f63b92a0fc6545cf3ad6828b4/showcase1.png" alt="Showcase 1" width="1000">
</p>

## Features
- Automatic element sizing (on running `install`)
- Panel blur (utilizing `imagemagick`)
- Easy theme-switching: The entire setup only uses 4 colors that are sourced from 2 files (`colors-hyprlock.sh` and `colors-hyprlock.conf`)
- Profile picture holder
- Network and bluetooth indicators
- Power status bar
- Uptime, current time and date
- Media player status

> [!NOTE]
> Panel blurring requires drawing ahead of time, which can be achieved by tweaking your `hypridle` or modifying the hyprlock launch command to run `~/.config/hypr/sakoora.hyprlock/hyprlock-run/panels` before running hyprlock. More info in [Notes](#notes).

## Showcase
<p align=center>
    <img src="https://github.com/pinkSakoora/sakoora.hyprlock/blob/33a5ec211ace6b2f63b92a0fc6545cf3ad6828b4/showcase2.png" alt="Showcase 2" width="1000">
</p>
<p align=center>
    <img src="https://github.com/pinkSakoora/sakoora.hyprlock/blob/33a5ec211ace6b2f63b92a0fc6545cf3ad6828b4/showcase3.png" alt="Showcase 3" width="1000">
</p>
<p align=center>
    <img src="https://github.com/pinkSakoora/sakoora.hyprlock/blob/33a5ec211ace6b2f63b92a0fc6545cf3ad6828b4/showcase4.png" alt="Showcase 4" width="1000">
</p>

## Installation
> [!WARNING]
> This has only been tested on Arch Linux.  

Cloning the repository and running `install` installs all required dependencies and sets up the hyprlock.
```
git clone https://github.com/pinkSakoora/sakoora.hyprlock.git
sakoora.hyprlock/install
```
The installer asks for confirmation before installing required packages.

If you wish to install the dependencies manually, they are:
```
hyprland hyprlock wlr-randr imagemagick grim bluez-utils networkmanager playerctl
```
- `wlr-randr` is required to fetch screen resolution.
- `imagemagick` is requied to draw panels.
- `grim` is used to take a screenshot for the drawing of panels.
- `bluez-utils` provides `bluetoothctl` which is used for the bluetooth indicator.
- `networkmanager` provides `nmcli` which is used for the network indicator.
- `playerctl` is used to fetch info about currently playing media.

## Notes
1. Every file created/modified by the installer is located within `~/.config/hypr/sakoora.hyprlock`, with the except of `hyprlock.conf`, and font files. The old `hyprlock.conf` (if any) has a prefix of `-pre-sakoora` added to it. The added fonts are Josefin Sans and Fira Code Nerd Font Mono (at `~/.local/share/fonts/ttf`.)
2. The panels drawing script creates a folder named `hyprlock-cache` in `~/.cache`, in which it stores all drawn panels. This script should be called before hyprlock is launched to ensure accurate panel blurring.

An example hypridle listener would be:
```
listener {
timeout = 270    # this timeout should be less than the timeout to launch hyprlock 
    on-timeout = ~/.config/hypr/sakoora.hyprlock/hyprlock-run/panels    # set up all required assets for hyprlock
}
```
And an example hyprland keybind to lock the screen would be: 
```
bind = $mainMod, W, exec, ~/.config/hypr/sakoora.hyprlock/hyprlock-run/panels && hyprlock --grace 5
```
3. The default installed theme is a modified version of catppuccin-macchiato. The colors can be changed by modifying them in `~/.config/hypr/sakoora.hyprlock/colors-hyprlock.sh` and `~/.config/hypr/sakoora.hyprlock/colors-hyprlock.conf`.
