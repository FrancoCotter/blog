---

layout:  post
title:   "关于 List 与 Marker 之间你需要知道的那些事(翻译)"
subtitle:   ""
date:       "2023-07-20 16:27:00"
author:     "Mariano"
header-img: "img/list-marker-gap.png"
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
     
   但事與願違，這行代碼不起作用，事實上， `::marker` 近支持一下部分主要與文本相關的 `CSS` 屬性。例如，你可以更改 `marker` 的 `font-size` 和 `color`，並通過設置字符串或者 `URL` 來定義自定義的 `marker` 。所以，明白了原理，就支持我上面的設想是奢望了，`marker` 不支持 `margin` 和 `padding` 真的很令人沮喪啊。  
     
   空格真的是在自定義標記後插入間隙的唯一方法了嗎？我需要尋找答案，當我在研究這個主題的時候，我發現了一些有趣的發現，我想在文中把這些發現分享出來。  
     
     
  
  ## 添加 `padding` 和  `margin`  
    
     
   首先，讓我們確認 `<ul><li>` 這兩元素的 margin 和 padding。我為此創建了一個測試頁面，拖動相關的滑塊觀察列表標記兩側的檢舉效果。提示：請隨意使用重置（`reset`）按鈕將所有的空間重置為了其初始值。   
     
   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="NWELyRO" data-user="Mariano_M" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>  
     
     
   正如你所看到的，<li> 的 padding-left 增加了列表之後的間隙。其他三個屬性控制 marker 左側的間距，換句話說，控制列表項的縮進。  
     
   請注意，即使列表項的 padding-left 的值為 0px，標記後面仍然有一個最小的空隙。這個間隙不能通過間隙啊 margin 或者 padding 來縮小，具體的最小間隙取決於每個瀏覽器自己的標準。  

   ![]({{site.baseurl}}/img/margin-padding-position-outside.png)  
   ``` 
    前三個屬性將整個列表（包括 marker）推倒右側。第四個屬性僅將列表項的內容推到右側。
   ```   
   總結來說，清單項目的內容被定位在與瀏覽器特定的標記最小距離上，並且這個間隙可以通過給 <li> 添加 padding-left 進一步增加。
   接下來，讓我們看看當我們將標記放在清單項目內部時會發生什麼情況。  
     
   # 將標記移到清單項目內部  
     
   
list-style-position 屬性接受兩個關鍵字：outside（預設值）和inside，inside 會將標記移動到清單項目內部。後者在創建具有全寬度清單項目的設計時非常有用。  
  
  ![]({{site.baseurl}}/img/list-marker-position-inside.webp)  
    

   如果標記現在在清單項目內部，這是否意味著在 <li> 上的 padding-left 不再增加標記後的間隙？讓我們來看看。在我的測試頁面上，通過勾選框啟用 list-style-position: inside。這個變化會如何影響四個 padding 和 margin 屬性？

正如您所看到的，<li> 上的 padding-left 現在會增加標記左側的間距。這意味著我們失去了在標記後增加間隙的能力。在這種情況下，如果能夠為 ::marker 本身添加 margin-right 就很有用，但如上所述，這是不起作用的。 

       
    ![]({{site.baseurl}}/img/margin-padding-position-inside.png)    
      
   
此外，Chromium 中存在一個錯誤，導致在切換到內部定位後，標記後的間隙會增加三倍。預設情況下，間隙的長度約為文本大小的三分之一。因此，在預設的字體大小為 16px 的情況下，間隙約為 5.5px。在 Chrome 中，切換到內部定位後，間隙會增長到完整的 16px。這個錯誤影響到了圓點、圓圈和方塊標記，但不影響順序數字標記。

下圖展示了在 macOS 上三個主要瀏覽器中，外部和內部定位的清單標記的默認渲染方式。為了方便比較間隙大小的差異，我將所有清單項目的標記水平對齊。  
  
   ![]({{site.baseurl}}/img/outside-inside-gap-difference.png)  
     
   
 總結來說，切換到 list-style-position: inside 會引入兩個問題。我們無法再通過在 <li> 上使用 padding-left 增加間隙，而且間隙大小在不同瀏覽器之間不一致。

最後，讓我們看看當我們將默認清單標記替換為自定義標記時會發生什麼情況。      

   
     
切換到自定義標記有兩種方法：

使用 list-style-type 和 list-style-image 屬性
使用 ::marker 伪元素上的 content 屬性
content 屬性更強大。例如，它允許我們使用 counter() 函數來訪問清單項目的順序號（隱式清單項目計數器），並用自定義字符串進行修飾。
  

