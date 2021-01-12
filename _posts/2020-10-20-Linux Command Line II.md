---
layout: post
title: Linux Command Line II
key: 20201020
tags:
  - Linux
  - Ubuntu
  - Shell
---


## Permissions

### view permissions

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l
total 8
-rw-rw-r-- 1 hadley hadley   92 Okt 20 21:28 file.txt
drwxrwxr-x 2 hadley hadley 4096 Okt 20 21:33 test1
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:42 test.cpp
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:01 ttt
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:42 x
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:43 x1
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:42 y
```
* The first character identifies the file type. If it is a dash ( - ) then it is a normal file. If it is a d then it is a directory.
* The following 3 characters represent the permissions for the owner. A letter represents the presence of a permission and a dash ( - ) represents the absence of a permission. In this example the owner has all permissions (read, write and execute).
* The following 3 characters represent the permissions for the group. In this example the group has the ability to read but not write or execute. Note that the order of permissions is always read, then write then execute.
* Finally the last 3 characters represent the permissions for others (or everyone else). In this example they have the execute permission and nothing else.
<!--more-->
### change permissions

Grant execute permission to the user:

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ chmod u+x file.txt 
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l
total 8
-rwxrw-r-- 1 hadley hadley   92 Okt 20 21:28 file.txt
```

Remove write permission to the group:
``` bash
adley@hadley-MacBookPro:~/Developments/parentDirectory$ chmod g-w file.txt 
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l
total 8
-rwxr--r-- 1 hadley hadley   92 Okt 20 21:28 file.txt
```


Setting permissions shorthand:

| Octal         | Binary        | 
| ------------- |:-------------:| 
| 0             | 000           | 
| 1             | 001           |
| 2             | 010           |   
| 3             | 011           |   
| 4             | 100           |   
| 5             | 101           |   
| 6             | 110           |   
| 7             | 111           |   

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ chmod 777 file.txt 
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l
total 8
-rwxrwxrwx 1 hadley hadley   92 Okt 20 21:28 file.txt
```

Permissions for directories
* r - you have the ability to read the contents of the directory (ie do an ls)
* w - you have the ability to write into the directory (ie create files and directories)
* x - you have the ability to enter that directory (ie cd)

``` bash
hadley@hadley-MacBookPro:~/Developments$ ls parentDirectory
file.txt  test1  test.cpp  ttt  x  x1  y
```

``` bash
hadley@hadley-MacBookPro:~/Developments$ chmod 400 parentDirectory
hadley@hadley-MacBookPro:~/Developments$ ls -ld parentDirectory
dr-------- 3 hadley hadley 4096 Okt 20 21:43 parentDirectory
hadley@hadley-MacBookPro:~/Developments$ cd parentDirectory
bash: cd: parentDirectory: Permission denied
hadley@hadley-MacBookPro:~/Developments$ ls parentDirectory
file.txt  test1  test.cpp  ttt  x  x1  y
```

``` bash
hadley@hadley-MacBookPro:~/Developments$ chmod 100 parentDirectory
hadley@hadley-MacBookPro:~/Developments$ ls -ld parentDirectory
d--x------ 3 hadley hadley 4096 Okt 20 21:43 parentDirectory
hadley@hadley-MacBookPro:~/Developments$ ls parentDirectory
ls: cannot open directory 'parentDirectory': Permission denied
hadley@hadley-MacBookPro:~/Developments$ cd parentDirectory
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ pwd
/home/hadley/Developments/parentDirectory
```

You may have a directory which you don't have the read permission for. It may have files within it which you do have the read permission for. As long as you know the file exists and it's name you can still read the file.

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cat file.txt
asfsaf
asfasfd
:x
sfsafaf
```


## Filters

### Head
Head is a program that prints the first so many lines of it's input. By default it will print the first 10 lines but we may modify this with a command line argument.

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ head data.txt 
Fred apples 20
Susy oranges 5
Mark watermellons 12
Robert pears 4
Terry oranges 9
Lisa peaches 7
Susy oranges 12
Mark grapes 39
Anne mangoes 7
Greg pineapples 3
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ head -3 data.txt 
Fred apples 20
Susy oranges 5
Mark watermellons 12
```

### Tail
Tail is the opposite of head. Tail is a program that prints the last so many lines of it's input. By default it will print the last 10 lines but we may modify this with a command line argument.

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ tail data.txt 
Mark watermellons 12
Robert pears 4
Terry oranges 9
Lisa peaches 7
Susy oranges 12
Mark grapes 39
Anne mangoes 7
Greg pineapples 3
Oliver rockmellons 2
Betty limes 14
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ tail -3 data.txt 
Greg pineapples 3
Oliver rockmellons 2
Betty limes 14
```

