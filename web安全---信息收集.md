---
title: web安全---信息收集
---
[toc]
&nbsp;&nbsp;&nbsp;&nbsp;`web安全对于渗透提前的信息收集是很重要的。可以通过各种手段获取网站的各种信息。`
&nbsp;&nbsp;&nbsp;&nbsp;`例如：站长个人信息、域名相关信息（域名注册邮箱、dns信息、子域名）`
## 常见网站架构的类型
- php+mysql+win/linux
  > 1、2003 iis6.0/2008 iis7.0/2012 iis8.0
  > 2、apache
  > 3、nginx

- aspx+access/mssql+win
- jsp+oracle/mysql/+win/linux
  > 1、tomcat

- php+postgresql+linux
## 文件和目录的扫描
- 御剑后台扫描工具
  > 1、打开以后再域名输入框填入要扫描的后台地址
  > 2、在下面可以选择扫描的线程以及扫描的时间，还有文件类型。
  > 3、全部选择好以后就可以扫描了。
  
&nbsp; &nbsp; &nbsp;&nbsp;`使用御剑扫描器主要是网站的敏感目录，包括网站后台等。其原理也就是爆破，就是通过敏感目录的字典去匹配。`
- DirBuster
  > 1、填写目标网站地址
  > 2、自动切换模式
  > 3、设置线程，一般为20
  > 4、选择使用字典方式破解
  > 5、使用自己的字典或者使用默认的字典
  > 6、URL模糊测试
  > 7、设置变量/{dir}，运行时会背字典目录替换。
  > 8、开始
- Pk
## 子域名收集
- Layer子域名挖掘机
  > 1、选择DNS和端口
  > 2、输入扫描的域名
- SubDomainsBrute
  > 1、需要python环境
  > 2、安装库dnspython。pip install dnspython。
  > 3、dict文件里面是软件的字典
  > 4、suDomainBrute.py qq.com
  > 5、suDomainBrute.py qq.com -f subnames_full.txt -o qq.com.txt     -f是指定字典
- chaojiping
  > ping.chinaz.com
  > 可以检测是不是cdn
