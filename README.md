\# ❄️ NixOS Configuration by Nabil K Sabu

<div align="center">
  <img src="https://brand.nixos.org/logos/nixos-logo-default-gradient-white-regular-horizontal-recommended.svg" alt="NixOS Logo" width="400"/>
</div>

---

A **reproducible**, **declarative**, and **customizable** NixOS setup for gaming, development, and daily use.

---

## 📜 Overview

This repository contains my **personal NixOS configuration**, designed for a seamless experience with:

- **🎮 Gaming**: NVIDIA drivers, Steam, Proton, and GameMode.
- **💻 Development**: Git, GitHub CLI, Python, and VS Codium.
- **🌐 Daily Use**: GNOME desktop, Firefox, and system utilities.

---

## 🔧 Features

| Feature                     | Description                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|
| **NVIDIA GPU Support**      | Optimized for hybrid graphics (AMD/NVIDIA).                                  |
| **Steam Gaming**            | ProtonUp-Qt, GameMode, and MangoHud for enhanced gaming.                     |
| **GNOME Desktop**           | Customized and streamlined for productivity.                                |
| **System Utilities**        | Fastfetch, Git, and GitHub CLI pre-installed.                               |

---

## 📋 Configuration

Here’s a snippet of my `configuration.nix`:

```nix
{ config, pkgs, lib, ... }:

{
  imports = [ ./hardware-configuration.nix ];

  boot.loader.systemd-boot.enable = true;
  boot.kernelPackages = pkgs.linuxPackages_latest;

  networking.hostName = "nixos";
  networking.networkmanager.enable = true;

  hardware.nvidia = {
    open = true;
    prime.offload.enable = true;
    package = config.boot.kernelPackages.nvidiaPackages.latest;
  };

  programs.steam.enable = true;
  programs.gamemode.enable = true;

  environment.systemPackages = with pkgs; [
    wget fastfetch git gh vscodium python315 heroic mangohud protonup-ng
  ];

  services.xserver.desktopManager.gnome.enable = true;
  services.displayManager.ly.enable = true;
}