-n, --lines=[+]NUM
              output the last NUM lines, instead of the last 10; or use -n +NUM to  output  starting  with
              line NUM

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cat -n data.txt 
     1  Fred apples 20
     2  Susy oranges 5
     3  Mark watermellons 12
     4  Robert pears 4
     5  Terry oranges 9
     6  Lisa peaches 7
     7  Susy oranges 12
     8  Mark grapes 39
     9  Anne mangoes 7
    10  Greg pineapples 3
    11  Oliver rockmellons 2
    12  Betty limes 14
    13  test.\test[ss]
    14  aaabbbbccdddddeee
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ tail -n +10 data.txt 
Greg pineapples 3
Oliver rockmellons 2
Betty limes 14
test.\test[ss]
aaabbbbccdddddeee
```


### Sort

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ sort data.txt 
Anne mangoes 7
Betty limes 14
Fred apples 20
Greg pineapples 3
Lisa peaches 7
Mark grapes 39
Mark watermellons 12
Oliver rockmellons 2
Robert pears 4
Susy oranges 12
Susy oranges 5
Terry oranges 9
```

### nl

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ nl -s '.*' -w 3 data.txt
  1.*Fred apples 20
  2.*Susy oranges 5
  3.*Mark watermellons 12
  4.*Robert pears 4
  5.*Terry oranges 9
  6.*Lisa peaches 7
  7.*Susy oranges 12
  8.*Mark grapes 39
  9.*Anne mangoes 7
 10.*Greg pineapples 3
 11.*Oliver rockmellons 2
 12.*Betty limes 14
```

### wc

-l give number of lines, -w give number of words

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ wc -l data.txt 
12 data.txt
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ wc -lw data.txt 
 12  36 data.txt

```

show number of files in current directory:
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l | wc -l
9
```

### cut

cut defaults to using the TAB character as a separator to identify fields. In our file we have used a single space instead so we need to tell cut to use that instead. The separator character may be anything you like, for instance in a CSV file the separator is typically a comma ( , ). This is what the -d option does (we include the space within single quotes so it knows this is part of the argument). The -f option allows us to specify which field or fields we would like. If we wanted 2 or more fields then we separate them with a comma as below.

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cut -f 1,2 -d ' ' data.txt 
Fred apples
Susy oranges
Mark watermellons
Robert pears
Terry oranges
Lisa peaches
Susy oranges
Mark grapes
Anne mangoes
Greg pineapples
Oliver rockmellons
Betty limes
```

### sed
The initial s stands for substitute and specifies the action to perform (there are others but for now we'll keep it simple). Then between the first and second slashes ( / ) we place what it is we are searching for. Then between the second and third slashes, what it is we wish to replace it with. The g at the end stands for global and is optional. If we omit it then it will only replace the first instance of search on each line. With the g option we will replace every instance of search that is on each line. Let's see an example. Say we ran out of oranges and wanted to instead give those people bananas.


``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ sed 's/watermellons/test/g' data.txt 
Fred apples 20
Susy oranges 5
Mark test 12
Robert pears 4
Terry oranges 9
Lisa peaches 7
Susy oranges 12
Mark grapes 39
Anne mangoes 7
Greg pineapples 3
Oliver rockmellons 2
Betty limes 14
```

### uniq

uniq stands for unique and it's job is to remove duplicate lines from the data. One limitation however is that those lines must be adjacent (ie, one after the other). 


```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cat data.txt 
Fred apples 20
Susy oranges 5
Mark watermellons 12
Robert pears 4
Terry oranges 9
Lisa peaches 7
Susy oranges 12
Mark grapes 39
Anne mangoes 7
Greg pineapples 3
Oliver rockmellons 2
Betty limes 14
Betty limes 14
Betty limes 14
Betty limes 14
Betty limes 14
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ uniq data.txt 
Fred apples 20
Susy oranges 5
Mark watermellons 12
Robert pears 4
Terry oranges 9
Lisa peaches 7
Susy oranges 12
Mark grapes 39
Anne mangoes 7
Greg pineapples 3
Oliver rockmellons 2
Betty limes 14
```

### tac
Linux guys are known for having a funny sense of humor. The program tac is actually cat in reverse. It was named this as it does the opposite of cat. Given data it will print the last line first, through to the first line.

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ tac data.txt 
Betty limes 14
Oliver rockmellons 2
Greg pineapples 3
Anne mangoes 7
Mark grapes 39
Susy oranges 12
Lisa peaches 7
Terry oranges 9
Robert pears 4
Mark watermellons 12
Susy oranges 5
Fred apples 20
```

### diff
https://www.geeksforgeeks.org/diff-command-linux-examples/

































