---
layout:     post
title:      "[转载]响应式图片101(三):图片分辨率"
subtitle:   ""
date:       2015-10-27 21:30:00
author:     "Mariano"
header-img: "img/experience.jpg"
tags:  

    - 响应式 
    - 响应式图片
---  
自从苹果发布带retina显示屏的iPhone 4，网页设计人员一直在找一个处理高分屏的方案。于是引入了srcset和它的显示密度。  
## 使用srcset的切换解决方案  
首先提醒大家，显示密度是一种分辨率切换使用情况。当我们解决分辨率切换问题时，我们需要使用srcset。

我们想要使用srcset的原因是它让浏览器可以选择。当使用<picture>元素提供的media属性时，实际上我们在告诉浏览器必须使用哪个图片。这对于艺术切换很有效。

遇到分辨率切换的情况时，浏览器知道哪张图片显示效果最好。它可以根据网络情况或用户行为等因素来做决定。

因此除非是艺术切换的情况，我们应该让浏览器本身来自动选择。   
 
##显示密度描述  
显示密度的语法很直观：  
![]({{site.baseurl}}/img/srcset-display-density2.png)  
  
srcset属性被添加在<img>元素上的。srcset的值是一个用逗号分隔的列表。列表中的每个项包含一张图片的路径并且按倍数（例如,1x,2x,3x...）提供多张分辨率的图片。  
  
```html
<img src="cat.jpg" alt="cat" srcset="cat.jpg, cat-2X.jpg 2x">
```    
##这看起来很简单...  
  
这很简单,试想你需要关心的是显示密度。那么我们会经常碰到吗？

让我们来看一下第1部分中的Apple Watch图片  
  
![]({{site.baseurl}}/img/hero_ygold_edition_800.jpg)  
  
像之前提到的那样，这张图片是5144px × 1698px并且在2倍下大小为398K。还有一张1倍的版本。让我们把它们与Blackberry Curve 9310上单一分辨率的图片尺寸做对比：  
  
|Image          |Width         |Height          |File Size    |  
|:------------: |:------------:|:--------------:|:-----------:|
|2x large       |5144          |1698            |398K         |
|1x large       |2572          |849             |256K         |
|320px, 
 Single Density |320           |106             |8K           |  
   
表格中的最后一行，我把图片大小改变为320px宽另存为JPEG从而看看它会怎样。

显然两个尺寸的图片是不够的。当然，我们可以把320作为1倍图然后重写标记如下：  
  
```html
<img srcset="cat.jpg, cat-2X.jpg 2x, cat-3x.jpg 3x, […], cat-16x.jpg 16x">
```  
这会让我们有从320px到5144px的图片，但我觉得这样很愚蠢。

这就是我认为显示密度描述比其他解决方案不可取的另一个主要原因。我没有任何兴趣来维护一大堆不同显示密度的可用性。

我们难道要提供1x,1.5x,2x,3x更多种情况吗？如果算上其他例如iPhone6 Plus的缩减像素呢？

有一点我在大家开始用响应式图片时没有提到。如果在多个图片断点上有多个图片密度，有时候就需要重复图片源,因为尺寸很小的2倍图可能与1倍在大的图片断点上是一样的。

很快这样就会变得糟糕。  
  
## 显示密度描述符最适合固定宽度图片  
当你在处理固定宽度图片元素的密度可选时，屏幕密度描述显得很不方便而且存在许多不足。

需要什么来代替呢？本系列的第四部分将会介绍：Srcset宽度描述符。


    
> 转载自：[http://www.w3cplus.com/responsive/responsive-images-101-part-3-srcset-display-density.html](http://www.w3cplus.com/responsive/responsive-images-101-part-3-srcset-display-density.html)     
>原文来自：[http://blog.cloudfour.com/responsive-images-101-part-3-srcset-display-density/](http://blog.cloudfour.com/responsive-images-101-part-3-srcset-display-density/)
