# LINUX FILESYSTEM HIERARCHY (FHS)
*Maintained by Muhammad Awais*

Linux organizes everything under one single root directory, unlike Windows which has separate drives like C and D. Every file, every device, every piece of configuration lives somewhere under that one root. This document breaks down every major directory in plain, simple language.

## / (Root)
This is the top of everything. Every other directory lives inside this one. When the system boots, root is the very first thing that gets mounted, because without it nothing else can load. Think of it as the trunk of a tree, with every directory being a branch growing out of it.

## /bin (Essential User Commands, Binaries)
Contains the basic commands everyone uses daily, things like `ls`, `cp`, `mv`, `cat`, and `pwd`. These are the tools needed for the system to even function at a basic level. Every user, whether normal or root, uses these constantly. On modern distros this directory is often just a symlink pointing to `/usr/bin`.

## /boot (Boot Files)
Holds the Linux kernel image and the bootloader files (like GRUB) along with the initial ramdisk. This is what gets read the moment your computer powers on, before the rest of the operating system even loads. If this directory gets corrupted, your system simply will not boot.

## /dev (Device Files)
Linux treats hardware as if it were a file, and this is where that happens. Your hard disk, your mouse, your keyboard, even random number generators, all get represented here as special device files. For example `/dev/sda` is your disk, and `/dev/input/mouse0` represents your mouse. These files do not take up real storage space, they are dynamically created by the kernel through a system called udev whenever hardware is detected.

## /etc (Configuration Files)
This is where system wide settings live. User account information sits in `/etc/passwd`, password hashes sit in `/etc/shadow`, and SSH server settings sit in `/etc/ssh/sshd_config`. Basically any service that runs persistently in the background and needs the same settings every time it starts keeps its configuration here. This is also a favorite target for attackers since it holds so much sensitive system information.

## /home (User Home Directories)
Every regular user gets their own personal directory here, like `/home/awais`. This is where your documents, downloads, and personal configuration files live. Each user typically only has access to their own home directory unless permissions are changed.

## /lib (Shared Libraries)
Programs do not carry all their own code. Common functionality, like printing text or allocating memory, is stored once in shared library files here (with a `.so` extension) and every program borrows from them at runtime. This saves space and makes updates easier, since fixing a library once updates it for every program that uses it.

## /lib32 and /lib64 (Architecture Specific Libraries)
Computers process data in either 32 bit or 64 bit mode, and each mode needs its own version of libraries because they are not compatible with each other. Modern systems mainly use 64 bit libraries stored here, but some older programs are still compiled as 32 bit, so a separate set of 32 bit libraries is kept around just for backward compatibility. This is common in penetration testing since a lot of practice binaries and old exploits are compiled as 32 bit.

## /media (Auto Mounted Removable Devices)
When you plug in a USB drive or insert a CD, the desktop environment automatically mounts it here so you can browse the files right away, usually under a path like `/media/username/devicename`. This only applies to storage devices, not input devices like your mouse or keyboard, since those do not carry files that can be browsed.

## /mnt (Manual Temporary Mounts)
This is an empty directory reserved for administrators to manually mount things using the `mount` command, things like an extra disk partition, a disk image for forensic analysis, a network share, or an ISO file. The difference from `/media` is control. `/media` is automatic and handled by the system, `/mnt` is manual and handled by you through the terminal.

A disk can normally only be mounted in one place at a time. Mounting it somewhere means attaching its contents to a specific directory so you can access it, similar to fitting a door into a wall. That same door cannot be fitted into two walls at once under normal circumstances.

## /opt (Optional or Third Party Software)
Some software companies prefer to bundle their entire application, binary, libraries, and resources, into one single self contained directory instead of scattering it across the system. That software lives here, each application getting its own subdirectory like `/opt/google/chrome`. This makes uninstalling easy since you can often just delete the directory, and it avoids conflicts with system libraries.

