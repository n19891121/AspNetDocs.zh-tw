---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 附錄：修正 It 範例應用程式 (使用 Azure) 建立真實世界的雲端應用程式 |Microsoft Docs
author: MikeWasson
description: 以 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會解釋13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 549d1513279190ae5abe87c59a48e1caa1cfa5f7
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702929"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>附錄：修正 It 範例應用程式 (使用 Azure) 建立真實世界的雲端應用程式

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> **以 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 它說明13個模式和實務，可協助您成功開發雲端 web 應用程式。 如需電子書的詳細資訊，請參閱 [第一章](introduction.md)。

此附錄適用于使用 Azure 來建立真實世界的雲端應用程式，其中包含下列各節，提供可供您下載的修正程式範例應用程式的其他相關資訊：

- [已知問題](#knownissues)
- [最佳做法](#bestpractices)
- [如何從本機電腦上的 Visual Studio 執行應用程式](#run-in-vs)
- [如何使用 Windows PowerShell 腳本將基礎應用程式部署至 Azure App Service Web Apps](#deploybase)
- [針對 Windows PowerShell 腳本進行疑難排解](#troubleshooting)
- [如何使用佇列處理將應用程式部署至 Azure App Service Web Apps 和 Azure 雲端服務](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>已知問題

最初開發的修正程式是為了說明這種電子書中所顯示的一些模式。 不過，由於電子書是要建立真實世界的應用程式，因此我們會將修正程式碼的程式碼提供給審核和測試程式，就像我們在發行的軟體中所做的一樣。 我們發現了許多問題，並與任何真實世界的應用程式一樣，我們已修正一些問題，而其中有些是延後的版本。

下列清單包含應該在實際執行應用程式中解決的問題，但基於其中一個原因或另一個原因，我們決定不在修正此範例應用程式的初始版本中解決問題。

### <a name="security"></a>安全性

- 確定您無法將工作指派給不存在的擁有者。
- 確定您只能查看和修改您所建立或指派給您的工作。
- 針對登入頁面和驗證 cookie 使用 HTTPS。
- 指定驗證 cookie 的時間限制。

### <a name="input-validation"></a>輸入驗證

一般情況下，生產應用程式會比修正 It 應用程式執行更多輸入驗證。 例如，允許上傳的影像大小/影像檔案大小應受限制。

### <a name="administrator-functionality"></a>系統管理員功能

系統管理員應該能夠變更現有工作的擁有權。 例如，工作建立者可能會離開公司，除非已啟用系統管理存取權，否則不會有任何人具有維護工作的許可權。

### <a name="queue-message-processing"></a>佇列訊息處理

修正 It 應用程式中的佇列訊息處理設計為簡單，以使用最少的程式碼來說明以佇列為中心的工作模式。 這個簡單的程式碼對實際的生產環境應用程式來說並不足夠。

- 程式碼不保證每個佇列訊息最多隻會處理一次。 當您從佇列取得訊息時，有一個超時時間，在此期間內，其他佇列接聽程式不會顯示訊息。 如果在刪除訊息之前超時過期，則會再次顯示訊息。 因此，如果背景工作角色實例花了很長的時間來處理訊息，則理論上可能會有相同的訊息處理兩次，而導致資料庫中有重複的工作。 如需有關此問題的詳細資訊，請參閱 [使用 Azure 儲存體佇列](https://msdn.microsoft.com/library/ff803365.aspx#sec7)。
- 藉由批次處理訊息抓取，佇列輪詢邏輯可能更符合成本效益。 每次您呼叫 [>cloudqueue](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)時，都會產生交易成本。 相反地，您可以呼叫 [>cloudqueue。 GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (記下複數的 ' ) ，以在單一交易中取得多個訊息。 Azure 儲存體佇列的交易成本非常低，因此在大部分的情況下，對成本所造成的影響並不明顯。
- 佇列訊息處理常式代碼中的緊密迴圈會導致 CPU 親和性，而不會有效率地使用多核心 Vm。 更好的設計會使用工作平行處理來平行執行數個非同步工作。
- 佇列訊息處理只有基本的例外狀況處理。 例如，程式碼不會處理 [有害訊息](https://msdn.microsoft.com/library/ms789028.aspx)。  (當訊息處理造成例外狀況時，您必須記錄錯誤並刪除訊息，否則背景工作角色會再次嘗試處理它，而迴圈將會無限期地繼續進行。 ) 

### <a name="sql-queries-are-unbounded"></a>SQL 查詢未系結

目前的修正程式碼不會限制索引頁面的查詢可能傳回的資料列數目。 如果在資料庫中輸入大量的工作，所接收的結果清單大小可能會造成效能問題。 解決方法是執行分頁。 如需範例，請參閱 [使用 ASP.NET MVC 應用程式中的 Entity Framework 進行排序、篩選及分頁](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)。

### <a name="view-models-recommended"></a>建議視圖模型

修正 It 應用程式會使用 FixItTask 實體類別，在控制器與視圖之間傳遞資訊。 最佳做法是使用視圖模型。 領域模型 (例如，FixItTask 實體類別) 是以資料持續性所需的方式來設計，而視圖模型則是針對資料呈現所設計。 如需詳細資訊，請參閱 [12 ASP.NET MVC 最佳作法](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)。

### <a name="secure-image-blob-recommended"></a>建議使用安全映射 blob

修正 It 應用程式會將已上傳的影像儲存為公用，這表示尋找該 URL 的任何人都可以存取影像。 映射可以受到保護，而不是公用。

### <a name="no-powershell-automation-scripts-for-queues"></a>沒有適用于佇列的 PowerShell 自動化腳本

範例 PowerShell 自動化腳本只是針對在 Azure App Service Web Apps 中完整執行的修正程式的基底版本所撰寫。 我們尚未提供用來設定和部署至 web 應用程式的腳本，以及佇列處理所需的雲端服務環境。

### <a name="special-handling-for-html-codes-in-user-input"></a>使用者輸入中的 HTML 程式碼特殊處理

ASP.NET 會在使用者輸入文字方塊中輸入腳本，以防止惡意使用者嘗試跨網站腳本攻擊的許多方式。 而 `DisplayFor` 用來顯示工作標題和附注的 MVC 協助程式，會自動將其傳送至瀏覽器的值進行 HTML 編碼。 但在生產環境應用程式中，您可能會想要採取額外的量值。 如需詳細資訊，請參閱 [ASP.NET 中的要求驗證](https://msdn.microsoft.com/library/hh882339.aspx)。

<a id="bestpractices"></a>
## <a name="best-practices"></a>最佳作法

以下是在程式碼審核和測試原始版本的 Fix It 應用程式中探索到的一些問題。 某些原因是原始編碼員不知道特定的最佳作法，因為程式碼是快速撰寫的，且不適用於發行的軟體。 我們在此列出的問題，是因為我們在此評論和測試中所學到的內容，對於也開發 web 應用程式的其他人可能很有説明。

### <a name="dispose-the-database-repository"></a>處置資料庫儲存機制

`FixItTaskRepository`類別必須處置 Entity Framework `DbContext` 實例。 做法是 `IDisposable` 在類別中執行 `FixItTaskRepository` ：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

請注意，AutoFac 會自動處置 `FixItTaskRepository` 實例，因此我們不需要明確地處置它。

另一個選項是從移除 `DbContext` 成員變數 `FixItTaskRepository` ，並改為在 `DbContext` 語句內的每個儲存機制方法內建立區域變數 `using` 。 例如：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>以 DI 的形式註冊 singleton

因為只 `PhotoService` 需要一個類別和類別的實例 `Logger` ，所以這些類別應該註冊為*DependenciesConfig.cs*中相依性[插入的單一實例](https://code.google.com/p/autofac/wiki/InstanceScope)：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>安全性：不要向使用者顯示錯誤詳細資料

原始的修正 It 應用程式沒有一般錯誤頁面，而且只是讓所有例外狀況反升至 UI，因此一些例外狀況（例如資料庫連接錯誤）可能會導致瀏覽器顯示完整的堆疊追蹤。 詳細的錯誤資訊有時可能會促進惡意使用者的攻擊。 解決方法是記錄例外狀況詳細資料，並向不包含錯誤詳細資料的使用者顯示錯誤頁面。 應用程式已記錄的修正程式，為了顯示錯誤頁面，我們新增 `<customErrors mode=On>` 了 Web.config 檔案中。

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

根據預設，這會導致顯示錯誤的 *Views\Shared\Error.cshtml* 。 您可以自訂 *錯誤. cshtml* 或建立您自己的錯誤網頁檢視，並加入 `defaultRedirect` 屬性。 您也可以針對特定錯誤指定不同的錯誤頁面。

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>安全性：只允許其建立者編輯工作

[儀表板索引] 頁面只會顯示已登入之使用者所建立的工作，但是惡意使用者可以建立一個 URL，其中包含其他使用者工作的識別碼。 我們已在 *DashboardController.cs* 中新增程式碼，以在該情況下傳回404：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>不要忍受例外狀況

原始的修正 It 應用程式在記錄 SQL 查詢所產生的例外狀況之後，只會傳回 null：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

這會讓使用者看起來像是查詢成功，但是沒有傳回任何資料列。 解決方法是在捕捉和記錄之後重新擲回例外狀況：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>攔截背景工作角色中的所有例外狀況

背景工作角色中任何未處理的例外狀況都會導致 VM 回收，因此您想要將您在 try-catch 區塊中所做的一切包裝起來，並處理所有例外狀況。

### <a name="specify-length-for-string-properties-in-entity-classes"></a>在實體類別中指定字串屬性的長度

為了顯示簡單的程式碼，原始版本的 Fix It 應用程式未針對 FixItTask 實體的欄位指定長度，因此它們定義為資料庫中的 Varchar (max) 。 因此，UI 會接受幾乎任何數量的輸入。 指定長度會設定限制，以套用至 web 網頁中的使用者輸入和資料庫中的資料行大小：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>當私用成員未預期變更時，將其標記為唯讀

例如，在類別中， `DashboardController` `FixItTaskRepository` 系統會建立實例，而且不應該變更，因此我們將它定義為 [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx)。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>使用清單。任何 ( # A1 而不是清單。計數 ( # A3 &gt; 0

如果您只在意清單中的一個或多個專案是否符合指定的準則，請使用 [任何](https://msdn.microsoft.com/library/bb534972.aspx) 方法，因為它會在找到符合準則的專案時立即傳回，但 `Count` 方法一律必須逐一查看每個專案。 儀表板 *索引 cshtml* 檔案最初具有下列程式碼：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

我們已將它變更為：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>使用 MVC 協助程式在 MVC 視圖中產生 Url

針對首頁上的 [ **建立修正它** ] 按鈕，修正 it 應用程式硬式編碼錨定元素：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

針對像這樣的視圖/動作連結，最好是使用 [Url。動作](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML helper，例如：

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>使用工作延遲而非執行緒。背景工作角色中的睡眠

新的專案範本會將背景 `Thread.Sleep` 工作角色的範例程式碼放在程式碼中，但造成執行緒的睡眠可能會導致執行緒集區產生其他不必要的執行緒。 您可以使用 [工作] 來避免這種情況，請改用 [ [延遲](https://msdn.microsoft.com/library/hh139096.aspx) ]。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>避免 async void

如果非同步方法不需要傳回值，則傳回型別， `Task` 而不是 `void` 。

這個範例來自 `FixItQueueManager` 類別：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

您只應使用 `async void` 最上層的事件處理常式。 如果您將方法定義為 `async void` ，呼叫端就**await**無法等候方法或攔截方法擲回的任何例外狀況。 如需詳細資訊，請參閱 [非同步程式設計中的最佳做法](https://msdn.microsoft.com/magazine/jj991977.aspx)。

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>使用取消權杖從背景工作角色迴圈中斷

通常，背景工作角色上的 **Run** 方法包含無限迴圈。 當背景工作角色停止時，就會呼叫 [RoleEntryPoint](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) 方法。 您應該使用這個方法來取消在 **Run** 方法內進行的工作並正常結束。 否則，進程可能會在作業中途終止。

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>退出自動 MIME 探查程式

在某些情況下，Internet Explorer 報告的 MIME 類型與 web 伺服器所指定的類型不同。 比方說，如果 Internet Explorer 在以 HTTP 回應標頭 Content-type： text/純文字格式傳遞的檔案中尋找 HTML 內容，Internet Explorer 會判斷內容應轉譯為 HTML。 可惜的是，這種「MIME 探查」也可能會導致裝載不受信任內容之伺服器的安全性問題。 為了對抗這個問題，Internet Explorer 8 對 MIME 型別判斷程式碼進行了一些變更，並讓應用程式開發人員選擇不使用 [mime 探查](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。 下列程式碼已加入 *Web.config* 檔案中。

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>啟用配套和縮制

當 Visual Studio 建立新的 Web 專案時，預設不會啟用 JavaScript 檔案的組合和縮制。 我們在 BundleConfig.cs 中新增了一行程式碼：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>針對驗證 cookie 設定到期時間-時

根據預設，驗證 cookie 會在兩周內到期。 較短的時間更安全。 您可以在 *StartupAuth.cs*中變更此設定：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>如何從本機電腦上的 Visual Studio 執行應用程式

有兩種方式可以執行「修正 It」應用程式：

- 執行基底應用程式，將新的工作直接寫入至 SQL 資料庫。
- 使用佇列加上後端服務來執行應用程式，以建立工作。 佇列模式是以 [佇列為中心的工作模式](queue-centric-work-pattern.md)描述。

<a id="runbase"></a>
### <a name="run-the-base-application"></a>執行基底應用程式

1. 安裝 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。
2. 安裝 [適用于 Visual Studio 的 AZURE SDK for .net](https://azure.microsoft.com/downloads/)。
3. 從 [MSDN 程式碼庫](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)下載 .zip 檔案。
4. 在檔案總管中，以滑鼠右鍵按一下 .zip 檔案，然後按一下 [屬性]，然後在屬性視窗按一下 [解除封鎖]。
5. 解壓縮檔案。
6. 按兩下 .sln 檔案以啟動 Visual Studio。
7. 從 [ **工具** ] 功能表中，按一下 [ **NuGet 封裝管理員**]，然後 **封裝管理員主控台**。
8. 在封裝管理員主控台 (PMC) 中，按一下 [還原]。
9. 結束 Visual Studio。
10. 啟動 [Azure 儲存體模擬器](/azure/storage/common/storage-use-emulator)。
11. 重新開機 Visual Studio，開啟您在上一個步驟中關閉的方案檔。
12. 請確定 FixIt 專案已設定為啟始專案，然後按 CTRL + F5 執行專案。

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>使用佇列處理來執行應用程式

1. 依照指示執行 [基底應用程式](#runbase)，然後關閉瀏覽器並關閉 Visual Studio。
2. 以系統管理員許可權啟動 Visual Studio。  (您將使用 Azure 計算模擬器，而且需要系統管理員許可權。 ) 
3. 在 Web 專案) 的*MyFixIt*專案中，于應用程式*Web.config*檔案 (，將值變更 `appSettings/UseQueues` 為 "true"：

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. 如果 [Azure 儲存體模擬器](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) 仍未執行，請重新開機它。
5. 同時執行 FixIt Web 專案和 MyFixItCloudService 專案。

    使用 Visual Studio：

   1. 按 **F5** 執行 FixIt 專案。
   2. 在**方案總管**中，以滑鼠右鍵按一下 MyFixItCloudService 專案，然後按一下 [ **Debug**  >  **開始新實例**]。

    使用 Visual Studio 2013 Express for Web：

   3. 在方案總管中，以滑鼠右鍵按一下 FixIt 方案，然後選取 [ **屬性**]。
   4. 選取 **多個啟始專案**。
   5. 在 [MyFixIt 和 MyFixItCloudService] 下的 [ **動作** ] 下拉式清單中，選取 [ **啟動**]。
   6. 按一下 [確定]。
   7. 按 **F5** 執行這兩個專案。

      當您執行 MyFixItCloudService 專案時，Visual Studio 會啟動 Azure 計算模擬器。 根據您的防火牆設定，您可能需要允許模擬器通過防火牆。

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>如何使用 Windows PowerShell 腳本將基礎應用程式部署至 Azure App Service Web Apps

為了說明 [自動化所有專案](automate-everything.md) 模式，會在 Azure 中提供可在 Azure 中設定環境的腳本，並將專案部署至新的環境，以修正 It 應用程式。 下列指示說明如何使用腳本。

如果您想要在 Azure 中執行，而不使用佇列，且您已使用佇列在本機執行變更，請務必先將 UseQueues appSetting 值設回 false，再繼續進行下列指示。

這些指示假設您已在本機下載並執行 Fix It 解決方案，且您有 Azure 帳戶，或有您有權管理的 Azure 訂用帳戶。

1. 安裝 **Azure PowerShell** 主控台。 如需指示，請參閱 [如何安裝和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。

    此自訂的主控台已設定為使用您的 Azure 訂用帳戶。 Azure 模組會安裝在 *Program Files* 目錄中，並且會在每次使用 Azure PowerShell 主控台時自動匯入。

    如果您想要使用不同的主機程式，例如 Windows PowerShell ISE，請務必使用 [import-module](https://go.microsoft.com/fwlink/?LinkID=141553) Cmdlet 匯入 azure 模組，或使用 azure 模組中的命令來觸發模組的自動匯入。
2. 使用 [以 **系統管理員身分執行** ] 選項開始 Azure PowerShell。
3. 執行 [ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) Cmdlet，將 Azure PowerShell 執行原則設定為 `RemoteSigned` 。 輸入 [是]) 的 **Y** (完成原則變更。

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    此設定可讓您執行未經過數位簽署的本機腳本。  (您也可以將執行原則設定為 `Unrestricted` ，這樣就不需要稍後解除封鎖步驟，但基於安全性理由，不建議這麼做。 ) 
4. 執行 `Add-AzureAccount` Cmdlet 以設定具有您帳號憑證的 PowerShell。

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    這些認證會在一段時間後過期，您必須重新執行 `Add-AzureAccount` Cmdlet。 在撰寫這本電子書的時候，認證到期前的時間限制為12個小時。
5. 如果您有多個訂用帳戶，請使用 Select-azuresubscription Cmdlet 來指定您要在其中建立測試環境的訂用帳戶。
6. 使用和 Cmdlet 匯入相同 Azure 訂用帳戶的管理 `Get-AzurePublishSettingsFile` 憑證 `Import-AzurePublishSettingsFile` 。 這些 Cmdlet 的第一個會下載憑證檔案，第二個則是指定該檔案的位置，以便匯入該檔案。 > [!IMPORTANT]
   > 將下載的檔案保留在安全的位置，或在您完成時將其刪除，因為其中包含可用來管理 Azure 服務的憑證。

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    憑證會用於偵測開發電腦 IP 位址的 REST API 呼叫，以便在 SQL Database 伺服器上設定防火牆規則。
7. 執行 [設定位置](https://go.microsoft.com/fwlink/p/?linkid=293912) Cmdlet (別名為 `cd` 、 `chdir` 和 `sl`) ，以流覽至包含腳本的目錄。  (它們位於 [修正 It 方案] 資料夾的 [ *自動化* ] 資料夾中。如果目錄名稱包含空格，請 ) 以引號括住路徑。 例如，若要流覽至 `c:\Sample Apps\FixIt\Automation` 目錄，您可以輸入下列命令：

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. 若要允許 Windows PowerShell 執行這些腳本，請使用 [解除封鎖](https://go.microsoft.com/fwlink/p/?linkid=294021) 檔案 Cmdlet。  (腳本被封鎖，因為它們是從網際網路下載的。 ) 

    > [!WARNING]
    > 安全性-在 `Unblock-File` 任何腳本或可執行檔上執行之前，請在 [記事本] 中開啟檔案，檢查命令，並確認它們不包含任何惡意程式碼。

    例如，下列命令會 `Unblock-File` 在目前目錄中的所有腳本上執行 Cmdlet。

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. 若要建立基本的 web 應用程式 (沒有任何佇列處理) 修正它的應用程式，請執行環境建立腳本。

    必要 `Name` 參數會指定資料庫的名稱，也會用於腳本所建立的儲存體帳戶。 名稱在 azurewebsites.net 網域內必須是全域唯一的。 如果您指定的名稱不是唯一的，例如 Fixit 或 Test (，或甚至如同範例中的 fixitdemo) ，則 `New-AzureWebsite` Cmdlet 會失敗，並出現報告衝突的內部錯誤。 腳本會將名稱轉換為全部小寫，以符合 web 應用程式、儲存體帳戶和資料庫的名稱需求。

    必要 `SqlDatabasePassword` 參數會指定將為 SQL Database 建立之系統管理員帳戶的密碼。 請勿在密碼 (中包含特殊 XML 字元 &amp; &lt; &gt; ; ) 。 這是撰寫腳本的方式限制，而不是 Azure 的限制。

    例如，如果您想要建立名為 "fixitdemo" 的 web 應用程式，並使用 "Passw0rd1" SQL Server 系統管理員密碼，您可以輸入下列命令：

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    名稱在 azurewebsites.net 網域中必須是唯一的，而且密碼必須符合密碼複雜度的 SQL Database 需求。  (範例 Passw0rd1 符合需求。 ) 

    請注意，此命令的開頭為 \" ".。。 為了協助防止惡意執行腳本，Windows PowerShell 要求您在執行腳本時提供腳本檔案的完整路徑。 您可以使用點來指出目前目錄 (」。 \") 或提供完整路徑，例如：

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    如需腳本的詳細資訊，請使用 `Get-Help` Cmdlet。

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    您可以使用 `Detailed` `Full` get-help Cmdlet 的、、 `Parameters` 和 `Examples` 參數來篩選傳回的說明。

    如果腳本失敗或產生錯誤，例如 "AzureWebsite： Call Set-Select-azuresubscription and Select-azuresubscription first"，您可能還未完成 Azure PowerShell 的設定。

    腳本完成後，您可以使用 Azure 管理入口網站查看已建立的資源，如「 [自動化所有專案](automate-everything.md) 」一章所示。
10. 若要將 FixIt 專案部署到新的 Azure 環境，請使用 *AzureWebsite.ps1* 腳本。 例如：

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    部署完成時，瀏覽器會開啟，並修正在 Azure 中執行的瀏覽器。

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>針對 Windows PowerShell 腳本進行疑難排解

執行這些腳本時，最常遇到的錯誤與許可權相關。 確定 `Add-AzureAccount` `Import-AzurePublishSettingsFile` 已成功，且您已在相同的 Azure 訂用帳戶中使用它們。 即使 `Add-AzureAccount` 成功，您也可能必須再次執行。 新增的許可權會 `Add-AzureAccount` 在12小時內過期。

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>物件參考未設定成物件的執行個體。

如果腳本傳回錯誤，例如「物件參考未設定為物件的實例」，這表示 Windows PowerShell 找不到要處理的物件 (這是) 的 null 參考例外狀況，請執行 `Add-AzureAccount` Cmdlet，然後再試一次腳本。

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError：伺服器發生內部錯誤。

`New-AzureWebsite`當 azurewebsites.net 網域中的名稱不是唯一時，此 Cmdlet 會傳回內部錯誤。 若要解決此錯誤，請使用不同的名稱值，其位於 *New-AzureWebsiteEnv.ps1*的 name 參數中。

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>重新開機腳本

如果您需要重新開機 *New-AzureWebsiteEnv.ps1* 腳本，因為它在列印「腳本已完成」訊息之前失敗，您可能會想要刪除腳本停止之前所建立的資源。 例如，如果腳本已建立 ContosoFixItDemo web 應用程式，而您使用相同的名稱再次執行腳本，腳本將會失敗，因為該名稱已在使用中。

若要判斷腳本停止之前建立的資源，請使用下列 Cmdlet：

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`：若要執行此 Cmdlet，請透過管道將資料庫伺服器名稱傳送至 `Get-AzureSqlDatabase` ：   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

若要刪除這些資源，請使用下列命令。 請注意，如果您刪除資料庫伺服器，就會自動刪除與伺服器相關聯的資料庫。

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>如何使用佇列處理將應用程式部署至 Azure App Service Web Apps 和 Azure 雲端服務

若要啟用佇列，請在 MyFixIt\Web.config 檔案中進行下列變更。 在底下 `appSettings` ，將的值變更 `UseQueues` 為 "true"：

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

然後將 MVC 應用程式部署至 Azure App Service 中的 web 應用程式，如 [先前](#deploybase)所述。

接著，建立新的 Azure 雲端服務。 Fix It 應用程式隨附的腳本不會建立或部署雲端服務，因此您必須使用 Azure 入口網站。 在入口網站中，按一下 [**新增**  --  **計算**–**雲端服務**  --  **快速建立**]，然後輸入 URL 和資料中心位置。 使用您用來部署 web 應用程式的相同資料中心。

![](the-fix-it-sample-application/_static/image1.png)

部署雲端服務之前，您必須先更新一些設定檔。

在 MyFixIt.WorkerRole\app.config 的下方 `connectionStrings` ，將連接字串的值取代 `appdb` 為 SQL Database 的實際連接字串。 您可以從入口網站取得連接字串。 在入口網站中，按一下 [ **SQL 資料庫**]  -  **appdb**  -  **View SQL Database ADO .net、ODBC、PHP 和 JDBC 的連接字串**。 複製 ADO.NET 連接字串，並將值貼到 app.config 檔案中。 \_以您的資料庫密碼取代 "{您的密碼在 \_ 這裡}"。  (假設您使用腳本來部署 MVC 應用程式，則在腳本參數中指定了資料庫密碼 `SqlDatabasePassword` 。 ) 

結果看起來應該如下所示：

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

在相同的 MyFixIt.WorkerRole\app.config 檔案中，于底下的 [ `appSettings` Azure 儲存體帳戶] 中，取代兩個預留位置值。

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

您可以從入口網站取得存取金鑰。 請參閱 [如何管理儲存體帳戶](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)。

在 MyFixItCloudService\ServiceConfiguration.Cloud.cscfg 中，將相同的兩個預留位置值取代為 Azure 儲存體帳戶。

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

現在您已準備好部署雲端服務。 在 [方案探索] 中，以滑鼠右鍵按一下 [MyFixItCloudService] 專案，然後選取 [ **發行**]。 如需詳細資訊，請參閱[本教學](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)課程的第2部分中的「將[應用程式部署至 Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)」。

> [!div class="step-by-step"]
> [[上一步]](more-patterns-and-guidance.md)
