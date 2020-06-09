Linux for Developers
=====================

by The Linux Foundation

# Week 2

#### Title: Text Editors

### Introduction to Text Editos

* Types of editors available
	1. vi - standard editor available on all UNIX-like systems
	1. vim-enhanced - same as vi but with many enhancements
	1. vim-X11 - vi with full graphical support
	1. emacs - standard editor available on all UNIX-like systems
	1. xemacs - varient of emacs, preferred by some
	1. nano - small and easy to use
	1. gedit - graphical editor part of GNOME desktop
	1. KWrite - graphical editor part of KDE desktop
	1. kate - graphical editor part of KDE desktop
	1. nedit - simple graphical editor

* vi and emacs
	1. They are always available on every Linux installation, though one will often not find emacs in a default installation
	1. vi and emacs, have a pure text-based form that runs perfectly well in a non-graphical environment
	1. They also have X-based graphical forms that would extend their capabilities

* nano
	1. Very easy to use and simple

* gedit and KWrite
	1. Both are easy to begin with, extremely capable and configurable

### vi Editor

* vi is short for view
* The actual name of the program was probably vim, to which vi has been the alias to as its substitute name
* vi --> pronounced as vee-eye
* There are two fundamental modes, and you toggle between each with the escape key
	1. command mode
	1. insert mode

* Both GNOME and KDE offer graphical interfaces for the vi text editor. 
* GNOME offers gvim, while KDE offers kvim.
* Online Tutorial : https://www.openvim.com/

### emacs Editor

* Emacs is available on all Linux systems, occasionally it's not installed by default
* It's one of the very first open source software projects, originally written by Richard Stallman who founded the Free Software Foundation, which gave rise to the new project
* Emacs has almost an infinite variety of capabilities beyond text editing, such as 
	1. email
	1. debugging
	1. constitutes a complete integrated development environment, etc
* There's only one mode in emacs, unlike the two modes in vi
* In order to do special control functions and issue commands relevant to the editor, you use either the ***Control (Ctrl) key*** or the ***META key***
* For the ***META key***, you can easily use either ***ALT*** or ***Escape*** in combination with other keys


#### Title: Shells, Bash, and the Command Line

### Shell

1. The `#!/bin/bash` at the beginning of the script should be familiar to anyone who has developed any kind of script in UNIX environments
1. Following the magic `#!` characters goes the name of whatever scripting language interpreter is tasked with executing the following lines
1. Choices include 
	1. `/usr/bin/perl`
	1. `/bin/bash`
	1. `/bin/csh`
	1. `/usr/bin/python`
	1. `/bin/sh`
1. Linux provides a wide choice of shells; exactly what is available to use is listed in /etc/shells; e.g. on one system we get:
	```bash
	$ cat /etc/shells
	/bin/sh
	/bin/bash
	/sbin/nologin
	/bin/tcsh
	/bin/csh
	/bin/ksh
	/bin/zsh
	```


### The Development Shells (History)

* We're going to briefly cover the history of the development of basic shell interpreters, as they're used at the command line in Linux and other operating systems
* Most Linux users will use bash as their default command line shell


* Shells and Their History 
	* ***sh, or shell***, was written by Steve Bourne at AT&T back in 1977.Therefore, it's called the Bourne Shell
		- Every other shell has descended from it in some fashion
	* ***C shell*** was written by Bill Joy at UC Berkeley, right after sh was started
		- It looks quite a bit different than sh, but its syntax is much more like the ***C programming language***, and that's where the name comes from
	* ***tcsh*** - Various enhancements to C shell were incorporated some years later in tcsh
		- It's not important exactly where the name comes from, but on most modern systems, csh just links to the actual program tcsh
	* ***ksh*** was written by David Korn, and hence the name
		- It dates back to 1982. It's pretty compatible with sh, but has a lot of new features
		- A lot of system administrators have always liked using ksh
	* ***Bash*** was written five years later as a project of the GNU project. It stands for ***B***ourne ***A***gain ***SH***ell. And it's a major upgrade of sh, and incorporated many ideas that are also appear in ***ksh***
	* A much more recent one, well, just three years more recent, is ***Z shell***
		- Named after a professor at Princeton University, Zhong Shao, who used it as his login name
		- It has extended features, but it's not in as wide use


* If you really want maximum portability you shouldn't use features which are only understood by bash
	- but virtually all systems today are running bash instead of sh. So there's really no need to do that on any UNIX system.
* It's pretty easy to port scripts between ***sh***, ***ksh***, and ***bash***
* Porting scripts from ***csh*** variants is complicated because of its quite different syntax. On the other hand, porting scripts between ***sh, ksh and bash*** is relatively easy and straightforward.


#### Title: Filesystem Layout, Partitions, Paths, and Links

### Filesystems : Introduction

> The **Filesystem Hierarchy Standard (FHS)** was initially administered by the **Free Standards Group**, and now is administered by **The Linux Foundation**

* According to the UNIX tradition, there is a root filesystem which starts at the slash (/) directory, and all filesystems or partitions can be found in a tree descending from there
* Other partitions, whether they're on the local machine or somewhere on the network, are mounted at various subdirectory points under that root filesystem
* The Linux Foundation administers the **Filesystem Hierarchy Standard**, the **FHS**, which specifies what the main directory should be, and what their purposes are.
* Most Linux distributions try to respect the FHS, but none of them follow it exactly


### Partitioning Considerations

> For the most basic **commonly used Partitioning Scheme**, you would have: **3 Partitions**: `/boot`, `/`, and `swap`.

* A very common simple scheme is to have 3 partitions, 
	1. **`/boot`**
		* is small, just holds kernels and initial ram disk, some configuration files, the GRUB directories
		* Contents do not change very often and you really don't want them corrupted, so keeping them on a separate partition often makes sense
	1. **`/`**
		* contains everything else on your system, all your user files, system files, applications, configuration development tools, etc., would be there
		* It's generally good to have a separate swap partition that's at least as big as the amount of memory on your system, which is convenient to use if you're running short on memory
	1. **`swap`**
		* swap partition should be at least as big as the amount of memory on your system
		* You can use swap files instead of partitions, but this is a weaker method due to both efficiency and stability considerations
		* It seems to be default on the most recent Ubuntu systems.
		* If you really want a simple setup, you just not have a separate partition for `/boot`, just have it to `/` and swap

* Other ways to set up partitions and especially if you have a multiple user system, it makes more sense to use these more complicated setups
	1. You might put the **home directory** or **user accounts** on a separate partition.
	1. You might put **`/user`** on a separate partition because it's pretty static, it doesn't change very much, but `/var` and `/tmp` are pretty volatile, and the `/tmp` partition is very temporary, so you may want to have that in a world of its own
	1. Using **Network Filesystems**, **NFS**, and might not even be available untill the system is fully running
	1. If we use **LVM**, **Logical Volume Manager**, which we also will discuss, you have even more flexibility because you can have your partition set up in a way that is rather distinct from the way the physical volume is set up
		* It's more flexible, it's easier to resize partitions, get rid of them and do other things with them later than when you have true physical partitions


