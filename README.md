#!/bin/bash

# Update and upgrade
sudo dnf update -y && sudo dnf upgrade -y

# Enable RPM Fusion repositories (free and non-free)
sudo dnf install -y \
  https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
  https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

# Add Flathub remote if not already added
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

# Swap ffmpeg-free with ffmpeg
sudo dnf swap -y ffmpeg-free ffmpeg --allowerasing

# Install Neofetch
sudo dnf install -y neofetch

# Install Wine and Winetricks
sudo dnf install -y wine
sudo dnf install -y winetricks

# Installing important applications
# Install Steam
sudo dnf install -y steam

# Install ProtonUp
sudo flatpak install -y flathub net.davidotek.pupgui2

# Install Flameshot
sudo dnf install -y flameshot

# Install Heroic Launcher
sudo flatpak install -y flathub com.heroicgameslauncher.hgl

# Install Signal
sudo flatpak install -y flathub org.signal.Signal

# Install Discord
sudo flatpak install -y flathub com.discordapp.Discord

# Install Blender
sudo flatpak install -y flathub org.blender.Blender

# Install VLC
sudo flatpak install -y flathub org.videolan.VLC

# Install Cider
sudo flatpak install -y flathub sh.cider.Cider

# Install ProtonVPN
sudo flatpak install -y flathub com.protonvpn.www

# Install QBittorrent
sudo flatpak install -y flathub org.qbittorrent.qBittorrent

# Install Bitwarden
sudo flatpak install -y flathub com.bitwarden.desktop

# Install Freetube
sudo flatpak install -y flathub io.freetubeapp.FreeTube

# Install OnlyOffice
sudo flatpak install -y flathub org.onlyoffice.desktopeditors

# Install MegaSync
sudo flatpak install -y flathub nz.mega.MEGAsync

# Install Drivers
# Install NVIDIA drivers
sudo dnf install -y akmod-nvidia

# Rebuild the kernel modules
sudo akmods

# Reboot to apply changes
sudo reboot
