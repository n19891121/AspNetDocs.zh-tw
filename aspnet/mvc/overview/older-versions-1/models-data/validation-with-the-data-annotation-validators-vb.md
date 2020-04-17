---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: 使用資料註解驗證器 (VB) 進行驗證 :微軟文件
author: rick-anderson
description: 利用數據註釋模型綁定器在 mVC 應用程式中執行驗證ASP.NET。 瞭解如何使用不同類型的驗證器...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: cabdf6dab9e5de53a45adcf126705533fca02de7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542634"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a>驗證與資料註解驗證器 (VB)

由[微軟](https://github.com/microsoft)

> 利用數據註釋模型綁定器在 mVC 應用程式中執行驗證ASP.NET。 瞭解如何使用不同類型的驗證器屬性,並在 Microsoft 實體框架中使用它們。

在本教學中,您將瞭解如何使用數據註釋驗證器在 ASP.NET MVC 應用程式中執行驗證。 使用數據註釋驗證器的優點是,它們僅通過向類屬性添加一個或多個屬性(如"必需"或"字串長度"屬性)即可執行驗證。

在使用數據註釋驗證器之前,必須下載數據註釋模型綁定器。 您可以通過[按一下此處](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)從 CodePlex 網站下載數據註釋模型粘合劑範例。

請務必瞭解,數據註釋模型綁定器不是 Microsoft ASP.NET MVC 框架的正式部分。 儘管數據註釋模型活頁夾是由 Microsoft ASP.NET MVC 團隊創建的,但 Microsoft 不會為本教程中介紹和使用的數據註釋模型粘合劑提供官方產品支援。

## <a name="using-the-data-annotation-model-binder"></a>使用資料註解模型繫結器

為了在ASP.NET MVC 應用程式中使用數據註釋模型綁定器,首先需要添加對 Microsoft.Web.Mvc.Dataannotations.dll 程式集和 System.元件模型.Datathethe.dll 程式集的引用。 選擇選單選項 **「專案」,新增參考**。 接下來,按一下 **「瀏覽」** 選項卡並瀏覽到下載(並解壓縮)數據註釋模型裝訂器範例的位置(參見**圖 1)。**

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

**圖 1**: 新增對資料註解模型載入([按下以檢視全尺寸影像](validation-with-the-data-annotation-validators-vb/_static/image3.png))

同時選擇 Microsoft.Web.Mvc.Data註解.dll 程式集和系統.元件模型.DataAnnotations.dll 程式集,然後單擊 **"確定"** 按鈕。

不能使用系統.元件模型.Data註釋.dll 程式集包含在 .NET 框架服務包 1 與數據註釋模型綁定器。 您必須使用系統版本.元件模型.Data註釋.dll 程式集包含在數據註釋模型裝訂器示例下載中。

最後,您需要在 Global.asax 檔中註冊 DataAnnotations 模型綁定器。 將以下代碼列加入到應用程式\_Start() 事件處理程式,\_以便應用程式 Start() 方法如下所示:

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

此代碼行將 DataAnnotationsModelBinder 註冊為整個ASP.NET MVC 應用程式的預設模型活頁夾。

## <a name="using-the-data-annotation-validator-attributes"></a>使用資料註解驗證器屬性

使用數據註釋模型裝訂器時,可以使用驗證器屬性執行驗證。 系統.元件模型.Data註解命名空間包括以下驗證器屬性:

- 範圍 – 使您能夠驗證屬性的值是否介於指定的值範圍之間。
- 正規表示式 – 使您能夠驗證屬性的值是否與指定的正規表示式模式匹配。
- 必需 = 使您能夠根據需要標記屬性。
- 字串長度 – 使您能夠為字串屬性指定最大長度。
- 驗證 = 所有驗證器屬性的基類。

> [!NOTE] 
> 
> 如果任何標準驗證器未滿足驗證需求,則始終可以選擇通過從基本驗證屬性繼承新的驗證器屬性來創建自定義驗證器屬性。

**清單1**中的「產品」類說明瞭如何使用這些驗證器屬性。 名稱、說明和單價屬性按要求進行標記。 Name 屬性的字串長度必須小於 10 個字元。 最後,UnitPrice 屬性必須匹配表示貨幣金額的正則運算式模式。

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

**清單1**:型號\Product.vb

"產品"類說明瞭如何使用一個附加屬性:顯示名稱屬性。 在錯誤訊息中顯示屬性時,顯示Name 屬性允許您修改屬性的名稱。 您可以顯示錯誤消息"需要價格",而不是顯示錯誤消息"需要價格"

> [!NOTE] 
> 
> 如果要完全自訂驗證器顯示的錯誤訊息,則可以將自訂錯誤訊息分配給驗證器的 ErrorMessage 屬性,如下所示:`<Required(ErrorMessage:="This field needs a value!")>`

您可以將**清單 1**中的「產品」類與 清單**2**中的 Create() 控制器操作一起使用。 當模型狀態包含任何錯誤時,此控制器操作重新顯示"創建"檢視。

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

**清單2**:控制器\產品控制器.vb

最後,您可以通過右鍵單擊 Create() 操作並選擇功能表選項 **「添加檢視**」來在**清單 3**中創建檢視。 創建以 Product 類為模型類的強類型視圖。 從檢視內容下拉清單中**選擇"創建**"(參見**圖 2**)。

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

**圖 2**: 新增建立檢視

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

**清單3**:檢視\產品\創建.aspx

> [!NOTE] 
> 
> 從「**新增檢視」** 選單選項產生的「創建窗體」 中移除「 Id」 欄位。 由於 Id 欄位對應於標識列,因此您不希望允許使用者輸入此欄位的值。

如果提交表單以創建產品,並且未輸入所需欄位的值,則將顯示**圖 3**中的驗證錯誤消息。

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

**圖 3**:缺少必填欄位

如果輸入無效的貨幣金額,則將顯示**圖 4**中的錯誤消息。

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

**圖4**:無效貨幣金額

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>將資料註解驗證器與實體框架一起使用

如果使用 Microsoft 實體框架生成數據模型類,則無法將驗證器屬性直接應用於類。 由於實體框架設計器生成模型類,因此下次在設計器中進行任何更改時,將對模型類所做的任何更改都將被覆蓋。

如果要將驗證器與實體框架生成的類一起使用,則需要創建元數據類。 將驗證器應用於元數據類,而不是將驗證器應用於實際類。

例如,假設您已使用實體框架創建了 Movie 類(參見**圖 5**)。 此外,假設您要使影片標題和導演屬性成為所需的屬性。 在這種情況下,您可以在**清單 4**中創建部分類和元數據類。

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

**圖 5**: 實體框架產生的影片類別

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

**清單4**:模型_Movie.vb

**清單4**中的檔包含名為「電影」和「MovieMetaData」的兩個類。 "影片"類是部分類。 它對應於數據模型.Designer.vb 檔中包含的實體框架生成的部分類。

目前,.NET 框架不支援部分屬性。 因此,無法通過將驗證器屬性應用於**清單 4**中檔中定義的 Movie 類的屬性,從而將驗證器屬性應用於 DataModel.designer.vb 檔中定義的 Movie 類的屬性。

請注意,影片部分類用指向 MovieMetaData 類的元數據類型屬性進行修飾。 MovieMetaData 類包含影片類屬性的代理屬性。

驗證器屬性應用於 MovieMetaData 類的屬性。 標題、控制器和日期釋放屬性都標記為必需屬性。 必須為 Director 屬性分配包含少於 5 個字元的字串。 最後,顯示Name 屬性應用於 Date 下達屬性,以顯示錯誤消息,如"需要發佈日期發佈"欄位。 而不是錯誤"需要日期釋放欄位」。

> [!NOTE] 
> 
> 請注意,MovieMetaData 類中的代理屬性不需要表示與 Movie 類中的相應屬性相同的類型。 例如,Director 屬性是 Movie 類中的字串屬性和 MovieMetaData 類中的物件屬性。

**圖 6**中的頁面演示了在為 Movie 屬性輸入無效值時返回的錯誤消息。

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

**圖 6**: 使用驗證器與實體框架 ([按下以檢視全尺寸影像](validation-with-the-data-annotation-validators-vb/_static/image14.png))

## <a name="summary"></a>總結

在本教學中,您學習了如何使用數據註釋模型綁定器在ASP.NET MVC 應用程式中執行驗證。 您學習了如何使用不同類型的驗證器屬性,如"必需"和"字串長度"屬性。 在使用 Microsoft 實體框架時,您還學習了如何使用這些屬性。

> [!div class="step-by-step"]
> [上一步](validating-with-a-service-layer-vb.md)
