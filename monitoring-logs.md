# System Monitoring and Logs in RHEL

## Introduction

Monitoring system performance and analyzing logs are crucial tasks for system administrators. This guide covers essential tools and techniques for monitoring RHEL-based systems and managing logs effectively.

---

## Monitoring System Performance

### Using `top`

The `top` command provides a real-time view of system resource usage, including CPU, memory, and running processes.
```bash
 top
```

Press `q` to exit.

### Using `htop`

A more user-friendly alternative to `top` is `htop`. Install it using:
```bash
 sudo dnf install -y htop
 htop
```

Use arrow keys to navigate and `F10` to quit.

### Checking CPU Usage with `mpstat`

The `mpstat` command (from the `sysstat` package) provides CPU usage statistics:
```bash
 sudo dnf install -y sysstat
 mpstat
```

### Monitoring Memory Usage with `free`

To check memory utilization:
```bash
 free -h
```

### Checking Disk Usage with `df` and `du`

View disk usage for mounted filesystems:
```bash
 df -h
```

Analyze specific directory sizes:
```bash
 du -sh /path/to/directory
```

### Monitoring Network Activity with `nload`

Install `nload` to monitor real-time network traffic:
```bash
 sudo dnf install -y nload
 nload
```

---

## System Logs Management

Logs provide critical system and security event information. RHEL stores logs in `/var/log/`.

### Viewing Logs with `journalctl`

RHEL uses `journald` for logging. Some useful commands:

View full system log:
```bash
 journalctl
```

View logs for a specific service (e.g., SSH):
```bash
 journalctl -u sshd
```

View logs since last boot:
```bash
 journalctl -b
```

### Checking Logs in `/var/log/`

- System logs: `/var/log/messages`
- Authentication logs: `/var/log/secure`
- Boot logs: `/var/log/boot.log`

Example to view logs:
```bash
 cat /var/log/messages | less
```

### Filtering Logs

To find specific events, use `grep`:
```bash
 journalctl | grep "error"
```

---

## Setting Up Log Rotation

Log rotation prevents logs from consuming excessive disk space.

The `logrotate` tool manages log rotation based on `/etc/logrotate.conf` and `/etc/logrotate.d/` configurations.

Manually trigger log rotation:
```bash
 sudo logrotate -f /etc/logrotate.conf
```

---
