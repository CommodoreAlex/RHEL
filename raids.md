# RAID Configuration Guide for RHEL  

This guide provides instructions for configuring RAID (Redundant Array of Independent Disks). 

RAID configurations improve data redundancy, increase performance, and offer flexibility in disk management. This guide covers multiple RAID levels and provides basic configuration steps using both software RAID (mdadm) and hardware RAID.

## 📌 Table of Contents  

- [Introduction to RAID](#introduction-to-raid)  
- [RAID Levels](#raid-levels)  
- [Requirements](#requirements)  
- [Setting up Software RAID with mdadm](#setting-up-software-raid-with-mdadm)  
- [Create RAID Arrays](#create-raid-arrays)  
- [Monitor and Manage RAID](#monitor-and-manage-raid)  
- [Hardware RAID Configuration](#hardware-raid-configuration)  
- [Troubleshooting RAID](#troubleshooting-raid)  

## Introduction to RAID  

RAID (Redundant Array of Independent Disks) is a technology that combines multiple hard drives into one logical unit to improve data redundancy, performance, or both. There are several RAID levels, each designed to serve specific needs in terms of fault tolerance and speed.

## RAID Levels  

Each RAID level has its own advantages and trade-offs. Here's a quick summary of commonly used RAID levels:  

- **RAID 0 (Striping)**: Provides increased performance but no redundancy. Data is split across multiple disks for faster access.  

- **RAID 1 (Mirroring)**: Provides redundancy by duplicating the data across two or more disks, which ensures data protection in case of a failure.  

- **RAID 5 (Striping with Parity)**: Provides redundancy with the ability to recover from one disk failure. Data is striped across multiple disks with parity distributed across them.  

- **RAID 10 (1+0)**: Combines the benefits of RAID 1 and RAID 0. It provides redundancy and performance by mirroring data and then striping across multiple disks.  

## Requirements  

- **Multiple disks**: Ensure you have at least two disks to configure RAID. The number of disks required depends on the RAID level you plan to configure (e.g., RAID 1 needs at least 2 disks, RAID 5 needs at least 3 disks).  
- **Root privileges**: You need administrative rights to create RAID arrays and manage disks.  

## Setting up Software RAID with mdadm  

`mdadm` is a powerful utility for managing software RAID arrays in Linux systems.

### 1. Install `mdadm`  

```bash
sudo dnf install mdadm
```

### 2. Verify available disks

Check the disks you want to use for RAID:
```bash
lsblk
```

### 3. Create a RAID Array

Use `mdadm` to create a RAID array. Here's an example for creating RAID 1 (mirroring) with two disks `/dev/sda` and `/dev/sdb`:
```bash
sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sda /dev/sdb
```

- **/dev/md0**: Name of the RAID device
- **--level=1**: RAID level (1 for mirroring)
- **--raid-devices=2**: Number of devices in the array

### 4. Verify RAID Array

Check the status of your RAID array:
```bash
sudo mdadm --detail /dev/md0
```

### 5. Create Filesystem on RAID Array

Once the RAID array is created, you need to create a filesystem:
```bash
sudo mkfs.ext4 /dev/md0
```

### 6. Mount RAID Array

Mount the RAID array to a directory:
```bash
sudo mount /dev/md0 /mnt
```

### 7. Configure RAID Array to Auto-Mount at Boot

Edit `/etc/fstab` to ensure the RAID array mounts automatically:
```bash
echo '/dev/md0 /mnt ext4 defaults 0 0' | sudo tee -a /etc/fstab
```

## Create RAID Arrays

To create other RAID levels like RAID 0, RAID 5, or RAID 10, follow similar steps, adjusting the RAID level and number of devices accordingly.

Example for **RAID 5** with three disks `/dev/sda`, `/dev/sdb`, and `/dev/sdc`:
```bash
sudo mdadm --create /dev/md0 --level=5 --raid-devices=3 /dev/sda /dev/sdb /dev/sdc
```

For **RAID 10** with four disks `/dev/sda`, `/dev/sdb`, `/dev/sdc`, and `/dev/sdd`:
```bash
sudo mdadm --create /dev/md0 --level=10 --raid-devices=4 /dev/sda /dev/sdb /dev/sdc /dev/sdd
```

## Monitor and Manage RAID

To check the status of your RAID array:
```bash
sudo cat /proc/mdstat
```

To view detailed information about the RAID array:
```bash
sudo mdadm --detail /dev/md0
```

To stop a RAID array (for example, if you're removing a disk):
```bash
sudo mdadm --stop /dev/md0
```

To remove a failed disk from a RAID array:
```bash
sudo mdadm --remove /dev/md0 /dev/sdb
```

To add a new disk to a RAID array:
```bash
sudo mdadm --add /dev/md0 /dev/sdc
```

## Hardware RAID Configuration

While software RAID is managed using tools like `mdadm`, hardware RAID configurations are done through the server's RAID controller BIOS or a dedicated RAID management tool. Refer to your hardware's manual or use tools like `megacli` (for LSI controllers) or `storcli` (for Broadcom controllers) to configure RAID arrays on hardware.

Example for creating a RAID 1 using a hardware RAID controller:
```bash
storcli /c0 add vd type=raid1 drives=0:0,0:1
```

(Replace `/c0` with your controller and `0:0,0:1` with your drives' IDs).

## Troubleshooting RAID

### 1. Identifying a Failed Disk

Use the following command to identify failed disks:
```bash
sudo mdadm --detail /dev/md0
```

If a disk has failed, it will be marked as "failed" or "removed."

### 2. Replacing a Failed Disk

If a disk fails, replace it with a new disk and add it to the array using the `mdadm --add` command.

### 3. Rebuilding the RAID Array

After replacing a disk, you may need to rebuild the array to restore redundancy:
```bash
sudo mdadm --assemble --scan
```

### 4. Checking RAID Health

Check the health of your RAID array regularly to ensure it is functioning properly. A failing array will show errors in the `mdadm` or `dmesg` logs.
```bash
dmesg | grep md
```

---

This guide provides the basics for configuring and managing RAID arrays on a RHEL-based system using `mdadm` for software RAID and hardware RAID tools. For advanced RAID management, refer to your hardware's documentation and specialized tools.
