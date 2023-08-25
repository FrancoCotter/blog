---
layout:  post
title:   "色彩指南"
subtitle:   ""
date:       2023-08-25
author:     "Mariano"
header-img: "img/ColorChartForWebsite_1000x.jpg"
tags:    

   - Color
   - 色彩
   - UI/UX
---      
原文请阅读：[A Nerd’s Guide to Color on the Web](https://css-tricks.com/nerds-guide-color-web/)  
 

``在互联网上，有许多处理颜色的方法。我认为了解所使用的机制是很有帮助的，颜色也不例外。让我们深入探讨一些关于互联网上颜色的技术细节。``  
  
# 颜色混合（Color mixing）   
  
理解色彩的关键是要知道，儿时用色彩的方式与在计算机上使用色彩是不同的，因为存在着颜料混合的问题。儿时，我们使用的是颜料。颜料和打印机墨水中的微小颗粒被称为颜料，它们混合在一起并反射出色彩，呈现在我们的眼睛中。这是减法混合色彩。你加入的颜色越多，颜色就变得越深，直到变成棕色。原色接近你所熟悉的：红、黄、蓝。但是当你将这些颜色与减法混合色彩相结合时，你会得到棕色。

而在计算机（或任何显示器）上，我们使用的是光。这意味着当所有的颜色混合在一起时，它们会形成白色。在艾萨克·牛顿著名的棱镜颜色实验之前，人们认为颜色是存在于物体内部而不是从物体反射和吸收的。牛顿使用棱镜来证明他的理论，即阳光或明亮的白光实际上是由几种颜色组成的。他用棱镜将这些颜色分离，形成了彩虹，并尝试进一步分离蓝色。蓝色没有分离，表明颜色并不是在棱镜内部，而是棱镜在分离光线。这意味着在加法混合色彩中，也就是我们在显示器中看到的颜色混合方式，红、绿和蓝可以用来产生所有颜色，即RGB。在这种混合方式中，红色和绿色混合会生成黄色。 
<div class="p">
    <div class="p5">
    <img src="{{site.baseurl}}/img/pigment.jpg">
    </div>
    <div class="p5">
        <img src="{{site.baseurl}}/img/color-mixing.jpg">
    </div>
    <style>
       .p{display: flex;justify-content: space-between; width: 100%;}.p5{width: 50%;}.p5 img{width: 100%;display: block;}
    </style>
</div> 


