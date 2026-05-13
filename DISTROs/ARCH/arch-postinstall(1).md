

# links
* https://github.com/swaywm/sway/blob/master/config.in
* https://github.com/swaywm/sway/wiki
* https://github.com/Infinirc/nvfd
* https://archlinux.org/

# Arch Linux Post-Install Setup Guide
> Sway + Wayland + NVIDIA RTX 3090 + Ollama workstation

---

## 1. First Boot Prep

### Update system
```bash
sudo pacman -Syu
```

### Configure pacman
Edit `/etc/pacman.conf`:
```ini
# Uncomment for 32-bit support (Steam, Wine, etc.)
[multilib]
Include = /etc/pacman.d/mirrorlist

# Quality of life
Color
ParallelDownloads = 5
```

### Fast mirrors with reflector
```bash
sudo pacman -S reflector
sudo reflector --country US --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```

Create `/etc/xdg/reflector/reflector.conf` for auto-refresh on boot:
```
--country US
--age 12
--protocol https
--sort rate
--save /etc/pacman.d/mirrorlist
```
```bash
sudo systemctl enable reflector.service
```

---

## 2. AUR Helper (paru)

```bash
sudo pacman -S --needed base-devel git
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
cd .. && rm -rf paru
```

---

## 3. GPU Drivers (NVIDIA — RTX 3090)

> `nvidia` is the driver. `nvidia-utils` is the userspace companion (OpenGL, Vulkan).
> `lib32-nvidia-utils` adds 32-bit support for Steam/Wine.
> Use `nvidia-dkms` if you're on a non-default kernel (linux-zen, linux-lts, etc.)

```bash
sudo pacman -S nvidia-dkms nvidia-utils lib32-nvidia-utils nvidia-settings
sudo pacman -S nvtop   # terminal GPU monitor
```

### Enable DRM kernel modesetting (required for Wayland)
Edit `/etc/default/grub`:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet nvidia-drm.modeset=1"
```
```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

### Early NVIDIA module loading (prevents black screen)
Edit `/etc/mkinitcpio.conf`:
```
MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)
```
```bash
sudo mkinitcpio -P
```

### NVIDIA persistence daemon
```bash
sudo systemctl enable nvidia-persistenced.service
```

---

## 4. Fan Control — nvfd

> nvfd uses NVML directly — no `nvidia-settings` required.
> Works on Wayland and headless. Has a TUI dashboard and interactive curve editor.
> https://github.com/Infinirc/nvfd

### Install from source
```bash
git clone https://github.com/Infinirc/nvfd.git
cd nvfd
sudo scripts/install.sh   # auto-detects OS, installs deps, builds, sets up systemd
cd .. && rm -rf nvfd
```

### Enable daemon
```bash
sudo systemctl enable --now nvfd.service
```

### Config files
| File | Path |
|---|---|
| Mode settings | `/etc/nvfd/config.json` |
| Fan curve | `/etc/nvfd/curve.json` |

### Fan curve format (`/etc/nvfd/curve.json`)
```json
{
    "30": 30,
    "40": 40,
    "50": 55,
    "60": 65,
    "70": 85,
    "80": 100
}
```

### Common commands
```bash
nvfd                    # Launch TUI dashboard
nvfd status             # Show current GPU/fan status
nvfd curve edit         # Interactive ncurses curve editor
nvfd curve show         # Print current curve
nvfd curve 60 70        # Set curve point: 60°C → 70% fan
nvfd 80                 # Set all fans to fixed 80%
nvfd auto               # Return fans to driver control
nvfd list               # List all GPUs
```

### Reload config without restart
```bash
sudo systemctl reload nvfd   # sends SIGHUP
```

---

## 5. Wayland + Sway

### Install Sway and core tools
```bash
sudo pacman -S sway swaybar swaybg swayidle swaylock
sudo pacman -S waybar          # status bar (polybar equivalent)
sudo pacman -S wofi            # app launcher (rofi equivalent)
sudo pacman -S mako            # notification daemon
sudo pacman -S wl-clipboard    # clipboard
sudo pacman -S grim slurp      # screenshots
sudo pacman -S foot            # Wayland-native terminal
sudo pacman -S alacritty       # alternative terminal
```

### NVIDIA Wayland environment variables
Add to `/etc/environment`:
```bash
LIBVA_DRIVER_NAME=nvidia
XDG_SESSION_TYPE=wayland
GBM_BACKEND=nvidia-gbm
__GLX_VENDOR_LIBRARY_NAME=nvidia
WLR_NO_HARDWARE_CURSORS=1
NIXOS_OZONE_WL=1              # Electron apps (VS Code, Discord, etc.)
MOZ_ENABLE_WAYLAND=1          # Firefox
QT_QPA_PLATFORM=wayland
SDL_VIDEODRIVER=wayland
```

