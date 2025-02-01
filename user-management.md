# User and Group Management in RHEL

Managing users and groups effectively is essential for system administration in RHEL-based Linux environments. This guide will cover creating, modifying, and deleting users and groups, setting permissions, and enforcing security policies.

---

## User Management

### Creating a New User

To create a new user, use the `useradd` command:
```bash
sudo useradd username
```

Set a password for the user:
```bash
sudo passwd username
```

To create a user with a home directory (if not created by default):
```bash
sudo useradd -m username
```

### Modifying a User Account

To change user information, use `usermod`:
```bash
sudo usermod -c "Full Name" username
```

To change a user's home directory:
```bash
sudo usermod -d /new/home/directory username
```

To add a user to a supplementary group:
```bash
sudo usermod -aG groupname username
```

### Deleting a User

To remove a user account:
```bash
sudo userdel username
```

To remove a user and their home directory:
```bash
sudo userdel -r username
```

---

## Group Management

### Creating a Group

To create a new group:
```bash
sudo groupadd groupname
```

### Adding Users to a Group

To add a user to an existing group:
```bash
sudo usermod -aG groupname username
```

### Viewing Group Memberships

To see which groups a user belongs to:
```bash
groups username
```

To view all system groups:
```bash
cat /etc/group
```

### Removing a User from a Group

To remove a user from a group:
```bash
sudo gpasswd -d username groupname
```

### Deleting a Group

To delete a group:
```bash
sudo groupdel groupname
```

---

## Managing Permissions and Ownership

### Changing File Ownership

To change the ownership of a file or directory:
```bash
sudo chown username:groupname filename
```

### Modifying File Permissions

To change permissions using `chmod`:
```bash
chmod 755 filename
```

Where:
- `7` = read, write, execute (owner)
- `5` = read and execute (group)
- `5` = read and execute (others)

To recursively change permissions for a directory:
```bash
chmod -R 700 /path/to/directory
```

### Using Access Control Lists (ACLs)

To grant additional permissions using ACL:
```bash
sudo setfacl -m u:username:rwx filename
```

To view ACLs on a file:
```bash
getfacl filename
```

---

## Best Practices

- Always create user accounts with the principle of least privilege.
- Use strong passwords and enforce password policies.
- Regularly audit user accounts and remove unused ones.
- Utilize groups for easier permission management instead of assigning permissions per user.
