---
layout: post
title: 使用Composer来管理你的PHP依赖
excerpt: Composer 是 PHP 的一个依赖管理工具。它允许你申明项目所依赖的代码库，它会在你的项目中为你安装他们。
categories: php
---

“php是世界上最好的语言”，确实php语法的简单、学习成本低、使用宽松、开源组件多等让php得到了最好的语言的称号，但是没有最完美，只有更完美，今天介绍一下php包依赖管理工具

### 为什么要使用Composer

   ruby、Python、nodejs等都有自己的包依赖管理工具，他们使得依赖代码组织的有统一的规范，方便对依赖的引用、升级、管理等，而不是copy源码的方式来引入一个依赖，Composer是一个不错的工具
   
### 如何使用Composer
   
- *NIX下安装
   
    ```
    curl -sS https://getcomposer.org/installer | php
    ```
    
    或
    
    ```
    php -r "readfile('https://getcomposer.org/installer');" | php
    ```
    
    然后
    
    ```
    mv composer.phar /usr/local/bin/composer
    ```

- 使用Composer

请移步[http://docs.phpcomposer.com/00-intro.html#Using-Composer](http://docs.phpcomposer.com/00-intro.html#Using-Composer)

注：国内建议切换一下镜像[http://www.phpcomposer.com/](http://www.phpcomposer.com/)

