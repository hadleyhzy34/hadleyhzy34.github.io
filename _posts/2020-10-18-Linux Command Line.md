---
layout: post
title: Linux Command Line
key: 20201018
tags:
  - Linux
  - Ubuntu
  - Shell
---


## Basic Command Line

### The Shell, Bash
Shell is a program that takes commands from the keyboard and gives them to the operating system to perform.
If you would like to know which shell you are using you may use a command called `echo` to display a system variable stating your current shell.

``` bash
hadley@hadley-MacBookPro:~$ echo $SHELL
/bin/bash
```

### pwd
``` bash
hadley@hadley-MacBookPro:~$ pwd
/home/hadley
```
<!--more-->

### ls
To list the contents of your current working directory:  
``` bash
hadley@hadley-MacBookPro:~/Developments$ ls
data_structure_and_algorithm  Hadleyhzy.github.io
```

To list the contents of desired working directory:
```bash
hadley@hadley-MacBookPro:~/Developments$ ls /home
hadley
```
Hidden Files:
```bash
hadley@hadley-MacBookPro:~/Developments$ ls -a
.  ..  data_structure_and_algorithm  Hadleyhzy.github.io
```

Hidden Files without `.` and `..` directory in the list:
```bash
hadley@hadley-MacBookPro:~/Developments/Hadleyhzy.github.io$ ls -A
404.html          .eslintrc                  LICENSE            screenshot.png
about.md          favicon.ico                node_modules       
```

Enable and Disable colored output:
You can enable and disable the colored output of the ls command using the –color option. The –color option takes 3 values, never, always and auto.

Long listing format of ls:
``` bash
hadley@hadley-MacBookPro:~/Developments$ ls -l
total 8
drwxrwxr-x 20 hadley hadley 4096 Okt 18 12:48 data_structure_and_algorithm
drwxrwxr-x 17 hadley hadley 4096 Okt 18 11:15 Hadleyhzy.github.io
```

* First character indicates whether it is a normal file ( - ) or directory ( d ).
* Next 9 characters are permissions for the file or directory. 
* The next field is the number of blocks. 
* The next field is the owner of the file or directory.
* The next field is the group the file or directory belongs to (users in this case).
* Following this is the file size(default size should be bytes).
* Next up is the file modification time.
* Finally we have the actual name of the file or directory.

Changin file size unit in long listing format:
``` bash
hadley@hadley-MacBookPro:~/Documents/test6$ ls -l --block-size=k
total 44K
-rwxrwxr-x 1 hadley hadley 38K Okt 10 22:57 main
-rw-rw-r-- 1 hadley hadley  1K Okt 10 22:55 main.cpp
hadley@hadley-MacBookPro:~/Documents/test6$ ls -l --block-size=M
total 1M
-rwxrwxr-x 1 hadley hadley 1M Okt 10 22:57 main
-rw-rw-r-- 1 hadley hadley 1M Okt 10 22:55 main.cpp
hadley@hadley-MacBookPro:~/Documents/test6$ ls -l --block-size=G
total 1G
-rwxrwxr-x 1 hadley hadley 1G Okt 10 22:57 main
-rw-rw-r-- 1 hadley hadley 1G Okt 10 22:55 main.cpp
```
Printing human readable file size in long listing format:
``` bash
hadley@hadley-MacBookPro:~/Documents/test6$ ls -lh
total 44K
-rwxrwxr-x 1 hadley hadley 38K Okt 10 22:57 main
-rw-rw-r-- 1 hadley hadley 198 Okt 10 22:55 main.cpp
```
Getting help:
```bash
hadley@hadley-MacBookPro:~/Documents/test6$ man ls
```

### Paths
Absolute paths specify a location (file or directory) in relation to the root directory. You can identify them easily as they always begin with a forward slash ( / )

Relative paths specify a location (file or directory) in relation to where we currently are in the system. They will not begin with a slash.

#### More on path
``` bash
hadley@hadley-MacBookPro:~$ cd ~
hadley@hadley-MacBookPro:~$ pwd
/home/hadley
hadley@hadley-MacBookPro:~$ ls ./Books/
Modern+Operating+Systems+4th@www.java1234.com.pdf
hadley@hadley-MacBookPro:~$ ls ./Books/../
Books    Developments  Downloads  Pictures  snap       Videos
Desktop  Documents     Music      Public    Templates
```

