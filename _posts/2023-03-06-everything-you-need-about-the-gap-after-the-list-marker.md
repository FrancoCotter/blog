---

layout:  post
title:   "关于 List 与 Marker 之间你需要知道的那些事(翻译)"
subtitle:   ""
date:       "2023-03-06 17:24:00"
author:     "Mariano"
header-img: "img/promise.jpg"
tags:  

   - 翻译
   - List 列表
   - Marker
   - CSS
 
---
  
  
   當我在 Google's web.dev 博客上讀到這篇文章 [“Creative List Styling”](https://web.dev/creative-list-styling/) 並注意他們給出的案例代碼中的這個 `::marker` 讓人感覺很奇怪。因為在整個 list 的內置 marker 都是豆點，或者是升序排列的數字抑或字母。但案例中的 `::marker` 偽類卻允許可以自定義它的整個樣式，無論是用自定義字符或者圖片皆可。

   ```css  
      
      ::marker {
         content: url('/marker.svg') '';
      }
         

   ```  
     
   這個例子讓我注意到使用矢量的 SVG 圖形也可以用作自定義 marker，但這一行 css 中，content 的值，中間有一個單獨的空格 `(" ")` 跟在 url 的後面。這個空格的目的就好像是要在自定義的 marker 后插入一個間隙。    
     
   ![]({{site.baseurl}}/img/svg-marker-and-space.png)   
     
     
   當我看到這段代碼時，我立即想知道是否有更好的方法來創造這個間隙呢？因為在 content 的值里附加一個空格 `（" "）` 更像是一種臨時的解決策略而非最佳的解決方案。`CSS` 提供了 `margin` 和 `padding` 的標準方法來分割頁面上的元素，在這種情況下我能使用這些屬性嗎？

   首先，我要嘗試用適當的邊距來替換空格。  
     
   ```css  
     
       
   ::marker{
      content:url('/marker.svg');
      margin-right:1ch;

   }
   
   ```  
     
   但事與願違，這行代碼不起作用，事實上， `::marker` 近支持一下部分主要與文本相關的 `CSS` 屬性。例如，你可以更改 `marker` 的 `font-size` 和 `color`，並通過設置字符串或者 `URL` 來定義自定義的 `marker` 。所以，明白了原理，就支持我上面的設想是奢望了，`marker` 不支持 `margin` 和 `padding` 真的很令人沮喪啊