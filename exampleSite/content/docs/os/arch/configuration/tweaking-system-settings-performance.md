---
title: "Tweaking System Settings for Performance in Arch Linux"
date: 2024-10-14
description: "Master advanced techniques to optimize Arch Linux performance through strategic system tweaks. Learn to fine-tune kernel parameters, manage resources efficiently, and boost system responsiveness."
keywords: ["Arch Linux", "performance tuning", "system settings", "Linux optimization", "kernel parameters", "resource management", "system responsiveness", "I/O scheduling", "CPU governor"]
---

# Tweaking System Settings for Performance in Arch Linux

## Table of Contents
1. [Introduction](#introduction)
2. [CPU Performance Optimization](#cpu-performance-optimization)
3. [Memory Management Tweaks](#memory-management-tweaks)
4. [Storage and I/O Optimization](#storage-and-io-optimization)
5. [Network Performance Tuning](#network-performance-tuning)
6. [Graphics and Display Enhancements](#graphics-and-display-enhancements)
7. [Kernel Parameter Optimization](#kernel-parameter-optimization)
8. [Systemd Service Management](#systemd-service-management)
9. [Boot Time Optimization](#boot-time-optimization)
10. [Power Management for Performance](#power-management-for-performance)
11. [Monitoring and Benchmarking](#monitoring-and-benchmarking)
12. [Conclusion](#conclusion)

## 1. Introduction
Optimizing Arch Linux for peak performance involves careful adjustment of various system settings. This guide will walk you through advanced techniques to enhance your system's speed and responsiveness while maintaining stability.

## 2. CPU Performance Optimization
Optimize CPU performance with governor settings:

```bash
# Check current governor
cat /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor

# Set performance governor
echo "performance" | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor

# For persistent change, edit /etc/default/cpupower
sudo nano /etc/default/cpupower
# Set: governor='performance'
```

Consider using tools like `cpupower` for more granular control.

## 3. Memory Management Tweaks
Adjust swappiness and cache pressure:

```bash
# Reduce swappiness (default is 60)
echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.d/99-sysctl.conf

# Adjust cache pressure
echo "vm.vfs_cache_pressure=50" | sudo tee -a /etc/sysctl.d/99-sysctl.conf

# Apply changes
sudo sysctl --system
```

Consider enabling zram for better memory management:

```bash
sudo pacman -S zram-generator
```

## 4. Storage and I/O Optimization
Optimize I/O scheduler and mount options:

```bash
# Check current I/O scheduler
cat /sys/block/sda/queue/scheduler

# Set BFQ scheduler
echo "bfq" | sudo tee /sys/block/sda/queue/scheduler

# Edit fstab for optimized mount options
sudo nano /etc/fstab
# Add 'noatime,commit=60' to mount options
```

Consider using the `deadline` scheduler for SSDs.

## 5. Network Performance Tuning
Enhance network stack performance:

```bash
# Increase network buffer sizes
echo "net.core.rmem_max=16777216" | sudo tee -a /etc/sysctl.d/99-network.conf
echo "net.core.wmem_max=16777216" | sudo tee -a /etc/sysctl.d/99-network.conf

# Enable TCP Fast Open
echo "net.ipv4.tcp_fastopen=3" | sudo tee -a /etc/sysctl.d/99-network.conf

# Apply changes
sudo sysctl --system
```

## 6. Graphics and Display Enhancements
Optimize graphics performance:

- Install appropriate GPU drivers
- Configure Xorg for performance:

```bash
sudo nano /etc/X11/xorg.conf.d/20-intel.conf
# Add:
Section "Device"
    Identifier  "Intel Graphics"
    Driver      "intel"
    Option      "AccelMethod"  "sna"
    Option      "TearFree"     "true"
EndSection
```

- Consider using a lightweight compositor like Picom

## 7. Kernel Parameter Optimization
Fine-tune kernel parameters:

```bash
sudo nano /etc/sysctl.d/99-sysctl.conf

# Add or modify:
kernel.nmi_watchdog = 0
vm.dirty_ratio = 10
vm.dirty_background_ratio = 5
```

## 8. Systemd Service Management
Optimize systemd services:

```bash
# Analyze boot time
systemd-analyze blame

# Disable unnecessary services
sudo systemctl disable bluetooth.service
sudo systemctl disable avahi-daemon.service

# Mask services that are not needed
sudo systemctl mask lvm2-monitor.service
```

## 9. Boot Time Optimization
Reduce boot time:

- Enable parallel startup of services
- Reduce timeout values in bootloader

```bash
sudo nano /etc/default/grub
# Modify: GRUB_TIMEOUT=1
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## 10. Power Management for Performance
Optimize power management without sacrificing performance:

```bash
sudo pacman -S tlp
sudo systemctl enable tlp.service
sudo systemctl start tlp.service
```

Configure TLP for balanced performance and power saving.

## 11. Monitoring and Benchmarking
Use tools to monitor and benchmark your system:

```bash
sudo pacman -S htop iotop
sudo pacman -S sysbench

# Example CPU benchmark
sysbench cpu run
```

Regularly monitor system performance to ensure optimizations are effective.

## 12. Conclusion
Tweaking system settings can significantly enhance Arch Linux performance. Remember to test changes thoroughly and revert any that cause instability. Continuous monitoring and adjustment are key to maintaining an optimized system.