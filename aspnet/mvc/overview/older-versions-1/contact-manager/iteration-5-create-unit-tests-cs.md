---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
title: 反覆運算#5 = 創建單元測試 (C#) |微軟文件
author: rick-anderson
description: 在第五次反覆運算中,我們通過添加單元測試使應用程式更易於維護和修改。 我們模擬我們的資料模型類,並為 o...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 28ad8f80-b8a5-444e-b478-8b15a846060c
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
msc.type: authoredcontent
ms.openlocfilehash: c005a8ffc3b09c126d796f2feb74d402cb784aa2
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542348"
---
# <a name="iteration-5--create-unit-tests-c"></a>反覆項目 #5 – 建立單元測試 (C#)

由[微軟](https://github.com/microsoft)

[下載代碼](iteration-5-create-unit-tests-cs/_static/contactmanager_5_cs1.zip)

> 在第五次反覆運算中,我們通過添加單元測試使應用程式更易於維護和修改。 我們類比數據模型類,並為控制器和驗證邏輯構建單元測試。

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>編譯聯絡人管理ASP.NET MVC 應用程式 (C#)

在本系列教程中,我們從頭到尾構建整個聯繫人管理應用程式。 透過聯絡人管理員應用程式,您可以儲存連絡人資訊 (姓名、電話號碼和電子郵件位址) 人員清單。

我們通過多次反覆運算構建應用程式。 每次反覆運算時,我們都會逐步改進應用程式。 此多反覆運算方法的目標是使您能夠瞭解每次更改的原因。

- 反覆運算#1 - 創建應用程式。 在第一次反覆運算中,我們以最簡單的方式創建聯繫人管理器。 我們添加對基本資料庫操作的支援:創建、讀取、更新和刪除 (CRUD)。

- 反覆運算#2 - 使應用程式看起來不錯。 在此反覆運算中,我們通過修改預設ASP.NET MVC 檢視母版頁和級聯樣式表來改進應用程式的外觀。

- 反覆運算#3 - 添加表單驗證。 在第三個反覆運算中,我們添加基本表單驗證。 我們防止人們在未填寫所需表單欄位的情況下提交表單。 我們還驗證電子郵件地址和電話號碼。

- 反覆運算#4 - 使應用程式鬆散耦合。 在第四次反覆運算中,我們利用多種軟體設計模式,使維護和修改聯繫人管理器應用程式變得更加容易。 例如,我們重構應用程式以使用存儲庫模式和依賴項注入模式。

- 反覆運算#5 - 創建單元測試。 在第五次反覆運算中,我們通過添加單元測試使應用程式更易於維護和修改。 我們類比數據模型類,並為控制器和驗證邏輯構建單元測試。

- 反覆運算#6 - 使用測試驅動開發。 在第六次反覆運算中,我們首先編寫單元測試並針對單元測試編寫代碼,從而向應用程式添加新功能。 在此反覆運算中,我們添加聯繫人組。

- 反覆運算#7 - 添加Ajax功能。 在第七次反覆運算中,我們通過增加對Ajax的支援來提高應用程式的回應性和性能。

## <a name="this-iteration"></a>此反覆運算

在 Contact Manager 應用程式的上一次反覆運算中,我們將應用程式重構為更鬆散耦合。 我們將應用程式劃分為不同的控制器、服務和存儲庫層。 每個層通過介面與層交互。

我們重構了應用程式,使應用程式更易於維護和修改。 例如,如果需要使用新的數據存取技術,我們可以簡單地更改儲存庫層而不接觸控制器或服務層。 通過使聯繫人管理器鬆散耦合,我們使應用程式對更改更具彈性。

但是,當我們需要向聯繫人管理器應用程式添加新功能時,會發生什麼情況? 或者,當我們修復 Bug 時會發生什麼情況? 編寫代碼的可悲但經過充分驗證的事實是,每當您觸控程式碼時,都會產生引入新 Bug 的風險。

例如,一天好,您的經理可能會要求您向聯繫人管理器添加新功能。 她希望您添加對聯繫人組的支援。 她希望您允許使用者將聯繫人組織成"朋友"、"業務"等組。

為了實現此新功能,您需要修改聯繫人管理器應用程式的所有三個層。 您需要向控制器、服務層和儲存庫添加新功能。 一旦開始修改代碼,您就可能會破壞以前起作用的功能。

像上次反覆運算中所做的那樣,將應用程式重構為單獨的層是一件好事。 這是一件好事,因為它使我們能夠對整個層進行更改,而無需接觸應用程式的其餘部分。 但是,如果要使層中的代碼更易於維護和修改,則需要為代碼創建單元測試。

使用單元測試來測試單個代碼單元。 這些代碼單位小於整個應用程式層。 通常,使用單元測試來驗證代碼中的特定方法的行為方式是否達到預期。 例如,您將為 ContactManager 服務類公開的 CreateContact() 方法創建單元測試。

應用程式單元測試工作就像安全網一樣。 每當修改應用程式中的代碼時,都可以運行一組單元測試,以檢查修改是否破壞了現有功能。 單元測試使代碼可以安全地修改。 單元測試使應用程式中的所有代碼都更具更改的彈性。

在此反覆運算中,我們將單元測試添加到我們的聯繫人管理器應用程式中。 這樣,在下一次反覆運算中,我們可以將聯繫人組添加到我們的應用程式中,而不必擔心破壞現有功能。

> [!NOTE] 
> 
> 有多種單元測試框架,包括 NUnit、xUnit.net 和 MbUnit。 在本教學中,我們使用 Visual Studio 附帶的單位測試框架。 但是,您可以同樣輕鬆地使用這些替代框架之一。

## <a name="what-gets-tested"></a>測試內容

在理想情況下,所有代碼都將由單元測試覆蓋。 在完美的世界,你會有完美的安全網。 您將能夠修改應用程式中的任何代碼行,並通過執行單元測試立即知道更改是否中斷了現有功能。

然而,我們並不生活在一個完美的世界。 實際上,在編寫單元測試時,您專注於為業務邏輯編寫測試(例如,驗證邏輯)。 特別是,您*不會*為數據訪問邏輯或視圖邏輯編寫單元測試。

為了有用,單元測試必須非常快速地執行。 您可以輕鬆地為應用程式累積數百(甚至數千個)單元測試。 如果單元測試需要很長時間才能運行,則可以避免執行它們。 換句話說,對於日常編碼目的,長時間運行單元測試是無用的。

因此,您通常不會為與資料庫互動的代碼編寫單元測試。 對即時資料庫運行數百個單元測試將太慢。 相反,您模擬資料庫並編寫與模擬資料庫交互的代碼(我們討論下面嘲笑資料庫)。

出於類似的原因,您通常不會為檢視編寫單元測試。 為了測試檢視,必須啟動 Web 伺服器。 由於旋轉 Web 伺服器是一個相對緩慢的過程,因此不建議為檢視創建單元測試。

如果檢視包含複雜的邏輯,則應考慮將邏輯移動到説明程式方法中。 您可以為在不旋轉 Web 伺服器的情況下執行的 Helper 方法編寫單元測試。

> [!NOTE] 
> 
> 雖然編寫數據訪問邏輯或視圖邏輯的測試在編寫單元測試時不是個好主意,但這些測試在構建功能或集成測試時可能非常有價值。

> [!NOTE] 
> 
> ASP.NET MVC 是 Web 窗體檢視引擎。 雖然 Web 窗體檢視引擎依賴於 Web 伺服器,但其他檢視引擎可能不是。

## <a name="using-a-mock-object-framework"></a>使用模擬物件框架

構建單元測試時,您幾乎總是需要利用類比物件框架。 類比物件框架使您能夠為應用程式中的類創建類比和存根。

例如,可以使用 Mock Object 框架生成儲存庫類的類比版本。 這樣,您可以在單元測試中使用類比存儲庫類而不是真正的存儲庫類。 使用類比儲存庫使您能夠在執行單元測試時避免執行資料庫代碼。

可視化工作室不包括類比物件框架。 但是,有幾種商業和開源模擬物件框架可用於 .NET 框架:

1. Moq - 此框架在開源 BSD 許可證下可用。 你可以從[https://code.google.com/p/moq/](https://code.google.com/p/moq/)下載莫克。
2. 犀牛類比 - 此框架可在開源 BSD 許可證下提供。 你可以從[http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)下載犀牛類比。
3. 類型隔離器 - 這是一個商業框架。 可以從 下載試用[http://www.typemock.com/](http://www.typemock.com/)版 。

在本教學中,我決定使用 Moq。 但是,您可以同樣輕鬆地使用 Rhino Mocks 或 Typemock 隔離器為聯絡人管理器應用程式創建 Mock 物件。

在使用 Moq 之前,您需要完成以下步驟:

1. .
2. 在解壓縮下載之前,請確保右鍵按一下檔並按下標記為 **「取消阻止」** 的按鈕(參見圖 1)。
3. 解壓縮下載。
4. 通過右鍵按一下 ContactManager 中的「引用」資料夾並選擇 **「添加引用**」,添加對 Moq 程式集的引用。 在「瀏覽」選項卡下,瀏覽到解壓縮 Moq 的資料夾,然後選擇 Moq.dll 程式集。 按一下 [確定]**** 按鈕。
5. 完成這些步驟后,參考文件應類似於圖 2。

[![解除阻止莫克](iteration-5-create-unit-tests-cs/_static/image1.jpg)](iteration-5-create-unit-tests-cs/_static/image1.png)

**圖 01**: 取消封鎖 Moq([按下以檢視全尺寸影像](iteration-5-create-unit-tests-cs/_static/image2.png))

[![新增 Moq 後的參考](iteration-5-create-unit-tests-cs/_static/image2.jpg)](iteration-5-create-unit-tests-cs/_static/image3.png)

**圖 02**: 新增 Moq([按下以檢視全尺寸影像](iteration-5-create-unit-tests-cs/_static/image4.png))後的參考

## <a name="creating-unit-tests-for-the-service-layer"></a>為服務層建立單元測試

讓我們首先為聯繫人管理器應用程式的服務層創建一組單元測試。 我們將使用這些測試來驗證我們的驗證邏輯。

在 ContactManager.測試項目中創建名為" 模型" 的新資料夾。 接下來,右鍵按兩下"模型"資料夾並選擇 **「添加、新建測試**」。 將顯示圖 3 所示**的「添加新測試**」對話方塊。 選擇 **「單元測試」** 樣本並命名新測試ContactManager ServiceTest.cs。 按下 **「確定」** 按鈕將新測試添加到測試專案。

> [!NOTE] 
> 
> 通常,您希望測試項目的資料夾結構與 ASP.NET MVC 專案的資料夾結構匹配。 例如,將控制器測試放在控制器資料夾中,在模型資料夾中放置模型測試,等等。

[![型號_連絡管理員服務測試.cs](iteration-5-create-unit-tests-cs/_static/image3.jpg)](iteration-5-create-unit-tests-cs/_static/image5.png)

**圖 03**:型號_ContactManagerServiceTest.cs([按下以檢視全尺寸影像](iteration-5-create-unit-tests-cs/_static/image6.png))

最初,我們要測試 ContactManager 服務類公開的 CreateContact() 方法。 我們將建立以下五個測試:

- 創建聯絡人() - 當有效的聯繫人傳遞給方法時,創建聯繫人() 的測試返回該值為 true。
- 創建聯絡人需要先名() - 測試當缺少名字的聯繫人傳遞給 CreateContact() 方法時,錯誤訊息是否添加到模型狀態。
- 創建聯絡人需要LastName() - 測試當缺少姓氏的聯絡人傳遞給 CreateContact() 方法時,將錯誤消息添加到模型狀態。
- 建立聯絡人無效電話() - 測試當電話號碼無效的聯繫人傳遞給 CreateContact() 方法時,錯誤訊息是否添加到模型狀態。
- 創建聯絡人無效電子郵件() - 測試當具有無效電子郵件地址的連絡人傳遞給 CreateContact() 方法時,錯誤訊息是否添加到模型狀態。

第一個測試驗證有效的聯繫人未生成驗證錯誤。 其餘的測試檢查每個驗證規則。

這些測試的代碼包含在清單 1 中。

**清單1 - 型號_聯繫管理員服務測試.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample1.cs)]

由於我們使用清單 1 中的 Contact 類,因此我們需要將對 Microsoft 實體框架的引用添加到我們的測試專案中。 添加對系統.Data.實體程式集的引用。

清單1包含一個名為初始化()的方法,該方法用 [測試初始化] 屬性進行修飾。 在運行每個單元測試之前自動調用此方法(在每個單元測試之前調用此方法 5 次)。 初始化()方法建立具有以下代碼行的模擬儲存庫:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample2.cs)]

