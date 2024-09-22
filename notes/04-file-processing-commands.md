#  linux file processing commands

###  overview

`file` determine a file's type - remember linux file extensions are only for convenience  

`cat` concatenate files to standard output  

`zcat` like cat but with compressed files

`more`  filter for paging through text files

`less` same as more but with additional features

`head`  output the first part of a file

`tail`  output the last part of a file

`cp` copy files and directories

`md5sum`  compute and checks md5 message digest

`rm`  deletes a file

`mv`  move or rename files

`wc`  print newline, word, and bute counts of a file

##  `file`

`file`  determine file type

`$  file [options] FILE`

file tests each argument in an attempt to classify it.  there are three sets of tests, performed in this order - filesystem tests, magic tests, and language tests.  the first test that succeeds causes the file type to be printed

pertinent options include

`-z` try to look inside compressed files

`-Z` try to look inside compressed files, but report information about the contents only not the compression

`file notes/*`

```bash
~/Documents/linux-operating-systems main*
❯ file notes/*
notes/01-introduction.md:             ASCII text, with very long lines (337)
notes/02-help-commands.md:            ASCII text
notes/03-file-system-directory.md:    Unicode text, UTF-8 text, with very long lines (552)
notes/04-file-processing-commands.md: ASCII text
```


`xxd notes/04-file-processing-commands.md | head` reveals `2320 206c` as the magic number for the file

```bash
~/Documents/linux-operating-systems main*
❯ xxd notes/04-file-processing-commands.md | head
00000000: 2320 206c 696e 7578 2066 696c 6520 7072  #  linux file pr
00000010: 6f63 6573 7369 6e67 2063 6f6d 6d61 6e64  ocessing command
00000020: 730a 0a23 2323 2020 6f76 6572 7669 6577  s..###  overview
00000030: 0a0a 6066 696c 6560 2064 6574 6572 6d69  ..`file` determi
00000040: 6e65 2061 2066 696c 6527 7320 7479 7065  ne a file s type
00000050: 202d 2072 656d 656d 6265 7220 6c69 6e75   - remember linu
00000060: 7820 6669 6c65 2065 7874 656e 7369 6f6e  x file extension
00000070: 7320 6172 6520 6f6e 6c79 2066 6f72 2063  s are only for c
00000080: 6f6e 7665 6e69 656e 6365 2020 0a0a 6063  onvenience  ..`c
00000090: 6174 6020 636f 6e63 6174 656e 6174 6520  at` concatenate
```

`xxd info/syllabus.pdf | head` reveals `2550 4446` as the magic number for the pdf file

```bash 
~/Documents/linux-operating-systems main*
❯ xxd info/syllabus.pdf | head
00000000: 2550 4446 2d31 2e37 0d0a 25b5 b5b5 b50d  %PDF-1.7..%.....  
00000010: 0a31 2030 206f 626a 0d0a 3c3c 2f54 7970  .1 0 obj..<</Typ  
00000020: 652f 4361 7461 6c6f 672f 5061 6765 7320  e/Catalog/Pages          
00000030: 3220 3020 522f 4c61 6e67 2865 6e29 202f  2 0 R/Lang(en) /         
00000040: 5374 7275 6374 5472 6565 526f 6f74 2037  StructTreeRoot 7
00000050: 3020 3020 522f 4d61 726b 496e 666f 3c3c  0 0 R/MarkInfo<<
00000060: 2f4d 6172 6b65 6420 7472 7565 3e3e 2f4d  /Marked true>>/M
00000070: 6574 6164 6174 6120 3537 3720 3020 522f  etadata 577 0 R/
00000080: 5669 6577 6572 5072 6566 6572 656e 6365  ViewerPreference
00000090: 7320 3537 3820 3020 523e 3e0d 0a65 6e64  s 578 0 R>>..end
```

`xxd notes/image.png | head` reveals `8950 4e47` as the magic number for the png file

```bash
~/Documents/linux-operating-systems main*                        
❯ xxd notes/image.png
00000000: 8950 4e47 0d0a 1a0a 0000 000d 4948 4452  .PNG........IHDR   
00000010: 0000 0700 0000 0400 0806 0000 00e6 ff4d  ...............M
00000020: 8200 0000 0173 5247 4200 aece 1ce9 0000  .....sRGB.......
00000030: 0044 6558 4966 4d4d 002a 0000 0008 0001  .DeXIfMM.*......
00000040: 8769 0004 0000 0001 0000 001a 0000 0000  .i..............
00000050: 0003 a001 0003 0000 0001 0001 0000 a002  ................
00000060: 0004 0000 0001 0000 0700 a003 0004 0000  ................
etc
```

