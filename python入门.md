---
title: python入门
---
[toc]
## 一、变量
- Python中的变量不需要声明，可以直接通过赋值来创建变量，变量赋值通过“=”实现
- 变量赋值时应该注意数据类型。
- 可以同时为多个变量赋值，但变量与数值的个数必须相等们之间用逗号隔开。
- 变量名尽量具有现实意义，不能使用系统保留的关键字作为变量变量名。

## 二、输出
- print语句可以同时输出多个元素，元素之间用逗号","隔开。print遇到逗号会输出一个空格。
- 如果希望输出的内容之间没有空格，可以把他作为字符串连接在一起，此时数据类型必须保持一致。
  > 1、str(prots)强制转为为字符型。
  > 2、+：必须是相同的类型。

- print语句在输出的内容后面会自动加上一个换行符号\n，如果在输出的内容后面跟上逗号，换行就取消了。

## 三、字符串处理的常用方法
`在Python中一切皆对象，每个字符串都是一个对象。`
- 使用dir可以查看对象的使用方法。
- 使用help命令可以查看某个方法的帮助信息。
- split方法
  > 将字符串根据某个分隔符今次那个分割，分割之后得到一个列表。
  > c.split(".")

- in
  > in不是一个方法，是一个语句
  > true  or  false
```
site="www.baidu.com"
web="baidu"
web in site        //看看web字符串在不在site字符串里面。

"baidu" in "www.baidu.com"
```

- strip()方法
  > 去除字符串头尾指定的字符，如果不指定，默认去除空格以及回车、换行等空白字符。
```
>>> web="www.baidu.com"
>>> web.strip(".com")
'www.baidu'
>>> web.strip("www.")
'baidu.com'

```

- upper()、lower()方法
  > upper()方法可以将字符串转换成大写形成。
  > lower()方法可以将字符串转换成小写形成。
 ```
  >>> web="wWW.BaiDU.Com"
  >>> web.upper()

`WWW.BAIDU.COM'
  >>> web.lower()
'www.baidu.com'

 ```
  
- center方法
  > 使指定的字符串居中显示，两侧再加上指定数量的字符。
```
>>> print "welcome".center(30,'*')
***********welcome************

```
 
 ## 四、列表
 - 在列表中可以集中存放多个数据，并且数据类型不必统一，列表用[]表示。
 - 可以通过索引来获取列表的指定数据，索引从0开始。
   > 可以使用一段连续的索引，比如[0:2]，这是一个左闭右开区间，他的作用就是获取索引号是0和1的量数据。
 - 在列表中可以根据元素查出其对应的索引，这成为切体。
```
>>> port=[21,22,80]
>>> dir(port)
>>> port.append("ssh")  //在列表末尾追加ssh
>>> port.pop(3)   //去除标号为3的数值
>>> port.insert(3,40)  //在标号为3的位置上插入数值为40
>>> port.index(22)   //查找数值为22的标号是多少
```
 - 使用list()函数可以将一个字符串转为列表。
 - 通过len()函数可以统计列表中元素的个数。
  
```
>>> ip="192.168.1.1"
>>> ip.split(".")       //split以"."为分隔符分割形成一个列表
['192', '168', '1', '1']
>>> print ip.split(".")[0]+"."+ip.split(".")[1]+"."+ip.split(".")[2]+"."
192.168.1.

```

## 五、元组、字典和迭代
`元组与列表相似，不同之处在于元组中的数据只能被调用，而不能被修改，元组用()表示。`
- 如果元组中只有一个元素，那么在元素的后面必须加上逗号。
 
`字典的优点是具有极快的查找速度,字典使用｛｝定义。`
- 字典使用键-值（key-value）的形式存储，每一对键值成为一个项。
- 字典中的每一个键和它的值都是以冒号分割，同时用逗号分割两个项。
- 字典使用key来引用字典中某个键所对应的值。
```
>>> services={"ftp":21,"ssh":22}
>>> services
{'ftp': 21, 'ssh': 22}
>>> services["ssh"]
22
>>> services.keys()
['ftp', 'ssh']
>>> services.has_key("ssh")
True
>>> services["smtp"]=25  //修改或者添加
>>> services
{'ftp': 21, 'smtp': 25, 'ssh': 22}

