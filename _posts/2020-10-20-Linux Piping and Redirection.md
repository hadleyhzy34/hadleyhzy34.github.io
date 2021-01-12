---
layout: post
title: Linux Command Line - Piping and Redirection
key: 20201021
tags:
  - Linux
  - Ubuntu
  - Shell
---

## Redirecting to a file

save current command output to a file instead of printed to the screen.
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l > list
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cat list
total 16
-rw-rw-r-- 1 hadley hadley  230 Okt 21 22:08 data_test.txt
-rw-rw-r-- 1 hadley hadley  230 Okt 21 21:01 data.txt
-rwxrwxrwx 1 hadley hadley   92 Okt 20 21:28 file.txt
-rw-rw-r-- 1 hadley hadley    0 Okt 21 22:08 list
drwxrwxr-x 2 hadley hadley 4096 Okt 21 21:09 test1
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:42 test.cpp
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:01 ttt
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:42 x
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:43 x1
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:42 y
```
<!--more-->
If we redirect to a file which does not exist, it will be created automatically for us. If we save into a file which already exists, however, then it's contents will be cleared, then the new output saved to it.
{:.info}

* append new data to the end of current file

```bash
hadley@hadley-MacBookPro:~/Developments$ ls -l >> parentDirectory/data_test.txt 
hadley@hadley-MacBookPro:~/Developments$ cat parentDirectory/data_test.txt 
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
test.\test[ss]
aaabbbbccdddddeee
total 220
drwxrwxr-x 20 hadley hadley   4096 Okt 18 12:48 data_structure_and_algorithm
drwxrwxr-x 17 hadley hadley   4096 Okt 18 11:15 Hadleyhzy.github.io
drwxr--r--  3 hadley hadley   4096 Okt 21 22:08 parentDirectory
-rwxrwxr-x  1 hadley hadley 207288 Okt 21 09:23 test
-rw-rw-r--  1 hadley hadley    289 Okt 21 09:23 test.cpp
```

* send data the other way

A lot of programs (as we've seen in previous sections) allow us to supply a file as a command line argument and it will read and process the contents of that file. Given this, you may be asking why we would need to use this operator. The above example illustrates a subtle but useful difference. You'll notice that when we ran wc supplying the file to process as a command line argument, the output from the program included the name of the file that was processed. When we ran it redirecting the contents of the file into wc the file name was not printed. This is because whenever we use redirection or piping, the data is sent anonymously. So in the above example, wc recieved some content to process, but it has no knowledge of where it came from so it may not print this information. As a result, this mechanism is often used in order to get ancillary data (which may not be required) to not be printed.
{:.info}

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ wc -l <data.txt 
14
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ wc -l < data.txt >ttest
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cat ttest 
14
```
## Redirecting STDERR

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l test.h
ls: cannot access 'test.h': No such file or directory
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l test.h>errors.txt
ls: cannot access 'test.h': No such file or directory
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cat errors.txt 
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l test.h 2>errors.txt
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cat errors.txt 
ls: cannot access 'test.h': No such file or directory
```

Now let's look at the third stream which is Standard Error or STDERR. The three streams actually have numbers associated with them (in brackets in the list at the top of the page). STDERR is stream number 2 and we may use these numbers to identify the streams. If we place a number before the > operator then it will redirect that stream (if we don't use a number, like we have been doing so far, then it defaults to stream 1).
{:.info}


Maybe we wish to save both normal output and error messages into a single file. This can be done by redirecting the STDERR stream to the STDOUT stream and redirecting STDOUT to a file. We redirect to a file first then redirect the error stream. We identify the redirection to a stream by placing an & in front of the stream number (otherwise it would redirect to a file called 1).
{:.info}

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l test.cpp test.h >myoutput 2>&1
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ cat myoutput 
ls: cannot access 'test.h': No such file or directory
-rw-rw-r-- 1 hadley hadley 0 Okt 20 21:42 test.cpp
```

## Piping

Now we'll take a look at a mechanism for sending data from one program to another. It's called piping and the operator we use is ( | ) (found above the backslash ( \ ) key on most keyboards). What this operator does is feed the output from the program on the left as input to the program on the right. In the example below we will list only the first 3 files in the directory.
{:.info}


```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls | head -3
data.txt
errors.txt
file.txt
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls | head -3 | tail -1
file.txt
```






