**magic numbers of various files**

| description | extension | magic number |
|:------------|:-----------|:-------------|
| adobe illustrator | `.ai` | `25 50 44 46 [%PDF]` |
| bitmap graphic | `.bmp` | `42 4d [BM]` |
| class file | `.class` | `CA FE BA BE` |
| jpeg graphics file | `.jpg` | `FFD8` |
| jpeg 2000 graphic file | `.jp2` | `0000000C6A5020200D0A [....jP..]` |
| gif graphic file | `.gif` | `47 49 46 38 [GIF89]` |
| tif graphic file | `.tif` | `49 49 [II]` |
| png graphic file | `.png` | `89 50 4E 47 .PNG` |

##  `cat`

`cat` concatenate files and print on the standard output

`$cat [option] FILE`

concatenate files to standard output

pertinent options include

`-A` will show you tabs and new lines

`cat 01-introduction.md`

```bash
~/Documents/linux-operating-systems/notes main*                  
❯ cat 01-introduction.md
#  linux operating systems

##  schedule

week 1: course introduction
week 2: linux help commands
week 3: linux file system commands
week 4: linux file processing commands
week 5: linux search commands
week 6: linux file permission commands
...
```

`cat -A 01-introduction.md`

```bash
~/Documents/linux-operating-systems/notes main*                     
❯ cat -A 01-introduction.md
#  linux operating systems$
$
##  schedule$
$
week 1: course introduction$
week 2: linux help commands$
week 3: linux file system commands$
week 4: linux file processing commands$
week 5: linux search commands$
week 6: linux file permission commands$
```

##  `zcat`

`zcat` `gzip`, `gunzip`, `zcat` compress or expand files

`$zcat [option] name FILE`

`zcat` uncompresses either a list of files on the command line or its standard input and writes the uncompressed data on standard output.  `zcat` will uncompress files that have the correct magic number whether they have a `.gz` suffix or not

##  `more` and `less`

most of the functionality is inside the program itself, once you start scrolling through a text file

you can use the `-N` option to see line numbers which can sometimes be helpful if you're diagnosing a problem with a script

when you're inside more or less, you can use the following commands to help you in scrolling 

`g` go to the top of the file

`G` go to the bottom of the file 

`/` highlight search results for the string that follow `/`

`&` only display search results for the string that follows `&`

`n` advance to next search terms

`N` return to previous search term

##  `head` and `tail`

`head` output the first part of files

print the first 10 lines of each file to standard output

`tail` output the last part of files

print the last 10 lines of each file to standard output

`$ head/tail [option] FILE`

pertinent options include

`-n` change the default number of lines printed

you can also combine the two commands, via pipe, to focus on text

##  `cp`

`cp` copy files and directories

description copy source to dest or multiple sources to directory

`$ cp [option] SOURCE DEST`

pertinent options include

`-b` make a backup of each existing destination file

`-r` copy directories recursively

`-u` copy only when the SOURCE file is newer than the destination file or when the destination file is missing

## `md5sum`

`md5sum` compute and check md5 message digest

print or che k md5 128-bit checksums

`$ md5sum [option] FILE`

pertinent options include

`-c` read md5 sums from the files and check them

##  `rm`

`rm` removes files or directories

`rm` removes each specified file.  by default, it does not remove directories

`$ rm [option] [FILE]`

pertinent options include

`-i` prompt before every removal

`-r` remove directories and their contents recursively

##  `mv`

`mv` move or rename files

rename source to destination or move sources to directory

`$mv [option] SOURCE DEST`

pertinent options include

`-b` make a backup of each existing destination file

`-u` copy only when the source file is newer than the destination file or when the destination file is missing

`mv info/syllabus.pdf notes`

