---
layout:     post
title:      "[转载]响应式图片101(五):图片尺寸"
subtitle:   ""
date:       2015-12-06 20:30:00
author:     "Mariano"
header-img: "img/experience.jpg"
tags:  

    - 响应式 
    - 响应式图片
---    
  
上一次我们已经发现了srcset宽度描述符的威力，但他们同时也面临着新挑战－当图片开始下载时浏览器知道的只有视窗尺寸。

现在，是时候认识这篇故事里的英雄了：sizes属性。  
  
![]({{site.baseurl}}/img/sizes-hero.jpg)    

# Size属性必不可少！    
  
使用srcset宽度描述符时都需要sizes属性。

事实上，sizes只有在使用宽度描述符时才有意义。如果使用显示密度描述符的话，就不需要sizes属性。因为浏览器会不知道如何处理它。  
  
## size语法  
  
最初，在所有响应式图片的新标准中，sizes是我最难想通的一个属性。  
  
![]({{site.baseurl}}/img/sizes-800.png)  
  
像srcset一样，sizes属性包含一个逗号分隔的列表。这个逗号分隔列表描述了根据视口而变化的图片尺寸。

我要重申这点因为这是理解sizes属性的关键。

我们告诉浏览器多大尺寸的图片与多大尺寸的视窗相关。并且能让浏览器知道根据视口尺寸的变化它们之间的关系如何变化。  
  
```html
<img src="cat.jpg" alt="cat"
  srcset="cat-160.jpg 160w, cat-320.jpg 320w, cat-640.jpg 640w, cat-1280.jpg 1280w"
  sizes="(max-width: 480px) 100vw, (max-width: 900px) 33vw, 254px">
```  
  
像srcset一样，每个由逗号分隔的项目包含两个由空格分隔的值。

## 媒体情况

第一个值是媒体情况。媒体情况类似于媒体查询，但功能不全，必入，你不能写@media screen，但是可以做想要在某个尺寸上做的任何事情。

通常，媒体情况会类似于(max-width:480px)或者也许是(min-width:480px)。

## 长度

每个逗号分隔项的第二个值是长度。长度单位通常是视窗宽度（vw）。

很有可能你之前没见过vw单位。它确实很新，但是在当今浏览器里已经被广泛支持。

每个vw单位代表视窗宽度的1%，那么100vw就是100%视窗宽度而33vw就是33%视窗宽度。

长度不一定要用视窗宽度单位。长度可以是任何长度单位包括绝对和相对长度。你甚至可以用CSS calc()来动态计算margin。

## 浏览器如何选择正确的sizes

浏览器开始读取逗号分隔列表值时，它会获取符合媒体情况的第一个值。

来看一下我们的样例标签和sizes属性的顺序。  

```html
<img src="cat.jpg" alt="cat"
  srcset="cat-160.jpg 160w, cat-320.jpg 320w, cat-640.jpg 640w, cat-1280.jpg 1280w"
  sizes="(max-width: 480px) 100vw, (max-width: 900px) 33vw, 254px">
```  
翻译成的指令的符号列表，结果如下：

* (max-width: 480px) 100vw：视窗等于或小于480px，图片是100%视窗宽度。
* (max-width: 900px) 33vw：视窗等于或小于900px，因为之前的媒体情况这个规则永远不会生效。因此，规则生效意味着视窗宽度为481px到900px。视窗宽度从901px宽到无限大的情况下，图片宽度为254px。
* 254px：当前没有媒体情况列表，在没有其他媒体情况满足的情况下长度为默认值。在这种情况下，媒体情况要包含尺寸为900px的视窗。因此，视窗宽度从901px到无限大，图片宽度为254px。     

 
注意：在本文发布时，Walmart Grocery网站没有使用srcset和sizes。这些都是假设的标记。想要实际观察srcset和sizes，请访问最近才开始使用srcset和sizes的The Guardian。  
## 如果把内容和表现分离呢？

我看到许多关于响应式图片新规范的吐槽。大多数人抱怨其复杂性而忽视事实上网页中的图片本来就很复杂以及[WWIC]((http://www.ftrain.com/wwic.html)的一些变化。

但是有一个吐槽我个人非常赞同，现在我们在标签上添加信息表示——图片尺寸。我好奇是否有任何一个参与响应式图片标准制定的人在某种程度上提出过这种担忧。

不幸的是，这是不可避免的。像在第4部分中谈到的那样，浏览器在不知道页面图片尺寸的情况下就开始下载图片资源了。

唯一支持预加载和确保下载正确资源的方式是在标签中提供图片尺寸信息。

## 预加载究竟值的吗？

如果你像我一样思考，也许会怀疑预加载会带来那么多问题的话那它本身还有价值吗？

有。绝对有。  
![]({{site.baseurl}}/img/pre-loader-faster-web.jpg)  
  
Andy Davies写了一篇文章关于使用预加载后Google和Firefox在平均页面加载速度上分别提升了20%和10%。Steve Souders认为“预加载是浏览器实现的单个最佳的表现改进。”

我们不能简单把网页的优秀表现归功于响应式图片。

因此，我们需要找到一个平衡点。sizes属性就是平衡点。它提供给浏览器完成工作的恰当信息。

## Srcset和sizes ＝ 智能浏览器

srcset和sizes提供了所有在分辨率切换情况下需要的功能。它给浏览器提供恰当的信息来让浏览器做出明智的决定。  
  
 ![]({{site.baseurl}}/img/smart-dog.jpg)   
  
 但是如果你想要更多的控制该怎么办呢？遇到艺术切换该怎么办？我们将在下一节中向大家介绍有关于这方面的知识——`<picture>`元素。


>转自：[http://www.w3cplus.com/responsive/responsive-images-101-part-5-sizes.html](http://www.w3cplus.com/responsive/responsive-images-101-part-5-sizes.html)  
原文来自:[http://blog.cloudfour.com/responsive-images-101-part-5-sizes/](http://blog.cloudfour.com/responsive-images-101-part-5-sizes/)