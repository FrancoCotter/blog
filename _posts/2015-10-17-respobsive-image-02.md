---
layout:     post
title:      "[转载]响应式图片101(二):图片加载"
subtitle:   ""
date:       2015-10-17 21:30:00
author:     "Mariano"
header-img: "img/experience.jpg"
tags:  

    - 响应式 
    - 响应式图片
---  
  
我们需要的响应式图片解决方案的主要原因之一是<img>元素功能不足。它只有一个src属性，只能加载一张图片资源，但是我们需要加载多个资源。

既然如此，你可能会很惊讶怎么我们还在讨论<img>元素而不是其他新东西例如<picture>和srcset。

不管采用哪种响应式图片方案，<img>元素必不可少。

<img>元素在所有的内联响应式图片解决方案中都饱受诟病。我喜欢把img当做一个添加和应用所有响应式图片规则的盒子。  
![]({{site.baseurl/img/img-required.png}})  
  
你可以用JavaScript来监控img元素上currentSrc的变化。下面一段简单的脚本用来监控改变并输出到页面上：    
  
```js
(function() {
  var currentSrc, oldSrc, imgEl;
  var showPicSrc = function() {
    oldSrc     = currentSrc;
    imgEl      = document.getElementById('picimg');
    currentSrc = imgEl.currentSrc || imgEl.src;
    if (typeof oldSrc === 'undefined' || oldSrc !== currentSrc) {
      document.getElementById('logger').innerHTML = currentSrc;
    }
  };
  //You may wish to debounce resize if you have performance concerns
  window.addEventListener('resize', showPicSrc);
  window.addEventListener('load', showPicSrc);
})(window); 
```  
将你的浏览器慢慢的缩小，你将看到如下图的一个变化效果：  
  
![]({{site.baseurl}}/img/responsvie-image.gif)    
  
## 为什么会这样  
<img>总是显示当前资源，这意味着任何与<img>元素交互的JavaScript代码都会如期持续工作。

（还没提到几十年来浏览器开发人员写的非常有价值的正确处理图片代码）

正如Eric Portis所说，当我们使用新的响应式图片标准时，“我们正逐渐加强img”的特性。  
  
## 还需要img以外的东西吗？  
在一些场景下单独用img可能就够了：

* 固定宽度，单一分辨率网页:如果你没有用响应式设计并且不用担心"retina"屏幕，img元素就够了。
* 文件尺寸差别很小:对于有些图片，最大版本和最小版本的尺寸没有很大区别。常见的有logo，图标和其他不需要根据视窗变化的小图片。如果文件尺寸没什么区别，一张图片可能就够了。
* 使用基于矢量的图片例如SVG:如果使用基于矢量的图片格式例如SVG，图片可以自由缩放并不需要多张图片。在这种情况下，可以直接用SVG做为img的图片源。  


当然，这取决于需要适配的浏览器是否支持SVG。最好使用picture元素来提供可选的图片格式作为备用方案。会在这个系列里将会介绍这个元素的使用。    

## 想要支持高分辨屏幕怎么办？  
如果想要支持高分屏，我们需要扩展<img>元素。请看这个系列的第3部分:Srcset显示分辨率。  



  
> 转载自：[http://www.w3cplus.com/responsive/responsive-images-101-definitions.html](http://www.w3cplus.com/responsive/responsive-images-101-definitions.html)     
>原文来自：[http://blog.cloudfour.com/responsive-images-101-definitions/](http://blog.cloudfour.com/responsive-images-101-definitions/)
