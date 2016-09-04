---
layout:     post
title:      "[转载]响应式图片101(四):srcset宽度描述符"
subtitle:   ""
date:       2015-11-29 20:30:00
author:     "Mariano"
header-img: "img/experience.jpg"
tags:  

    - 响应式 
    - 响应式图片
---  
    
在响应式图片101系列教程中的第三篇中，我们学习了显示密度描述，并且总结出它们适合用于固定宽度图片，但是对于自适应图片有所不足。    

伸缩使图片就需要用到srcset的宽度描述符。  
  
# 宽度描述符  
宽度描述符的语法与屏幕密度描述符类似。srcset属性值是逗号分隔的图片源和描述列表。  
  
![]({{site.baseurl}}/img/srcset-width-descriptors.png)  
区别在于不是用1x,2x或其他值来表示密度，我们列出了图片源的宽度例如320w，480w等。  
  
```html
<img src="cat.jpg" alt="cat" 
  srcset="cat-160.jpg 160w, cat-320.jpg 320w, cat-640.jpg 640w, cat-1280.jpg 1280w">
```  
  
图片源的宽度会让人很困惑。宽度描述符会根据分辨率来寻找图片源文件。

换句话说如果在一个图片编辑器中打开一张图片，它的分辨率是多少呢？获取图片的宽度放置在srcset属性中。  
    
# 浏览器选择最佳图片资源   
  
当使用宽度描述符，你给浏览器提供了一系列图片以及它们的真实宽度,因此浏览器可以选择最佳图片源。浏览器是怎么做的呢？

你的第一反应一定是浏览器检查页面上元素的尺寸并与图片列表尺寸对比。这有点道理，但实际上并不是这样。

我们来看，当浏览器开始下载图片时，通常它并不知道页面中图片的尺寸。  
  
# 浏览器预加载和合理资源下载  
如果查看浏览器渲染页面的时间线，你会发现一些引人注目的事情。  
![]({{site.baseurl}}/img/aneventapart-timeline-full.jpg)   
就在浏览器下载HTML后不久，它继续请求CSS和JavaScript。但是在CSS和JavaScript完成下载前，浏览器开始下载图片。

因为CSS和JavaScript都没下载完成，浏览器下载图片时并不知道页面布局。由于不知道布局，它就不知道图片元素的尺寸。

顺带一提，预加载行为正是为什么我们不能用CSS或JavaScript解决内联响应式图片的原因。在浏览器开始下载时它们还不可用。

浏览器唯一知道的是视窗尺寸。一旦我们过渡到了显示密度选择符，一切都与视窗尺寸紧紧相关。  
  
# 为什么影响呢？  
视窗是真实图片尺寸的抽象替代品。用Walmart’s Grocery页面上的图片作为例子：  
![]({{site.baseurl}}/img/delivery-walmart-small-800.jpg)  
在小视窗下，图片几乎和视窗宽度尺寸相同。

然而在大屏幕中，情况不同：  
![]({{site.baseurl}}/img/delivery-walmart-widescreen-800.jpg)  
  
在第二个例子里，视窗宽度为1540px，但是图片宽度只有254px。知道视窗尺寸不足以给浏览器提供选择合适图片源的信息。  
  
# 尺寸属性来解决！  
我们如何让浏览器知道页面中的图片尺寸，从而让浏览器可以在srcset列表中下载正确的图片呢？如何使用图片尺寸属性，欢迎阅读本系列教程的第五部分——图片尺寸！  





  
> 转载自：[http://www.w3cplus.com/responsive/responsive-images-101-part-4-srcset-width-descriptors.html](http://www.w3cplus.com/responsive/responsive-images-101-part-4-srcset-width-descriptors.html)     
>原文来自：[http://blog.cloudfour.com/responsive-images-101-part-4-srcset-width-descriptors/](http://blog.cloudfour.com/responsive-images-101-part-4-srcset-width-descriptors/)