不幸的是，Safari 目前尚不支持 ::marker 上的 content 屬性（WebKit bug）。因此，我將使用 list-style-type 屬性來定義自定義標記。您仍然可以使用 ::marker 選擇器來為通過 list-style-type 声明的自定義標記設定樣式。這方面的 ::marker 在 Safari 中是支持的。  

  
任何 Unicode 字符都有潛在的可能用作自定義清單標記，但實際上只有一小部分字符的官方名稱中實際上包含“Bullet”一詞，因此我想在這裡為參考編譯它們。  
       
      
｜ Character ｜Name   ｜ Code ｜ point｜ CSS keyword｜
｜-----------｜ ------｜------｜------｜------------｜
｜•          ｜Bullet ｜U+2022｜      ｜        disc｜
｜‣          ｜Triangular Bullet｜U+2023｜｜        ｜
｜⁃          ｜Hyphen Bullet｜U+2043 ｜｜           ｜
｜⁌          ｜Black Leftwards Bullet｜U+204C｜｜   ｜	
｜⁍          ｜Black Rightwards Bullet｜U+204D｜｜	 ｜
｜◘          ｜Inverse Bullet｜U+25D8｜｜           ｜
｜◦          ｜White Bullet｜U+25E6｜  ｜     circle｜
｜☙          ｜Reversed Rotated Floral 
                          Heart Bullet｜U+2619｜｜   ｜
｜❥          ｜Rotated Heavy Black Heart
                                Bullet｜U+2765｜｜   ｜
｜❧          ｜Rotated Floral Heart Bullet｜U+2767｜｜｜
｜⦾          ｜Circled White Bullet｜U+29BE｜｜      ｜	
｜⦿          ｜Circled Bullet｜U+29BF｜｜           ｜
  
    
現在讓我們看看將默認的清單標記替換為 list-style-type: "•"（U+2022 Bullet）時會發生什麼情況。這個字符與默認的圓點字符相同，所以不應該有任何主要的渲染差異。在我的測試頁面上，啟用 list-style-type 選項並觀察標記的任何變化。

正如您所看到的，有兩個重要的變化：

標記後不再有最小間隙。
圓點變得更小，好像以較小的字體大小呈現。
根據 CSS Counter Styles Level 3，默認的清單標記（圓點）應該是“類似於 • U+2022 BULLET”。看起來瀏覽器會增加默認圓點的大小，以使其更易讀。Firefox甚至使用了一個特殊的字體 -moz-bullet-font 來呈現標記。  

  
小尺寸問題可以使用CSS修復嗎？在我的測試頁面上，打開標記樣式並觀察當您更改標記的字體大小、行高和字體時會發生什麼。

正如您所見，增加字體大小會導致自定義標記垂直不對齊，而減小行高無法修正此問題。垂直對齊屬性（vertical-align），可以輕鬆解決此問題，但在::marker上不受支持。

但您是否注意到更改字體家族可能會使標記變大？嘗試將其設置為Tahoma。這可能是解決小尺寸問題的一個足夠好的解決方法，儘管我尚未測試哪種字體在主要瀏覽器和操作系統上效果最佳。

您可能還注意到，當您將標記置於列表項目內部時，Chromium的錯誤不再發生。這意味著自定義標記可以作為此錯誤的解決方法。這也帶我們來到主要問題，以及我開始研究這個主題的原因。如果您定義了自定義標記並將其放置在列表項目內部，則標記後面沒有間隙，也沒有通過標准方式插入間隙的方法。

自定義標記後沒有最小間隙。
::marker不支持填充或邊距。
<li>上的padding-left不會增加間隙，因為標記被放置在內部。
總結
以下是我在文章中提到的所有關鍵事實的總結：

瀏覽器對<ul>和<ol>元素應用了40像素的默認padding-inline-start。
內置列表標記（圓點、數字等）後有最小間隙。自定義標記（字符串或URL）後沒有最小間隙。
通過對<ul>添加padding-left可以增加間隙的長度，但僅在標記位於列表項目外部（默認模式）時有效。
自定義字符串標記的默認大小比內置標記小。在::marker上更改字體家族可以增加它們的大小。
結論
回顧一下文章開頭的代碼示例，我現在明白為什麼內容值中有一個空格字符了。在SVG標記後插入間隙的更好方法就是這樣。這是一個必需的解決方法，因為無論多少邊距和填充都無法在放置在列表項目內部的自定義標記後插入間隙。在::marker上使用margin-right可以輕鬆實現，但不受支持。

在::marker添加對更多屬性的支持之前，Web開發人員通常無法選擇隱藏標記並使用::before偽元素模擬它。最近我自己就不得不這樣做，因為我無法更改標記的背景顏色。希望不用等待太久，就能有一個更強大的::marker偽元素。