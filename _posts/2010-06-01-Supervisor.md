---
layout: post
title: Supervisor Linux下进程管理利器
excerpt: Supervisor is a client/server system that allows its users to monitor and control a number of processes on UNIX-like operating systems
categories: Linux
---

Linux下有时候要以daemon的方式运行进程，nohup是一个非常方便的命令，但是假如我们运行的是一个后台服务，nohup则不能很方便或者不能帮助我们监控、管理、启动多个进程，这时候我们可以借助Supervisor来满足我们的需求

supervisor是用Python开发的一套通用的进程管理程序，能将一个普通的命令行进程变为后台daemon，并监控进程状态，异常退出时能自动重启。除此之外有比较规范的日志机制，并提供基于XML-RPC的通用API，可以实现类似web远程进程管理监控工具

以ubuntu为例

- 安装Supervisor只需要一行命令

```shell
apt-get install supervisor
```

- 默认可以在/etc/supervisor/conf.d/下编写supervisor的配置文件，以<font color="red">**conf**</font>作为文件扩展名

来个例子：

```shell
[program:php-server]
command = /usr/local/bin/php -S 0.0.0.0:8888
``` 
把上述文件命名为xxx.conf保存在/etc/supervisor/conf.d/下

```shell
#执行命令
supervisorctl reload

#如果没有启动过supervisord则执行
supervisord -c /etc/supervisor/supervisord.conf

#然后启动刚刚编辑的配置文件
supervisorctl start php-server
```
OK，至此我们已经用supervisor启动了我们的进程，关于supervisor的更多配置项和命令参数大家可以参考官方文档
[http://www.supervisord.org/](http://www.supervisord.org/)

