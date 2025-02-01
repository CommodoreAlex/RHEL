### Process and Service Management

Managing processes and services efficiently is crucial to maintaining system stability and performance. In RHEL-based systems, you can control and monitor system processes and services using a variety of commands and tools. This section covers managing system processes, controlling services, and handling background jobs.

#### 1. **Managing Processes**

A **process** is a running instance of a program. Every time a program is executed, it becomes a process with a unique process ID (PID).

##### Viewing Processes:

To view a list of running processes, use the `ps` command:
```bash
ps aux
```

This command displays detailed information about all running processes, including their PID, memory usage, and the command that launched them.

For a dynamic view, use `top` or `htop` (if installed):
```bash
top
```

`htop` is a more user-friendly alternative with color-coded output:
```bash
sudo dnf install htop
htop
```

##### Searching for a Process:

To search for a specific process, use the `pgrep` command:
```bash
pgrep <process_name>
````

For example, to find the PID of a running Apache server:
```bash
pgrep httpd
````

##### Killing a Process:

If a process becomes unresponsive or you need to stop it, you can kill it using the `kill` command followed by the PID:
```bash
sudo kill <PID>
````

To forcefully kill a process, use the `-9` signal:
```bash
sudo kill -9 <PID>
````

##### Managing Process Priority:

To change the priority (nice value) of a process, use the `renice` command. A lower nice value increases the priority of the process:
```bash
sudo renice -n -10 -p <PID>
````

#### 2. **Service Management**

In RHEL-based systems, **services** are managed using `systemd`, the default init system. Services are background processes that provide core functionality, such as networking, logging, and web hosting.

##### Starting and Stopping Services:

To start a service:
```bash
sudo systemctl start <service_name>
````

For example, to start the SSH service:
```bash
sudo systemctl start sshd
```

To stop a service:
```bash
sudo systemctl stop <service_name>
````

##### Enabling and Disabling Services:

To enable a service to start automatically at boot:
```bash
sudo systemctl enable <service_name>
````

To disable a service from starting at boot:
```bash
sudo systemctl disable <service_name>
````

##### Checking the Status of a Service:

To check whether a service is running:
```bash
sudo systemctl status <service_name>
````

For example, to check the status of the SSH service:
```bash
sudo systemctl status sshd
```
##### Restarting a Service:

To restart a service (useful if you’ve made configuration changes):
```bash
sudo systemctl restart <service_name>
````

##### Listing All Services:

To list all active services on your system:
```bash
sudo systemctl list-units --type=service
````

#### 3. **Managing System Boot and Shutdown**

`systemd` is responsible for system startup and shutdown. You can control the system's power state with the following commands:

##### Rebooting the System:

To reboot the system:
```bash
sudo reboot
````

##### Shutting Down the System:

To shut down the system:
```bash
sudo shutdown now
````

To schedule a shutdown:
```bash
sudo shutdown +10
````

This command will shut down the system in 10 minutes.

##### Checking System Boot Logs:

To view the system’s boot logs:
```bash
journalctl -b
```

This shows logs from the most recent boot.

#### 4. **Managing Background Processes and Jobs**

In addition to managing processes and services, you may need to manage background tasks and jobs that are not linked to a terminal session.

##### Running a Process in the Background:

To run a process in the background, append an `&` at the end of the command:
```bash
long_running_task &
````

##### Viewing Background Jobs:

To see a list of background jobs, use the `jobs` command:
```bash
jobs
````

##### Bringing a Background Job to the Foreground:

To bring a background job back to the foreground, use the `fg` command:
```bash
fg %1
```

The `%1` refers to the job number.

##### Managing Jobs with `nohup`:

To run a process that keeps running even after you log out, use `nohup`:
```bash
nohup long_running_task &
````

This is useful for processes you want to keep running after closing your terminal session.

#### 5. **Using `systemctl` for Advanced Service Management**

For advanced service management tasks, `systemctl` provides several useful features:

**Reboot after service failure**: To automatically restart a service if it fails, use the `Restart` directive in the service's unit file:
```bash
[Service]
Restart=always
```

Systemd service unit files in these locations can include:
1. **`/usr/lib/systemd/system/`** (Default system services, installed by packages)
    - `sshd.service` (OpenSSH server)
    - `httpd.service` (Apache web server)
    - `cron.service` (Cron job scheduler)
    - `docker.service` (Docker daemon)
2. **`/etc/systemd/system/`** (Custom or overridden services, created by users/admins)
    - `myapp.service` (Custom application service)
    - `nginx.service` (Customized Nginx service)
    - `custom-backup.service` (Automated backup script)
3. **`~/.config/systemd/user/`** (User-specific services, for non-root users)
    - `syncthing.service` (Personal file synchronization)
    - `mpd.service` (Music Player Daemon for a user)
    - `vpn-client.service` (User-specific VPN connection)

Each file defines how systemd should manage the corresponding service.

**Applying Changes**: After modifying the unit file, reload systemd and restart the service:
```bash
sudo systemctl daemon-reload sudo systemctl restart <service-name>
```

**View service logs**: To view logs for a service, use `journalctl`:
```bash
sudo journalctl -u <service_name>
```

---


Effective process and service management are essential for maintaining a responsive and secure RHEL system. By using `systemd` and various commands like `systemctl`, `ps`, and `top`, you can ensure your system operates efficiently and troubleshoot issues as they arise.
