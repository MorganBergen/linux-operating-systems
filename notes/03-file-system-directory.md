#  linux file system & linux directory structure

##  directory commands

`man file-hierarchy` - file system hierarchy overview

`man hier` describes the file system directories

`ls` list storage

`du` estimate file space usage

`df` report file system disk space usage

`mkdir` make directory

`rmdir` remove directory

`cd` change directory

`pwd` print working directory

##  `man file-hierarchy`

`file-hierarchy` provides a file system hierarchy overview of the linux system file directory.  you can access it by typing `man file-hierarchy` in the linux cli.  doing so give you a good description of the directories in linux along with their purposes.  as with other man pages, you can search for terms of interest by pressing the `/` key, typing a search term, and hitting enter.  using an `&` instead of `/` will hide all other lines of text that don't contain the search term.  pressing `&` again followed by enter will show all lines as before.

##  `man hier`

typing `man hier` in the command line gives you a similar output to `man file-hierarchy` but with a more detailed and more complete description of the various directories in linux

`/` this is the root directory.  where the whole tree starts

`/etc` contains configuration files which are local to the machine.  some larger software packages, like x11, can have their own subdirectories below `/etc`.  site wide configuration files may be placed here or in `/usr/etc`.  nevertheless, programs should always look for these files in `/etc` and you may have links for these files to `/usr/etc`

`/home` on machines with home directories for users, these are usually beneath this directory, directly or not.  the structure of this directory depends on local administration decisions

`/media`  this directory contains mount points for removable media such as cd and dvd disks or usb sticks.  on systems where more than one device exists for mounting a certain type of media, mount directories can be created by appending a digit to the name of those available above starting with `0`, but the unqualified name must also exist

`/mnt`  this directory is a mount point for a temporarily mounted filesystem.  in some distributions, `/mnt` contains subdirectories intended to be used as mount points for several temporary filesystem

`/tmp`  this directory contains temporary files which may be deleted with no notice, such as by a regular job or at system boot up

`/usr/bin`  this is the primary directory for executable programs.  most programs executed by normal users which are not needed for booting or for repairing the system and which are not installed locally should be placed in this directory

`/usr/sbin`  this directory contains program binaries for system administration which are not essential for the boot process, for mounting `/usr` or for system repair

`/var/log`  miscellaneous log files

##  `ls`

`ls` list directory contents

**usage** `$ ls [option] file

**description** list information about the files (the current directory by default).  sort entries alphabetically if non of `-cftuvSUX` nor `--sort` is specified

##  `ls` pertinent options

`ls -a`  do not ignore entries staring with `.` which are hidden files

`ls -l -s -h`  human readable, print sizes like 1k 234m 2g

`ls -l`  use a long listing format, prints the actual size of the file

`ls -R`  list subdirectories recursively

`ls -s`  print the allocated size of each file in blocks 

`-r` reverse order while sorting

`-S` sort by file size, largest first

`-t` sort by time, newest (modification time) first

`-u` access time (atime), access, use


```bash
❯ ls -ls
total 232
  allocated file size in bytes         actual file size in bytes
  ↓                                    ↓
  0 drwx------@   3 owner  staff      96 May 27  2022 Applications
  8 -rw-r--r--    1 owner  staff     805 Sep 14  2022 Brewfile
  0 drwx------@   8 owner  staff     256 Sep  6 13:55 Desktop
  0 drwx------@  21 owner  staff     672 Sep  6 14:15 Documents
  0 drwx------@  11 owner  staff     352 Sep  6 12:21 Downloads
  0 drwxr-xr-x@   4 owner  staff     128 Dec 15  2023 ITS
  0 drwx------@ 140 owner  staff    4480 May 19 22:02 Library
  0 drwx------+  21 owner  staff     672 Sep  1 18:16 Movies
  0 drwx------+   7 owner  staff     224 Sep  1 19:08 Music
  0 drwx------@   5 owner  staff     160 May 19  2022 OneDrive
  0 drwxr-xr-x    3 owner  staff      96 Jun 30  2022 PATH
  0 drwx------+   7 owner  staff     224 Jul 30  2022 Pictures
  0 drwxr-xr-x+   5 owner  staff     160 May 19  2022 Public
  0 drwxr-xr-x+   5 owner  staff     160 Jan 31  2023 Sites
  0 drwxr-xr-x    5 owner  staff     160 Jun 13  2022 VIA
  0 drwxr-xr-x   22 owner  staff     704 Apr 19  2021 homebrew
  0 drwxr-xr-x  138 owner  staff    4416 Mar 19 12:28 node_modules
216 -rw-r--r--@   1 owner  staff  110379 Mar 19 12:30 package-lock.json
  8 -rw-r--r--@   1 owner  staff     204 Mar 19 12:28 package.json
  0 drwxr-xr-x   19 owner  staff     608 Oct  7  2022 powerlevel10k
```

##  `du`

`du`  estimate file space usage

**usage** `$ du [option] file`

**description**  summarize disk usage of the set of files, recursively for directories

`-h`  print sizes in human readable format e.g.  1k, 234m 2g

`-s`  display only a total for each argument

`--si`  like `-h` but uses powers of 1000 not 1024

##  `df`

`df`  ‘

`df -H`

`df -h`

##  `pwd`

`pwd` -  print name of current / working directory

usage `$ pwd` 

description -  print the full filename of the current working directory

##  `cd`

`cd` -  change the shell working directory

usage `$ cd directory`

description -  change the current directory to dir.  the default dir is the value of the home shell variable.  the home shell variable can be seen with the command `echo $HOME`, it should be the home of the user account under which the command was run i.e. `/home/student`

`cd ~` - is the same as just running cd

##  `mkdir`

`mkdir` -  make directories

usage `$ mkdir [option] directory`

description -  create the directory or directories if they do not already exist

persistent options include 

`mkdir -m` -  set file mode permissions 

`mkdir -p` -  make parent directories as needed

##  `rmdir`

`ls -i` -  list files with inode number, inode is a unique number that the operating system assigns to a file


##  assessment

**question 1 -  what does the -i option for the ls command do?**

`ls -i` print the index number of each file

**question 2 -  what is the actual size of the clmystery/cheatsheet.md file?**

`ls -lsh` - 13844 bytes

**question 3 -  what is the largest file in the `/home/student clmystry` directory? include file extension**

`ls -lSrh clmystery` - cheatsheet.pdf

**question 4 -  what is the purpose of the `/dev` directory?**

`man hier` - special or device files, which refer to physical devices

**question 5 -  what is the human readable power of 1024 size of the `clmystery` directory?**

`du -sh clmystery` - 14m

**question 6 -  what is the full path of the home directory for the student account?**

`pwd` - `/home/student`

**question 7 -  in the class vm, what commands could one use to switch home directory of the student user?**

use `cd ~` or `cd` or `/home/student`

**question 8 -  what animal is the mascot of linux?**

penguin

**question 9 -  which of the following is the largest file system mounted on the class vm?**

`ll` - /dev/sda3

**question 10 -  what is the approximate size of `/dev/sda2` in mb?**

`/dev $ df -h` - 512