#!/bin/bash

# Enable RPM Fusion repositories (free and non-free)
sudo dnf install -y \
  https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
  https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

# Swap ffmpeg-free with ffmpeg
sudo dnf swap -y ffmpeg-free ffmpeg --allowerasing

# Install NVIDIA drivers
sudo dnf install -y akmod-nvidia

# Rebuild the kernel modules
sudo akmods

# Reboot to apply changes
sudo reboot