此代碼行使用 Moq 框架從 IContactManagerRepository 介面生成類比儲存庫。 使用類比儲存庫而不是實際的實體聯繫人管理器儲存庫,以避免在運行每個單元測試時訪問資料庫。 類比儲存庫實現 IContactManagerRepository 介面的方法,但這些方法實際上不執行任何操作。

> [!NOTE] 
> 
> 使用 Moq 框架時,mockRepository 和\_\_mockRepository.Object 區別是有區別的。 前者是指類&lt;比 IContactManagerManagerRepository&gt;類,該類包含用於指定類比儲存庫如何執行的方法。 後者是指實現 IContactManager 儲存庫介面的實際類比儲存庫。

創建 ContactManagerService 類的實例時,類比儲存庫在初始化() 方法中使用。 所有單獨的單元測試都使用此聯繫人管理器服務類的此實例。

清單1包含與每個單元測試對應的五種方法。 這些方法中的每一個都用 [TestMethod] 屬性進行修飾。 運行單元測試時,將調用具有此屬性的任何方法。 換句話說,使用 [TestMethod] 屬性修飾的任何方法都是單元測試。

第一個單元測試名為 CreateContact(),驗證在將 Contact 類的有效實例傳遞給該方法時調用 CreateContact() 傳回該值為 true。 測試創建 Contact 類的實例,調用 CreateContact() 方法,並驗證 CreateContact() 傳回該值為 true。

