# File System and Storage Management in RHEL

## Overview

Managing the file system and storage is a crucial aspect of system administration in RHEL-based environments. This guide covers essential commands and concepts related to partitions, mounting, LVM, and disk management.

---

## Understanding the Linux File System Hierarchy

RHEL follows the **Filesystem Hierarchy Standard (FHS)**, which organizes directories and files in a structured manner:

- `/`: Root directory (contains everything)
- `/boot`: Bootloader files
- `/etc`: Configuration files
- `/home`: User home directories
- `/var`: Variable data (logs, caches, etc.)
- `/usr`: User binaries and libraries

For a complete hierarchy, refer to `man hier`.

---

## Disk Partitioning

Disk partitioning allows you to divide storage into separate sections.

### Listing Available Disks

```bash
lsblk
fdisk -l
```

### Creating a New Partition (Using `fdisk`)

Select the disk:
```bash
fdisk /dev/sdX
```

1. Create a new partition (`n` command).
2. Write changes (`w` command).

For GPT partitions, use `gdisk` instead of `fdisk`.

---

## Formatting a Partition

Once a partition is created, format it with a file system:
```bash
mkfs.ext4 /dev/sdX1   # Format as ext4
mkfs.xfs /dev/sdX1    # Format as XFS (recommended for RHEL)
```

Check the file system type:
```bash
blkid /dev/sdX1
```

---

## Mounting and Unmounting File Systems

Mounting attaches the partition to the Linux directory tree.

### Temporary Mounting:

```bash
mount /dev/sdX1 /mnt
```

### Persistent Mounting (via `/etc/fstab`):

Add the following entry to `/etc/fstab`:
```bash
/dev/sdX1  /mnt  xfs  defaults  0 0
```

Then, apply changes:
```bash
mount -a
```

### Unmounting a Partition:

```bash
umount /mnt
```

---

## Logical Volume Management (LVM)

LVM allows flexible disk management by grouping multiple physical volumes.

### Creating an LVM Setup:

**Initialize physical volumes:**
```bash
pvcreate /dev/sdX1 /dev/sdX2
```

**Create a volume group (VG):**
```bash
vgcreate my_vg /dev/sdX1 /dev/sdX2
```

**Create a logical volume (LV):**
```bash
lvcreate -L 10G -n my_lv my_vg
```

**Format and mount the LV:**
```bash
mkfs.xfs /dev/my_vg/my_lv
mount /dev/my_vg/my_lv /mnt
```

### Resizing an LVM Volume:

**Extend an LV:**
```bash
lvextend -L +5G /dev/my_vg/my_lv
resize2fs /dev/my_vg/my_lv  # For ext4
xfs_growfs /mnt             # For XFS
```

**Reduce an LV (requires unmounting):**
```bash
umount /mnt
e2fsck -f /dev/my_vg/my_lv
resize2fs /dev/my_vg/my_lv 5G
lvreduce -L 5G /dev/my_vg/my_lv
mount /dev/my_vg/my_lv /mnt
```


---

## Monitoring Disk Usage

### Checking Disk Space:

```bash
df -h
```

### Checking Inode Usage:

An **inode** is a data structure on a filesystem that stores metadata about a file or directory, such as its size, permissions, owner, and location on disk, excluding its name.

```bash
df -i
```

### Finding Large Files:

```bash
du -sh /path/to/directory
```

---

## Automounting with `autofs`

To automatically mount file systems when accessed, install `autofs`:
```bash
yum install -y autofs
```

Configure `/etc/auto.master` and `/etc/auto.misc` to define mount points.

---

## File System Checking and Repair

To check and repair a file system:
```bash
fsck /dev/sdX1  # For ext4
xfs_repair /dev/sdX1  # For XFS
```

Ensure the file system is unmounted before running repair tools.

---
