# Networking Configuration on RHEL

## Overview

Networking is a critical aspect of any Linux system, allowing communication between devices and services. In RHEL-based systems, network configuration is managed using **NetworkManager**, command-line tools, and configuration files.

## Checking Network Interfaces

List available network interfaces:
```bash
ip a
```

Or using:
```bash
nmcli device status
```

## Configuring Static IP Address

To configure a static IP, edit the appropriate network configuration file:
```bash
sudo vi /etc/sysconfig/network-scripts/ifcfg-<interface-name>
```

Example configuration for a static IP:
```ini
DEVICE=eth0
BOOTPROTO=none
ONBOOT=yes
IPADDR=192.168.1.100
PREFIX=24
GATEWAY=192.168.1.1
DNS1=8.8.8.8
DNS2=8.8.4.4
```

Restart networking service:
```bash
sudo systemctl restart NetworkManager
```

Or bring the interface up manually:
```bash
sudo nmcli connection up <interface-name>
```

## Using `nmcli` for Network Management

Show active connections:
```bash
nmcli con show
```

Modify an existing connection:
```bash
nmcli con mod <connection-name> ipv4.addresses 192.168.1.100/24 ipv4.gateway 192.168.1.1 ipv4.dns "8.8.8.8 8.8.4.4" ipv4.method manual
```

Bring the connection up:
```bash
nmcli con up <connection-name>
```


## Managing Network Services

Restart Network Manager:
```bash
sudo systemctl restart NetworkManager
```

Enable it at boot:
```bash
sudo systemctl enable NetworkManager
```


## Firewall Considerations

Ensure your firewall allows traffic on necessary ports:

```bash
sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --add-service=ssh --permanent
sudo firewall-cmd --reload
```

## Troubleshooting Network Issues

Check interface status:
```bash
ip link show
```

Restart network service:
```bash
sudo systemctl restart NetworkManager
```

Test connectivity:
```bash
ping 8.8.8.8
```

View logs:
```bash
journalctl -u NetworkManager --no-pager | tail -n 20
```

---

