---
title: mac上github的clone项目提速
date: 2018-10-04 16:41:02
tags: [Mac, github]
categories: Front-End
---

## 前言

平时自己上github，clone小点的项目速度的快慢对我来说影响不大（其实是之前没有国外的服务器，没试过命令行FQ），但是遇到大的项目需要等待很久，前些时买了服务器，也闲来无事折腾试试。 进入正题：

## 方案一

通过修改hosts文件（亲测有效）

在[IP Lookup]( https://www.ipaddress.com)工具中分别查询github的`github.com`和`github.global.ssl.fastly.net`域名的IP地址，

 打开的hosts（hosts文件位置：【Windows】`C:\Windows\System32\drivers\etc\host【`Mac】执行 `sudo vi /etc/hosts` ）文件中添加如下格式：

```
192.30.253.112 github.com
151.101.13.194 github.global.ssl.fastly.net
```

最后执行`ipconfig /flushdns`命令，刷新 DNS 缓存。

**对比图**

修改前：

![](/images/github提速-配置前.jpg)

修改后：

![](/images/github提速-配置后.jpg)

## 方案二

用`proxychains-ng`这个命令行FQ软件。(方法来自方应杭)

**安装**

```
 # 自己从github下载并编译
 git clone https://github.com/rofl0r/proxychains-ng.git  
 cd proxychains-ng   //进入proxychains-ng目录
 sudo ./configure               //使用root身份运行 
 sudo make 
 sudo make install
 sudo cp ./src/proxychains.conf /etc/proxychians.conf //配置文件复制到/etc目录下
 # brew安装
 brew install proxychains-ng
```

安装完后有一个`proxychains4`的命令，配置`/etc/proxychians.conf`文件，找到`[ProxyList]`，然后加上`socks5     127.0.0.1 1080` 其中1080端口对应本地的端口号。

**使用**

默认方法： `proxychain4 curl -L google.com ` ,即在命令前加上proxychains4

我的方法： 

新建一个配置文件 

```bash
 # 文件~/proxychains.conf
 strict_chain
 quiet_mode
 proxy_dns 

 remote_dns_subnet 224
 tcp_read_time_out 15000
 tcp_connect_time_out 8000
 [ProxyList]
 socks5     127.0.0.1 1080
```

配置~/.zshrc（或~/.bashrc）用`alias`

```
alias pc='proxychains4 -f ~/proxychains.conf'
```

之后在使用就可以只用`pc`命令后面跟上你要FQ的命令即可。


**如果你是mac系统 那么需要关闭SIP（System Integrity Protection）**

macOS 10.11后，苹果加入SIP设置就会导致部分命令是执行不成功的，就包括使用socks的proxychains4。如果我们要解决这个问题，我们就要关掉SIP。

- 重启Mac，按下Command+R直到出现Apple Logo。
- 选择实用工具->终端。
- 输入命令csrutil disable。出现类似于“成功禁用SIP”的意思就表示成功了。

如果还要打开SIP，最后的步骤csrutil enable即可
