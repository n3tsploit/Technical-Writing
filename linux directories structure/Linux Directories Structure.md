# Linux Directory Structure
![[Untitled Diagram.drawio (2).drawio.png]]
Linux is a very important tool for people in the IT industry e.g developers and cybersecurity professionals. It is therefore an added advantage if one knows the ins and outs of the linux system and how things are organised in it.
In this article I'll be taking you through the directory structure of the llinux file system.This article is directed towards people who are still new to the linux system.

Linux uses the Filesystem Hierarchy Standard (FHS) in the layout of its system.In this standard all the files and directories of the system are under the root directory(/) regardless of whether they are stored in different virtual or physical devices.

### / 
This is the root directory.It holds everything in your linux file system.It is similar to C:\ directory found in windows.

### /boot
Boot-related files  are found in this directory.These are files required while booting the system.Data found here is processed first before the kernel begins executing user-mode programs.An example of such files are Grub Boot loader files and vmlinux.

### /bin
Essensial User binaries which some might call "executable programs", are located here.One thing to note is that /bin contains shells e.g bash,zsh and common linux commands e.g ps,ls, rm etc. that all users can use. Other binaries such as browsers are stored in /usr/bin/.

### /dev
/dev directory contains device files.Device files represent hardware devices connected to your Linux system that applications interact with via I/O system calls. This shows an important aspect of the linux filesystem which is that everything is either a file or a directory.
One device file worth taking note of is the /dev/null.Anything sent here dissapears, its some sort of a "black hole".

### /etc
Linux System confugaration files like the boot loader's configuration files are in this directory.
- /etc/opt stores configuration for ad-on packages
- /etc/sgml stores configuration for  software that processes SGML
- /etc/xll stores configuration for the X Window System
- /etc/xml stores configuration for  software that processes XML
- /etc/passwd stored encrypted user passwords

Confugartion files affecting specific users are in the user's home directory.

### /home
Each user's home folder is located in this directory. The folders are named according to the user's username and contain their data and configuration files.

### /lib
This directory hold kernel modules and essential shared system libraries needed by /bin and /sbin. The filenames of files in this directory are in the formart either ld* or lib*.so.* .

### /lost+found
Any corrupted files found during rebooting is stored in this directory.This helps you to recover as much data as you can.

### /media
This directory is  where removable devices are mounted.Examples of such devices are Usb disk,CD/DVD ROM (mounted at /media/cdrom), floppy disks (mounted at /media/floppy)etc. Contents of those devices can be accessed from here.

### /mnt
This is where temporary  file systems are mounted by sysadmins while using them.Network shares is an example of such.

### /opt
Add-on application Packages are found here. These are proprietary software/ third party software  and are not available in the distribution’s repository.

### /proc
It Contains information on system processes, kernel and configuration parameters.It is a virtual filesystem hence does not contain any 'real' files.

### /root
This is the home directory of the root user. It is worth noting that only the root user has priviledges to write in this directory.

### /run
It stores volatile data which occurs at runtime.

### /sbin
This directory contains essential binaries that are  run by system administrator for system maintenance and/or administrative tasks.

### /srv
This directory contains data files for services provided by system.I.e website files of apache server or FTP servers.

### /sys
This directory is found in modern linux systems.It  a virtual filesystem that stores information about hardware devices and its drivers and kernel features.

### /tmp
This stores temporary application files created by system or user. These files are deleted everytime the system is rebooted.

### /usr
This directory contains binaries,programs,utilities and files used by the users.
- User binary files are under /usr/bin.
- System binaries used by the system administrator ie sshd and userdel are under /usr/sbin
- Lbraries for /usr/bin and usr/sbin are under /usr/lib
- Programs installed from the source are under /usr/local
- Standard include files are in /usr/include
- Source codes  i.e the kernel are found  in /usr/src
- Docmentation which is common to all libraries are found in /usr/share

### /var
Variable files are found in this directory. These are files whose contents are expected to change as the system runs.Examples of such files are system log files, lock files, print queues etc.
- /var/cache - cached files from application programs are stored here
- /var/lib - Holds dynamic data libraries and files.
- /var/log - log files are found here
- /var/opt - variable data of packages in /opt/
- /var/mail - mailbox files are held here
- /var/spool - Tasks in queues waiting to be processed are stored here.
- /var/run - Holds information on the system since it booted
- /var/tmp - It holds temporary files saved between reboots of the system
- /var/log - It contains lock files created by programs to show that a certain file or device is being by it.

## Conclusion
I hope this article has helped you get an overview of how the top level linux directories are structed.
Thank you for your time.