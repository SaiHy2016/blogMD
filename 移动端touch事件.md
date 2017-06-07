---
title: 移动端touch事件整理
date: 2017-05-28 14:44:44
tags: 学习
---
移动端触摸事件

* `touchstart事件`：触摸时触发（坐标信息可以从`touches`里获得）
* `touchmove事件`：滑动时触发（同上）
* `touched事件`：手指离开时触发（需要从`changeTouches`中获取离开时坐标）
* `touchcancel事件`：当系统停止跟踪触摸的时候触发

上面的这些事件都会冒泡，也都可以取消。虽然这些触摸事件没有在DOM规范中定义，但是它们却是以兼容DOM的方式实现的。所以，每个触摸事件的event对象都提供了在鼠标实践中常见的属性：bubbles(起泡事件的类型)、cancelable(是否用 preventDefault() 方法可以取消与事件关联的默认动作)、clientX(返回当事件被触发时，鼠标指针的水平坐标)、clientY(返回当事件触发时，鼠标指针的垂直坐标)、screenX(当某个事件被触发时，鼠标指针的水平坐标)和screenY(返回当某个事件被触发时，鼠标指针的垂直坐标)。除了常见的DOM属性，触摸事件还包含下面三个用于跟踪触摸的属性。
* `touches`：表示当前跟踪的触摸操作的touch对象的数组。
* `targetTouches`：特定于事件目标的Touch对象的数组。
* `changeTouches`：表示自上次触摸以来发生了什么改变的Touch对象的数组。

 每个Touch对象包含的属性如下。
 * `clientX`：触摸目标在视口中的x坐标。
 * `clientY`：触摸目标在视口中的y坐标。
 * `identifier`：标识触摸的唯一ID。
 * `pageX`：触摸目标在页面中的x坐标。
 * `pageY`：触摸目标在页面中的y坐标。
 * `screenX`：触摸目标在屏幕中的x坐标。
 * `screenY`：触摸目标在屏幕中的y坐标。
 * `target`：触目的DOM节点目标。