---
layout: post
title: php中的多进程编程
excerpt: 简单介绍下php中的多进程编程
categories: php
---

先简单介绍一个场景，互联网软件开发中，我们可能需要在搞活动的是好大批量给自己的用户发送营销短信，无疑这种场景用PHP单进程方法循环便利所有用户手机号去做实现压力可能是比较大的，因为我们在调用第三方短信通道接口的时候会遇到网络IO阻塞的问题，会使我们的程序时间都浪费在了这上面，

这时候我们可能想到了常用的多线程或者多进程方式同时发起多个socket链接来缓解网络io阻塞问题

下面简单介绍下Linux环境下php多进程编程的实现

- 重点在 **pcntl_fork** 函数 — 在当前进程当前位置产生分支（子进程）fork创建了一个子进程，父进程和子进程 都从fork的位置开始向下继续执行，不同的是父进程执行过程中，得到的fork返回值为子进程 号，而子进程得到的是0。

下面直接上Example

```
<?php
$pid = pcntl_fork();
//父进程和子进程都会执行下面代码
if ($pid == -1) {
    //错误处理：创建子进程失败时返回-1.
     die('could not fork');
} else if ($pid) {
     //父进程会得到子进程号，所以这里是父进程执行的逻辑
     pcntl_wait($status); //等待子进程中断，防止子进程成为僵尸进程。
} else {
     //子进程得到的$pid为0, 所以这里是子进程执行的逻辑。
}
?>
```
php多进程的常用场景除了解决网络IO阻塞耗时的问题，也可能用在大批数据处理的场景下，这里有个php使用redis作为消息系统实现的异步消息队列框架大家可以参考学习一下[https://github.com/chrisboulton/php-resque](https://github.com/chrisboulton/php-resque)

关于php多进程编程涉及的更多知识请参阅手册[http://php.net/manual/zh/book.pcntl.php](http://php.net/manual/zh/book.pcntl.php)
