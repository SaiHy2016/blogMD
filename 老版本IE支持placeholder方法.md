---
title: placeholder支持
date: 2017-06-01 08:16:16
tags: 学习
---
IE9及以上不支持placeholder属性，可以通过一下方法模拟：
	if('placeholder' in document.createElement('input')){
	        }else{
	            $('[placeholder]').focus(function() {
	                var input = $(this);
	                if (input.val() == input.attr('placeholder')) {
	                    input.val('');
	                    input.removeClass('placeholder');
	                }
	            }).blur(function() {
	                var input = $(this);
	                if (input.val() == '' || input.val() == input.attr('placeholder')) {
	                    input.addClass('placeholder');
	                    input.val(input.attr('placeholder'));
	                }
	            }).blur();
	        }