- wydomain 猪猪侠
  > 1、[下载](https://github.com/ring04h/wydomain)
  > 2、字典是wydomain.csv，安装依赖库，方法同上。
  > 3、dnsburte.py -d aliyun.com -f dnspod.csv -o aliyun.log
- Sublist3r
  > 1、[点击下载](https://github.com/aboul3la/Sublist3r)
  > 2、安装依赖库。pip install -r requirements.txt
  > 3、sublist3r.py -d qq.com -b -o qq.txt
- 浏览器site:qq.com
- Github代码仓库
- 站长帮手links在线查询

## whois信息/ip反查/邮箱反查/资产相关/域名查询ip
`域名查询到注册人和邮箱`
`可以通过注册人或者注册邮箱反查网站和注册人`
- 终端whois直接查
- [站长工具](http://icp.chinaz.com/)
- [爱站](https://www.aizhan.com)
- 超级ping可以检查是否使用了cdn
- C段查询
- 天眼
 ## 端口服务
 ### nmap
`服务器开放的端口，知道端口再查询这个端口由什么服务`
`端口：80http 443https 53dns 25smtp 22ssh 23telnet20、21ftp 110pop3 119nntp 143imap 179bgp 135-139、445RPC 500vpn 5060voip 123ntp)`
- nmap -Pn -sV www.baidu.com
  > -Pn 不ping的情况下给服务器进行扫描
  > -sV 查询详细的服务

- nmap -Pn -sV 103.97.177.22 -oN laowine.txt
  > -oN 保存文件格式

- nmap -Pn -sV 103.97.177.22 -O
  > -O 系统扫描

- nmap -Pn -sV -A 103.97.177.22 
  > -A 综合扫描

- nmap -all 103.97.177.22
  > 所有端口进行扫描

- nmap -p0-65535 192.168.0.107
  > 对0-65535的端口进行扫描

- nmap -Pn -sV 103.97.177.22 --open
  > 只查看打开（open）的端口

- nmap -v -A -F -iL target.com.txt -oX target_f.xml
  > -F 快速扫描
  > -iL 通过文件导入地址
  > oN 将标准输出直接写入指定的文件
  > oG 输出便于通过bash或者perl处理的格式,非xml
  > oX 输出xml文件
  > oS  将所有的输出都改为大写

- nmap -Pn -sV -sU 103.97.177.22
  > UDP扫描

### 御剑端口扫描
- 填入ip地址
- 设置端口范围】
- 在seting.ini文件里面可以设置线程

### python扫描工具
- 可以在网上找，实在找不到也可以私聊老酒并说明来意，网上python脚本还是比较多的。或者大佬自己写一个。

## web信息探测
- 网站类型：判断网站是独立开发还是cms二次修改或者cms套用模板。
- 敏感文件：网站的登录接口、后台、未被保护的页面、备份文件（www.rarwebroot.zip.)
### cms识别
- 云悉WEB指纹CMS识别
- 御剑cms识别工具
- [http://whatweb.bugscaner.com/look/](http://whatweb.bugscaner.com/look/)免费不注册

### 网站和常见端口的信息刺探
- 浏览器头信息
- moon_scanbak
  > 扫描备份文件
  > 创建url.txt，并写入需要扫描的域名
  > 生成bak.txt文件。

- [insightscan/scanner](https://github.com/AnthraX1/InsightScan)
  > 单文件多线程端口扫描器
  > scanner.py 103.97.177.0/24 -p 1 1024 -t 20   扫描1-1024端口
  > scanner.py 103.97.177.0/24 -p 80,8080 -t 20  扫描80，8080
  > scanner.py 103.97.177.0/24 -S -t 20 -d
  > -S服务检测， -d检查的东西保存为html文件

- moon_header
- HBSv1.0.exe 
  > 简单的刺探信息

## 邮箱信息收集
- [theHarvester](https://github.com/laramies/theHarvester）
  > python3 theHarvester.py -d freebuf.com -b baidu
  > 建议在linux下
- 社工库
- qq群
- whois注册邮箱

## CDN寻找真实ip
### 使用超级ping查看是否使用了cdn
- [http://ping.chinaz.com/](http://ping.chinaz.com/)
- [http://ping.aizhan.com/](http://ping.aizhan.com/)
- [https://www.17ce.com/](https://www.17ce.com/)

### 找到真实的IP的方法
`找到真实IP可以继续旁站检测，找其他站进行突破，也可以绕过cdn进行访问，从而绕过waf针对攻击语言的拦截，发现有攻击语句就会对攻击的IP进行封堵。`
- dns历史绑定记录
  > DNS查询[https://dnsdb.io/zh-cn/](https://dnsdb.io/zh-cn/)
  > 微步在线[https://x.threatbook.cn](https://x.threatbook.cn)
  > DNS、IP等查询[http://viewdns.info/](http://viewdns.info/)
  > CDN查询IP[https://tools.ipip.net/cdn.php](https://tools.ipip.net/cdn.php)
  > [https://sitereport.netcraft.com/](https://sitereport.netcraft.com/)

- 子域名解析
> 通过子域名的解析指向，也可能指向目标的同一个IP
> 使用工具对子域名进行穷举
> 在线子域名查询
> >[https://securitytrails.com/list/apex_domain](https://securitytrails.com/list/apex_domain)
> >[http://tool.chinaz.com/subdomain/](http://tool.chinaz.com/subdomain/)
> >[https://phpinfo.me/domain/](https://phpinfo.me/domain/)

- ico图标通过空间搜索找真实ip
  > 找到ico
  > 在钟馗之眼搜索ico
  > [http://quake.360.cn](https://quake.360.cn)
 
 - censys
   > 先在[https://crt.sh](https://crt.sh)查找目标网站ssl的hash
   > 在利用censys查找hash得到真实IP