## /proc (Live Kernel and Process Information)
This is a virtual filesystem, meaning nothing here is actually stored on disk. The kernel generates this data live, on the spot, every time you read it. Every running process gets its own directory named after its process ID, showing details like memory usage and open files. System wide info like `/proc/cpuinfo` and `/proc/meminfo` also lives here. It essentially works like a live camera feed into what the kernel already knows about your system, and tools like `ps` and `top` actually read from here behind the scenes.

## /root (Root User Home Directory)
This is the personal home directory for the root user, separate from `/home`. It is kept close to the root filesystem so that root can still log in and fix things even if `/home` fails to mount for some reason. Do not confuse this with `/` (the root of the whole filesystem), they are two completely different things.

## /run (Runtime State for Services)
Also a RAM based virtual filesystem like `/proc`, but the key difference is who writes the data. In `/proc`, the kernel automatically generates everything without being asked. In `/run`, services themselves choose to write small notes about their own state, like their process ID (`/run/sshd.pid`) or a communication socket (`/run/docker.sock`). Think of `/proc` as an automatic camera recording everything, and `/run` as a sign in sheet where each service writes its own entry. Everything here gets wiped on reboot since it lives in RAM.

## /sbin (System Administration Commands, System Binaries)
Similar to `/bin`, but these are commands mainly meant for system administration, usually requiring root privileges since they can make powerful or destructive changes. Examples include `fdisk` for managing disk partitions, `mkfs` for formatting a filesystem, `reboot`, and `iptables` for firewall rules. Keeping these separate from `/bin` helps clearly mark which commands are safe for daily use and which ones need extra caution.

## /srv (Service Data)
Holds data that is served to other systems by services running on this machine. If you are running a website, the site files might live in `/srv/www`. If you are running an FTP server, the files being shared could live in `/srv/ftp`. Git repositories hosted on the server can also live here. Basically this is the designated place for data your machine is actively serving out to others, keeping it separate from personal user files and system configuration.

## /sys (Kernel and Hardware Interface)
Another virtual filesystem, similar in spirit to `/proc`, but focused specifically on hardware devices and kernel modules rather than processes. It exposes a structured, organized view of every device connected to your system and lets you interact with kernel settings directly through simple file reads and writes. Where `/proc` leans more toward processes and general system stats, `/sys` leans more toward hardware and driver level details.

## /tmp (Temporary Files)
A directory anyone and anything on the system can write to, meant purely for short lived, temporary files. Installers, compilers, and your own test scripts often use this space. On modern systems it usually lives in RAM, so it gets wiped automatically on reboot. Because it is world writable, it is also a well known attack surface in cybersecurity, commonly abused for privilege escalation tricks, staging malware temporarily, or accidentally leaking sensitive data left behind carelessly. Note that a remote attacker cannot write here directly from outside, they first need some form of access to the system itself, through a vulnerability or stolen credentials, before they can touch this directory.

## /usr (User System Resources)
Despite the name, this is not really about individual users, it holds the bulk of installed software on the system. Inside it you will find `/usr/bin` for most non essential programs, `/usr/lib` for their libraries, and `/usr/share` for documentation and shared resources. This is typically the largest directory on the system since almost every application you install ends up here.

## /var (Variable Data)
Short for variable, this directory holds data that constantly changes while the system runs, unlike `/usr` which stays mostly static. Logs live in `/var/log`, website files served by a web server can live in `/var/www`, mail inboxes and cron job data also live here. For anyone doing security analysis or incident response, `/var/log` is usually the very first place to check, since it records login attempts, errors, and timestamps that tell the story of what happened on a system.

## Conclusiion
Everything in Linux boils down to one simple idea. If something needs to run at boot, it lives near `/boot` or `/bin`. If something is a live snapshot of the system, it lives in `/proc` or `/sys`. If something is temporary, it lives in `/tmp` or `/run`. If something is meant to last and be organized, it lives in `/etc`, `/usr`, or `/var`. Once that pattern clicks, the entire filesystem stops feeling random and starts feeling like a well designed map.

![A visual guide to the Linux Filesystem](assets/linux(FHS).png) 