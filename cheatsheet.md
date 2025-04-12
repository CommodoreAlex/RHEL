# 🖥Basic Linux Command Guide for System Administrators  

This guide provides essential Linux commands for beginner system administrators working with Red Hat-based distributions.

## Table of Contents  
- [System Information](#system-information)
- [File and Directory Management](#file-and-directory-management)  
- [File Creation and Editing](#file-creation-and-editing)
- [User and Group Management](#user-and-group-management)  
- [Permissions and Ownership](#permissions-and-ownership)  
- [Process Management](#process-management)  
- [Service and Systemctl Management](#service-and-systemctl-management)  
- [Networking Commands](#networking-commands)  
- [Package Management (DNF)](#package-management-dnf)  
- [System Monitoring](#system-monitoring)  
- [Disk and Storage Management](#disk-and-storage-management)  

## System Information

```bash
uname -r # Display Linux kernel version 
hostname # Show system hostname 
whoami # Show current logged-in user 
uptime # Show system uptime 
date # Display system date and time 
cal # Show calendar 
df -h # Show disk usage in human-readable format 
free -m # Display memory usage in MB
```

## File and Directory Management  

```bash
pwd             # Show current directory path  
ls -l           # List files in long format  
ls -a           # List all files, including hidden ones  
cd /path        # Change directory  
mkdir dir       # Create a new directory  
rmdir dir       # Remove an empty directory  
rm file         # Remove a file  
rm -r dir       # Remove a directory and its contents  
cp src dst      # Copy file or directory  
mv old new      # Rename or move a file  
find /path -name "*.log"  # Find files by name  
```

## File Creation and Editing

```bash
touch file          # Create an empty file  
echo "Hello" > file  # Create a file with content  
cat > file         # Create a file and write to it (Ctrl+D to save)  
nano file          # Open file in Nano editor  
vim file           # Open file in Vim editor  
vi file            # Open file in Vi editor  
cat file           # View file content  
head -n 10 file    # Show first 10 lines of a file  
tail -n 10 file    # Show last 10 lines of a file  
```

## User and Group Management

```bash
whoami       # Show current user  
id user      # Show user ID and group ID  
adduser user # Add a new user  
passwd user  # Change user password  
usermod -aG group user  # Add user to a group  
groups user  # Show groups of a user  
deluser user # Delete a user  
```

## Permissions and Ownership

```bash
ls -l        # View file permissions  
chmod 644 file  # Change file permissions (rw-r--r--)  
chown user:file file  # Change file owner and group  
chmod +x script.sh  # Make a script executable  
umask 022     # Default permission settings  
```  

## Process Management

```bash
ps aux       # List all running processes  
top          # Monitor system processes  
htop         # Interactive process viewer (install via `dnf install htop`)  
kill PID     # Kill a process by PID  
pkill name   # Kill processes by name  
bg           # Resume a process in the background  
fg           # Bring a background process to the foreground  
```

## Service and Systemctl Management

```bash
systemctl status service  # Check service status  
systemctl start service   # Start a service  
systemctl stop service    # Stop a service  
systemctl restart service # Restart a service  
systemctl enable service  # Enable a service at boot  
systemctl disable service # Disable a service at boot  
journalctl -xe           # View system logs  
```

## Networking Commands

```bash
ip a          # Show IP addresses  
ip route      # Display routing table  
ping host     # Test network connectivity  
curl url      # Fetch URL content  
wget url      # Download a file  
netstat -tulnp  # Show open ports (install via `dnf install net-tools`)  
ss -tulnp     # Show open sockets and ports  
```

## Package Management (DNF)

```bash
dnf install package  # Install a package  
dnf remove package   # Remove a package  
dnf update          # Update all packages  
dnf list installed  # List installed packages  
dnf search package  # Search for a package  
rpm -qa | grep package  # Find installed RPM package  
```

## System Monitoring

```bash
uptime        # Show system uptime  
df -h         # Display disk space usage  
du -sh folder # Show folder size  
free -m       # Show memory usage  
vmstat 1      # Display CPU and memory stats  
iostat        # Show CPU and I/O usage (install via `dnf install sysstat`)  
```

## Disk and Storage Management

```bash
lsblk         # List block devices  
fdisk -l      # Show disk partitions  
mount /dev/sdX /mnt  # Mount a device  
umount /mnt   # Unmount a device  
mkfs.ext4 /dev/sdX  # Format a disk as ext4  
df -h         # Check disk usage  
```

---
