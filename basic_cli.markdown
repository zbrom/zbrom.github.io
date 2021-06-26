---
layout: page
background: '/img/ghorr_banner.png'
title: Basic CLI
categories : dropdown
permalink: /arch/basic_cli/
---

Here you will find some basic useful command line interface (CLI) commands for Arch Linux.  Commands should apply to all Arch builds assuming you are using systemd.  For additional flags, please view the man pages of any of the following applications.
________________________________________________________________________________________________________________

#### *Package Management:*

##### Pacman:

    Update your system:
    
<code>pacman -Syu</code>

    Download a new package:
    
<code>pacman -S</code>
    
    Display information about a package:
    
<code>pacman -Si</code>
    
    Search for a locally installed package:
    
<code>pacman -Ss</code>

Yay (Download from the [Arch User Repository](https://aur.archlinux.org){:target="_blank"}):

    Update your system:

<code>yay -Syu</code>

    Download a new package:
    
<code>yay -S</code>

    Display information about a package:
    
<code>yay -Si</code>

##### Systemd Commands

Systemctl:

    Start a service:

<code>systemctl start [name of service].service</code>
    
    Stop a service:

<code>systemctl stop [name of service].service</code>
    
    Enable a service permanently:

<code>systemctl enable [name of service].service</code>
   
    Disable a service:

<code>systemctl disable [name of service].service</code>
    
    Check the status of a service:
    
<code>systemctl status [name of service].service</code>

#### *User Management*

Adding Users

Add users with:  useradd

<code>useradd -m -g [initial_group] -G [additional_groups] -s [login_shell] [username]</code>

    -m creates the user home directory as /home/[username]; within their home directory, a non-root user can write files, delete them, install programs, and so on.
    -g defines the group name or number of the user’s initial login group; the group name must exist; if a group number is provided, it must refer to an already existing group; if not specified, the behavior of useradd will depend on the USERGROUPS_ENAB variable contained in /etc/login.defs.
    -G introduces a list of supplementary groups which the user is also a member of; each group is separated from the next by a comma, with no intervening spaces; the default is for the user to belong only to the initial group.
    -s defines the path and filename of the user’s default login shell; Arch Linux init scripts use Bash; after the boot process is complete, the default login shell is the one specified here; ensure the chosen shell package is installed if choosing something other than Bash.

Change a password:

<code>passwd</code>

Remove a user:

<code>userdel -r [username]</code>

#### Group Management

Display group membership along with the user’s UID and associated GIDs:
    
<code>id [user]</code>

    List all groups on the system:

<code>cat /etc/group</code>

    Create a new group:
    
<code>groupadd [group]</code>

    Remove a group:

<code>groupdel [group]</code>
    
    Add a user to a group:

<code>gpasswd -a [user] [group]
    
    Remove a user from a group:

<code>gpasswd -d [user] [group]

