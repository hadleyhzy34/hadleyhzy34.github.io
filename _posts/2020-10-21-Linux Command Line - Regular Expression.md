---
layout: post
title: Linux Command Line - Regular Expressions
key: 20201021
tags:
  - Linux
  - Ubuntu
  - Shell
---

## Egrep
egrep is a program which will search a given set of data and print every line which contains a given pattern. It is an extension of a program called grep. It's name is odd but based upon a command which did a similar function, in a text editor called ed. It has many command line options which modify it's behaviour so it's worth checking out it's man page. ie the -v option tells grep to instead print every line which does not match the pattern.

``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ egrep 'mellon' data.txt 
Mark watermellons 12
Oliver rockmellons 2
```

`-v` to tells egrep to instread print every line which does not match the pattern

<!--more-->

``` bash 
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ egrep -v 'mellon' data.txt 
Fred apples 20
Susy oranges 5
Robert pears 4
Terry oranges 9
Lisa peaches 7
Susy oranges 12
Mark grapes 39
Anne mangoes 7
Greg pineapples 3
Betty limes 14
```
check their line number as well

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ egrep -n 'mellon' data.txt 
3:Mark watermellons 12
11:Oliver rockmellons 2
```

check how many lines did match

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ egrep -c 'mellon' data.txt 
2
```

Regular expression overview

identify any line with two or more vowels in a row

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ egrep '[aeiou]{1,}' data.txt 
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
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ egrep '[aeiou]{2,}' data.txt 
Robert pears 4
Lisa peaches 7
Anne mangoes 7
Greg pineapples 3
```

any line with a 2 on it which is not the end of the line
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ egrep '1.+' data.txt 
Mark watermellons 12
Susy oranges 12
Betty limes 14
```

* $ - matches the end of the line.
* ^ - matches the beginning of the line.

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ egrep '2$' data.txt 
Mark watermellons 12
Susy oranges 12
Oliver rockmellons 2
```

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ egrep '^F' data.txt 
Fred apples 20
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ egrep '^[A-D]' data.txt 
Anne mangoes 7
Betty limes 14
```


each line which contains either 'Fred' or 'Robert' or 'Susy'
``` bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ egrep 'Fred|Robert|Susy' data.txt 
Fred apples 20
Susy oranges 5
Robert pears 4
Susy oranges 12
```

## grep

``` bash
grep [options] pattern [files]
```
Note that if pattern does not include spaces or any other special characters then you don't need to use quotes
{".info}

* -i: Ignored, case for matching

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -i "fred" data.txt 
Fred apples 20
```

* -c : this prints only a count of the lines that match a pattern

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -c "oranges" data.txt 
3
```

* -l : display list of a filenames only, we can just display the files that contains the given string/pattern
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -l "apple" data.txt 
data.txt
```
search all files in current directory:
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -l "Fred" *
data.txt
grep: test1: Is a directory
```


* -w : display only the matched pattern, by default, grep displays the entire line which has the matched string.

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -l "apple" data.txt 
data.txt
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -w "apple" data.txt 
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -w "apples" data.txt 
Fred apples 20
```
* -o : displays only the matched string by using the -o option
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -o "Fred" 
data.txt:Fred
```
* -n : show line number while displaying the output

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -n "oranges" data.txt 
2:Susy oranges 5
5:Terry oranges 9
7:Susy oranges 12
```

* -v : displays lines that are not matched with the specified search string pattern

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -v "^[A-K]" data.txt 
Susy oranges 5
Mark watermellons 12
Robert pears 4
Terry oranges 9
Lisa peaches 7
Susy oranges 12
Mark grapes 39
Oliver rockmellons 2
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep "^[M-Z]" data.txt 
Susy oranges 5
Mark watermellons 12
Robert pears 4
Terry oranges 9
Susy oranges 12
Mark grapes 39
Oliver rockmellons 2
```

showing lines that end with a string
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep "2$" data.txt 
Mark watermellons 12
Susy oranges 12
Oliver rockmellons 2
```

