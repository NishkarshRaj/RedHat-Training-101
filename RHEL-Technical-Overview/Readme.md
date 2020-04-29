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

## File System Hierarchy

* Tree structure with root at the root 
```
ls /
```

* **bin:** executable for all users

* **sbin:** executable for root

**BCD!!!** ```$ ls -l /``` shows both bin and sbin are symbolic links to **usr/bin** and **usr/sbin** respectively.

* **usr** - actual binaries
**Example** - usr/bin/ls , usr/sbin/ip

**Where is the command/file** ```$ whereis [filename]```

* **boot/** - kernel is stored on boot directory. Bootloader is also there

* **etc/** - Extended Text Configurations

* **dev** - dev

* **home** 

* **/root** - home of root

* **tmp** - temporary space

* **/var** - variable space - spool data, logging data, temporary space, caches etc.

**BCD!!! /temp versus /var/tmp - purges - auto deletes 10 and 30 days respectively**

## Editing files using ViM - Text Editor

```
$ vim # vi improved in default command mode
```

* **Extended Command mode** - Use colon!!
* **:write [filename]** # For creation on first time

```
$ vim [file name]
```

### Command mode

** yy - copy line
** p - paste copied line
** 10p - paste copied line 10 times
** dd - delete line
** 9dd - delete next 9 lines
** o - insert mode at EOF new line - append mode
** ZZ - save and quit (without going into extended mode)
** :q! - Quit without saving 

```
$ vimtutor # learn more about vim editor
```

## Organizing Users and Groups

* Users always belong to one primary group by default - Same name as username
* Create users
```
$ user # shows multiple user related commands 
```

```
$ useradd [username]
```

* Information about user

```
$ id [username] #uid, gid (primary user with same name as username), supplementary groups
```

* Create a group

```
$ group
```

```
$ groupad [group name]
```

* Add user to supplementary group
```
$ usermod -aG [groupname] [username] # Append to Group list
```

```
$ id [user name]
```

* Add password to the user
```
$ passwd [username] # if username not passed we change password of current user
```

* Delete user
```
$ userdel [user name] # Does not delete user files and home directory
```

* Delete group
```
$ groupdel [group name]
```

* User configuration files in **etc/passwd** - Not password but all configuration files
```
$ grep [username] /etc/passwd
```

* See password
```
$ grep [username] /etc/shadow # shows encrypted password # Cannot see password of other users
```

* See group details
```
$ grep [group name] /etc/group
```

* Run a command on other user interface without switching using su
```
$ sudo -u [username] [command]
```

* Switch to root
```
$ su -
```

* Return to parent terminal
```
$ exit
```

## File Permissions

* Three types of permission 
1. Read
2. Write
3. Execute

* Every file has 10 bits for its description. **Check this by** `$ ls -l [filename]`
* First bit is file type -,d,l,b etc.
* Next 9 bits are grouped into 3 for permissions rwx
* User, Primary Group, and Other are the three groups

```$ ls -l [file]```
Shows the 10 bits followed by user owner and its primary group.

* To check which group the user belongs to, use ```$ groups [username]```

**Changing File Permission - chmod command**

* `$ chmod [u/g/o][+/-][r/w/x] [file]` 

* **Ownership - Can be user level or grouped level**

```$ chown [group1]:[group2] [file]```

## Managing Software - Introduction to RPM

**RPM:** RedHat Package Manager - archive of dependencies and packages to be installed

* RPM Software - apart from package manager, files are also present - **.rpm extension**
* Open source vendors might be risky to use - always use trusted vendors like RedHat.

* Subscription Manager is used for RedHat repository
```$ subscription-manager register```

```$ subscription-manager attach```

```$ subscription-manager repos --disable='=' --enable=[repo name]``` # Disable all repos

```$ subscription-manager repos --list```

* Deploy Satellite server common to all the devices in the organization - download only once and use for all - common repository to update and deploy to all. 
* Satellite server are basically local central caching for common versioning to all devices in the organization
* The server can store the packages in local web server which has to be configured with all devices

