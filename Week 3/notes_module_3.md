Linux for Developers
=====================

by The Linux Foundation

# Week 3

#### Title: System Initialization

### System Boot

#### GRUB

> **GRUB has two versions: GRUB 1 on older systems, and GRUB 2 on newer systems.**
#
> **Current GRUB Version is `GRUB 2`**
#
> What is the proper order of system initialization stages on most x86-based systems?
> **BIOS --> GRUB --> init (PID 1)**


* All x86-based physical Linux systems, that includes laptops, most workstations, et cetera, use a software system called **GRUB**, which stands for **GR**and **U**nified **B**ootloader, that handles the earliest phases of the system startup
* This is not true when you get to embedded devices, such as set-top boxes, medical devices et cetera
	- They use other platforms, such as **Das U-Boot** in order to start 
* GRUB has a number of important features, you can boot into alternative operating systems, make your choice at boot time. This is called a **Bootloader**
* Given operating system, 
	* You can make choices as to which kernel you want to start with
	* You can use different initial ramdisk
	* You can specify different options that the system should start with
* In GRUB 2, there's really only one configuration file in the boot directory that counts and that's called **grub.cfg**
	* Exactly where it is will depend a little on your kind of system, both in terms of your distribution and your hardware, but it will be there someplace
	* Generally, this is not a file you edit by hand, it's a file that's generated for you when you are configuring the system, or installing a new kernel, or compiling a new kernel, etc
* Other directories on our system that matter
	* Under **`/etc/grub.d`** (this file can be edited), there's a number of files that control how GRUB works
	* Under **`/etc/default`** (this file can be edited), there's a file named **grub**, which contains basic parameters that GRUB needs
	* These files ( **`/etc/grub.d`** , **`/etc/default`** ) can be edited by hand and they're used to generate **grub.cfg**

```
1. Some of the most important features of GRUB are:
	* You can boot into alternative operating systems. You can make this choice at boot time.
	* Within a given operating system, you can choose which kernel you want to start with.
	* You can use different initial ramdisk.
	* You can specify different options that the system should start with.
	* You can change boot parameters at boot time, without needing to change configuration files on the machine.
```

#### BOOT

* When the system boots, it begins with the so-called **BIOS** space, basic input-output system, or CMOS, identifying, initializing the most important system and attach peripheral devices, such as input like a keyboard and initial hard-disk, so that you can actually load the kernel
	* You can make choices in the BIOS about booting off a peripheral device, maybe a USB drive, for instance
* Older systems have what's called the **Master Boot Record**, that contains both the partition table and the bootloader, which is part of GRUB that loads the actual operating system
* The kernel itself can have different names, usually it's **vmlinuz**, and then appended with a version number
	* The **z** in **vmlinuz** indicates that the kernel is compressed, as it loads it decompresses itself.
#
### System Initialization

> The order in which the following system initialization methods were introduced
> **SysVinit -> Upstart -> systemd**


#### init

* The first program which runs on the system is called **init**
	* Generally, it has a **process ID of 1**, later processes have higher process IDs
	* Traditionally, this was considered the parent of everything that follows
		* Technically, that's not really true, some processes are started directly by the kernel, rather than being the children
* What **init** does?
	* It configures all aspects of the environment
	* It starts all the processes needed for logging into the system and keeping track of things
	* it also keeps track of what happens when something terminates to make sure it does it as cleanly as possible

#### SysVinit

* Historically, all distributions were based on what's called **System V init(SysVinit)** that goes back to early Unix days
* The basic idea was that you went through a sequence of steps as a system started up
* Each step required a completion of the earlier step, until you reached a fully operational step, probably with a complete graphical environment of its own workstation or laptop
* This scheme was developed decades ago	under rather different circumstances
	* The original target of course was multi-user mainframe systems, and not personal computers or laptops, or the other kinds of systems we have today
	* Target was a single processor system
	* One was not that concerned with how often a system was started and shut down, and how long it took was not that important
		* **`Startup`** was viewed as a serial process, divided into a series of sequential stages; each stage required completion before the next could proceed, so it did not easily take advantage of parallel processing that could be done on multiple processors or cores
		* **`Shutdown/reboot`** was seen as a relatively rare event and exactly how long it took was not considered important
	* It was more important just to get things right
