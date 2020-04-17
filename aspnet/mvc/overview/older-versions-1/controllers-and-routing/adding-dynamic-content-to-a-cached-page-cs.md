---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: 將動態內容新增到快取頁面 (C#) |微軟文件
author: rick-anderson
description: 瞭解如何在同一頁中混合動態和緩存的內容。 快取後取代讓您能夠顯示動態內容,如橫幅播發。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c8cd70a15c1ae93f7cf9b0a026b37b07e489040
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542283"
---
# <a name="adding-dynamic-content-to-a-cached-page-c"></a>將動態內容新增至快取的頁面 (C#)

由[微軟](https://github.com/microsoft)

> 瞭解如何在同一頁中混合動態和緩存的內容。 快取後取代讓您能夠在已快取的頁面中顯示動態內容,如橫幅播發或新聞專案。

通過利用輸出緩存,您可以顯著提高ASP.NET MVC 應用程式的性能。 在每次請求頁面時,該頁可以生成一次,並緩存在多個使用者的記憶體中,而不是每次請求頁面時重新生成頁面。

但有一個問題。 如果您需要在頁面中顯示動態內容,該怎麼辦? 例如,假設您要在頁面中顯示橫幅廣告。 您不希望緩存橫幅播發,以便每個使用者看到相同的播發。 你不會這樣賺錢的!

幸運的是,有一個簡單的解決方案。 您可以利用稱為*快取後取代*ASP.NET 架構的功能。 快取後取代讓您能夠取代已快存在記憶體中的頁面中的動態內容。

通常,當您使用 [OutputCache] 屬性輸出快取頁面時,該頁將緩存在伺服器和用戶端(Web 瀏覽器)上。 使用緩存後替換時,頁面僅緩存在伺服器上。

#### <a name="using-post-cache-substitution"></a>使用快取後取代

使用緩存後替換需要兩個步驟。 首先,您需要定義一個方法,該方法返回表示要在緩存頁中顯示的動態內容的字串。 接下來,調用 HttpResponse.Write 替代() 方法將動態內容注入頁面。

例如,假設您要在快取的頁面中隨機顯示不同的新聞專案。 清單 1 中的類公開一個名為 RenderNews()的方法,該方法從三個新聞項清單中隨機返回一個新聞項。

**清單1 = 模型\新聞.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

要利用緩存後替換,請致電 HttpResponse.Write 替代()方法。 Write替代()方法設置代碼,以動態內容替換緩存頁的區域。 Write替代()方法用於在清單2的視圖中顯示隨機新聞項。

**清單 2 = 檢視\home_Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

渲染新聞方法傳遞給寫入替換() 方法。 請注意,不調用 RenderNews 方法(沒有括弧)。 相反,對該方法的引用將傳遞給 Write 替代。)

已緩存索引視圖。 視圖由清單 3 中的控制器返回。 請注意,Index() 操作用 [OutputCache] 屬性進行修飾,該屬性會導致索引視圖緩存 60 秒。

**清單3 = 控制器\主控制器.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

即使快取了 Index 檢視,當您請求「索引」頁時,也會顯示不同的隨機新聞項。 請求「索引」頁時,頁面顯示的時間在 60 秒內不會更改(參見圖 1)。 時間不變的事實證明頁面被緩存了。 但是,Write替代()方法(隨機新聞項)注入的內容隨每個請求而變化。

**圖 1 = 在快取的頁面中注入動態新聞專案**

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>在說明器方法使用快取時取代

利用緩存後替換的一種更簡單的方法是在自定義説明器方法中封裝對 Write 替代() 方法的調用。 清單4中的説明方法說明了此方法。

**清單4 = AdHelper.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

清單4包含一個靜態類,它公開了兩種方法:渲染Banner()和RenderBanner內部()。 RenderBanner() 方法表示實際幫助器方法。 此方法擴展了標準ASP.NET MVC HtmlHelper 類,以便您可以像任何其他説明器方法一樣在視圖中調用 Html.RenderBanner()。

renderBanner() 方法呼叫將 RenderBanner 內部() 方法傳遞給 Write 取代() 方法的 HttpResponse.Write 替換() 方法。

RenderBanner 內部() 方法是一種私有方法。 此方法不會作為幫助器方法公開。 RenderBanner 內部() 方法從三個橫幅廣告圖像清單中隨機返回一個橫幅廣告圖像。

清單5中修改後的索引檢視說明了如何使用 RenderBanner() 説明器方法。 請注意,在檢視&lt;頂部包含額外的&gt;%@ 匯入 % 指令,用於匯入 MvcApplication1.Helpers 命名空間。 如果忽略導入此命名空間,則 RenderBanner() 方法將不會顯示為 Html 屬性上的方法。

**清單 5 = 檢視\home_Index.aspx(使用 RenderBanner() 方法)**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

請求清單 5 中由檢視呈現的頁面時,每個請求都會顯示不同的橫幅播發(參見圖 2)。 頁面被緩存,但橫幅播發由 RenderBanner() 幫助器方法動態注入。

**圖 2 = 顯示隨機橫幅播發的索引檢視**

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a>總結

本教程介紹了如何動態更新緩存頁中的內容。 您學習了如何使用 HttpResponse.Write 替代() 方法,以便將動態內容注入緩存頁面。 您還學習了如何在 HTML 說明器方法中封裝對 Write 替代() 方法的呼叫。

盡可能利用快取, 會對 Web 應用程式的效能產生顯著影響。 如本教學中所述,即使您需要在頁面中顯示動態內容,您也可以利用緩存。

> [!div class="step-by-step"]
> [前一個](improving-performance-with-output-caching-cs.md)
> [下一個](creating-a-controller-cs.md)
