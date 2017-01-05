---
layout: post
title:  "配置Shadowsocks时无法运行sudo ssserve的解决办法"
date:   2017-01-04 20:09:28 -0600
categories: 编程麻瓜
---
#### 前提
这是写给和我一样的编程麻瓜看的。

#### 正文
刚放假的那几天，虽然没有回国。但我不禁想到，回到『墙』后面，上网体验会大打折扣，于是研究了一下如何在[AWS](https://aws.amazon.com/)上配置最基础的[Shadowsocks](https://shadowsocks.org/en/index.html)服务。在这直白地解释一下，每一个AWS的新用户都有一年的免费服务，在此期间运行在上面的云服务大都不用花什么钱，魔法上网这种吃流量的事情，挂在上面最好不过了。想动手操作一下的小能手们可以参照这篇[教程](http://celerysoft.github.io/2016-01-15.html)，30分钟包教包会。

启动Shadowsocks运行：

> $ ssserver -c /etc/shadowsocks/config.json -d start
permission denied

一般来说我们不是root账户安装Shadosocks(此处若有误，请大神们斧正。)，因此下意识的会运行sudo命令：
>$ sudo ssserver -c /etc/shadowsocks/config.json -d start
sudo: ssserver: command not found

这是因为`ssserver`不在`~/.profile`里的缘故。

但一般不推荐直接把命令直接添加进`~/.profile`，具体讨论见此[How to correctly add a path to PATH?](http://unix.stackexchange.com/questions/26047/how-to-correctly-add-a-path-to-path?answertab=active#tab-top)

不过有一个偷懒的方法，运行:
>$ which ssserver
/usr/local/bin

因此`ssserver`在`~/usr/local/bin`目录下，所以运行：
>$ sudo /usr/local/bin/ssserver -c /etc/shadowsocks/config.json -d start

这样就可以了。

如果你的命令很少用到，或者不知道怎么把命令添加到全局环境里。这是个凑合的方法。

Done！
