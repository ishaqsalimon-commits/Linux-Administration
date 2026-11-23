# Linux Administration – Research Questions

## Project Overview

This project contains research questions and answers covering the fundamental concepts of Linux Administration. It explores Linux operating systems, user and file management, system administration, networking, package management, system monitoring, security, backup and recovery.

The purpose of this project is to develop an understanding of Linux administration and the commands used to manage and maintain Linux systems.

## Table of Contents

1. [Basic Concepts](#1-basic-concepts)
2. [User and File Management](#2-user-and-file-management)
3. [System Administration](#3-system-administration)
4. [Networking](#4-networking)
5. [Package Management](#5-package-management)
6. [Monitoring and Performance](#6-monitoring-and-performance)
7. [Security](#7-security)
8. [Backup and Recovery](#8-backup-and-recovery)
9. [Conclusion](#9-conclusion)
10. [References](#10-references)

---

## 1. Basic Concepts

### 1.1 Differences Between Linux, Windows and macOS

Linux, Windows and macOS are operating systems used to manage computer hardware and software.

| Feature | Linux | Windows | macOS |
|---|---|---|---|
| Source code | Open-source | Proprietary | Proprietary |
| Cost | Mostly free | Usually requires a licence | Included with Apple computers |
| Security | Strong security features | Built-in security features | Built-in security features |
| Customisation | Highly customisable | Moderately customisable | Limited customisation |
| Common use | Servers and desktops | Personal and business computers | Apple computers |

Linux is popular because it is flexible, secure, free and suitable for server administration.

### 1.2 Linux File System Hierarchy

Linux uses a hierarchical file system that starts from the root directory (`/`).

Important directories include:

- `/bin` - Essential user commands.
- `/etc` - System configuration files.
- `/home` - Personal user directories.
- `/root` - Root administrator's home directory.
- `/var` - Variable data and log files.
- `/tmp` - Temporary files.
- `/boot` - Boot files.
- `/dev` - Device files.
- `/usr` - Applications and system utilities.

### 1.3 Linux Distributions

A Linux distribution is an operating system built around the Linux kernel with additional software and utilities.

Popular distributions include:

1. **Ubuntu:** Used for desktops, servers and cloud computing.
2. **Debian:** Known for stability and reliability.
3. **Kali Linux:** Used for penetration testing and cybersecurity.
4. **Fedora:** Popular with developers and technology enthusiasts.
5. **Red Hat Enterprise Linux:** Used in enterprise environments.

---

## 2. User and File Management

### 2.1 Managing Users and Groups

Linux administrators create and manage users and groups to control system access.

| Command | Description |
|---|---|
| `sudo adduser john` | Creates a user |
| `sudo passwd john` | Changes a password |
| `sudo userdel john` | Deletes a user |
| `sudo usermod -aG developers john` | Adds a user to a group |
| `sudo groupadd developers` | Creates a group |
| `sudo groupdel developers` | Deletes a group |
| `id john` | Displays user information |

Example:

```bash
sudo adduser john
sudo groupadd developers
sudo usermod -aG developers john
groups john
```

### 2.2 Linux File Permissions

Linux file permissions determine who can read, write and execute files.

The three main permissions are:

- `r` - Read permission.
- `w` - Write permission.
- `x` - Execute permission.

Permissions are assigned to:

- User (owner).
- Group.
- Others.

Example:

```bash
chmod 755 file.txt
chmod 644 file.txt
chmod u+x script.sh
```

| Permission | Numeric Value |
|---|---:|
| Read | 4 |
| Write | 2 |
| Execute | 1 |
| None | 0 |

### 2.3 Managing File Ownership

Linux uses `chown` and `chgrp` to manage ownership.

```bash
sudo chown john file.txt
sudo chgrp developers file.txt
sudo chown john:developers file.txt
```

These commands change file ownership and group ownership.

---

## 3. System Administration

### 3.1 System Services and Daemons

System services are background programs that perform important operating system tasks.

The `systemctl` command manages services on systems using systemd.

```bash
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl restart ssh
sudo systemctl status ssh
sudo systemctl enable ssh
sudo systemctl disable ssh
```

### 3.2 Scheduling Tasks with Cron and At

Cron schedules repetitive tasks, while `at` schedules one-time tasks.

Edit cron jobs:

```bash
crontab -e
```

Example:

```bash
0 2 * * * /home/john/backup.sh
```

This executes a backup script every day at 2 AM.

Schedule a one-time task:

```bash
at 5:00 PM
```

### 3.3 The /etc/fstab File

The `/etc/fstab` file stores information about file systems and their mounting configurations.

Mount a file system:

```bash
sudo mount /dev/sdb1 /mnt
```

Unmount a file system:

```bash
sudo umount /mnt
```

Display disk information:

```bash
df -h
```

---

## 4. Networking

### 4.1 Basic Linux Networking Commands

| Command | Purpose |
|---|---|
| `ifconfig` | Displays network interface information (legacy) |
| `ip addr` | Displays IP addresses |
| `ip link` | Displays network interfaces |
| `ping` | Tests network connectivity |
| `netstat` | Displays network statistics (legacy) |
| `ss` | Displays socket information |
| `ip route` | Displays routing information |

Examples:

```bash
ip addr
ping google.com
ss -tuln
ip route
```

### 4.2 Configuring a Static IP Address

A static IP address is manually assigned to a computer or server.

Example using Netplan:

```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: false
      addresses:
        - 192.168.1.100/24
      routes:
        - to: default
          via: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 1.1.1.1
```

Apply the configuration:

```bash
sudo netplan apply
```

### 4.3 Linux Firewalls

Firewalls control incoming and outgoing network traffic.

Linux commonly uses iptables and firewalld.

Using iptables:

```bash
sudo iptables -L
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

Using firewalld:

```bash
sudo systemctl start firewalld
sudo firewall-cmd --state
sudo firewall-cmd --add-service=ssh --permanent
sudo firewall-cmd --reload
```

---

## 5. Package Management

### 5.1 Linux Package Managers

Package managers install, update and remove software.

| Package Manager | Distributions | Package Format |
|---|---|---|
| APT | Ubuntu and Debian | DEB |
| YUM | Older RHEL-based systems | RPM |
| DNF | Fedora and modern RHEL-based systems | RPM |

### 5.2 Installing, Updating and Removing Packages

Using APT:

```bash
sudo apt update
sudo apt upgrade
sudo apt install nginx
sudo apt remove nginx
```

Using DNF:

```bash
sudo dnf install nginx
sudo dnf update
sudo dnf remove nginx
```

Using YUM:

```bash
sudo yum install nginx
sudo yum update
sudo yum remove nginx
```

---

## 6. Monitoring and Performance

### 6.1 Linux Performance Monitoring Tools

Linux provides different tools for monitoring system performance.

| Tool | Purpose |
|---|---|
| `top` | Monitors running processes and resource usage |
| `htop` | Interactive process monitoring |
| `vmstat` | Monitors memory, CPU and system activity |
| `iostat` | Monitors CPU and disk input/output |

Examples:

```bash
top
htop
vmstat 2
iostat -xz 2
```

### 6.2 Checking Disk Usage

The `df` command displays disk space availability.

```bash
df -h
```

The `du` command displays directory storage usage.

```bash
du -sh /home
du -sh *
```

---

## 7. Security

### 7.1 Secure Shell (SSH)

SSH stands for Secure Shell. It provides encrypted remote access to Linux systems.

Install the SSH server on Ubuntu:

```bash
sudo apt update
sudo apt install openssh-server
```

Start and enable SSH:

```bash
sudo systemctl start ssh
sudo systemctl enable ssh
```

Connect to a remote server:

```bash
ssh username@192.168.1.100
```

Generate SSH keys:

```bash
ssh-keygen -t ed25519
```

### 7.2 SELinux and AppArmor

SELinux and AppArmor are security systems that restrict access to system resources.

**SELinux:**
- Commonly used in Fedora and Red Hat systems.
- Uses security policies to control processes.
- Helps prevent unauthorised access.

Check status:

```bash
sestatus
```

**AppArmor:**
- Commonly used in Ubuntu.
- Uses security profiles to restrict applications.
- Controls application access to files and resources.

Check status:

```bash
sudo aa-status
```

---

## 8. Backup and Recovery

### 8.1 Linux Backup Tools

Backups protect important information against accidental deletion, system failures and data corruption.

**Rsync:**

Synchronises files and directories.

```bash
rsync -av /home/user/ /backup/user/
```

**Tar:**

Creates compressed archives.

```bash
tar -czvf backup.tar.gz /home/user
```

Extract an archive:

```bash
tar -xzvf backup.tar.gz
```

**DD:**

Copies data at a low level, including disks and partitions.

```bash
sudo dd if=/dev/sdb of=/backup/disk.img bs=4M status=progress
```

Use `dd` carefully because incorrect device names can cause data loss.

### 8.2 System Recovery Strategies

Common Linux recovery strategies include:

1. Performing regular backups.
2. Using a Linux Live USB to access damaged systems.
3. Restoring files from backup archives.
4. Using recovery mode to troubleshoot boot problems.
5. Using `fsck` to check and repair file systems.
6. Checking system logs using `journalctl`.
7. Maintaining disaster recovery plans.

Example:

```bash
sudo fsck /dev/sdb1
journalctl -xe
```

---

## 9. Conclusion

Linux administration is an essential skill in information technology. It involves managing users, files, system services, networking, software packages, security and system performance.

Understanding Linux commands and administration tools helps system administrators maintain reliable, secure and efficient computer systems.

This project provides a foundation for learning practical Linux administration and understanding how Linux systems are managed in real-world IT environments.

---

## 10. References

The following official resources were used as references for Linux administration research:

1. [Linux Kernel Documentation](https://www.kernel.org/doc/html/latest/)
2. [Ubuntu Server Documentation](https://ubuntu.com/server/docs)
3. [Debian Documentation](https://www.debian.org/doc/)
4. [Red Hat Enterprise Linux](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux)
5. [systemd Documentation](https://www.freedesktop.org/software/systemd/man/latest/systemctl.html)
6. [Linux Manual Pages](https://man7.org/linux/man-pages/)

---

**Project:** Linux Administration Research Questions  
**Category:** Linux / System Administration  
**Format:** Markdown (`README.md`)  
**Platform:** GitHub