* -e : specifies expression with -e option, can use multiple times:
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -e "Fred" -e "Mark" data.txt 
Fred apples 20
Mark watermellons 12
Mark grapes 39
```

Display directories:
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l | grep "^d"
drwxrwxr-x 2 hadley hadley 4096 Okt 20 21:33 test1
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l | grep "^-"
-rw-rw-r-- 1 hadley hadley  197 Okt 21 19:51 data.txt
-rwxrwxrwx 1 hadley hadley   92 Okt 20 21:28 file.txt
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:42 test.cpp
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:01 ttt
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:42 x
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:43 x1
-rw-rw-r-- 1 hadley hadley    0 Okt 20 21:42 y
```

* `^` : use `^` with `[]`, the pattern must not contain any character in the set specified

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep "^[^A-K]" data.txt 
Susy oranges 5
Mark watermellons 12
Robert pears 4
Terry oranges 9
Lisa peaches 7
Susy oranges 12
Mark grapes 39
Oliver rockmellons 2
```

`.` to match any one character

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep "pears.4" data.txt 
Robert pears 4
```

`\` to ignore the special meaning of the character following it
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep 'test\.\\test\[ss\]' data.txt 
test.\test[ss]
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -F "test.\test[ss]" data.txt 
test.\test[ss]
```


`*` : zero or more occurrences of the previous character

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep "a*b*c*d*e" data.txt 
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
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep "aaab*c*d*e" data.txt 
aaabbbbccdddddeee
```
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep Betty *.txt
data.txt:Betty limes 14
```

Note the difference between `*` in pattern and `*` in files.
{:.warning}

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep "*tt" data.txt 
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep "tt" data.txt 
Betty limes 14
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep "B*tt" data.txt 
Betty limes 14
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep tt *.txt
data.txt:Betty limes 14
```


check how many processed are running on your system as youtube-music
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ps -ef | grep -c youtube-music
11
```

* Recursive Search

search all files inside current directory:
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -r Betty *
data.txt:Betty limes 14
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ ls -l test1/
total 4
-rw-rw-r-- 1 hadley hadley 230 Okt 21 21:09 data.txt
-rw-rw-r-- 1 hadley hadley   0 Okt 20 19:59 test1.txt
-rw-rw-r-- 1 hadley hadley   0 Okt 20 20:03 test2.txt
-rw-rw-r-- 1 hadley hadley   0 Okt 20 21:32 test3.cpp
-rw-rw-r-- 1 hadley hadley   0 Okt 20 21:33 test4.py
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -r Betty *
data.txt:Betty limes 14
test1/data.txt:Betty limes 14
```

search files with certain extension:
`grep -inr --include=\*.extension 'searchterm' ./`

* -r: recursively

* -i: ignore-case

* -n: each output line is preceded by its relative line number in the file

* --include: all `*.txt`: text files

* ./: Start at current directory.

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -inr --include=*.txt 'Betty' ./
./test1/data.txt:12:Betty limes 14
./data.txt:12:Betty limes 14
```

Note difference below:
{:.warning}


Note the difference between `-r` and `-R` and difinition of symbolic links:

https://linuxize.com/post/how-to-use-grep-command-to-search-files-in-linux/

```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -r Betty *
data.txt:Betty limes 14
test1/data.txt:Betty limes 14
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -r Betty *.txt
data.txt:Betty limes 14
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ grep -r Betty .
./test1/data.txt:Betty limes 14
./data.txt:Betty limes 14
```
search file name with certain extension recursively:
```bash
hadley@hadley-MacBookPro:~/Developments/parentDirectory$ find . -iname '*.txt'
./file.txt
./test1/test2.txt
./test1/test1.txt
./test1/data.txt
./data.txt
```

Note that iname does a case insensitive search.





































































