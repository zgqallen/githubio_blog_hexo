---
title: Advanced GDB Usage
date: 2017-07-31 15:48:35
tags: gdb;
categories: Tools
description: "Advanced GDB Usage"
shadow: true
feature:
toc: true
---

This Page was a summary of the advanced gdb usge in daily work, for the basic usage of gdb will not being described here.

## 1. Advanced commands in using
> gdb> info share - show the shared libraries load by process.
> gdb> until (line number) - run until to the line number in case you want to break out the while&for loop.
> gdb> finish - run out of the this function call.
> gdb> call (function name) - call a function in current context.
> gdb> disas (function name) - check the assembly code for a function.
> gdb> run (arguments) - run the program with arguments. 
> gdb> bt - get the call stack for current thread.
> gdb> frame (stack number) - change stack frame to specfic function call.
> gdb> info regs - show the values of current registers.
> gdb> list filename:line - list the code of filename:line
> gdb> info - list all info sub commands and which are helpful.

<!-- more -->
## 2. Set condition break point and watch
we can set the normal break point as below:
> gdb> break (function name)
> gdb> break filename:line
> gdb> break address

In case you want to stop a break point in condition you can do as below:
> gdb> break if val==(some value)

But sometimes, the critical case was string comparasion, you can't compare 2 strings with == directly. In some case, the strcmp may help you, but some are not. In these cases, below gdb native function will help:
```c
_memeq(buf1, buf2, length) - Returns one if the length bytes at the addresses given by buf1 and buf2 are equal. Otherwise it returns zero.
_streq(str1, str2) - Returns one if the string str matches the regular expression regex. Otherwise it returns zero. The syntax of the regular expression is that specified by Python’s regular expression support. 
_strlen(str) - Returns one if the strings str1 and str2 are equal. Otherwise it returns zero. 
_regex(str, regex) - Returns the length of string str. 
```
Sometimes, you want to watch a variable but it was thread level's variable, you can watch the address change directly as below:
> gdb> p &variable - get the address of the variable. 
> gdb> watch \*(int\*)address 

## 3. Multiple threads debugging using gdb
You need get some information of all  threads:
> gdb> info threads -- show all threads
> gdb> thread apply all bt -- show call stack for all threads
> gdb> thread (thread num) -- change the current thread to specfic thread.

Sometimes you need continuing debug the current thread, but other thread schedule may break up. You can lock the thread scheduler as below:
> gdb> set scheduler-locking on

## 4. Show the content of memory
A generic way to show the value in gdb as below:
> gdb> p values|pointer

But most cases, we may need check the values of the address directly, do as below:
> gdb> x /nfu (address)
n - indicates the number of block want to show
f - indicates the format to show the address(x for hex;d for 10-ary; u for unsigned 10-ary;o for 8-ary; t for bin; i for instructions show; c for char)
u - the length of a address unit (b for 1 byte; h for double byte: w for 4 bytes; g for 8 bytes)

## 5. Define a function to call later
you may want to show some information without specific function, then you can define function as below call:
> gdb> define function
> gdb> content
> gdb> end

For example:
> gdb> define mallocinfox
> gdb> set \$\_\_f = fopen("arena.txt", "w+")
> gdb> call malloc\_info(0, \$\_\_f)
> gdb> call fclose(\$\_\_f)
> gdb> end

## 6. Gdb in batch mode
Sometimes, you just want to attach a process and get some information, but you don't want to hold the process with gdb, you can do in batch mode as below:
> gdb -ex "set pagination 0" -ex "Command" -ex "detch" -batch -p $pid
For example:
> gdb -ex "set pagination 0" -ex "thread apply all bt" -ex "detch" -batch -p 12456

