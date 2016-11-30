---
layout: post
title: Bootstrap modal不支持多层弹窗问题解决
excerpt: Bootstrap 多层modal 造成"Maximum call stack size exceeded"问题解决
categories: 前端
---

产品需求，临时做了一次前端，使用到了bootstrap modal插件弹窗两次，查看chrome console 报错

先上代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link href="http://cdn.bootcss.com/bootstrap/2.3.2/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
<a href="#myModal1" role="button" class="btn" data-toggle="modal">modal1</a>
<!-- Modal1 -->
<div id="myModal1" class="modal hide fade" tabindex="-1" role="dialog"  aria-hidden="true">
    <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-hidden="true">×</button>
        <h3>Modal1 header</h3>
    </div>
    <div class="modal-body">
        <button id="modal2_open" class="btn" type="button" data-toggle="modal" data-target="#myModal2">Launch modal2</button>
    </div>
    <div class="modal-footer">
        <button id="modal2_close" class="btn" data-dismiss="modal" aria-hidden="true">关闭</button>
    </div>
</div>
<!-- Modal2 -->
<div id="myModal2" class="modal hide fade" tabindex="-5" role="dialog" aria-hidden="true">
    <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-hidden="true">×</button>
        <h3>Modal2 header</h3>
    </div>
    <div class="modal-body">
        <p>Modal2 body</p>
    </div>
    <div class="modal-footer">
        <button class="btn" data-dismiss="modal" aria-hidden="true">关闭</button>
    </div>
</div>
<script src="http://cdn.bootcss.com/jquery/1.11.1/jquery.min.js"></script>
<script src="http://cdn.bootcss.com/bootstrap/2.3.2/js/bootstrap.min.js"></script>
</body>
</html> 
```
上述代码在弹窗1里面加了一个按钮触发弹窗2，结果chrome console显示
<font color="red">Uncaught RangeError: Maximum call stack size exceeded</font>
解决方案，在弹窗2开启前先把弹窗1关掉，当弹窗2关闭时，启用弹窗1
主要代码

在启动和关闭弹窗2的按钮上分别加上onclick事件处理

```javascript
$('#modal2_open').modal('hide');
//and
$('#modal2_close').modal('show');
```

