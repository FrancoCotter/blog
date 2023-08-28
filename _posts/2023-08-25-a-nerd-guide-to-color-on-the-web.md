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
原文请阅读：[A Nerd’s Guide to Color on the Web](https://css-tricks.com/nerds-guide-color-web/){:target="_blank"}    
 

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
       .p{display: flex;justify-content: space-between; width: 100%;align-items: baseline;margin-bottom:1em}.p5{width: 50%;}.p5 img{width: 100%;display: block;}
    </style>
</div>   
    

监视器是由许多小的光点组合而成的，它们共振产生了无数的颜色。分辨率是指显示器上包含的个别彩色点（即像素）的数量。在我们拥有监视器之前，艺术家们就一直在使用这种类型的光频率。塞拉和点彩派艺术家们用红色和绿色混合创造出黄色，就像《拉·格札特》中的绘画作品一样（尽管他更倾向于使用术语“色光素派”。其他人称之为分割主义）。这种绘画是基于一种信念创作的，即光学混合在你的眼中创造出更纯粹的共鸣，而传统的减法颜料混合则不然。

![]({{site.baseurl}}/img/seurat-detail.jpg)

监视器有几种不同的显示模式，它们改变了我们通过它们感知颜色的方式。我们用术语“色彩位深”来表达这一点。可以同时显示的颜色数量由色彩位深决定。如果我们的位深为1，我们可以产生两种颜色，即单色。位深为两级时可以创建4种颜色，依此类推，直到达到32位深。然而，常见的用于网络的监视器具有24位深度和16,777,216种颜色，即真彩色和透明通道。

我们称之为真彩色是因为我们的人眼可以辨别出10,000,000种独特的颜色，因此24位深度肯定可以满足这一需求。在这24位深度中，有8位用于红色、绿色和蓝色。其余的位用于透明度或Alpha通道。

让我们利用这些珍贵的信息来探究一下网络上可用的颜色属性吧。      
  
# 色值（Color values）  
  

最后一节展示了rbga（x，x，x，y）的含义，但让我们更详细地解释一下，并展示一些其他属性及其用途。在RGB通道的网页颜色值中，我们在0-255的范围内指定颜色。  
  
```
x is a number from 0-255
y is a number from 0.0 to 1.0
rgb(x, x, x); or rgba(x, x, x, y);

Example: rbga(150, 150, 150, 0.5);
```  
  
# Hex 值（Hex Values）  
  
Hex colors是开发人员在Web上指定颜色的最常见方式。它采用了一种十分精巧的表示方法，让计算机轻松理解并快速处理颜色。

让我们回顾一下字节的概念，它由8位组成。每个Hex color或数字代表一个字节，用来表示红、绿和蓝三个分量的强度。这种三元组的表示方式简洁明了，每个分量使用两位来表示。在Hexadecimal（十六进制）系统中，一个字节的值范围从00到FF，相当于十进制的0到255。

Hexadecimal之所以得名，是因为它使用了基数为16的系统。在这个系统中，值的表示采用了0到9和A到F的字符，0代表最低值，而F代表最高值。因此，#000000代表纯黑色，而#FFFFFF代表纯白色。

为了更加简洁和便于书写，在一些情况下，我们可以使用缩写形式来表示重复值的三元组。例如，#00FFFF可以简写为#0FF。这种缩写形式在编程中非常实用，方便快捷。

Hex colors不仅仅是计算机理解的一种方式，它也是一种视觉上美观的设计语言。通过Hex colors，我们能够轻松地表达出各种鲜艳丰富的色彩，为Web界面带来更加生动和吸引人的外观。但是，如果您要更深入地处理颜色，HSL（色调、饱和度、亮度）可能更容易阅读。  
  
# HSL值（HSL Values）  
  
HSL值，即色相（Hue）、饱和度（Saturation）和亮度（Lightness）值，提供了一种复杂的颜色表示方法。与RGB值依赖于显示器对颜色的解释方式不同，HSL值是基于人类视觉和Munsell色彩系统的原理运作的。

在这个系统中，颜色被分解为三个基本组成部分。首先是色相，它决定了颜色在色轮上的位置。色相以0°至360°的角度进行测量，红色为0°，绿色为120°，蓝色为240°。通过调整色相值，可以实现广泛的鲜艳颜色。

接下来是饱和度，它定义了颜色的纯度或强度。饱和度的值范围从0%（灰色或去饱和）到100%（完全饱和和鲜艳）。调整饱和度值可以创建出细微的淡色或大胆醒目的色调。

最后是亮度，它决定了颜色的亮度或暗度。亮度值范围从0%（黑色）到100%（白色）。通过修改亮度值，我们可以创建出各种深沉和阴暗的色调，也可以创建出明亮通透的色调。

HSL色彩模型根植于数学原理和人类视觉感知，提供了一种强大而细致的表达和操控颜色的方式。它允许更大的控制和创造力，使我们能够打造出视觉上令人惊叹和和谐的配色方案。  
   
![]({{site.baseurl}}/img/Munsell_1929_color_solid.png)
  
    
色相在360度（一个完整的圆）上旋转，而饱和度和亮度是从0到100的百分比值。  
  
```
x is a number from 0 - 360
y is a percentage from 0% to 100%
z is a number from 0.0 to 1.0
hsl(x, y, y); or hsla(x, y, y, z);

Example: hsla(150, 50%, 50%, 0.5);
```  
  

在计算机领域，浏览器之间转换RGB和HSL值只需要简单的代码改动（准确来说，只需11行代码）。然而，对于我们这些普通人来说，使用HSL更加直观易懂。想象一下一个圆轮，中心是浓烈饱和的内容。这个华丽的演示完美展示了HSL的表达方式。
  
![]({{site.baseurl}}/img/hsla.gif)  
  
**几年前，Chris还开发了一个很棒的工具，名为"hsla explorer"，你可以在[这里查看](https://css-tricks.com/examples/HSLaExplorer/){:target="_blank"} 。**
  

如果你对处理颜色没什么特别的技巧，hsla()提供了一些相当简单的规则，可以为开发者创建出漂亮的效果。在下面的生成色彩部分，我们将更详细地介绍这个。  
  
# 命名颜色（Named Colors）  
  
作为开发人员，我们也可以使用命名颜色。然而，命名颜色因其不准确性而被认为难以处理。最著名且“出名”的例子是，深灰实际上比灰色更浅，而青柠和青柠绿是完全不同的颜色。甚至有一个由Chris Heilmann制作的网页游戏，你可以在其中尝试猜测命名颜色。在过去，chucknorris被定义为一种血红色（就我所知，现在只在HTML中支持），但这是我最喜欢的颜色之一。命名颜色可以用于快速演示颜色的使用，但通常开发人员使用Sass或其他预处理器将颜色值存储为十六进制、RGBA或HSLA，并将它们映射到公司内部使用的颜色名称。  
  
# 颜色变量（Color Variable）    

一个好的做法是将颜色变量存储起来，而不直接使用它们，而是将它们映射到具有更语义化命名方案的其他变量中。CSS具有原生变量，例如：  
  
```less

:root {
  --brandColor: red;
}
body {
  background: var(--brandColor);
} 

```  
  
但在撰写本文时，这些变量在微软浏览器中尚未得到广泛应用。

CSS预处理器也支持变量，因此您可以设置变量，例如$brandPrimary，并在代码库中使用它们。或者使用一个映射：    
  
``` less

$colors:(
    mainBrand:#FA6ACC,secondaryBrand:#F02A52,highlight:#09A6E5
);
@function color($key){
    @if map-has-key($colors,$key){
        @return map-get($colors,$key);
    }
    @warn "Unknow `#{$key}` in $colors.";
    @return null;
}
// _component.scss
.element{
    background-color:color(hightlight); // #09A6E4
}

```   

请记住，在这里命名非常重要。抽象的命名有时很有用，这样，如果您将表示蓝色的变量更改为橙色，您就不必逐个重命名所有的颜色值。更糟糕的是，不要放出一个标志说“$blue现在是橙色。”（哀伤的长号声）   

   
# 当前颜色关键字（currentColor）      
  
currentColor是一个非常有用的值。它遵循层叠规则，并且对于将颜色值扩展到盒阴影、轮廓、边框甚至背景等方面非常有用。

假设您创建了一个div，然后在其中创建了另一个div。下面的代码将为内部div创建橙色边框：  
  
```scss
.div-external{color:orange;}
.div-internal{border:1px solid currentColor;}
```  
  
这对于图标系统非常有用，无论是SVG图标还是图标字体。您可以将currentColor设置为填充（fill）、描边（stroke）或颜色（color）的默认值，然后使用语义化适当的CSS类来样式化。   

# 预处理器（Preprocessors）    
  
CSS预处理器非常适用于调整颜色。以下是一些不同预处理器关于颜色函数的文档链接：  
  
* [Sass functions](https://sass-lang.com/documentation/modules/){:target="_blank"}  
* [Less functions](https://lesscss.org/functions/#color-operations){:target="_blank"}  
* [Stylus functions](https://stylus-lang.com/docs/bifs.html){:target="_blank"}  
* [颜色函数的PostCSS插件](https://github.com/postcss/postcss-color-function){:target="_blank"}  示例  
  

以下是我们可以使用Sass进行的一些酷炫操作：  
  
```scss
mix($color1, $color2, [$weight])
adjust-hue($color, $degrees)
lighten($color, $amount)
darken($color, $amount)
saturate($color, $amount)
```    
  

确实，使用预处理器可以以编程方式混合和修改颜色的方法有数十种，我们不会深入讨论所有方法，但是以下是一个很好的[互动资源](http://jackiebalzer.com/color){:target="_blank"}，可以提供更详细的信息。  
  
# 颜色属性（Color Properties）    
  
在CSS中，颜色属性可以用于设置字体颜色。如果您要设置一个大区域的颜色，应该使用background-color属性，除非是SVG元素，这时您应该使用fill属性。边框可以使用border属性来设置HTML元素的边框，而SVG元素则使用stroke属性。  
  

  
# 盒子阴影和文本阴影（Box and Text Shadows）  
  

 box-shadow和text-shadow属性可以接受颜色值。文本阴影可以接受2-3个值，即水平阴影（h-shadow）、垂直阴影（v-shadow）和可选的模糊半径。盒子阴影可以接受2-4个值，包括水平阴影、垂直阴影、可选的模糊距离和可选的扩展距离。您还可以在开始时使用"inset"关键字来创建倒置的阴影效果。这个[网站](http://www.cssmatic.com/box-shadow){:target="_blank"}  提供了一个很好的演示，其中包含易于复制粘贴的代码。   
   

 # 渐变（Gradients）  

 
线性渐变通过指定方向来实现，可以选择从上到下、从下到上、从左到右、从右到左、指定角度或径向渐变。在渐变中，我们可以指定不同颜色的停止点，并在每个停止点处定义所需的颜色。这些颜色停止点也可以包含透明度。  
  

事例：  
  
<p class="codepen" data-height="300" data-theme-id="light" data-default-tab="result" data-slug-hash="gOZPRJG" data-user="Mariano_M" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>  
  

 
大多数渐变的语法并不难编写，但我非常喜欢使用[在线渐变生成器](https://www.colorzilla.com/gradient-editor/){:target="_blank"}  ，~~因为它还会为了支持IE6-9而创建复杂的filter属性~~。这里[还有一个非常漂亮的UI渐变生成器](https://uigradients.com/#Combi){:target="_blank"}  。这个生成器非常酷，而且是开源的，你可以为其做出贡献。    
  

在SVG中创建渐变也同样简单。我们可以定义一个带有id的块，并在其中引用。我们还可以选择性地定义渐变的表面区域。  
  
```html
<linearGradient id="Gradient">
  <stop id="stop1" offset="0" stop-color="white" stop-opacity="0" />
  <stop id="stop2" offset="0.3" stop-color="black" stop-opacity="1" />
</linearGradient>
```  
  
这些渐变也支持不透明度，所以我们可以实现一些很好的效果，例如将它们作为遮罩进行动画处理，以及图层效果。  
  
<p class="codepen" data-height="300" data-theme-id="light" data-default-tab="result" data-slug-hash="YzdwQmZ" data-user="Mariano_M" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>  
  

在WebKit浏览器中，也可以实现渐变文本效果，我们在[CSS-Tricks网站](https://css-tricks.com/snippets/css/gradient-text/){:target="_blank"}  上有一个非常好的代码片段可以使用。  
  

# 生成色彩（Generative Color）    
  

有一些很酷的方法可以一次性生成许多令人惊叹的色彩。当用代码创建生成艺术或UI元素时，我发现这些方法非常有趣。

只要保持在上一节指定的范围内，你可以在Sass（或任何CSS预处理器）或JavaScript中使用for循环，或者使用Math.Random()和Math.floor()来获取颜色值。我们需要使用Math.floor()或Math.ceil()，因为如果我们不返回整数，就会出错，无法得到一个有效的颜色值。

一个好的经验法则是不要同时更新所有三个值。我发现，在一个值范围内有较大的偏差，第二个值范围内有较小的偏差，而第三个值则没有偏差，效果很好。例如，使用hsl色彩模型非常方便，因为你知道从0到360循环遍历色调将给你一个完整的范围。而hue-rotate属性的角度是一个完整的圆，所以你不必局限于0到360的范围，甚至可以尝试使用-480或600等值，浏览器仍然可以解析。  
  
```less
    @mixin colors($max,$color-frequency){
    $color:300/$max;
    @for $i from 1 through $max{
        .s#{$i}{
            border: 1px solid hsl(($i-10)*($color*1.25),($i-1)*($color/$color-frequency),40%);
            }
        }
    } 
    .demo{
    @include colors(20,2);
    }