#### home directory and root directory
``` bash
hadley@hadley-MacBookPro:~$ pwd
/home/hadley
hadley@hadley-MacBookPro:~$ ls ../../
bin    cdrom  home   lib64       media  proc  sbin  sys  var
boot   dev    lib    libx32      mnt    root  snap  tmp
build  etc    lib32  lost+found  opt    run   srv   usr
hadley@hadley-MacBookPro:~$ ls /
bin    cdrom  home   lib64       media  proc  sbin  sys  var
boot   dev    lib    libx32      mnt    root  snap  tmp
build  etc    lib32  lost+found  opt    run   srv   usr
```
If you run the command cd without any arguments then it will always take you back to your home directory.
``` bash
hadley@hadley-MacBookPro:~/Documents$ pwd
/home/hadley/Documents
hadley@hadley-MacBookPro:~/Documents$ cd 
hadley@hadley-MacBookPro:~$ pwd
/home/hadley
```

### Special folders
* /etc - Stores config files for the system.
* /var/log - Stores log files for various system programs. (You may not have permission to look at everything in this directory. Don't let that stop you exploring though. A few error messages never hurt anyone.)
* /bin - The location of several commonly used programs (some of which we will learn about in the rest of this tutorial.
* /usr/bin - Another location for programs on the system.


## Files
Everything is a file
A text file is a file, a directory file, your keyboard is a file, your monitor is a file. Under linux system, it igonres the extension and looks inside the file to determine what type of file it is. `file` command can be used to find certain type of file is.

``` bash
hadley@hadley-MacBookPro:~/Developments$ file Hadleyhzy.github.io/
Hadleyhzy.github.io/: directory
hadley@hadley-MacBookPro:~/Developments$ file Hadleyhzy.github.io/index.html 
Hadleyhzy.github.io/index.html: UTF-8 Unicode text
hadley@hadley-MacBookPro:~/Developments$ file data_structure_and_algorithm/array/leetcode_array/283_move_zeros.cpp 
data_structure_and_algorithm/array/leetcode_array/283_move_zeros.cpp: C++ source, UTF-8 Unicode text
```

Deal with spaces in names  
* Quotes  
* Escape Characters  
``` bash
hadley@hadley-MacBookPro:~/Developments$ cd 'holiday photos'
hadley@hadley-MacBookPro:~/Developments/holiday photos$ pwd
/home/hadley/Developments/holiday photos
hadley@hadley-MacBookPro:~/Developments/holiday photos$ cd ..
hadley@hadley-MacBookPro:~/Developments$ cd holiday\ photos
hadley@hadley-MacBookPro:~/Developments/holiday photos$ pwd
/home/hadley/Developments/holiday photos
```

Manual Pages to explain every command available on your system.
``` bash
hadley@hadley-MacBookPro:~$ man ls
LS(1)                            User Commands                           LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List  information  about  the FILEs (the current directory by default).
       Sort entries alphabetically if none of -cftuvSUX nor --sort  is  speci‐
       fied.

       Mandatory  arguments  to  long  options are mandatory for short options
       too.

       -a, --all
              do not ignore entries starting with .

       -A, --almost-all
              do not list implied . and ..
```

## File Manipulation
`mkdir` `rmdir` `touch` `cp` `mv` `rm`

### Making a directory
`-p` Making parent directories

``` bash
hadley@hadley-MacBookPro:~/Developments$ mkdir -p parentDirectory/test
hadley@hadley-MacBookPro:~/Developments$ ls -l
total 36
drwxrwxr-x 20 hadley hadley  4096 Okt 18 12:48 data_structure_and_algorithm
drwxrwxr-x 17 hadley hadley  4096 Okt 18 11:15 Hadleyhzy.github.io
drwxrwxr-x  3 hadley hadley  4096 Okt 20 19:48 parentDirectory
-rwxrwxr-x  1 hadley hadley 17680 Okt 19 14:34 test
-rw-rw-r--  1 hadley hadley   206 Okt 19 14:33 test.cpp
```

`-v`  Print a message for each created directory

``` bash
hadley@hadley-MacBookPro:~/Developments$ mkdir -pv pDirectory/test
mkdir: created directory 'pDirectory'
mkdir: created directory 'pDirectory/test'
```
Removing a directory, directory must be empty before it maybe removed

``` bash
hadley@hadley-MacBookPro:~/Developments$ rmdir -pv pDirectory/test
rmdir: removing directory, 'pDirectory/test'
rmdir: removing directory, 'pDirectory'
```

Creating a Blank File

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test$ touch test.txt
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test$ ls
test.txt
```


Copying a file

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test$ cp test.txt test1.txt
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test$ ls
test1.txt  test.txt
```

Copying a directory

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cp test test1
cp: -r not specified; omitting directory 'test'
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls
test
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cp -r test test1
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls
test  test1
```

Moving a file:

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ mv test/test2.txt test1/
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cd test1/
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test1$ ls
test1.txt  test2.txt  test.txt
```

Moving a Directory

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ mv test test1/
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cd test1/
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test1$ ls
test  test1.txt  test2.txt  test.txt
```
Renaming Files and Directories

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test1$ mv test test_x
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test1$ ls
test1.txt  test2.txt  test.txt  test_x
```

Removing a file and non empty Directories

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test1$ rm test.txt 
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test1$ ls
test1.txt  test2.txt  test_x
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test1$ rm -r test_x
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test1$ ls
test1.txt  test2.txt
```

### Vi Text Editor

* `ZZ` - Save and exit
* `:q!` - discard all changes since the last save and exit
* `:w` - save file but don't exit
* `:wq` - again, save and exit

`cat` vs `less`: less for smaller files and less for larger files

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cat file.txt 
asfsaf
asfasfd
:x
sfsafaf

asfsafaf
```
* `nG` - move to the nth line
* `G` - move to the last line
* `w` - move to the beginning of the next word
* `nw` - move forward n word
* `b` - move to the beginning of the previous word
* `nb` - move back n word
* `{` - move backward one paragraph
* `}` - move forward one paragraph


* `x` - delete a single character
* `nx` - delete n characters
* `dd` - delete the current line
* `dn` - d followed by a movement command

### display/hide line numbers

1. create ~/.exrc
2. add `set number` or `set nonumber`


### Wild Cards

1. `*`

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test1$ ls
test1.txt  test2.txt  test3.cpp  test4.py
hadley@hadley-MacBookPro:~/Developments/parentDirectory/test1$ ls *.txt
test1.txt  test2.txt
```

It is actually bash (The program that provides the command line interface) that does the translation for us. When we offer it this command it sees that we have used wildcards and so, before running the command ( in this case ls ) it replaces the pattern with every file or directory (ie path) that matches that pattern. We issue the command:

* ls b*
Then the system translates this into:

* ls barry.txt blah.txt bob

2. `?`

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls
file.txt  test1  ttt
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls *.???
file.txt
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls ?i*
file.txt
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls */
test1.txt  test2.txt  test3.cpp  test4.py
```

3. `[]`

* looking for everyfile whose name either begins with x or y.

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls
file.txt  test1  test.cpp  ttt  x  y
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls [xy]*
x  y
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls [x-y]*
x  x1  y
```

* find file whose name includes a digit in it 

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls *[0-9]*
x1

test1:
test1.txt  test2.txt  test3.cpp  test4.py
```

* look for any character which is not one of the following

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls
file.txt  test1  test.cpp  ttt  x  x1  y
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls [^a-x]*
y
```
* find file type in a directory

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ file *
file.txt: ASCII text
test1:    directory
test.cpp: empty
ttt:      empty
x:        empty
x1:       empty
y:        empty
```

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -lh /home/*/.bash_history
-rw------- 1 hadley hadley 9,3K Okt 20 21:14 /home/hadley/.bash_history
```

Note that .bash_history is a file in a typical users home directory that keeps a history of commands the user has entered on the command line.
``` bash
less ~/.bash_history
```
{:.info}










































