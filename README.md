<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>NixOS Configuration by Nabil K Sabu</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      line-height: 1.6;
      color: #333;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      background-color: #f9f9f9;
    }
    .header {
      text-align: center;
      margin-bottom: 30px;
    }
    .logo {
      width: 300px;
      height: auto;
      margin-bottom: 20px;
    }
    .divider {
      text-align: center;
      margin: 30px 0;
      font-size: 24px;
      color: #646cff;
    }
    .footer {
      text-align: center;
      margin-top: 50px;
      font-size: 14px;
      color: #666;
    }
    h1, h2 {
      color: #4a4a4a;
    }
    .highlight {
      color: #646cff;
      font-weight: bold;
    }
    pre {
      background-color: #f0f0f0;
      padding: 15px;
      border-radius: 5px;
      overflow-x: auto;
    }
    .snowflake {
      color: #646cff;
      font-size: 20px;
      margin: 0 10px;
    }
  </style>
</head>
<body>
  <div class="header">
    <object data="https://brand.nixos.org/logos/nixos-logo-default-gradient-black-regular-horizontal-recommended.svg" type="image/svg+xml" class="logo">
      NixOS Logo
    </object>
    <h1>NixOS Configuration</h1>
    <p>A <span class="highlight">reproducible</span>, <span class="highlight">declarative</span>, and <span class="highlight">customizable</span> NixOS setup for gaming, development, and daily use.</p>
  </div>

  <div class="divider">
    <span class="snowflake">❄️</span>
    <span class="snowflake">❄️</span>
    <span class="snowflake">❄️</span>
  </div>

  <h2>📜 Overview</h2>
  <p>This repository contains my personal <a href="https://nixos.org/">NixOS</a> configuration. It is designed for a seamless experience with:</p>
  <ul>
    <li><strong>Gaming</strong>: NVIDIA drivers, Steam, Proton, and GameMode.</li>
    <li><strong>Development</strong>: Git, GitHub CLI, Python, and VS Codium.</li>
    <li><strong>Daily Use</strong>: GNOME desktop, Firefox, and system utilities.</li>
  </ul>

  <h2>🔧 Features</h2>
  <ul>
    <li><strong>NVIDIA GPU Support</strong>: Optimized for hybrid graphics (AMD/NVIDIA).</li>
    <li><strong>Steam Gaming</strong>: ProtonUp-Qt, GameMode, and MangoHud for enhanced gaming.</li>
    <li><strong>GNOME Desktop</strong>: Customized and streamlined for productivity.</li>
    <li><strong>System Utilities</strong>: Fastfetch, Git, and GitHub CLI pre-installed.</li>
  </ul>

  <h2>📋 Configuration</h2>
  <p>Here’s a snippet of my <code>configuration.nix</code>:</p>
  <pre>
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
  </pre>

  <h2>🚀 Usage</h2>
  <ol>
    <li>Clone this repository:</li>
    <pre>git clone https://github.com/nabilksabu/nix-cofig.git</pre>
    <li>Apply the configuration:</li>
    <pre>sudo nixos-rebuild switch</pre>
  </ol>

  <div class="footer">
    <p>Powered by <a href="https://nixos.org/">NixOS</a> | Maintained by <a href="https://github.com/nabilksabu">Nabil K Sabu</a></p>
  </div>
</body>
</html>
