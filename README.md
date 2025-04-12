# RHEL-Based Linux Systems Administration Guide for Beginners

Welcome to the **RHEL-Based Linux Systems Administration Guide**! This repository provides a structured approach for beginners to learn **Red Hat Enterprise Linux (RHEL)** system administration. Whether you're setting up a server, managing users, configuring security, or troubleshooting issues, this guide will help you build a strong foundation in Linux system administration.

---

## Table of Contents

1. [Introduction](introduction.md)
2. [Cheat Sheet](cheatsheet.md)
3. [Installation and Setup](installation.md)
4. [User and Group Management](user-management.md)
5. [File System and Storage](filesystem-management.md)
6. [Networking Configuration](networking.md)
7. [Package Management with DNF](package-management.md)
8. [System Monitoring and Logs](monitoring-logs.md)
9. [Security and SELinux](security-selinux.md)
10. [Process and Service Management](process-services.md)
11. [Firewall and Network Security](firewall-security.md)
12. [Backup and Recovery](backup-recovery.md)
13. [Performance Tuning](performance.md)
14. [Troubleshooting and Debugging](troubleshooting.md)
15. [RAID Configuration](raids.md)
16. [iptables Configuration](iptables.md)

---

## Introduction

**What is RHEL?**

Red Hat Enterprise Linux (RHEL) is a widely used enterprise-grade Linux distribution known for its stability, security, and scalability. It is commonly used in data centers, cloud environments, and enterprise IT infrastructures. This guide focuses on RHEL-based distributions, including **CentOS Stream, Rocky Linux, and AlmaLinux**.

---

## Cheat Sheet  

This **Cheat Sheet** provides a quick reference for essential Linux commands that system administrators frequently use in RHEL-based distributions, including **CentOS Stream, Rocky Linux, and AlmaLinux**. Whether you're managing files, users, processes, or networking, this section helps you quickly recall important commands without diving into full documentation.  

For a detailed breakdown, see the [Cheat Sheet Guide](cheatsheet.md).  

---

## Installation and Setup

Learn how to install RHEL and its alternatives step-by-step:

- Downloading RHEL, CentOS Stream, Rocky Linux, or AlmaLinux
- Creating a bootable USB and installing the OS
- Setting up basic system configurations
- Configuring repositories and package updates

See [Installation and Setup](installation.md) for full instructions.

---

## User and Group Management

Understanding user and group management is crucial for securing and administering a Linux system:

- Creating and managing users and groups
- Assigning permissions and ownership
- Using `sudo` and managing administrative privileges
- Understanding `/etc/passwd`, `/etc/shadow`, and `/etc/group`

More details in [User and Group Management](user-management.md).

---

## File System and Storage

Learn how to manage storage and file systems efficiently:

- Understanding the Linux file system structure
- Mounting and unmounting file systems
- Managing disk partitions using `fdisk` and `parted`
- Using LVM (Logical Volume Manager) for storage flexibility
- Working with `ext4`, `XFS`, and other file systems

Details in [File System and Storage](filesystem-storage.md).

---

## Networking Configuration

Configure and manage networking in RHEL-based systems:

- Setting up static and dynamic IP addresses
- Managing network interfaces using `nmcli` and `nmtui`
- Understanding DNS, DHCP, and routing
- Configuring SSH for secure remote access

See [Networking Configuration](networking.md) for guidance.

---

## Package Management with DNF

Manage software installations and updates using `dnf`:

- Installing, updating, and removing packages
- Managing repositories and third-party sources
- Working with RPM packages manually

Guide available in [Package Management with DNF](package-management.md).

---

## System Monitoring and Logs

Monitor system performance and logs for troubleshooting:

- Using `top`, `htop`, and `vmstat` for performance analysis
- Checking logs with `journalctl`, `dmesg`, and `/var/log`
- Setting up and managing system logging with `rsyslog`

See [System Monitoring and Logs](monitoring-logs.md).

---

## Security and SELinux

Enhance system security using best practices and SELinux:

- Configuring and enforcing SELinux policies
- Managing user authentication and password policies
- Securing SSH and preventing brute-force attacks
- Hardening system configurations

Details in [Security and SELinux](security-selinux.md).

---

## Process and Service Management

Manage system processes and services effectively:

- Controlling system services with `systemctl`
- Managing background processes and jobs
- Understanding process signals and priorities

Learn more in [Process and Service Management](process-services.md).

---

## Firewall and Network Security

Set up and manage firewalls using `firewalld`:

- Configuring rules and zones
- Opening and closing ports securely
- Setting up NAT and port forwarding

See [Firewall and Network Security](firewall-security.md) for details.

---

## Backup and Recovery

Ensure data integrity with a proper backup strategy:

- Using `rsync`, `tar`, and `scp` for file backups
- Setting up automatic backups with `cron`
- Recovering from system failures

More details in [Backup and Recovery](backup-recovery.md).

---

## Performance Tuning

Optimize system performance with best practices:

- Tuning CPU, memory, and disk performance
- Using `sysctl` for kernel parameter tuning
- Managing swap and optimizing resource allocation

See [Performance Tuning](performance.md).

---

## Troubleshooting and Debugging

Diagnose and fix common issues in RHEL-based systems:

- Resolving boot and kernel issues
- Debugging network connectivity problems
- Troubleshooting slow performance and high resource usage

Guide available in [Troubleshooting and Debugging](troubleshooting.md).

---

## RAID Configuration

Learn how to configure and manage RAID setups on RHEL-based systems:

- Understanding RAID levels (RAID 0, 1, 5, 10, etc.)
- Creating and managing RAID arrays with `mdadm`
- Resizing, repairing, and managing RAID arrays
- Monitoring RAID arrays' health and performance
- Troubleshooting common RAID issues

Guide available in [RAID Configuration](raids.md).

---

## iptables Configuration

Configure and manage firewall rules using `iptables` on RHEL-based systems:

- Understanding iptables chains, tables, and rules
- Creating and managing custom firewall rules
- Configuring network address translation (NAT) and port forwarding
- Saving and restoring iptables configurations
- Troubleshooting common firewall issues

Guide available in [iptables Configuration](iptables.md).

---
