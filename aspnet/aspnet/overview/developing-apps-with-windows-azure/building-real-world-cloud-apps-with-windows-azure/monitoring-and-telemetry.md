---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: 監視和遙測(使用 Azure 構建真實世界雲應用) |微軟文件
author: MikeWasson
description: 使用 Azure 電子書建構真實世界雲端應用基於 Scott Guthrie 開發的演示文稿。 它解釋了13種模式和做法,他可以...
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f61810ea7b486b2fa0bbb234edea7541eedde835
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676031"
---
# <a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>監視和遙測(使用 Azure 建構真實世界雲應用)

由[邁克·瓦森](https://github.com/MikeWasson),[里克·安德森](https://twitter.com/RickAndMSFT),[湯姆·戴克斯特拉](https://github.com/tdykstra)

[下載修復項目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 使用 Azure 電子書**建構真實世界雲端應用**基於 Scott Guthrie 開發的演示文稿。 它解釋了 13 種模式和做法,這些模式和做法可以説明您成功開發雲端的 Web 應用。 有關電子書的資訊,請參閱[第一章](introduction.md)。

很多人依靠客戶來讓他們知道他們的應用程式何時關閉了。 這不是任何地方的最佳實踐,尤其是在雲中。 不能保證快速通知,當您收到通知時,您通常會收到關於所發生的事情的最小或誤導性數據。 有了良好的遙測和日誌記錄系統,您可以瞭解應用發生的情況,當出現問題時,您可以馬上發現並處理有用的故障排除資訊。

## <a name="buy-or-rent-a-telemetry-solution"></a>購買或租用遙測解決方案

> [!NOTE]
> 本文是在[應用程式見解](/azure/application-insights/app-insights-overview)發佈之前編寫的。 應用程式見解是 Azure 上遙測解決方案的首選方法。 有關詳細資訊[,請參閱為ASP.NET網站設定應用程式見解](/azure/application-insights/app-insights-asp-net)。

雲環境的偉大之一是,它真的很容易購買或租出你的方式的勝利。 遙測就是一個例子。 無需大量精力,即可獲得一個非常好的遙測系統啟動和運行,非常經濟。 有一群偉大的合作夥伴與 Azure 整合,其中一些合作夥伴具有免費層,因此您可以免費獲取基本遙測數據。 以下是 Azure 上目前可用的少數功能:

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[微軟系統中心](http://www.petri.co.il/microsoft-system-center-introduction.htm#)還包括監控功能。

我們將快速完成設置新遺物,以顯示使用遙測系統是多麼容易。

在 Azure 管理門戶中,註冊該服務。 按下 **"新建**",然後單擊"**儲存**"。 將顯示選擇**載入項目**「對話框」。 向下滾動並按下 **「新遺物**」。。

![選擇載入項目](monitoring-and-telemetry/_static/image1.png)

按一下右箭頭並選擇所需的服務層。 對於此演示,我們將使用免費套餐。

![個人化載入項目](monitoring-and-telemetry/_static/image2.png)

按下右箭頭,確認"購買",新遺物現在顯示在門戶中的載入項中。

![審核購買](monitoring-and-telemetry/_static/image3.png)

![管理門戶中的新遺物載入項](monitoring-and-telemetry/_static/image4.png)

按下 **「連線資訊**」並複製許可證金鑰。

![連線資訊](monitoring-and-telemetry/_static/image5.png)

跳到門戶中的 Web 應用的 **「設定**」選項卡,將**效能監視**設定為 **「載入項**」,並將 **「選擇載入項**」下拉清單設定為 **「新建」。** 然後按下「**保存**」。

![設定選項卡中的新遺物](monitoring-and-telemetry/_static/image6.png)

在可視化工作室中,在應用中安裝新的遺物 NuGet 包。

![設定選項卡中的開發人員分析](monitoring-and-telemetry/_static/image7.png)

將應用部署到 Azure 並開始使用它。 創建一些修復它的任務,以提供一些活動,為新遺物監視。

然後返回門戶**的「載入項**」選項卡中的 **「新遺物**」頁,然後按下「**管理**」。 門戶使用單一登錄進行身份驗證,將您發送到新文物管理門戶,這樣您就不必再次輸入憑據。 概述"頁提供了各種性能統計資訊。 (按一下影像可查看概覽頁面全尺寸。

[![新的遺物監視選項卡](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

以下是一些可以檢視的統計資訊:

- 一天中不同時間的平均響應時間。

    ![回應時間](monitoring-and-telemetry/_static/image10.png)
- 一天中不同時間(以每分鐘請求)的輸送量率。

    ![Throughput](monitoring-and-telemetry/_static/image11.png)
- 伺服器 CPU 時間用於處理不同的 HTTP 請求。

    ![Web 交易時間](monitoring-and-telemetry/_static/image12.png)
- 在應用程式代碼的不同部份花費的 CPU 時間:

    ![追蹤詳細資訊](monitoring-and-telemetry/_static/image13.png)
- 歷史績效統計資訊。

    ![歷史表現](monitoring-and-telemetry/_static/image14.png)
- 對外部服務的調用,如 Blob 服務,以及有關服務的可靠性和回應速度的統計資訊。

    ![外部服務](monitoring-and-telemetry/_static/image15.png)

    ![外部服務](monitoring-and-telemetry/_static/image16.png)

    ![外部服務](monitoring-and-telemetry/_static/image17.png)
- 有關世界或美國 Web 應用流量來自何處的資訊。

    ![[地理位置]](monitoring-and-telemetry/_static/image18.png)

您還可以設置報表和事件。 例如,您可以說,每當您開始看到錯誤時,請發送電子郵件提醒支援人員注意問題。

![報表](monitoring-and-telemetry/_static/image19.png)

新遺跡只是遙測系統的一個示例;您也可以從其他服務獲得所有這些。 雲的優點是,無需編寫任何代碼,只需支付極少或無費用,您突然可以獲得有關應用程式如何使用以及客戶實際體驗的更多資訊。

<a id="log"></a>
## <a name="log-for-insight"></a>記錄洞察

遙測包是很好的第一步,但您仍必須檢測自己的代碼。 遙測服務告訴您何時出現問題,並告訴您客戶正在經歷什麼,但可能無法讓您深入瞭解代碼中發生的情況。

您不希望遠端到生產伺服器以查看應用正在執行的操作。 當您有一台伺服器時,這可能很實用,但是,當您已擴展到數百台伺服器,而您不知道需要遠端插入哪些伺服器時,該怎麼辦? 日誌記錄應提供足夠的資訊,您永遠不必遠端到生產伺服器來分析和調試問題。 您應該記錄足夠的資訊,以便僅通過日誌隔離問題。

### <a name="log-in-production"></a>登錄生產

只有當出現問題並且想要調試時,許多人才會在生產中打開跟蹤。 這可以在您意識到問題的時間與獲取有關問題的有用故障排除信息之間引入大量延遲。 您獲得的資訊可能對間歇性錯誤沒有説明。

在存儲成本低廉的雲環境中,我們建議始終在生產中保留日誌記錄。 這樣,當錯誤發生時,您已經記錄了它們,並且您擁有的歷史數據可以説明您分析隨時間而發展或在不同的時間定期發生的問題。 您可以自動執行清除過程以刪除舊日誌,但您可能會發現設置此類進程比保留日誌的成本更高。

與故障發生時所需的所有資訊可用,可以節省的故障排除時間和資金,日誌記錄的額外成本微不足道。 然後,當有人告訴你,他們昨晚8點左右有一個隨機錯誤,但他們不記得錯誤,你可以很容易找出問題是什麼。

每月不到 4 美元,您可以保留 50 GB 的日誌,只要牢記一件事,日誌記錄的性能影響就微不足道了--為了避免性能瓶頸,請確保日誌記錄庫是非同步的。

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>區分通知需要操作的紀錄

日誌是用來通知(我想讓你知道一些事情)或ACT(我希望你做點什麼)。 小心只編寫 ACT 日誌,以便真正需要人員或自動過程才能採取行動的問題。 太多的 ACT 日誌會產生噪音,需要太多的工作來篩選所有日誌,以找到真正的問題。 如果您的 ACT 日誌自動觸發一些操作,例如向支援人員發送電子郵件,請避免讓數千個此類操作由單個問題觸發。

在 .NET System.診斷追蹤中,可以為日誌分配錯誤、警告、資訊和調試/詳細級別。 您可以通過為 ACT 紀錄保留錯誤等級並使用較低級別的 INFORM 日誌來區分 ACT 和 INFORM 日誌。

![記錄層級](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>在執行時設定紀錄紀錄等級

雖然在生產中始終啟用日誌記錄是值得的,但另一個最佳做法是實現日誌記錄框架,使您能夠在運行時調整要記錄的詳細級別,而無需重新部署或重新啟動應用程式。 例如,當您在中使用`System.Diagnostics`中的跟蹤工具時,可以創建錯誤、警告、資訊和調試/詳細日誌。 我們建議您始終在生產中記錄錯誤、警告和資訊日誌,並且希望能夠動態添加調試/詳細日誌記錄,以便逐案進行故障排除。

Azure 應用服務中的 Web 應用具有將日`System.Diagnostics`誌寫入 檔案系統、表存儲或 Blob 儲存的內置支援。 您可以為每個儲存目標選擇不同的日誌記錄級別,並且無需重新啟動應用程式即可動態更改日誌記錄級別。 Blob 儲存支援使在應用程式日誌上運行[HDInsight](https://docs.microsoft.com/azure/hdinsight/)分析作業變得更加容易,因為 HDInsight 知道如何直接處理 Blob 儲存。

### <a name="log-exceptions"></a>記錄例外狀況

不要只是把*例外。日誌記錄代碼中的 ToString()。* 這樣就排除了上下文資訊。 在 SQL 錯誤的情況下,它忽略了 SQL 錯誤編號。 對於所有異常,請包括上下文資訊、異常本身和內部異常,以確保提供故障排除所需的一切。 例如,上下文資訊可能包括伺服器名稱、事務標識符和使用者名(但不包括密碼或任何機密!

如果您依賴每個開發人員在異常日誌記錄中做正確的事情,其中一些則不會。 為了確保每次都以正確的方式完成,請直接在記錄器介面中生成異常處理:將異常物件本身傳遞給記錄器類,並在記錄器類中正確記錄異常數據。

### <a name="log-calls-to-services"></a>記錄對服務的呼叫

我們強烈建議您在每次應用調用服務時編寫日誌,無論是資料庫還是 REST API 或任何外部服務。 不僅在日誌中包括成功或失敗的指示,還包括每個請求需要多長時間。 在雲環境中,您經常會看到與慢速相關的問題,而不是完全的中斷。 通常需要 10 毫秒的東西可能會突然開始需要一秒鐘。 當有人告訴您你的應用很慢時,您希望能夠查看 New Relic 或任何您擁有的遙測服務並驗證其體驗,然後您希望能夠查看您自己的日誌,以深入瞭解其速度緩慢的原因。

### <a name="use-an-ilogger-interface"></a>使用 ILogger 介面

我們建議您在創建生產應用程式時創建一個簡單的*ILogger*介面,並在其中輸入一些方法。 這樣以後可以輕鬆地更改日誌記錄實現,並且不必遍通所有代碼即可完成。 我們可以在整個 Fix `System.Diagnostics.Trace` It 應用中使用該類,但我們在實現*ILogger*的日誌記錄類中使用它,並且在整個應用程式中進行*ILogger*方法調用。

這樣,如果您希望使日誌記錄更豐富,則可以使用所需的任何日誌記錄機制進行替換[`System.Diagnostics.Trace`](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs)。 例如,隨著應用的增長,您可能決定要使用更全面的日誌記錄包,如[NLog](http://nlog-project.org/)或[企業庫日誌記錄應用程式塊](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)。 [(Log4Net](http://logging.apache.org/log4net/)是另一個流行的日誌記錄框架,但它不執行非同步日誌記錄。

使用 NLog 等框架的一個可能原因是為了方便將日誌記錄輸出劃分為單獨的大容量和高價值數據存儲。 這有助於您高效地存儲大量不需要執行快速查詢的 INFORM 資料,同時保持對 ACT 資料的快速存取。

### <a name="semantic-logging"></a>語意記錄

有關可以生成更多有用診斷資訊的日誌記錄的較新方法,請參閱[企業庫語義日誌記錄應用程式塊 (SLAB)。](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/) SLAB 使用 .NET 4.5 中的 Windows (ETW)[事件追蹤](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx)和[事件源](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx)支援來創建更結構化和可查詢的日誌。 您可以為記錄的每種類型的事件定義不同的方法,從而使您能夠自定義寫入的資訊。 例如,要記錄 SQL 資料庫錯誤,可以呼`LogSQLDatabaseError`叫方法 。 對於此類異常,您知道關鍵資訊是錯誤編號,因此您可以在方法簽名中包含錯誤編號參數,並將錯誤編號記錄為您編寫的日誌記錄中的單獨欄位。 由於該數位位於單獨的欄位中,因此,如果將錯誤編號串聯到消息字串中,則可以比您更容易、更可靠地獲取基於 SQL 錯誤數的報告。

## <a name="logging-in-the-fix-it-app"></a>登入修復它應用程式

### <a name="the-ilogger-interface"></a>ILogger 介面

這裡是*ILogger*介面在修復它應用程式。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

這些方法讓您能夠在系統支援的四個等級上寫入紀錄 *。* TraceApi 方法用於記錄具有延遲資訊的外部服務調用。 您還可以為調試/詳細級別添加一組方法。

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger 介面的記錄器實現

介面的實現非常簡單。 它基本上只是調用標準*系統。* 以下代碼段顯示所有三種資訊方法以及每個方法。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>呼叫 ILogger 方法

每次修復 It 應用中的代碼捕獲異常時,它都會調用*ILogger*方法來記錄異常詳細資訊。 每次調用資料庫、Blob 服務或 REST API 時,它都會在調用之前啟動秒錶,在服務返回時停止秒表,並記錄已用的時間以及有關成功或失敗的資訊。

請注意,日誌消息包括類名稱和方法名稱。 最好確保日誌消息標識應用程式代碼的哪一部分編寫了它們。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

因此,現在每次修復它應用調用 SQL 資料庫時,您都可以看到調用、調用它的方法以及它到底花了多長時間。

![紀錄中的 SQL 資料庫查詢](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

如果流覽日誌,可以看到資料庫調用所採用的時間是可變的。 這些資訊可能很有用:因為應用會記錄所有這些,因此您可以分析資料庫服務隨時間變化的性能的歷史趨勢。 例如,服務在大部分時間中可能速度很快,但請求可能會失敗,或者回應在一天中的某些時間可能會變慢。

您可以為 Blob 服務執行相同的操作 - 每次應用上載新檔時,都有一個日誌,並且您可以準確查看上載每個檔所花的時間。

![Blob 上傳紀錄](monitoring-and-telemetry/_static/image23.png)

每次調用服務時,只需多寫幾行代碼,現在每當有人說他們遇到問題時,您就會確切知道問題所在,無論是錯誤,還是運行速度很慢。 您可以精確定位問題的根源,而無需遠端插入伺服器或在錯誤發生後打開日誌記錄,並希望重新創建它。

## <a name="dependency-injection-in-the-fix-it-app"></a>修復它應用中的依賴項注入

您可能想知道上面所示範例的儲存庫建構函式如何取得紀錄器介面實現:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

要將介面連線到實現,應用程式使用[相依項(DI)](http://en.wikipedia.org/wiki/Dependency_injection)與[AutoFac](http://autofac.org/)。 DI 使您能夠在整個代碼的許多地方使用基於介面的物件,並且只需在一個位置指定在實例化介面時使用的實現。 這使得更改實現變得更加容易:例如,您可能希望將 System. 診斷記錄器替換為 NLog 記錄器。 或者對於自動測試,您可能需要替換記錄器的類比版本。

修復 It 應用程式在所有儲存庫和所有控制器中使用 DI。 控制器類別的建構函數取得*ITaskRepository*介面的方式與儲存函式庫取得紀錄器介面的方式相同:

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

該應用程式使用 AutoFac DI 庫自動為這些建構函數提供*任務儲存庫*和*記錄器*實例。

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

此代碼基本上表示,無論構造函數需要*ILogger*介面,在*記錄器*類的實例中傳遞,每當它需要*IFixItTaskRepository*介面時,都會在*FixItTaskRepository*類的實例中傳遞。

[AutoFac](http://autofac.org/)是您可以使用的許多依賴項注入框架之一。 另一個受歡迎的是[Unity,](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx)這是由微軟模式和實踐推薦和支援。

## <a name="built-in-logging-support-in-azure"></a>Azure 內建紀錄記錄支援

Azure 支援 Azure[應用服務中的 Web 應用](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)的以下類型的紀錄記錄:

- 系統.診斷追蹤(您可以打開和關閉,並在不重新啟動網站的情況下動態設置級別)。
- 視窗事件。
- IIS 紀錄 (HTTP/FREB)。

Azure 支援[雲服務中的](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics)以下類型的紀錄記錄:

- 系統.診斷跟蹤。
- 效能計數器。
- 視窗事件。
- IIS 紀錄 (HTTP/FREB)。
- 自定義目錄監視。

修復它應用使用系統.診斷跟蹤。 在 Web 應用中進行診斷日誌記錄只需在門戶中翻轉交換機或調用 REST API。" 在門戶中,按一下網站的 **「設定」** 選項卡,然後向下滾動以查看 **「應用程式診斷**」部分。 您可以打開或關閉日誌記錄,並選擇所需的日誌記錄級別。 可以讓 Azure 將日誌寫入檔案系統或儲存帳戶。

![設定選項的應用程式診斷與站台診斷](monitoring-and-telemetry/_static/image24.png)

在 Azure 中啟用日誌記錄後,可以在可視化工作室輸出視窗中看到日誌的創建。

![串流記錄選單](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![串流記錄選單](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

您還可以將日誌寫入儲存帳戶,並使用可以造訪 Azure 儲存表服務的任何工具(如可視化工作室中的**伺服器資源管理器**或[Azure 儲存資源管理員](https://azure.microsoft.com/features/storage-explorer/))查看日誌。

![伺服器資源管理員中的紀錄](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>總結

實現開箱即用的遙測系統、在您自己的代碼中記錄儀器並在 Azure 中設定日誌記錄非常簡單。 當您遇到生產問題時,遙測系統和自定義日誌的組合將説明您快速解決問題,以免它們成為客戶的主要問題。

[在下一章](transient-fault-handling.md)中,我們將介紹如何處理瞬態錯誤,以便它們不會成為您必須調查的生產問題。

## <a name="resources"></a>資源

如需詳細資訊，請參閱下列資源。

主要有關遙測的文件:

- [微軟模式與實作 - Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱檢測和遙測指南、服務計量指導、運行狀況終結點監視模式和運行時重新配置模式。
- [雲中的彭妮捏合:在 Azure 網站上啟用新的遺物效能監視](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)。
- [Azure 雲服務上大規模服務設計的最佳做法](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 馬克·西姆斯和邁克爾·托馬斯的白皮書。 請參閱遙測和診斷部分。
- [具有應用程式見解的下一代開發](https://msdn.microsoft.com/magazine/dn683794.aspx)。 MSDN 雜誌文章。

主要有關紀錄紀錄的文件:

- [語義紀錄記錄應用程式區塊 (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/). 尼爾·麥肯齊介紹了使用SLAB進行語義日誌記錄的情況。
- [使用語義紀錄紀錄建立結構化與有意義的紀錄](https://channel9.msdn.com/Events/Build/2013/3-336)。 (視訊)朱利安·多明格斯介紹了使用SLAB進行語義日誌記錄的情況。
- [EF6 SQL 紀錄紀錄 = 第 1 部份:簡單紀錄紀錄](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/)。 Arthur Vickers 演示如何記錄在 EF 6 中實體框架執行的查詢。
- [在 ASP.NETmVC 應用程式中,與實體框架的連線恢復能力和命令攔截](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 在由九部分組成的教程系列中,第四部分演示了如何使用 EF 6 命令攔截功能來記錄實體框架發送到資料庫的 SQL 命令。
- [使用 C# 5.0 呼叫方資訊屬性改進紀錄紀錄](http://www.dotnetcurry.com/showarticle.aspx?ID=972)。 如何輕鬆地將調用方法的名稱記錄到文本中,而無需將其硬編碼為文本或使用反射來手動獲取它。

主要有關故障排除的文件:

- [Azure 故障&amp;排除 除錯部落格](https://blogs.msdn.com/b/kwill/)。
- [Azure 工具 – Azure 開發人員支援團隊使用的診斷實用程式](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true)。 介紹並提供可用於 Azure VM 以下載和運行各種診斷和監視工具的工具的下載連結。 當您需要診斷特定 VM 上的問題時非常有用。
- [使用視覺化工作室在 Azure 應用服務中排除 Web 應用故障](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)。 用於開始使用 System.診斷追蹤和遠端除錯的分步教程。

影片：

- [容解安全:建譯可擴充的、有彈性的雲端服務](https://channel9.msdn.com/Series/FailSafe)。 由烏爾里希·霍曼、馬克·默庫里和馬克·西姆斯的九集系列。 以一種非常易訪問和有趣的方式展示高級概念和架構原則,從Microsoft客戶諮詢團隊 (CAT) 與實際客戶的經驗中得出的故事。 第 4 和第 9 集是關於監視和遙測的。 第 9 集包括監控服務 MetricsHub、AppDynamics、新遺物和尋呼業務概述。
- [構建大:從 Azure 客戶那裡吸取的經驗教訓 - 第二部分](https://channel9.msdn.com/Events/Build/2012/3-030)。 馬克·西姆斯談論為故障設計和檢測一切。 類似於故障安全系列,但進入更多如何使用的詳細資訊。

代碼範例:

- [Azure 的雲服務基礎知識](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 由 Microsoft Azure 客戶諮詢團隊創建的範例應用程式。 演示遙測和日誌記錄實踐,如以下文章中所述。 該示例使用[NLog](http://nlog-project.org/)實現應用程式日誌記錄。 有關相關文件,請參閱[有關遙測和紀錄記錄的四個 TechNet wiki 文章系列](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)。

> [!div class="step-by-step"]
> [前一個](design-to-survive-failures.md)
> [下一個](transient-fault-handling.md)
