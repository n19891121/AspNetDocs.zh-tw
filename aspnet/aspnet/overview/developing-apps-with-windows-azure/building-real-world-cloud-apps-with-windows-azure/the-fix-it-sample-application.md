---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: '附錄: 修復它範例應用程式(使用 Azure 構建真實世界的雲端應用程式) |微軟文件'
author: MikeWasson
description: 使用 Azure 電子書建構真實世界雲端應用基於 Scott Guthrie 開發的演示文稿。 它解釋了13種模式和做法,他可以...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675989"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>附錄:修復它範例應用程式(使用 Azure 建構真實世界的雲端應用程式)

由[邁克·瓦森](https://github.com/MikeWasson),[里克·安德森](https://twitter.com/RickAndMSFT),[湯姆·戴克斯特拉](https://github.com/tdykstra)

[下載修復項目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> 使用 Azure 電子書**建構真實世界雲端應用**基於 Scott Guthrie 開發的演示文稿。 它解釋了 13 種模式和做法,這些模式和做法可以説明您成功開發雲端的 Web 應用。 有關電子書的資訊,請參閱[第一章](introduction.md)。

使用 Azure 電子書建構真實世界雲端應用的此附錄包含以下部分,這些部分提供有關「修復它」範例應用程式的其他資訊,您可以下載:

- [已知問題](#knownissues)
- [最佳作法](#bestpractices)
- [如何從本地電腦上的 Visual Studio 執行應用](#run-in-vs)
- [如何使用 Windows PowerShell 文稿將基本應用部署到 Azure 應用服務 Web 應用](#deploybase)
- [對 Windows 電源外殼文稿進行故障排除](#troubleshooting)
- [如何將具有佇列處理的應用部署到 Azure 應用服務 Web 應用和 Azure 雲端服務](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>已知問題

Fix It 應用程式最初是為了盡可能簡單地說明本電子書中介紹的一些模式而開發的。 但是,由於電子書是關於構建真實世界的應用程式,因此我們進行了修復 It 代碼的審核和測試過程,類似於我們為發佈軟體所做的操作。 我們發現了一些問題,與任何實際應用程式一樣,我們修復了其中一些問題,其中一些問題被推遲到以後的版本中。

以下清單包括應在生產應用程式中解決的問題,但由於以下原因,我們決定在 Fix It 範例應用程式的初始版本中不解決。

### <a name="security"></a>安全性

- 確保無法將任務分配給不存在的擁有者。
- 確保只能查看和修改您創建或分配給您的任務。
- 將 HTTPS 用於登錄頁面和身份驗證 Cookie。
- 指定身份驗證 Cookie 的時間限制。

### <a name="input-validation"></a>輸入驗證

通常,生產應用執行比修復它應用更多的輸入驗證。 例如,允許上載的圖像大小/圖像檔大小應加以限制。

### <a name="administrator-functionality"></a>管理員功能

管理員應該能夠更改現有任務的擁有權。 例如,任務的建立者可能會離開公司,除非啟用了管理訪問,否則任何人都無權維護該任務。

### <a name="queue-message-processing"></a>佇列訊息處理

修復 It 應用中的佇列消息處理設計為簡單,以便用最少的代碼來說明以隊列為中心的工作模式。 此簡單代碼不足以用於實際生產應用程式。

- 該代碼不保證最多處理一次每個佇列消息。 當您從佇列中收到消息時,有一個超時期間,在此期間消息對其他佇列偵聽器不可見。 如果超時在刪除郵件之前過期,則消息將再次可見。 因此,如果輔助角色實例花費很長時間來處理消息,則從理論上講,同一消息可以處理兩次,從而導致資料庫中出現重複的任務。 有關此問題的詳細資訊,請參閱[使用 Azure 儲存佇列](https://msdn.microsoft.com/library/ff803365.aspx#sec7)。
- 通過批處理消息檢索,佇列輪詢邏輯可能更具成本效益。 每次調用[CloudQueue.GetMessageasync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)時,都會有一個交易成本。 相反,您可以調用[CloudQueue.GetMessagesAsync(](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx)請注意複數""),在單個事務中獲取多條消息。 Azure 儲存佇列的事務成本非常低,因此在大多數情況下,對成本的影響並不大。
- 佇列消息處理代碼中的緊密迴圈會導致 CPU 關聯性,而 CPU 關聯性不會有效地利用多核 VM。 更好的設計將使用任務並行性並行運行多個非同步任務。
- 佇列消息處理只有基本的異常處理。 例如,程式碼不處理[有害訊息](https://msdn.microsoft.com/library/ms789028.aspx)。 (當消息處理導致異常時,您必須記錄錯誤並刪除消息,否則輔助角色將再次嘗試處理該錯誤,並且迴圈將無限期地繼續。

### <a name="sql-queries-are-unbounded"></a>SQL 查詢未繫結

當前修復代碼對索引頁的查詢可能返回的行數沒有限制。 如果資料庫中輸入了大量任務,則接收的結果清單的大小可能會導致性能問題。 解決方案是實現分頁。 例如,請參閱在[ASP.NET mVC 應用程式中使用實體框架對實體框架進行排序、篩選和分頁](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)。

### <a name="view-models-recommended"></a>檢視推薦的模型

修復它應用使用 FixItTask 實體類在控制器和檢視之間傳遞資訊。 最佳做法是使用視圖模型。 域模型(例如 FixItTask 實體類)是圍繞數據持久性所需的內容設計的,而視圖模型可以設計為數據表示。 有關詳細資訊,請參閱[12 ASP.NET MVC 最佳實務](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)。

### <a name="secure-image-blob-recommended"></a>建議使用安全映像 blob

Fix It 應用將上傳的圖像存儲為公共圖像,這意味著找到 URL 的任何人都可以訪問這些圖像。 圖像可以保護而不是公開。

### <a name="no-powershell-automation-scripts-for-queues"></a>沒有在佇列的 PowerShell 自動化文稿

示例 PowerShell 自動化文本僅針對完全在 Azure 應用服務 Web 應用中運行的修復它的基本版本編寫。 我們沒有提供用於設置和部署到 Web 應用以及佇列處理所需的雲端服務環境的腳本。

### <a name="special-handling-for-html-codes-in-user-input"></a>使用者輸入 HTML 代碼的特殊處理

ASP.NET通過在使用者輸入文本框中輸入腳本,自動防止惡意用戶嘗試跨網站腳本攻擊的多種方式。 MVC`DisplayFor`幫助程式用於顯示任務標題和註釋,自動對其進行 HTML 編碼它發送到瀏覽器的值。 但在生產應用中,您可能需要採取其他措施。 有關詳細資訊,請參閱ASP.NET[中的要求驗證](https://msdn.microsoft.com/library/hh882339.aspx)。

<a id="bestpractices"></a>
## <a name="best-practices"></a>最佳作法

以下是在修復 It 應用的原始版本的代碼審查和測試中發現后修復的一些問題。 有些是由於原始編碼器不知道特定的最佳實踐造成的,有些只是因為代碼編寫得很快,並非針對發佈的軟體。 我們在這裡列出問題,以防我們從這次審查和測試中學到的東西對正在開發 Web 應用程式的其他人有説明。

### <a name="dispose-the-database-repository"></a>處置資料庫儲存庫

類`FixItTaskRepository`必須釋放實體框架`DbContext`實例。 我們通過在`FixItTaskRepository`類中`IDisposable`實現 來實現此情況:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

請注意,AutoFac 將自動`FixItTaskRepository`釋放 實例,因此我們不需要顯式處置它。

另一個選項是從 中`DbContext`刪除成員變數`FixItTaskRepository`,而是在語句內在`DbContext`每個 儲存庫方法中創建`using`一個局部變數。 例如：

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>使用 DI 註冊單例

由於只需要`PhotoService`類`Logger`和 類的一個實例,因此這些類應註冊為*DependenciesConfig.cs*[中依賴項注入的單個實例](https://code.google.com/p/autofac/wiki/InstanceScope):

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>安全性:不向使用者顯示錯誤詳細資訊

原始修復 It 應用沒有通用錯誤頁,只是讓所有異常都冒泡到 UI 上,因此某些異常(如資料庫連接錯誤)可能會導致向瀏覽器顯示完整的堆疊跟蹤。 詳細的錯誤信息有時可能促進惡意用戶的攻擊。 解決方案是記錄異常詳細資訊,並將錯誤頁顯示給不包含錯誤詳細資訊的使用者。 修復它應用已經記錄,為了顯示錯誤頁面,我們添加了`<customErrors mode=On>`Web.config 檔。

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

默認情況下,這將導致*顯示檢視\共用\Error.cshtml*以查找錯誤。 您可以自訂*Error.cshtml*或創建自己的錯誤頁面檢視並`defaultRedirect`添加 屬性。 您還可以為特定錯誤指定不同的錯誤頁。

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>安全性:僅允許其建立者編輯工作

"儀錶板索引"頁僅顯示登錄使用者創建的任務,但惡意使用者可以創建具有其他使用者任務的 ID 的 URL。 我們*DashboardController.cs 中*添加了代碼,以在這種情況下返回 404:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>不要吞咽異常

原始修復 It 應用程式在紀錄 SQL 查詢產生的例外後剛剛傳回 null:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

這將使用戶看起來好像查詢成功,但只是沒有返回任何行。 解決方案是在捕獲和日誌記錄後重新引發異常:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>擷取輔助角色中的所有例外

輔助角色中的任何未處理異常都將導致 VM 被回收,因此您希望在 try-catch 塊中包裝所有操作,並處理所有異常。

### <a name="specify-length-for-string-properties-in-entity-classes"></a>指定實體類別的字串屬性的長度

為了顯示簡單代碼,修復它應用的原始版本沒有指定 FixItTask 實體欄位的長度,因此在資料庫中將其定義為 varchar(max)。 因此,UI 將接受幾乎任何數量的輸入。 指定長度設定適用於網頁中的使用者輸入和資料庫中的欄大小的限制:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>當私人成員不需要更改時,將它們標記為唯讀

例如,在類中`DashboardController`,將`FixItTaskRepository`建立一個實例,並且不需要更改,所以我們將其定義為[唯讀](https://msdn.microsoft.com/library/acdd6hb7.aspx)。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>使用清單。任何()而不是清單。計數() &gt; 0

如果您所關心的只是清單中的一個或多個項是否符合指定的條件,請使用[Any](https://msdn.microsoft.com/library/bb534972.aspx)方法,因為它在找到符合條件的項後立即返回`Count`,而 該方法始終必須遍遍遍每個項。 儀表板*索引.cshtml*檔案最初具有以下代碼:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

我們將其更改為:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>使用 MVC 說明器在 MVC 檢視中產生網址

對於主頁上的「**修復 It」** 按鈕,「修復它」應用硬編碼錨點元素:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

對於像這樣的檢視/操作連結,最好使用[網址.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 幫助程式,例如:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>使用任務.延遲而不是線程.睡眠在輔助角色中

新專案範本將工作角色的範例`Thread.Sleep`代碼放入其中,但導致線程處於睡眠狀態可能會導致線程池生成其他不必要的線程。 您可以使用[Task.delay](https://msdn.microsoft.com/library/hh139096.aspx)來避免這種情況。

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>避免非空隙

如果非同步方法不需要傳回值,則傳`Task`回`void`類型 而不是 。

這個範例來自類別`FixItQueueManager`:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

應僅對`async void`頂級事件處理程式使用。 如果將方法定義為`async void`,調用方無法**等待**該方法或捕獲方法引發的任何異常。 有關詳細資訊,請參閱[非同步編程中的最佳做法](https://msdn.microsoft.com/magazine/jj991977.aspx)。

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>使用取消權杖從輔助角色循環中斷

通常,輔助角色上的**Run**方法包含無限迴圈。 當輔助角色停止時,將調用[角色入口點.onStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)方法。 應使用此方法取消在**Run**方法內完成的工作並正常退出。 否則,進程可能在操作過程中終止。

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>選擇宣告自動 MIME 嗅探程序

在某些情況下,Internet Explorer 報告 MIME 類型與 Web 伺服器指定的類型不同。 例如,如果 Internet Explorer 在使用 HTTP 回應標頭內容類型:文本/純文交付的檔中尋找 HTML 內容,則 Internet Explorer 確定內容應呈現為 HTML。 遺憾的是,這種"MIME嗅探"還可能導致託管不受信任的內容的伺服器出現安全問題。 為了解決這個問題,Internet Explorer 8 對 MIME 類型的確定代碼進行了一些更改,並允許應用程式開發人員[選擇宣告 MIME 嗅探](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。 以下代碼已新增到*Web.config 檔案中*。

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>實現捆綁和最小化

當 Visual Studio 創建新的 Web 專案時,預設情況下不會啟用 JavaScript 檔的捆綁和小化。 我們在BundleConfig.cs中添加了一行代碼:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>為身份驗證 Cookie 設定過期逾時

默認情況下,身份驗證 Cookie 將在兩周後過期。 更短的時間更安全。 您可以在*StartupAuth.cs*中變更這個設定:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>如何從本地電腦上的 Visual Studio 執行應用

有兩種方法可以運行修復它應用:

- 運行將新任務直接寫入 SQL 資料庫的基本應用程式。
- 使用佇列和後端服務運行應用程式以建立任務。 佇列模式在以[隊列為中心的工作模式](queue-centric-work-pattern.md)一章中描述。

<a id="runbase"></a>
### <a name="run-the-base-application"></a>執行基本應用程式

1. 安裝[視覺工作室 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).
2. 為[.NET 安裝用於視覺工作室的 Azure SDK。](https://azure.microsoft.com/downloads/)
3. 從[MSDN 程式庫](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)下載 .zip 檔案。
4. 在「檔案資源管理器」中,右鍵按下 .zip 檔案並按下「屬性」,然後在「屬性」視窗中按下「取消阻止」。
5. 解壓縮檔。
6. 按兩下 .sln 檔以啟動可視化工作室。
7. 在 **'工具'** 選單中,按下**NuGet 套件管理員**,然後單擊**套件管理員主控台**。
8. 在包管理器主控台 (PMC) 中,按一下「還原」。
9. 結束 Visual Studio。
10. 啟動[Azure 儲存模擬器](/azure/storage/common/storage-use-emulator)。
11. 重新啟動 Visual Studio,打開在上一步中關閉的解決方案檔。
12. 確保 FixIt 專案設置為啟動項目,然後按 CTRL_F5 運行該專案。

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>使用佇列處理執行應用程式

1. 按照[運行基本應用程式](#runbase)的說明操作,然後關閉瀏覽器並關閉 Visual Studio。
2. 使用管理員許可權啟動可視化工作室。 (您將使用 Azure 計算模擬器,這需要管理員許可權。
3. 在*MyFixIt*專案中的應用程式*Web.config*檔案中(Web 專案`appSettings/UseQueues`),將的值 更改為「true」:

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. 如果[Azure 儲存模擬器](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)未運行,則重新啟動它。
5. 同時運行修復 It Web 專案和 MyFixIt 雲端服務專案。

    使用視覺工作室:

   1. 按**F5**以運行 FixIt 專案。
   2. 在**解決方案資源管理器**中,右鍵單擊 MyFixIt雲端服務專案,然後單擊 **「調試** > **啟動新實例**」。

    使用視覺化工作室 2013 快速網頁:

   3. 在解決方案資源管理員中,右鍵按下 FixIt 解決方案並選擇**屬性**。
   4. 選擇**多個啟動項目**。
   5. 在 MyFixIt 和 MyFixIt雲端服務下的 **「操作**」下拉清單中,選擇 **「開始**」。
   6. 按一下 [確定]  。
   7. 按 **F5** 執行這兩個專案。

      運行 MyFixItCloud 服務專案時,Visual Studio 將啟動 Azure 計算模擬器。 根據您的防火牆配置,您可能需要允許模擬器通過防火牆。

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>如何使用 Windows PowerShell 文稿將基本應用部署到 Azure 應用服務 Web 應用

為了說明[「自動執行所有內容」](automate-everything.md)模式,修復 It 應用附帶了在 Azure 中設置環境並將專案部署到新環境的腳本。 以下說明說明如何使用腳本。

如果要在 Azure 中運行而不使用佇列,並且所做的更改是為了在本地使用佇列運行,請確保在繼續執行以下說明之前將 Use 佇列應用設置值設定為 false。

這些說明假定您已在本地下載並運行修復 It 解決方案,並且您具有 Azure 帳戶或已授權管理的 Azure 訂閱。

1. 安裝**Azure PowerShell**主控台。 如需指示，請參閱 [如何安裝和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。

    此自定義主控台配置為與 Azure 訂閱配合使用。 Azure 模組安裝在 *「程式檔」* 目錄中,並在每次使用 Azure PowerShell 控制台時自動匯入。

    如果喜歡在不同的主機程式(如 Windows PowerShell ISE)中工作,請確保使用[導入模組](https://go.microsoft.com/fwlink/?LinkID=141553)cmdlet 導入 Azure 模組或使用 Azure 模組中的命令觸發模組的自動導入。
2. 使用 **「以管理員身份執行」** 選項啟動 Azure PowerShell。
3. 執行[設定執行原則](https://go.microsoft.com/fwlink/p/?linkid=293941)「cmdlet 以將 Azure`RemoteSigned`PowerShell 執行政策設定為 。 輸入**Y(** 對於是)以完成策略更改。

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    這個設定讓您能夠執行未進行數位簽名的本地文稿。 (您還可以將執行策略設置為`Unrestricted`,這將在以後無需取消阻止步驟,但出於安全原因不建議這樣做。
4. 運行`Add-AzureAccount`cmdlet 以使用您的帳戶認證設定 PowerShell。

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    這些憑據將在一段時間後過期,您必須重新運行`Add-AzureAccount`cmdlet。 在編寫此電子書時,憑據過期前的時間限制為 12 小時。
5. 如果您有多個訂閱,請使用選擇 Azure 訂閱 cmdlet 指定要在 中創建測試環境的訂閱。
6. 使用`Get-AzurePublishSettingsFile`和`Import-AzurePublishSettingsFile`cmdlet 匯入同一 Azure 訂閱的管理證書。 第一個 cmdlet 下載憑證檔,在第二個 cmdlet 中,您可以指定該檔案的位置以匯入它。 > [!IMPORTANT]
   > 將下載的檔案保存在安全位置,或完成後將其刪除,因為它包含可用於管理 Azure 服務的證書。

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    該證書用於 REST API 呼叫,該呼叫檢測開發機的 IP 位址,以便在 SQL 資料庫伺服器上設定防火牆規則。
7. 執行[「設定位置](https://go.microsoft.com/fwlink/p/?linkid=293912)cmdlet」(`cd``chdir``sl`別名為 和 ),以瀏覽到包含文稿的目錄。 (它們位於"修復它"解決方案資料夾中的*自動化*資料夾中。如果任何目錄名稱包含空格,則將路徑放入引號中。 例如,要導航到目錄,`c:\Sample Apps\FixIt\Automation`可以輸入以下命令:

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. 要允許 Windows PowerShell 運行這些文稿,請使用[取消阻止檔案](https://go.microsoft.com/fwlink/p/?linkid=294021)cmdlet。 (腳本被阻止,因為它們是從 Internet 下載的。

    > [!WARNING]
    > 安全性`Unblock-File`- 在運行任何文稿或可執行檔之前,在記事本中打開該檔,檢查命令,並驗證它們不包含任何惡意代碼。

    例如,以下命令在當前目錄中的所有文稿`Unblock-File`上運行 cmdlet。

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. 要為基礎創建 Web 應用(無佇列處理)修復它應用,請執行環境創建腳本。

    所需的`Name`參數指定資料庫的名稱,並且也用於腳本創建的存儲帳戶。 名稱在azurewebsites.net域中必須全域唯一。 如果指定的名稱不唯一(如 Fixit 或 Test(甚至如示例中的 fixitdemo),`New-AzureWebsite`則 cmdlet 失敗,並出現報告衝突的內部錯誤。 該文本將名稱轉換為所有小寫,以符合 Web 應用、存儲帳戶和資料庫的名稱要求。

    所需`SqlDatabasePassword`參數指定將為 SQL 資料庫創建的管理員帳戶的密碼。 不要在密碼中包含特殊的 XML 字元(;)。&amp; &lt; &gt; 這是腳本編寫方式的限制,而不是 Azure 的限制。

    例如,如果要建立名為「fixitdemo」的 Web 應用並使用 SQL Server 管理員密碼「Passw0rd1」,則可以輸入以下命令:

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    名稱在azurewebsites.net網域中必須是唯一的,並且密碼必須滿足SQL資料庫對密碼複雜性的要求。 (示例 Passw0rd1 確實滿足要求。

    請注意,該命令以"開頭。\". 為了説明防止惡意執行腳本,Windows PowerShell 要求您在運行文稿時提供腳本檔的完全限定路徑。 可以使用點來指示當前目錄 (")。\"或提供完全限定的路徑,例如:

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    有關腳本的詳細資訊,請使用`Get-Help`cmdlet。

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    您可以使用 取得`Detailed``Full`説明 cmdlet`Parameters``Examples`的, 與 參數來篩選傳回的說明。

    如果文本失敗或生成錯誤,例如"新建 Azure 網站:先調用集 Azure 訂閱和選擇 Azure 訂閱",則可能尚未完成 Azure PowerShell 的配置。

    文稿完成後,可以使用 Azure 管理門戶查看已創建的資源,如[「自動所有內容」](automate-everything.md)章節所示。
10. 要將 FixIt 專案部署到新的 Azure 環境,請使用*Azure 網站.ps1*腳本。 例如：

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    部署完成後,瀏覽器將在 Azure 中運行修復它時打開。

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>對 Windows 電源外殼文稿進行故障排除

運行這些腳本時遇到的最常見的錯誤與許可權有關。 確保`Add-AzureAccount``Import-AzurePublishSettingsFile`並成功,並且將它們用於相同的 Azure 訂閱。 即使`Add-AzureAccount`成功,你也得再次運行它。 添加`Add-AzureAccount`的許可權將在 12 小時內過期。

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>物件參考未設定成物件的執行個體。

如果腳本返回錯誤(如"物件引用未設置為物件的實例",這意味著 Windows PowerShell 找不到要處理的物件(這是空引用異常),請運行`Add-AzureAccount`cmdlet 並重試該腳本。

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>內部錯誤:伺服器遇到內部錯誤。

當`New-AzureWebsite`名稱在azurewebsites.net網域中不唯一時,cmdlet 返回內部錯誤。 要解決錯誤,請使用名稱的其他值,該值位於*New-Azure 網站Env.ps1*的名稱參數中。

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>重新啟動文稿

如果需要重新啟動*New-Azure 網站Env.ps1*腳本,因為它在列印"腳本已完成"消息之前出現故障,則可能需要刪除腳本在停止之前創建的資源。 例如,如果文稿已創建 ContosoFixItDemo Web 應用,並且您再次使用相同的名稱運行文稿,則該文本將失敗,因為該名稱正在使用中。

要確定文稿在停止之前建立的資源,請使用以下 cmdlet:

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`: 要執行此 cmdlet,請將`Get-AzureSqlDatabase`資料庫伺服器 名稱導管到 :`Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

要刪除這些資源,請使用以下命令。 請注意,如果刪除資料庫伺服器,則會自動刪除與伺服器關聯的資料庫。

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>如何將具有佇列處理的應用部署到 Azure 應用服務 Web 應用和 Azure 雲端服務

要啟用佇列,請確保在 MyFixIt_Web.config 檔中進行以下更改。 在`appSettings`下,將`UseQueues`的值更改為「true」:

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

然後,將 MVC 應用程式部署到 Azure 應用服務中的 Web 應用,如[前面](#deploybase)所述。

接下來,創建新的 Azure 雲服務。 修復 It 應用中包含的腳本不會創建或部署雲服務,因此必須為此使用 Azure 門戶。 在門戶中,按下 **「新** -- **計算**+**雲端服務** -- **快速創建**」,然後輸入 URL 和資料中心位置。 使用部署 Web 應用的同一資料中心。

![](the-fix-it-sample-application/_static/image1.png)

在部署雲服務之前,需要更新某些配置檔。

在 MyFixIt.WorkerRole_app.config`connectionStrings`中,在`appdb`下, 將連接字串的值替換為 SQL 資料庫的實際連接字串。 可以從門戶獲取連接字串。 在門戶中,按一下**ADO .Net、ODBC、PHP 和 JDBC 的****SQL 資料庫** - **appdb** - 檢視 SQL 資料庫連接字串。 複製ADO.NET連接字串並將該值貼上到app.config檔中。 將「此處的\_密碼\_」替換為資料庫密碼。 (假設您使用腳本部署 MVC 應用,則可以在腳本`SqlDatabasePassword`參數中 指定資料庫密碼。

結果應如下所示:

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

在同一 MyFixIt.WorkerRole_app.config`appSettings`檔下 ,替換 Azure 儲存帳戶的兩個占位符值。

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

可以從門戶獲取訪問密鑰。 請參考[如何管理儲存帳號](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)。

在 MyFixItCloudService 服務配置.Cloud.cscfg 中,替換 Azure 儲存帳戶的兩個占位符值。

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

現在,您已準備好部署雲服務。 在「解決方案流覽」中,右鍵單擊 MyFixIt雲端服務專案並選擇 **「發布」。** 有關詳細資訊,請參閱[本教程的第](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)2 部分中的"[將應用程式部署到 Azure"。](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)

> [!div class="step-by-step"]
> [上一步](more-patterns-and-guidance.md)
