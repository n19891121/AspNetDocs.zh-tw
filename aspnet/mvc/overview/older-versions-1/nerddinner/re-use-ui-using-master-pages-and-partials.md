---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 使用母版頁和部分重用 UI |微軟文件
author: rick-anderson
description: 步驟 7 探討了在檢視範本中應用" DRY 原則" 的方法,以便使用部分檢視範範本和母版頁來消除代碼重複。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f381c4424a9fa0718cd234beeb01ce41bc4ca61e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542595"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>重複使用使用主版頁面和部分頁面的 UI

由[微軟](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第7步,該教程示範如何使用ASP.NET MVC 1 構建小型但完整的 Web 應用程式。
> 
> 步驟 7 探討了在檢視範本中應用" DRY 原則" 的方法,以便使用部分檢視範範本和母版頁來消除代碼重複。
> 
> 如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。

## <a name="nerddinner-step-7-partials-and-master-pages"></a>神經晚餐步驟 7:部分和母版頁

MVC 擁抱ASP.NET的設計理念之一是"不要重複自己"原則(通常稱為"DRY")。 DRY 設計有助於消除代碼和邏輯的重複,最終使應用程式構建速度更快,更易於維護。

我們已經看到 DRY 原則應用於我們的一些 NerdDinner 方案。 舉幾個例子:我們的驗證邏輯在我們的模型層中實現,這使得它可以在控制器中編輯和創建方案之間強制執行;我們正在跨「編輯」、「詳細資訊」和「刪除」操作方法重用「未找到」檢視範範範範範範範範範範範範範範範範範範範範;我們使用具有檢視範本的約定命名模式,這樣無需在調用 View() 説明器方法時顯式指定名稱;我們正在重新使用 DinnerFormViewModel 類進行編輯和創建操作方案。

現在,讓我們來看看如何在我們的視圖範本中應用"DRY 原則",以消除代碼重複。

### <a name="re-visiting-our-edit-and-create-view-templates"></a>重新存取的編輯及建立檢視範本

目前,我們使用兩個不同的檢視範本 - "Edit.aspx"和"Create.aspx" - 以顯示我們的晚餐表單 UI。 快速直觀地比較它們,突出顯示它們有多相似。 下面是建立表單的外觀:

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

下面是我們的「編輯」表單外觀:

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

沒有什麼區別嗎? 除了標題和標題文本之外,窗體佈局和輸入控制項是相同的。

如果我們打開"Edit.aspx"和"Create.aspx"視圖範本,我們會發現它們包含相同的表單佈局和輸入控制代碼。 這種重複意味著我們最終必須作出兩次更改,每當我們介紹或改變一個新的晚餐屬性 - 這是不好的。

### <a name="using-partial-view-templates"></a>使用部分檢視範本

mVC ASP.NET支援定義可用於封裝頁面子部分的檢視呈現邏輯的「部分檢視」樣本的能力。 "部分"提供了一種有用的方法來定義一次視圖呈現邏輯,然後在應用程式之間的多個位置重用它。

為了説明"DRYup"我們的 Edit.aspx 和 Create.aspx 視圖範本複製,我們可以創建名為"DinnerForm.ascx"的部分視圖範本,該範本封裝了兩者共有的窗體佈局和輸入元素。 我們將透過右鍵按下 /Views/Dinners 目錄並選擇「&gt;新增- 檢視」選單命令來執行此操作:

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

這將顯示「添加檢視」對話框。 我們將命名要創建「DinnerForm」的新檢視,在對話框中選擇「創建部分視圖」複選框,並指示我們將傳遞一個 DinnerFormViewModel 類:

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

當我們按下「添加」按鈕時,Visual Studio 將在「@Views_Dinners」目錄中為我們創建新的「DinnerForm.ascx」視圖範本。

然後,我們可以將重複的表單佈局/輸入控制代碼從我們的 Edit.aspx/ Create.aspx 視圖範本複製/粘貼到新的「DinnerForm.ascx」部分檢視範本中:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

然後,我們可以更新我們的"編輯"和"創建"視圖範本,以調用 DinnerForm 部分範本並消除表單複製。 我們可以在檢視範本中呼叫 Html.Render 部分(「DinnerForm」)來執行此操作:

##### <a name="createaspx"></a>建立.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>編輯.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

在調用 Html.Render 部分(例如:*視圖/Dinners/DinnerForm.ascx)時,您可以顯式限定所需的部分範本的路徑。 但是,在上面的代碼中,我們利用了 mVC ASP.NET中基於約定的命名模式,並將"DinnerForm"指定為要呈現的部分名稱。 當我們這樣做時ASP.NET MVC 將首先查看基於約定的視圖目錄(對於 DinnerSController,這將是 /視圖/晚餐)。 如果找不到部分範本,它將在 /Views/共享目錄中查找它。

當僅使用部分檢視的名稱調用 Html.Render 部分()時,ASP.NET MVC 將傳遞給調用視圖範本使用的相同模型和 ViewData 字典物件。 或者,有重載版本的 Html.Render 偏()使您能夠傳遞備用模型物件和/或 ViewData 字典供部分視圖使用。 這對於只想傳遞完整模型/視圖模型子集的方案非常有用。

| **側主題:為什麼&lt;&gt;%&lt;而不是&gt;%= % ?** |
| --- |
| 使用此代碼您可能注意到的一個微妙事情是,在呼&lt;叫 Html.Render.Render 部分()&lt;時,&gt;我們&gt;使用的是 % 塊 而不是 %% 塊。 &lt;%=&gt; %ASP.NET 塊表示開發人員想要呈現指定值(例如:%= &lt;"你好"&gt;百分比 將呈現"你好")。 &lt;%&gt;區塊表示開發人員想要執行代碼,並且其中的任何呈現輸出都必須顯式完成(例如:&lt;百分比回應.Write("你好")%&gt;。 我們使用&lt;上述 Html.Render&gt;部分程式碼的% 區塊的原因是 Html.Render 部份() 方法不傳回字串,而是將內容直接輸出到呼叫檢視範本的輸出流。 這樣做是出於性能效率的原因,並且這樣做可以避免創建(可能非常大的)臨時字串物件。 這減少了記憶體使用量,並提高了應用程式的總體輸送量。 使用 Html.Render 部份()時,一個常見的錯誤是忘記在呼叫結束時添加分號,而該分&lt;號在&gt;% 塊內。 例如,此代碼將導致編譯器錯誤:% &lt;Html.Render 部分("DinnerForm")您&gt;需要編&lt;寫: % html.render部分("DinnerForm");%&gt;這是&lt;因為&gt;% % 塊是自包含的程式碼語句,並且使用 C# 程式碼語句時需要用分號終止。 |

### <a name="using-partial-view-templates-to-clarify-code"></a>使用部分檢視樣本來澄清代碼

我們創建了"DinnerForm"部分視圖範本,以避免在多個位置複製視圖呈現邏輯。 這是創建部分檢視範本的最常見原因。

有時,即使只在單個位置調用部分視圖,創建部分視圖仍然有意義。 非常複雜的檢視範本在提取檢視呈現邏輯並將其分區為一個或多個命名良好的部分範本時,通常更容易閱讀。

例如,在我們的項目中考慮 Site.master 檔中的以下代碼段(我們稍後將查看)。 代碼相對直接讀取 - 部分是因為在螢幕右上角顯示登入/登出連結的邏輯封裝在「LogOnUserControl」部分:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

每當您發現自己試圖瞭解檢視範本中的 html/代碼標記時感到困惑,請考慮如果提取某些標記並將其重構為命名良好的部分檢視,是否不清楚。

### <a name="master-pages"></a>主版頁面

除了支援部分檢視外,ASP.NET MVC 還支援創建可用於定義網站通用佈局和頂級 html 的「母版頁」範本的功能。 然後,可以將內容占位符控件添加到母版頁,以標識視圖可以覆蓋或"填充"的可替換區域。 這提供了一種非常有效(和 DRY)的方法,用於跨應用程式應用通用佈局。

默認情況下,新的ASP.NET MVC 專案會自動向其添加母版頁範本。 此母版頁名為「Site.master」,位於 [視圖] 共用] 資料夾中:

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

預設的 Site.master 檔如下所示。 它定義網站的外層 html,以及頂部導航功能表。 它包含兩個可取代的內容佔位元控制檔 - 一個用於標題,另一個用於要取代頁面的主要內容的位置:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

我們為NerdDinner應用程式創建的所有檢視範本("清單"、"詳細資訊"、"編輯"、"創建"、"未找到"等)都基於此 Site.master 範本。 當我們使用「新增檢視」對話框建立檢視時,預設情況下新增到頂部&lt;% = 頁面&gt;% 指令的「MasterPageFile」屬性指示此指示:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

這意味著我們可以更改 Site.master 內容,並在呈現任何檢視範本時自動應用和使用更改。

讓我們更新我們的網站.master 的標頭部分,以便我們的應用程式的標頭是"NerdDinner"而不是"我的 MVC 應用程式"。 讓我們還更新我們的導航功能表,以便第一個選項卡是「查找晚餐」(由 HomeController 的 Index() 操作方法處理),並且讓我們添加一個名為"主持晚餐「的新選項卡(由 DinnersController 的 Create() 操作方法處理):

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

當我們保存 Site.master 檔並刷新瀏覽器時,我們將看到我們的標頭更改顯示在應用程式中的所有檢視中。 例如：

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

使用 */Dinners/編輯/[id]* URL:

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>後續步驟

部分頁和母版頁提供了非常靈活的選項,使您能夠乾淨地組織視圖。 您會發現,它們可説明您避免複製檢視內容/代碼,並使檢視範本更易於閱讀和維護。

現在,讓我們重新訪問我們之前構建的清單方案,並啟用可擴展的分頁支援。

> [!div class="step-by-step"]
> [前一個](use-viewdata-and-implement-viewmodel-classes.md)
> [下一個](implement-efficient-data-paging.md)
