---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: 使用 Azure) 建立 Real-World 雲端應用程式的監視和遙測 (|Microsoft Docs
author: MikeWasson
description: 以 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會解釋13個模式和實務，
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f61810ea7b486b2fa0bbb234edea7541eedde835
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345575"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>使用 Azure) 建立 Real-World 雲端應用程式的監視和遙測 (

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 或 [下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **以 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 它說明13個模式和實務，可協助您成功開發雲端 web 應用程式。 如需電子書的詳細資訊，請參閱 [第一章](introduction.md)。

很多人都依賴客戶，讓他們知道應用程式何時關閉。 這並不是最佳做法，特別是在雲端中。 不保證會有快速通知，而且當您收到通知時，通常會收到最少量或誤導的資料。 有了良好的遙測與記錄系統，您就可以瞭解應用程式的情況，當發生問題時，您會立即找出問題，並提供實用的疑難排解資訊供您使用。

## <a name="buy-or-rent-a-telemetry-solution"></a>購買或出租遙測解決方案

> [!NOTE]
> 本文是在 [Application Insights](/azure/application-insights/app-insights-overview) 發行之前撰寫的。 Application Insights 是 Azure 上的遙測解決方案的慣用方法。 如需詳細資訊，請參閱 [設定 ASP.NET 網站的 Application Insights](/azure/application-insights/app-insights-asp-net) 。

雲端環境的最大好處之一，就是很容易購買或租借您的勝利。 遙測是範例。 如果沒有太多努力，您就能以非常符合成本效益的方式，讓遙測系統正常運作並執行。 有一堆很棒的夥伴與 Azure 整合，其中有些都有免費層–因此，您可以取得基本遙測資料。 以下是目前在 Azure 上提供的幾個專案：

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#) 也包含監視功能。

我們將快速逐步解說如何設定新的 Relic，以顯示使用遙測系統有多麼容易。

在 Azure 入口網站中，註冊服務。 按一下 [ **新增**]，然後按一下 [ **儲存**]。 [ **選擇附加** 元件] 對話方塊隨即出現。 向下鍵，然後按一下 [ **新增 Relic**]。

![選擇附加元件](monitoring-and-telemetry/_static/image1.png)

按一下向右箭號，然後選擇您想要的服務層級。 在此示範中，我們將使用免費層。

![個人化附加元件](monitoring-and-telemetry/_static/image2.png)

按一下向右箭號，確認 [購買]，新的 Relic 現在會顯示為入口網站中的附加元件。

![審查購買](monitoring-and-telemetry/_static/image3.png)

![入口網站中的新 Relic 附加元件](monitoring-and-telemetry/_static/image4.png)

按一下 [ **連接資訊**]，然後複製授權金鑰。

![連線資訊](monitoring-and-telemetry/_static/image5.png)

在入口網站 **中，移** 至 web 應用程式的 [設定] 索引標籤，將 [ **效能監視** ] 設定為 [ **附加**元件]，然後將 [ **選擇附加** 元件] 下拉式清單設定為 [ **新增 Relic**]。 然後按一下 [儲存]  。

![[設定] 索引標籤中的新 Relic](monitoring-and-telemetry/_static/image6.png)

在 Visual Studio 中，在您的應用程式中安裝新的 Relic NuGet 套件。

![[設定] 索引標籤中的開發人員分析](monitoring-and-telemetry/_static/image7.png)

將應用程式部署至 Azure，並開始使用它。 建立一些可修正 It 工作的工作，以提供一些活動讓新的 Relic 監視。

然後回到入口網站 [**附加**元件] 索引標籤中的 [**新增 Relic** ] 頁面，然後按一下 [**管理**]。 入口網站會將您傳送至新的 Relic 管理入口網站，並使用單一登入進行驗證，因此您不需要再次輸入認證。 [總覽] 頁面會顯示各種效能統計資料。  (按一下影像以查看完整大小的總覽頁面。 ) 

[![[新增 Relic 監視] 索引標籤](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

以下是您可以看到的一些統計資料：

- 每天不同時間的平均回應時間。

    ![回應時間](monitoring-and-telemetry/_static/image10.png)
- 每分鐘每分鐘要求 (的輸送量速率) 在每天的不同時間。

    ![輸送量](monitoring-and-telemetry/_static/image11.png)
- 花費在處理不同 HTTP 要求的伺服器 CPU 時間。

    ![Web 交易時間](monitoring-and-telemetry/_static/image12.png)
- 在應用程式程式碼的不同部分花費的 CPU 時間：

    ![追蹤詳細資料](monitoring-and-telemetry/_static/image13.png)
- 歷程記錄效能統計資料。

    ![歷程記錄效能](monitoring-and-telemetry/_static/image14.png)
- 呼叫外部服務（例如 Blob 服務），以及如何可靠且回應服務的相關統計資料。

    ![外部服務](monitoring-and-telemetry/_static/image15.png)

    ![外部服務](monitoring-and-telemetry/_static/image16.png)

    ![外部服務](monitoring-and-telemetry/_static/image17.png)
- 世界上或美國 web 應用程式流量來源的相關資訊。

    ![[地理位置]](monitoring-and-telemetry/_static/image18.png)

您也可以設定報表和事件。 例如，您可以在任何時候開始看到錯誤，將電子郵件傳送給警示支援人員來解決問題。

![報表](monitoring-and-telemetry/_static/image19.png)

新 Relic 只是遙測系統的其中一個範例;您也可以從其他服務取得全部。 雲端的好處是，您不需要撰寫任何程式碼，也不需要支付任何費用，因此您可以突然取得有關應用程式的使用方式，以及客戶實際遇到的資訊。

<a id="log"></a>
## <a name="log-for-insight"></a>深入解析的記錄

遙測封裝是很好的第一個步驟，但您仍然必須檢測自己的程式碼。 遙測服務會在發生問題時告訴您，並告訴您客戶所遇到的問題，但可能無法讓您深入瞭解程式碼中的狀況。

您不想要從遠端進入實際執行伺服器，以查看應用程式的執行情況。 當您有一部伺服器時，這可能是可行的，但是當您調整到數百部伺服器，而且您不知道需要遠端的伺服器時，該怎麼辦？ 您的記錄應該提供足夠的資訊，讓您不需要從遠端進入實際執行伺服器來分析和偵測問題。 您應該記錄足夠的資訊，讓您可以只透過記錄來隔離問題。

### <a name="log-in-production"></a>在生產環境中登入

很多人都只會在發生問題時，才在生產環境中開啟追蹤功能，而且想要進行調試。 這可能會在您注意到問題的時間與您取得有用的疑難排解資訊的時間之間產生顯著的延遲。 而您取得的資訊可能不會對間歇性錯誤有説明。

在儲存體成本低廉的雲端環境中，我們建議您一律在生產環境中保留登入。 如此一來，當錯誤發生時，您已經記錄了它們，而且您有歷程記錄資料可協助您分析隨著時間而開發的問題，或是在不同時間定期發生的問題。 您可以自動化清除程式來刪除舊的記錄檔，但是您可能會發現，設定這種處理常式比保留記錄的成本更高。

相較于疑難排解時間和金錢的增加，節省的成本很簡單，因為您可以在發生問題時，擁有所需的所有資訊。 當有人告訴您，他們最近一次在8:00 時有隨機的錯誤，但他們並不記得錯誤，您可以立即找出問題所在。

針對小於 $4 的月份，您可以保留 50 gb 的記錄，而記錄的效能影響會很簡單，只要您要記住一件事，就可以確保您的記錄程式庫是非同步。

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>區分記錄檔，以通知需要採取動作的記錄

記錄檔的目的是要通知 (我希望您知道) 或 ACT (我希望您) 進行一些動作。 請小心只針對真的需要人員或自動化程式來採取行動的問題，撰寫 ACT 記錄。 太多 ACT 記錄會造成雜訊，需要太多工作來進行查詢，才能找出真正的問題。 而且，如果您的 ACT 記錄會自動觸發一些動作，例如傳送電子郵件給支援人員，請避免單一問題觸發上千個這類動作。

在 .NET System 中，可以將錯誤、警告、資訊和偵錯工具/詳細層級指派給記錄。 您可以藉由保留 ACT 記錄的錯誤層級，並使用較低層級的通知記錄，來區分 ACT 與通知記錄。

![記錄層級](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>在執行時間設定記錄層級

雖然在生產環境中一定要有記錄功能，另一個最佳作法是採用記錄架構，讓您在執行時間依您要記錄的詳細層級進行調整，而不需要重新部署或重新開機應用程式。 例如，當您在中使用追蹤功能時， `System.Diagnostics` 您可以建立錯誤、警告、資訊和 Debug/Verbose 記錄。 建議您一律在生產環境中記錄錯誤、警告和資訊記錄，而且您會想要以個別案例為基礎，動態地新增 Debug/Verbose 記錄以進行疑難排解。

Azure App Service 中的 Web Apps 內建支援將記錄寫入 `System.Diagnostics` 檔案系統、資料表儲存體或 Blob 儲存體。 您可以為每個儲存體目的地選取不同的記錄層級，而且您可以即時變更記錄層級，而不需要重新開機應用程式。 Blob 儲存體支援可讓您更輕鬆地在應用程式記錄檔上執行 [HDInsight](https://docs.microsoft.com/azure/hdinsight/) 分析作業，因為 HDInsight 知道如何直接使用 Blob 儲存體。

### <a name="log-exceptions"></a>記錄例外狀況

請勿只 put *例外狀況。ToString ( * 您記錄程式碼中的 # B1。 這會留下內容相關資訊。 在 SQL 錯誤的情況下，會留下 SQL 錯誤號碼。 針對所有例外狀況，包括內容資訊、例外狀況本身和內部例外狀況，以確保您提供進行疑難排解所需的一切。 例如，內容資訊可能包含伺服器名稱、交易識別碼和使用者名稱 (但密碼或任何秘密！ ) 。

如果您依賴每位開發人員以例外狀況記錄來進行正確的作業，其中有些不是。 為了確保每次都能正確完成，請將例外狀況處理直接放入記錄器介面：將例外狀況物件本身傳遞給記錄器類別，並正確地在記錄器類別中記錄例外狀況資料。

### <a name="log-calls-to-services"></a>將通話記錄至服務

強烈建議您在每次應用程式向外呼叫服務時撰寫記錄，無論是對資料庫或 REST API 或任何外部服務。 包含在您的記錄中，不僅表示成功或失敗，也包含每個要求的時間長度。 在雲端環境中，您通常會看到與緩慢停機相關的問題，而不是完全中斷。 通常需要10毫秒的時間可能會突然開始花費一秒鐘。 當有人告訴您，您的應用程式速度很慢時，您想要查看新的 Relic 或您擁有的任何遙測服務並驗證其經驗，然後您想要能夠查看自己的記錄檔，以深入瞭解其速度很慢的原因。

### <a name="use-an-ilogger-interface"></a>使用 ILogger 介面

當您建立實際執行應用程式時，我們建議您建立簡單的 *ILogger* 介面，並將其中的一些方法放在其中。 這可讓您更輕鬆地變更記錄的執行，而不需要完成所有程式碼即可。 我們可以在 `System.Diagnostics.Trace` 整個 Fix It 應用程式中使用類別，但是我們會在執行 *ILogger*的記錄類別中的內容下使用它，而我們會在整個應用程式中進行 *ILogger* 方法呼叫。

如此一來，如果您想要讓記錄更豐富，可以 [`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) 使用您想要的任何記錄機制來取代。 例如，當您的應用程式成長時，您可能會決定要使用更完整的記錄套件，例如 [NLog](http://nlog-project.org/) 或 [Enterprise Library 記錄應用程式區塊](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)。  ([Log4Net](http://logging.apache.org/log4net/) 是另一個常用的記錄架構，但不會進行非同步記錄。 ) 

使用架構（例如 NLog）的其中一個可能原因，是有助於將記錄輸出分割成不同的高容量和高價值的資料存放區。 這可協助您有效率地儲存大量的通知資料，而您不需要對其執行快速查詢，同時維持對 ACT 資料的快速存取。

### <a name="semantic-logging"></a>語義記錄

如需更新的方式來進行記錄，以產生更有用的診斷資訊，請參閱 [企業程式庫語義記錄應用程式區塊 (樓板) ](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)。 在 .NET 4.5 中，使用 [Windows 的事件追蹤](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) 和 [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) 支援，可讓您建立更多結構化和可查詢的記錄。 您可以針對您記錄的每個事件種類定義不同的方法，讓您自訂所撰寫的資訊。 例如，若要記錄 SQL Database 錯誤，您可能會呼叫 `LogSQLDatabaseError` 方法。 對於這種例外狀況，您知道有一項重要的資訊是錯誤號碼，所以您可以在方法簽章中包含錯誤號碼參數，並將錯誤號碼記錄為您所撰寫記錄檔記錄中的個別欄位。 因為數位位於不同的欄位，所以您可以更輕鬆且可靠地取得以 SQL 錯誤號碼為基礎的報表，而不是只是將錯誤號碼串連到訊息字串。

## <a name="logging-in-the-fix-it-app"></a>登入修正 It 應用程式

### <a name="the-ilogger-interface"></a>ILogger 介面

以下是 Fix It 應用程式中的 *ILogger* 介面。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

這些方法可讓您以 *System. Diagnostics*支援的四個層級來撰寫記錄。 TraceApi 方法是用來記錄外部服務呼叫，並提供延遲的相關資訊。 您也可以加入一組用於 Debug/Verbose 層級的方法。

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger 介面的記錄器執行

介面的實，其實很簡單。 基本上，它只會呼叫標準的 *系統診斷* 方法。 下列程式碼片段會顯示這三個資訊方法，以及其中一個方法。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>呼叫 ILogger 方法

每次修正程式碼時，應用程式中的程式碼都會攔截例外狀況，它會呼叫 *ILogger* 方法來記錄例外狀況的詳細資料。 每次呼叫資料庫、Blob 服務或 REST API 時，它會在呼叫之前先啟動碼錶、在服務傳回時停止碼錶，以及記錄已耗用的時間，以及成功或失敗的相關資訊。

請注意，記錄訊息包含類別名稱和方法名稱。 最好的作法是確定記錄訊息會識別應用程式程式碼的哪個部分寫入它們。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

因此，在每次修正 It 應用程式對 SQL Database 進行呼叫時，您都可以看到呼叫、呼叫它的方法，以及確切的等候時間。

![記錄中的 SQL Database 查詢](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

如果您流覽記錄檔，就會看到資料庫呼叫 take 的時間是變數。 這項資訊可能很有用：因為應用程式會記錄所有資訊，您可以分析資料庫服務在一段時間內的執行歷程記錄趨勢。 比方說，服務的時間可能會很快，但要求可能會失敗，或回應可能會在一天的特定時間變慢。

您可以對 Blob 服務執行相同的動作–每次應用程式上傳新檔案時，都會有一個記錄檔，您可以看到上傳每個檔案所花的時間。

![Blob 上傳記錄檔](monitoring-and-telemetry/_static/image23.png)

每次您呼叫服務時，都只需撰寫幾行程式碼就行了，現在每當有人說他們遇到問題時，您就知道問題是什麼、是錯誤，還是即使執行速度很慢也是一樣。 您可以找出問題的來源，而不需要從遠端進入伺服器，或在錯誤發生之後開啟記錄，並希望重新建立記錄。

## <a name="dependency-injection-in-the-fix-it-app"></a>修正 It 應用程式中的相依性插入

您可能會想知道上述範例中的存放庫函式如何取得記錄器介面執行：

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

為了將介面連接到執行程式，應用程式會使用相依性 [插入](http://en.wikipedia.org/wiki/Dependency_injection) (DI) 與 [AutoFac](http://autofac.org/)。 DI 可讓您在程式碼中的許多地方使用以介面為基礎的物件，而且只需要在單一位置指定介面具現化時所用的實作為。 這可讓您更輕鬆地變更執行：例如，您可能想要以 NLog 記錄器取代 System. 診斷記錄器。 或者，針對自動化測試，您可能會想要以模擬版本的記錄器取代。

修正 It 應用程式會在所有存放庫和所有控制器中使用 DI。 控制器類別的函式會取得 *ITaskRepository* 介面，與存放庫取得記錄器介面的方式相同：

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

應用程式會使用 AutoFac DI 程式庫，自動提供這些函式的 *TaskRepository* 和 *記錄器* 實例。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

這段程式碼基本上會指出，任何位置的函式都需要 *ILogger* 介面、傳入 *記錄器* 類別的實例，而且只要需要 *IFixItTaskRepository* 介面，就會傳入 *FixItTaskRepository* 類別的實例。

[AutoFac](http://autofac.org/) 是許多您可以使用的相依性插入架構之一。 另一個常用的是 [Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx)，Microsoft 模式和實務的建議和支援。

## <a name="built-in-logging-support-in-azure"></a>Azure 中的內建記錄支援

Azure [針對 Azure App Service 中的 Web Apps](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)支援下列類型的記錄：

-  (您可以立即開啟和關閉並設定層級，而不需要重新開機網站) 。
- Windows 事件。
-  (HTTP/FREB) 的 IIS 記錄。

Azure [在雲端服務中](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)支援下列類型的記錄：

- 系統診斷追蹤。
- 效能計數器。
- Windows 事件。
-  (HTTP/FREB) 的 IIS 記錄。
- 自訂目錄監視。

修正 It 應用程式使用系統診斷追蹤。 若要在 web 應用程式中啟用系統診斷記錄，您只需要在入口網站中翻轉切換開關或呼叫 REST API。 在入口網站中，按一下您網站 **的 [設定** ] 索引標籤，並向下滾動以查看 **應用程式診斷** 區段。 您可以開啟或關閉登入，並選取您想要的記錄層級。 您可以讓 Azure 將記錄寫入檔案系統或儲存體帳戶。

![[設定] 索引標籤中的應用程式診斷和網站診斷](monitoring-and-telemetry/_static/image24.png)

在 Azure 中啟用記錄之後，您可以在建立 Visual Studio 的輸出視窗中看到記錄。

![串流記錄功能表](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![串流記錄功能表](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

您也可以將記錄寫入至儲存體帳戶，並使用可存取 Azure 儲存體表格服務的任何工具來加以查看，例如 Visual Studio 或[Azure 儲存體總管](https://azure.microsoft.com/features/storage-explorer/)中的**伺服器總管**。

![伺服器總管中的記錄](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>摘要

執行現成的遙測系統、在您自己的程式碼中檢測記錄，並在 Azure 中設定記錄，其實很簡單。 當您遇到生產環境問題時，遙測系統和自訂記錄的組合將有助於您在問題成為客戶的主要問題之前迅速解決問題。

在 [下一章](transient-fault-handling.md) 中，我們將探討如何處理暫時性錯誤，讓它們不會成為您必須調查的生產環境問題。

## <a name="resources"></a>資源

如需詳細資訊，請參閱下列資源。

遙測檔主要：

- [Microsoft 模式和實務-Azure 指引](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱檢測和遙測指引、服務計量指引、健康情況端點監視模式，以及執行時間重新設定模式。
- [雲端中的捏合：在 Azure 網站上啟用新的 Relic 效能監視](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)。
- [Azure 雲端服務上 Large-Scale 服務設計的最佳做法](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 以標記 Simm 和 Michael Thomassy 的白皮書。 請參閱遙測和診斷區段。
- [使用 Application Insights](https://msdn.microsoft.com/magazine/dn683794.aspx)的新一代開發。 MSDN 雜誌文章。

記錄的主要相關檔：

- [語義記錄應用程式區塊 (樓板) ](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)。 Neil Mackenzie 會提供使用樓板進行語義記錄的案例。
- [使用語義記錄來建立結構化且有意義的記錄](https://channel9.msdn.com/Events/Build/2013/3-336)。  (Video) Julian Dominguez 會呈現使用樓板進行語義記錄的案例。
- [EF6 SQL 記錄-第1部分：簡單記錄](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/)。 Arthur Vickers 說明如何記錄 EF 6 中 Entity Framework 所執行的查詢。
- [ASP.NET MVC 應用程式中的連接恢復功能和命令攔截 Entity Framework](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 第四個在九部分的教學課程系列中，說明如何使用 EF 6 命令攔截功能，藉由 Entity Framework 來記錄傳送至資料庫的 SQL 命令。
- [使用 c # 5.0 呼叫端資訊屬性來改善記錄](http://www.dotnetcurry.com/showarticle.aspx?ID=972)。 如何輕鬆地記錄呼叫方法的名稱，而不需將其硬式編碼為常值或使用反映來手動取得。

檔主要是關於疑難排解：

- [Azure 疑難排解 &amp; 調試 blog](https://blogs.msdn.com/b/kwill/)。
- [AzureTools – Azure 開發人員支援小組所使用的診斷公用程式](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true)。 介紹並提供工具的下載連結，可在 Azure VM 上用來下載及執行各種不同的診斷和監視工具。 當您需要診斷特定 VM 上的問題時，會很有用。
- [使用 Visual Studio 針對 Azure App Service 中的 web 應用程式進行疑難排解](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)。 開始使用系統診斷追蹤和遠端偵錯程式的逐步教學課程。

影片：

- [安全：建立可調整的彈性雲端服務](https://channel9.msdn.com/Series/FailSafe)。 Ulrich Homann、Marc Mercuri 和 Mark Simm 的九部分系列。 以非常容易存取且有趣的方式提供高階概念和架構原則，並以 Microsoft 客戶諮詢團隊 (貓) 體驗實際客戶的案例。 集4和9與監視和遙測有關。 第9集包含監視服務 MetricsHub、AppDynamics、New Relic 和 PagerDuty 的總覽。
- [打造 Big：從 Azure 客戶學習的課程-第二部分](https://channel9.msdn.com/Events/Build/2012/3-030)。 Mark Simm 討論設計失敗和檢測一切。 類似于安全性群組，但深入探討如何詳細資料。

程式碼範例：

- [Azure 中的雲端服務基本](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)概念。 Microsoft Azure 客戶諮詢小組所建立的範例應用程式。 示範遙測和記錄做法，如下列文章所述。 此範例會使用 [NLog](http://nlog-project.org/)來執行應用程式記錄。 如需相關檔，請參閱 [四篇有關遙測和記錄的 TechNet wiki 文章](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)。

> [!div class="step-by-step"]
> [上一個](design-to-survive-failures.md) 
> [下一步](transient-fault-handling.md)
