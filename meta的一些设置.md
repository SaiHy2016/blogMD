---
title: meta一些设置
date: 2017-06-07 10:26:26
tags: 学习
---
META标签分两大部分：HTTP标题信息(HTTP-EQUIV)和页面描述信息(NAME)。
1. HTTP-EQUIV 

  HTTP-EQUIV类似于HTTP的头部协议，它回应给浏览器一些有用的信息，以帮助正确和精确地显示网页内容。常用的HTTP-EQUIV类型有：

  1.1 Content-Type和Content-Language (显示字符集的设定) 
    设定页面使用的字符集，用以说明主页制作所使用的文字已经语言，浏览器会根据此来调用相应的字符集显示page内容。 
    用法:
    	<meta http-equiv="Content-Type" Content="text/html; Charset=gb2312">
    	<meta http-equiv="Content-Language" Content="zh-CN" >
  1.2 Refresh (刷新) 