Linux for Developers
=====================

by The Linux Foundation

# Week 4

#### Title: System Monitoring

### System Monitoring : Overview

* There are many command-line utilities used in Linux routinely to monitor the system's performance.
* There are straightforward everyday utilities, such as **top**, which lets you manage CPU usage and see what processes are taking up the most resources on your system
* Two well-known ones that ship on every system are
	* GNOME System Monitoring
	* ksysguard
	* then there are other alternative and more robust methods, which are available from Linux distributions with a graphical interface
#
* How the kernel handles so-called kernel modules, and how it manages devices?
	* One of the strengths of the Linux kernel is that you can add things at runtime and remove them when you no longer need it. These are called **Kernel Modules**
	* A kernel module might have to be added to enable a new device that's added to the system, that maybe is plugged into a USB port
		* for example, or it might be something like a new network protocol that isn't actually running right now, but the capability is there if you load a module

#
* How device management goes, it's pretty complicated to make sure that when a device is added to the system or found at boot, that it's handled properly?
	* Linux uses something called **udev**, or **user device** as a facility in order to enable this
#
* Basic Commands and Utilities
	* Many basic commands and utilities are the same in Linux and other UNIX-like operating systems
	* While there may be some variation in some of the options and syntax, the purpose remains the same
	* Here are lists of these commands grouped by general area of coverage
		* File Compression
			* **bunzip2, bzcat, bdiff, bzip2, bzless**
			* **gunzip, gzexe, gzip, zcat, zless**
			* **zip, upzip**
			* **xz, unxz, xzcat**
		* File Ownership, Permissions and Attributes
			* **attr, chgrp, chown, chmod**
		* Files
			* **awk, basename, cat, col, cp, cpio, csplit, cut, dd, diff, dirname, egrep, expand, file, fgrep, fmt, grep, head, join, less, more, sed, tail, tar**
		* Filesystem
			* **cd, chroot, df, dirs, du, fdisk, fsck, fuser, ln, ls, mkdir, mv, pushd, popd, rm, rmdir**
		* Networking
			* **arp, domainname, finger, ftp, host, hostname, ip, route, ifconfig, netstat**
		* Job Control
			* **at, atrm, batch, crontab, exec, exit, ipcs, ipcrm, kill, killall**
		* Expression Evaluation
			* **bc, dc, eval, expr, factor, false, true**


### File Transfer Tools

> FileZilla provides a great graphical client, but it is not the dominant ftp server used on Linux. On Linux, vsftpd is the dominant ftp server used.

* FTP client abound, from the familiar command line ftp and enhanced (or dumbed down depending on your point of view) version such as **ftp**, **ncftp**, and **qftp**
	* You can use well-known graphical clients, like **FileZilla**
	* You can just use your browser, because FTP downloading capability at least is built into any browser that you might be using.
	* The dominant ftp server in use of Linux systems is **vsftp**, which is both simple and highly configurable
* Somewhat more general transfer opportunities are provided by both **curl** and **wget** and their associates, 
	* They can handle protocols such as **ftp**, **http**, etc.
* **ftp** is kind of deprecated now, it's actually **not used** by some **major projects** such as the Linux kernel
	* It's considered relatively insecure
* Alternatives of ftp
	* Secure shell clients and servers, **ssh** for instance, built on the OpenSSH implementation, and they include programs, like
		* **scp** for secure copy
		* **sftp** for secure ftp
	* **rsync** has server and client utilities, and they enable very rapid file transfer and synchronization between remote computers
	* There are some very old fashioned insecure programs you should never use such as **rsh** and **rcp**
#
* Monitoring and Performance Utilities
	* Process and Load Monitoring Utilities
		* **top** --> Process activity, dynamically updated
		* **uptime** --> How long the system is running and the average load
		* **ps** --> Detailed information about processes
		* **pstree** --> A tree of processes and their connections
		* **mpstat** --> Multiple processor usage
		* **iostat** --> CPU utilization and I/O statistics
		* **sar** --> Display and collect information about system activity
		* **numastat** --> Information about NUMA (Non-Uniform Memory Architecture)
		* **strace** --> Information about all system calls a process makes
	* Memory Monitoring Utilities
		* **free** --> Brief summary of memory usage
		* **vmstat** --> Detailed virtual memory statistics and block I/O, dynamically updated
		* **pmap** --> Process memory map
	* I/O Monitoring Utilities
		* **iostat** --> CPU utilization and I/O statistics
		* **iotop** --> I/O statistics including per process
		* **sar** --> Display and collect information about system activity
		* **vmstat** --> Detailed virtual memory statistics and block I/O, dynamically updated
	* Network Monitoring Utilities
		* **netstat** --> Detailed networking statistics
		* **iptraf** --> Gather information on network interfaces
		* **tcpdump** --> Detailed analysis of network packets and traffic
		* **wireshark** --> Detailed network traffic analysis

### Graphical Monitoring Tools

> **gnome-system-monitor** is a graphical monitoring tool installed on any Linux distribution that provides the GNOME desktop. It generates statistics in real time, but you don't have the ability to save the data
#
> **ksysguard** is another graphical monitoring tool, which has far more extensive capabilities than gnome-system-monitor

* Graphical monitoring tools
	* **gnome-system-monitor** comes with the GNOME desktop
		* All statistics are generated in real time
		* It's easy to examine things like CPU load, how much memory and swap you're using, network bytes, etc
		* But there are no ability to save data and you have a very limited choice to display items
#
* KDE has a more powerful similar utility called **ksysguard**
	* It's far more configurable, you can choose what sensors or monitors you want to display
	* You can have a lot of different windows available at once
	* You can show remote systems at the same time
	* You can save what you're doing, etc