```bash
~/Documents/linux-operating-systems main*
❯ l
total 24
drwxr-xr-x   7 owner  staff   224B Sep 16 22:30 .
drwx------@ 21 owner  staff   672B Sep 20 21:06 ..
-rw-r--r--@  1 owner  staff   6.0K Aug  8 18:55 .DS_Store
drwxr-xr-x  15 owner  staff   480B Sep 21 18:24 .git
-rw-r--r--@  1 owner  staff   722B Sep 16 17:20 README.md
drwxr-xr-x   3 owner  staff    96B Aug  8 18:55 info
drwxr-xr-x   7 owner  staff   224B Sep 16 22:30 notes

~/Documents/linux-operating-systems main*
❯ mv info/syllabus.pdf notes

~/Documents/linux-operating-systems main*
❯ cd notes

~/Documents/linux-operating-systems/notes main*
❯ l
total 7016
drwxr-xr-x  8 owner  staff   256B Sep 21 18:28 .
drwxr-xr-x  7 owner  staff   224B Sep 16 22:30 ..
-rw-r--r--  1 owner  staff   1.3K Sep  2 16:01 01-introduction.md
-rw-r--r--  1 owner  staff   4.1K Sep  2 16:01 02-help-commands.md
-rw-r--r--@ 1 owner  staff   7.3K Sep  8 13:35 03-file-system-directory.md
-rw-r--r--@ 1 owner  staff   7.7K Sep 21 18:27 04-file-processing-commands.md
-rw-r--r--@ 1 owner  staff   3.2M Dec 19  2023 image.png
-rw-r--r--@ 1 owner  staff   195K Aug  8 18:55 syllabus.pdf
```

##  `wc`

`wc`  print newline, word, and byte counts for each file

`$ wc [option] file`

print newline, word, and byte counts for each file, and a total line if more than one file is specified.  a word is a non zero length sequence of character delimited by white space.

pertinent options include

`-l` print the newline counts

`-m` print the character counts

`-w` print the word counts

`wc README.md`

```bash
~/Documents/linux-operating-systems main*
❯ wc README.md
      20      75     722 README.md
```

`wc notes/*`

```bash
~/Documents/linux-operating-systems main*
❯ wc notes/*
      44     224    1350 notes/01-introduction.md
     155     694    4237 notes/02-help-commands.md
     203    1215    7491 notes/03-file-system-directory.md
     316    1459    9411 notes/04-file-processing-commands.md
   11952   96526 3361523 notes/image.png
   12670  100118 3384012 total
```

##  assessment

question 1 -  how many text files are there in the `week4assessment` directory  

`$ ls week4assessment | wc -l` $\rightarrow$ `7`

answer 1 -  7

question 2 -  read `file1`.  what is the message?  

`$ cat file1` $\rightarrow$ `You're doing good so far, keep going.`

answer 2 -  `You're doing good so far, keep going.`

question 3 -  which of the text files in the `week4assessment` directory is the smallest?  

`$ ls -l week4assessment | sort -k 5` $\rightarrow$ `file2`

answer 3 -  `file2`

question 4 -  read the file identified in question 3.  what is the message?  

`$ cat file2` $\rightarrow$ `This really isn't much of a file.`

answer 4 -  `This really isn't much of a file.`

question 5 -  which of the following is the `md5` message digest of `file5` in the `week4assessment` directory?  

`$ md5sum file5` $\rightarrow$ `eae77731cf3ad3a33235e0b2011e4116 file5`

answer 5 -  `eae77731cf3ad3a33235e0b2011e4116`

question 6 -  which of the following is the largest file in the `week4assessment` directory?  

`$ ls -l week4assessment | sort -k 5` $\rightarrow$ `file6`

answer 6 -  `file6`

question 7 -  what is the file type of the file you identified in question 6?  

`$ file file6` $\rightarrow$ `ELF 32-bit LSB Executable`

answer 7 -  `ELF 32-bit LSB Executable`

question 8 -  how many words are in `file4` in the `week4assessment` directory?  

`$  wc -w file4` $\rightarrow$ `8 file4` 

answer 8 -  `8`

question 9 -  how many characters are in `file4` in the `week4assessment` directory?  

`$ wc -m file4` $\rightarrow$ `38 file4`

answer 9 -  `38`

question 10 -  read the first line in `/snap/core20/2318/usr/share/info/grep.info.gz`.  what version of `makeinfo` produced the file?

`$ zcat grep.info.gz | head -n 1` $\rightarrow$ `GNU makeinfo 6.15` 

answer 10 -  `GNU makeinfo 6.5` 