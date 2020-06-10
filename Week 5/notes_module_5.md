Linux for Developers
=====================

by The Linux Foundation

# Week 5

#### Title: System Administration

### System Installation

> You must have free disk space or unpartitioned disk space, on your hardware to create a multi-boot system
#
> You can test what a distribution looks like using live media, without installing anything on your hardware.
#
> Most Linux distributions make available more than one graphical interface option

* What are some installation methods you can use for Linux?
	1. Network-based installation
		* You can install completely over the network if you have TFTP set up
	1. Use live media (CD, DVD, USB stick, etc)
		* performance is poor
	1. Install Linux directly on your machine from the network, CD, DVD, USB, etc
* Nothing much to write for this section. Check Slide Notes for instructions.

### Using Yast

> On SUSE systems, YAST is your basic interface for all system administration. 

* Graphical tools for package management on **openSUSE** with the **GNOME interface**
	* The basic tool for doing this is called **YaST**, **Y-A-S-T**, which stands for **Y**et **A**nother **S**etup **T**ool, and it's available in all **SUSE-based** systems
* Nothing much to write for this section. Check Slide Notes for instructions.

### RPM

> rpm is a low-level command designed for individual packages listed on the command line or for groups of packages listed on the command line. It does not by itself solve package dependency issues.

* Nothing much to write for this section. Check Slide Notes for instructions.

### dpkg : debian systems

> `dpkg --listfiles` displays the files in a package

* Nothing much to write for this section. Check Slide Notes for instructions.

### Using yum and dnf

> Linux distributions include graphical interfaces for package management. For example, yumex on Red Hat-based systems.
#
> EPEL stands for Extra packages for Enterprise Linu

* Nothing much to write for this section. Check Slide Notes for instructions.

### Logging Files

* System log files are essential for monitoring and troubleshooting. In Linux, these messages appear in various files under **/var/log**
* Ultimate control of how messages are dealt with is controlled by the **syslogd** daemon (usually **rsyslogd** on modern systems) common to many UNIX-like operating systems. The newer systemd-based systems can use **journalctl** instead, but usually retain **syslogd** and cooperate with it.
* Important messages are sent not only to the logging files, but also to the system console window; if you are not running X or are at a virtual terminal, you will see them directly there as well. In addition, these messages will be copied to **/var/log/messages** (or to **/var/log/syslog** on Ubuntu), but if you are running X, you have to take some steps to view them.
* A good way to see them is to open a terminal window, and in that window, type **`tail -f /var/log/messages`**. On a GNOME desktop, you can also access the messages by clicking on **System > Administration > System Log** or **Applications > System Tools > Log File Viewer** in your Desktop menus, and other desktops have similar links you can locate.
* In order to keep log files from growing without bound, the **logrotate** program is run periodically and keeps four previous copies (by default) of the log files (optionally compressed) and is controlled by **/etc/logrotate.conf**
* Here are some of the important log files found under **/var/log**
	* **boot.log** --> System boot messages
	* **dmesg** --> Kernel messages saved after boot. To see the current contents of the kernel message buffer, type dmesg
	* **messages** or **syslog** --> All important system messages
	* **secure** --> Security related messages


#### Title: Users and Groups

### Basics of Users and Groups

> The first non-root user when the system is installed will be 1000
#
> When creating a new account with useradd, not all distributions will create a home directory by default. For example, Ubuntu and openSUSE do not create a home directory by default.

* Every Linux user, every user on the system is assigned a unique user ID, which is really just an integer, and you also get a group ID
* All modern Linux systems store normal users with an ID of 1,000 and they go up from there
	* the first user when the system is installed will be 1,000, the next user it's added it will be 1001, et c
* Very old Linux systems from Red Hat started with 500, but now everybody uses 1,000
* User IDs of less than a 1,000 are certain system users which have special purposes
* the superuser root has a user id of 0
* There is very important files on the system in the /etc/ directory
	1. /passwd --> /etc/passwd
		* This has a series of lines, each of which identifies a different user, each of which identifies a different user
		* (george:x:1000:1000:George Metesky:/home/george:/bin/bash)
			* Account Name: george
				* the name of the user on the system, which should not contain capital letters
			* Password: (x)
				* this can be a encrypted password, an asterisk, or an x depending on how security is set up on the system
			* User ID: 1000
				* the numerical value for User ID
			* Group ID: 1000
				* the numerical value for primary Group ID
			* Full User Name: George Metesky
				* this field can be used for other purposes, but is almost always used for full username
			* Directory: /home/george
				* User's home directory
			* Shell: /bin/bash
				* The user's default shell, which is the program run when logging in; if you see a **/sbin/nologin** or any non-executable program, this means user cannot directly login
	1. /group --> /etc/group
		* Groups of users who share some common interests. Maybe they're working on a project together, or they are all students, or they are all faculty, or are all in the some department, and they want to share some resources, typically files
		* for any user, there's at least one group that is just their own, and has... The group ID is the same as the user ID

