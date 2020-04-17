---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: 將資料傳遞到查看母版頁 (VB) |微軟文件
author: rick-anderson
description: 本教學的目的是解釋如何將數據從控制器傳遞到視圖母版頁。 我們檢查將資料傳遞到檢視的兩種策略...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: ef65541a5f2297414f923e2f8108a14de67531e5
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542465"
---
# <a name="passing-data-to-view-master-pages-vb"></a>將資料傳遞至檢視主版頁面 (VB)

由[微軟](https://github.com/microsoft)

[下載 PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> 本教學的目的是解釋如何將數據從控制器傳遞到視圖母版頁。 我們檢查將數據傳遞到檢視母版頁的兩種策略。 首先,我們討論一個簡單的解決方案,該解決方案會導致應用程式難以維護。 接下來,我們將研究一個更好的解決方案,它需要更多的初始工作,但會產生一個更可維護的應用程式。

## <a name="passing-data-to-view-master-pages"></a>將資料傳遞到檢視母版頁

本教學的目的是解釋如何將數據從控制器傳遞到視圖母版頁。 我們檢查將數據傳遞到檢視母版頁的兩種策略。 首先,我們討論一個簡單的解決方案,該解決方案會導致應用程式難以維護。 接下來,我們將研究一個更好的解決方案,它需要更多的初始工作,但會產生一個更可維護的應用程式。

### <a name="the-problem"></a>問題

假設您正在建構影片資料庫應用程式,並且您想要在應用程式的每一頁上顯示影片類別清單(參見圖 1)。 此外,假設影片類別清單存儲在資料庫表中。 在這種情況下,從資料庫中檢索類別並在視圖母版頁中呈現影片類別清單是有意義的。

[![在檢視母版頁中顯示影片類別](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)

**圖 01**: 在檢視母版頁中顯示影片類別 ([按下以檢視全尺寸影像](passing-data-to-view-master-pages-vb/_static/image3.png))

這就是問題所在。 如何檢索母版頁中的電影類別清單? 在母版頁中直接調用模型類的方法是很有誘惑力的。 換句話說,最好在母版頁中包含從資料庫檢索數據的代碼。 但是,繞過 MVC 控制器訪問資料庫將違反完全分離問題是構建 MVC 應用程式的主要好處之一。

在 MVC 應用程式中,您希望 MVC 視圖和 MVC 模型之間的所有互動都由 MVC 控制器處理。 這種關注點的分離產生了更可維護、適應性強和可測試的應用。

在 MVC 應用程式中,傳遞給檢視的所有數據(包括檢視母版頁)都應通過控制器操作傳遞到檢視。 此外,數據應利用視圖數據傳遞。 在本教程的其餘部分中,我將檢查將視圖數據傳遞到視圖母版頁的兩種方法。

### <a name="the-simple-solution"></a>簡單解決方案

讓我們從將檢視數據從控制器傳遞到視圖母版頁的最簡單的解決方案開始。 最簡單的解決方案是在每個控制器操作中傳遞母版頁的檢視數據。

考慮清單 1 中的控制器。 它公開名為`Index()`和`Details()`的兩個操作。 操作`Index()`方法返回「影片」資料庫表中的每個影片。 操作`Details()`方法返回特定影片類別中的每部電影。

**清單1 |`Controllers\HomeController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

請注意,和`Index()``Details()`操作都添加兩個項以查看數據。 該`Index()`操作添加了兩個鍵:類別和影片。 類別鍵表示檢視母版頁顯示的電影類別清單。 影片鍵表示「索引」檢視頁顯示的影片清單。

該`Details()`操作還添加了兩個名為類別和影片的鍵。 類別鍵再次表示檢視母版頁顯示的電影類別清單。 影片鍵表示「詳細資訊」檢視頁顯示的特定類別中的電影清單(參見圖 2)。

[!["詳細資訊"檢視](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)

**圖 02**: 「詳細資訊」檢視 ([按下以檢視全尺寸影像](passing-data-to-view-master-pages-vb/_static/image6.png))

索引檢視包含在清單 2 中。 它只是遍達視圖數據中由影片項表示的電影清單。

**清單2 |`Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

視圖母版頁包含在清單 3 中。 視圖母版頁從檢視數據中參數地表示並呈現類別項表示的所有影片類別。

**清單3 |`Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

所有數據都通過檢視數據傳遞到視圖和視圖母版頁。 這是將數據傳遞到母版頁的正確方法。

那麼,這個解決方案有什麼問題呢? 問題是,此解決方案違反了DRY(不要重複自己)原則。 每個控制器操作都必須添加完全相同的影片類別清單才能查看數據。 應用程式中具有重複的代碼會使應用程式更難維護、調整和修改。

### <a name="the-good-solution"></a>良好的解決方案

在本節中,我們將檢查將數據從控制器操作傳遞到視圖母版頁的替代方法和更好的解決方案。 我們不是在每個控制器操作中添加母版頁的影片類別,而是僅將影片類別添加到視圖數據一次。 檢視母版頁使用的所有檢視數據都添加到應用程式控制器中。

應用程式控制器類包含在清單 4 中。

應用程式控制器類包含在清單 4 中。

**清單4 |`Controllers\ApplicationController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

關於清單4中的應用程式控制器,您應該注意三件事。 首先,請注意,類從基 System.Web.Mvc.Controller 類繼承。 應用程式控制器是控制器類。

其次,請注意應用程式控制器類是必繼承類。 MustInherit 類是一個必須由具體類實現的類。 由於應用程式控制器是 MustInherit 類,因此不能直接調用類中定義的任何方法。 如果嘗試直接調用應用程式類,則會收到"找不到資源"錯誤消息。

第三,請注意,應用程式控制器包含一個構造函數,該構造函數添加要查看數據的影片類別清單。 從應用程式控制器繼承的每個控制器類都會自動調用應用程式控制器的建構函數。 每當對從應用程式控制器繼承的任何控制器調用任何操作時,影片類別將自動包含在視圖數據中。

清單 5 中的影片控制器從應用程式控制器繼承。

**清單5 |`Controllers\MoviesController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

與上一節中討論的「家庭控制器」一樣,電影控制器公開了名為`Index()`和`Details()`的兩種操作方法。 請注意,檢視母版頁顯示的影片類別清單不會添加以查看 或`Index()``Details()`方法中的數據。 由於「影片」控制器從應用程式控制器繼承,因此將添加影片類別清單以自動查看數據。

請注意,此為視圖母版頁添加視圖數據的解決方案並不違反 DRY(不要重複自己)原則。 添加要查看數據的影片類別清單的代碼僅包含在一個位置:應用程式控制器的構造函數。

### <a name="summary"></a>總結

在本教程中,我們討論了將視圖數據從控制器傳遞到視圖母版頁的兩種方法。 首先,我們研究了一種簡單但難以維持的方法。 在第一部分中,我們討論了如何在應用程式中的每個控制器操作中為視圖母版頁添加視圖數據。 我們的結論是,這是一個糟糕的方法,因為它違反了DRY(不要重複自己)的原則。

接下來,我們研究了添加視圖母版頁所需的數據以查看數據更好的策略。 我們不是在每個控制器操作中添加檢視數據,而是在應用程式控制器中只添加一次視圖數據。 這樣,當將數據傳遞到ASP.NET MVC 應用程式中的檢視母版頁時,可以避免重複的代碼。

> [!div class="step-by-step"]
> [上一步](creating-page-layouts-with-view-master-pages-vb.md)
