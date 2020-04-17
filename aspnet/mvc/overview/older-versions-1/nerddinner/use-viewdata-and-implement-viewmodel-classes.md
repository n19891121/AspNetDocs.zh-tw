---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 使用檢視數據並實現檢視模型類 |微軟文件
author: rick-anderson
description: 步驟 6 顯示了如何支援更豐富的表單編輯方案,並討論了兩種方法,可用於將數據從控制器傳遞到視圖:...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 7fa2af2a55d12bbe11b29dff594823a1e5ea0152
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541100"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>使用 ViewData 和實作 ViewModel 類別

由[微軟](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第6步,該教學示範如何使用ASP.NET MVC 1 構建小型但完整的 Web 應用程式。
> 
> 步驟 6 顯示了如何支援更豐富的表單編輯方案,並討論了可用於將數據從控制器傳遞到視圖的兩種方法:ViewData 和 ViewModel。
> 
> 如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>神經晚餐步驟 6:查看數據和視圖模型

我們介紹了一些表單發佈方案,並討論了如何實現創建、更新和刪除 (CRUD) 支援。 現在,我們將進一步實施 DinnersController,並支援更豐富的表單編輯方案。 在此過程中,我們將討論兩種可用於將數據從控制器傳遞到視圖的方法:ViewData 和 ViewModel。

### <a name="passing-data-from-controllers-to-view-templates"></a>將資料從控制器傳遞到檢視範本

MVC 模式的一個定義特徵是嚴格"關注點分離",它有助於在應用程式的不同元件之間強制執行。 模型、控制器和視圖都有定義明確的角色和職責,它們之間以定義明確的方式相互通信。 這有助於提高可測試性和代碼重用性。

當 Controller 類別決定將 HTML 回應呈現回用戶端時,它負責顯式將呈現回應所需的所有資料傳遞給檢視範本。 檢視範本絕不應執行任何資料檢索或應用程式邏輯,而應限制自己僅具有由控制器從模型/數據中驅動的呈現代碼。

現在,我們的 DinnersController 類傳遞給檢視範本的模型數據簡單而直接 — 在 Index()的情況下,是晚餐物件的清單,如果是詳細資訊(、Edit()、Create() 和刪除()的情況下,只有一個晚餐物件。 當我們向應用程式添加更多 UI 功能時,我們通常需要傳遞的不僅僅是這些數據,才能在檢視範本中呈現 HTML 回應。 例如,我們可能希望將"編輯"和"創建檢視"中的"國家/地區"欄位從 HTML 文本框更改為下拉清單。 我們不是在檢視範本中硬編碼國家名稱的下拉清單,而是希望從我們動態填充的支援國家/地區列表中生成它。 我們需要一種方法,將 Dinner 物件*和支援*的國家/ 地區清單從控制器傳遞到視圖範本。

讓我們來看看兩種實現此目的的方法。

### <a name="using-the-viewdata-dictionary"></a>使用檢視資料字典

控制器基類公開一個"ViewData"字典屬性,該屬性可用於將其他數據項從控制器傳遞到視圖。

例如,為了支援我們希望將「編輯」視圖中的「國家/地區」文本框從 HTML 文本框更改為下拉清單的方案,我們可以更新我們的 Edit() 操作方法,以傳遞(除了晚餐物件之外)可用作國家/地區下拉清單的模型的 SelectList 物件。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

上面 SelectList 的建構函數正在接受要使用下拉清單以及當前選擇的值填充下拉清單的縣清單。

然後,我們可以更新我們的 Edit.aspx 檢視範本,以使用 Html.DropDownList() 説明程式方法,而不是我們以前使用的 Html.TextBox() 幫助器方法:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

上面的 Html.DropDownList() 説明器方法採用兩個參數。 第一個是要輸出的 HTML 窗體元素的名稱。 第二個是我們通過 ViewData 字典傳遞的"選擇清單" 我們使用 C#"as"關鍵字將字典中的類型轉換為 SelectList。

現在,當我們運行應用程式並訪問瀏覽器中的 */Dinners/Edit/1* URL 時,我們將看到我們的編輯 UI 已更新以顯示國家/地區清單而不是文本框:

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

由於我們還從 HTTP-POST Edit 方法呈現 Edit 檢視範本(在發生錯誤時),我們希望確保在錯誤方案中呈現檢視範本時,還要更新此方法以將 SelectList 添加到 ViewData:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

現在,我們的晚餐控制器編輯方案支援下拉清單。

### <a name="using-a-viewmodel-pattern"></a>使用檢視模型模式

ViewData 字典方法具有相當快速且易於實現的好處。 但是,有些開發人員不喜歡使用基於字串的字典,因為拼寫錯誤可能導致在編譯時不會捕獲的錯誤。 未鍵入的 ViewData 字典還要求在檢視範本中使用強類型語言(如 C#)時使用「as」運算符或強制轉換。

我們可以使用的另一種方法是通常稱為「視圖模型」 模式的方法。 使用此模式時,我們創建針對特定檢視方案優化的強類型類,並公開視圖範本所需的動態值/內容的屬性。 然後,我們的控制器類可以填充這些視圖優化的類並將其傳遞給我們的視圖範本使用。 這支援檢視範本中的類型安全、編譯時間檢查和編輯器對講。

例如,為了啟用晚餐表單編輯方案,我們可以創建一個「DinnerFormViewModel」類,如下所示,該類公開了兩個強類型屬性:一個「晚餐」物件,以及填充國家/地區下拉清單所需的 SelectList 模型:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

然後,我們可以更新我們的 Edit() 操作方法,使用從存儲庫檢索的 Dinner 物件創建 DinnerFormViewModel,然後將其傳遞到檢視範本:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

然後,我們將更新視圖範本,以便它期望有一個「DinnerFormViewModel」而不是「Dinner」物件,例如,更改 edit.aspx 頁面頂部的「繼承」屬性:

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

一旦我們這樣做,視圖範本中「模型」屬性的對講義將更新,以反映我們傳遞的 DinnerFormViewModel 類型的物件模型:

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

然後,我們可以更新視圖代碼以擺脫它。 請注意,下面我們如何不更改要創建的輸入元素的名稱(表單元素仍將命名為"標題"、"國家/地區"),但我們正在更新 HTML 幫助器方法,以便使用 DinnerFormViewModel 類檢索值:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

在呈現錯誤時,我們還將更新編輯帖子方法以使用 DinnerFormViewModel 類:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

我們還可以更新我們的 Create() 操作方法,以重複使用完全相同的*DinnerFormViewModel*類,使這些國家 / 地區也能夠刪除清單。 下面是 HTTP-GET 實現:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

下面是 HTTP-POST 建立方法的實現:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

現在,我們的"編輯"和"創建"螢幕都支持選擇國家/地區的下拉清單。

### <a name="custom-shaped-viewmodel-classes"></a>自訂元件的檢視模型類別

在上面的場景中,我們的 DinnerFormViewModel 類直接將 Dinner 模型物件公開為屬性,以及支援 SelectList 模型屬性。 此方法適用於要在檢視範本中創建的 HTML UI 與網域模型物件相對接近的情況。

對於情況並非如此的情況,可以使用的一個選項是創建一個自定義形狀的 ViewModel 類,其物件模型更優化以供視圖使用,並且可能與基礎域模型物件的外觀完全不同。 例如,它可能會公開從多個模型物件收集的不同屬性名稱和/或聚合屬性。

自定義形狀的 ViewModel 類既可用於將數據從控制器傳遞到要渲染的檢視,也可用於幫助處理發回控制器操作方法的表單數據。 對於此後續方案,您可能讓操作方法使用發佈表單的數據更新 ViewModel 物件,然後使用 ViewModel 實例映射或檢索實際域模型物件。

自定義形狀的 ViewModel 類可以提供很大的靈活性,並且每當在檢視範本中查找呈現代碼或操作方法中的表單發佈代碼開始變得過於複雜時,都是要調查的內容。 這通常表明網域模型與您生成的 UI 不乾淨對應,並且中間自定義形狀的 ViewModel 類可以提供説明。

### <a name="next-step"></a>後續步驟

現在,讓我們來瞭解一下如何使用部分頁和母版頁來重用和共用整個應用程式中的 UI。

> [!div class="step-by-step"]
> [前一個](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [下一個](re-use-ui-using-master-pages-and-partials.md)
