---
title: "Network Configuration"
description: "Instructions for configuring network settings during the Debian installation, including wired and wireless connections, IP address assignment, and DNS settings."
icon: "code"
draft: false
toc: true
weight: 1
---

## Introduction

Proper network configuration is essential during the Debian installation process to ensure connectivity for downloading updates, accessing repositories, and completing the installation. This guide provides step-by-step instructions for configuring **wired** and **wireless connections**, assigning **IP addresses**, and setting up **DNS settings**. Whether you're using DHCP or need to configure your network manually, this tutorial will guide you through the setup process.

## Prerequisites

Before starting the network configuration, ensure the following:

- You've booted into the **Debian installer environment** using a USB drive, DVD, or other installation media.
- You have access to either a **wired** (Ethernet) or **wireless** (Wi-Fi) network.
- **Network credentials**: If you're setting up a manual network or connecting via Wi-Fi, ensure you have the correct IP address, gateway, subnet, and DNS details (for manual configuration) or the Wi-Fi passphrase for secure networks.

## Step 1: Boot into the Debian Installer

1. **Insert the Debian installation media** (USB, DVD, etc.) into your computer.
2. Restart the system and boot from the installation media. You may need to access the BIOS/UEFI (by pressing `F2`, `F12`, or `Esc` during startup) to change the boot order.
3. Once the Debian installer environment is launched, follow the on-screen prompts to begin the installation.

## Step 2: Access Network Configuration

During the installation process, you’ll reach a stage where you can configure the network settings. 

1. **Select "Configure the network"** from the Debian installer menu. 
2. The installer will display a list of network interfaces detected on your machine:
   - **Wired connections** typically use `eth0` or similar.
   - **Wireless connections** use `wlan0` or a similar interface.
3. Choose the interface corresponding to your desired connection type (e.g., **eth0** for Ethernet or **wlan0** for Wi-Fi).

## Step 3: Configure a Wired Connection

If you're using a wired Ethernet connection, follow these steps:

1. **Select the wired network interface** (e.g., `eth0`) from the list of available interfaces.
2. **DHCP configuration**: If your network uses **DHCP** (Dynamic Host Configuration Protocol), which is common in most home and office networks, choose the option to configure the interface using DHCP.
   - The installer will automatically attempt to obtain an IP address, subnet, gateway, and DNS information from the network.
3. **Manual configuration**: If DHCP is not available or you prefer to assign a static IP address, select the option to manually configure the network:
   - Enter the following details provided by your network administrator:
     - **IP Address** (e.g., 192.168.1.100)
     - **Subnet Mask** (e.g., 255.255.255.0)
     - **Gateway** (e.g., 192.168.1.1)
     - **DNS Server** (e.g., 8.8.8.8 or your preferred DNS server)
   
4. Once configured, proceed to test the connection (as described later in Step 5).

## Step 4: Configure a Wireless Connection

If you need to connect to a wireless network, follow these steps:

1. **Select the wireless network interface** (e.g., `wlan0`) from the list of available interfaces.
2. **Scan for available networks**: The installer will prompt you to scan for nearby Wi-Fi networks. Choose the **SSID** (network name) of your desired Wi-Fi network from the list of available options.
3. **Enter the Wi-Fi security key**: If the network is password-protected (WPA2, WPA3, etc.), you’ll be prompted to enter the **Wi-Fi passphrase**.
4. **DHCP or Manual Configuration**:
   - For most Wi-Fi networks, DHCP will automatically assign an IP address and other network settings.
   - If you need to manually configure the wireless connection, follow the same steps outlined in the manual wired configuration (entering IP address, subnet mask, gateway, and DNS server).

Once the wireless configuration is complete, the system will attempt to connect to the selected network.

## Step 5: Verify Network Configuration

After configuring the network, it's important to verify that your connection is working correctly:

1. **Check network settings**: Review the network configuration details displayed by the installer. Confirm that the IP address, gateway, and DNS settings are correct.
   
2. **Test network connectivity**: The installer may automatically perform a network connectivity test by pinging a known server (e.g., `google.com`). If this is not done automatically, you can manually test the connection:
   
   - If connected to a wired network, ping an external IP address like Google's DNS server:
     ```bash
     ping 8.8.8.8
     ```
   - Alternatively, ping a domain name to check if DNS is working:
     ```bash
     ping google.com
     ```

3. **Troubleshooting**:
   - If the test fails, recheck your network settings, including the IP address, gateway, and DNS details.
   - Ensure that the correct network interface is selected (wired vs. wireless) and that the Wi-Fi passphrase is correct if using Wi-Fi.
   
4. **Proceed with installation**: Once network connectivity is verified, continue with the remaining steps of the Debian installation process.

## Additional Tips

- **Switching between DHCP and Manual**: If you're unsure whether DHCP is enabled on your network, try configuring with DHCP first. If it fails, switch to manual configuration with static IP settings.
- **Advanced Networking**: For complex networking scenarios (e.g., proxy servers, VLANs, custom DNS settings), consult the network administrator or refer to Debian's official documentation for advanced setup options.

## Conclusion

Properly configuring network settings during the Debian installation ensures that your system can connect to the internet and access online resources for software updates and package installations. By following these steps for either wired or wireless networks, you can set up reliable network connectivity on your Debian system with ease.