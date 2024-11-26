#  process commands

`bg`  backgrounds a running process

`&`  how to start a process running in the background

`fg`  foregrounds a running process

`jobs`  lists backgrounded processes

`ps`  snapshot list of current processes

`pgrep`  look up processes based on name

`top`  live display of current processes

`kill`, `pkill`, `killall` kills a process

###  processes and daemons

programs running in linux can be processes or daemons

processes are just programs that are running on linux

running processes are active

sleeping processes are inactive

zombie processes have completed

daemons are programs that run in the background of linux, regardless of which user is logged in

daemons are called services in the windows operating system

for macintosh computers, daemons are called agents or launch daemons

###  `bg`

`bg`  move jobs to the background

`$ bg` after job has been paused by `ctrl-z` training a command with `&` starts the process in the background

`fg`  move job to the foreground

`$ fg [job specifier (see jobs command)]` 

the job specifier isn't needed if there's only one backgrounded process

###  `ps`

`ps`  report a snapshot of the current processes

`$ ps [options]` 

displays information about a selection of the active processes.  if you want a repetitive update of the selection and the displayed information, use top instead

pertinent options include

`a`  lift the bsd style only yourself restriction

`p [PID]`  select by pid

`u`  display user oriented format

`e`  show the environment after the command

`f`  ascii art process hierarchy

`x`  lift the bsd style must have `tty` restriction 

`-u`  select by effective user id (euid) or name

###  `man ps`

```zsh
PS(1)                                   General Commands Manual                                   PS(1)

NAME
     ps – process status

SYNOPSIS
     ps [-AaCcEefhjlMmrSTvwXx] [-O fmt | -o fmt] [-G gid[,gid...]] [-g grp[,grp...]] [-u uid[,uid...]]
        [-p pid[,pid...]] [-t tty[,tty...]] [-U user[,user...]]
     ps [-L]

DESCRIPTION
     The ps utility displays a header line, followed by lines containing information about all of your
     processes that have controlling terminals.

     A different set of processes can be selected for display by using any combination of the -a, -G,
     -g, -p, -T, -t, -U, and -u options.  If more than one of these options are given, then ps will
     select all processes which are matched by at least one of the given options.

     For the processes which have been selected for display, ps will usually display one line per
     process.  The -M option may result in multiple output lines (one line per thread) for some
     processes.  By default all of these output lines are sorted first by controlling terminal, then by
     process ID.  The -m, -r, and -v options will change the sort order.  If more than one sorting
     option was given, then the selected processes will be sorted by the last sorting option which was
     specified.

     For the processes which have been selected for display, the information to display is selected
     based on a set of keywords (see the -L, -O, and -o options).  The default output format includes,
     for each process, the process' ID, controlling terminal, CPU time (including both user and system
     time), state, and associated command.
```

###  `ps` state codes

as part of its output `ps` will display the state of teh running process using codes.  these codes can help you diagnose a process that isn't responsive

```zsh
Last login: Thu Nov 14 14:39:21 on ttys000
~                                                                   02:40:14 PM
❯ ps u
USER    PID  %CPU %MEM      VSZ    RSS   TT  STAT STARTED      TIME COMMAND
owner 18776   7.2  0.1 411307520  10592 s000  S     2:40PM   0:00.22 -zsh
owner 19431   0.0  0.0 410592928   1120 s000  S     2:40PM   0:00.00 sleep 5
owner 19430   0.0  0.0 410737216   2240 s000  S     2:40PM   0:00.00 /Users/owner/.cache/gitstatus/gitstatusd-darwin-arm64 -G v1.5.4 -s 1 -u 1 -d 1 -c 1 -m -1 -v FATAL -t 20

owner 18790   0.0  0.0 411024928   1712 s000  S     2:40PM   0:00.00 -zsh
owner 18788   0.0  0.0 411024928   2544 s000  S     2:40PM   0:00.00 -zsh

```

###  `pgrep`

`pgrep`  look up processes based on name and other attributes

`$ pgrep [options] pattern`

`pgrep` looks through the currently running processes and lists the process IDs which match the selection criteria to `stdout`.  all the criteria have to match

pertinent options include

`-c`  print a count of matching processes

`-i`  match processes case insensitively 

`-u`  only match processes whose effective user id is listed

`-a`  list the full command line as well as the process id

###  `top`

`top`  display linux processes

`$ top`

the top program provides a dynamic real time view of a running system

pertinent options include use them to toggle top while running

`h`  help 

`q`  quit

`k`  kill a task and then prompted for `pid`

`c`  command line / program name toggle

`L`  locate a string and then prompted for a string