```

`通过for循环可以遍历列表、元组或是字典中的值，这种遍历就成为迭代。`
```
遍历列表
>>> port=[21,11,80]
>>> for i in port:
...     print i,
... 
21 11 80
遍历元组同列表。
遍历字典
>>> services
{'ftp': 21, 'smtp': 25, 'ssh': 22}
>>> for key in services:
...     print key
... 
ftp
smtp
ssh
在遍历字典的时候默认只能显示字典中的键，要想遍历键和值需要下面的。
>>> for key in services:
...     print key+":"+str(services[key])
... 
ftp:21
smtp:25
ssh:22

```

## 六、if选择
- if语句的语法格式
```
if True:         //python区分大小写
	print "OK"
else:
	print "NO"
```
- 冒号不能漏掉，缩进必须统一
- 所有的python合法的表达式都可以作为条件表达式，只要表达式的值不是False、0、空值，python的解释器都可以认为与True等价。
```
#!/usr/bin/env python
#coding:utf-8

if True:
    print "ok"
else:
    print "no"

print "hello!

```

## 七、异常
- 程序运行过程中难免会出现错误，当python检测到错误时，解释器就无法继续执行下去，于是抛出相应的信息，这些统称为异常信息。
 > syntaxError:invalidn syntax  //语法错误
 
 - 合理的使用异常处理可以使得程序更加健壮，具有很强的容错性，不会因为用户的不小心的错误输入或其他运行时原因而总成程序终止，也可以使用异常处理结构为用户提供更加友好的提示。

### try/except语句
- try子句中的代码块包含可能会引发异常的语句，而except子句用来捕捉相应的异常。
- 程序执行时，如果try子句中没有异常发生,那么except子句在try语句执行之后被忽略；如果try子句中有异常发生，那么该部分的其他语句将被忽略，直接跳到except部分，执行其后面的子句。
```
 精确显示错误
except Exception,e:
	print e
出错就pass掉，不显示。
except:
	pass
```

## 八、函数 
- 函数提供了高效的可重用代码块
- 根据各自特定的作用，将程序分割成互相独立的函数是一个良好的编程序习惯，这样便于代码重用，并使程序更易于阅读。
- 通过def语句定义函数，函数中的内容必须缩进。return用于把函数的结果返回。如果没有return语句，函数执行后也会返回结果，指示结果为None。return None可以简写为return。
- 每一个后缀为.py文件都会被视作一个python模块，可以被其他的python程序调用。
  
```python
		每个python脚本在运行的时候都有一个—__name__属性，通过它可以识别程序的使用方式，即程序在作为模块导入还是独立运行，如果程序是作为模块被导入，那么__name__属性的值就被自动设置为模块名；如果是作为脚本独立使用，那么_name_属性的值会被自动设置为字符串"__main__"。
第一种方式：
if __name_=="__main__" 
当前程序是不是独立运行的。

第二种方式：
def main():
	程序
if __name_=="__main_"
	main()
```

## 九、For循环
 ```
 1、列表
>>> for i in [1,2,3]:
...     print i
...
1
2
3

