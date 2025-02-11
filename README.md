#!/bin/bash

# Update and upgrade
sudo dnf update -y && sudo dnf upgrade -y

# Enable RPM Fusion repositories (free and non-free)
sudo dnf install -y \
  https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
  https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

# Install app-stream metadata
sudo dnf4 group update core -y || sudo dnf group upgrade core -y

# Add Flathub remote if not already added
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

# Swap ffmpeg-free with ffmpeg and get proper multimediaplayback
sudo dnf swap -y ffmpeg-free ffmpeg --allowerasing
sudo dnf4 group upgrade multimedia
sudo dnf upgrade @multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin # Installs gstreamer components. Required if you use Gnome Videos and other dependent applications.
sudo dnf group install -y sound-and-video # Installs useful Sound and Video complement packages.

# Video decoding and acceleration
sudo dnf install -y ffmpeg-libs libva libva-utils

# If on AMD chipset and used the above, use this
sudo dnf swap -y mesa-va-drivers mesa-va-drivers-freeworld
sudo dnf swap -y mesa-vdpau-drivers mesa-vdpau-drivers-freeworld

# OpenH264 for Firefox, enable the OpenH264 Plugin in Firefox's settings after
sudo dnf install -y openh264 gstreamer1-plugin-openh264 mozilla-openh264
sudo dnf config-manager setopt fedora-cisco-openh264.enabled=1

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

# Install Heroic Launcher
sudo flatpak install -y flathub com.heroicgameslauncher.hgl

# Install Discord
sudo flatpak install -y flathub com.discordapp.Discord

# Install VLC
sudo flatpak install -y flathub org.videolan.VLC

# Install Drivers
# Install NVIDIA drivers

# sudo dnf install -y akmod-nvidia

# Rebuild the kernel modules
# sudo akmods

# Reboot to apply changes
sudo reboot
