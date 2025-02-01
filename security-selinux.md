### Security and SELinux

Security is a critical aspect of system administration, and RHEL provides robust tools and features to secure your system. One of the most powerful security frameworks in RHEL-based systems is SELinux (Security-Enhanced Linux), which helps enforce access control policies and provides an additional layer of protection.

#### 1. **Overview of SELinux**

SELinux is a mandatory access control (MAC) system that enhances security by enforcing policies that restrict how processes interact with each other and the system's resources. Unlike traditional discretionary access control (DAC) models, SELinux operates on the principle of least privilege, ensuring that even if an attacker gains access to a user or process, they cannot easily escalate their privileges or affect other parts of the system.

##### Key Concepts:

- **SELinux Modes**:
    - **Enforcing**: SELinux policies are enforced, and access is denied if a process tries to perform an unauthorized action.
    - **Permissive**: SELinux only logs policy violations but does not enforce them, allowing you to debug configurations.
    - **Disabled**: SELinux is completely turned off, which is not recommended for production systems.
- **Contexts**: Each file, process, and resource in the system has an associated SELinux context, consisting of three parts:
    - **User**: Represents the security user of the resource (e.g., system_u, user_u).
    - **Role**: Defines the role the resource belongs to (e.g., sysadm_r).
    - **Type**: Describes the specific type of object or process (e.g., httpd_t for web servers).

#### 2. **Configuring SELinux**

##### Checking SELinux Status:

To check the current SELinux status and mode, run:
```bash
getenforce
```

This command will return `Enforcing`, `Permissive`, or `Disabled`.

To view more detailed information about SELinux:
```bash
sestatus
```

##### Enabling or Disabling SELinux:

You can change the SELinux mode by editing the `/etc/selinux/config` file. Here's how:

1. **Open the SELinux configuration file**:
```bash
sudo vi /etc/selinux/config
```

2. **Modify the `SELINUX` parameter**:

To enable SELinux, set it to `enforcing` or `permissive`:
```bash
SELINUX=enforcing
```

To disable SELinux:
```bash
SELINUX=disabled
```

3. **Reboot the system** for the changes to take effect.

#### 3. **SELinux Policy Management**

##### Changing SELinux Modes Temporarily:

You can change the mode of SELinux temporarily without rebooting by using the `setenforce` command:
```bash
sudo setenforce 1  # Enforcing mode
sudo setenforce 0  # Permissive mode
```

##### Modifying SELinux Policies:

To adjust SELinux policies for specific applications or use cases, the `semanage` tool is used. For example, to allow a web server to connect to a specific port:
```bash
sudo semanage port -a -t http_port_t -p tcp 8080
```

##### Checking SELinux Alerts:

SELinux logs policy violations in `/var/log/audit/audit.log`. To view recent alerts:
```bash
sudo ausearch -m avc -ts recent
```

#### 4. **Security Best Practices**

- **Enforce SELinux**: Always use SELinux in Enforcing mode for better security.
- **Update SELinux Policies**: Regularly update SELinux policies to ensure they are up-to-date with the latest security patches.
- **Use SELinux for Web Servers**: Configure SELinux contexts for web servers (e.g., Apache, Nginx) to limit what resources they can access.
- **Avoid Disabling SELinux**: Only disable SELinux in rare circumstances, and never on production servers.

#### 5. **Securing SSH and Preventing Brute-Force Attacks**

##### Configuring SSH:

To harden SSH, modify the `/etc/ssh/sshd_config` file:

**Disable root login**:
```bash
PermitRootLogin no
```

**Limit user access**: Only allow specific users to log in:
```bash
AllowUsers user1 user2
```

**Enable key-based authentication**: Disable password-based login and enforce SSH keys:
```bash
PasswordAuthentication no
```

For detailed SSH configurations security-wise, see: https://github.com/CommodoreAlex/Services
##### Install and Configure Fail2ban:

Fail2ban is a useful tool for preventing brute-force SSH attacks. To install and configure it:
```bash
sudo dnf install fail2ban
```

Start and enable the service:
```bash
sudo systemctl enable --now fail2ban
```

Fail2ban will automatically block IP addresses that have multiple failed login attempts.

#### 6. **Hardening System Configurations**

**Disable unnecessary services**: Disable services that are not required for your system’s function.

**Use auditd**: The `auditd` service helps track security-relevant events. Install and configure it:
```bash
sudo dnf install audit
sudo systemctl enable --now auditd
```

Check logs using:
```bash
sudo ausearch -m avc
```

---


Securing your RHEL-based system involves multiple layers, from enforcing SELinux policies to securing SSH and managing services. By understanding and configuring SELinux, you ensure that your system has a robust access control mechanism that provides an additional layer of defense against unauthorized access and potential exploits.
