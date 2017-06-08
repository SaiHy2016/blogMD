---
title: meta一些设置（未完）
date: 2017-06-07 10:26:26
tags: 学习
---
META标签分两大部分：HTTP标题信息(HTTP-EQUIV)和页面描述信息(NAME)。

## name 属性

 ```html
  1、<meta name="Generator" contect="">用以说明生成工具（如Microsoft FrontPage 4.0）等；

  2、<meta name="KEYWords" contect="">向搜索引擎说明你的网页的关键词；

  3、<meta name="DEscription" contect="">告诉搜索引擎你的站点的主要内容；

  4、<meta name="Author" contect="你的姓名">告诉搜索引擎你的站点的制作的作者；

  5、<meta name="Robots" contect= "all|none|index|noindex|follow|nofollow">

  　 其中的属性说明如下：
  　 设定为all：文件将被检索，且页面上的链接可以被查询；
    设定为none：文件将不被检索，且页面上的链接不可以被查询；
    设定为index：文件将被检索；
    设定为follow：页面上的链接可以被查询；
    设定为noindex：文件将不被检索，但页面上的链接可以被查询；
    设定为nofollow：文件将不被检索，页面上的链接可以被查询。
```

## http-equiv属性

```
1、<meta http-equiv="Content-Type" contect="text/html";charset=gb_2312-80">和 <meta http-equiv="Content-Language" contect="zh-CN">用以说明主页制作所使用的文字以及语言；又如英文是ISO-8859-1字符集，还有BIG5、utf-8、shift-Jis、Euc、Koi8-2等字符集；
2、<meta http-equiv="Refresh" contect="n;url=http://yourlink">定时让网页在指定的时间n内，跳转到页面http://yourlink；
3、<meta http-equiv="Expires" contect="Mon,12 May 2001 00:20:00 GMT">可以用于设定网页的到期时间，一旦过期则必须到服务器上重新调用。需要注意的是必须使用GMT时间格式；
4、<meta http-equiv="Pragma" contect="no-cache">是用于设定禁止浏览器从本地机的缓存中调阅页面内容，设定后一旦离开网页就无法从Cache中再调出；
5、<meta http-equiv="set-cookie" contect="Mon,12 May 2001 00:20:00 GMT">cookie设定，如果网页过期，存盘的cookie将被删除。需要注意的也是必须使用GMT时间格式；
6、<meta http-equiv="Pics-label" contect="">网页等级评定，在IE的internet选项中有一项内容设置，可以防止浏览一些受限制的网站，而网站的限制级别就是通过meta属性来设置的；
7、<meta http-equiv="windows-Target" contect="_top">强制页面在当前窗口中以独立页面显示，可以防止自己的网页被别人当作一个frame页调用；
8、<meta http-equiv="Page-Enter" contect="revealTrans(duration=10,transtion= 50)">和<meta http-equiv="Page-Exit" contect="revealTrans(duration=20，transtion=6)">设定进入和离开页面时的特殊效果，这个功能即FrontPage中的“格式/网页过渡”，不过所加的页面不能够是一个frame页面。
Open Graph Protocol
Meta Property=og标签是什么呢?
og是一种新的HTTP头部标记，即Open Graph Protocol：

The Open Graph Protocol enables any web page to become a rich object in a social graph.+ n3 }

即这种协议可以让网页成为一个“富媒体对象”。
用了Meta Property=og标签，就是你同意了网页内容可以被其他社会化网站引用等，目前这种协议被SNS网站如Fackbook、renren采用。
SNS已经成为网络上的一大热门应用，优质的内容通过分享在好友间迅速传播。为了提高站外内容的传播效率，2010年F8会议上Facebook公布 了一套开放内容协议(Open Graph Protocol)，任何网页只要遵守该协议，SNS就能从页面上提取最有效的信息并呈现给用户。

  <meta property=”og:type” content=”video”/>
  <meta property=”og:title” content=”五月天_突然好想你MV现场版”/>
  <meta property=”og:image” content=”http://g1.ykimg.com/0100641F464A ... 9-76EA-E5E20A1887C4″/>
  <meta property=”og:url” content=”http://v.youku.com/v_show/id_XMTIyMTY5NzMy.html”/>
  <meta property=”og:videosrc” content=”http://player.youku.com/player.p ... AutoPlay=true/v.swf”/>
  <meta property=”og:width” content=”500″ />
  <meta property=”og:height” content=”416″ />
  <meta property=”og:type” content=”video”/>
  <meta property=”og:title” content=”五月天_突然好想你MV现场版_AA”/>
  <meta property=”og:image” content=”http://g1.ykimg.com/0100641F464A ... EA-E5E20A1887C44444″/>
  <meta property=”og:url” content=”http://v.youku.com/v_show/id_XMTIyMTY5NzMyyyyyyyyyyyyyyyy.html”/>
  <meta property=”og:videosrc” content=”http://player.youku.com/player.p ... AutoPlay=true/y.swf”/>
  <meta property=”og:width” content=”600″ />
  <meta property=”og:height” content=”716″/>

  <meta http-equiv="Content-Language" content="zh-CN" />    html代码语言采用中文
  <meta property="qc:admins" content="153033120760567656375" />  QQ登陆声明
  <meta property="wb:webmaster" content="e9da5e10879ed7c9" />   微博登陆声明
  <meta name="google-site-verification" content="tPkY-Quj85Ni78uIWOIREPO9k5xczDgjch10qsLfVfs" /> google的网站认证代码，证明该网站的所有者是你
  ```