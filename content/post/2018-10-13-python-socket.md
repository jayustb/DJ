---
title: 本博客第一篇文章使用python进行Socket传输
author: DashJay
date: '2018-10-13'
slug: python-socket
categories:
  - Python
  - Socket
  - 网络
tags:
  - Python
  - Socket
  - 网络
lastmod: '2018-10-13T09:52:27+08:00'
keywords: []
description: ''
comment: no
toc: no
autoCollapseToc: no
postMetaInFooter: no
hiddenFromHomePage: no
contentCopyright: no
reward: no
mathjax: no
mathjaxEnableSingleDollar: no
mathjaxEnableAutoNumber: no
hideHeaderAndFooter: no
flowchartDiagrams:
  enable: no
  options: ''
sequenceDiagrams:
  enable: no
  options: ''
---

<!--more-->

> Socket用来进行网络传输的底层包,是对TCP/IP(UDP)的封装,这次我使用Python在一台虚拟机中给另一台虚拟机传输一个内容

首先代码如下

```python
import socket

def main():
    # Create Socket
    udp_socket = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

    # Use socket to send and recieve
    addr = ('10.211.55.14' ,8080)
    s = b'Fuck You'
    udp_socket.sendto(s,addr)

    # Close Socket    
    udp_socket.close()
if __name__ == "__main__":
    main()

```

随着这个程序的运行,我的另一边Windows机器中的的调试助手也收到了消息

<img src="/post/2018-10-13-python-socket_files/屏幕快照 2018-10-13 09.55.58.png" alt="收到了Fuck You字样" width="70%"/>

### 1.在这个过程中我遇到了一些有关虚拟机的问题,打算弄明白一点,下面是一些记录

其实整个电脑虚拟机里有很多虚拟网卡,申请到了很多不同的ip,把网络适配设置好可以让电脑处于同一个局域网下.

### 2.老师教给我我使用了ipython3,交互模式

这种交互类型非常给力,可以使用`ls`等基础命令

### 3.本来只能发送byte-like的字符

`udp_socket.sendto(send_data.encode("utf-8"),addr)`

使用`encode`方法让发送顺利

### 4.怎么接收数据呢???

我们需要监听(绑定)某个端口才能收到别人发送过来的消息

```python
import socket

def main():
    # Create Socket
    udp_socket = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

    # Use socket to send and recieve
    # empty the ip can get one ip of this device
    addr = ("",8080)
    udp_socket.bind(addr)

    # wait for the data from other
    # 1024 shows that the maxsize of data
    recv_data = udp_socket.recvfrom(1024)

    # show what recieve
    print(recv_data[0].decode('utf-8'))

    # Close Socket    
    udp_socket.close()
if __name__ == "__main__":
    main()
    
```
绑定之后等待设置接受最大的内容,然后坐等就行了额最后接收到之后会储存在命名的数组中

随着windows中数据的发送:

<img src="/post/2018-10-13-python-socket_files/屏幕快照 2018-10-13 10.33.23.png" alt="" width="99%"/>

Ubuntu这边也收到了相关的内容

<img src="/post/2018-10-13-python-socket_files/屏幕快照 2018-10-13 10.33.17.png" alt="" width="99%"/>

### 5.有关编码的问题总之比较麻烦

### 6.只能bind自己的信息

### 7.如果想循环接受设置一个While True就好了

```python

import socket

def main():
    # Create Socket
    # 创建套接字
    udp_socket = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

    localaddr = ("",8878)
    udp_socket.bind(localaddr)

    while True:
        recv_data = udp_socket.recvfrom(1024)
        recv_msg = recv_data[0].decode('gbk')
        recv_addr = recv_data[1]
        print("%s : %s"%(str(recv_addr),recv_msg))    

    # Close Socket    
    udp_socket.close()
if __name__ == "__main__":
    main()
    
```

只要一直发送就能接受啦
<img src="/post/2018-10-13-python-socket_files/屏幕快照 2018-10-13 11.18.02.png" alt="" width="99%"/>

Ubuntu这边一直在接受

<img src="/post/2018-10-13-python-socket_files/屏幕快照 2018-10-13 11.18.10.png" alt="" width="99%"/>

### 8.但是有一些端口的问题还要讲一下

操作系统会给要发送数据的软件却没有端口的时候,会给他们随即分配一个随即端口

端口在:`1024-65535`这个范围之内

如果之前绑好了的,发送的时候始终会使用此端口

一个端口只能被一个软件绑定