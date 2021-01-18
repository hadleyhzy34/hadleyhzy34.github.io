---
layout: post
title: GDB Tutorial
key: 20201127
categories: 
  - C++
tags:
  - C++
  - vim
  - GDB
  - debugging
  - linux
---

### getting started

* compile

1. C++

``` terminal
g++ -g main.cpp -o main
```

2. C

``` terminal

```



* loading a program to debug

```terminal
gdb <executable_file_name>
```

``` terminal
Hadleys-MacBook-Pro:gdb hadley$ gdb main
GNU gdb (GDB) 10.1
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-apple-darwin18.7.0".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from main...
Reading symbols from /Users/hadley/Development/gdb/main.dSYM/Contents/Resources/DWARF/main...
```

* run the program

```terminal
run
```

```terminal
(gdb) run
Starting program: /Users/hadley/Development/gdb/main 
Unable to find Mach task port for process-id 774: (os/kern) failure (0x5).
 (please check gdb is codesigned - see taskgated(8))
```
{:.warning}

Solution:

Codesigning requires a certificate. The following procedure explains how to create one and apply it to gdb:

* Start the Keychain Access application (in /Applications/Utilities/Keychain Access.app)
* Select the Keychain Access -> Certificate Assistant -> Create a Certificate... menu
Then:
* Choose a name for the new certificate (this procedure will use "gdb-cert" as an example)
* Set "Identity Type" to "Self Signed Root"
* Set "Certificate Type" to "Code Signing"
* Activate the "Let me override defaults" option
* Click several times on "Continue" until the "Specify a Location For The Certificate" screen appears, then set "Keychain" to "System"
* Click on "Continue" until the certificate is created
* Finally, in the view, double-click on the new certificate, and set "When using this certificate" to "Always Trust"
* Exit the Keychain Access application and restart the computer (this is unfortunately required)
* Once a certificate has been created, the debugger can be codesigned as follow. In a Terminal, run the following command:
( $ codesign -fs gdb-cert /usr/local/bin/gdb
* where "gdb-cert" should be replaced by the actual certificate name chosen above.
* When run as sudo, gdb will no longer report the taskgated error.
{:.info}


Conditional Breakpoints:

```terminal
(gdb) break fun2
Breakpoint 1 at 0x100000cdf: file main.cpp, line 10.
```



g++ -std=c++17 -O2 -Wall -pedantic -pthread main.cpp -o main && ./main

11 14

<!--more-->

cpp reference


cplusplus.com

sharedptr



    





