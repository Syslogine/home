---
title: "Configuring Network Interfaces with systemd-networkd"
date: 2024-10-14
description: "Learn how to configure network interfaces in Arch Linux using systemd-networkd."
keywords: ["Arch Linux", "network configuration", "systemd-networkd", "Linux administration"]
---

# Configuring Network Interfaces with systemd-networkd

This tutorial provides a detailed guide on configuring network interfaces in Arch Linux using `systemd-networkd`, allowing for effective network management.

## Table of Contents

1. [Introduction to systemd-networkd](#introduction-to-systemd-networkd)
2. [Prerequisites](#prerequisites)
3. [Basic systemd-networkd Configuration](#basic-systemd-networkd-configuration)
4. [Configuring Wired Connections](#configuring-wired-connections)
5. [Configuring Wireless Connections](#configuring-wireless-connections)
6. [Static IP Configuration](#static-ip-configuration)
7. [DHCP Configuration](#dhcp-configuration)
8. [DNS Configuration with systemd-resolved](#dns-configuration-with-systemd-resolved)
9. [Network Bonding and Bridging](#network-bonding-and-bridging)
10. [VLANs Configuration](#vlans-configuration)
11. [Troubleshooting](#troubleshooting)
12. [Best Practices and Security Considerations](#best-practices-and-security-considerations)
13. [Conclusion](#conclusion)

## 1. Introduction to systemd-networkd

`systemd-networkd` is a system daemon that manages network configurations. It detects and configures network devices as they appear, as well as creates virtual network devices. This tool is part of the systemd suite and provides a powerful and flexible way to configure network interfaces in Arch Linux.

## 2. Prerequisites

Before starting, ensure you have:

- A working Arch Linux installation
- Root or sudo access
- Basic knowledge of Linux command line
- Text editor of your choice (e.g., nano, vim)

## 3. Basic systemd-networkd Configuration

To start using `systemd-networkd`:

1. Enable and start the service:
   ```bash
   sudo systemctl enable systemd-networkd
   sudo systemctl start systemd-networkd
   ```

2. Create a network configuration directory if it doesn't exist:
   ```bash
   sudo mkdir -p /etc/systemd/network
   ```

## 4. Configuring Wired Connections

To configure a wired connection:

1. Create a new file in `/etc/systemd/network/` with a `.network` extension:
   ```bash
   sudo nano /etc/systemd/network/20-wired.network
   ```

2. Add the following content:
   ```ini
   [Match]
   Name=eth0

   [Network]
   DHCP=yes
   ```

   Replace `eth0` with your actual interface name.

3. Save the file and restart `systemd-networkd`:
   ```bash
   sudo systemctl restart systemd-networkd
   ```

## 5. Configuring Wireless Connections

For wireless connections, you'll need to use `wpa_supplicant` alongside `systemd-networkd`:

1. Install `wpa_supplicant`:
   ```bash
   sudo pacman -S wpa_supplicant
   ```

2. Create a `wpa_supplicant` configuration file:
   ```bash
   sudo nano /etc/wpa_supplicant/wpa_supplicant-wlan0.conf
   ```

3. Add your wireless network details:
   ```
   network={
       ssid="YourNetworkSSID"
       psk="YourNetworkPassword"
   }
   ```

4. Create a network file for the wireless interface:
   ```bash
   sudo nano /etc/systemd/network/25-wireless.network
   ```

5. Add the following content:
   ```ini
   [Match]
   Name=wlan0

   [Network]
   DHCP=yes
   ```

6. Enable and start `wpa_supplicant`:
   ```bash
   sudo systemctl enable wpa_supplicant@wlan0
   sudo systemctl start wpa_supplicant@wlan0
   ```

## 6. Static IP Configuration

To set a static IP:

1. Edit your network file:
   ```bash
   sudo nano /etc/systemd/network/20-wired.network
   ```

2. Modify the content:
   ```ini
   [Match]
   Name=eth0

   [Network]
   Address=192.168.1.100/24
   Gateway=192.168.1.1
   DNS=8.8.8.8
   ```

## 7. DHCP Configuration

DHCP is enabled by default in the earlier examples. You can customize DHCP settings:

```ini
[Match]
Name=eth0

[Network]
DHCP=yes

[DHCP]
UseDNS=no
UseNTP=yes
SendHostname=yes
```

## 8. DNS Configuration with systemd-resolved

`systemd-resolved` manages DNS resolution:

1. Enable and start `systemd-resolved`:
   ```bash
   sudo systemctl enable systemd-resolved
   sudo systemctl start systemd-resolved
   ```

2. Create a symlink for `/etc/resolv.conf`:
   ```bash
   sudo ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf
   ```

3. Configure DNS in your network file:
   ```ini
   [Network]
   ...
   DNS=8.8.8.8 8.8.4.4
   ```

## 9. Network Bonding and Bridging

For advanced setups like bonding or bridging:

1. Create a bond:
   ```ini
   [NetDev]
   Name=bond0
   Kind=bond

   [Bond]
   Mode=active-backup
   ```

2. Create a bridge:
   ```ini
   [NetDev]
   Name=br0
   Kind=bridge
   ```

## 10. VLANs Configuration

To set up VLANs:

```ini
[NetDev]
Name=vlan10
Kind=vlan

[VLAN]
Id=10
```

## 11. Troubleshooting

Common troubleshooting steps:

- Check service status: `systemctl status systemd-networkd`
- View logs: `journalctl -u systemd-networkd`
- Verify configuration: `networkctl`
- Test connectivity: `ping -c 4 archlinux.org`

## 12. Best Practices and Security Considerations

- Keep configurations simple and well-documented
- Use predictable interface names
- Secure wireless networks with strong passwords
- Regularly update your system
- Use firewalls to protect your network interfaces

## 13. Conclusion

`systemd-networkd` provides a powerful and flexible way to manage network configurations in Arch Linux. By understanding its capabilities and syntax, you can effectively set up and manage various network scenarios, from simple DHCP setups to complex configurations involving VLANs, bonds, and bridges.

Remember to always test your configurations thoroughly, especially in production environments. With practice, you'll find `systemd-networkd` to be a robust tool for network management in Arch Linux.