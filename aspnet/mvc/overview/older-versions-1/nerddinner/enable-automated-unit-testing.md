---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 開啟自動單元測試 |微軟文件
author: rick-anderson
description: 步驟 12 演示如何開發一套自動單元測試,以驗證我們的 NerdDinner 功能,這將讓我們有信心進行更改...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 7fe84efd9e4cc359c19d5ab9e22c579b80207e9c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541464"
---
# <a name="enable-automated-unit-testing"></a>啟用自動化單元測試

由[微軟](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第12步,它介紹了如何使用 ASP.NETmVC 1構建小型但完整的Web應用程式。
> 
> 步驟 12 演示如何開發一套自動單元測試,以驗證我們的 NerdDinner 功能,這將讓我們有信心在未來對應用程式進行更改和改進。
> 
> 如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。

## <a name="nerddinner-step-12-unit-testing"></a>神經晚餐步驟 12:單元測試

讓我們開發一套自動單元測試,以驗證我們的NerdDinner功能,這將讓我們有信心在未來對應用程式進行更改和改進。

### <a name="why-unit-test"></a>為什麼選擇單元測試?

在一天早上上班時,你突然閃現出一些關於你正在處理的應用程序的靈感。 您意識到,您可以實現一個更改,這將使應用程式顯著更好地。 它可能是清理代碼、添加新功能或修復 Bug 的重構。

當你到達計算機時,您面臨的問題是「進行這種改進有多安全? 如果做出改變有副作用或破壞某些東西呢? 更改可能很簡單,只需幾分鐘即可實現,但如果手動測試所有應用程式方案需要數小時,該怎麼辦? 如果您忘記覆蓋場景,而損壞的應用程式投入生產,該怎麼辦? 做出這種改進真的值得付出所有努力嗎?

自動單元測試可以提供一個安全網,使您能夠持續增強應用程式,並避免害怕您正在處理的代碼。 通過自動測試來快速驗證功能,使您能夠自信地編寫代碼,並使您能夠做出改進,否則您可能覺得這樣做並不自在。 它們還有助於創建更可維護且使用壽命更長的解決方案,從而獲得更高的投資回報。

ASP.NET MVC 框架使單元測試應用程式功能變得簡單自然。 它還支援測試驅動開發 (TDD) 工作流,支援基於測試優先的開發。

### <a name="nerddinnertests-project"></a>內德晚餐.測試專案

當我們在本教程開始時創建NerdDinner 應用程式時,系統會提示我們進行一個對話框,詢問我們是否希望創建一個單元測試專案以配合應用程式專案:

![](enable-automated-unit-testing/_static/image1.png)

我們保留了「是,創建一個單元測試專案」單選按鈕 -導致「NerdDinner.Test」專案被添加到我們的解決方案中:

![](enable-automated-unit-testing/_static/image2.png)

NerdDinner.測試專案引用NerdDinner應用程式專案程式集,並使我們能夠輕鬆地向其添加自動測試,以驗證應用程式功能。

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>為我們的晚餐模型類創建單元測試

讓我們向NerdDinner.測試專案添加一些測試,以驗證我們在構建模型層時創建的Dinner類。

我們將首先在我們的測試項目中創建一個名為"模型"的新資料夾,我們將在這裡放置與模型相關的測試。 然後,我們將右鍵單擊該資料夾並選擇 **「添加&gt;- 新測試」** 功能表命令。 這將彈出「添加新測試」對話方塊。

我們將選擇創建「單元測試」並將其命名為「DinnerTest.cs」:

![](enable-automated-unit-testing/_static/image3.png)

當我們按下「ok」按鈕 Visual Studio 會向專案添加(並打開)DinnerTest.cs 檔時:

![](enable-automated-unit-testing/_static/image4.png)

默認的 Visual Studio 單元測試範本內有一堆樣板代碼,我覺得有點亂。 讓我們清理它,以便只包含以下代碼:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

上面的 DinnerTest 類上的 [TestClass] 屬性將其識別為包含測試的類以及可選的測試初始化和拆解代碼。 我們可以通過在其中添加具有 [TestMethod] 屬性的公共方法來定義其中的測試。

下面是我們將添加的兩個測試中的第一個,即鍛煉我們的晚餐課程。 第一個測試驗證,如果新晚餐的創建沒有正確設置所有屬性,則我們的晚餐無效。 第二個測試驗證我們的晚餐是否有效,當晚餐具有具有有效值的所有屬性設置時:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

您在上面會注意到我們的測試名稱非常明確(而且有些詳細)。 我們這樣做是因為我們可能最終創建數百或數千個小測試,我們希望能夠輕鬆快速確定每個測試程序的意圖和行為(尤其是在查看測試運行程式中的失敗清單時)。 測試名稱應以測試的功能命名。 上面我們使用的是"名詞\_\_應該動詞"命名模式。

我們使用「AAA」測試模式構建測試,該模式代表「安排、操作、斷言」:

- 排列:設定正在測試的裝置
- 操作:鍛煉被測試的單位並捕獲結果
- 斷言:驗證行為

當我們編寫測試時,我們希望避免讓單個測試執行太多操作。 相反,每個測試應只驗證一個概念(這將使確定故障原因變得更加容易)。 一個好的準則是嘗試每個測試只有一個斷言語句。 如果在測試方法中有多個斷言語句,請確保它們都用於測試同一概念。 如有疑問,再做一次測試。

### <a name="running-tests"></a>正在執行測試

Visual Studio 2008 專業版(和更高版本)包括一個內置測試運行程式,可用於在 IDE 中運行 Visual Studio 單元測試專案。 我們可以選擇解決方案選單**中的&gt;「&gt;測試- 執行-所有測試**」命令(或鍵入 Ctrl R,A)來執行我們所有的單元測試。 或者,我們可以將游標定位到特定的測試類或測試方法中,並使用**當前上下文菜單&gt;中的&gt;測試運行 測試**命令(或鍵入 Ctrl R、T)來運行單元測試的子集。

讓我們將游標定位在 DinnerTest 類中,並鍵入"Ctrl R,T"以運行我們剛剛定義的兩個測試。 當我們執行此操作時,Visual Studio 中將顯示一個「測試結果」視窗,我們將看到其中列出的測試運行結果:

![](enable-automated-unit-testing/_static/image5.png)

*注意:預設情況下,VS 測試結果視窗不顯示"類名稱"列。您可以通過在「測試結果」視窗中右鍵按下並使用「添加/刪除列」選單命令來添加此內容。*

我們的兩個測試只用了一小部分時間就可以運行了,正如您所看到的,它們都通過了。 現在,我們可以通過創建驗證特定規則驗證的其他測試來擴展它們,並涵蓋我們添加到 Dinner 類的兩種説明方法 - IsUserHost() 和 IsUser 註冊()。 為 Dinner 類提供所有這些測試將使將來向該課程添加新業務規則和驗證變得更加簡單和安全。 我們可以將新的規則邏輯添加到 Dinner,然後在幾秒鐘內驗證它是否沒有破壞我們以前的任何邏輯功能。

請注意,使用描述性測試名稱如何便於快速瞭解每個測試正在驗證的內容。 我建議使用 **「工具&gt;- 選項」** 選單命令,打開&gt;測試工具- 測試執行設定螢幕,並選取中「按兩下失敗或不確定的單位測試結果顯示測試中的失敗點」複選框。 這將允許您雙擊測試結果視窗中的故障,並立即跳轉到斷言失敗。

### <a name="creating-dinnerscontroller-unit-tests"></a>建立晚餐控制器單元測試

現在,讓我們創建一些單元測試,以驗證我們的 DinnersController 功能。 我們將從右鍵單擊測試專案中的"控制器"資料夾開始,然後選擇**&gt;「新增測試」** 功能表命令。 我們將創建一個「單元測試」並將其命名為「DinnersControllerTest.cs」。

我們將創建兩種測試方法,以驗證 DinnersController 上的細節() 操作方法。 第一個將驗證在請求現有晚餐時是否返回了視圖。 第二個將驗證在請求不存在的晚餐時是否返回「未找到」檢視:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

上述代碼編譯乾淨。 但是,當我們運行測試時,它們都失敗:

![](enable-automated-unit-testing/_static/image6.png)

如果我們查看錯誤消息,我們將看到測試失敗的原因是因為我們的 DinnersRepository 類無法連接到資料庫。 我們的NerdDinner應用程式使用連接字串到本地SQL Server Express檔案,該檔\_位於NerdDinner應用程式專案的#App資料目錄下。 由於我們的NerdDinner.測試專案編譯並運行在不同的目錄中,然後以應用程式專案運行,因此連接字串的相對路徑位置不正確。

*我們可以*通過將 SQL Express 資料庫檔案複製到測試專案來解決此問題,然後在測試專案的 App.config 中向它添加適當的測試連接字串。 這將使上述測試解除阻止並運行。

但是,使用真實資料庫的單位測試代碼帶來了許多挑戰。 具體來說：

- 它顯著減慢了單元測試的執行時間。 運行測試所需的時間越長,執行測試的可能性就越小。 理想情況下,您希望單元測試能夠在幾秒鐘內運行,並且讓它像編譯項目一樣自然地完成。
- 它在測試中使設置和清理邏輯複雜化。 您希望每個單元測試都隔離並獨立於其他測試(沒有副作用或依賴項)。 在對真實資料庫工作時,您必須注意狀態並在測試之間重置它。

讓我們來看看一種稱為"依賴注入"的設計模式,它可以幫助我們解決這些問題,並避免使用真實資料庫作為測試的需要。

### <a name="dependency-injection"></a>相依性插入

現在,晚餐控制器與晚餐存儲庫類緊密地"耦合"。 "耦合"是指類顯式依賴於另一個類才能工作的情況:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

由於 DinnerRepository 類需要訪問資料庫,因此 DinnersController 類在 DinnerRepository 上的緊密耦合依賴關係最終要求我們有一個資料庫才能測試 DinnersController 操作方法。

我們可以採用稱為"依賴注入"的設計模式來克服這一問題,這種方法在使用依賴項(如提供數據訪問的存儲庫類)中不再隱式創建。 相反,依賴項可以顯式傳遞給使用構造函數參數使用它們的類。 如果使用介面定義依賴項,則我們可以靈活地通過單元測試方案的"假"依賴項實現。 這使我們能夠創建實際上不需要訪問資料庫的特定於測試的依賴項實現。

為了看到此操作,讓我們使用 DinnersController 實現依賴項注入。

#### <a name="extracting-an-idinnerrepository-interface"></a>擷取 IDinner 儲存庫介面

我們的第一步是創建一個新的 IDinnerRepository 介面,該介面封裝了控制器檢索和更新 Dinner 所需的儲存庫合同。

我們可以手動定義此介面協定,通過右鍵單擊 #Model 資料夾,然後選擇 **「添加-&gt;新專案」** 功能表命令並創建名為 IDinnerRepository.cs 的新介面。

或者,我們可以使用內置於 Visual Studio 專業版(和更高版本)的重構工具,從現有的 DinnerRepository 類中自動提取和創建我們的介面。 要使用 VS 擷取此介面,只需將游標放在 DinnerRepository 類別的文字編輯器中,然後右鍵按下選擇 **「重構-&gt;抽取介面」** 選單指令:

![](enable-automated-unit-testing/_static/image7.png)

這將啟動「提取介面」對話框,並提示我們建立介面的名稱。 它將預設為 IDinnerRepository,並自動選擇現有 DinnerRepository 類上的所有公共方法以添加到介面:

![](enable-automated-unit-testing/_static/image8.png)

當我們按下「確定」按鈕時,Visual Studio 將為我們的應用程式添加新的 IDinnerRepository 介面:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

我們現有的 DinnerRepository 類將被更新,以便實現介面:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>更新晚餐控制器以支援建構函數注入

現在,我們將更新 DinnersController 類以使用新介面。

目前,晚餐控制器是硬編碼的,因此其「晚餐存儲庫」欄位始終是一個晚餐存儲庫類:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

我們將更改它,以便「晚餐存儲庫」欄位是IDinner儲存庫類型,而不是晚餐儲存庫。 然後,我們將添加兩個公共 DinnersController 構造函數。 其中一個構造函數允許將IDinnerRepository作為參數傳遞。 另一個是使用我們現有的 DinnerRepository 實現的預設建構函數:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

由於預設情況下ASP.NET MVC 使用預設構造函數創建控制器類,因此運行時的 DinnersController 將繼續使用 DinnerRepository 類來執行數據訪問。

但是,我們現在可以更新我們的單元測試,以便使用參數構造函數在"假"晚餐存儲庫實現中傳遞。 此「假」晚餐存儲庫不需要訪問真實資料庫,而是使用記憶體中的範例數據。

#### <a name="creating-the-fakedinnerrepository-class"></a>建立假晚餐儲存庫類

讓我們創建一個假晚餐存儲庫類。

我們將首先在我們的NerdDinner.測試項目中創建一個"Fakes"目錄,然後向它添加新的FakeDinnerRepository類(右鍵單擊該文件夾並選擇 **"&gt;添加- 新類**"):

![](enable-automated-unit-testing/_static/image9.png)

我們將更新代碼,以便 FakeDinnerRepository 類實現 IDinnerRepository 介面。 然後,我們可以右鍵單擊它並選擇「實現介面 IDinnerRepository」上下文菜單命令:

![](enable-automated-unit-testing/_static/image10.png)

這將導致 Visual Studio 自動將所有 IDinnerRepository 介面成員添加到我們的 FakeDinnerRepository 類,並包含預設的「存分之外」實現:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

然後,我們可以更新 FakeDinnerRepository 實現,以處理作為構造函數參數&lt;傳遞&gt;給 它的 記憶體中清單晚餐集合:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

我們現在有一個假的IDinnerRepository實現,它不需要資料庫,而是可以處理存儲中晚餐物件清單。

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>將假晚餐儲存庫與單元測試一起使用

讓我們返回到由於資料庫不可用而較早失敗的 DinnersController 單元測試。 我們可以更新測試方法,使用以下代碼將填充在記憶體中晚餐數據樣本的假晚餐存儲庫更新給 DinnersController:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

現在,當我們運行這些測試時,它們都通過了:

![](enable-automated-unit-testing/_static/image11.png)

最重要的是,它們只需一小部分秒才能運行,並且不需要任何複雜的設置/清理邏輯。 我們現在可以單元測試所有我們的 DinnersController 操作方法代碼(包括清單、分頁、詳細資訊、創建、更新和刪除),而無需連接到真正的資料庫。

| **側主題:相依項注入框架** |
| --- |
| 執行手動依賴項注入(如上所示)工作正常,但隨著應用程式中依賴項和元件數量的增加,維護起來確實變得更加困難。 .NET 存在多個依賴項注入框架,可説明提供更多依賴項管理靈活性。 這些框架有時也稱為"控制反轉"(IoC) 容器,它們提供了機制,支援在運行時指定依賴項並將其傳遞給物件(通常使用構造函數注入)的額外配置支援級別。 .NET 中一些較流行的 OSS 依賴項注入 / IOC 框架包括:AutoFac、Ninject、Spring.NET、結構映射和溫莎。 ASP.NET MVC 公開擴展 API,使開發人員能夠參與控制器的解析和實例化,並使依賴項注入/IoC 框架能夠安全地整合到此過程中。 使用 DI/IOC 框架還將使我們能夠從 DinnersController 中刪除預設構造函數 , 這將完全消除它和 DinnerRepository 之間的耦合。 我們不會使用依賴注入/IOC框架與我們的NerdDinner應用程式。 但是,如果NerdDinner代碼庫和功能的增長,我們可以考慮未來的問題。 |

### <a name="creating-edit-action-unit-tests"></a>建立編輯操作儲存單元測試

現在,讓我們創建一些單元測試,以驗證 DinnersController 的編輯功能。 我們將首先測試我們的編輯操作的 HTTP-GET 版本:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

我們將創建一個測試,以驗證在請求有效晚餐時,由 DinnerFormViewModel 物件支援的視圖是否呈現回:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

但是,當我們運行測試時,我們會發現它失敗,因為當 Edit 方法訪問User.Identity.Name屬性以執行 Dinner.Is託管By() 檢查時,將引發一個空引用異常。

控制器基類上的 User 物件封裝有關登錄使用者的詳細資訊,並在執行時創建控制器時由 ASP.NET MVC 填充。 由於我們在 Web 伺服器環境之外測試 DinnersController,所以未設置使用者物件(因此為空引用異常)。

### <a name="mocking-the-useridentityname-property"></a>類比User.Identity.Name屬性

類比框架使我們能夠動態創建支援測試的從屬物件的假版本,從而使測試更容易。 例如,我們可以在"編輯"操作測試中使用類比框架動態創建一個使用者物件,我們的 DinnersController 可用於查找模擬使用者名。 這將避免在運行測試時引發空引用。

有許多 .NET 模擬框架可用於ASP.NET MVC(您可以在此處查看它們[http://www.mockframeworks.com/](http://www.mockframeworks.com/)的清單: 為了測試我們的NerdDinner應用程式,我們將使用一個開源類比框架,稱為"Moq",可以從[http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)免費下載 。

下載後,我們將在NerdDinner.測試專案中向Moq.dll程式集添加參考:

![](enable-automated-unit-testing/_static/image12.png)

然後,我們將向測試類添加「創建 DinnerSControllerA(使用者名)」説明器方法,該方法以使用者名作為參數,然後「類比」DinnersController 實例上的User.Identity.Name屬性:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

上面,我們使用 Moq 創建一個模擬物件,該物件偽造了控制器上下文物件(ASP.NET MVC 傳遞給控制器類以公開運行時物件(如使用者、請求、回應和工作階段)。 我們在 Mock 上調用「setupGet」方法,以指示 ControllerContext 上的HttpContext.User.Identity.Name屬性應返回我們傳遞給幫助器方法的使用者名字符串。

我們可以類比任意數量的控制器上下文屬性和方法。 為了說明這一點,我還為 Request.Is 驗證屬性添加了 SetupGet() 調用(下面測試實際上不需要它,但這有助於說明如何模擬請求屬性)。 完成後,我們將控制器上下文類比的實例分配給 DinnersController,我們的幫助器方法返回。

現在,我們可以編寫使用此幫助器方法測試涉及不同使用者的編輯方案的單位測試:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

現在,當我們運行測試時,他們通過:

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>測試更新模型()方案

我們創建了涵蓋"編輯"操作的 HTTP-GET 版本的測試。 現在,讓我們創建一些測試來驗證編輯操作的 HTTP-POST 版本:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

我們支援此操作方法的有趣新測試方案是它在 Controller 基類上使用 UpdateModel() 幫助器方法。 我們使用此説明器方法將表單發佈值綁定到我們的 Dinner 物件實例。

下面是兩個測試,它們演示如何為 UpdateModel() 幫助器方法提供表單發佈值。 我們將通過創建和填充 FormCollection 物件來執行此操作,然後將其分配給控制器上的"ValueProvider"屬性。

第一個測試驗證在成功保存瀏覽器時是否重定向到詳細資訊操作。 第二個測試驗證,當發佈無效輸入時,操作會再次用錯誤消息重新顯示編輯檢視。

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>測試總結

我們介紹了單元測試控制器類中涉及的核心概念。 我們可以使用這些技術輕鬆創建數百個簡單的測試,以驗證我們應用程式的行為。

由於我們的控制器和模型測試不需要真正的資料庫,因此它們非常快速且易於運行。 我們將能夠在數秒內執行數百個自動測試,並立即獲得反饋,了解我們所做的更改是否違反了某些內容。 這將有助於我們有信心不斷改進、重構和改進我們的應用程式。

我們將測試作為本章的最後一個主題進行介紹,但不是因為測試是您在開發過程結束時應該做的! 相反,您應該在開發過程中儘早編寫自動化測試。 這樣做使您能夠在開發時立即獲得反饋,説明您仔細考慮應用程式的用例方案,並指導您設計應用程式時要牢記乾淨的分層和耦合。

本書的後一章將討論測試驅動開發 (TDD)以及如何將其與 mVC ASP.NET一起使用。 TDD 是一種反覆運算碼實踐,您首先編寫生成的代碼將滿足的測試。 使用 TDD,您首先創建一個測試,以驗證即將實現的功能。 首先編寫單元測試有助於確保您清楚地瞭解該功能及其應該如何工作。 只有在編寫測試(並且已驗證測試失敗)後,您才會實現測試驗證的實際功能。 由於您已經花時間考慮了該功能應該如何工作的用例,因此您將更好地瞭解這些要求以及如何最好地實現這些要求。 完成實現後,您可以重新運行測試,並立即獲得有關該功能是否正常工作的反饋。 我們將在第 10 章中介紹 TDD。

### <a name="next-step"></a>後續步驟

一些最後的總結評論。

> [!div class="step-by-step"]
> [前一個](use-ajax-to-implement-mapping-scenarios.md)
> [下一個](nerddinner-wrap-up.md)