#
#### New Methods of Controlling System Startup

* To deal with intrinsic limitations of SysVinit, new methods of controlling system startup were developed and have replaced it in all new systems.
* Two main schemes were adopted by Linux distributors:
	1. **Upstart**
		* Upstart was developed by Ubuntu and was first deployed in 2006, and this was an improvement over the earlier methods
		* Adopted in Fedora 9 and RHEL 6 and its clone, such as CentOS, Scientific Linux, and Oracle Linux
		* In openSUSE it was offered as an option since version 11.3
	1. **systemd**
		* Systemd is more recent. Fedora was the first major distribution to adopt it in 2011

> Both these methods ( **Upstart** and **systemd** ) take advantage of multiple CPUs and being able to do many things at onc
#
> The only important command there for day-to-day use is **systemctl**
#
> init is the first user-level process that runs on the system and continues to run until the system is shutdown.

* All major distributions have moved to Systemd
* Upstart is now considered obsolete and Systemd has been phased out in major distributions


#### System Runlevels

> **Runlevel 0** is reserved for the **System Halt State**

* In a SysVinit system, there are different runlevels that run from 0 to 6
* Normally a full graphical system is considered runlevel 5
* Runlevel 1 is single user mode or emergency mode, and it's for special purposes, where you have only one user there to repair a system for instance

#
#### Title: Memory

### Memory

1. Linux uses a virtual memory system (VM), as do all modern operating systems: the virtual memory is larger than the physical memory.
1. Each process has its own, protected address space. Addresses are virtual and must be translated to and from physical addresses by the kernel whenever a process needs to access memory.
1. The kernel itself also uses virtual addresses; however the translation can be as simple as an offset depending on the architecture and the type of memory being used.
1. The kernel allows fair shares of memory to be allocated to every running process, and coordinates when memory is shared among processes. In addition, mapping can be used to link a file directly to a process’s virtual address space. Furthermore, certain areas of memory can be be protected against writing and/or code execution.
1. The free utility gives a very terse report on free and used memory in your system
	* Syntax
		* `free -mt`
1. For more detailed memory information we can use command mentioned below
	* Syntax
		* `cat /proc/meminfo`
1. If we had only wanted to drop the page cache, we would have echoed a 1, not a 3; we have also dropped the dentry and inode caches, which is why the freed memory is more than that released from the page cache.


#### Swap

* Linux employs a virtual memory system in which the operating system can function as if it had more memory than it really does. This kind of memory overcommission functions in two ways
	* Many programs do not actually use all the memory they are given permission to use. Sometimes, this is because child processes inherit a copy of the parent’s memory regions utilizing a COW (Copy On Write) technique, in which the child only obtains a unique copy (on a page-by-page basis) when there is a change
	* When memory pressure becomes important, less active memory regions may be swapped out to disk, to be recalled only when needed again
* Such swapping is usually done to one or more dedicated partitions or files; Linux permits multiple swap areas, so the needs can be adjusted dynamically. Each area has a priority and lower priority areas are not used until higher priority areas are filled
* To see what your system is currently using for swap areas with
	* Syntax
		* `cat /proc/swaps`
* To see current usage of swap
	* Syntax
		* `free`
* The only commands involving swap are mkswap for formatting a swap file or partition, swapon for enabling one (or all) swap area, and swapoff for disabling one (or all) swap area
* Command to turn off all swap memory
	* Syntax
		* `sudo swapoff -a`
	* **swapon** turns on swap and **swapoff** turns off swap

### Threading Models

#### Processes and Threads

