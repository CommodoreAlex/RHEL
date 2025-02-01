# Package Management with DNF

## Overview

DNF (Dandified YUM) is the default package manager for RHEL-based Linux distributions. It is used to install, update, and manage software packages efficiently.

## Installing Packages

To install a package, use the following command:
```bash
sudo dnf install <package-name>
```

Example:
```bash
sudo dnf install httpd
```

## Removing Packages

To remove an installed package:
```bash
sudo dnf remove <package-name>
```

Example:
```bash
sudo dnf remove httpd
```

## Updating Packages

To update a specific package:
```bash
sudo dnf update <package-name>
```

Example:
```bash
sudo dnf update httpd
```

To update all installed packages:
```bash
sudo dnf update -y
```

## Searching for Packages

To search for available packages:
```bash
dnf search <package-name>
```

Example:
```bash
dnf search nginx
```

## Listing Installed Packages

To list all installed packages:
```bash
dnf list installed
```

To check if a specific package is installed:
```bash
dnf list installed | grep <package-name>
```

## Enabling and Disabling Repositories

To list available repositories:
```bash
dnf repolist
```

To enable a repository:
```bash
sudo dnf config-manager --set-enabled <repo-name>
```

To disable a repository:
```bash
sudo dnf config-manager --set-disabled <repo-name>
```

## Clearing the DNF Cache

To clean up unnecessary cache files:
```bash
sudo dnf clean all
```


---