`&`  locate next and find next occurrence of string

`u`  show specific user only and then prompted for a username

`M`, `N`, `P`, `T`  sort columns by `%MEM` `PID` `%CPU` `TIME+`

```zsh
Processes: 661 total, 3 running, 658 sleeping, 2703 threads                                     14:47:42
Load Avg: 3.03, 2.84, 2.86  CPU usage: 13.84% user, 8.38% sys, 77.77% idle
SharedLibs: 781M resident, 136M data, 70M linkedit.
MemRegions: 186852 total, 5273M resident, 336M private, 2021M shared.
PhysMem: 15G used (2125M wired, 1312M compressor), 243M unused.
VM: 262T vsize, 4915M framework vsize, 0(0) swapins, 12(0) swapouts.
Networks: packets: 3982887/4338M in, 1517462/467M out. Disks: 11106696/142G read, 6105369/80G written.

PID    COMMAND      %CPU  TIME     #TH    #WQ  #PORT MEM    PURG   CMPRS  PGRP  PPID  STATE
5611   fileprovider 100.0 90:08.24 8/1    7/1  157   34M    128K   5280K  5611  1     running
14657  iTerm2       41.7  00:40.41 10     7    340+  138M-  32M+   14M-   14657 1     sleeping
1      launchd      16.5  06:24.78 3      2    3660  24M    0B     5936K  1     0     sleeping
377    WindowServer 15.6  35:17.00 22     6    2656- 678M+  41M+   152M   377   1     sleeping
0      kernel_task  13.9  42:37.61 541/10 0    0     10M-   0B     0B     0     0     running
22180  top          5.1   00:00.49 1/1    0    27    7970K+ 0B     0B     22180 21517 running
5712   AXVisualSupp 3.7   02:05.75 11     5    318   18M    0B     4928K  5712  1     sleeping
8120   Moom Classic 2.4   00:10.87 6      4    247+  21M    0B     8400K  8120  1     sleeping
15985  com.apple.We 2.4   00:51.63 8      2    93    229M   0B     17M    15985 1     sleeping
```

###  `kill`

`kill`  send a signal to a process

`$  kill [options] PID`

the default signal for kill is `TERM`.  use `-l` or `-L` to list available signals.  particular useful signals include `HUP`, `INT`, `KILL`, `STOP`, `CONT`, `0`.  alternative signals may be specified in three ways `-9`, `-SIGKILL`, `-KILL`

pertinent `SIGNALS` include

`SIGINT`  least violent of the ignorable signals, like pressing `ctrl-c`

`-SIGNUP`  for program hang-ups, will attempt to restart process

`SIGTERM`  graceful exit, can be blocked, doesn't kill child processes

`SIGNKILL`  abrupt exit, can't be blocked, kills child processes

###  `killall`

`killall`  kill processes by name

`$ killall [option(s)] NAME`

`killall` sends a signal to all processes running any of the specified commands

pertinent options include

`-s`  send this signal instead of `SIGTERM`

`-l`  list all known signal names, can use same as kill `SIGNALS`

essentially think of `killall` as a command with `grep` capabilities, `pkill` is also a command that can be used instead of `killall`

###  assessment questions

start firefox from the terminal by typing "firefox", followed by the enter key. after the Firefox browser starts, return to the terminal and pause Firefox so that you can background it. what key combination did you use to pause Firefox?

`ctrl+z`

now that Firefox is paused, you need to background it. what command did you enter at the terminal to background Firefox?

`bg`

run the jobs command. what was the status of Firefox?

`Running`

now, bring Firefox back to the foreground of the terminal. what command did you use?

`fg 1`

use one of the commands we covered in class to determine the full command line that started Firefox. from which directory was it executed?

`snap`

linux processes are similar to services in Windows and Linux daemons are similar to Windows processes.

`false`

in the terminal type "dd if=/dev/zero of=/dev/null" (you should be able to tab-complete the file paths). now, open another terminal and use one of the commands we covered in class to see the percentage of memory the "dd" process is using. which percentage range below covers the amount of memory being used by "dd"?

`90 - 100`

use one of the commands we covered in class to determine the state of the "dd" process. which of the below states is indicated for the "dd" process?

`R+`

match the kill SIGNAL to a description below.

`SIGNUP`  will attempt to restart the process.

`SIGNINT`  least "violent" of the four signals

`SIGTERM`  graceful exit that won't kill child processes

`SIGKILL`  abrupt exit that will kill child processes

in linux, the "ps" commands gives you a "snapshot" of current processes; whereas "top" gives you a dynamic, real-time view of the processes.

`true`