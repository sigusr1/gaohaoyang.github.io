---
layout: post  
title:  "串口通信中ICRNL惹的祸"  
date:   2017-08-19  
categories: 其他  
tags: 串口 转义 termios  
author: coderhuo  
mathjax: true  
---

* content
{:toc}

不怕不知道, 就怕不知道自己不知道。







设备A和设备B通过串口通讯，如下图所示。使用COBS进行编解码主要是为了报文分割（解决粘包半包问题）。  

![通信示意图](http://data.coderhuo.tech/blog/cr_to_lr.jpg)


开发和测试期间，A和B之间通信均正常。等到A设备批量生产的时候，极个别A设备和B无法正常通信。  

第一反应是A和B的COBS编解码库（A和B由不同公司开发）会不会有问题，比如发送方编码错误或者接收方解码错误。于是把A编码后的报文用B的COBS模块解码，结果发现解码出来的原始报文是对的。可以确认不是COBS导致的。  

于是要求驱动组同事在A的驱动层加打印，观察A的驱动层发给串口模块的数据是否正确，发现也是对的。  

事已至此，基本可以排除掉A的问题，于是要求对方在B的驱动层加打印，观察发现，B的驱动层接收到的数据完全正确，但是在传给应用层的时候，总是把0x0D转换成0x0A。

搜索资料发现，如果串口通信中设置了ICRNL选项，则会将回车符(0x0D)转换成换行符（0x0A）。B方排查代码发现，果然设置了该选项。  

顺便说下，如果串口用于数据传输，可以设置成Raw mode，关闭回显、行控制、转义等功能:

```

termios_p->c_iflag &= ~(IGNBRK | BRKINT | PARMRK | ISTRIP | INLCR | IGNCR | ICRNL | IXON);  
termios_p->c_oflag &= ~OPOST;  
termios_p->c_lflag &= ~(ECHO | ECHONL | ICANON | ISIG | IEXTEN);  
termios_p->c_cflag &= ~(CSIZE | PARENB);  
termios_p->c_cflag |= CS8;

```




**参考文档：**  
[https://linux.die.net/man/3/termios](https://linux.die.net/man/3/termios)