其餘測試驗證當使用無效的 Contact 呼叫 CreateContact() 方法時,該方法將返回 false,並且預期的驗證錯誤訊息將添加到模型狀態。 例如,"創建連絡人需求名稱()「測試將創建聯繫人類的實例,該類的 FirstName 屬性具有空字串。 接下來,使用無效的聯繫人調用 CreateContact() 方法。 最後,測試驗證 CreateContact() 傳回 false,並且模型狀態包含預期的驗證錯誤訊息" 需要名字。

您可以通過選擇功能表選項 **「測試」、「執行」、「解決方案中的所有測試」(CTRL+R、A)** 來在清單 1 中執行單元測試。 測試結果顯示在「測試結果」視窗中(參見圖 4)。

[![測試結果](iteration-5-create-unit-tests-cs/_static/image4.jpg)](iteration-5-create-unit-tests-cs/_static/image7.png)

**圖 04**: 測試結果 ([按下以檢視全尺寸影像](iteration-5-create-unit-tests-cs/_static/image8.png))

## <a name="creating-unit-tests-for-controllers"></a>為控制器建立單元測試

ASP.NETMVC 應用程式控制使用者互動流。 測試控制器時,要測試控制器是否返回正確的操作結果並查看數據。 您可能還希望測試控制器是否與模型類以預期的方式交互。

