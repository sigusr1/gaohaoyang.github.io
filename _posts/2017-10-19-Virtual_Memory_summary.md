---
layout: post  
title:  "虚拟内存探究，深入理解进程地址空间"  
date:   2017-10-19
categories: 翻译  
tags: 虚拟内存 翻译 
author: sigusr1  
mathjax: true  
---

* content
{:toc}

想了解堆栈等虚拟内存相关知识吗？  
想知道下面这张进程地址空间示意图是如何一步一步画出来的吗？  
《虚拟内存探究》系列文章将通过实验的方式带你学习相关知识。  

![](http://34.210.34.184:8888/blog/virtual_memory/virtual_memory_diagram_v2.png)








## 中文版 ###

- 第一篇:[虚拟内存探究 -- 第一篇:C strings & /proc](https://sigusr1.github.io/2017/10/12/Virtual_Memory_C_strings_proc/)
- 第二篇:[虚拟内存探究 -- 第二篇:Python 字节](https://sigusr1.github.io/2017/10/15/Virtual_Memory_python_bytes/)
- 第三篇:[虚拟内存探究 -- 第三篇:一步一步画虚拟内存图](https://sigusr1.github.io/2017/10/16/Virtual_Memory_drawing_VM_diagram/)
- 第四篇:[虚拟内存探究 -- 第四篇:malloc, heap & the program break](https://sigusr1.github.io/2017/10/18/Virtual_Memory_malloc_and_heap/)


## 英文版 ###

- Chapter 0:[Hack The Virtual Memory: C strings & /proc](https://blog.holbertonschool.com/hack-the-virtual-memory-c-strings-proc/)
- Chapter 1:[Hack The Virtual Memory: Python bytes](https://blog.holbertonschool.com/hack-the-virtual-memory-python-bytes/)
- Chapter 2:[Hack The Virtual Memory: Drawing the VM diagram](https://blog.holbertonschool.com/hack-the-virtual-memory-drawing-the-vm-diagram/)
- Chapter 3:[Hack the Virtual Memory: malloc, the heap & the program break](https://blog.holbertonschool.com/hack-the-virtual-memory-malloc-the-heap-the-program-break/)
