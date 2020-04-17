---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: 設定與偵測微軟文件
author: rick-anderson
description: ASP.NET 2.0 中的配置和檢測發生了重大變化。 新的ASP.NET配置 API 允許進行配置更改。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: 30ea2ffd3d055c5373a33615bc19a8f68fb568ab
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543050"
---
# <a name="configuration-and-instrumentation"></a>設定與檢測

由[微軟](https://github.com/microsoft)

> ASP.NET 2.0 中的配置和檢測發生了重大變化。 新的ASP.NET配置 API 允許以程式設計方式進行配置更改。 此外,存在許多新的配置設置允許新的配置和檢測。

ASP.NET 2.0 中的配置和檢測發生了重大變化。 新的ASP.NET配置 API 允許以程式設計方式進行配置更改。 此外,存在許多新的配置設置允許新的配置和檢測。

在本模組中,我們將討論配置 API ASP.NET,因為它與讀取和寫入ASP.NET配置檔有關,我們還將討論ASP.NET檢測。 我們還將介紹ASP.NET跟蹤中提供的新功能。

## <a name="aspnet-configuration-api"></a>ASP.NET 設定 API

ASP.NET配置 API 允許您使用單個程式設計介面開發、部署和管理應用程式配置數據。 您可以使用設定 API 以程式設計方式開發和修改完整的 ASP.NET 配置,而無需直接編輯設定檔中的 XML。 此外,您可以在開發的應用程式和腳本、基於 Web 的管理工具以及 Microsoft 管理主控台 (MMC) 管理單元中使用配置 API。

以下兩個設定管理工具使用設定 API,並包含在 .NET 框架版本 2.0 中:

- mMC ASP.NET,它使用配置 API 簡化管理任務,提供來自配置層次結構所有級別的本地配置數據的整合檢視。
- 網站管理工具,允許您管理本地和遠端應用程式的設定設置,包括託管站點。

ASP.NET配置 API 包含一組ASP.NET管理物件,可用於以程式設計方式配置網站和應用程式。 管理物件作為 .NET 框架類庫實現。 配置 API 程式設計模型透過編譯時強制實施資料類型,有助於確保代碼的一致性和可靠性。 為了更輕鬆地管理應用程式配置,配置 API 允許您將從配置層次結構中的所有點合併的數據視為單個集合,而不是將數據視為來自不同配置檔的單獨集合。 此外,設定 API 讓您能夠操作整個應用程式設定,而無需直接編輯設定檔中的 XML。 最後,API 透過支援管理工具(如網站管理工具)來簡化配置任務。 配置 API 透過支援在電腦上創建設定檔並在多台電腦上運行配置腳本來簡化部署。

> [!NOTE]
> 配置 API 不支援創建 IIS 應用程式。

## <a name="working-with-local-and-remote-configuration-settings"></a>使用本地端與遠端設定設定

配置物件表示應用於特定實體實體(如電腦)或邏輯實體(如應用程式或網站)的配置設置的合併視圖。 指定的邏輯實體可以存在於本地電腦或遠端伺服器上。 當指定實體不存在設定檔時,配置物件表示由計算機.config 檔定義的預設設定設定。

使用以下類別的一個開啟的設定方法,可以取得設定物件:

1. 配置管理員(如果您的實體是用戶端應用程式)。
2. Web 設定管理員類別(如果您的實體是 Web 應用程式)。

這些方法將返回一個配置物件,該物件反過來提供了處理基礎配置檔所需的方法和屬性。 您可以造訪這些檔案進行讀取或寫入。

### <a name="reading"></a>讀取

您可以使用 GetSection 或 GetSectionGroup 方法讀取配置資訊。 讀取的使用者或進程必須對層次結構中的所有配置檔具有讀取許可權。

> [!NOTE]
> 如果使用採用路徑參數的靜態 GetSection 方法,則路徑參數必須引用運行代碼的應用程式。 否則,將忽略該參數,並返回當前正在運行的應用程式的配置資訊。

### <a name="writing"></a>撰寫

您可以使用 Save 方法之一來寫入設定資訊。 寫入的使用者或進程必須具有當前配置層次結構級別的配置檔和目錄的寫入許可權,以及層次結構中所有配置檔的讀取許可權。

要產生表示指定實體繼承的設定設定的設定檔,請使用以下儲存配置方法之一:

1. 建立新設定檔的儲存方法。
2. 保存 As 方法用於在另一個位置生成新的設定檔。

## <a name="configuration-classes-and-namespaces"></a>設定類別與命名空間

許多配置類和方法彼此相似。 下表描述了最常用的配置類和命名空間。

| **設定類別或命名空間** | **說明** |
| --- | --- |
| [系統.設定](https://msdn.microsoft.com/library/system.configuration.aspx)命名空間 | 包含所有 .NET 框架應用程式的主配置類。 節處理程式類用於從 GetSection 和 GetSectionGroup 等方法獲取節的配置數據。 這兩種方法是非靜態的。 |
| 系統.設定.設定類別 | 表示電腦、應用程式、Web 目錄或其他資源的一組配置數據。 此類包含用於更新配置設定和獲取對節和節組的引用的有用方法,如 GetSection 和 GetSectionGroup。 此類用作獲取設計時設定資料的方法的傳回類型,例如 Web 配置管理員和設定管理器 類的方法。 |
| 系統.Web.設定命名空間 | 包含ASP.NET[配置設定](https://msdn.microsoft.com/library/b5ysx397.aspx)中定義的ASP.NET配置部分的節處理程式類。 節處理程式類用於從 GetSection 和 GetSectionGroup 等方法獲取節的配置數據。 |
| 系統.Web.設定.Web配置管理員類別 | 提供了獲取對運行時和設計時配置設置引用的有用方法。 這些方法使用 System.配置.配置類作為返回類型。 您可以使用此類的靜態 GetSection 方法或系統的非靜態 GetSection 方法。 對於 Web 應用程式設定,建議使用 System.Web.配置.Web 配置管理器 類而不是系統.配置.配置管理器類。 |
| [系統.設定.提供者](https://msdn.microsoft.com/library/system.configuration.provider.aspx)命名空間 | 提供了一種自定義和擴展配置提供程式的方法。 這是配置系統中所有提供程式類的基類。 |
| [系統.Web.管理](https://msdn.microsoft.com/library/system.web.management.aspx)命名空間 | 包含用於管理和監視 Web 應用程式運行狀況的類和介面。 嚴格地說,此命名空間不被視為配置 API 的一部分。 例如,跟蹤和事件觸發由此命名空間中的類完成。 |
| [系統管理.偵測](https://msdn.microsoft.com/library/system.management.instrumentation.aspx)命名空間 | 提供應用程式檢測所需的類,以便通過 Windows 管理檢測 (WMI) 向潛在使用者公開其管理資訊和事件。 ASP.NET運行狀況監視使用 WMI 傳遞事件。 嚴格地說,此命名空間不被視為配置 API 的一部分。 |

## <a name="reading-from-aspnet-configuration-files"></a>從ASP.NET設定檔讀取

WebManagerManager 類是從ASP.NET配置檔讀取的核心類。 讀取ASP.NET設定檔基本上有三個步驟:

1. 使用 OpenWeb 設定方法獲取配置物件。
2. 獲取對設定檔中所需部分的引用。
3. 從配置檔中讀取所需的資訊。

配置物件表示不表示特定的配置檔。 相反,它表示計算機、應用程式或網站的配置的合併視圖。 以下代碼示例實例化表示名為*ProductInfo*的 Web 應用程式的配置的配置物件。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> 請注意,如果 /ProductInfo 路徑不存在,上述代碼將返回計算機中指定的默認配置。

獲得配置物件後,可以使用 GetSection 或 GetSectionGroup 方法深入瞭解配置設置。 以下範例取得對上述 ProductInfo 應用程式的模擬設定的參考:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>寫入ASP.NET設定檔

與從設定檔讀取一樣,WebManagerManager 類是寫入Asp.NET配置檔的核心。 還有三個步驟要寫入ASP.NET配置檔。

1. 使用 OpenWeb 設定方法獲取配置物件。
2. 獲取對設定檔中所需部分的引用。
3. 使用"儲存"或"儲存"方法從配置檔中寫入所需的資訊。

以下代碼將編譯&lt;&gt;元素的**除錯**屬性變更為 false:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

執行此代碼時&lt;,webApp&gt;應用程式的*Web.config*檔編譯元素的**調試**屬性將設置為 false。

## <a name="systemwebmanagement-namespace"></a>系統.Web.管理命名空間

System.Web.管理命名空間提供用於管理和監視ASP.NET應用程式的運行狀況的類和介面。

日誌記錄是通過定義將事件與提供程式關聯的規則來完成的。 規則定義發送到提供程式的事件類型。 以下基本事件可供您紀錄:

| **WebBase 事件** | 所有事件的基礎事件類。 包含所有事件(如事件代碼、事件詳細資訊代碼、引發事件的日期和時間、序列號、事件消息和事件詳細資訊)所需的屬性。 |
| --- | --- |
| **網路管理事件** | 管理事件的基本事件類,如應用程式存留期、請求、錯誤和審核事件。 |
| **網路偵測事件** | 應用程式以固定間隔生成的事件,用於捕獲有用的運行時狀態資訊。 |
| **網路審計事件** | 安全審核事件的基類,用於標記授權失敗、解密失敗*等條件。* |
| **Web請求事件** | 所有資訊請求事件的基類。 |
| **WebBase 錯誤事件** | 指示錯誤條件的所有事件的基類。 |

可用的提供程式類型允許您將事件輸出發送到事件查看器、SQL 伺服器、Windows 管理檢測 (WMI) 和電子郵件。 預先配置的提供程式和事件映射減少了記錄事件輸出所需的工作量。

ASP.NET 2.0 使用事件日誌提供程式開箱即用,基於應用程式域啟動和停止來記錄事件,以及記錄任何未處理的異常。 這有助於介紹一些基本方案。 例如,假設您的應用程式引發異常,但使用者不保存錯誤,並且無法重現它。 使用預設事件日誌規則,您將能夠收集異常和堆疊資訊,以便更好地瞭解發生了哪種錯誤。 如果應用程式正在失去會話狀態,則應用另一個示例。 在這種情況下,您可以在事件日誌中查看以確定應用程式域是否正在回收,以及應用程式域最初停止的原因。

此外,健康監測系統是可擴展的。 例如,可以定義自訂 Web 事件,在應用程式中觸發這些事件,然後定義一條規則,將事件資訊發送到提供者(如電子郵件)。 這允許您輕鬆地將檢測與運行狀況監視提供程式綁定。 作為另一個範例,您可以在每次處理訂單時觸發事件,並設置將每個事件發送到 SQL Server 資料庫的規則。 當用戶連續多次無法登錄時,還可以觸發事件,並將事件設置為使用基於電子郵件的提供程式。

預設提供程式和事件的配置存儲在全域 Web.config 檔中。 全域 Web.config 檔案將儲存在 Machine.config 檔中的所有基於 Web 的設定儲存在 ASP.NET 1x 中。 全域 Web.config 檔案位於以下目錄中:

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

全域&lt;Web.config 檔的運行狀況&gt;監視 部分提供預設配置設定。 您可以通過在 Web.config 檔中&lt;為應用程式實現&gt;執行狀況監視 部分來覆蓋這些設定或設定您自己的設定。

全域&lt;Web.config 檔的執行狀況&gt;監視 部份包含以下項目:

| **供應商** | 包含為事件查看器、WMI 和 SQL 伺服器設置的提供程式。 |
| --- | --- |
| **事件對應** | 包含各種 WebBase 類的映射。 如果生成自己的事件類,則可以擴展此清單。 生成自己的事件類可比向其發送資訊的提供程式提供更精細的粒度。 例如,您可以將未處理的異常配置為發送到 SQL Server,同時將您自己的自訂事件發送到電子郵件。 |
| **規則** | 將事件映射連結到提供程式。 |
| **緩衝** | 與 SQL Server 和電子郵件提供程式一起使用,以確定將事件刷新到提供程式的頻率。 |

下面是來自全域 Web.config 檔中的代碼範例。

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>如何將事件儲存到事件檢視器

如前所述,在全域 Web.config 檔中為您配置了用於在事件檢視器中記錄事件提供程式。 預設情況下,記錄基於**WebBaseErrorEvent**和**Web 失敗稽核事件的所有事件**。 您可以添加其他規則以將其他資訊記錄到事件日誌。 例如,如果要記錄所有事件(*即*基於**WebBaseEvent**的每個事件),可以向 Web.config 檔新增以下規則:

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

此規則會將 **「所有事件事件**」映射連結到事件日誌提供者。 事件映射和提供者都包含在全域 Web.config 檔中。

## <a name="how-to-store-events-to-sql-server"></a>如何儲存的事件儲存到 SQL 伺服器

此方法使用**ASPNETDB**資料庫,該資料庫由\_Aspnet regsql.exe 工具生成。 預設提供程式使用 LocalSqlServer 連接字串,該字串使用應用\_資料資料夾中的基於檔案的資料庫或 SQL Server 的本地 SQLExpress 實例。 本地SqlServer連接字串和 SqlProvider 都在全域 Web.config 檔中配置。

全域 Web.config 檔中的 LocalSqlServer 連接字串如下所示:

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

如果要使用另一個 SQL Server 實體,則需要使用\_Aspnet regsql.exe 工具,該工具可在 %windir%_Microsoft.Net_Framework_v2.0 中找到。\*資料夾。 使用 Aspnet\_regsql.exe 工具在 SQL Server 實體上生成自訂**ASPNETDB**資料庫,然後將連接字串添加到應用程式設定檔,然後使用新的連接字串添加提供者。 創建**ASPNETDB**資料庫後,需要設定規則以將事件映射連結到 sqlProvider。

無論是使用預設 SqlProvider 還是配置自己的提供程式,都需要添加一條規則,將提供程式與事件映射連結。 以下規則將上面創建的新提供程式連結到 **「所有事件」** 事件映射。 此規則將基於**WebBaseEvent**記錄所有事件,並將它們發送到將使用 MYASPNETDB 連接字串的 MySqlWebEvent 提供程式。 以下代碼新增了一條規則,用於將提供程式與事件映射連結:

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

如果只想向 SQL Server 傳送錯誤,可以新增以下規則:

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>如何將事件轉寄到 WMI

您還可以將事件轉發到 WMI。 預設情況下,WMI 提供程式在全域 Web.config 檔中為您配置。

以下代碼範例新增一條規則以將事件轉寄到 WMI:

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

您需要添加一個規則來將事件映射關聯到提供者,以及一個 WMI 偵聽器應用程式來偵聽事件。 以下代碼範例新增一條規則,將 WMI 提供程式連結到 **「所有事件」** 事件映射:

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>如何將事件轉寄到電子郵件

您還可以將事件轉發給電子郵件。 請注意您映射到電子郵件供應商的事件規則,因為您可能會無意中向自己發送大量可能更適合 SQL Server 或事件日誌的資訊。 有兩個電子郵件供應商;簡單郵件Web事件供應商和範本郵件Web事件供應商。 每個屬性具有相同的配置屬性,但「範本」和「詳細範本錯誤」屬性除外,這兩個屬性僅在範本IdmailWebEvent提供程式上可用。

> [!NOTE]
> 這些電子郵件提供程式均未為您配置。 您需要將它們添加到 Web.config 檔中。

這兩個電子郵件供應商之間的主要區別是 SimpleMailWebEventProvider 在無法修改的通用範本中發送電子郵件。 範例 Web.config 檔案使用以下規則將此電子郵件提供者新增到已設定提供者清單中:

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

還會新增以下規則以將電子郵件提供程式綁定到 **「所有事件」** 事件映射:

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 追蹤

在 2.0 ASP.NET中,跟蹤有三個主要增強功能。

1. 整合追蹤功能
2. 追蹤訊息的程式設計存取
3. 改進應用程式級追蹤

## <a name="integrated-tracing-functionality"></a>整合追蹤功能

現在,您可以將 System.Diagnostics.Trace 類發出的消息路由到ASP.NET跟蹤輸出,並將ASP.NET跟蹤發送的消息路由到 System.診斷.Trace。 您還可以將ASP.NET檢測事件轉發到 System.診斷.Trace。 此功能由&lt;追蹤&gt;元素的新**writeTo診斷追蹤**屬性提供。 當此布爾值為 true 時,ASP.NET跟蹤消息將轉發到 System.診斷跟蹤基礎結構,供註冊以顯示 Trace 消息的任何偵聽器使用。

## <a name="programmatic-access-to-trace-messages"></a>追蹤訊息的程式設計存取

ASP.NET 2.0 允許透過**TraceContextRecord**類和**追蹤記錄**集合對所有追蹤訊息進行程式設計存取。 訪問跟蹤消息的最有效方法是註冊**TraceContextEventHandler**委託(ASP.NET 2.0 中也是新的)來處理新的**跟蹤完成**事件。 然後,您可以根據需要循環訪問跟蹤消息。

以下代碼範例說明瞭這一點:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

在上面的示例中,我循環流覽跟蹤記錄集合,然後將每條消息寫入回應流。

## <a name="improved-application-level-tracing"></a>改進應用程式級追蹤

通過引入&lt;&gt;追蹤 元素的新**最新**屬性,應用程式級跟蹤得到了改進。 此屬性指定是否顯示最新的應用程式級跟蹤輸出,是否丟棄超出請求Limit 指示限制的較舊跟蹤數據。 如果為 false,則在達到請求 Limit 屬性之前,將顯示請求的追蹤數據。

## <a name="aspnet-command-line-tools"></a>ASP.NET 命令列工具

有幾個命令列工具可以説明配置ASP.NET。 ASP.NET開發人員應該熟悉 aspnet\_regiis.exe 工具。 ASP.NET 2.0 提供了另外三個命令列工具,以説明配置。

以下命令列工具可用:

| **工具** | **使用** |
| --- | --- |
| **阿斯普內\_雷吉斯.exe** | 允許在IIS註冊ASP.NET。 此工具有兩個版本附帶 ASP.NET 2.0,一個用於 32 位元系統(在 Framework 資料夾中),另一個用於 64 位元系統(在 Framework64 資料夾中)。64 位元版本將不會安裝在 32 位元作業系統上。 |
| **阿斯普內\_雷格斯** | ASP.NET SQL Server 註冊工具用於建立 Microsoft SQL Server 資料庫,供 ASP.NET中的 SQL Server 提供者使用,或從現有資料庫中添加或刪除選項。 Aspnet\_regsql.exe 檔案位於 Web 伺服器上的 [驅動器:]WINDOWS_Microsoft.NET_Framework_versionNumber 資料夾中。 |
| **阿斯普內\_註冊瀏覽器.exe** | ASP.NET瀏覽器註冊工具將所有系統範圍的瀏覽器定義解析和編譯到程式集中,並將程式集安裝到全域程式集緩存中。 該工具使用瀏覽器定義檔 (。BROWSER 檔案)來自 .NET 框架瀏覽器子目錄。 該工具可以在 %SystemRoot%\Microsoft.NET_Framework_version_目錄中找到。 |
| **阿斯普內\_編譯器.exe** | ASP.NET編譯工具使您能夠編譯ASP.NET Web 應用程式,無論是就位還是部署到目標位置(如生產伺服器)。 就地編譯有助於應用程式性能,因為最終使用者在編譯應用程式時不會遇到對應用程式的第一個請求的延遲。 |

由於 aspnet\_regiis.exe 工具對於 ASP.NET 2.0 並不新鮮,因此我們不會在此處討論它。

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>ASP.NET SQL 伺服器註冊\_工具 - aspnet regsql.exe

您可以使用ASP.NET SQL 伺服器註冊工具設置多種類型的選項。 可以指定 SQL 連接,指定哪些 ASP.NET 應用程式服務使用 SQL Server 來管理資訊,指示哪個資料庫或表用於 SQL 快取依賴項,以及添加或刪除對使用 SQL Server 儲存過程和工作階段狀態的支援。

多個ASP.NET應用程式服務依賴於提供程式來管理從資料源存儲和檢索數據。 每個提供程式都特定於數據源。 ASP.NET包括用於以下ASP.NET功能的 SQL Server 提供者:

- 成員資格[(Sqlsasprovider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)類)。
- 角色管理[(SqlRole Provider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)類)。
- 設定檔[(SqlProfile Provider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx)類)。
- Web 部件個人化[(Sql 個人化提供程式](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx)類)。
- Web 事件[(SqlWebEvent 提供程式](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx)類)。

安裝ASP.NET時,伺服器的Machine.config檔包括配置元素,這些元素為依賴於提供程式的每個ASP.NET功能指定SQL Server提供程式。 默認情況下,這些提供程式配置為連接到 SQL Server Express 2005 的本地使用者實例。 如果更改提供者使用的預設連接字串,則在使用電腦配置中配置的任何ASP.NET功能之前,必須使用 Aspnet\_regsql.exe 安裝 SQL Server 資料庫和所選功能的資料庫元素。 如果使用 SQL 註冊工具指定的資料庫不存在(如果在命令列上未指定資料庫,則 aspnetdb 將是預設資料庫),則當前使用者必須有權在 SQL Server 中創建資料庫以及在資料庫中創建架構元素。

### <a name="sql-cache-dependency"></a>SQL 快取相依性

ASP.NET輸出緩存的高級功能是 SQL 快取依賴項。 SQL 緩存依賴項支援兩種不同的操作模式:一種是使用表輪詢ASP.NET實現,另一種模式使用 SQL Server 2005 的查詢通知功能。 SQL 註冊工具可用於配置表輪詢操作模式。

### <a name="session-state"></a>工作階段狀態

默認情況下,會話狀態值和資訊存儲在ASP.NET進程中的記憶體中。 或者,您可以將會話數據存儲在 SQL Server 資料庫中,其中會話數據可以由多個 Web 伺服器共用。 如果使用 SQL 註冊工具為工作階段狀態指定的資料庫不存在,則當前使用者必須有權在 SQL Server 中創建資料庫以及在資料庫中創建架構元素。 如果資料庫確實存在,則當前用戶必須有權在現有資料庫中創建架構元素。

在 SQL Server 上安裝工作階段狀態資料庫\_,請執行 Aspnet regsql.exe 工具,並隨命令提供以下資訊:

- 使用 **-S**選項的 SQL Server 實體名稱。
- 具有在運行 SQL Server 的電腦上創建資料庫的許可權的帳戶的登錄認證。 使用 **-E**選項使用目前登入的使用者,或使用 **-U**選項指定使用者 ID 以及 **-P**選項來指定密碼。
- **-ssadd**命令行選項用於添加會話狀態資料庫。

預設情況下,不能使用 Aspnet\_regsql.exe 工具在運行 SQL Server 2005 Express 版的電腦上安裝作業階段狀態資料庫。

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>ASP.NET瀏覽器註冊工具 -\_阿斯網 註冊瀏覽器.exe

在ASP.NET版本 1.1 中,Machine.config&lt;檔&gt;包含一個稱為瀏覽器Cap 的部分。 本節包含一系列 XML 條目,這些條目根據正則表達式定義了各種瀏覽器的配置。 對於ASP.NET版本 2.0,一個新的 。BROWSER 檔案使用 XML 項目定義特定瀏覽器的參數。 通過添加新 的瀏覽器,可以添加新 瀏覽器上的資訊。BROWSER 檔案到位於系統上 %SystemRoot%_Microsoft.NET_Framework_conFIG_瀏覽器的資料夾。

因為應用程式每次需要瀏覽器資訊時都未讀取 .config 檔案,因此您可以建立新的 。BROWSER 檔和執行 Aspnet\_註冊瀏覽器.exe 以向程式集添加所需的更改。 這允許伺服器立即存取新的瀏覽器資訊,因此您不必關閉任何應用程式來獲取資訊。 應用程式可以通過當前 HttpRequest 的瀏覽器屬性訪問瀏覽器功能。

執行 aspnet\_regbrowser.exe 時,以下選項可用:

| **選項** | **說明** |
| --- | --- |
| **-?** | 在命令視窗中顯示\_Aspnet regb 瀏覽器.exe 幫助文字。 |
| **-i** | 建立運行時瀏覽器功能程式集並將其安裝到全域程式集緩存中。 |
| **-u** | 從全域程式集緩存卸載運行時瀏覽器功能程式集。 |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>ASP.NET編譯工具 -\_阿斯普 內編譯器.exe

ASP.NET編譯工具可通過兩種常規方式使用:用於就地編譯和編譯以進行部署,其中指定了目標輸出目錄。

### <a name="compiling-an-application-in-place"></a>[編譯就地的應用程式](https://msdn.microsoft.com/library/ms229863.aspx)

ASP.NET編譯工具可以就地編譯應用程式,即模仿對應用程式發出多個請求的行為,從而導致定期編譯。 預編譯網站的使用者不會因為在第一次請求時編譯頁面而遇到延遲。

在就位預編譯網站時,應用以下項:

- 該網站保留其文件和目錄結構。
- 您必須具有伺服器上站點使用的所有程式設計語言的編譯器。
- 如果任何檔編譯失敗,則整個網站將失敗編譯。

在向應用程式添加新源檔後,還可以重新編譯應用程式。 該工具僅編譯新的或更改的檔案,除非您包含 **-c**選項。

> [!NOTE]
> 包含嵌套應用程式的應用程式的編譯不會編譯嵌套應用程式。 嵌套應用程序必須單獨編譯。

### <a name="compiling-an-application-for-deployment"></a>[編譯應用程式進行部署](https://msdn.microsoft.com/library/ms229863.aspx)

通過指定目標Dir參數,編譯用於部署的應用程式(編譯到目標位置)。 目標 Dir 可以是 Web 應用程式的最終位置,也可以進一步部署編譯的應用程式。 使用 **-u**選項編譯應用程式的方式,您可以更改編譯應用程式中的某些檔,而無需重新編譯它。 Aspnet\_編譯器.exe 區分靜態和動態文件類型,並在創建生成的應用程式時以不同的方式處理它們。

- 靜態檔類型是那些沒有關聯的編譯器或生成提供程式的檔,例如其命名具有擴展名的檔,如 .css、.gif、.htm、.html、.jpg、.js 等。 這些檔只是複製到目標位置,並保留其在目錄結構中的相對位置。
- 動態檔類型是具有關聯編譯器或生成提供程式的檔,包括具有ASP.NET特定檔名擴展名的檔,如 .asax、.ascx、.ashx、.aspx、.browser、.master 等。 ASP.NET編譯工具從這些檔生成程式集。 如果省略 **-u**選項,該工具還會創建檔案名擴展名的檔。將原始源檔映射到其程式集的 COMPILE。 為了確保保留應用程式源的目錄結構,該工具會在目標應用程式中的相應位置生成占位符檔。

您必須使用 **-u**選項來指示可以修改已編譯應用程式的內容。 否則,後續修改將被忽略或導致運行時錯誤。

下表描述了在包含 **-u**選項時,ASP.NET編譯工具如何處理不同的檔案類型。

| **檔案類型** | **編譯器操作** |
| --- | --- |
| .ascx, .aspx, .master | 這些檔被拆分為標記和原始程式碼,其中包括代碼背後的檔和包含在腳本 runat_「server」&lt;&gt;元素中的任何代碼。 原始程式碼被編譯成程式集,名稱派生自哈希演演演算法,並且程式集放置在 Bin 目錄中。 任何內聯代碼,即包含在 括**&lt;** 弧**%** 和 括弧之間的代碼,都包含在標記中,並且未編譯。 建立與源檔同名的新檔以包含標記並放置在相應的輸出目錄中。 |
| .ashx, .asmx | 這些檔不會編譯,並且會移動到輸出目錄,以現在和未編譯。 如果希望編譯處理程式代碼,請將代碼放入\_App Code 目錄中的原始程式碼檔中。 |
| .cs, .vb, .jsl, .cpp (不包括前面列出的檔案類型的代碼後檔案) | 這些檔被編譯並作為引用它們的程式集中的資源包含在其中。 源檔不會複製到輸出目錄。 如果未引用代碼檔,則不編譯它。 |
| 自訂檔案類型 | 這些檔未編譯。 這些檔將複製到相應的輸出目錄。 |
| 套\_用程式碼子目錄中的原始碼檔案 | 這些檔被編譯成程式集並放置在 Bin 目錄中。 |
| .resx 和 .資源\_檔案在 套用全域資源子目錄 | 這些檔被編譯成程式集並放置在 Bin 目錄中。 在主\_輸出目錄下不建立應用全域資源子目錄,並且源目錄中的 .resx 或 .resource 檔不會複製到輸出目錄。 |
| .resx 和 .資源\_檔案在套用資源子目錄 | 這些檔不會編譯,並複製到相應的輸出目錄。 |
| 套\_用 主題子目錄中 .skin 檔案 | .skin 檔和靜態主題檔不會編譯,並複製到相應的輸出目錄。 |
| .browser Web.config 靜態檔案類型 程式集已存在於 Bin 目錄中 | 這些檔將像一樣複製到輸出目錄。 |

下表描述了在省略 **-u**選項時,ASP.NET編譯工具如何處理不同的文件類型。

| **檔案類型** | **編譯器操作** |
| --- | --- |
| .aspx, .asmx, .ashx, .master | 這些檔被拆分為標記和原始程式碼,其中包括代碼背後的檔和包含在腳本 runat_「server」&lt;&gt;元素中的任何代碼。 原始程式碼被編譯成程式集,名稱派生自哈希演演演算法。 生成的程式集放置在 Bin 目錄中。 任何內聯代碼,即包含在 括**&lt;** 弧**%** 和 括弧之間的代碼,都包含在標記中,並且未編譯。 編譯器創建新檔以包含與源檔同名的標記。 這些生成的檔放置在 Bin 目錄中。 編譯器還創建與源檔同名但具有擴展名的檔。包含映射資訊的 COMPILED。 .COMPILED 檔案放置在與源檔的原始位置對應的輸出目錄中。 |
| .ascx | 這些檔被拆分為標記和原始碼。 原始程式碼被編譯成程式集並放置在 Bin 目錄中,名稱派生自哈希演演演算法。 不生成標記檔。 |
| .cs, .vb, .jsl, .cpp (不包括前面列出的檔案類型的代碼後檔案) | 由 .ascx、.ashx 或 .aspx 檔生成的程式集引用的原始碼被編譯到程式集中並放置在 Bin 目錄中。 不會複製任何源檔。 |
| 自訂檔案類型 | 這些檔像動態檔一樣編譯。 根據它們所基於的文件類型,編譯器可以將映射檔放置在輸出目錄中。 |
| 套\_用程式碼子目錄中檔案 | 此子目錄中的原始碼檔被編譯到程式集中並放置在 Bin 目錄中。 |
| 套\_用全域資源子目錄中的檔案 | 這些檔被編譯成程式集並放置在 Bin 目錄中。 在主\_輸出目錄下不創建應用全域資源子目錄。 如果設定檔指定應用於"全部",則 .resx 和 .resources 檔將複製到輸出目錄。 如果[生成提供程式](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)引用它們,則不複製它們。 |
| .resx 和 .資源\_檔案在套用資源子目錄 | 這些檔被編譯到具有唯一名稱的程式集中,並放置在 Bin 目錄中。 沒有 .resx 或 .resource 檔案複製到輸出目錄。 |
| 套\_用 主題子目錄中 .skin 檔案 | 主題被編譯到程式集中並放置在 Bin 目錄中。 為 .skin 檔案創建存根檔,並放置在相應的輸出目錄中。 靜態檔(如 .css)將複製到輸出目錄。 |
| .browser Web.config 靜態檔案類型 程式集已存在於 Bin 目錄中 | 這些檔將照樣複製到輸出目錄。 |

### <a name="fixed-assembly-names"></a>[固定程式集名稱](https://msdn.microsoft.com/library/ms229863.aspx##)

某些方案(如使用 MSI Windows 安裝程式部署 Web 應用程式)需要使用一致的檔名和內容,以及一致的目錄結構來識別更新的程式集或配置設置。 在這些情況下,可以使用 **-固定名稱**選項指定ASP.NET編譯工具應為每個源檔編譯程式集,而不是使用將多個頁面編譯到程式集中的位置。 這可能導致大量程式集,因此,如果您擔心可伸縮性,則應謹慎使用此選項。

### <a name="strong-name-compilation"></a>[強名稱編譯](https://msdn.microsoft.com/library/ms229863.aspx##)

\_提供 -aptca、-delaysign、-**鍵容器**和 **-鍵檔案**選項,以便您可以使用 Aspnet 編譯器.exe 創建強命名程式集,而無需單獨使用[強名稱工具 (Sn.exe)。](https://msdn.microsoft.com/library/k5b5tt23.aspx) **-aptca** **-delaysign** 這些選項以**允許部份信任的呼叫者屬性**、**程式集延遲屬性**、**程式集 KeyName 屬性**與**程式集金鑰檔案屬性**。

討論這些屬性超出了本課程的範圍。

## <a name="labs"></a>實驗室

以下每個實驗室都基於以前的實驗室。 你需要按順序做它們。

## <a name="lab-1-using-the-configuration-api"></a>實驗 1:使用設定 API

1. 創建一個名為*mod9lab*的新網站。
2. 向網站添加新的 Web 配置檔。
3. 將以下內容加入到 Web.config 檔案:

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

這將確保您具有保存對 Web.config 檔更改的許可權。

1. 將新的 Label 控制項添加到 Default.aspx 並將 ID 更改為**lblDebugStatus。**
2. 將新的按鈕控制項添加到 Default.aspx。
3. 將按鈕控制項的 ID 變更為**btnToggleDebug**與「文字」來**切換除錯狀態**。
4. 開啟 Default.aspx 的代碼背後檔的代碼檢視,並為**System.Web.設定**添加**using**語句,如下所示:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. 新增兩個私有變數和一個\_Page Init 方法,如下所示:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. 將以下代碼加入頁面\_載入:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. 保存和流覽預設值.aspx。 請注意,"標籤"控制器顯示當前調試狀態。
2. 按兩下設計器中的「按鈕」控制項,並將以下代碼加入到 Button 控制項的 Click 事件:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. 保存並瀏覽預設.aspx,然後單擊該按鈕。
2. 按下每個按鈕後打開 Web.config 檔**debug**,&lt;並觀察&gt;編譯 部分中的調試屬性。

## <a name="lab-2-logging-application-restarts"></a>實驗 2:記錄應用程式重新啟動

在本實驗中,您將建立代碼,以允許您在事件查看器中切換應用程式關閉、啟動和重新編譯的日誌記錄。

1. 將下拉清單添加到預設.aspx,並將 ID 更改為 ddlLogApp 事件。
2. 將下拉清單的**自動 PostBack**屬性設定為**true**。
3. 將三個專案添加到下拉清單的「專案」集合中。 使第一個項目**的文本***選擇值*和值 -1。 將**文字與****值**為**true,** 並使第三個的**文字**與**值****為 false**。
4. 將新標籤添加到預設.aspx。 將 ID 變更為**lblLogApp 事件**。
5. 打開 default.aspx 的代碼後面檢視,並為類型為 Health 監視節的變數添加新聲明,如下所示:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. 將以下代碼加入到頁\_Init 中的現有代碼:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. 按兩下下拉清單,並將以下代碼添加到「選定索引更改」事件:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. 瀏覽預設值.aspx。
2. 將下拉設定為**False**。
3. 清除事件檢視器中的應用程式日誌。
4. 按一下這個按鈕可更改應用程式的除錯屬性。
5. 刷新事件檢視器中的應用程式日誌。 

    1. 是否有任何事件被記錄?
    2. 為什麼或為什麼不?
6. 將下拉清單設置為 **「True」。**
7. 按這裏按鈕可切換應用程式的除錯屬性。
8. 刷新應用程式登錄事件檢視器。 

    1. 是否有任何事件被記錄?
    2. 應用關閉的原因是什麼?
9. 嘗試打開和關閉日誌記錄,並查看對 Web.config 檔所做的更改。

## <a name="more-information"></a>其他相關資訊：

ASP.NET 2.0 的提供程式模型允許您不僅為應用程式檢測創建自己的提供程式,還可用於許多其他用途,如成員資格、配置檔等。有關編寫自訂提供應用程式將應用程式事件記錄到文字檔的詳細資訊,請造[訪 此連結](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp)。
