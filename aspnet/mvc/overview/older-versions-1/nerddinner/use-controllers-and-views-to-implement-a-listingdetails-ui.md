---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 使用控制器和檢視實現清單/詳細資訊 UI |微軟文件
author: rick-anderson
description: 步驟 4 展示如何向應用程式添加控制器,該應用程式利用我們的模型為使用者提供數據清單/詳細資訊導航體驗...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 49c7dc977477a4edbfcfc68b166ae7ea3fa22f2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541308"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>使用控制器和檢視來實作清單/詳細資料 UI

由[微軟](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第4步,它介紹了如何使用 ASP.NETmVC 1構建小型但完整的Web應用程式。
> 
> 步驟 4 演示如何向應用程式添加控制器,該應用程式利用我們的模型為使用者提供在 NerdDinner 網站上晚餐的數據列表/詳細資訊導航體驗。
> 
> 如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。

## <a name="nerddinner-step-4-controllers-and-views"></a>神經晚餐步驟 4:控制器和檢視

對於傳統的 Web 框架(經典 ASP、PHP、ASP.NET Web 窗體等),傳入 URL 通常映射到磁碟上的檔。 例如:諸如"/Products.aspx"或"/Products.php"這樣的 URL 請求可能由"Products.aspx"或"Products.php"檔處理。

基於 Web 的 MVC 框架以略有不同的方式將 URL 映射到伺服器代碼。 它們不是將傳入 URL 映射到檔,而是將 URL 映射到類上的方法。 這些類稱為"控制器",它們負責處理傳入的 HTTP 請求、處理使用者輸入、檢索和保存數據以及確定要發送回用戶端的回應(顯示 HTML、下載檔、重定向到其他 URL 等)。

現在,我們已經為我們的NerdDinner應用程式建立了基本模型,我們的下一步將是向應用程式添加一個控制器,利用它為使用者提供我們網站上的 Dinner 的數據列表/詳細資訊導航體驗。

### <a name="adding-a-dinnerscontroller-controller"></a>新增晚餐控制器控制器

我們將從右鍵單擊 Web 專案中的「控制器」資料夾開始,然後選擇 **「新增-&gt;控制器」** 選單命令(您也可以通過鍵入 Ctrl-M、Ctrl-C 來執行此指令):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

這會彈出「新增控制器」對話框:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

我們將命名新的控制器「DinnersController」,然後單擊「添加」按鈕。 然後,Visual Studio 將在我們的 @控制器目錄下添加DinnersController.cs檔:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

它還將在代碼編輯器中打開新的 DinnersController 類。

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>新增一個晚餐控制器類別

我們希望讓使用我們的應用程式的訪問者流覽即將舉辦的晚宴清單,並允許他們點擊清單中的任何晚餐以查看有關此晚餐的具體細節。 我們將透過發佈應用程式的以下網址執行此操作:

| **URL** | **目的** |
| --- | --- |
| */晚餐/* | 顯示即將來臨的晚宴的 HTML 清單 |
| */晚餐/詳情/[id]* | 顯示網址 中嵌入的「id」參數指示的特定晚餐的詳細資訊, 這將與資料庫中的晚餐 ID 匹配。 例如:/Dinners/詳細資訊/2 將顯示一個 HTML 頁面,其中詳細介紹了晚餐 ID 值為 2 的晚餐。 |

我們將通過向 DinnersController 類中添加兩種公共「操作方法」來發佈這些 URL 的初始實現,如下所示:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

然後,我們將運行NerdDinner應用程式,並使用我們的瀏覽器來調用它們。 鍵入 *「/Dinners/」URL*將導致我們的*Index()* 方法執行,並且它將發送回以下回應:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

鍵入 *"/晚餐/詳細資訊/2"URL*將導致運行*我們的詳細資訊()* 方法,併發送回以下回應:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

您可能想知道 - ASP.NET MVC 如何知道創建我們的 DinnersController 類並調用這些方法? 為了理解這一點,讓我們快速瞭解路由的工作原理。

### <a name="understanding-aspnet-mvc-routing"></a>瞭解ASP.NET MVC 路由

ASP.NET MVC 包含強大的 URL 路由引擎,在控制 URL 如何映射到控制器類方面提供了很大的靈活性。 它允許我們完全自定義ASP.NET MVC 如何選擇要建立的控制器類、調用哪種方法,以及配置不同的方式,以便變數可以從 URL/Querystring 自動解析並傳遞給方法作為參數參數。 它提供了靈活性,完全優化了SEO網站(搜尋引擎優化),以及發佈任何我們想要從應用程式。

默認情況下,新的ASP.NET MVC 專案附帶一組已註冊的 URL 路由規則。 這使我們能夠輕鬆啟動應用程式,而無需顯式配置任何內容。 預設路由規則註冊可以在專案的「應用程式」類別中找到, 我們可以透過按兩下專案根目錄中的「Global.asax」檔案來開啟:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

預設ASP.NET MVC 路由規則在此類的「註冊路由」方法中註冊:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

"路線。上面的 MapRoute()方法調用註冊了一個預設路由規則,該規則使用 URL 格式將傳入 URL 映射到控制器類:"//{控制器}/{{{操作}/{id}" - 其中"控制器"是要實例化的控制器類的名稱,"操作"是要調用它的公共方法的名稱,"id"是嵌入在 URL 中的可選參數,可以作為參數傳遞給該方法。 傳遞給"MapRoute()"方法調用的第三個參數是一組預設值,用於在 URL 中不存在的控制器/操作/id 值(控制器 = "Home",操作 ="索引",Id=")。

下面是一個表,演示如何使用預設的<em>"//控制器\/{操作}/{id}"</em>路由規則映射各種 URL:

| **URL** | **控制器類** | **動作方法** | **傳遞的參數** |
| --- | --- | --- | --- |
| */晚餐/細節/2* | 晚餐控制器 | 詳細資訊(ID) | id=2 |
| */晚餐/編輯/5* | 晚餐控制器 | 編輯(ID) | id=5 |
| */晚餐/創建* | 晚餐控制器 | Create() | N/A |
| */晚餐* | 晚餐控制器 | 索引() | N/A |
| */首頁* | 家用控制器 | 索引() | N/A |
| */* | 家用控制器 | 索引() | N/A |

最後三行顯示正在使用的預設值(控制器 = 主頁、操作 + 索引、ID ="")。 由於「Index」方法註冊為預設操作名稱(如果未指定),因此「/Dinners」和「/home」URL 會導致在其控制器類上調用 Index() 操作方法。 由於"Home"控制器在未指定時註冊為預設控制器,因此"/" URL會導致創建 HomeController,並調用其上的索引() 操作方法。

如果您不喜歡這些預設 URL 路由規則,好消息是它們很容易更改 - 只需在上面的註冊路由方法中編輯它們即可。 但是,對於我們的NerdDinner應用程式,我們不會更改任何預設URL路由規則,而只是將它們作為本操作使用。

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>使用我們的晚餐控制器的晚餐儲存庫

現在,讓我們用使用我們的模型的實現替換當前對 DinnersController Index() 和詳細資訊()操作方法的實現。

我們將使用之前構建的 DinnerRepository 類來實現該行為。 我們將首先添加一個"使用"語句,該語句引用"NerdDinner.Model"命名空間,然後聲明我們的 DinnerRepository 的實例作為 DinnerController 類上的字段。

在本章的後面部分,我們將介紹"依賴注入"的概念,並展示我們的控制器獲取對 DinnerRepository 的引用的另一種方法,該存儲庫可實現更好的單元測試 -但現在,我們將創建一個類似於下面的 DinnerRepository 內聯實例。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

現在,我們準備使用檢索到的數據模型物件生成 HTML 回應。

### <a name="using-views-with-our-controller"></a>將檢視與我們的控制器一起使用

雖然可以在我們的操作方法中編寫代碼來組裝 HTML,然後使用*Response.Write()* 説明器方法將其發送回用戶端,但這種方法很快就會變得相當笨拙。 更好的方法是,我們只能在 DinnersController 操作方法中執行應用程式和數據邏輯,然後將呈現 HTML 回應所需的數據傳遞給負責提供其 HTML 表示的單獨"視圖"範本。 正如我們在一瞬間看到的,"視圖"範本是一個文字檔,通常包含 HTML 標記和嵌入呈現代碼的組合。

將控制器邏輯與視圖渲染分離帶來了幾個大好處。 特別是,它有助於在應用程式代碼和UI格式/呈現代碼之間強制實施明確的"關注點分離"。 這使得與 UI 呈現邏輯隔離的單元測試應用程式邏輯變得更加容易。 它便於以後修改 UI 呈現範本,而無需更改應用程式代碼。 而且,它可以使開發人員和設計人員更輕鬆地在專案上協作。

我們可以更新 DinnersController 類,以指示我們希望使用視圖範本發送回 HTML UI 回應,方法是將兩種操作方法的方法簽名從返回類型的"void"改為"ActionResult"。" 然後,我們可以調用控制器基類上的*View()* 幫助器方法返回如下所示的「ViewResult」物件:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

我們在上面使用的*View()* 説明器方法的簽名如下所示:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

*View()* 説明程式方法的第一個參數是我們要用於呈現 HTML 回應的檢視範本檔的名稱。 第二個參數是一個模型物件,其中包含檢視範本為呈現 HTML 回應所需的數據。

在我們的 Index() 操作方法中,我們調用*View()* 説明器方法,並指示我們希望使用"Index"視圖範本呈現晚餐的 HTML 清單。 我們正在傳遞檢視範本一系列 Dinner 物件,以便從以下角度生成清單:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

在我們的「詳細資訊」操作方法中,我們嘗試使用 URL 中提供的 ID 檢索 Dinner 物件。 如果找到有效的"晚餐",我們調用*View()* 説明器方法,指示我們要使用"詳細資訊"視圖範本來呈現檢索到的 Dinner 物件。 如果請求無效的晚餐,我們會呈現一條有用的錯誤消息,指示使用"NotFound"視圖範本(以及僅採用範本名稱的*View()* 幫助器方法的重載版本不存在 Dinner:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

現在,讓我們實現"未找到"、"詳細資訊"和"索引"視圖範本。

### <a name="implementing-the-notfound-view-template"></a>實作「未找到」檢視範本

我們將首先實現"NotFound"視圖範本 -它顯示一條友好的錯誤消息,指示找不到請求的晚餐。

我們將通過在控制器操作方法中定位文本游標來創建新的檢視範本,然後右鍵按一下並選擇「新增檢視」選單命令(我們還可以通過鍵入 Ctrl-M、Ctrl-V 來執行此命令):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

這將彈出一個"添加視圖"對話框,如下所示。 預設情況下,對話方塊將預填充創建檢視的名稱,以匹配啟動對話框時光標所採用的操作方法的名稱(在本例中為"詳細資訊")。 由於我們想要首先實現「未找到」範本,我們將重寫此檢視名稱並將其設置為「未找到」:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

按下「添加」按鈕時,Visual Studio 將在「_Views_Dinners」目錄中為我們創建新的「NotFound.aspx」檢視範本(如果目錄不存在,它還會創建該範本):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

它還將在代碼編輯器中打開我們新的「NotFound.aspx」檢視範本:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

默認情況下,查看範本有兩個"內容區域",我們可以在其中添加內容和代碼。 第一個允許我們自定義發回的 HTML 頁面的"標題" 第二個允許我們自定義發回的 HTML 頁面的「主要內容」。

要實現我們的「未找到」檢視範本,我們將添加一些基本內容:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

然後,我們可以在瀏覽器中試用。 為此,讓我們請求 *"/晚餐/詳細資訊/9999"URL。* 這將引用資料庫中當前不存在的晚餐,並導致我們的 DinnersController.詳細資訊() 操作方法呈現我們的「未找到」檢視範本:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

在上面的螢幕截圖中,您會注意到一件事,那就是我們的基本檢視範本繼承了一堆環繞螢幕上主要內容的 HTML。 這是因為我們的檢視範本使用「母版頁」樣本,使我們能夠在網站上的所有視圖上應用一致的佈局。 我們將在本教程的後續部分討論母版頁如何工作。

### <a name="implementing-the-details-view-template"></a>實作「詳細資訊」檢視範本

現在,讓我們實現「詳細資訊」檢視範本, 它將為單個晚餐模型生成 HTML。

我們將通過將文字游標定位到「詳細資訊」操作方法中,然後右鍵單擊並選擇「添加檢視」選單命令(或按 Ctrl-M,Ctrl-V) 來執行此操作:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

這將彈出「添加檢視」對話框。 我們將保留預設檢視名稱("詳細資訊")。 我們還在對話框中選擇"創建強類型視圖"複選框,並選擇(使用組合框下拉下)我們從控制器傳遞到視圖的模型類型的名稱。 對於此檢視,我們傳遞一個 Dinner 物件(此類型的完全限定名稱為:「NerdDinner.Model.Dinner」):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

與之前選擇創建"空視圖"的範本不同,這次我們將選擇使用"詳細資訊"範本自動"基架"視圖。 我們可以通過更改上面對話方塊中的「查看內容」 下拉清單來指示這一點。

"Scaffold"將根據我們傳遞給它的 Dinner 物件生成我們詳細資訊視圖範本的初始實現。 這為我們提供了一種快速開始視圖範本實現的簡單方法。

當我們按下「添加」按鈕時,Visual Studio 將在「@Views_Dinners」目錄中為我們創建新的「詳細資訊.aspx」檢視範本檔:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

它還將在代碼編輯器中打開我們新的"Details.aspx"視圖範本。 它將包含基於 Dinner 模型的詳細資訊視圖的初始基架實現。 基架引擎使用 .NET 反射來查看通過該資料庫的類上公開的公共屬性,並將根據找到的每個類型添加適當的內容:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

我們可以請求 *"/晚餐/詳細資訊/1"URL*以查看瀏覽器中此"詳細資訊"基架實現的外觀。 使用此網址會顯示我們首次建立資料庫時手動到資料庫的晚餐之一:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

這讓我們快速啟動和運行,並為我們提供了詳細資訊.aspx 視圖的初始實現。 然後,我們可以去調整它,以自定義 UI,以讓我們滿意。

當我們更仔細地查看 Details.aspx 範本時,我們會發現它包含靜態 HTML 以及嵌入式呈現代碼。 &lt;%&gt;程式碼塊在檢視樣本呈現時執行代碼&lt;,%=&gt;% 程式碼塊執行其中包含的代碼,然後將結果呈現給範本的輸出流。

我們可以在View中編寫代碼,該代碼訪問使用強類型"Model"屬性從控制器傳遞的"Dinner"模型物件。 Visual Studio 在編輯器中存取此「模型」屬性時,為我們提供了完整的代碼無意義:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

讓我們做一些調整,以便我們最終的詳細資訊視圖範本的源如下所示:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

當我們再次訪問 *「/晚餐/細節/1」URL*時,它現在將呈現如下:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>實現「索引」檢視範本

現在,讓我們實現"索引"視圖範本 - 這將生成即將推出的晚餐的清單。 為此,我們將將文本游標定位在 Index 操作方法中,然後右鍵單擊並選擇「添加檢視」功能表命令(或按 Ctrl-M、Ctrl-V)。

在"添加視圖"對話框中,我們將保留名為"索引"的視圖範本,並選擇"創建強類型視圖"複選框。 這一次,我們將選擇自動生成「列表」檢視範範本,並選擇「NerdDinner.Model.Dinner」作為傳遞給檢視的模型類型(由於我們已指示我們正在創建「列表」基架將導致添加視圖對話框假定我們將一系列 Dinner 物件從控制器傳遞到視圖):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

當我們按下「添加」按鈕時,Visual Studio 將在「@Views_Dinners」目錄中為我們創建新的「Index.aspx」檢視範本檔。 它將「支架」在其中的初始實現,提供我們傳遞給檢視的 Dinner 的 HTML 表清單。

當我們運行應用程式並訪問 *「/Dinners/」URL*時,它將呈現我們的晚餐清單,如下所示:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

上面的表格解決方案為我們提供了一個網格般的佈局,我們的晚餐數據 – 這不是我們想要為我們的消費者面對晚餐上市。 我們可以更新 Index.aspx 檢視範本並對其進行修改以列出較少的資料列,&lt;並&gt;使用 ul 元素呈現它們,而不是使用以下代碼呈現表:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

當我們迴圈展示模型中的每個晚餐時,我們使用上述"var"關鍵字。 不熟悉 C# 3.0 的人可能會認為使用"var"意味著晚餐對像是後期綁定的。 相反,這意味著編譯器使用針對強類型"模型"屬性的類型推理(類型為&lt;&gt;"IE500Dinner"),並將本地"Dinner"變數編譯為 Dinner 類型 - 這意味著我們在代碼塊中獲取完全的無意義和編譯時間檢查:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

當我們在瀏覽器中的 */Dinners* URL 上刷新時,我們更新的視圖現在如下所示:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

看起來更好,但還沒有完全存在。 我們的最後一步是使最終使用者能夠點擊清單中的單個晚餐並查看有關它們的詳細資訊。 我們將透過呈現連結到晚餐控制器上「詳細資訊」操作方法的 HTML 超連結元素來實現此內容。

我們可以在 Index 檢視中以兩種方式之一生成這些超連結。 第一種是手動建立&lt;&gt;HTML 元素,如下所示,&lt;&gt;其中&gt;我們在&lt;HTML 元素內嵌入 % 區塊:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

我們可以使用的替代方法是利用 MVC 中 ASP.NET 內建的「Html.ActionLink())」幫助器方法,該方法支援以程式設計方式&lt;建立&gt;HTML 元素, 該 元素連結到控制器上的另一個操作方法:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

