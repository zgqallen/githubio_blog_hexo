---
title: Overview of Virtual Memory in Linux Kernel and memory allocation in glibc
date: 2017-08-03 19 20:26:20
tags: Virtual_Memory
categories: Knowledge
description: "Overview of Virtual Memory in Linux Kernel and memory allocation in glibc"
shadow: true
feature:
toc: true
---

Long ago, I have presentd an overview of virtual memory in Linux kernel and memory memory in glibc. Now i am lazy to write these again, so I try to upload the PPT in images. As you know, each pages has details knowledge could be digged into, so you have further view, please google the keywords.
## Overview of VM system in Linux ##
![VM](/images/memory/Slide3.PNG)
<!--more-->
## Overview of MMU and Buddy & Slab allocator ##
![VM](/images/memory/Slide4.PNG)
## LifeCycle of Page frames ##
![VM](/images/memory/Slide5.PNG)
## Address Space and VMA mapping in Kernel ##
![VM](/images/memory/Slide6.PNG)
## Pic for summary memory in Kernel ##
![VM](/images/memory/Slide7.PNG)
## Glibc memory allocation concepts ##
![VM](/images/memory/Slide8.PNG)
## Brk and mmap ##
![VM](/images/memory/Slide9.PNG)
## Internal structure of glibc ##
![VM](/images/memory/Slide10.PNG)
## malloc and free process in glibc ##
![VM](/images/memory/Slide11.PNG)
## Some keypoints for glibc ##
![VM](/images/memory/Slide12.PNG)
## Tips for heap profile ##
![VM](/images/memory/Slide13.PNG)