```  
  
在这个演示中，我使用这些方法来制作水果圈颜色。  
  
<p class="codepen" data-height="300" data-theme-id="light" data-default-tab="result" data-slug-hash="wvRMqvX" data-user="Mariano_M" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>  
  

同样地，还有这个，使用不同的范围（在列表中快速滚动）  
  
<p class="codepen" data-height="300" data-theme-id="light" data-default-tab="result" data-slug-hash="abPdyzv" data-user="Mariano_M" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>



在下面的代码中，我借助Math.random()函数，将其应用于RGB值中，以在相同的范围内生成丰富多彩的颜色。这个演示是基于React的三维虚拟现实体验。如果我使用for循环，也能达到相同的效果，但我选择随机化颜色以反映运动的感觉。这个项目的创意无限。  

[![]({{site.baseurl}}/img/three2.png)](https://sdras.github.io/react-aframe-demo1/){:target="_blank"}  
  
<p align="center">点击图片查看事例</p>    
  

# JavaScript  

```js
class App extends React.Component {
  render () {
    const items = [],
          amt1 = 5,
          amt2 = 7;
    for (let i = 0; i < 30; i++) {
     let rando = Math.floor(Math.random() * (amt2 - 0 + 1)) + 0,
          addColor1 = parseInt(rando * i),
          addColor2 = 255 - parseInt(7 * i),
          updateColor = `rgb(200, ${addColor1}, ${addColor2})`;
      items.push(
	    // ...
        );
    }
    return (
       // ...
       {items}
      
    );
  }
}
```  

  

  

  




