# Fundamental Linux Commands

## Overview

Linux provides several command-line utilities and system directories that are essential for system administration and cybersecurity operations.

This lab explores fundamental Linux concepts, including filesystem navigation, user and group management, package installation, privilege management, and text editing using Nano.

Understanding these concepts is important when administering Linux systems, investigating servers, and working in cybersecurity environments such as Capture The Flag (CTF) challenges.

## Lab Objective

Learn how to use some fundamental Linux commands and understand important Linux concepts.

## Lab Purpose

Explore basic Linux administration operations, including:

- Important Linux files and directories.
- Creating users and groups.
- Managing user group membership.
- Installing software packages.
- Using elevated privileges with `sudo`.
- Editing files using Nano.

## Lab Environment

- **Operating System:** Kali Linux
- **Environment:** Virtual Machine
- **Terminal:** Linux Command Line
- **Package Manager:** APT

## Lab Walkthrough

### Task 1: Explore Important Linux Files and Directories

Begin by opening a terminal in Kali Linux.

Navigate to the root directory:

```bash
cd /
```

Linux has several important directories and configuration files that are useful when administering or investigating a system.

| Path | Purpose |
|---|---|
| `/tmp` | Stores temporary files used by applications and processes. Its contents may be removed during system cleanup or shutdown. |
| `/root` | Home directory of the root user. |
| `/usr` | Contains many user applications, libraries, documentation, and system resources. |
| `/var` | Stores variable data such as logs, caches, databases, and application data. |
| `/bin` | Contains essential user command binaries. |
| `/sbin` | Contains essential system administration binaries. |
| `/etc/passwd` | Stores user account information, including usernames, user IDs, group IDs, and home directories. |
| `/etc/shadow` | Stores password hash information and password-aging data. Access is restricted. |
| `/etc/sudoers` | Defines sudo privileges and permissions for users and groups. |
| `/proc` | Virtual filesystem exposing process and kernel information. |
| `/sys` | Virtual filesystem exposing information about devices, drivers, and the kernel. |
| `/dev` | Contains device files representing hardware and virtual devices. |

**Important security considerations:**

- `/etc/passwd` is generally readable by ordinary users, but it does not normally contain password hashes.
- `/etc/shadow` contains password hash information and is normally accessible only to root and specifically authorized processes.
- `/etc/sudoers` controls which users and groups can execute commands with elevated privileges. Use `visudo` when editing this configuration.
- `/proc`, `/sys`, and `/dev` are special filesystems that expose kernel, process, and device interfaces rather than ordinary directories containing conventional files.
- On modern Linux distributions, `/bin` and `/sbin` may be symbolic links to directories under `/usr`.

### Task 2: Add Users and Groups

Linux supports multiple user accounts and groups to manage access and permissions.

Creating users and groups is an important part of Linux system administration.

These operations normally require root privileges or appropriate administrative permissions.

#### 1. Create a User

Use the `adduser` command:

```bash
sudo adduser username
```

Replace `username` with the desired account name.

On Kali Linux, `adduser` typically guides you through setting a password and providing optional user information.

#### 2. Create a Group

Use the `addgroup` command:

```bash
sudo addgroup groupname
```

Replace `groupname` with the desired group name.

#### 3. Add a User to a Group

Use the `usermod` command:

```bash
sudo usermod -aG sudo username
```

This adds the specified user to the `sudo` group.

Understanding the options:

- `usermod` modifies an existing user account.
- `-a` appends the user to supplementary groups without removing existing supplementary group memberships.
- `-G` specifies the supplementary group or groups.

**Security consideration:**

Adding a user to the `sudo` group grants significant administrative privileges. Only trusted users should receive this level of access.

### Task 3: Install Packages Using APT

APT (Advanced Package Tool) is the package management system used by Debian-based Linux distributions, including Kali Linux.

It allows users to install, update, and manage software packages from configured repositories.

First, update the package information:

```bash
sudo apt update
```

Check for the available ProxyChains package:

```bash
apt search proxychains
```

Install the appropriate package available in your configured repositories. On Kali Linux, the package is commonly:

```bash
sudo apt install proxychains4
```

APT may request your current user's password and ask for confirmation before installing the package.

Type `Y` when prompted to continue.

**Understanding sudo:**

The `sudo` command allows an authorized user to execute a command with elevated privileges without having to switch permanently to the root account.

For example:

```bash
sudo apt install proxychains4
```

When prompted, enter the password of the currently logged-in user who has sudo privileges.

The password characters may not appear while typing. This is normal terminal behavior.

**Important distinction:**

- `sudo` executes a command with elevated privileges.
- `su` switches to another user account.
- `sudo su -` opens a root login shell.

Using `sudo` for individual administrative commands is generally preferable to remaining logged in as root unnecessarily.

### Task 4: Edit Files Using Nano

Nano is a command-line text editor available on Linux systems.

It allows users to create, view, and modify text files directly from the terminal.

Open a file named `md5sums.txt`:

```bash
nano md5sums.txt
```

If the file exists in the current directory, Nano opens it for editing. If it does not exist, Nano allows you to create it.

Within the Nano interface:

- Use the arrow keys to navigate.
- Type directly to add or modify text.
- Use the displayed keyboard shortcuts to perform editing operations.

#### Save and Exit

To save changes:

1. Press `Ctrl + O`.
2. Press `Enter` to confirm the filename.

To exit Nano:

1. Press `Ctrl + X`.

If changes have not been saved, Nano will ask whether you want to save them before exiting.

## Important Commands Covered

| Command | Function |
|---|---|
| `cd /` | Navigates to the root directory. |
| `adduser` | Creates a user account. |
| `addgroup` | Creates a group. |
| `usermod -aG` | Adds a user to supplementary groups. |
| `apt update` | Refreshes package repository information. |
| `apt search` | Searches available packages. |
| `apt install` | Installs a software package. |
| `sudo` | Executes commands with elevated privileges. |
| `nano` | Opens a terminal-based text editor. |
| `visudo` | Safely edits the sudoers configuration. |

## Practical Applications in Cybersecurity

Understanding fundamental Linux commands is essential for system administration, security assessments, and ethical hacking.

These skills are useful for:

- Navigating Linux filesystems during system investigations.
- Understanding important system configuration files.
- Managing user accounts and group memberships.
- Reviewing administrative privileges.
- Installing and maintaining security tools.
- Understanding Linux access control.
- Editing configuration files and scripts.
- Identifying potential privilege and permission misconfigurations.

## Screenshots / Evidence

The following screenshots are recommended to document the practical work.

Save the actual screenshots in a folder named `screenshots/` in the repository.

1. **`01-linux-directories.png`** — Terminal showing navigation to `/` and exploration of important Linux directories.
2. **`02-user-management.png`** — Terminal showing the user and group management commands.
3. **`03-group-membership.png`** — Terminal showing the command used to add a user to the `sudo` group.
4. **`04-apt-package-installation.png`** — Terminal showing the APT package installation process.
5. **`05-sudo-privileges.png`** — Terminal showing an administrative command executed using `sudo`.
6. **`06-nano-text-editor.png`** — Nano interface displaying `md5sums.txt`.

*Note: Add screenshots only after capturing the corresponding practical work. Do not present suggested evidence as completed results.*

## Conclusion

This lab introduces essential Linux administration concepts and commands.

Understanding Linux directories, user and group management, package installation, privilege management, and text editing provides a foundation for more advanced Linux system administration and cybersecurity activities.