2、通过range()函数生成连续数列
>>> for i in range(1,5):
...     print i,
...
1 2 3 4
>>>
range(初始值，终止值，步长)，range得到的是一个左闭右开区间。
>>> range(1,10)   //默认步长为1
[1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> range(1,9,2)
[1, 3, 5, 7]
>>>

 ```
 
 ## 十、文件
 - 1、文件操作的基本流程
   > 1、调用open()函数打开文件，并创建一个File对象。
   > 2、调用File对象的read()或write()等方法，对文件内容进行读写等操作。
   > 3、调用File对象的close()方法，关闭并保存文件内容。

- open()函数
```
1、通过open()函数以指定模式打开文件并创建文件对象：
				文件对象=open('文件路径','模式')
2、文件打开模式主要包括：
		r只只读模式
		w只写模式
		a追加模式
3 如果传递给open()的文件名不存在，写模式和追加模式都会创建一个新的空文件。
```
- 读取文件
```
1、read()可以一次性的读取文件所有内容，也可以读取指定的前几个字节的数据。
			f.raed()
			f.read(12)
2、readline()方法可以从文件中读取一行并作为结果返回
			f.readline()
3、readlines()方法读取文件，返回一个列表，文件的每一行作为列表的一个元素：
```
- 通过字符串的strip()方法将文件中每行末尾的\n去除。

##  十一、导入模块
- 模块也叫库，每个模块中都内置了大量的功能，函数、类和变量。它就像积木，可以根据需要进行调用组合。
- 模块就是程序，每个模块就是一个后缀为.py的Python的程序。
- Python的模块分布为标准模块和第三方模块，标准模块是Python内置的，第三方模块需要安装之后才能使用。
- 可以通过help命令了解每个模块的基本帮助信息，如：help（‘sys’）
```
1、模块导入方法：
		a、直接调用模块:import 模块名
		b、从模块中调用某个函数：from 模块名 import 函数名
		
2、eg：
			import os
			form os import *      //os里面的所有函数
			form os import system   //直接调用system()方法。
			
```

## 十二、sys模块
- sys是一个标准模块，与python解释器密切相关
- sys.argv
```
1、sys.argv是一个变量，专门用来向python解释器传递参数，类似于shell脚本编程中的位置变量。
#!/usr/bin/env python
#coding:utf-8

import sys
print "脚本文件你是：",sys.argv[0]
print "用户输入的参数数量：",len(sys.argv)-1
print "所有的参数：",sys.argv
print "用户输入的第一个参数：",sys.argv[1]
print "用户输入的第二个参数：",sys.argv[2]
print "用户输入的第三个参数：",sys.argv[3]
运行结果： 
脚本文件你是： ./sys.py
用户输入的参数数量： 3
所有的参数： ['./sys.py', 'me', 'you', 'he']
用户输入的第一个参数： me
用户输入的第二个参数： you
用户输入的第三个参数： he
                                    
```
- sys.exit()
```
1、sys.exit()是一个方法，作用是退出当前程序
	sys.exit()，退出当前程序，并返回systemExit异常
	sys.exit(0)，正常退出
	sys.exit("退出程序")，显示一段提示信息。
	
if len(sys.argv) != 2:
    print "正确使用方法："+sys.argv[0] + "IP列表文件"
    print "例如：./sys.py /root/ip.txt"
    sys.exit()

```

## 十三、os模块
- os模块提供了访问操作系统服务的功能。
- 它最常用的是os.system()方法，可以在Python中使用操作系统命令。
```
1、os.system("ls /root")

2、os.path.isfile()方法，判断指定的对象是否为文件，返回True或False。
		os.path.isfile("/root/pass.txt")
		
3、os.path.isdir()方法，判断指定的对象是否为目录

4、os.path.exists()方法，判断指定的对象是否存在
```
## 十四、多线程
- 进程是线程的容器，线程是操作系统调度和分配处理器时间的基本单位，负责执行包括在进程地址空间中的代码。
- 当进程被创建时，操作系统会自动为之创建一个线程，称为主线程，主线程会更具需要动态创建其他子线程。
- 通过threading模块中的Thread()类可以创建和管理线程对象
```
t=threading.Thread(target=需要执行的函数,args=(向函数传递的参数))
t.start()     执行
```

## 十六、Optparse模块
- 利用该模块可以设置选项，通过选项向脚本传递所需要的参数
- %prog表示当前脚本的文件名
- 每个程序都是自带有-h选项
```
#!/usr/bin/env python
#coding:utf-8

from optparse import OptionParser
usage="Usage:%prog -f <filename> -i <ip address>"
parser=OptionParser(usage=usage )
parser.add_option("-f","--file",type="string",dest="filename", help="IP file")     //选项
parser.add_option("-i","--ip",type="string",dest="address",help="IP address")
(options,args)=parser.parse_args()        //固定格式，parse_args()方法获取定义的选项和参数

print options.filename
print options.address

```