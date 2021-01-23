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

### gdb installations

* Linux

```terminal
apt-get install gdb
```

* Mac OS

``` terminal
brew install gdb
```

### loading a program to debug

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

Q:A
{:.warning}

#### Problem

```terminal
(gdb) run
Starting program: /Users/hadley/Development/gdb/main 
Unable to find Mach task port for process-id 774: (os/kern) failure (0x5).
 (please check gdb is codesigned - see taskgated(8))
```
{:.warning}

#### Solution

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


### source code

``` c++
#include <iostream>
#include <vector>
using namespace std;

void func1(){
    int variable1 = 10;
    cout<<variable1<<endl;
}

void func2(){
    int variable2 = 20;
    cout<<variable2<<endl;
}

int main(){
    vector<int> array(5);
    //cout<<"test"<<array[10]<<endl;
    cout<<array.max_size()<<endl;
    cout<<"the current array size is: "<<array.size()<<endl;
    cout<<"test for index out of range "<<array[-1]<<" "<<&array[-1]<<endl;
    for(int i=0;i<20;i++){
  cout<<i<<"test "<<array[i]<<&array[i]<<endl;
    }
    for(int i=0;i<6;i++){
  array[i]=i;
  cout<<i<<" "<<array[i]<<endl;
    }
    func1();
    func2();
    for(int i=0;i<20;i++){
  cout<<"the current variable i is: "<<i<<endl;
    }
    int variable_main = 20;
    cout<<variable_main<<endl;
}
```



### commands 

#### start debugging

```terminal
(gdb) start
Temporary breakpoint 1 at 0x5555555551e5: file main.cpp, line 9.
Starting program: /home/hadley/Developments/gdb/main 

Temporary breakpoint 1, main () at main.cpp:9
9	int main(){
```

#### step `n` and `step + number_of_steps`  

`next` won't jump into functions, but if function name is set to be break point, then `next` will still jump into functions:

``` terminal
(gdb) n
10	    func1();
(gdb) n
10
11	    int variable_main = 20;
```

`step` jump into functions:

``` terminal
(gdb) step 
12		cout<<"the current variable i is: "<<i<<endl;
(gdb) step
the current variable i is: 6
11	    for(int i=0;i<20;i++){
(gdb) step 2
the current variable i is: 7
11	    for(int i=0;i<20;i++){
(gdb) step 2
the current variable i is: 8
11	    for(int i=0;i<20;i++){
```


#### breakpoint debugging  

* breakpoint + lineNumber/func_name

``` terminal
(gdb) b 4
Breakpoint 5 at 0x5555555551a9: file main.cpp, line 4.
(gdb) b func1
Breakpoint 2 at 0x5555555551c9: file main.cpp, line 4.
```

* conditional breakpoint

`break + lineNumber/func_name if + expression`

``` terminal
(gdb) break 28 if array[1]==1
Breakpoint 1 at 0x1592: file main.cpp, line 28.
```

It means if vector array element at index 1 is 1, then program stops right before line 28.
{:.info}

``` terminal
(gdb) i b
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x0000555555555592 in main() at main.cpp:28
  stop only if array[1]==1
  breakpoint already hit 1 time
```


* hit breakpoint

1. start the program

``` terminal
(gdb) start
Temporary breakpoint 7 at 0x5555555551e5: file main.cpp, line 9.
Starting program: /home/hadley/Developments/gdb/main 

Temporary breakpoint 7, main () at main.cpp:9
9	int main(){
1: b = {i = {0, 1068498944}, d = 0.0625}
```

2. continue the program  

`continue` or `c` will make the program run automatically until it reaches breakpoints or end of the program, in the case below, it first reaches the only breakpoint, then it reaches the end of the program.  

``` terminal
(gdb) c
Continuing.

Breakpoint 5, func1 () at main.cpp:4
4	void func1(){
1: b = {i = {0, 1068498944}, d = 0.0625}
```

it reaches the end of the program: 

``` terminal
(gdb) c
Continuing.
10
20
[Inferior 1 (process 62339) exited normally]
```

* check breakpoints

``` terminal
(gdb) i b
Num     Type           Disp Enb Address            What
2       breakpoint     keep y   0x00005555555551a9 in func1() at main.cpp:4
	breakpoint already hit 1 time
```

* disable or delete breakpoint

``` terminal
(gdb) disable 2
(gdb) i b
Num     Type           Disp Enb Address            What
2       breakpoint     keep n   0x00005555555551a9 in func1() at main.cpp:4
	breakpoint already hit 1 time
```

delete breakpoint using `clear + linenumber/func_name` or `delete + number_breakpoints`   

``` terminal
(gdb) i b
Num     Type           Disp Enb Address            What
2       breakpoint     keep y   0x00005555555551a9 in func1() at main.cpp:4
	breakpoint already hit 1 time
6       breakpoint     keep y   0x00005555555551fd in main() at main.cpp:12
(gdb) delete 2
(gdb) i b
Num     Type           Disp Enb Address            What
6       breakpoint     keep y   0x00005555555551fd in main() at main.cpp:12
(gdb) clear 12

(gdb) i b
Deleted breakpoint 6 No breakpoints or watchpoints.
```

delete all breakpoints:

``` terminal
(gdb) delete
Delete all breakpoints? (y or n) y
```

#### variables read/write

* print variable

`print+variable_name`  


``` terminal
(gdb) run
Starting program: /home/hadley/Developments/gdb/main 

Breakpoint 10, func1 () at main.cpp:5
5	    int variable1 = 10;
(gdb) print variable1
$2 = 21845
(gdb) n
6	    cout<<variable1<<endl;
(gdb) print variable1
$3 = 10
```

* set variable value

``` terminal
(gdb) set array[1]=11
(gdb) print array[1]
$13 = 11
(gdb) print array
$14 = std::vector of length 5, capacity 5 = {0, 11, 2, 3, 4}
```

#### check stack info

when program calls a function, function address/function variable will be pushed into stack, use `bt` to check stack info.

``` terminal
(gdb) run
Starting program: /home/hadley/Developments/gdb/main 

Breakpoint 1, func1 () at main.cpp:4
4	void func1(){
(gdb) bt
#0  func1 () at main.cpp:4
#1  0x0000555555555252 in main () at main.cpp:15
```






``` terminal



* Conditional Breakpoints:

```terminal
(gdb) break fun2
Breakpoint 1 at 0x100000cdf: file main.cpp, line 10.
```


#### Reference

1. https://www.cnblogs.com/kingos/p/4514756.html
2. http://witmax.cn/gdb-usage.html
3. https://www.cnblogs.com/chenmingjun/p/8280889.html
4. https://blog.csdn.net/horotororensu/article/details/82256832
5. https://blog.csdn.net/awm_kar98/article/details/82840811



g++ -std=c++17 -O2 -Wall -pedantic -pthread main.cpp -o main && ./main

11 14

<!--more-->

cpp reference


cplusplus.com

sharedptr



    





