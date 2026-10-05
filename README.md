<div align="center">

# 🐧 Linux Environment & Post-Installation Setup Suite
### Comprehensive Ubuntu / Debian Post-Install Provisioning, Development Tooling & System Optimization Guide

[![Linux](https://img.shields.io/badge/OS-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](https://www.kernel.org/)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-26.04%20LTS-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com/)
[![Bash](https://img.shields.io/badge/Shell-Bash%20%2F%20Zsh-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Docker](https://img.shields.io/badge/Container-Docker%20CE-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-CEFF00?style=for-the-badge&logoColor=black)](LICENSE)

<br/>

**A curated, production-tested workstation setup guide and command-line reference for rapid system provisioning, desktop customization, security hardening, and developer toolchain configuration on modern Ubuntu/Debian distributions.**

<br/>

[System Updates](#-system-updates) •
[Packages & Apps](#-essential-applications--system-tools) •
[Developer Toolchain](#-developer-toolchains) •
[GNOME Customization](#-gnome-tweaks--desktop-customization) •
[Docker Setup](#-docker-engine--compose) •
[License](#-license)

</div>

<br/>

---

## 📌 Overview

This repository provides an automated, repeatable post-installation setup guide for configuring fresh Linux installations (tested on Ubuntu LTS / GNOME Wayland). It streamlines system updates, driver/codec installations, power management optimization, developer runtime provisioning, and desktop styling.

---

## 🔄 System Updates

### Update & Upgrade System Packages
```bash
# Update package indices
sudo apt update

# Upgrade installed packages
sudo apt upgrade -y

# Full upgrade (handles new dependencies & kernel packages)
sudo apt full-upgrade -y

# Remove orphaned dependencies & clear package cache
sudo apt autoremove -y
sudo apt autoclean
```

---

## 📦 Essential Applications & System Tools

```bash
# Core productivity & system utilities
sudo apt install obs-studio vlc gimp gparted synaptic htop neofetch -y

# Restricted media codecs & fonts
sudo apt install ubuntu-restricted-extras -y

# Laptop battery optimization (TLP)
sudo apt install tlp tlp-rdw -y
sudo systemctl enable --now tlp

# Essential build toolchain & networking utilities
sudo apt install build-essential git wget curl -y

# Enable Uncomplicated Firewall (UFW)
sudo apt install ufw -y
sudo ufw enable
sudo ufw status
```

---

## 🛠️ Installing Standalone `.deb` Packages

```bash
# Install local deb package with automatic dependency resolution
sudo apt install ./path/to/package.deb
```

> **Best Practice:** Use `apt install ./package.deb` (with `./`) rather than `dpkg -i` to automatically resolve and fetch missing upstream dependencies.

---

## 🎨 GNOME Tweaks & Desktop Customization

```bash
# Install GNOME management tools
sudo apt install gnome-tweaks gnome-shell-extensions gnome-shell-extension-manager -y
```

### Desktop Ergonomics Tweaks
```bash
# Enable click-to-minimize on the dock
gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'

# Display battery percentage in top bar
gsettings set org.gnome.desktop.interface show-battery-percentage true

# Enable touchpad tap-to-click
gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true
```

### Custom Themes & Icons
```bash
# Create local styling directories
mkdir -p ~/.themes ~/.icons ~/.local/share/fonts
```

![Home folder with .themes and .icons created](Setup-Home-Folder-Themes-Icons.png)

> Extract downloaded themes into `~/.themes` and icons into `~/.icons`, then apply via **GNOME Tweaks → Appearance**.

---

## 📦 Flatpak & Flathub Integration

```bash
# Install Flatpak engine & add Flathub repository
sudo apt install flatpak -y
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

---

## 🟢 Developer Toolchains

### Node.js (via NVM)
```bash
# Install Node Version Manager (NVM)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.7/install.sh | bash

# Reload shell configuration
source ~/.bashrc

# Install Node.js LTS release
nvm install --lts
nvm use --lts

# Verify installation
node -v && npm -v
```

---

## 🐳 Docker Engine & Compose

```bash
# Add Docker's official GPG key
sudo apt-get update
sudo apt-get install ca-certificates curl -y
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# Install Docker packages
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

# Add current user to docker group (non-root execution)
sudo usermod -aG docker $USER
```

---

## 🔧 Additional System Optimization

| Purpose | Command |
| :--- | :--- |
| **Snap Package Support** | `sudo apt install snapd -y` |
| **Secure Shell Server** | `sudo apt install openssh-server -y` |
| **System Timezone** | `sudo timedatectl set-timezone America/Toronto` |
| **Disk Space Analyzer** | `sudo apt install ncdu -y && ncdu /` |
| **Zsh & Oh My Zsh** | `sudo apt install zsh -y && sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` |

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
