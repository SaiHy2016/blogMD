---
title: 防止页面被iframe嵌套
date: 2017-06-6 10:40:42
tags: 学习
---
1. 方案一
        if (top != self) {
          top.location = self.location;
        }
2. 方案二
         if (self == top) {
           var theBody = document.getElementsByTagName('body')[0];
           theBody.style.display = "block";
         } else {
           top.location = self.location;
         }
3. 方案三
        在响应头里加一个X-Frame-Options
           取值有三种，大部分浏览器都支持：
          1. DENY：浏览器拒绝当前页面加载任何Frame页面
          2. SAMEORIGIN：frame页面的地址只能为同源域名下的页面
          3. ALLOW-FROM origin：origin为允许frame加载的页面地址