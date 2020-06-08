Linux for Developers
=====================

by The Linux Foundation

# Week 1

#### Title: Linux and the Operating System

### Kernel vs. Operating System and Tools

> ***Linux is only the kernel of the Operating System***

###### Kernel

* The work kernel is often sloppy applied to the entire operating system and environment on the computers which are equiped with complete linux distribution; but in fact, there are quite a few components which are necessary in order to have a fully functional platform.
* Narrowly defined, Linux is only the ***kernel*** of the operating system(OS)
	* The kernel is central component that connects the hardware to the software, and manages the system' resources, such as memory, CPU time sharing among competing applications and services
	* It handles all the devices that are connected to the computer by including so-called device drivers, and makes them available for the operating system to use
* As system running only a kernel has limited functionality, and the only place you will see that is in a dedicated device(often termed as ***embedded device***) such as inside an appliance.

###### Operating System

- In order to do something useful and to be able to do variety of things as needs arise, you need some other components, which in and of themselves are not strictly part of Linux:
	* Important System Libraries
		* Usually these are ***shared libraries*** or ***dynamic linked libraries***
		* They can be used simultaneously by more than one program
		* The most important one is ***libc***, which is used by virtually every application (among other things it handles the communication between the applications and kernel)
	* Important System Devices (sometimes called ***daemons***) --> All sorts of system services or applications that often run in the background waiting for a task to be done are often called ***daemons***
		* Started when the system runs to control and monitor activities on the system, e.g. networking, printing, disk maintenance, noticing when new equipment is plugged in, monitoring system loads and performance, etc.
	* Basic ***system utilities***
		* Those which handle listing files, viewing them, renaming them, removing them, etc.; bringing network connections up and down; compressing and decompressing files, etc.
		* Many of these utilities (which are often simple ones) are needed by the services already mentioned
		* A particularly important program is the ***command shell*** program, which is what users interact with when they work at a command line, but which is also used by non-interactive scripts
		* The default shell for Linux is usually ***Bash***, which stands for ***B***ourne ***A***gain ***SH***ell, since it is an extension of the older sh, or Bourne Shell program.

* Main Components of Linux Operating System
	* Strictly speaking, the ingredients we discussed (kernel, including device drivers, services, and utilities) are enough to constitute a complete operating system, but other ingredients will be found on general service computers, as what we presented will only give you a ***command-line based terminal***

* Graphical User Inetrface (GUI)
	* Normal users will almosy always be running a ***Graphical User Interface (GUI)***
	* Almost all desktop linux systems will be built using the ***X Window System***(or X) as the base of this interface; it has been around since at least 1984
	* Besides X, there will be a so-called ***window manager*** which controls the appearances and behavior of windows
	* And a ***desktop manager*** which controls the entire desktop; the two most common choices in linux are ***GNOME*** and ***KDE***


### History of Linux

* Linux needed many other components in order to constitute a complete operating system, most of which were supplied by the GNU project in an early stage, including compilers, debuggers, etc
* The first really usable Linux distributions, started around 1992 and they're still in use; in particular, Slackware, Debian, the predecessor of SUSE and Red Hat.
* In 2000, the ***OSDL***, ***the Open Source Development Lab***, was founded in Portland, Oregon, as an independent organization to promote and optimize Linux
* In 2007, there was a major change when it united with another group to form ***The Linux Foundation***, which is now 11 years old [as of 2018] and whose mission is to protect, improve and standardize Linux, with support from many major corporate clients and sponsors as well as a lot of smaller organizations and companies
* OSDL merged with the Free Standards Group in 2007 to form The Linux Foundation, with a base mission to promote, protect, improve and standardize Linux.
* There was a big push in 2000 when IBM invested over a billion dollars in Linux, and when Oracle first imported its database to Linux, and ever since then, it has grown exponentially.

### UNIX and Linux

* We will consider the relationship of Unix and Linux
* Technically, Linux is only the kernel. Everything else that makes up the full operating system comes from a variety of different sources
* Linux is not Unix, although is clearly Unix-like, it is generally not certified as being actual Unix
* Unix goes back at least as far as 1969. It was at the beginning intended to be the operating system for serious heavy iron enterprise system
* By the time Linux was originated in 1991, Unix itself had split into a number of different versions and there was a complicated family tree with two major groupings: System V and BSD
* There were many Unix variants. Most were associated with hardware companies and were shipped with the hardware companies computers, SGI had IRIX, Sun had SunOS and later Solaris, IBM had AIX, Cray had UNICOS, et cetera. Each one of these manufacturers had different varieties running on their own hardware.
* ***SCO*** was one of the only variants not arising from hardware company.

* ***GNU***
	* The Free Software Foundation project, the GNU project, which stands for GNUs Not Unix, came in and made an extremely valuable contribution by making hardware and operating system independent versions of many basic utilities that administrators and developers use everyday, things like tar, ls, grep, et cetera, as well as compilers and libraries
	* Without the GNU project, you really wouldn't have had Linux, at least nothing like we have today
	* There are people who insist Linux should really be called GNU/Linux or something similar, but let's stay out of such silly arguments and we'll just call it Linux.