#
#### Title: Kernel Modules and Device Management

### Loading/Unloading Kernel Modules

> **lsmod** tells only about currently loaded modules

* Many facilities in the Linux kernel can either be built-in to the kernel when it is initially loaded, or dynamically added (or removed) later as modules, upon need or demand. Indeed, all but some of the most central kernel components are designed to be modular.
* Such modules may or may not be device drivers; for example, they may implement a certain network protocol or filesystem. Even in cases where the functionality will virtually always be needed, incorporation of the ability to load and unload as a module facilitates development, as kernel reboots are not required to test changes.
* Even with the widespread usage of kernel modules, Linux retains a monolithic kernel architecture, rather than a microkernel one. This is because once a module is loaded, it becomes a fully functional part of the kernel, with few restrictions. It communicates with all kernel sub-systems primarily through shared resources, such as memory and locks, rather than through message passing as might a microkernel.
* Linux is hardly the only operating system to use modules; certainly Solaris does it, as well as does AIX, which terms them kernel extensions. However, Linux uses them in a particularly robust fashion.
* Module loading and unloading must be done as the root user. If you know the full path name, you can always load the module directly with:
	* Syntax
		* `sudo /sbin/insmod <pathto>/module_name.ko`
	* A kernel module always has a file extension of **.ko**, as in **e1000e.ko**, **ext4.ko**, or **nouveau.ko**
* While the module is loaded, you can always see its status with the **lsmod** command
* Direct removal can always be done with:
	* Syntax
		* `sudo /sbin/rmmod module_name`
	* Note that it is not necessary to supply the full path name or the .ko extension when removing a module.
* In most circumstances, the **insmod** and **rmmod** commands are not usually used to load/unload modules, but rather the **modprobe** command is
	* Syntax
		```bash
		sudo /sbin/modprobe module_name
		sudo /sbin/modprobe -r module_name
		```
	* For modprobe to work, the modules must be installed in the proper location, generally under **`/lib/modules/$(uname -r)`** where **`$(uname -r)`** gives the current kernel version, such as 4.18.3
	* You can also pass parameters to modprobe in the exact same fashion as you do with insmod, as in
		* Syntax
			* `sudo /sbin/modprobe module_name.ko irq=12 debug=3`
* The modinfo command can be used to find out information about kernel modules, whether they are loaded or not, as in
	* Syntax
		```bash
		/sbin/modinfo my_module
		/sbin/modinfo <pathto>/my_module.ko
		```

#
* There are some important things to keep in mind when loading and unloading modules:
	* It is impossible to unload a module that is being used by another module, which can be seen from the **lsmod** listing.
	* It is impossible to unload a module that is being used by one or more processes, which can also be seen from the **lsmod** listing. However, there are modules which do not always keep track of this reference count, such as network device driver modules, as it would make it too difficult to temporarily replace a module without shutting down and restarting much of the whole network stack.
	* When a module is loaded with **modprobe**, the system will automatically load any other modules that are required to be loaded first.
	* When a module is unloaded with **modprobe -r**, the system will automatically unload any other modules being used by the module, if they are not being simultaneously used by any other loaded modules.
	* Files in the **/etc/modprobe.d** directory control some parameters that come into play when loading with **modprobe**. These parameters include module name aliases and automatically supplied options. This directory also contains information about blacklisted modules, which should never be located and loaded.


### Device Management

* There are three main types of devices which will probably be connected to your system,
	1. Character
		* Character devices are sequential streams; they take byte streams of data, they mainly implement open, close, read, and write functions
		* It could be a serial port, a parallel port, a printer, for instance, sound cards, et c
	1. Block
		* Block devices are what we usually think of as storage devices, and they only take data in block-size multiples
		* /O operations are generally cached and there may be some delay before they're actually accomplished, we reference the disk, and so there are things like CD-ROMs, hard disks, etc
	1. Network
		* They transfer actually packets of data, not blocks or streams. So, they're quite different
		* Even though these packets of data may go out in the stream and be reassembled into blocks
		* Internally, there's a so-called socket interface, and you have reception and transmission functions, instead of read and write functions
		* They're known by name, such as eth0, perhaps, for the first Ethernet card, and wlan0 for the first wireless card
#
* The user-space driver, which is not a component of the Linux kernel, would work completely in user-space
	* For example, Linux printer drivers are always done this way
* Character and block devices have something known as a device node, which is how the system interfaces with them by doing input or output operations than device nodes
* We make these device nodes with the **mknod** command from the command line, and it's pretty straightforward
	* You give it a name for the device, and you say what type of device it is, and you give what's known as the major and the minor number
	* The major number distinguishes the type of device and the minor number is either the instance of that device or the way it's being used
* These **nodes** can be used by user-level programs to communicate with the device, using normal I/O system calls such as **open()**, **close()**, **read()**, and **write()**
* A device driver can manage more than one device node

#### /dev Directory

* Device nodes are normally placed in the /dev directory and can be created with
	* Syntax
		* `sudo mknod [-m mode] /dev/name <type> <major> <minor>`
	* **mknod()** system call can also be used
* The major number distinguishes the type of device
	* It identifies the driver associated with the device; all device nodes of the same type(block or character) with the same major number use the same driver
* The minor number is either the instance of that device or the way it's being used
	* It is used only by the device driver to differentiate between the different devices it may control


> Rules for device naming are located in the /etc/udev/rules.d directory
> Ideally, you would like to register devices with just their names. However, we cannot just get rid of major and minor numbers, as POSIX requires them.