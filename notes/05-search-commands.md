#  linux search commands

###  overview

[`grep`](##grep) -  grep used for regular expression searches for text in file

[`grep` options](##grep-options)

[`find`](##find) -  find used to find files and so much more

[`find` options](##find-options)

[google regex cheat sheet](https://www.rexegg.com/regex-quickstart.html)

##  `grep`

`grep`, `egrep`, `fgrep`, `rgrep` - print lines that match patterns

`$ grep [options] [patterns] file`

grep searches for patterns in each file.  patterns is one or more patterns separated by newline characters, and grep prints eac line that matches a pattern.  typically, patterns should be quoted when grep is used in a shell command.

##  `grep` options

`-v`  invert the sense of matching to select non-matching lines

`-n`  prefix each line of output with the 1 based line number within its input file

`-c`  suppress normal output; instead print a count of matching lines for each input file

`-i`  ignore case distinctions in patterns and input data, so that characters that differ only in case match each other

`-r`  read all files under each directory, recursively, following symbolic links only if they are on the command line

`-h`  suppress the prefixing of file names on output

`-l`  suppress normal output; instead print the name of each input file from which output would normally have been printed

`-e`  obtain patterns from file, one per line.  if this option is used multiple times, search for all patterns given

`-E`  use extended regular expressions to include special characters, such as `{` `}` without escaping them

`-A`  print num lines of trailing context after matching lines

`-B`  print num lines of leading context before matching lines

`-C`  print num lines of output context

**basic regular expressions**

`^`  and `$` anchoring -  the caret `^` and the dollar sign `$` are meta characters that respectively match the empty string at the beginning and end of a line

`\b`, `\<` `\>` -  the symbols `\<` and `\>` respectively match the empty string at the beginning and end of a word.  the symbol `\b` matches the empty string at the edge of a word

##  `find`

search of files in a directory hierarchy

`$ find [options] [starting point] file`

gnu find searches the directory tree rooted at each given starting point by evaluating the given expression from left to right, according to the rules of precedence (see section operators), until the outcome is known (the left hand side is false for and operations, true for or), at which point find moves on to the next file name.  if no starting point is specified, `.` is assumed.

##  `find` options

`-maxdepth`  descend at most levels (a non negative integer) levels of directories below the starting points

`-minddepth`  do not apply any tests or actions at levels less than levels ( a non negative integer)

`-type`  file is of type (f for file or d for directory)

`-name`  base of file name (the file with the leading directories removed) matches shell pattern `[pattern]`

`-iname`  like `-name`, but the match is case insensitive

`-atime`  file was last accessed less than, more than or exactly `n*24` hours ago

`ctime/mtime`  file's data was last changed (metadata) / modified (data) less than, more than or exactly `n*24` hours ago

`-amin`  file was last accessed less than, more than or exactly `n` minutes ago

`/cmin/mmin`  file's status was last changed (metadata) / modified (data) less than, more than or exactly `n` minutes ago

`N`  refers to the number used in the above commands.  `N`  is the exact number, `-N+`  is greater than the number, `-N-`  is less than the number

`-perms`  file's permission bits are exactly mode (octal or symbolic)

`-exec`  execute command; true if `0` status is returned must be followed by `{}`, `\;`, `{}+`

`-execdir`  like `-exec` but the specified command is run from the subdirectory containing the matched file, which is not normally the directory in which you started find

###  examples

```bash
student@student-virtual-machine:~$ ls clmystery/
cheatsheet.md   encoded  hint2  hint4  hint6  hint8         LICENSE.md  README.md
cheatsheet.pdf  hint1    hint3  hint5  hint7  instructions  mystery     solution
```

```bash
student@student-virtual-machine:~$ grep help clmystery/cheatsheet.md
`ls` will list the files in the current directory.  It's helpful for figuring out where you are, what files exist, and what subfolders exist.
This is helpful if you want to, say, remove a header row from a CSV file:
```

```bash
student@student-virtual-machine:~$ grep help clmystery/*
clmystery/cheatsheet.md:`ls` will list the files in the current directory.  It's helpful for figuring out where you are, what files exist, and what subfolders exist.
clmystery/cheatsheet.md:This is helpful if you want to, say, remove a header row from a CSV file:
clmystery/instructions:There's been a murder in Terminal City, and TCPD needs your help.
grep: clmystery/mystery: Is a directory
clmystery/README.md:There's been a murder in Terminal City, and TCPD needs your help.
```

```bash
student@student-virtual-machine:~$ grep -r help clmystery/* | head -n 20
clmystery/cheatsheet.md:`ls` will list the files in the current directory.  It's helpful for figuring out where you are, what files exist, and what subfolders exist.
clmystery/cheatsheet.md:This is helpful if you want to, say, remove a header row from a CSV file:
clmystery/instructions:There's been a murder in Terminal City, and TCPD needs your help.
clmystery/mystery/crimescene:'Oh, you can't help that,' said the Cat: 'we're all mad here. I'm mad.
clmystery/mystery/crimescene:Alice did not quite know what to say to this: so she helped herself
clmystery/mystery/crimescene:other side of the garden, where Alice could see it trying in a helpless
clmystery/mystery/crimescene:not help thinking there MUST be more to come, so she sat still and said
clmystery/mystery/crimescene:help me out of THIS!' (Sounds of more broken glass.)
clmystery/mystery/crimescene:anxiously about her. 'Oh, do let me help to undo it!'
clmystery/mystery/crimescene:Alice thought decidedly uncivil. 'But perhaps he can't help it,' she
clmystery/mystery/crimescene:desperate that she was ready to ask help of any one; so, when the Rabbit
clmystery/mystery/crimescene:not help thinking there MUST be more to come, so she sat still and said
clmystery/mystery/crimescene:desperate that she was ready to ask help of any one; so, when the Rabbit
clmystery/mystery/crimescene:'I couldn't help it,' said Five, in a sulky tone; 'Seven jogged my
clmystery/mystery/crimescene:not help thinking there MUST be more to come, so she sat still and said
clmystery/mystery/crimescene:with such a puzzled expression that she could not help bursting out
clmystery/mystery/crimescene:other side of the garden, where Alice could see it trying in a helpless
clmystery/mystery/crimescene:help me out of THIS!' (Sounds of more broken glass.)
clmystery/mystery/crimescene:anxiously about her. 'Oh, do let me help to undo it!'
clmystery/mystery/crimescene:help me out of THIS!' (Sounds of more broken glass.)
student@student-virtual-machine:~$ grep help clmystery/cheatsheet.md
`ls` will list the files in the current directory.  It's helpful for figuring out where you are, what files exist, and what subfolders exist.
This is helpful if you want to, say, remove a header row from a CSV file:
student@student-virtual-machine:~$ grep -c help clmystery/cheatsheet.md
2
student@student-virtual-machine:~$ grep -v help clmystery/cheatsheet.md | head -n 20
Playing with text on the command line
=====================================

The command line (also known as the command line interface, or CLI, or sometimes the terminal), is a plain text-based interface for executing commands on a computer.  If you've ever seen a movie about hackers from the 1980s, like *WarGames*, where they stare at a prompt on a black screen and type in commands one at a time, it's basically that.

You have a prompt, and you can type in a command and hit 'Enter' to execute it.  An example command would be:

        touch newfile.txt

This command will create a file called `newfile.txt`.

How to access the command line
------------------------------

**Mac OS X:** Go to /Applications/Utilities and click on "Terminal" or search for "Terminal" in Spotlight.

**Desktop Linux:** You can search for the "Terminal" application from the Dash.  Let's be honest, though, if you're running Linux, you probably don't need this tutorial.

**Windows:** Windows is a bit of a special case.  If you go to the Start Menu and click "Run", and then type "cmd" and hit enter, it will open the Windows version of the command line.  Unfortunately, the Windows version of the command line kind of has its own system, so for the purposes of following these examples, you'll want to install Cygwin, which will allow you to mimic a Linux-style command line:

student@student-virtual-machine:~$ grep -cv help clmystery/cheatsheet.md
356
student@student-virtual-machine:~$ grep -n help clmystery/cheatsheet.md
116:`ls` will list the files in the current directory.  It's helpful for figuring out where you are, what files exist, and what subfolders exist.
291:This is helpful if you want to, say, remove a header row from a CSV file:
student@student-virtual-machine:~$ grep -n help clmystery/*
clmystery/cheatsheet.md:116:`ls` will list the files in the current directory.  It's helpful for figuring out where you are, what files exist, and what subfolders exist.
clmystery/cheatsheet.md:291:This is helpful if you want to, say, remove a header row from a CSV file:
clmystery/instructions:25:There's been a murder in Terminal City, and TCPD needs your help.
grep: clmystery/mystery: Is a directory
clmystery/README.md:28:There's been a murder in Terminal City, and TCPD needs your help.
student@student-virtual-machine:~$ grep -h help clmystry/*
grep: clmystry/*: No such file or directory
student@student-virtual-machine:~$ grep -h help clmystery/*
`ls` will list the files in the current directory.  It's helpful for figuring out where you are, what files exist, and what subfolders exist.
This is helpful if you want to, say, remove a header row from a CSV file:
There's been a murder in Terminal City, and TCPD needs your help.
grep: clmystery/mystery: Is a directory
There's been a murder in Terminal City, and TCPD needs your help.
student@student-virtual-machine:~$ grep -l help clmystery/*
clmystery/cheatsheet.md
clmystery/instructions
grep: clmystery/mystery: Is a directory
clmystery/README.md
student@student-virtual-machine:~$ grep Path clmystery/cheatsheet.md
#### Relative Paths
#### Absolute Paths
student@student-virtual-machine:~$ grep path clmystery/cheatsheet.md
Specifying a file or directory as a relative path means you are specifying where it sits relative to the directory you're in.  For example, let's say you're in the `videos` subdirectory of the `files` directory.  You'll see this prompt:
If you execute a command like `touch newfile.txt`, it will create `newfile.txt` inside the current directory.  Relative paths don't start with a slash.
Specifying a file or directory as an absolute path means you are specifying where it sits on the computer in absolute terms, starting from the top level.  For example, let's say you're in the `videos` subdirectory of the `files` directory again.
If you execute a command like `touch /files/music/newfile.txt`, it will create `newfile.txt` inside a different folder, the `music` subfolder of the `files` folder.  *Absolute paths start with a slash.*
If you use an absolute path, the command will do the same thing no matter what directory you execute it from.
**Starting a path with a slash** means you want to give the entire path and ignore what directory you're currently in.
**Not starting a path with a slash** means you want to give the path starting from the directory you're in.
If you're ever unsure of what directory you're in, you can use the `pwd` (Print Working Directory) command to get the absolute path of the current directory.
`cd` is a command to change the current directory, and must be followed by a directory you want to change to.  You can supply an absolute or relative path.
student@student-virtual-machine:~$ grep -i path clmystery/cheatsheet.md
#### Relative Paths
Specifying a file or directory as a relative path means you are specifying where it sits relative to the directory you're in.  For example, let's say you're in the `videos` subdirectory of the `files` directory.  You'll see this prompt:
If you execute a command like `touch newfile.txt`, it will create `newfile.txt` inside the current directory.  Relative paths don't start with a slash.
#### Absolute Paths
Specifying a file or directory as an absolute path means you are specifying where it sits on the computer in absolute terms, starting from the top level.  For example, let's say you're in the `videos` subdirectory of the `files` directory again.
If you execute a command like `touch /files/music/newfile.txt`, it will create `newfile.txt` inside a different folder, the `music` subfolder of the `files` folder.  *Absolute paths start with a slash.*
If you use an absolute path, the command will do the same thing no matter what directory you execute it from.
**Starting a path with a slash** means you want to give the entire path and ignore what directory you're currently in.
**Not starting a path with a slash** means you want to give the path starting from the directory you're in.
If you're ever unsure of what directory you're in, you can use the `pwd` (Print Working Directory) command to get the absolute path of the current directory.
`cd` is a command to change the current directory, and must be followed by a directory you want to change to.  You can supply an absolute or relative path.
student@student-virtual-machine:~$ grep Yellow clmystery/mystery/vehicles | head -n 3
Color: Yellow
Color: Yellow
Color: Yellow
student@student-virtual-machine:~$ grep -A 3 Yellow clmystery/mystery/vehicles | head -n 5
Color: Yellow
Owner: Jianbo Megannem
Height: 5'6"
Weight: 246 lbs
--
student@student-virtual-machine:~$ grep -B 3 Yellow clmystery/mystery/vehicles | head -n 5

License Plate T3YUHF6
Make: Toyota
Color: Yellow
--
student@student-virtual-machine:~$ grep -C 3 Yellow clmystery/mystery/vehicles | head -n 17

License Plate T3YUHF6
Make: Toyota
Color: Yellow
Owner: Jianbo Megannem
Height: 5'6"
Weight: 246 lbs
--

License Plate AJ0AHI2
Make: Toyota
Color: Yellow
Owner: Matti Othman
Height: 5'7"
Weight: 235 lbs
--

student@student-virtual-machine:~$ head clmystery/mystery/people
***************
To go to the street someone lives on, use the file
for that street name in the 'streets' subdirectory.
To knock on their door and investigate, read the line number
they live on from the file.  If a line looks like gibberish, you're at the wrong house.
***************

NAME    GENDER  AGE     ADDRESS
Alicia Fuentes  F       48      Walton Street, line 433
Jo-Ting Losev   F       46      Hemenway Street, line 390
student@student-virtual-machine:~$ grep Walton clmystery/mystery/people
Alicia Fuentes  F       48      Walton Street, line 433
Aksana Melian   F       86      Walton Street, line 175
Jin Walton      M       58      Savin Hill Avenue, line 159
Kristina Walton F       44      Conrad Street, line 306
Patrick Kiyotake        M       62      Walton Street, line 401
Louis Zhou      M       28      Walton Street, line 253
Walton Souleymane       M       29      Rosemont Street, line 241
student@student-virtual-machine:~$ grep "^Walton" clmystery/mystery/people
Walton Souleymane       M       29      Rosemont Street, line 241
student@student-virtual-machine:~$ grep 19 clmystery/mystery/people | head -n 5
Kelly Gemmell   F       24      Johnson Avenue, line 219
Marina Tchuanyo F       19      Causeway Street, line 399
Anja Solar      F       60      Harleston Street, line 319
Nataliya Lippok F       45      Grieco Terrace, line 419
Samantha Ahamada        F       47      Bancroft Street, line 191
student@student-virtual-machine:~$ grep "\<19\>" clmystery/mystery/people | head -n 5
Marina Tchuanyo F       19      Causeway Street, line 399
Yoon Kelsey     F       19      Loring Place, line 458
Laurence Zyabkina       M       19      Joyce Road, line 18
Anastasia England       F       19      Hartlawn Road, line 464
Gisela Sampson  F       19      Ricker Terrace, line 386
student@student-virtual-machine:~$ grep "\b19$" clmystery/mystery/people | head -n 5
Heather Billings        F       38      Culbert Street, line 19
student@student-virtual-machine:~$ egrep [0-9]{3} clmystery/mystery/vehicles | head -n 6
Weight: 246 lbs
Weight: 205 lbs
Weight: 227 lbs
License Plate D875IMS
Weight: 198 lbs
Weight: 199 lbs
student@student-virtual-machine:~$ grep -E -B 4 [0-9]{3} clmystery/mystery/vehicles | head -n 6
Make: Toyota
Color: Yellow
Owner: Jianbo Megannem
Height: 5'6"
Weight: 246 lbs
--
student@student-virtual-machine:~$ cat /etc/hosts
127.0.0.1       localhost
127.0.1.1       student-virtual-machine

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
student@student-virtual-machine:~$ egrep '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1-3} /etc/hosts
> ^C
student@student-virtual-machine:~$ egrep '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1-3}' /etc/hosts
student@student-virtual-machine:~$ egrep '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' /etc/hosts
127.0.0.1       localhost
127.0.1.1       student-virtual-machine
student@student-virtual-machine:~$ find clmystery/ | head -n 17
clmystery/
clmystery/hint6
clmystery/hint3
clmystery/README.md
clmystery/hint7
clmystery/hint1
clmystery/instructions
clmystery/solution
clmystery/cheatsheet.md
clmystery/hint8
clmystery/hint5
clmystery/hint4
clmystery/cheatsheet.pdf
clmystery/encoded
clmystery/.git
clmystery/.git/objects
clmystery/.git/objects/info
```

##  assessment

**question 1**

how many times does the word "Robert" in the `/home/student/clmystery/people` file?

```bash
student@student-virtual-machine:~/clmystery/mystery$ grep -o 'Robert' people | wc -l
28
```

`28`

**question 2**

how many people who have the first name of "Robert" appear in the `/home/student/clmystery/mystery/people` file?

```bash
student@student-virtual-machine:~/clmystery/mystery$ grep 'Robert ' people
Robert Marennikova      M       78      Parkson Street, line 24
Robert Ryan     M       16      Washburn Avenue, line 247
Robert Loch     M       56      Allston Court, line 307
Robert Dent     M       28      Rustic Road, line 325
Robert Choi     M       58      Redlands Road, line 383
Robert Lovtcova M       36      Oakridge Street, line 62
Robert Dibaba   M       62      Cefalo Road, line 361
Robert Kang     M       39      Tampa Street, line 118
Robert Moutoussamy      M       83      Hunter Street, line 452
Robert Kraljev  M       48      Wesleyan Place, line 348
Robert Toumi    M       65      Ashton Place, line 410
Yuderqui Mrak   F       32      Robert Street, line 487
Robert Pereyra  M       71      Waldemar Avenue, line 29
Robert Skrzypulec       M       54      Whitcomb Avenue, line 301
Robert Mothersille      M       74      Grimes Street, line 273
Robert Adamiec  M       69      Jess Street, line 203
Robert Knowles  M       27      Worcester Square, line 139
Robert Gan      M       44      Old Amory Street, line 12
Roger Hocking   M       50      Robert Street, line 445
```

`17`

**question 3**

how many females appear in the `/home/student/clmystery/mystery/people` file?

```bash
student@student-virtual-machine:~/clmystery/mystery$ grep -o 'F ' people | wc -l
2238
```

`2238`

**question 4**

how many red colored cars are listed in `/home/student/clmystery/mystery/vehicles` file?

```bash
student@student-virtual-machine:~/clmystery/mystery$ grep -o 'Red' vehicles | wc -l
449
``` 

`449`

**question 5**

of all the vehicles listed in the `clmystery/mystery/vehicles` file, how many have a license plate that begins with "T3"

```bash
student@student-virtual-machine:~/clmystery/mystery$ grep " T3" vehicles

License Plate T3YUHF6
License Plate T3HX6N5
License Plate T33VNK9
License Plate T30F7FL
License Plate T3FEPWN

student@student-virtual-machine:~/clmystery/mystery$ grep -o " T3" vehicles | wc -l
5
```

`5`

**question 6**

how many different crime scene reports (based on Crime Scene Report #s) are included in the `clmystery/mystery/crimescene` file?

`1000`

**question 7**

in how many interviews (each interview is summarized in a file in the `clmystery/mystery/interviews` directory) were "soldiers" mentioned?

`10`

```bash
student@student-virtual-machine:~/clmystery/mystery/interviews$ grep -r 'soldiers' .
./interview-6894000:hedgehog to, and, as the doubled-up soldiers were always getting up
./interview-4950099:pack, she could not tell whether they were gardeners, or soldiers, or
./interview-7580872:diamonds, and walked two and two, as the soldiers did. After these came
./interview-5766907:hedgehog to, and, as the doubled-up soldiers were always getting up
./interview-14153840:First came ten soldiers carrying clubs; these were all shaped like
./interview-14153840:diamonds, and walked two and two, as the soldiers did. After these came
./interview-86395001:'Their heads are gone, if it please your Majesty!' the soldiers shouted
./interview-86395001:The soldiers were silent, and looked at Alice, as the question was
./interview-155049:hedgehog to, and, as the doubled-up soldiers were always getting up
./interview-53318557:'Their heads are gone, if it please your Majesty!' the soldiers shouted
./interview-53318557:The soldiers were silent, and looked at Alice, as the question was
./interview-18270219:diamonds, and walked two and two, as the soldiers did. After these came
./interview-618764:hedgehog to, and, as the doubled-up soldiers were always getting up

student@student-virtual-machine:~/clmystery/mystery/interviews$ grep -ro 'soldier' . | wc -l
10
```

`10`

**question 8**

how many people with the first name "Robert" have a membership to Costco based on the files in the `clmystery/mystery/memberships` directory?

`3`

**question 9**

how many total directories are in the clmystery directory including the `clmystery` directory, itself

`22`

**question 10**

how many total files are in the `clmystery` directory and all its sub directories?

`702`





