* Unix and Linux may not be the same thing, but the main developers of Linux had a solid foundation in Unix and they borrowed many basic components, 
	1. inode-based filesystems
	1. the use of device nodes to access hardware
	1. the way scheduling is done --> Multi-processing
	1. how processes and threads are created and destroyed

* Linux is very open and accommodates change from all directions, this is actually helping avoid the kind of fracturing that took place in Unix

### Linux Distribution

* There are many Linux distributions, literally hundreds or even thousands of them, though there's only a small number that are used in large numbers, and they vary by the usage, the hardware, the audience and what kind of support that you have
* So, what does the distribution do? 
	* Well, it packages up all the software you could need in a convenient way that makes it easy to install, upgrade, remove, etc.
	* It makes sure that all the different components of the software work well together
	* It's a bridge between the upstream developers, the people who actually write the code, and the end users
	* It makes sure that information flows in both directions
	* Distributions test the software under far more varied conditions that the upstream developers can do or any particular user can do, and they try to find things that are wrong and also resolve any conflicts between different software packages
	* Distributions also employ a lot of people to do significant work on the individual components within the distribution, the packages, the software packages, as well as the general functioning of the operating system, and even the Linux kernel itself

*  Three major families of Linux distribution
	* Red Hat, which includes
		* CentOS
		* Scientific Linux
		* Fedora
		* Oracle Linux
	* Debian, which includes
		* Ubuntu
		* Linux Mint
	* SUSE, which includes 
		* openSUSE

* Software is installed or removed and controlled through package management systems, and there are two major ones 
	1. RPM --> It is used in all Red Hat and SUSE-derived systems
	1. Debian --> It is used in all Debian-derived systems, not surprisingly


#### Title: Graphical Environments and Interfaces

### Graphical Layer Interfaces

* There are three basic layers and each one has a choice of options for what you can use
* These are 
	- The X Window System
		- The X Window system, usually just called X these days, has a long history, it goes back to at least 1984
		- In its early incarnations, it was designed to handle displaying the results on remote computers at your local workstation or X client, the X terminal, as it was called
		- All-in-all, it was a ***communication protocol***.
		- It wasn't originally designed to just be run on an individual computer
		- X function is relatively simple, it handles
			- The keyboard
			- The pointer
			- It displays the result on the screen
		- X nomenclature
			- The server is what runs on your local machine, which handles the input and display
			- the client is the application being displayed and is as likely to be anywhere on the network and worldwide internet as it is on the local machine
			- This differs from the usual server/client distinction you may be used to, where the server is a remote machine, and the client is local machine.
		- Criticism of X:
			- X grew out of a network paradigm, sometimes it's criticized as having high overhead because it's using the whole network stack, even if it's on a local workstation or a laptop
				- But that's no longer the truth, X uses Unix domain sockets, shared memory, and other features
				- Such that that criticism really doesn't hold any weight in modern systems
		- Alternatives to X
			- New alternatives, in particular, gaining popularity is ***Wayland***
			- It has been the default in Fedora for quite some time now, in the Fedora distribution
			- Wayland is far more secure than X

	- The Window Manager
		- The window manager controls things like the appearance of 
			- A window
			- The title bar
			- Scroll bars look like
			- It handles multiple desktops, which is a very common feature used in Linux systems
			- Other visual effects
		- Different types of window managers
			- For GNOME3, the default is ***mutter***
			- For KDE it is ***kwin***
			- Other ones in use include ***metacity***, ***fvwm***, ***fluxbox***, ***enlightenment***, ***sawfish***,  and ***xfwm***
			* Some are very flashy, some are rather minimal and work very quickly.

	- The Desktop Manager
		- It is what the user actually sees and it controls what's on the desktop
		- It sits above X and the window manager
		- This provides 
			- taskbars
			- menu bars
			- drop-down menus
			- controls drag
			- drop between applications
			- menus
			- icons
			- program launchers
			- all the stuff that any experienced computer user is used to on any graphical desktop environment
		- Most common ones are 
			1. GNOME --> heavily dependent on the gtk set of graphical libraries
			1. KDE --> built upon QT libraries
			1. Other exist including XFCE, or XFCE 4
		- You can generally choose which desktop you want when you're doing the installation
		- If you feel like installing the software for both, you can usually choose between, let's say GNOME or KDE when you boot the system


#### Title: Getting Help

### Getting Help

* There are three basic command line tools people use to get documentation
	- ***man*** Pages or manual pages
		- Basically, everything on the system must have a man page as a general rule
	- info
		- ***info*** is a hyperlinked system of help, that's probably the first hyperlink system of help ever used
		- It comes from the Free Software Foundation's GNU project and then most commands have a help option you can give, which tells you a basic syntax of the command and its options
	- --help and help
		- The shell interpreter has a ***help*** command which you can type help and in the name of a command and, for a lot of the commands, you can get basic documentation that way.

### Graphical Interfaces: GNOME and KDE

* GNOME
	* If you are running a GNOME desktop you can invoke graphical help system directly from the command line by typing:
		* gnome-help
* KDE
	* If you are running a KDE desktop you can invoke graphical help system directly from the command line by typing:
		* ***khelpcenter***
			* NOTE : the command may be ***kdehelpcenter*** instead

