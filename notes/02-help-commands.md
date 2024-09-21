#  linux help commands

###  keyboard shortcuts

`[ctl + alt + t]` opens a new terminal

`[ctl + l]`  clears your terminal

`[ctl + c]`  kills a running program

`[ctl + z]`  pauses a running program

`[ctl + r]`  searches prior commands for a keyword

`[up-arrow]`  goes back to prior command you ran

`[shift + ctl + c]`  copies highlighted text in the terminal

`[shift + ctl + v]`  pastes the copied text in the terminal

`$ program.cpp` to run a program from the terminal, just type the name of the program (tab-
complete is your friend)

###  commands 

`apt`  package manager for debian-based systems

`apropros`  search command for manual page names and descriptions

`whereis`  prints all locations of command

`man`  linux man page

`info`  linux info page

`--help`  help option available for most cli commands

`/usr/share/doc/`  directory for program documentation

`whatis`  prints one line description of command

###  `apt`

`apt`  command line interface for `apt`

**usage**  `$ apt [options] command` run with super user privileges

**description**  `apt` provides a high level command line interface for the package management system

###  `apropos`

`apropos`  search the manual page names and descriptions

usage `$ apropos [options] keyword`

description  each manual page has a short description available within it.  `apropos` searches the descriptions for instances of keyword.

for example use `apropos pdf` 

searching tip.  the use of grep can aid us in our use of `apropos` to search for command sto run.  to do this, we'll have to pipe `|` the output of apropos to grep, as depicted

`$  apropos pdf | grep infor` 

###  `wherreis`

after if find a command i want to use, i can see what type of information is available it with `whereis`

###  `man` manual pages

###  scrolling through the manual page

###  `man` options usage tip

###  `info` information pages

###  `--help` and `--usage`

###  `whatis`

###  let's give it a try

can someone find a command for me to view a `.jpg` file 

`apropos jpg`

`ristretto -V`

`ristretto --help`

`ristretto image.jpg`

`ctrl + alt + t`

update and then install 

###  assessment

1.  Use the "apropos" command to find a desktop (not command line) calculator for this version of xubuntu. What is the name of the program you found?  

`$  apropos calculator`

`mate-calc`

2.  What is the description of the desktop calculator you found, as stated in its man page?

`$ man mate-calc`

`mate-calc` is the official calculator for the mate desktop environment

3.  Which of the following is the file path of the executable for the desktop calculator program you found?

`$ whereis mate-calc`

`/usr/bin/mate-calc`

4.  What is the version of the desktop calculator program you found?

`$ mate-calc --version`

`1.26.0`

5.  What is the default text editor for this version of xubuntu Blank 1? (Hint: what default program would open a text file, such as "instructions" in the clmystery directory (/home/student/clmystery/instructions))

`$ xdg-open ./clmystery/instructions`

Mousepad

6.  Let's find a puzzle game we can play. It has to have monsters in it. Use apropos to find a game for us. What game did you find Blank 1?

`$ apropos puzzle | grep -i Monster`

sgt-undead

7.  which of the following file path of the executable for the puzzle game you found?

`$ whereis sgt-undead`

`/usr/games/sgt-undead`

8.  The game you found appears to have problems displaying the contents of its help file (from the game), so you'll need to use its man page for instructions on how to play. I find the monster icons to be too scary. How would I replace them with letters?

`$ man sgt-undead`, `/letters`

Toggle them off by pressing "A" key

9.  The monster game was way too disturbing for me to play. I think we should just stick with solitaire. Use apt to find a solitaire game we can play. Since this is a Linux class, it has to have penguins in the description. What game did you find ace-of-penguins?

`$ apt search solitaire`l

`ace-of-penguins`

10.  You don't need to install the game you found for us (unless you want to). If you did want to install it, which of the following commands would you use?

`sudo apt update -y`, `sudo apt install ace-of-penguins`

