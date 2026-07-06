<div align=center>

<img src="https://github.com/pinkSakoora/sakoora.hyprlock/blob/33a5ec211ace6b2f63b92a0fc6545cf3ad6828b4/lockbanner.png" alt="banner" width="1000"> <br>

<br>

Clean, unique hyprlock styles, bundled with a convenient installer.

</div>

<br>

<h2 align=center> overview </h2>

Notable features include:

- Adaptive element sizing and positioning according to screen resolution (when running `install`)
- Easy style switching (requiring just one word changes in `current-style.conf`)
- Self contained file structure (more in [notes](#notes))
- Small color palette: 4 colors sourced from 2 files (`colors-hyprlock.sh` and `colors-hyprlock.conf`), allowing for easier theme switching
- Various widget scripts, including network and bluetooth indicators, power status, uptime, date, time, and media player status.
- Other effects such as panel blurring, image snippets, and gradients, powered by `imagemagick`

<br>

<h2 align=center> styles preview </h2>

<h3 align=center> style-1 </h3>

<p align=center>
    <img src="https://github.com/pinkSakoora/sakoora.hyprlock/blob/33a5ec211ace6b2f63b92a0fc6545cf3ad6828b4/showcase1.png" alt="style-1 showcase" width="1000">
</p>

> [!NOTE]
> Panel blurring requires drawing ahead of time. This requires you to run the drawing script (located at `~/.config/hypr/sakoora.hyprlock/style-1/scripts/panels`) before launching hyprlock. More in [notes](#notes).

<h3 align=center> style-2 </h3>

<p align=center>
    <img src="https://github.com/pinkSakoora/sakoora.hyprlock/blob/4776f89b9890c03ecb36f2436d9fe65e01a300b0/showcase2.png" alt="style-2 showcase" width="1000">
</p>

> [!NOTE]
> Image snippets and gradients require drawing ahead of time. This requires you to run the drawing script (located at `~/.config/hypr/sakoora.hyprlock/style-2/scripts/panels`) before launching hyprlock. More in [notes](#notes).

<br>

<h2 align=center> Installation </h2>

> [!WARNING]
> This has only been tested on Arch Linux.  

Cloning the repository and running `install` installs all required dependencies and sets it up.
```
git clone https://github.com/pinkSakoora/sakoora.hyprlock.git
sakoora.hyprlock/install
```
The installer asks for confirmation before installing required packages.

If you wish to install the dependencies manually, they are:
```
hyprland hyprlock imagemagick grim bluez-utils networkmanager playerctl
```
- `imagemagick` is requied to draw panels.
- `grim` is used to take a screenshot for the drawing of panels.
- `bluez-utils` provides `bluetoothctl` which is used for the bluetooth indicator.
- `networkmanager` provides `nmcli` which is used for the network indicator.
- `playerctl` is used to fetch info about currently playing media.

## Notes
1. Every file created/modified by the installer is located within `~/.config/hypr/sakoora.hyprlock`, with the exception of `hyprlock.conf`, and font files. The old `hyprlock.conf` (if any) has a suffix of `-pre-sakoora` added to it. The added fonts are Josefin Sans and Fira Code Nerd Font Mono (at `~/.local/share/fonts/ttf`.)
2. The `panels` script for each style creates a folder named `hyprlock-cache` in `~/.cache`, in which it stores all drawn panels. This script should be called before hyprlock, especially in the case of panel drawing to ensure accuracy.

An example hypridle listener would be:
```
listener {
timeout = 270    # this timeout should be less than the timeout to launch hyprlock 
    on-timeout = ~/.config/hypr/sakoora.hyprlock/style-x/scripts/panels    # set up all required assets for hyprlock, replace x with required style
}
```
And an example hyprland keybind to lock the screen would be: 
```
bind = $mainMod, W, exec, ~/.config/hypr/sakoora.hyprlock/style-x/scripts/panels && hyprlock --grace 5
```
3. The default installed theme is a modified version of catppuccin-macchiato. The colors can be changed by modifying them in `~/.config/hypr/sakoora.hyprlock/colors-hyprlock.sh` and `~/.config/hypr/sakoora.hyprlock/colors-hyprlock.conf`.