> Multiple threads in a process, they share this information. For instance, they all share the same memory
#
> A ***process*** is a running instance of a program and contains information such as environment variables and memory regions. A process can contain one or multiple threads
#
> Threads in a process have the same process ID and share the same environment, memory regions, etc.
#
> When the Linux kernel gets under extreme memory pressure, it invokes the dreaded **OOM** (**Out Of Memory**) Killer. This tries to select the **best** process to kill to help the system recover gracefully
#
> **Note:** You should be able to compile the program by just doing `gcc -o lab_wastemem lab_wastemem.c`

* A **process** is a running instance of a program and contains information about environment variables, file descriptors and current directory, etc
* It can contain one or more **threads**, each of which has the same process ID and shares the same environment, memory regions (except for stack), etc
* While Linux permits threads(or processes) creation through the low level **clone()** system call, the most usual method is to use **pthread_create()** which is a part of the standard **POSIX Thread (pthreads)** library
* There's additional information besides the actual executing program, such as 
	* environmental variables
	* attached memory regions
	* what the current directory and files that are being used are, etc
* If you have multiple threads in a process, they share this information
* Portable way is to use a so-called POSIX threads library or pthreads library
	* The idea here is you can write it once, and use it anywhere on any system which has a pthreads implementation
	* The ideal of write once, and use anywhere, and complete portability, is just an ideal
		* There are cases where a program written on Linux won't work on Solaris properly and vice versa
			* For instance, Solaris will tend to automatically initialize improperly uninitialized mutexes. Linux will not and you may get program crashes

#
#### Title: Networking

### Networking and Network Interfaces

* The vast majority of network programming in Linux is done using the socket interface. Thus, standards-compliant programs should require little massage to work properly with Linux.

> ***Note:*** however, there are many enhancements and new features in the Linux networking implementation, such as new kinds of address and protocol families.
***For example***, Linux offers the netlink interface, which permits opening up socket connections between kernel sub-systems and applications (or other kernel sub-systems). 
This has been effectively deployed to implement firewall and routing applications.

* Historically, the wired Ethernet network devices have been known by a name such as ***eth0***, ***eth1***, etc., while wireless devices have had names like ***wlan0***, ***wlan1***, etc
* Basic information about active network interfaces on your system is gathered through the ***`ifconfig`*** utility
* Information displayed includes information about the hardware **MAC address**, the **MTU (maximum transfer unit)**, and the **IRQ** the device is tied to. Also displayed are the number of packets and bytes transmitted, received, or resulting in errors.
* Note you can see the statistical information in abbreviated form by looking at ***`/proc/net/dev`***, and in one quantity per line display in ***`/sys/class/net/eth0/statistics`***


### Using Predictable Network Interface Device Names

> The **Predictable Network Interface Device Names** scheme is a modern approach to naming network devices, adopted by all recent Linux distributions. It is strongly correlated with the use of udev and integration of systemd.
#
> Networking configuration interface which is newer and has extended capabilities : `ip`
Older one is : `ifconfig`

* Simply naming network devices as **eth0**, **eth1**, etc. can be problematic when multiple interfaces exist, or when the order in which the system probes for and then finds them is not deteministic and can depend on kernel version and options
* Many system administrators have solved this problem in a simple manner, by hard-coding associations between hardware (MAC) addresses and device names in system configuration files and startup scripts
* A more modern approach is offered by the ***Predictable Network Interface Device Scheme***, which is strongly correlated with the use of udev and integration with systemd

#### Five Types of Names

* There are now 5 types of names that devices can be given
	* Incorporating Firmware or BIOS provided index numbers for on-board devices, e.g. **eno1**
	* Incorporating Firmware or BIOS provided PCI Express hotplug slot index numbers, e.g. **ens1**
	* Incorporating physical and/or geographical location of the hardware connection, e.g. **enp2s0**
	* Incorporating the MAC address, e.g. **enx7837d1ea46da**
	* Using old classic method, e.g. **eth0**
* On a machine with two onboard PCI network interfaces that would have been **eth0** and **eth1** in the older naming system
	```bash
	$ ifconfig | grep enp
	enp2s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
	enp4s2: flags=4099<UP,BROADCAST,MULTICAST> mtu 1500
	```
* It is easy to turn off the new scheme and go back to the classic names, if so desired


