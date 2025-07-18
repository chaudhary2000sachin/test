# Standard Operating Procedure (SOP): Disk Usage and Ulimit Management

## Purpose

To provide best practices and step-by-step instructions for monitoring disk usage and managing user limits (`ulimit`) on Linux systems, especially in AWS EC2 environments, ensuring system stability, efficient resource utilization, and compliance with industry standards.

## Scope

This SOP applies to Linux-based systems, with a particular focus on AWS EC2 environments. It is intended for system administrators, DevOps engineers, and IT operations staff responsible for monitoring disk usage and configuring user limits.

## Prerequisites

- Access to a Linux system (preferably with root or sudo privileges).
- Basic knowledge of Linux command-line operations.
- AWS account and EC2 instance access for storage block management.
- Familiarity with text editors (e.g., nano, vim) for configuration file edits.
- Understanding of systemd service management (for resource limits on services).

## Procedure

---

## Table of Contents

1. [Introduction](#introduction)
2. [Disk Usage in Linux](#disk-usage-in-linux)
    - [1.1. Checking Disk Usage](#11-checking-disk-usage)
        - [1.1.1. `df` Command](#111-df-command)
        - [1.1.2. `du` Command](#112-du-command)
    - [1.2. Mount Points](#12-mount-points)
    - [1.3. Mounting and Unmounting Storage Blocks on AWS EC2](#13-mounting-and-unmounting-storage-blocks-on-aws-ec2)
3. [Configuring Ulimit Settings](#configuring-ulimit-settings)
    - [2.1. Checking Current Ulimit Values](#21-checking-current-ulimit-values)
    - [2.2. Setting Temporary Ulimit](#22-setting-temporary-ulimit)
    - [2.3. Configuring Persistent Ulimits for Users](#23-configuring-persistent-ulimits-for-users)
    - [2.4. Ulimit for systemd Services](#24-ulimit-for-systemd-services)
    - [2.5. Verifying Effective Limits](#25-verifying-effective-limits)
4. [References](#references)

---

## Introduction

This SOP provides best practices and step-by-step instructions for monitoring disk usage and managing user limits (`ulimit`) on Linux systems, with a specific focus on AWS EC2 environments. Following these guidelines ensures system stability, efficient resource utilization, and compliance with industry standards.

---

## Disk Usage in Linux

### 1.1. Checking Disk Usage

#### 1.1.1. `df` Command

The `df` command reports file system disk space usage.

- **Display disk usage in human-readable format:**
  ```bash
  df -h
  ```
  <img width="635" height="198" alt="Image" src="https://github.com/user-attachments/assets/f9b990a3-4a0e-4f30-ae87-b7354054ccd4" />

  
- **Show all mounted file systems (including pseudo-file systems):**
  ```bash
  df -a
  ```

  <img width="694" height="311" alt="Image" src="https://github.com/user-attachments/assets/5671b62e-2699-4433-a32b-dfa7b700046f" />
- **Show file system type for each partition:**
  ```bash
  df -T
  ```
  <img width="834" height="228" alt="Image" src="https://github.com/user-attachments/assets/24cffa6a-ec68-4d3c-9856-b1a013a4a0b9" />

#### 1.1.2. `du` Command

The `du` command estimates file and directory space usage.

- **Display directory usage in human-readable format:**
  ```bash
  du -h /path/to/directory
  ```
  <img width="515" height="121" alt="Image" src="https://github.com/user-attachments/assets/3be7168e-43f7-4e27-b9fb-aca70a20837c" />
- **Summarize total usage of a directory:**
  ```bash
  du -sh /path/to/directory
  ```

  <img width="441" height="75" alt="Image" src="https://github.com/user-attachments/assets/e75d623f-ebbd-481d-8842-cfc26af3dec8" />
- **Display size of all files and subdirectories:**
  ```bash
  du -a /path/to/directory
  ```

  <img width="822" height="291" alt="Image" src="https://github.com/user-attachments/assets/7c9a636f-66b5-44b8-a61b-47fe1a0f93fe" />
- **Show usage for each file and directory in the current directory:**
  ```bash
  du -sh *
  ```

  <img width="413" height="313" alt="Image" src="https://github.com/user-attachments/assets/34114756-3fe8-450f-9203-0262c0a93475" />

---

### 1.2. Mount Points

A mount point is a directory where an additional file system is attached and made accessible.

**Mount Syntax:**
```bash
sudo mount [options] <device> <mount_point>
```
- `<device>`: The partition to mount.
- `<mount_point>`: Directory to mount the device.
- `[options]`: Additional options for mounting.

**Common `mount` Options:**

| Option         | Description                                              |
| -------------- | --------------------------------------------------------|
| `-t <type>`    | File system type (ext4, ntfs, vfat, nfs, etc.)          |
| `-o <options>` | Mount options (`ro` for read-only, `rw` for read-write) |
| `-a`           | Mount all file systems listed in `/etc/fstab`            |
| `-l`           | List all currently mounted file systems                  |
| `--bind`       | Bind a directory to another location                     |

---

### 1.3. Mounting and Unmounting Storage Blocks on AWS EC2

**Steps to attach and mount a new EBS volume:**

1. **Attach EBS volume to your EC2 instance via AWS Console.**
2. **Detect the new disk:**
    ```bash
    lsblk
    ```

    <img width="563" height="198" alt="Image" src="https://github.com/user-attachments/assets/b99e501c-2015-4d0d-83dd-0f91574a183a" />

    - Here: xvdf is new disk with 10GB storage.

3. **Partition the new disk:**
    ```bash
    sudo fdisk /dev/xvdf
    ```
    - Inside `fdisk`, follow prompts:
        - `n` (new partition)
        - `p` (primary)
        - `1` (partition number)
        - `Enter` (accept defaults)
        - `w` (write changes)


    <img width="723" height="290" alt="Image" src="https://github.com/user-attachments/assets/6f49037e-33a1-4be3-949f-a895dbb41215" />

- Now check

     ```bash
    lsblk
    ```

  <img width="563" height="212" alt="Image" src="https://github.com/user-attachments/assets/e3f7e1b4-7f81-4f0f-9a0c-15c4ef9c5f95" />
  
4. **Create a file system:**
    ```bash
    sudo mkfs.ext4 /dev/xvdf1
    ```


    <img width="628" height="198" alt="Image" src="https://github.com/user-attachments/assets/8412e97f-7219-4d5d-bb95-c4552bb593ec" />
  
5. **Create a mount point:**
    ```bash
    mkdir extradisk
    ```

6. **Mount the partition:**
    ```bash
    sudo mount /dev/xvdf1 extradisk
    ```

    <img width="571" height="247" alt="Image" src="https://github.com/user-attachments/assets/2948f51d-7c75-4d38-9d18-628b09e3851c" />

7. **Unmount when needed:**
    ```bash
    sudo umount extradisk
    ```

    <img width="571" height="242" alt="Image" src="https://github.com/user-attachments/assets/15f7097d-06ad-402f-8947-f27229cc91db" />

---

## Configuring Ulimit Settings

`ulimit` sets user-level resource limits for system stability and security.

### 2.1. Checking Current Ulimit Values

- **All limits for current shell:**
  ```bash
  ulimit -a
  ```

   <img width="578" height="396" alt="Image" src="https://github.com/user-attachments/assets/d8aa11a7-5fb7-4072-aed2-331411f8ff72" />
  
- **For a specific limit (e.g., open files):**
  ```bash
  ulimit -n
  ```

   <img width="578" height="75" alt="Image" src="https://github.com/user-attachments/assets/063735c9-0863-44bd-9341-4d28d60aab59" />

### 2.2. Setting Temporary Ulimit

- **Set open files limit for current session:**
  ```bash
  ulimit -n 4096
  ```
  <img width="578" height="99" alt="Image" src="https://github.com/user-attachments/assets/5e7547c8-c72d-490c-92db-a93e8d8f12f3" />
> _Note: This change lasts only for the current shell session._

### 2.3. Configuring Persistent Ulimits for Users

- **Edit `/etc/security/limits.conf`:**
  ```bash
  sudo nano /etc/security/limits.conf
  ```
- **Add entries:**
  ```
  username   soft   nofile  4096
  username   hard   nofile  8192
  ```
  - For all users:
    ```
    *   soft   nofile  4096
    *   hard   nofile  8192
    ```

    <img width="853" height="576" alt="Image" src="https://github.com/user-attachments/assets/fc98799e-b2e2-46f4-8ca2-51b3ed573044" />

- **Fields:**
    - `soft`: User-modifiable limit (up to the hard limit)
    - `hard`: Max enforceable limit

### 2.4. Ulimit for systemd Services

- **Override or edit the service unit file:**
    ```
    [Service]
    LimitNOFILE=8192
    ```
- **Reload systemd and restart the service:**
    ```bash
    sudo systemctl daemon-reload
    sudo systemctl restart <service-name>
    ```

### 2.5. Verifying Effective Limits

- **After login or restart:**
    ```bash
    ulimit -a
    ```
- **For a running process (by PID):**
    ```bash
    cat /proc/<PID>/limits
    ```

---

## Troubleshooting

- If a new EBS volume does not appear after attachment, verify in AWS Console and check `lsblk` output.
- If unable to mount a partition, check filesystem type and mount point permissions.
- After editing `/etc/security/limits.conf`, log out and back in to apply user limits.
- For systemd service limit changes, ensure `daemon-reload` and service restart are performed.
- Review system logs (`/var/log/syslog`, `journalctl`) for errors related to disk or ulimit operations.

---

## References

- [Linux man pages: df(1), du(1), mount(8), umount(8)](https://man7.org/linux/man-pages/)
- [AWS Documentation: Attaching EBS Volumes](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-attaching-volume.html)
- [Linux System Administrator’s Guide](https://www.tldp.org/LDP/sag/html/)
- [systemd Resource Control](https://www.freedesktop.org/software/systemd/man/systemd.resource-control.html)

---

## Revision History

| Version | Date       | Author           | Description                        |
| ------- | ---------- | ----------------| -----------------------------------|
| 1.0     | 2025-07-18 | Sachin Chaudhary| Initial creation and documentation |
