---
title: Cscope Usage
date: 2017-08-02 19:26:20
tags: cscope
categories: Tools
description: "Cscope Usage"
shadow: true
feature:
toc: true
---

Actually the source insight is the fist choice code viewing tool for me, but it requires license and in Linux the vim is the powerful editor for me. So to better understanding the code, cscope is the best choice for me to read code in vim. Now i used the cscope more and more often.

## Generate the cscope meta data
Enter below commands at the top dir of the project, and then cscope.out will be generated:
> find . -name "\*.h" -o -name "\*.c" -o -name "\*.cc" -o -name "\*.cpp" > cscope.files
> cscope -bqR -i cscope.files

More parameters you can refer to cscope -h.
<!--more-->
## Use cscope to read code
After the cscope utility installed, you can vim a file as normal and input the cscope command, below help will show:
> :cscope
> cscope commands:
>	add : Add a new database	(Usage: add file|dir [pre-path] [flags])
>	find : Query for a pattern	(Usage: find c|d|e|f|g|i|s|t name)
>       c: Find functions calling this function
>       d: Find functions called by this function
>       e: Find this egrep pattern
>       f: Find this file
>       g: Find this definition
>       i: Find files #including this file
>       s: Find this C symbol
>       t: Find assignments to
>    help : Show this message              (Usage: help)
>    kill : Kill a connection              (Usage: kill #)
>    reset: Reinit all connections         (Usage: reset)
>    show : Show connections               (Usage: show)

Chinese reference:
> s: 查找C语言符号，即查找函数名、宏、枚举值等出现的地方
> g: 查找函数、宏、枚举等定义的位置，类似ctags所提供的功能
> d: 查找本函数调用的函数
> c: 查找调用本函数的函数
> t: 查找指定的字符串
> e: 查找egrep模式，相当于egrep功能，但查找速度快多了
> f: 查找并打开文件，类似vim的find功能
> i: 查找包含本文件的文件

## HotKeys defined for quick usage
Download the cscope HotKeys maps [cscope_maps.vim](http://cscope.sourceforge.net/cscope_maps.vim), and puts in dir `~/.vim/plugin/`. More details you can refer to the files, here I introduces the useful commands for me in daily works:
```
nmap <C-\>s :cs find s <C-R>=expand("<cword>")<CR><CR>	
nmap <C-\>g :cs find g <C-R>=expand("<cword>")<CR><CR>	
nmap <C-\>c :cs find c <C-R>=expand("<cword>")<CR><CR>	
nmap <C-\>t :cs find t <C-R>=expand("<cword>")<CR><CR>	
nmap <C-\>e :cs find e <C-R>=expand("<cword>")<CR><CR>	
nmap <C-\>f :cs find f <C-R>=expand("<cfile>")<CR><CR>	
nmap <C-\>i :cs find i ^<C-R>=expand("<cfile>")<CR>$<CR>
nmap <C-\>d :cs find d <C-R>=expand("<cword>")<CR><CR>	
```
Firstly move the cursor to the keyword which want to find, and then press the key `ctrl + '\'`, and then type option character, it will be the quick access to `:cscope find \* some_string`.

Another two useful quick hot key:
`ctrl + ]` - Quickly redirect to the function definition.
`ctrl + t` - Quickly back to the last frame.