Html.ActionLink() 説明器方法的第一個參數是要顯示的連結文本(在本例中為 Dinner 的標題),第二個參數是我們想要將連結生成的控制器操作名稱(在本例中為詳細資訊方法),第三個參數是一組要發送到操作的參數(作為具有屬性名稱/值的匿名類型實現)。 在這種情況下,我們指定我們要連結到的晚餐的「id」參數,並且由於 ASP.NET MVC 中的預設 URL 路由規則為 Html.ActionLink() 幫助器方法的"{控制器}/{操作}/{id}",因此 Html.ActionLink() 説明程式方法將生成以下輸出:

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

對於我們的 Index.aspx 檢視,我們將使用 Html.ActionLink() 說明器方法方法,並將每個晚餐都包含到相應詳細資訊 URL 的連結中:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

現在,當我們點擊 */Dinners* URL 時,我們的晚餐清單如下所示:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

當我們按一下清單中的任何晚餐時,我們將導航以查看有關它的詳細資訊:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>基於慣例的命名與 _Views目錄結構

默認情況下ASP.NET MVC 應用程式在解決檢視範本時使用基於約定的目錄命名結構。 這允許開發人員在從 Controller 類中引用檢視時避免對位置路徑進行完全限定。 默認情況下ASP.NET MVC 將在應用程式下方的\[[視圖\*控制器名稱] 目錄中尋找檢視範本檔。

例如,我們一直在研究 DinnersController 類,該類顯式引用三個視圖範本:「索引」、「詳細資訊」和」未找到」。 預設情況下,ASP.NET MVC 將在應用程式根目錄下的 *[Views_Dinners]* 目錄中尋找這些檢視:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

請注意,專案中當前存在三個控制器類(DinnersController、HomeController 和 AccountController - 在創建專案時預設添加了後兩個控制器類),並且_Views 目錄中有三個子目錄(每個控制器一個)。

從「主頁」和「帳戶」控制器引用的檢視將自動解析其檢視範本,這些範本來自相應的 *[視圖]主頁*和 *[視圖]帳戶*目錄。 *[Views]共用*子目錄提供了一種存儲在應用程式中多個控制器中重複使用的視圖範本的方法。 當 ASP.NET MVC 嘗試解析檢視範本時,它將首先在 *[視圖\[控制器]* 特定目錄中進行檢查,如果無法找到視圖範本,它將在 *[Views_Shared]* 目錄中查找。

在命名單個視圖範本時,建議的指導是讓視圖範本共用與導致其呈現的操作方法相同的名稱。 例如,上面的"Index"操作方法是使用"索引"視圖來呈現視圖結果,而"詳細資訊"操作方法使用"詳細資訊"視圖來呈現其結果。 這樣,就可以輕鬆快速查看與每個操作關聯的範本。

當檢視範本與在控制器上調用的操作方法具有相同的名稱時,開發人員不需要顯式指定視圖範本名稱。 相反,我們可以將模型物件傳遞給"View()"幫助器方法(不指定視圖名稱),並且ASP.NET MVC 將自動推斷我們希望在磁碟上使用 *[視圖\[\[控制器名稱] 操作名稱]* 視圖範本來呈現它。

這使我們能夠稍微清理一下控制器代碼,並避免在代碼中重複兩次名稱:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

上述代碼是實現一個不錯的晚餐清單/細節體驗的網站所需要的一切。

#### <a name="next-step"></a>後續步驟

我們現在有一個不錯的晚餐瀏覽體驗建立。

現在,讓我們啟用 CRUD(創建、讀取、更新、刪除)數據表單編輯支援。

> [!div class="step-by-step"]
> [前一個](build-a-model-with-business-rule-validations.md)
> [下一個](provide-crud-create-read-update-delete-data-form-entry-support.md)
