---

layout:  post
title:   "完整的 CSS Grid 指南"
subtitle:   ""
date:       "2023-08-24 18:53:00"
author:     "Mariano"
header-img: "img/CSS-GRID-3.png"
tags:  

   - CSS Grid
   - 界面设计
  
---      

    

原文请阅读[A Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/#aa-grid-template-columnsgrid-template-rows)  
   
#### CSS 网格的综合指南，重点关注网格父容器和网格子元素的设置。  
  
# 目录  
第一部分: <a href="#介绍">介绍</a>      
第二部分: <a href="#基本">基本</a>  
第三部分: <a href="#重要术语">重要术语</a>  
第四部分: <a href="#网格属性">网格属性</a>  
第五部分: <a href="#特殊单位和功能">特殊单位和功能</a>    
第六部分: <a href="#流式宽度列的代码片段">流式宽度列的代码片段</a>  

     
# 介绍  

### CSS 网格介绍    
  
CSS Grid Layout（又称为“Grid”或“CSS Grid”）是一种基于二维网格的布局系统，与过去的任何网页布局系统相比，它彻底改变了我们设计用户界面的方式。CSS 一直被用来布局网页，但它在这方面的表现并不出色。我们先是使用表格，然后是浮动、定位和内联块，但所有这些方法本质上都是权宜之计，而且缺少许多重要的功能（例如垂直居中）。虽然 Flexbox 也是一个很棒的布局工具，但它的单向流动适用于不同的场景——但实际上，Grid 与 Flexbox 非常好地协同工作！Grid是专门为解决我们在制作网站时长期以来一直苦苦摸索的布局问题而创建的第一个 CSS 模块。

本指南的目的是以最新版本规范存在的 Grid 概念为基础进行介绍。因此，我不会涵盖过时的 Internet Explorer 语法（尽管您当然可以在 IE 11 中使用 Grid）或其他历史性的权宜之计。

# 基本    
  
截至2017年3月，大多数浏览器（包括 Chrome、Firefox、Safari 和 Opera）已经在最新版本中原生支持 CSS Grid，不再需要加上浏览器前缀。不过，Internet Explorer 10 和 11 也支持 Grid，但使用了旧版本的实现和过时的语法。现在是利用 Grid 进行开发的最佳时机！

开始使用 Grid 布局，您需要将一个容器元素定义为网格，通过设置 `display: grid` 来实现，然后通过 `grid-template-columns` 和 `grid-template-rows` 来设置列和行的大小。接下来，通过 `grid-column` 和 `grid-row` 属性将子元素放入网格中。类似Flexbox，网格项的源顺序并不重要。您可以使用 CSS 以任意顺序来放置它们，这使得使用媒体查询来重新排列网格非常简单。想象一下，只需几行 CSS 代码就可以定义整个页面的布局，并通过媒体查询轻松地重新调整。
  
# 重要术语    
  

在深入了解 Grid 的概念之前，理解相关术语是非常重要的。由于涉及的术语在概念上都有相似之处，如果不先记住 Grid 规范中定义的它们的含义，很容易将它们混淆。但是不要担心，这些术语并不多。  
  
## Grid Container（网格容器） 
  
`display: grid` 被应用于的元素。它是所有网格项的直接父元素。在这个例子中，`container`是网格容器。   



### Grid Line（网格线）  
  
构成网格结构的分割线。它们可以是垂直的（"列网格线"）或水平的（"行网格线"），并位于行或列的两侧。在这里，黄色线是列网格线的一个例子。   
  
![]({{site.baseurl}}/img/terms-grid-line.svg)
  
### Grid Track（网格轨道）  
 
相邻网格线之间的空间。你可以将它们看作是网格的列或行。这是第二行和第三行网格线之间的网格轨道。   

![]({{site.baseurl}}/img/terms-grid-track.svg) 
  
### Grid Area（网格区域）  
  
由四个网格线所围绕的总空间。一个网格区域可以由任意数量的网格单元组成。这是在行网格线1和3以及列网格线1和3之间的网格区域。    
  
![]({{site.baseurl}}/img/terms-grid-area.svg) 

## Grid Item（网格项）  

网格容器的子元素（即直接后代）。在这里，item 元素是网格项，而 sub-item 不是。    


### Grid Cell（网格单元格）  
   
相邻行和相邻列网格线之间的空间。它是网格的一个单一“单元”。这是在第 1 行和第 2 行网格线之间，第 2 列和第 3 列网格线之间的网格单元格。  
  
![]({{site.baseurl}}/img/terms-grid-cell.svg) 

  
# 网格属性  

### 父元素的属性 （网格容器）   

#### display    

定义元素为网格容器，并为其内容建立一个新的网格格式化环境。   

值：    

 * `grid` - 生成一个块级网格容器，使其子元素按网格布局排列。
 * `inline-grid` - 生成一个内联级网格容器，使其子元素按网格布局排列。
 
  

#### grid-template-columns | grid-template-rows  

以用空格分隔的数值列表定义网格的列和行。这些数值代表轨道的尺寸，而它们之间的间隔则象征着网格线。

值：  

`<track-size>` - 可以是一个长度、一个百分比，或者使用 fr 单位表示网格中可用空间的分数。  

`<line-name>` - 您可以随意选择一个名称，比如"任意名称"。    


```css  
      .container {
        grid-template-columns: ...  ...;
        /* e.g. 
            1fr 1fr
            minmax(10px, 1fr) 3fr
            repeat(5, 1fr)
            50px auto 100px 1fr
        */
        grid-template-rows: ... ...;
        /* e.g. 
            min-content 1fr min-content
            100px 1fr max-content
        */
        }
```

网格线会自动从这些分配中分配正数，其中 -1 是最后一行的替代。   

![]({{site.baseurl}}/img/template-columns-rows-01.svg)  
  

但是您可以选择明确命名网格线。请注意线条名称的括号语法：    
  
```css
.container {
  grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end];
  grid-template-rows: [row1-start] 25% [row1-end] 100px [third-line] auto [last-line];
}
```  
![]({{site.baseurl}}/img/template-columns-rows-02.svg)   

  
请注意，一条线可以有多个名称。例如，在这里，第二条线将有两个名称：row1-end 和 row2-start：  
  
```css  
    .container {
        grid-template-rows: [row1-start] 25% [row1-end row2-start] 25% [row2-end];
    }
```  

如果您的定义包含重复部分，可以使用 repeat() 表示法来简化操作：   

```css
    .container {
        grid-template-columns: repeat(3, 20px [col-start]);
    }
```  


这等同于：  
  
```css 
    .container {
        grid-template-columns: 20px [col-start] 20px [col-start] 20px [col-start];
    }
```  
如果多行共享相同的名称，可以通过它们的行名和计数来引用它们。  
 
```css
    .item {
        grid-column-start: col-start 2;
    }
```  

`fr` 单位允许您将轨道的大小设置为网格容器的可用空间的一部分。例如，这将使每个项目的宽度为网格容器的三分之一：  

```css
    .container {
        grid-template-columns: 1fr 1fr 1fr;
    }
```       
在任何非灵活项之后计算可用的自由空间。在这个例子中，可供 fr 单位使用的自由空间总量不包括 50px：  
  
```css
    .container {
        grid-template-columns: 1fr 50px 1fr 1fr;
    }
```    
  
####  grid-template-areas  
  
通过引用使用 `grid-area` 属性指定的网格区域的名称来定义网格模板。重复网格区域的名称会使内容跨越这些单元格。句点表示一个空单元格。语法本身提供了网格结构的可视化。  
  
值：   
  
* `<grid-area-name>` - 是使用grid-area指定的网格区域的名称。  
* `.` - 句点表示一个空的网格单元格。 
* `none` - 没有定义网格区域。    
  
```css  
    .container {
        grid-template-areas: 
            "<grid-area-name> | . | none | ..."
            "...";
    }
```  
  
示例：  
  
```css  
    .item-a {
        grid-area: header;
    }
    .item-b {
        grid-area: main;
    }
    .item-c {
        grid-area: sidebar;
    }
    .item-d {
        grid-area: footer;
    }

    .container {
        display: grid;
        grid-template-columns: 50px 50px 50px 50px;
        grid-template-rows: auto;
        grid-template-areas: 
            "header header header header"
            "main main . sidebar"
            "footer footer footer footer";
    }
```  
这将创建一个由四列和三行组成的网格。整个顶部行将由标题区域组成。中间行将由两个主要区域、一个空单元格和一个侧边栏区域组成。最后一行是页脚区域。    
  
![]({{site.baseurl}}/img/dddgrid-template-areas.svg)  
  
您在声明中的每一行都需要有相同数量的单元格。

您可以使用任意数量的相邻句点来声明一个空单元格。只要句点之间没有空格，它们就表示一个单元格。

请注意，这种语法中没有为行命名，只有为区域命名。当您使用此语法时，区域两端的行实际上会自动获得名称。如果您的网格区域名为 `foo`，则该区域起始行线和起始列线的名称将为 `foo-start`，而最后一行线和最后一列线的名称将为 `foo-end`。这意味着某些行可能会有多个名称，例如上述示例中的最左边的行，它将有三个名称：header-start、main-start 和 footer-start。  
  
####  grid-template  
  
一种用于在单个声明中设置 `grid-template-rows`、`grid-template-columns` 和 `grid-template-areas` 的快捷方式。  
  
值：  

  * `none` -  将所有三个属性设置为初始值  
  * `<grid-template-rows> / <grid-template-columns>` - 分别将 grid-template-columns 和 grid-template-rows 设置为指定的值，并将 grid-template-areas 设置为 none。  
      
```css
    .container {
        grid-template: none | <grid-template-rows> / <grid-template-columns>;
    }
```  

它还接受一种更复杂但非常方便的语法来指定所有三个属性。这里是一个例子：   

```css
    .container {
        grid-template:
            [row1-start] "header header header" 25px [row1-end]
            [row2-start] "footer footer footer" 25px [row2-end]
            / auto 50px auto;
    }
```  
这等同于以下内容： 

```css
    .container {
        grid-template-rows: [row1-start] 25px [row1-end row2-start] 25px [row2-end];
        grid-template-columns: auto 50px auto;
        grid-template-areas: 
            "header header header" 
            "footer footer footer";
    }
```  

由于 grid-template 不会重置隐式网格属性（grid-auto-columns、grid-auto-rows 和 grid-auto-flow），这在大多数情况下可能是您想要做的，建议使用 grid 属性而不是 grid-template。  
  

####  column-gap | row-gap | grid-column-gap | grid-row-gap    

指定网格线的大小。您可以将其视为设置列/行之间的间距宽度。  
  
值：  

 * `<line-size>` - 一个长度值  
   
```css
    .container {
        /* standard */
        column-gap: <line-size>;
        row-gap: <line-size>;

        /* old */
        grid-column-gap: <line-size>;
        grid-row-gap: <line-size>;
    }
```  
  
示例：  

```css
    .container {
        grid-template-columns: 100px 50px 100px;
        grid-template-rows: 80px auto 80px; 
        column-gap: 10px;
        row-gap: 15px;
    }
```  
  
![]({{site.baseurl}}/img/dddgrid-gap.svg)    
  

这些间距只会在列/行之间创建，而不会在外边缘创建。

***注意：grid-前缀将被移除，并且 grid-column-gap 和 grid-row-gap 将被重命名为 column-gap 和 row-gap。非前缀属性已经在 Chrome 68+、Safari 11.2 Release 50+ 和 Opera 54+ 中得到支持。***
  

####  gap | grid-gap  
  
row-gap 和 column-gap 的简写方式是 gap。  
  
值：
* `<grid-row-gap> <grid-column-gap>` - 一个长度值    
  
```css
    .container {
        /* standard */
        gap: <grid-row-gap> <grid-column-gap>;
        /* old */
        grid-gap: <grid-row-gap> <grid-column-gap>;
    }
```    

示例： 

```css
    .container {
        grid-template-columns: 100px 50px 100px;
        grid-template-rows: 80px auto 80px; 
        gap: 15px 10px;
    }
```  

如果没有指定 row-gap，则设置为与 column-gap 相同的值。

***注意：grid-前缀已被弃用（但谁知道，可能永远不会从浏览器中删除）。实质上，grid-gap被重命名为gap。无前缀的属性已经在Chrome 68+，Safari 11.2 Release 50+和Opera 54+中得到支持。***  

  
####  justify-items  
  
沿着行内（行）轴对齐网格项（与 align-items 相反，align-items 是沿着块（列）轴对齐）。该值适用于容器中的所有网格项。   

值：    

* `start` – 将项目与其单元格的起始边缘对齐
* `end` – 将项目与其单元格的末尾边缘对齐 
* `center` – 将项目居中对齐于其单元格 
* `stretch` – 填充整个单元格的宽度（默认值）  

  
```css  
   .container {
        justify-items: start | end | center | stretch;
    }
```   

示例：   

```css  
    .container {
        justify-items: start;
    }
```  
  
![]({{site.baseurl}}/img/justify-items-start.svg)      

```css
    .container {
        justify-items: end;
    }
```  
 ![]({{site.baseurl}}/img/justify-items-end.svg)  
```css
    .container {
        justify-items: center;
    }
```    
![]({{site.baseurl}}/img/justify-items-center.svg)  
```css
    .container {
        justify-items: stretch;
    }
```    
![]({{site.baseurl}}/img/justify-items-stretch.svg)    

这个行为也可以通过justify-self属性在单个网格项上进行设置。  

  
####  align-items  

将网格项沿着块（列）轴对齐（与沿着内联（行）轴对齐的justify-items相对）。此值适用于容器内的所有网格项。  
  
值：  

* `stretch` - 将项目填充到单元格的整个高度（默认值）
* `start` - 将项目与其单元格的起始边缘对齐
* `end` - 将项目与其单元格的结束边缘对齐 
* `center` - 将项目居中对齐于其单元格 
* `baseline` - 沿着文本基线对齐项目。有基线的修饰符 - 第一个基线和最后一个基线，它们将在多行文本的情况下使用第一行或最后一行的基线。  
  
```css
    .container {
        align-items: start | end | center | stretch;
    }
```  
示例：  

```css
.container {
  align-items: start;
}
```      
![]({{site.baseurl}}/img/align-items-start.svg)    

```css
.container {
  align-items: end;
}
```    
![]({{site.baseurl}}/img/align-items-end.svg)   

```css
.container {
  align-items: center;
}
```    

![]({{site.baseurl}}/img/align-items-center.svg)     

```css
.container {
  align-items: stretch;
}
```  
![]({{site.baseurl}}/img/align-items-stretch.svg)     


这种行为也可以通过 align-self 属性在单个网格项目上设置。

还有修饰关键字 safe 和 unsafe（用法类似于 align-items: safe end）。安全关键字表示“尝试按照此方式对齐，但如果导致项目移动到无法访问的溢出区域，则不要对齐”，而不安全则允许将内容移动到无法访问的区域（“数据丢失”）。  
  

####  place-items  
  
place-items 属性可以在单个声明中设置 align-items 和 justify-items 属性。

值：

* `<align-items> / <justify-items>` - 第一个值设置 align-items，第二个值设置 justify-items。如果省略第二个值，则第一个值将分配给两个属性。 有关更多详情，请参阅 align-items 和 justify-items。

这对于快速实现多方向居中非常有用：

```css
    .center {
    display: grid;
    place-items: center;
    }
```  
####  justify-content  

有时，网格的总大小可能小于其网格容器的大小。如果所有网格项都使用非弹性单位（如px）进行大小调整，就可能发生这种情况。在这种情况下，您可以设置网格在网格容器内的对齐方式。该属性沿着行轴（而不是 align-content 属性沿着列轴）对齐网格。

值：

* `start` - 将网格与网格容器的起始边对齐 
* `end` - 将网格与网格容器的结束边对齐 
* `center` - 将网格居中对齐于网格容器 
* `stretch` - 调整网格项的大小，以使网格填充网格容器的整个宽度 
* `space-around` - 在每个网格项之间放置均等的空间，两端的空间为半个大小 
* `space-between` - 在每个网格项之间放置均等的空间，两端没有空间 
* `space-evenly` - 在每个网格   
  
```css
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;    
}
```  
  
示例：  
  
```css
.container {
  justify-content: start;
}
```    
![]({{site.baseurl}}/img/justify-content-start.svg)     
```css
.container {
  justify-content: end;    
}
```  
![]({{site.baseurl}}/img/justify-content-end.svg)     
```css
.container {
  justify-content: center;    
}
```  
![]({{site.baseurl}}/img/justify-content-center.svg)      
```css
.container {
  justify-content: stretch;    
}
```  
![]({{site.baseurl}}/img/justify-content-stretch.svg)       
```css
.container {
  justify-content: space-around;    
}
```  
![]({{site.baseurl}}/img/justify-content-space-around.svg)       
```css
.container {
  justify-content: space-between;    
}
```  
![]({{site.baseurl}}/img/justify-content-space-between.svg)       
```css
.container {
  justify-content: space-evenly;    
}
```    
![]({{site.baseurl}}/img/justify-content-space-evenly.svg)     
####  align-content  

 
有时候，你的网格的总大小可能小于其网格容器的大小。这可能是因为你的所有网格项都使用像素（px）等非弹性单位进行大小设置。在这种情况下，你可以设置网格在网格容器内的对齐方式。这个属性将网格沿着块（列）轴对齐（与 justify-content 属性相反，它是沿着内联（行）轴对齐网格）。  

值：
* `start` - 将网格与网格容器的起始边对齐 
* `end` - 将网格与网格容器的结束边对齐 
* `center` - 将网格居中对齐于网格容器 
* `stretch` - 调整网格项的大小以使网格填充网格容器的整个高度 
* `space-around` - 在每个网格项之间放置相等数量的空间，两端的空间大小为一半 
* `space-between` - 在每个网格项之间放置相等数量的空间，两端没有空间 
* `space-evenly` - 在每个网格项之间放置相等数量的空间，包括两端的空间   
  

```css
.container {
  align-content: start | end | center | stretch | space-around | space-between | space-evenly;    
}
```    
  
示例：  
  
```css
.container {
  align-content: start;    
}
```  
![]({{site.baseurl}}/img/align-content-start.svg) 

```css
.container {
  align-content: end;    
}
```  
![]({{site.baseurl}}/img/align-content-end.svg)  

```css
.container {
  align-content: center;    
}
```  
![]({{site.baseurl}}/img/align-content-center.svg)  

```css
.container {
  align-content: stretch;    
}
```  
![]({{site.baseurl}}/img/align-content-stretch.svg)  

```css
.container {
  align-content: space-around;    
}

```  
![]({{site.baseurl}}/img/align-content-space-around.svg)   

```css
.container {
  align-content: space-between;    
}
```  
![]({{site.baseurl}}/img/align-content-space-between.svg) 

```css
.container {
  align-content: space-evenly;    
}
```    
![]({{site.baseurl}}/img/align-content-space-evenly.svg)       

####  place-content  

 
place-content属性可以在一个声明中同时设置align-content和justify-content属性。

值：

* `<align-content> / <justify-content>` - 第一个值设置 align-content，第二个值设置 justify-content。如果省略第二个值，则将第一个值分配给两个属性。 除了 Edge 浏览器外，所有主要浏览器都支持 place-content 简写属性。

有关更多详细信息，请参阅 align-content 和 justify-content。  
  

####  grid-auto-columns | grid-auto-rows  
  
grid-auto-rows 属性用于指定任何自动生成的网格轨道（也称为隐式网格轨道）的大小。当网格项多于网格中的单元格或者网格项放置在显式网格之外时，会创建隐式轨道。

值：

* `<track-size>` - 可以是长度、百分比或网格中的可用空间的一部分（使用 fr 单位）  
  
```css
.container {
  grid-auto-columns: <track-size> ...;
  grid-auto-rows: <track-size> ...;
}
```
 
为了说明隐式网格轨道是如何创建的，请考虑以下情况：  
```css
.container {
  grid-template-columns: 60px 60px;
  grid-template-rows: 90px 90px;
} 
```    
![]({{site.baseurl}}/img/grid-auto-columns-rows-01.svg)  

这将创建一个 2 x 2 的网格。

但是现在想象一下，您使用 grid-column 和 grid-row 来定位您的网格项，像这样：  

 ```css
 .item-a {
  grid-column: 1 / 2;
  grid-row: 2 / 3;
}
.item-b {
  grid-column: 5 / 6;
  grid-row: 2 / 3;
}
 ```   

![]({{site.baseurl}}/img/grid-auto-columns-rows-02.svg)  

我们告诉.item-b 从列线 5 开始，到列线 6 结束，但我们从未定义过列线5或6。因为我们引用了不存在的线，所以会创建宽度为**0**的隐式轨道来填充这些空白。我们可以使用 grid-auto-columns 和 grid-auto-rows 来指定这些隐式轨道的宽度：  
  
```css
.container {
  grid-auto-columns: 60px;
}
```    

![]({{site.baseurl}}/img/grid-auto-columns-rows-03.svg)  
  
#### grid-auto-flow  
  

如果您有未在网格上明确放置的网格项，自动放置算法会自动放置这些项。这个属性控制自动放置算法的工作方式。

值：

* `row` - 告诉自动放置算法按顺序填充每一行，根据需要添加新行（默认值）
* `column` - 告诉自动放置算法按顺序填充每一列，根据需要添加新列 
* `dense` - 告诉自动放置算法如果较小的项稍后出现，尝试尽早填充网格中的空隙  
  
```css
.container {
  grid-auto-flow: row | column | row dense | column dense;
}
```  
 
注意，dense 只会改变项目的可视顺序，可能导致它们以错误的顺序呈现，这对可访问性不利。

示例：

考虑以下HTML代码：  

```html
<section class="container">
  <div class="item-a">item-a</div>
  <div class="item-b">item-b</div>
  <div class="item-c">item-c</div>
  <div class="item-d">item-d</div>
  <div class="item-e">item-e</div>
</section>
```   

您使用五列两行定义了一个网格，并将 grid-auto-flow 设置为 row（这也是默认值）：  

```css
.container {
  display: grid;
  grid-template-columns: 60px 60px 60px 60px 60px;
  grid-template-rows: 30px 30px;
  grid-auto-flow: row;
}
```   
在放置项目时，您只为其中两个指定了位置：  

```css
.item-a {
  grid-column: 1;
  grid-row: 1 / 3;
}
.item-e {
  grid-column: 5;
  grid-row: 1 / 3;
}
```    
  
由于我们将 grid-auto-flow 设置为 row，我们的网格将如下所示。请注意，我们没有放置的三个项目（item-b、item-c 和 item-d）会在可用行之间流动：  
  
![]({{site.baseurl}}/img/grid-auto-flow-01.svg)  

如果我们将 grid-auto-flow 设置为 column，那么 item-b、item-c 和 item-d 将会在列之间向下流动：  
  
```css
.container {
  display: grid;
  grid-template-columns: 60px 60px 60px 60px 60px;
  grid-template-rows: 30px 30px;
  grid-auto-flow: column;
}
```
![]({{site.baseurl}}/img/grid-auto-flow-02.svg)  
####  grid  
  

一条声明中设置所有以下属性的简写形式：grid-template-rows、grid-template-columns、grid-template-areas、grid-auto-rows、grid-auto-columns 和 grid-auto-flow（注意：只能在单个网格声明中指定显式或隐式网格属性）。

值：

* `none` - 将所有子属性设置为初始值。
* `<grid-template>` - 与 grid-template 简写形式相同。
* `<grid-template-rows> / [ auto-flow && dense? ] <grid-auto-columns>?` - 将 grid-template-rows 设置为指定的值。如果 auto-flow 关键字位于斜杠右侧，则将 grid-auto-flow 设置为 column。如果额外指定了 dense 关键字，则自动放置算法使用`“dense”`装箱算法。如果省略了 grid-auto-columns ，则设置为 auto。 
* `[ auto-flow && dense? ] <grid-auto-rows>? / <grid-template-columns>` - 将 grid-template-columns 设置为指定的值。如果 auto-flow 关键字位于斜杠左侧，则将 grid-auto-flow 设置为 row。如果额外指定了 dense 关键字，则自动放置算法使用`“dense”`装箱算法。如果省略了 grid-auto-rows，则设置为 auto。     

示例：  
  

以下两个代码块是等价的：  
  
```css
.container {
  grid: 100px 300px / 3fr 1fr;
}

.container {
  grid-template-rows: 100px 300px;
  grid-template-columns: 3fr 1fr;
}
```  
  
同样，以下两个代码块是等价的：  

```css
.container {
  grid: auto-flow / 200px 1fr;
}

.container {
  grid-auto-flow: row;
  grid-template-columns: 200px 1fr;
}
```
以及  
```css
.container {
  grid: auto-flow dense 100px / 1fr 2fr;
}

.container {
  grid-auto-flow: row dense;
  grid-auto-rows: 100px;
  grid-template-columns: 1fr 2fr;
}
```  
以下两个代码块是等价的：    

```css
.container {
  grid: 100px 300px / auto-flow 200px;
}

.container {
  grid-template-rows: 100px 300px;
  grid-auto-flow: column;
  grid-auto-columns: 200px;
}

```    

它还接受一种更复杂但非常方便的语法，可以同时设置所有内容。您可以指定 grid-template-areas、grid-template-rows 和 grid-template-columns，其他所有子属性都将设置为它们的初始值。您所做的是在其相应的网格区域中内联指定线名称和跟踪大小。以下是一个示例，最容易描述这个概念：  

```css
.container {
  grid: [row1-start] "header header header" 1fr [row1-end]
        [row2-start] "footer footer footer" 25px [row2-end]
        / auto 50px auto;
}
```    
等价于：    

```css
.container {
  grid-template-areas: 
    "header header header"
    "footer footer footer";
  grid-template-rows: [row1-start] 1fr [row1-end row2-start] 25px [row2-end];
  grid-template-columns: auto 50px auto;    
}
```

### 子元素的属性 （网格项）  

#### grid-column-start ｜ grid-column-end ｜ grid-row-start ｜ grid-row-end   

通过参考特定的网格线来确定网格项在网格中的位置。grid-column-start/grid-row-start 是网格项开始的线，而grid-column-end/grid-row-end 是网格项结束的线。

取值：

* `<line>` - 可以是一个数字，用于引用编号的网格线，或者是一个名称，用于引用命名的网线。  
* `span <number>` - 网格项将跨越所提供的网格轨道数。
* `span <name>` - 网格项将跨越直到达到下一个具有指定名称的线。
* `auto` - 表示自动布局、自动跨度或默认跨度为1的网格项。   
  
```css
.item {
  grid-column-start: <number> | <name> | span <number> | span <name> | auto;
  grid-column-end: <number> | <name> | span <number> | span <name> | auto;
  grid-row-start: <number> | <name> | span <number> | span <name> | auto;
  grid-row-end: <number> | <name> | span <number> | span <name> | auto;
}
```  
  
示例：  
  
```css
.item-a {
  grid-column-start: 2;
  grid-column-end: five;
  grid-row-start: row1-start;
  grid-row-end: 3;
}
```    
![]({{site.baseurl}}/img/grid-column-row-start-end-01.svg)    

```css
    .item-b {
    grid-column-start: 1;
    grid-column-end: span col4-start;
    grid-row-start: 2;
    grid-row-end: span 2;
    }
```    
![]({{site.baseurl}}/img/grid-column-row-start-end-02.svg)    
 
如果没有声明 grid-column-end/grid-row-end，网格项将默认跨越1个轨道。

网格项可以相互重叠。您可以使用 z-index 来控制它们的堆叠顺序。  

#### grid-column | grid-row   
  

分别为 grid-column-start + grid-column-end 和 grid-row-start + grid-row-end 的简写形式。

取值：

* `<start-line> / <end-line>` – 每个都接受与长手形式相同的所有值，包括 span。  
  
```css
.item {
  grid-column: <start-line> / <end-line> | <start-line> / span <value>;
  grid-row: <start-line> / <end-line> | <start-line> / span <value>;
}
```  

示例：  

```css
.item-c {
grid-column: 3 / span 2;
grid-row: third-line / 4;
}
```  
![]({{site.baseurl}}/img/grid-column-row.svg)     

如果没有声明结束行的值，网格项默认将跨越 1 个轨道。  
  
#### grid-area  
  
给一个项目命名，以便可以通过使用 grid-template-areas 属性创建的模板进行引用。或者，该属性可以用作 grid-row-start + grid-column-start + grid-row-end + grid-column-end 的更短的简写形式。

取值：

* `<name>` – 任意选择的名称 
* `<row-start> / <column-start> / <row-end> / <column-end>` – 可以是数字或命名的线  
  
```css
.item {
  grid-area: <name> | <row-start> / <column-start> / <row-end> / <column-end>;
}  
```  

示例：

作为给项目分配名称的方法：  
  
```css
.item-d {
  grid-area: header;
}
```  
作为 grid-row-start + grid-column-start + grid-row-end + grid-column-end 的简写形式：  

```css
.item-d {
  grid-area: 1 / col4-start / last-line / 6;
}
```    
![]({{site.baseurl}}/img/grid-area.svg)     

#### justify-self  
  

作为对齐格子项在单元格内沿行轴（与沿列轴对齐的 align-self 相反）的简写形式。此值适用于单个单元格内的格子项。

取值：

* `start` – 将格子项与单元格的起始边齐平对齐 
* `end` – 将格子项与单元格的末尾边齐平对齐 
* `center` – 将格子项居中对齐于单元格 
* `stretch` – 填充整个单元格的宽度（默认值）  
  
```css
.item {
  justify-self: start | end | center | stretch;
}
```  
  
示例：  

```css
.item-a {
  justify-self: start;
}
```
![]({{site.baseurl}}/img/justify-self-start.svg)   
```css
.item-a {
  justify-self: end;
}
```  
![]({{site.baseurl}}/img/justify-self-end.svg)   

```css
.item-a {
  justify-self: center;
}
```  
![]({{site.baseurl}}/img/justify-self-center.svg)   

```css
.item-a {
  justify-self: stretch;
}
```  
![]({{site.baseurl}}/img/justify-self-stretch.svg)    

要为网格中的所有项设置对齐方式，也可以通过 justify-items 属性在网格容器上设置此行为。  
  
#### align-self  
  
此属性用于沿列轴（与沿行轴对齐的 justify-self 相反）将网格项对齐到单元格内。此值适用于单个网格项内的内容。

取值：

* `start` – 将网格项与单元格的起始边齐平对齐 
* `end`– 将网格项与单元格的末尾边齐平对齐 
* `center` – 将网格项居中对齐于单元格 
* `stretch` – 填充整个单元格的高度（默认值）  
  
```css
.item {
  align-self: start | end | center | stretch;
}
```  
示例：  

  
```css
.item-a {
  align-self: start;
}
```  
![]({{site.baseurl}}/img/align-self-start.svg)     

```css
.item-a {
  align-self: end;
}
```  
![]({{site.baseurl}}/img/align-self-end.svg)    

```css
.item-a {
  align-self: center;
}
```  
![]({{site.baseurl}}/img/align-self-center.svg)   

```css
.item-a {
  align-self: stretch;
}
``` 
![]({{site.baseurl}}/img/align-self-stretch.svg)   

要对齐网格中的所有项，也可以通过 align-items 属性在网格容器上设置此行为。

#### place-self  

  
place-self 在单个声明中同时设置了 align-self 和 justify-self 属性。

取值:

* `auto` – 布局模式的“默认”对齐方式。
* `<align-self> / <justify-self>` – 第一个值设置 align-self，第二个值设置 justify-self。如果省略第二个值，则将第一个值分配给两个属性。    

示例：     

```css
.item-a {
  place-self: center;
}
```    
![]({{site.baseurl}}/img/place-self-center.svg)  

```css
.item-a {
  place-self: center stretch;
}
```  
![]({{site.baseurl}}/img/place-self-center-stretch.svg)    

除了 Edge 浏览器之外，所有主要浏览器都支持 place-self 的简写属性。  
 
# 特殊单位和功能    
  
## fr 单位（fr units）
  

在 CSS Grid 中，您可能会经常使用很多分数单位，比如 1fr。它们基本上表示“剩余空间的一部分”。因此，像下面这样的声明：  
  
```css
grid-template-columns: 1fr 3fr;
```  
大致意思是 25% 和 75%。除了分数单位更具弹性以外，这些百分比值比分数单位更具确定性。例如，如果您为这些基于百分比的列添加了填充，那么现在您已经破坏了 100% 的宽度（假设使用 content-box 的盒模型）。与其他单位相比，分数单位在与其他单位结合使用时也更加友好，您可以想象一下：  
  
```css
grid-template-columns: 50px min-content 1fr;
```  
  
## 尺寸关键字（Sizing Keywords）  
  

在调整行和列的大小时，你可以使用你习惯的所有长度单位，如 px、rem、% 等，但你也可以使用关键字：

* `min-content`：内容的最小尺寸。想象一下一行文字，比如“E pluribus unum”，min-content 可能是单词`“pluribus”`的宽度。 
* `max-content`：内容的最大尺寸。像上面的句子，max-content 是整个句子的长度。
* `auto`：这个关键字很像 fr 单位，除了在分配剩余空间时，它们在尺寸上“输给”了 fr 单位。 
* `分数单位`：参见上文。  
  
## 尺寸函数（Sizing Functions）  
  
* `fit-content()`函数利用可用空间，但永远不会小于 min-content，也永远不会大于 max-content。它能够根据可用空间自动调整尺寸，以适应内容的大小。  

* `minmax()`函数的作用正如其名：它设置了长度能够达到的最小值和最大值。这个函数非常适合与相对单位结合使用。例如，您可能希望某一列只能收缩到一定程度。minmax() 函数能够为您提供这种能力，非常实用且符合您的需求。    

```css
grid-template-columns: minmax(100px, 1fr) 3fr;  

```  
* `min()` 函数.
* `max()` 函数.   
  
## repeat() 函数及关键字  
  
使用repeat()函数可以节省一些打字。  
  
```css
grid-template-columns:
  1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;

/* easier: */
grid-template-columns:
  repeat(8, 1fr);

/* especially when: */
grid-template-columns:
  repeat(8, minmax(10px, 1fr));
```  
  

然而，当与关键字结合使用时，repeat() 函数可以变得更加精彩：

* `auto-fill`：在一行中尽可能容纳尽可能多的列，即使它们是空的。
* `auto-fit`：将所有列适应到空间中。优先扩展列以填充空间，而不是空列。 这是 CSS Grid 中最著名的片段之一，也是有史以来最棒的 CSS 技巧之一。  
  
```css
grid-template-columns: 
  repeat(auto-fit, minmax(250px, 1fr));
```  
  

[这里](https://css-tricks.com/auto-sizing-columns-css-grid-auto-fill-vs-auto-fit/)详细解释了关键字之间的区别。  
  
## 瀑布流式布局（Masonry） 
  

CSS 网格的一项实验性功能是瀑布流布局。请注意，有许多实现 CSS 瀑布流的方法，但大多数都是巧妙的技巧，要么有很大的局限性，要么不完全符合您的期望。

规范现在有一种官方的方法，而这个方法在 Firefox 中是通过一个标志来启用的：  
  
```css
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: masonry;
}
```  
 

请参阅[Rachel的文章](https://www.smashingmagazine.com/native-css-masonry-layout-css-grid/)进行深入了解。  
  

## 子网格（Subgrid）  
  

子网格是网格的一个非常有用的功能，它允许网格项拥有自己的网格，并从父网格继承网格线。  
  
```css
.parent-grid {
  display: grid;
  grid-template-columns: repeat(9, 1fr);
}
.grid-item {
  grid-column: 2 / 7;

  display: grid;
  grid-template-columns: subgrid;
}
.child-of-grid-item {
  /* gets to participate on parent grid! */
  grid-column: 3 / 6;
}
```

目前只有 Firefox 支持此功能，但它真的需要在所有地方得到支持。

另外，了解 `display: contents` ;也是很有用的。虽然不同于子网格，但在某些情况下，它可以以类似的方式发挥作用。  
  
```html
<div class="grid-parent">

  <div class="grid-item"></div>
  <div class="grid-item"></div>

  <ul style="display: contents;">
    <!-- These grid-items get to participate on 
         the same grid!-->
    <li class="grid-item"></li>
    <li class="grid-item"></li>
  </ul>

</div>
```
  
# 流式宽度列的代码片段    
  

没有使用媒体查询的情况下，根据可用空间自动调整为更多或更少的列的流式宽度列。  
  
```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  /* This is better for small screens, once min() is better supported */
  /* grid-template-columns: repeat(auto-fill, minmax(min(200px, 100%), 1fr)); */
  gap: 1rem;
}
```  
  
<p class="codepen" data-height="300" data-theme-id="dark" data-default-tab="html,result" data-slug-hash="BavNEgy" data-user="Mariano_M" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>  