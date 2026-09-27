# Linux Command for First-Time Setup

## 📝 Why?
Every time I install Linux, I need to do this. Sometimes I miss steps and have to repeat them. So I made this repository to ensure everything works fine on a fresh install.

> **Tested on:** Ubuntu 26.04 LTS (Resolute Raccoon) — GNOME 50 / Wayland
> **Last updated:** September 2026

---

## 🔄 System Updates

### Update package lists
```bash
sudo apt update
```

### Upgrade installed packages
```bash
sudo apt upgrade -y
```

### Full upgrade (handles dependencies + kernel)
```bash
sudo apt full-upgrade -y
```

### Clean up
```bash
sudo apt autoremove -y
sudo apt autoclean
```

---

## 📦 Install Favorite Apps
```bash
sudo apt install obs-studio vlc gimp gparted synaptic -y
```

### Install Ubuntu Restricted Extras
```bash
sudo apt install ubuntu-restricted-extras -y
```

### Install Preload
```bash
sudo apt install preload -y
```

### Improve Laptop Battery
```bash
sudo apt install tlp tlp-rdw -y
sudo systemctl enable --now tlp
```

### Install Build Essentials & Common Tools
```bash
sudo apt install build-essential git wget curl htop neofetch -y
```

### Enable Firewall (UFW)
```bash
sudo apt install ufw -y
sudo ufw enable
sudo ufw status
```

---

## 🛠️ Install Custom Software (.deb)
```bash
sudo dpkg -i /path/to/package.deb

# Fix missing dependencies if any
sudo apt install -f -y
```

---

## 🎨 Install GNOME Tweaks & Extensions
```bash
sudo apt install gnome-tweaks -y
sudo apt install gnome-shell-extensions -y
sudo apt install gnome-shell-extension-manager -y
```

### Taskbar app click to minimize
```bash
gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'
```

### Show battery percentage
```bash
gsettings set org.gnome.desktop.interface show-battery-percentage true
```

### Enable tap-to-click (laptops)
```bash
gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true
```

---

## 🟢 Node.js via NVM

### Install NVM (latest: v0.40.7)
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.7/install.sh | bash
```

### Reload shell config
```bash
source ~/.bashrc
```

### Install Node.js
```bash
# Latest version
nvm install node

# LTS version
nvm install --lts
nvm use --lts

# Verify
node -v && npm -v
```

> 💡 Check [nvm releases](https://github.com/nvm-sh/nvm/releases) for the newest version.

---

## 🎭 Install Theme
https://www.gnome-look.org/p/1619506

Create two folders in your home directory, press `Ctrl + H` to show hidden files, then create `.themes` & `.icons`:

```bash
mkdir -p ~/.themes ~/.icons ~/.local/share/fonts
```

Extract downloaded themes into `~/.themes` and icons into `~/.icons`, then apply via **GNOME Tweaks → Appearance**.

---

## 📦 Flatpak & Flathub
```bash
sudo apt install flatpak -y
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

> Reboot required after installing Flatpak.

---

## 🐳 Docker (Quick Install)
```bash
curl -fsSL https://get.docker.com | sh

# Add user to docker group
sudo usermod -aG docker $USER
```

> Log out and back in for group changes to take effect.

---

## ⚡ Bonus: One-Shot Setup Script
Save as `setup.sh` and run with `bash setup.sh`:

```bash
#!/bin/bash
set -e

echo "🔄 Updating system..."
sudo apt update && sudo apt full-upgrade -y

echo "🧹 Cleaning up..."
sudo apt autoremove -y && sudo apt autoclean

echo "📦 Installing apps..."
sudo apt install -y \
  obs-studio vlc gimp gparted synaptic \
  ubuntu-restricted-extras preload \
  tlp tlp-rdw ufw \
  build-essential git wget curl htop neofetch \
  gnome-tweaks gnome-shell-extensions gnome-shell-extension-manager

echo "🔥 Enabling firewall..."
sudo ufw --force enable

echo "🔋 Enabling TLP..."
sudo systemctl enable --now tlp

echo "🎨 GNOME tweaks..."
gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'
gsettings set org.gnome.desktop.interface show-battery-percentage true
gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true

echo "📁 Creating theme folders..."
mkdir -p ~/.themes ~/.icons ~/.local/share/fonts

echo "📦 Installing Flatpak..."
sudo apt install flatpak -y
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

echo "Done! Reboot recommended."
```

---

## 🔧 Additional Recommendations

| Task | Command |
|------|---------|
| Install Snap (if not present) | `sudo apt install snapd -y` |
| Enable SSH server | `sudo apt install openssh-server -y` |
| Set timezone | `sudo timedatectl set-timezone Region/City` |
| Check disk usage | `df -h` or install `ncdu` |
| Install Zsh + Oh My Zsh | `sudo apt install zsh -y && sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` |

---
