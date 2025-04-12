# Installation and Setup

## Overview

Setting up a **Red Hat Enterprise Linux (RHEL)** system is the first step towards managing a stable and secure Linux environment. This guide walks you through downloading, installing, and performing the initial setup for RHEL.

## Downloading RHEL

Red Hat offers various versions of RHEL, including a free **Developer Subscription** for personal use and learning. Follow these steps to obtain an ISO image:
1. Visit [Red Hat Customer Portal](https://access.redhat.com/)
2. Create an account and sign in
3. Navigate to **Downloads** > **RHEL**
4. Select the latest stable version and download the ISO file

## Creating Installation Media

Once you've downloaded the ISO, create a bootable USB drive:

**On Linux/macOS:**

```bash
sudo dd if=rhel-x.x-x86_64-dvd.iso of=/dev/sdX bs=4M status=progress
```

Replace `/dev/sdX` with your USB device.

**On Windows:**
- Use **Rufus** or **Balena Etcher** to write the ISO to a USB drive.

## Installing RHEL

### Step 1: Boot from USB/DVD

1. Insert the bootable USB into the target system
2. Restart the system and enter BIOS/UEFI (typically **F2, F12, Del, Esc** during boot)
3. Select the USB device as the primary boot option
4. Save and exit BIOS, then boot into the RHEL installer

### Step 2: Installation Wizard

1. **Select Language** → Choose your preferred language
2. **Installation Summary** → Configure:
    - **Keyboard Layout**
    - **Time & Date** (set your timezone)
    - **Installation Source** (should detect the USB/DVD automatically)
    - **Software Selection** → Choose **Server with GUI** or **Minimal Installation**
    - **Installation Destination** → Select your disk and choose automatic partitioning
    - **Network & Hostname** → Enable network and set hostname
3. Click **Begin Installation**

### Step 3: Set User Credentials

During installation, set up:
- **Root Password** (essential for administrative tasks)
- **Create a User** (recommended for daily use)

### Step 4: Complete Installation

- Once installation is done, **Reboot the system**
- Remove the installation media (USB/DVD)
- Log in and verify the installation

## Post-Installation Setup

### Update the System

After logging in, update all packages:
```bash
sudo dnf update -y
```

### Enable EPEL Repository (Optional)

To access extra packages:
```bash
sudo dnf install epel-release -y
```

### Set SELinux to Enforcing Mode

```bash
sudo setenforce 1
sudo nano /etc/selinux/config
# Ensure SELINUX=enforcing
```

### Enable Firewall

```bash
sudo systemctl enable --now firewalld
```

### Verify Network Connection

```bash
ip a
ping -c 4 google.com
```
