#  file permission commands

##  overview

[`stat` limited to use to see file permissions](#stat)

[`umask`  displays the file mode mask](#umask)

[`chmod`  change file permissions](#chmod)

[`chown`  change file user and group ownership](#chown)

[`chgrp`  change file group ownership](#chgrp)

[`./`  execute a program from the linux command line](#how-to-execute-a-file-from-linux-cli)

like many operating systems, linux is multi user.  in other words, there can and often is multiple user accounts on a linux system.  to prevent users from reading, modifying, or executing other users' file and programs, linux uses file permissions.  one can see the permissions of a file or directory using the `ls -l` as well as another command `stat`.

##  symbolic file permissions

`-rw-rw-r--   1 owner  staff     204 Mar 19  2024 package.json`

`-`  file type

`rw-rw-r--`  file permissions

`rw-`  user permissions

`rw-`  group permissions

`r--`  other permissions

the user which is `owner` who ones the file, has read `r` and write `w` permissions for the file.  the group who is `staff` also has read `r` and write `w` permissions, but all other only have read `r` permissions.

execute `x` is also a permission.  in the above example, it would appear in place of the `-` if the file were executable `-rwxrwxr-x`.  `rwx` are all considered symbolic representations of the permissions.

##  absolute file permissions

<details><summary><code>stat -l package.json</code></summary>
<br>

```bash
~
❯ stat -l package.json
-rw-r--r-- 1 owner staff 204 Mar 19 12:28:52 2024 package.json

~
❯ stat -r package.json
16777231 1281270 0100644 1 501 20 0 204 1710869336 1710869332 1710869332 1663205326 4096 8 0 package.json
```

</details>

<details><summary><code>stat -c %a clmystery/hint1</code></summary>
<br>

```bash
student@student-virtual-machine:~$  stat -c %A clmystery/hint1
-rw-rw-r--

student@student-virtual-machine:~$  stat -c %a clmystery/hint1
664
```

`664` is the absolute octal permissions used in linux to represent the permissions of a file.  as in the case of the symbolic file permissions, the absolute octal file permissions are separated by user, group, and other.  however the permissions are now represented by numbers, which are added together

`0`  no permission  
`1`  execute permission  
`2`  write permission  
`4`  read permission  

in the above file, the user `student` who owns the file, has read `4` plus write `2` permissions for the file `4 + 2 = 6`.  the group `student` who owns the file also has read `4` plus write `2` permissions for the file `4 + 2 = 6`, but all others only have read `4` permissions.  that's why the above permissions are represented by `664`

</details>

<details><summary><code>for i in {1..10}; do echo -ne $i"\t"; printf "%o\n" $i; done</code></summary>
<br>

the output of the first command below shows the octal equivalent of decimal 1 to 10.  

```bash
student@student-virtual-machine:~$  for i in {1..10}; do echo -ne $i"\t"; printf "%o\n" $i; done
1      1
2      2
3      3
4      4
5      5
6      6
7      7
8      10
9      11
10     12
```

</details>


<details><summary><code>for i in {1..7}; do number=$i; binary=$(echo "obase=2;$number" | bc); printf "%d\t%4s\n" $number $binary; done</code></summary>
<br>

the output of the second command shows the binary equivalent of decimal 1 to 7

```bash
student@student-virtual-machine:~$  for i in {1..7}; do number=$i; binary=$(echo "obase=2;$number" | bc); printf "%d\t%4s\n" $number $binary; done
1	   1
2	  10
3	  11
4	 100
5	 101
6	 110
7	 111
```

</details>

<details><summary><code>stat -c %a clmystery/hint1</code></summary>
<br>

as you can see the `rw-rw-r--` equates to 664 in binary
 
```bash
student@student-virtual-machine:~$  ls -l clmystery/hint1
-rw-rw-r-- 2 student student 146 Sep 11 14:47 clmystery/hint1

student@student-virtual-machine:~$  stat -c %a clmystery/hint1
664
```

</details>

##  `stat`

**definition**  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  display file or file system status

**usage**  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `$  stat [option] [file]`

**pertinent options include**

`-c` use the specified format instead of the default; output a newline after each use of format

`%a`  permission bits in octal

`%A`  permission bits and file type in human readable form

##  `umask`

**definition**  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; display or set file mode mask

**usage**  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   `$ unmask [option] mode`

**pertinent options include**

`-S`  makes the output symbolic; otherwise an octal number is output.  we will only use `umask` to demonstrate how the default permissions for a file or directory are set.  it can be used to temporarily change the default permissions, but will reset on exiting the terminal (there are files that can be modified to make it permanent)

##  `chmod`

**definition**  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; change file mode bits

**usage**  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `$ chmod [option] [mode] file` or  `$ chmod [option] [octal-mode] file`

**description**  &nbsp;&nbsp;  chmod changes the file mode bits of each given file according to mode, which can be either a symbolic representation of changes to make, or an octal number representing the bit pattern for the new mode bits.

**pertinent options include**

`-R`  change files and directories recursively

`--reference=RFILE`  use `RFILE`'s mode instead of `mode` values

chmod can set other permission bits, but we won't really cover them in class, beyond their description here.

`setuid`  run program as owner `chmod u+s`

`setgid`  run program as group `chmod g+s`

`sticky bit` if set on a directory, only the owner can delete the files in the directory `chmod +t`

for directories, `chmod` works a little differently.  permissions have the below described effects on a directory.

`read` list `ls` contents of directory

`write`  create / remove files from the directory

`execute`  `cd` into the directory; access files in the directory

##  `chown`

**definition**  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  change file owner and group

**usage**  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  `$ chown [option] owner:group file`

**description**  &nbsp;&nbsp;  `chown` changes the user and or group ownership of each given file

**pertinent options include**

`-R`  operate on files and directories recursively

`--reference=RFILE`  use `RFILE`'s owner and group rather than specifying `owner:group` values

##  `chgrp`

**definition**  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; change group ownership

**usage**  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `$ chgrp [option] group file`

**description**  &nbsp;&nbsp; change the group of each file to `group`.

**pertinent options include**

`-R`  operate on files and directories recursively

`--reference=RFILE`  use `RFILE`'s owner and group rather than specifying a `group` values

##  how to execute a file from linux cli

if we want to execute a file from the linux command line interface, we need to prepend the file with `./` without `./` prepended to the file name, linux will look in `PATH` variable to see if there's a program with the name of the file.  by using `./`, we are simply telling linux to run the executable file in the current directory.

##  assessment

**question 1**  

`cd` into the `week6assessment` and make `file1` executable for the user only `student` with a symbolic representation of the mode.  do not change any other permissions of the file.  what command did you use to make the file executable?  type in the command just as you typed it in the command line.

`chmod u+x file1`

**question 2**  

what message was revealed after you executed `file1`.  type in the message exactly as it appeared in the terminal when you executed the command.

`Congratulations! You made the file executable!`

**question 3**  

remaining in the `week6assessment` directory, make `file2` readable for the user only `student` with a symbolic representation of the mode.  do not change any other permissions of the file.  what command did you use to make the file readable?  type in the command just as you typed it in the command line.

`chmod u+r file2`

**question 4**  

read `cat file2`.  what message was revealed when you read `file2`?  type in the message exactly as it appeared in the terminal when you executed the command.

`Good job. You were able to read the message!`

**question 5**  

remaining in the `week6assessment` directory, make `file3` executable for the user only `student` with an octal representation of the mode.  do not change any other permissions of the file.  what command did you use to make the file executable?  type in the command just as you typed it in the command line.

`chmod 700 file3`

**question 6**  

read `cat file3`.  what message was revealed when you read `file3`?  type in the message exactly as it appeared in the terminal when you executed the command.

`Well done. Octals are a bit trickier to use, but more precise.`

**question 7**  

remaining in the `week6assessment` directory, make `file4` readable for the user only `student` with an octal representation of the mode.  do not change any other permissions of the file.  what command did you use to make the file readable?  type in the command just as you typed it in the command line.

`chmod 600 file4`

**question 8**  

read `cat file4`.  what message was revealed when you read `file4`?  type in the message exactly as it appeared in the terminal when you executed the command.

`You got it!`

**question 9**  

remain in the `week6assessment` directory.  without making any permission changes, attempt to list `ls` the files in the `assessment_directory` directory.  were you able to do it?

`no`

**question 10**  

use `chmod` to enable you to list the files in the `assessment_directory` directory.  remember to use least privilege.  in other words, grant file read privileges only to the user who needs them, not to all users or all members of the group.  also, don't over grant privileges (no need to make the file executable, just to read it) and don't remove privileges, only add them.  what command did you use to make the file readable?  type in the command just as you typed it in the command line.

`chmod u+r assessment_directory`