* Check list of repositories connected with device
```$ yum repolist all```

```$ subscription-manager status```

* Check the details of connected to repositories
```$ ls -l /etc/yum.repos.d```

* Check if package is installed or not
```$ yum info [package name]```

* Install package
```$ yum install [-y] [package name]```

* Update package
```$ yum update [package name]```

* Update all packages
```$ yum update```

* Remove software
```$ yum remove [package name]``` # Removes package and all the packages that were dependent on it
**Note: Never pass -y command to auto delete! Always check dependency**

## Configuring Network - Network Manager service
* Provides GUI and CLI (NMCLI)

```$ nmcli [double tab for options]```

* Show connections
```$ nmcli connection show```
* **UUID** - Universally Unique ID	

* Show detailed properties of connections
```$ nmcli connection show [connection name]```

* Show connections in current device
```
$ nmcli device show
```

* Create own connection profile
```
$ nmcli con add con-name [connection name] type [connection type] ifname [Interface name]
```
**Example:** `$ nmcli con add con-name static-connection type ethernet ifname enp1s0`

```$ nmcli con show```
* Green color for active connection ```$ nmcli con show --active```

* Modify Connection property
```$ nmcli con mod [name] [property] [value]

```$ nmcli con mod static-connection ipv4.addresses 10.0.0.1/24```

```$ nmcli con mod static-connection ipv4.gateway 10.0.0.254```

```$ nmcli con mod static-connection ipv4.dns 10.0.0.254```

* Active profile as current profile
```$ nmcli con up [connection name]```

* Delete profile
```$ nmcli con delete [connection name]```

**Note: Mod overwrites on default, we can append using +**
```$ nmcli con mod static-connection ipv4.addresses 10.0.0.1/24``` # overwrites old value
```$ nmcli con mod static-connection ipv4.addresses 10.0.0.2/24``` # Adds second value

* Check IP Address for Interface
```$ ip a s enp1s0``` # a for address and s for show

* Up command can be used to refresh the profile if already up

* All configurations of the network profiles are stored in **/etc/resolv.conf**

## Controlling System Startup Processes - Systemd Service

**Interface systemd with systemctl command**

* Service units to manage with Systemctl command - each unit has its own configuration file

* List the different unit configuration file
```$ systemctl list-unit-files```
Shows unit file with their current state - static/enabled/disabled

* Display units of specific type
```$ systemctl list-unit --type=service```

* Check status of specific unit
```$ systemctl status [unit name]```

* All units are initialized when system boots up.

* Restart the unit
```$ systemctl restart [unit name]``` # Process ID changes - stops and starts freshly

* Reload the unit
```$ systemctl reload [unit name]``` # Process Id does not change - does not stop, justs refresh - synchronize changes in memory

* Start a service
```$ systemctl start [service]```

* Enable a service
```$ systemctl enable [service]``` # Enable means that always load in memory when system boots up

## Introduction to Containers
* Isolation
* Portability
* Lightweight wrt virtual machine - shares kernel of parent.
* Multiple containers can co-exist in the same machine
* One container only has its required libraries
* Change in library in one container does not break another - isolation
* **Tools** - buildah, spokeo
* RedHat container registry - RedHat Container Catalog
```$ yum module install container```

## Introduction to Cockpit - Web Interface to RHEL Monitoring
* Start Cockpit
```$ systemctl enable --now cockpit.socket``` # Runs on TCP Port 9090

* Add valid certificates and get domain ID and password

* GUI support for user creation on left sidebar.

* Network manager on left sidebar - alternate to NMCLI
- Check data rate for sending and receiving data.

* Log Monitoring - Sidebar - See everything

* Software Update manager

* Terminal for administration via Cockpit

* Service - Systemctl service administrator

## Summary
* Developer Subscription - developers.redhat.com
* Products - access.redhat.com - Knowledge blogs as well
* RedHat Learning Subscription - learn.redhat.com