### Sway config location
`~/.config/sway/config`

### Default Sway config (full working baseline)
```
# Default config for sway
# Read `man 5 sway` for reference.

### Variables
set $mod Mod4
set $left h
set $down j
set $up k
set $right l
set $term foot
set $menu wofi --show drun

### Output configuration
output * bg /usr/share/backgrounds/sway/Sway_Wallpaper_Blue_1920x1080.png fill

### Idle configuration
exec swayidle -w \
    timeout 300 'swaylock -f -c 000000' \
    timeout 600 'swaymsg "output * power off"' \
        resume 'swaymsg "output * power on"' \
    before-sleep 'swaylock -f -c 000000'

### Input configuration
input "type:keyboard" {
    xkb_layout us
}

### Key bindings
bindsym $mod+Return exec $term
bindsym $mod+Shift+q kill
bindsym $mod+d exec $menu
bindsym $mod+Shift+c reload
bindsym $mod+Shift+e exec swaynag -t warning -m 'Exit sway?' -B 'Yes' 'swaymsg exit'

# Move focus
bindsym $mod+$left focus left
bindsym $mod+$down focus down
bindsym $mod+$up focus up
bindsym $mod+$right focus right
bindsym $mod+Left focus left
bindsym $mod+Down focus down
bindsym $mod+Up focus up
bindsym $mod+Right focus right

# Move windows
bindsym $mod+Shift+$left move left
bindsym $mod+Shift+$down move down
bindsym $mod+Shift+$up move up
bindsym $mod+Shift+$right move right
bindsym $mod+Shift+Left move left
bindsym $mod+Shift+Down move down
bindsym $mod+Shift+Up move up
bindsym $mod+Shift+Right move right

# Workspaces
bindsym $mod+1 workspace number 1
bindsym $mod+2 workspace number 2
bindsym $mod+3 workspace number 3
bindsym $mod+4 workspace number 4
bindsym $mod+5 workspace number 5
bindsym $mod+6 workspace number 6
bindsym $mod+7 workspace number 7
bindsym $mod+8 workspace number 8
bindsym $mod+9 workspace number 9
bindsym $mod+0 workspace number 10

bindsym $mod+Shift+1 move container to workspace number 1
bindsym $mod+Shift+2 move container to workspace number 2
bindsym $mod+Shift+3 move container to workspace number 3
bindsym $mod+Shift+4 move container to workspace number 4
bindsym $mod+Shift+5 move container to workspace number 5
bindsym $mod+Shift+6 move container to workspace number 6
bindsym $mod+Shift+7 move container to workspace number 7
bindsym $mod+Shift+8 move container to workspace number 8
bindsym $mod+Shift+9 move container to workspace number 9
bindsym $mod+Shift+0 move container to workspace number 10

# Layout
bindsym $mod+b splith
bindsym $mod+v splitv
bindsym $mod+s layout stacking
bindsym $mod+w layout tabbed
bindsym $mod+e layout toggle split
bindsym $mod+f fullscreen
bindsym $mod+Shift+space floating toggle
bindsym $mod+space focus mode_toggle
bindsym $mod+a focus parent

# Scratchpad
bindsym $mod+Shift+minus move scratchpad
bindsym $mod+minus scratchpad show

# Resize mode
mode "resize" {
    bindsym $left resize shrink width 10px
    bindsym $down resize grow height 10px
    bindsym $up resize shrink height 10px
    bindsym $right resize grow width 10px
    bindsym Left resize shrink width 10px
    bindsym Down resize grow height 10px
    bindsym Up resize shrink height 10px
    bindsym Right resize grow width 10px
    bindsym Return mode "default"
    bindsym Escape mode "default"
}
bindsym $mod+r mode "resize"

# Status bar
bar {
    position top
    status_command while date +'%Y-%m-%d %I:%M %p'; do sleep 1; done
    colors {
        statusline #ffffff
        background #323232
        inactive_workspace #32323200 #32323200 #5c5c5c
    }
}

include /etc/sway/config.d/*
```

> **Note for NVIDIA:** Sway officially only endorses Mesa drivers.
> If sway refuses to start, set this before launching:
> ```bash
> export SWAY_ALLOW_UNSUPPORTED_GPU=1
> sway
> ```

