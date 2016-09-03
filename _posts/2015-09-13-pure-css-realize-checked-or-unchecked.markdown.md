---
layout:     post
title:      "纯CSS实现选中取消"
subtitle:   ""
date:       2015-09-13 17:03:00
author:     "Mariano"
header-img: "img/css.png"
tags: 

    - CSS  
    - 前端  
---  
  
	  
	      
在以前需要实现对一排单选按钮后附有Label标签，通过label标签实现选中或非选中的时候，我们通常都会考虑使用js来实现，但用js实现的过程中，可能会有资源占用率的问题，所以，当我在做一个类似的项目的时候，我首先就是用js来写，因为简单、方便，不需要动什么脑子，可是考虑到资源占用率的问题或者对网络进行优化的时候，我不得不重新审视一下我的代码，我决定还是使用纯css来处理这个问题，下面给出我的思路

一排单选按钮，要想其中只能点选一个，就必须给所有的单选按钮设置一个相同的name。比如：  
  
```html
<input type='radio' name='test'/>
<input type='radio' name='test'/>
<inout type='radio' name='test'/>  
```  
后面在跟上一个label标签，要想label标签和单选按钮对应，就必须给所有的单选按钮设置id，并让后面的label标签对应此id，如：  

```html 
<input type='radio' name='test' id='radio-one'>
<label for='radio-one'>这是对应的radio1</label>
<input type='radio' name='test' id='radio-two'>
<label for='radio-two'>这是对应的radio2</label>
<input type='radio' name='test' id='radio-three'>
<label for='radio-three'>这是对应的radio3</label>  
```  
	  
html结构部分我们就书写完毕了，那么我们怎么通过css来实现选中取消呢，方法很简单，就是让所有的radio隐藏，通过使用为类来实现，代码如下：  

``` css 
input[type="radio"]{display:none;}
input[type="radio"]+label{background:#ccc;height:20px;width:50px;padding:1em 1.2em}
input[type="radio"]:checked+label{background:orange;}  
```  
	  
方法就是这样，是不是很简单就实现了  
  
  
  
    
#看一下效果吧  
  
  
![]({{site.baseurl}}/img/css-pure.gif)
	
