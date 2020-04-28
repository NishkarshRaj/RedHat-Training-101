# RedHat Enterprise Linux Technical Overview

## What is Linux, Open Source Software, and a Distribution?

**Open Source** - licensed - source code is open for community to read and update via a request.
- May or may not be free to use.
- Anyone can contribute.
- Community support

- Open Source projects can lead to better properietary project
**Example:** RedHat maintains opensource Linux Fedora distribution and the major changes lead to updated in the closed source RHEL.

**Distribution:** Here, combination of Linux kernel and softwares and dependencies, package management system, Interface etc. that are packaged and distributed under an open source license.

## Introduction to the Shell

**Shell:** Interface between kernel and user
RHEL uses Bash shell but users can switch shell.

**Prompt:** $ for normal users and # for root (administrative) user.

**Man pages:** To learn about any command

```
$ man [command name]
```

**Note:** `command name [argument]...` means that argument can be space separated and within square means they are optional

**Example:** ls command

```
$ ls 
```

```
$ ls -a
```

```
$ ls -all # combination of options
```

versus

```
$ ls --all # one keyword
```

**BCD!!** We can exit man page by pressing **Q**

### Connect to remote shell

```
$ ssh [device name]@[server name]
```

## Kernel and User Spaces

**Kernel:** Heart of Opearating System maintaining scheduling, processing, security etc.

**User Spaces:** High level user applications that users use by communicating with the kernel via interrupts and system calls.

**Process**
* State
* User
* Group
* Process ID (PID)
* Unique resources and user space

**Types of processes**

**1. Background process:** Cannot take input from terminal but gives output to the terminal.

**2. Daemon process:** Background processes that do not have anything to do with the terminal but are important for network and security mechanisms.

**3. Kernel Threads:** 

**PS command** - `$ ps`

* Information regarding running process
* pts - pseudo terminal session
* TTY - TellyType or Terminal

```
$ ps -ef
```

* e - all processes
* f - detailed information - PPID, Commands

**Note:**
* TTY - ? => Daemon process
* Commands in square brackets => Kernel threads

## Orientation to the Grapical User Interface - GNOME 3 Desktop Environment

* Activities at top left
* All activities and search bar within the Activity
* Drag and Drop activities on favorites
* Re-order the favorite bar on left sidebar
* Setup notifications - Access calender on center

### Workspaces

* Workspaces - Multiple Workspaces! (ALT+TAB for Windows)
* We can see multiple things opened together by clicking on Activities - Workspaces can be configured by dragging a process on right sidebar into an empty workspace.
* Different Logics must have unique workspace for good organization
* Switch workspace - **CTRL + ALT + Up/Down key**

## File Management in Linux
* Everything on Linux is a file

```
$ ls
```
* Different files have different color schemes

```
$ ls -l # long listing
```

**Types of file**
1. Normal file (extensions don't matter)
2. Directories
3. Linked files
4. block files (ls -l /dev/vda)

**How to check file type**

```
$ file [file name]
```

**Note:** File names are case sensitive

**Note:** Files are stored as tree

```
$ tree [dir]
```

### How to create linked files

```
$ ln [link to file] [linked file] # Hard link - file only # ls -l has file count = 2
```

```
$ ln -s [link to file] [linked file] # Soft links or Symbolic links - files and directories # ls -l starts with l
```