### Auto-start Sway from TTY
Add to `~/.zprofile` (or `~/.bash_profile`):
```bash
if [ -z "$WAYLAND_DISPLAY" ] && [ "$XDG_VTNR" -eq 1 ]; then
    export SWAY_ALLOW_UNSUPPORTED_GPU=1
    exec sway
fi
```

---

## 6. Audio (Pipewire)

```bash
sudo pacman -S pipewire pipewire-pulse pipewire-alsa wireplumber
sudo pacman -S pavucontrol
```

Enable for your user (not root):
```bash
systemctl --user enable --now pipewire pipewire-pulse wireplumber
```

---

## 7. Networking

```bash
sudo systemctl enable --now NetworkManager
sudo pacman -S networkmanager network-manager-applet
```

---

## 8. Bluetooth

```bash
sudo pacman -S bluez bluez-utils blueman
sudo systemctl enable --now bluetooth.service
```

---

## 9. Fonts

```bash
sudo pacman -S \
  noto-fonts \
  noto-fonts-cjk \
  noto-fonts-emoji \
  ttf-jetbrains-mono \
  ttf-fira-code \
  ttf-font-awesome

fc-cache -fv
```

---

## 10. Shell (zsh + starship)

```bash
sudo pacman -S zsh zsh-completions starship
chsh -s /bin/zsh
```

Add to `~/.zshrc`:
```bash
eval "$(starship init zsh)"
```

Starship config: `~/.config/starship.toml`

---

## 11. Ollama

```bash
paru -S ollama-cuda    # CUDA build for NVIDIA
sudo systemctl enable --now ollama.service

ollama pull qwen2.5-coder:32b
```

| Item | Path |
|---|---|
| Models | `~/.ollama/models/` |
| Service | `/etc/systemd/system/ollama.service` |

---

## 12. Flatpak

```bash
sudo pacman -S flatpak
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

---

## 13. Snapshots (Timeshift)

```bash
paru -S timeshift
sudo timeshift --create --comments "fresh install"
```

---

## 14. Locale & Timezone

```bash
# Check current state
locale
timedatectl
```

If wrong — edit `/etc/locale.gen`, uncomment `en_US.UTF-8 UTF-8`, then:
```bash
sudo locale-gen
```

`/etc/locale.conf`:
```
LANG=en_US.UTF-8
```

```bash
sudo timedatectl set-timezone America/Chicago
sudo hwclock --systohc
```

---

## 15. Sudo / Wheel Group

```bash
groups $USER   # verify wheel is listed

# If not:
sudo usermod -aG wheel $USER

# /etc/sudoers — always edit with visudo:
%wheel ALL=(ALL:ALL) ALL
```

---

## 16. Useful Utilities

```bash
sudo pacman -S \
  htop btop \
  neofetch \
  wget curl \
  unzip zip p7zip \
  rsync \
  man-db man-pages \
  git \
  tmux \
  ripgrep fd \
  python python-pip \
  ffmpeg \
  yt-dlp
```

---

## Key Config File Locations

| Config | Path |
|---|---|
| pacman | `/etc/pacman.conf` |
| mirrors | `/etc/pacman.d/mirrorlist` |
| mkinitcpio | `/etc/mkinitcpio.conf` |
| GRUB | `/etc/default/grub` |
| locale | `/etc/locale.gen`, `/etc/locale.conf` |
| environment vars | `/etc/environment` |
| hosts | `/etc/hosts` |
| sudoers | `/etc/sudoers` (edit via `visudo`) |
| Sway | `~/.config/sway/config` |
| Waybar | `~/.config/waybar/config` |
| Wofi | `~/.config/wofi/config` |
| Mako | `~/.config/mako/config` |
| Alacritty | `~/.config/alacritty/alacritty.toml` |
| zsh | `~/.zshrc` |
| starship | `~/.config/starship.toml` |
| zprofile (auto-start sway) | `~/.zprofile` |
| nvfd mode config | `/etc/nvfd/config.json` |
| nvfd fan curve | `/etc/nvfd/curve.json` |
| Ollama models | `~/.ollama/models/` |

---

## Services to Enable (summary)

```bash
# System (run with sudo)
sudo systemctl enable NetworkManager
sudo systemctl enable bluetooth
sudo systemctl enable reflector
sudo systemctl enable nvidia-persistenced
sudo systemctl enable nvfd
sudo systemctl enable ollama

# User (run as your user, no sudo)
systemctl --user enable pipewire pipewire-pulse wireplumber
```
