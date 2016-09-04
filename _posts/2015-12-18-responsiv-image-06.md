---
layout:     post
title:      "[转载]响应式图片101(六):picture元素"
subtitle:   ""
date:       2015-12-18 22:30:00
author:     "Mariano"
header-img: "img/experience.jpg"
tags:  

    - 响应式 
    - 响应式图片
---    
    
在第[3]({{site.baseurl}}/2015/10/22/responsive-image-03/)，[4]({{site.baseurl}}/2015/11/29/responsive-image-04/)，[5]({{site.baseurl}}/2015/12/06/resonsive-images-05/)部分中，我们专注于分辨率切换的解决方案。现在是时候来研究如何解决艺术指导了。

`<picture>`元素——尤其是媒体属性——被设计来简化艺术指导。    
  
![]({{site.baseurl}}/img/picture-syntax.png)   
  
`<picture>`元素包含一系列`<source>`子元素后跟着需要的`<img>`元素。source元素原理和video元素的子源类似。  
  
```html
<picture>
  <source media="(min-width: 900px)" srcset="cat-vertical.jpg">
  <source media="(min-width: 750px)" srcset="cat-horizontal.jpg">
  <img src="cat.jpg" alt="cat">
</picture>
```  
每个源必须有一个srcset属性，可选属性包括media，sizes和type。`<source>`元素上的sizes和srcset的使用和`<img>`上完全一样。

我们现在主要研究media属性。

## media属性

media属性的值是媒体查询。与sizes属性的媒体情况不同，这里的媒体查询是你熟知并喜爱的且功能完整。

当浏览器检查source元素列表时，使用第一个媒体查询匹配的源。如果没有媒体查询匹配，则使用`<img>`元素。

## media属性是指令，而不是建议

不像是srcset和sizes，当使用媒体属性，你在告诉浏览器应该使用哪个源。

浏览器无法自由选择一个不同源。它必须使用第一个媒体属性匹配当前浏览器状况的第一个`<source>`元素。

这就是带有媒体属性的`<picture>`元素非常适合艺术指导的原因。在艺术指导的使用情况中，设计师必须确保在特定视口尺寸下使用的图片与他们预期的一致否则设计可能会被破坏。

让我们来实际看一下。

## 实际情况下的picture元素

Shopify 使用`<picture>`元素来解决艺术指导的问题。Shopify’s在主页上突出了一个顾客，Corrine Anestopoulos，Biko Jewelry的联合创始人。  
  
![]({{site.baseurl}}/img/shopify-picture-example3.gif)    

在狭窄的屏幕上，Anestopoulos小姐的照片被裁减。因为图片不再是被简单缩小，这就是考虑到艺术指导的情况。

Shopify使用的标记将`<picture>`元素和srcset显示密度描述符结合。我为了简化标记而移除了冗长的图片路径并总结如下：  

```html
<picture>
  <source srcset="homepage-person@desktop.png, homepage-person@desktop-2x.png 2x"       
          media="(min-width: 990px)">
  <source srcset="homepage-person@tablet.png, homepage-person@tablet-2x.png 2x" 
          media="(min-width: 750px)">
  <img srcset="homepage-person@mobile.png, homepage-person@mobile-2x.png 2x" 
       alt="Shopify Merchant, Corrine Anestopoulos">
</picture>
```  

注：新改版的页面代码：  

```html
<picture class="">
  <!--[if IE 9]><video style="display: none;"><![endif]-->
  <source srcset="muttonhead-feature@desktop-a97f32476dec8ace5bff5581de852720.png 1x, muttonhead-feature@desktop-2x-9dfadafd12daaa37357521b5cfeb71c9.png 2x" media="(min-width: 990px)">
  <source srcset="muttonhead-feature@tablet-098c9c293a9fc4625c4e3881c293d284.png 1x, muttonhead-feature@tablet-2x-9e850f53007aca09e7c3b58d7b6d2ba1.png 2x" media="(min-width: 750px)">
  <!--[if IE 9]></video><![endif]-->
  <img srcset="muttonhead-feature@mobile-46b2bcd7fba4a422861fece5231085a3.png 1x, muttonhead-feature@mobile-2x-4e12c2522c827b69b53ad706aeaf6ba9.png 2x" alt="Shopify online store" class="">
</picture>
```

缩小你的浏览器窗口大小，你能看到图片的更换过程

仔细观察这些代码，Shopify使用了三个不同的图片断点。每个断点的图片宽度固定－断点间的宽度转变是跳跃的而不是连续的。

因为图片宽度固定，[srcset显示密度描述符]((http://www.w3cplus.com/responsive/responsive-images-101-part-3-srcset-display-density.html)就派上作用。因此对于每个断点来说，Shopify定义了一个1倍和一个2倍源文件。分解开来如下所示：

* `<source … media="(min-width: 990px)">`:最大尺寸的图片，Shopify把它称为桌面，是第一个图片源。媒体属性告诉浏览器这个源只有在视口宽度大于或等于990px才被使用。
* `<source … media="(min-width: 750px)">`:第二个源，“平板”图片，视口宽度大于或等于750px时使用。因为第一个源在990px时起作用并且浏览器选择匹配的第一个源，第二个源的有效视口宽度范围是750px到989px。
* `<img>`:如果前两个源没有匹配，说明视口宽度一定小于750px。这种情况下，会使用`<img>`元素上srcset。小屏幕会使用”移动设备”图片。
如果图片宽度自适应而不固定，Shopify本可以使用带srcset宽度描述符的`<picture>`而不是显示密度描述符。

## 最后一点小技巧

遇到艺术指导的情况，你会需要picture元素。另外picture规范的创造者还给网页开发带来了一份最终的大礼。在下一节中，将会向大家介绍图片的新格式相关知识，将带领大家进入图片格式的新世界之中。
 

>转自：[http://www.w3cplus.com/responsive/responsive-images-101-part-6-picture-element.html](http://www.w3cplus.com/responsive/responsive-images-101-part-6-picture-element.html)  
原文来自:[http://blog.cloudfour.com/responsive-images-101-part-6-picture-element/](http://blog.cloudfour.com/responsive-images-101-part-6-picture-element/)