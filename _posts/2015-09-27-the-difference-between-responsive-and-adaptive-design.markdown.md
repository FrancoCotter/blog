---
layout:     post
title:      "浅谈响应式设计和自适应设计的不同（翻译）"
subtitle:   ""
date:       2015-09-27 17:03:00
author:     "Mariano"
header-img: "img/fast.PNG"
tags: 

    - 翻译 
    - 响应式设计
    - Responsiv Design And Adaptive Design
    - CSS
---    
  
> 第一次翻译文章，肯定有很多的不准确和词汇用得不是特别标准的地方，以后会逐步提高自己翻译的水品  
  
    
正如你期望的那样，这个问题最近被频繁的提及。我们不时得会在 [CSS-Tricks 论坛](https://css-tricks/forums/)看到这些讨论，同样的问题也在我教授 web 设计的时候被问到。


这真是一个<strong>好问题</strong>！  
  
响应式设计自从被[Ethan Maricotte](http://alistapart.com/article/responsive-web-design)在2010年描述以来已经变成一个家喻户晓的术语。诚然我们可能需要去会花点时间理解它。而响应式这个概念在书籍中又是一个重要的 CSS 的“技巧”，并且足够重要乃至于退一万步说是为了提醒我们建造一个是什么的“响应式”网站以及它和“自适应”的不同  
  
OK，既然这样，那我们来看看它们之间有什么不同  
  
# 简略概述 
  
响应式和自适应站点都是基于浏览器浏览视窗改变而改变（最大的相同点莫过于：浏览器的宽度）  
  
响应式网站响应浏览器给予的任何尺寸。也许浏览器的宽度不是那么重要，站点通过布局调节（或者是设计功能）来适配屏幕。在这里，浏览器的<span style="background-color:#ccc">300px</span>或者<span style="background-color:#ccc">30000px</span>亦然不是那么重要了，因为布局总会得到响应。好吧，这至少来说是正确的！ 
  
### HTML CODE  
  
```html 
<div class="module">
	<h1>This is a responsive container</h1>
	<p>This container is <span class="element"></span>pixels wide when the browser is <span class="browser"></span>pixels wide.Resize the browser to see it changge</p>
</div>
```
  
### SCSS CODE   
  
  
```sass
	html{
		background:#333;
	}
	body{
		display:flex;
		justify-content:center;
		align-items:center;
	}
	.module{
		background-color:white;
		border-radius:10px;
		padding:20px;
		width:80%;
	}
```  
  
### JS CODE  
  
```js  
$(".element").html($(".module").width());
$(".browser").html($(window).width());
$(window).resize(function(){
$(".element").html($(".module").width());
$(".browser").html($(window).width());
})
```
    
自适应网站则通过特殊的点来适应浏览器的宽度。换句话说，网站只是聚焦一个浏览器的特殊宽度，通过这个点来到达适应布局  
  
### HTML CODE  
  
```html  
<div class="module">
	<h1>This is an adative container</h1>
	<p>This container is 800 pixels wide when the browser is any width over 500 pixels.Any below that,and the continer shrinks to 300 pxels</p>
</div>  
```  
 
### SCSS CODE  

```sass  
html{
background:#333;
}
body{
display:flex;
justify-content:centerl
align-items:center;
}
.module{
background-color:white;
border-radius:10px;
padding:20px;
width:800px;
}
@meida screen and (max-width:500px){
	.module{
		width:300px;
	}
}
```   
  
   
换个角度来思考就是平滑设计和snap设计的区别（译注：不知道snap design的意思，索性就用原文代替）。响应式设计之所以流畅，是因为无论设备宽高如何，它都会流畅的调节。而自适应设计，换句话说，它感觉卡卡的，因为在浏览器或设备改变宽高的时候，它也在页面做一些事情。下面的一个动画很形象的表明两者之间的不同  
  ![the difference between resposive and adaptive design]({{site.baseurl}}/img/rwd-vs-adapt-example.gif)   
  <hr>
  > <p style="text-align:center">响应式在上面，适应性在下面</p>  
      
注意到响应式的例子是根据环境的变化而流式改变，而自适应有点一卡一卡的  
  
# 详细说明
  
响应式网站和适应性网站的不同从上面的小小的例子可以窥见一二。你甚至可以把它看作为哲学上的不同  
  
让我们来考虑一下Ethan原始定义响应式web设计的关键：  
  
>对于响应式web设计应包含<b style="color:red">流式</b>布局，<b style="color:red">弹性</b>图像和媒体查询三种技术。但它也需要一种不同的思维方式。我们使用媒体查询来逐步提高我们在不同视觉环境下的工作，而不是用来隔离我们的内容以及特定设备的体验  
  
请注意文中的关键词流式(fluid)和弹性(flexible),响应式设计只是为寻找创建适应任何屏幕的优化体验的一种的手段，在这种情况下，设备已变得无关紧要。 这个想法挑战我们去创建一个可以根据给定任意情形改变上下文的网站。这就意味着我们的内容应该是流动的（使用百分比作为计量单位），我们服务的套件应该是弹性的（在正确的时间使用正确的套件服务正确的设备）以及在内容出现断点的时候使用媒体查询（相对于特定屏幕大小的宽度，比如iPhone）  
  
 比较一下我们所认为的自适应，他既不流畅也不灵活，但看起来也像是在一个特定的点实现了适应。显然，想要适应所有不同种的设备是很困难的。这有一个[特定设备的媒体查询](https://css-tricks.com/snippets/css/media-queries-for-standard-devices/)你可以参考一下  
   
     
# 响应式比自适应更好？    
  
我也不能回答这个问题，我相信这是两种不同的哲学，只是响应式设计来自[移动端的首次响应式web设计](https://responsivedesign.is/strategy/page-layout/mobile-first)，对于手边的项目来说你只是选择了一个好工具而已。  
  
你是否对于选择其中的一种感到困惑？如果你知道你的网站支持哪些特定的设备也许你会感到轻松一点。例如你决定iPhone6是你站点的唯一设备，那么适应它比其他设备来的更有效和轻松。另一方面，相对于市场上可能的任何设备(甚至还有尚未发行的)，响应式设计是未来网站发展的一个好策略。   
 
  
# 写在最后的话 
 响应式设计和自适应设计在处理现实中不同设备在不同背景查看网站的方法是相同的，他们只是用了各自的方法而已。  
   
记住：web是原生响应的，直到我们开始设计它时，它不需要响应或适应任何设备。  
  
如果你想更深入的找寻响应式设计，最好的方法就是练习。有足够多的资源帮助你开始，so have at it！，这里有几个让你开始：  
  
* [This is Responsive](http://bradfrost.github.io/this-is-responsive/):A collection of examples, patterns and resources curated by Brad Frost.
* [ResonsiveDesign.is](https://responsivedesign.is/):Another treasure trove of resources, in addition to articles and a podcast!
* [Resonsive Web Design Podcast](http://responsivewebdesign.com/podcast/):Speaking of podcasts, here's one co-hosted by Ethan Marcotte and Karen McGrane.
* [Responsive Web Design,by Ethan Marcotte](http://abookapart.com/products/responsive-web-design):Ethan literally wrote the book on it and did so with the utmost clarity.
  
    
>[原文链接](https://css-tricks.com/the-difference-between-responsive-and-adaptive-design/)
  
 