例如,清單 2 包含聯絡人控制器 Create() 方法的兩個單元測試。 第一個單元測試驗證當有效的聯繫人傳遞到 Create() 方法時,Create() 方法重定向到 Index 操作。 換句話說,當傳遞有效的聯繫人時,Create() 方法應返回表示索引操作的重定向到RouteResult。

在測試控制器層時,我們不想測試 ContactManager 服務層。 因此,我們在初始化方法中使用以下代碼模擬服務層:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample3.cs)]

在 CreateValidContact() 單元測試中,我們用以下代碼行模擬呼叫服務層 CreateContact() 方法的行為:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample4.cs)]

此代碼行在調用其 CreateContact() 方法時,會導致類比 ContactManager 服務返回該值 true。 通過類比服務層,我們可以測試控制器的行為,而無需在服務層中執行任何代碼。

第二個單元測試驗證 Create() 操作在將無效聯繫人傳遞給方法時是否返回"創建"視圖。 我們使服務層 CreateContact() 方法使用以下代碼行傳回錯誤值:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample5.cs)]

如果 Create() 方法按預期方式進行,則當服務層返回值為 false 時,它應返回"創建"視圖。 這樣,控制器可以在"創建"視圖中顯示驗證錯誤消息,並且使用者有機會更正無效的"連絡人"屬性。

如果計劃為控制器生成單元測試,則需要從控制器操作中返回顯式視圖名稱。 例如,不要返回如下所示的視圖:

返回視圖();

相反,返回檢視如下所示:

返回視圖("創建");

如果在返回檢視時不是顯式,則ViewResult.ViewName 屬性將返回一個空字串。

**清單2 - 控制器\連絡控制器測試.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample6.cs)]

## <a name="summary"></a>總結

在此反覆運算中,我們為聯繫人管理器應用程式創建了單元測試。 我們可以隨時運行這些單元測試,以驗證我們的應用程式是否仍按預期方式運行。 單元測試作為我們應用程式的安全網,使我們能夠在未來安全地修改我們的應用程式。

我們創建了兩組單元測試。 首先,我們通過為服務層創建單元測試來測試驗證邏輯。 接下來,我們通過為控制器層創建單元測試來測試流量控制邏輯。 在測試服務層時,我們通過類比存儲庫層將服務層的測試與存儲庫層隔離開來。 測試控制器層時,我們通過類比服務層來隔離控制器層的測試。

在下一次反覆運算中,我們修改聯繫人管理器應用程式,以便它支援連絡人組。 我們將使用稱為測試驅動開發的軟體設計過程將這項新功能添加到我們的應用程式中。

> [!div class="step-by-step"]
> [前一個](iteration-4-make-the-application-loosely-coupled-cs.md)
> [下一個](iteration-6-use-test-driven-development-cs.md)
