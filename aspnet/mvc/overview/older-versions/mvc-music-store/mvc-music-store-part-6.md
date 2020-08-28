---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: 第6部分：使用資料批註進行模型驗證 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第6部分說明如何使用模型 V 的資料批註 .。。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: 24d3f028a9a720e5b526518624c9c1c2ce2c37d4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044944"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a>第 6 部分：使用資料註解進行模型驗證

依 [Jon Galloway](https://github.com/jongalloway)

> MVC 音樂存放區是一個教學課程應用程式，介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 網頁程式開發。  
>   
> MVC 音樂商店是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。  
>   
> 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第6部分說明如何使用資料批註進行模型驗證。

我們的建立和編輯表單有一個重大問題：它們沒有進行任何驗證。 我們可以做一些事，像是將必要欄位留白或在 Price 欄位中輸入字母，而我們看到的第一個錯誤是從資料庫。

我們可以藉由將資料批註加入至模型類別，輕鬆地將驗證新增至我們的應用程式。 資料批註可讓我們描述要套用至模型屬性的規則，而 ASP.NET MVC 會負責強制執行這些規則，並向使用者顯示適當的訊息。

## <a name="adding-validation-to-our-album-forms"></a>將驗證新增至我們的專輯表單

我們將使用下列資料批註屬性：

- **必要** -表示屬性是必要欄位
- **DisplayName** –定義要用於表單欄位和驗證訊息的文字
- **StringLength** –定義字串欄位的最大長度
- **範圍** –提供數值欄位的最大值和最小值
- 系**結–將**參數或格式值系結至模型屬性時要排除或包含的欄位
- **ScaffoldColumn** –允許隱藏來自編輯器表單的欄位

*注意：如需有關使用資料批註屬性進行模型驗證的詳細資訊，請參閱 MSDN 檔，網址為：*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)

開啟專輯類別，並將下列 *using* 語句新增至頂端。

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

接下來，更新屬性以新增顯示和驗證屬性，如下所示。

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

在這裡，我們也將內容類型和演出者變更為虛擬屬性。 這可讓 Entity Framework 視需要延遲載入它們。

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

將這些屬性新增至我們的專輯模型之後，我們的 [建立] 和 [編輯] 畫面會立即開始驗證欄位，並使用我們所選擇的顯示名稱 (例如專輯封面 Url，而不是 AlbumArtUrl) 。 執行應用程式並流覽至/StoreManager/Create。

![](mvc-music-store-part-6/_static/image1.png)

接下來，我們會中斷某些驗證規則。 輸入0的價格，並將標題保留空白。 當我們按一下 [建立] 按鈕時，我們會看到顯示驗證錯誤訊息的表單，顯示哪些欄位不符合我們所定義的驗證規則。

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a>測試用戶端驗證

從應用程式的觀點來看，伺服器端驗證非常重要，因為使用者可以規避用戶端驗證。 不過，只有執行伺服器端驗證的網頁表單會出現三個重大問題。

1. 使用者必須等待表單張貼、在伺服器上驗證，以及將回應傳送到其瀏覽器。
2. 當使用者更正欄位，使其現在通過驗證規則時，不會立即收到意見反應。
3. 我們會浪費伺服器資源來執行驗證邏輯，而不是利用使用者的瀏覽器。

幸運的是，ASP.NET MVC 3 scaffold 範本內建用戶端驗證，不需要任何額外的工作。

在 [標題] 欄位中輸入單一字母可滿足驗證需求，因此會立即移除驗證訊息。

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> [上一個](mvc-music-store-part-5.md) 
> [下一步](mvc-music-store-part-7.md)
