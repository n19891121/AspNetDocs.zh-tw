---
uid: visual-studio/overview/2013/release-notes
title: 視覺工作室ASP.NET和網络工具 2013 發行說明 |微軟文件
author: rick-anderson
description: 本文檔介紹了 2013 年可視化工作室的 ASP.NET 和網路工具的發布。
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 4494b4acdd30384e1def89b7fff9bad30933e38e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543492"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>適用於 Visual Studio 2013 的 ASP.NET 和 Web 工具版本資訊

由[微軟](https://github.com/microsoft)

> 本文檔介紹了 2013 年可視化工作室的 ASP.NET 和網路工具的發布。

## <a name="contents"></a>內容

- [安裝說明](#TOC1)
- [文件](#TOC2)
- [軟體要求](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>2013年可視化工作室ASP.NET和網路工具的新功能

- [一ASP.NET](#TOC6)
- [新的 Web 專案體驗](#newproj)
- [ASP.NET腳手架](#scaffold)
- [瀏覽器連結](#browser-link)
- [視覺化工作室 Web 編輯器增強功能](#web-editor)
- [Visual Studio 中的 Azure 應用服務 Web 應用支援](#waws)
- [Web 發佈增強功能](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET Web 表單](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET Web API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET身份](#TOC8)
- [Microsoft OWIN 元件](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET剃刀 3](#TOC14)
- [ASP.NET應用程式掛起](#TOC15)
- [已知問題和重大變更](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>安裝注意事項

ASP.NET和Web工具為可視化工作室2013捆綁在主安裝程式,可以[在這裡](https://www.asp.net/downloads)下載。

<a id="TOC2"></a>
## <a name="documentation"></a>文件

有關 visual Studio 2013 的 ASP.NET 和 Web 工具的教程和其他資訊可從[ASP.NET 網站](https://www.asp.net/)獲得。

<a id="TOC4"></a>
## <a name="software-requirements"></a>軟體需求

ASP.NET和網路工具需要可視化工作室 2013。

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>2013年可視化工作室ASP.NET和網路工具的新功能

以下各節介紹版本中引入的功能。

<a id="TOC6"></a>
## <a name="one-aspnet"></a>一ASP.NET

隨著 Visual Studio 2013 的發表,我們朝著統一使用 ASP.NET 技術的經驗邁出了一步,以便您可以輕鬆混合和匹配所需的技術。 例如,可以使用 MVC 啟動專案,並在以後輕鬆地將 Web 窗體頁添加到專案,或在 Web 窗體專案中基架 Web API 中。 一ASP.NET就是讓你作為開發人員更容易在ASP.NET中做你喜歡的事情。 無論您選擇何種技術,您都可以確信自己正在構建"一ASP.NET"的可信底層框架。

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>新的 Web 專案體驗

我們在 Visual Studio 2013 中增強了創建新 Web 專案的經驗。 在 **「新建ASP.NET Web 專案**」對話框中,您可以選擇所需的項目類型、配置任何技術組合(Web 窗體、MVC、Web API)、設定身份驗證選項以及添加單元測試專案。

![新ASP.NET專案](release-notes/_static/image1.png)

新的對話框使您能夠更改許多範本的預設身份驗證選項。 例如,在建立ASP.NET Web 窗體專案時,您可以選擇以下任一選項:

- 不需要驗證
- 個人使用者帳戶(ASP.NET會員身份或社交提供者登入)
- 組織帳號 (網路應用程式中的活動目錄)
- Windows 驗證(Intranet 應用程式中的活動目錄)

![驗證選項](release-notes/_static/image2.png)

有關建立 Web 專案的新流程的詳細資訊,請參閱在[Visual Studio 2013 建立 ASP.NET Web 專案](creating-web-projects-in-visual-studio.md)。 關於新身份驗證選項的詳細資訊,請參考此文件後面的[ASP.NET 識別](#TOC8)。

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET腳手架

ASP.NET基架是ASP.NET Web 應用程式的代碼生成框架。 它可以輕鬆地向與數據模型交互的專案添加樣板代碼。

在 Visual Studio 的早期版本中,基架僅限於 ASP.NET MVC 專案。 借助 Visual Studio 2013,您現在可以對任何 ASP.NET 專案(包括 Web 窗體)使用基架。 Visual Studio 2013 目前不支援為 Web 窗體專案生成頁面,但您仍可以通過向專案添加 MVC 依賴項來使用 Web 窗體的腳手架。 將在將來的更新中添加對生成 Web 窗體頁面的支援。

使用基架時,我們確保在專案中安裝了所有必需的依賴項。 例如,如果從ASP.NET Web 窗體專案開始,然後使用基架添加 Web API 控制器,則所需的 NuGet 包和引用將自動添加到專案中。

要將 MVC 基架加入 Web 窗體專案,請新增**新的文手架,** 並在對話框視窗中選擇**MVC 5 相依項 。** 基架 MVC 有兩個選項;最小和完整。 如果選擇「最小」,則只有 ASP.NET MVC 的 NuGet 包和引用添加到專案中。 如果選擇"完整"選項,則添加最小依賴項以及 MVC 專案所需的內容檔。

支援基架非同步控制器使用實體框架6中的新異步功能。

有關詳細資訊和教程,請參閱[ASP.NET 腳手架概述](aspnet-scaffolding-overview.md)。

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>瀏覽器連結 + 瀏覽器和視覺化工作室之間的訊號R通道

新的[瀏覽器連結](using-browser-link.md)功能允許您將多個瀏覽器連接到 Visual Studio,並透過單擊工具列中的按鈕刷新所有瀏覽器。 您可以將多個瀏覽器連接到開發網站(包括移動模擬程式),然後單擊刷新以同時刷新所有瀏覽器。 瀏覽器連結還公開 API,使開發人員能夠編寫瀏覽器連結擴展。

![](release-notes/_static/image3.png)

通過使開發人員能夠利用瀏覽器連結 API,可以創建非常高級的方案,這些方案跨越 Visual Studio 和任何已連接的瀏覽器之間的邊界。 Web Essentials 利用 API 在 Visual Studio 和瀏覽器的開發人員工具、遠端控制行動模擬器等之間創建整合體驗。

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>視覺化工作室 Web 編輯器增強功能

Visual Studio 2013 包括用於 Web 應用程式中 Razor 檔案和 HTML 檔案的新 HTML 編輯器。 新的 HTML 編輯器提供基於 HTML5 的單一架構。 它有自動大括弧完成,jQuery UI和AngularJS屬性IntelliSense,屬性IntelliSense分組,ID和類名Intellisense,和其他改進,包括更好的性能,格式和智慧標籤。

以下螢幕截圖示範如何在 HTML 編輯器中使用 Bootstrap 屬性 IntelliSense。

![HTML 編輯器中的感知](release-notes/_static/image4.png)

Visual Studio 2013 還附帶了內置的咖啡腳本和 LESS 編輯器。 LESS 編輯器附帶了 CSS 編輯器中的所有很酷的功能,@import並具有針對鏈中所有 LESS 文件中的變數和混合值的特定 Intellisense。

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Visual Studio 中的 Azure 應用服務 Web 應用支援

在 Visual Studio 2013 中,使用用於 .NET 2.2 的 Azure SDK,可以使用**伺服器資源管理器**直接與遠端 Web 應用進行交互。 您可以登錄到 Azure 帳戶、創建新的 Web 應用、配置應用、查看即時日誌等。 SDK 2.2 發佈後不久,您將能夠在 Azure 中遠端在調試模式下運行。 安裝 .NET 的 Azure SDK 當前版本時,Azure 應用服務 Web 應用的大多數新功能在 Visual Studio 2012 中也起作用。

如需詳細資訊，請參閱下列資源：

- [在 Azure 應用服務中建立ASP.NET Web 應用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [使用 Visual Studio 疑難排解 Azure App Service 中的 Web 應用程式](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>Web 發佈增強功能

Visual Studio 2013 包括新的和增強的 Web 發佈功能。 以下提供其中一些範例：

- 輕鬆[自動進行 Web.config 檔案加密](https://go.microsoft.com/fwlink/?LinkId=325529)。 (此連結和以下兩個指向 MSDN 上的文檔,這些文檔可能直到 10 月 17 日深夜才可用。
- 在[部署期間輕鬆自動讓應用程式離線](https://go.microsoft.com/fwlink/?LinkId=325530)。
- 將 Web 部署設定為[使用檔案校驗和,而不是上次更改的日期](https://go.microsoft.com/fwlink/?LinkId=325531),以確定應複製到伺服器的檔。
- 使用 FTP 或檔案系統發佈方法以及 Web 部署時,快速發表單個選定檔(包括 Web.config)。

有關ASP.NET Web 部署的詳細資訊,請參閱[ASP.NET網站](https://go.microsoft.com/fwlink/?LinkId=322027)。

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7 包含一組豐富的新功能,在[NuGet 2.7 發行說明](http://docs.nuget.org/docs/release-notes/nuget-2.7)中對此進行了詳細介紹。

此版本的 NuGet 還無需為 NuGet 的包還原功能提供下載包的明確同意。 現在透過安裝 NuGet 授予同意(以及 NuGet 首選項對話方塊中的關聯複選框)。 現在,默認情況下,包還原只是工作。

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

### <a name="one-aspnet"></a>一ASP.NET

Web 窗體專案範本與新 one ASP.NET 體驗無縫集成。 您可以將 MVC 和 Web API 支援添加到 Web 窗體專案中,並且可以使用「一ASP.NET專案創建嚮導設定身份驗證。 有關詳細資訊,請參閱在[Visual Studio 2013 中建立 ASP.NET Web 專案](creating-web-projects-in-visual-studio.md)。

### <a name="aspnet-identity"></a>ASP.NET Identity

Web 表單樣專案樣本支援新的ASP.NET識別架構。 此外,範本現在支援創建 Web 窗體 Intranet 專案。 有關詳細資訊,請參閱在**Visual Studio 2013 中建立 ASP.NET Web 專案的**[認證方法](creating-web-projects-in-visual-studio.md#auth)。

### <a name="bootstrap"></a>啟動程序

Web 表單表板使用[Bootstrap](http://twitter.github.io/bootstrap/)提供時尚且回應迅速的外觀,讓您輕鬆自定義。 有關詳細資訊,請參閱[Visual Studio 2013 Web 專案範本中的 Bootstrap。](creating-web-projects-in-visual-studio.md#bootstrap)

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>一ASP.NET

Web MVC 專案範本與新一ASP.NET體驗無縫整合。 您可以使用「一ASP.NET項目創建嚮導自定義 MVC 專案並設定身份驗證。 ASP.NET MVC 5 的入門教程可以在[ASP.NET MVC 5 入門](../../../mvc/overview/getting-started/introduction/getting-started.md)中找到。

有關將 MVC 4 專案升級到 MVC 5 的資訊,請參閱[如何將 ASP.NET MVC 4 和 Web API 專案升級到 ASP.NET MVC 5 和 Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。

### <a name="aspnet-identity"></a>ASP.NET Identity

MVC 專案範本已更新,用於ASP.NET標識進行身份驗證和標識管理。 一個教程,包括Facebook和谷歌認證和新的會員API可以在[創建ASP.NETMVC 5應用程式與Facebook和谷歌OAuth2和OpenID登錄](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md),[並建立ASP.NETMVC應用程式與auth和SQL DB,並部署到Azure應用程式服務](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。

### <a name="bootstrap"></a>啟動程序

MVC 專案範本已更新,可使用[Bootstrap](http://getbootstrap.com/)提供時尚且回應迅速的外觀,讓您輕鬆自定義。 有關詳細資訊,請參閱[Visual Studio 2013 Web 專案範本中的 Bootstrap。](creating-web-projects-in-visual-studio.md#bootstrap)

### <a name="authentication-filters"></a>驗證篩選器

身份驗證篩選器是 ASP.NET MVC 中一種新型篩選器,在 ASP.NET MVC 管道中的授權篩選器之前運行,允許您為所有控制器指定每個操作、每個控制器或全域的身份驗證邏輯。 身份驗證篩選器處理請求中的憑據並提供相應的主體。 身份驗證篩選器還可以添加身份驗證質詢以回應未經授權的請求。

### <a name="filter-overrides"></a>篩選器覆寫

現在,可以通過指定覆蓋篩選器來覆蓋應用於給定操作方法或控制器的篩選器。 覆蓋篩選器指定一組不應為給定作用域(操作或控制器)運行的篩選器類型。 這允許您配置全域應用的篩選器,但隨後排除某些全域篩選器應用於特定操作或控制器。

### <a name="attribute-routing"></a>屬性路由

ASP.NET MVC 現在支援屬性路由,這要歸[http://attributerouting.net](http://attributerouting.net)功於 Tim McCall(作者)的貢獻。 使用屬性路由,您可以通過對操作和控制器進行說明來指定路由。

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>屬性路由

ASP.NET Web API 現在支援屬性路由,這要[http://attributerouting.net](http://attributerouting.net)歸功於 Tim McCall(作者)的貢獻。 使用屬性路由,您可以通過指定操作和控制器來指定 Web API 路由,如下所示:

[!code-csharp[Main](release-notes/samples/sample1.cs)]

屬性路由使您能夠對 Web API 中的 URI 進行更多控制。 例如,您可以使用單個 API 控制器輕鬆定義資源層次結構:

[!code-csharp[Main](release-notes/samples/sample2.cs)]

屬性路由還提供用於指定可選參數、預設值和路由約束的便捷語法:

[!code-csharp[Main](release-notes/samples/sample3.cs)]

有關屬性路由的詳細資訊,請參閱[Web API 2 中的屬性路由](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)。

### <a name="oauth-20"></a>OAuth 2.0

Web API 和單頁應用程式專案範本現在支援使用 OAuth 2.0 進行授權。 OAuth 2.0 是一個用於授權客戶端訪問受保護資源的框架。 它適用於各種用戶端,包括瀏覽器和行動裝置。

對 OAuth 2.0 的支援基於 Microsoft OWIN 元件為承載身份驗證和實現授權伺服器角色而提供的新安全中間件。 或者,可以使用組織授權伺服器(如 Windows Server 2012 R2 中的 Azure 活動目錄或 ADFS)授權用戶端。

### <a name="odata-improvements"></a>O 資料改進

**支援$select、$expand、$batch和$value**

ASP.NET Web API OData 現在完全支援$select、$expand和$value。 您還可以使用$batch請求批處理和處理更改集。

$select和$expand選項允許您更改從 OData 終結點傳回的數據的形狀。 有關詳細資訊,請參閱在[Web API OData 中介紹$select 和$expand支援](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)。

**提高可擴充性**

OData for 物質現在可擴展。 您可以添加 Atom 條目元數據、支援命名串流和媒體連結項目、添加實例註釋以及自訂連結的生成方式。

**沒有類型支援**

現在,您可以構建 OData 服務,而無需為實體類型定義 CLR 類型。 相反,您的 OData 控制器可以獲取或返回**IEdmObject**的實例 ,這是用於序列化/反序列化的 OData 實例。

**重用現有模型**

如果您已有現有的實體數據模型 (EDM),現在可以直接重用它,而不必構建新的實體數據模型。 例如,如果您使用的是實體框架,則可以使用 EF 為您生成的 EDM。

### <a name="request-batching"></a>要求處理

請求批處理將多個操作合併到單個 HTTP POST 請求中,以減少網路流量並提供更順暢、更不健談的使用者介面。 ASP.NET Web API 現在支援幾種要求批次處理策略:

- 使用 OData 服務$batch終結點。
- 將多個請求打包到單個 MIME 多部分請求中。
- 使用自定義批處理格式。

要啟用要求批次處理,只需將具有批次處理處理程式的路由新增到 Web API 設定中:

[!code-csharp[Main](release-notes/samples/sample4.cs)]

您還可以控制請求或按順序執行,還是按任何順序執行。

### <a name="portable-aspnet-web-api-client"></a>可移植ASP.NET Web API 用戶端

現在,可以使用ASP.NET Web API 用戶端創建跨 Windows 應用商店和 Windows Phone 8 應用程式的便攜式類庫。 您還可以創建可在用戶端和伺服器之間共用的可移植的要件。

### <a name="improved-testability"></a>提高可測試性

Web API 2 使單元測試 API 控制器變得更加容易。 只需使用請求消息和配置實例化 API 控制器,然後調用要測試的操作方法。 對於執行連結生成的操作方法,也很容易類比**UrlHelper**類。

### <a name="ihttpactionresult"></a>IHTTPAction 結果

現在,您可以實現 IHttpActionResult 來封裝 Web API 操作方法的結果。 從 Web API 操作方法傳回的 IHttpActionResult 由 ASP.NET Web API 執行時執行,以生成產生的回應消息。 可以從任何 Web API 操作傳回 IHttpActionResult,以簡化 Web API 實現單元測試。 為方便起見,一些IHttpActionResult實現在開箱即用,包括用於返回特定狀態代碼、格式化內容或內容協商回應的結果。

### <a name="httprequestcontext"></a>HTTPRequestContext

新的**HttpRequestContext**追蹤與請求關聯的任何狀態,但無法立即從請求中獲取。 例如,可以使用**HttpRequestContext**獲取路由資料、與請求關聯的主體、用戶端證書 **、UrlHelper**和虛擬路徑根。 您可以輕鬆地為單元測試目的創建**HTTPRequestContext。**

由於請求的主體隨請求一起流動,而不是依賴於**Thread.CurrentThe,** 因此主體現在在請求在 Web API 管道中時在請求的整個生存期內可用。

### <a name="cors"></a>CORS

多虧了布羅克·艾倫的另一個巨大貢獻,ASP.NET現在完全支援跨原請求共用 (CORS)。

瀏覽器安全性可防止網頁對另一個網域提出 AJAX 要求。 [CORS](http://www.w3.org/TR/cors/)是一種 W3C 標準,允許伺服器放鬆同源策略。 使用 CORS，伺服器可以明確允許某些跨源要求，然而拒絕其他要求。

Web API 2 現在支援 CORS,包括自動處理預檢請求。 如需詳細資訊，請參閱 [在 ASP.NET Web API 中啟用跨原始來源要求](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)。

### <a name="authentication-filters"></a>驗證篩選器

驗證篩選器是 web API 中 ASP.NET 一種新型篩選器,在 ASP.NET Web API 管道中授權篩選器之前運行,允許您為所有控制器指定每個操作、每個控制器或全域的身份驗證邏輯。 身份驗證篩選器處理請求中的憑據並提供相應的主體。 身份驗證篩選器還可以添加身份驗證質詢以回應未經授權的請求。

### <a name="filter-overrides"></a>篩選器覆寫

現在,可以通過指定重寫篩選器來覆蓋應用於給定操作方法或控制器的篩選器。 覆蓋篩選器指定一組不應為給定作用域(操作或控制器)運行的篩選器類型。 這允許您添加全域篩選器,但隨後從特定操作或控制器中排除某些篩選器。

### <a name="owin-integration"></a>OWIN 整合

ASP.NET Web API 現在完全支援 OWIN,可以在任何支援 OWIN 的主機上運行。 還包括一個**主機身份驗證篩選器**,它提供與 OWIN 身份驗證系統的集成。

通過 OWIN 整合,您可以與其他 OWIN 中間件(如 SignalR)一起,在您自己的進程中自行託管 Web API。 有關詳細資訊,請參閱使用[OWIN ASP.NET Web API 進行自託管](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET信號R 2.0

以下各節介紹 SignalR 2.0 的功能。

- [基於 OWIN 建譯](#builtonowin)
- [地圖集線與地圖連線現在是對應訊號](#MapSignalR)
- [跨域支援](#crossdomain)
- [透過單點觸控和單體機器人支援 iOS 和 Android](#mobile)
- [可攜式 .NET 用戶端](#portable)
- [新的自主機包](#selfhost)
- [向後相容的伺服器支援](#backwardcompat)
- [已移除此.NET 4.0 的伺服器支援](#remove40)
- [將訊息傳送到客戶端及群組清單](#messagelist)
- [傳送使用者傳送訊息](#sendtouser)
- [更好的錯誤處理支援](#errorhandling)
- [更簡便的集線器單元測試](#unittesting)
- [JavaScript 錯誤處理](#javascripterror)

有關如何將現有的 1.x 專案升級到 SignalR 2.0 的範例,請參閱[升級 SignalR 1.x 專案](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)。

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>基於 OWIN 建譯

SignalR 2.0 完全基於[OWIN(.NET 的開放 Web 介面)](http://owin.org/)構建。 此更改使 SignalR 的設定過程在 Web 託管和自託管 SignalR 應用程式之間更加一致,但還需要多次 API 更改。

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>地圖集線與地圖連線現在是對應訊號

為了與 OWIN 標準相容,這些方法已重新`MapSignalR`命名為 。 `MapSignalR`在沒有參數的情況下調用將映射所有中心(如`MapHubs`版本1.x);映射單個**持久連接**物件,將連接類型指定為類型參數,並將連接的 URL 擴展作為第一個參數。

該方法`MapSignalR`在 Owin 啟動類中調用。 Visual Studio 2013 包含 Owin 啟動類的新範本;要使用此樣本,請使用以下操作:

1. 右鍵單擊項目
2. 選擇 **'新增****',新專案...**
3. 選擇**Owin 啟動類別**。 Startup.cs命名**新類。**

在**Web 應用程式中,**`MapSignalR`包含該方法 的 Owin 啟動類別後使用 Web.Config 檔的應用程式設定節點中的條目添加到 Owin 的啟動過程中,如下所示。

在**自託管應用程式中**,啟動類作為`WebApp.Start`方法的類型參數傳遞。

**映射 SignalR 1.x 中的集線器與連線(來自 Web 應用程式中的全域應用程式檔案):** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**映射 SignalR 2.0 中的集線器與連線(來自 Owin 啟動類別):** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

在**自託管應用程式中**,啟動類`WebApp.Start`作為 方法的類型參數傳遞,如下所示。

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>跨域支援

在 SignalR 1.x 中,跨域請求由單個啟用 CrossDomain 標誌控制。 此標誌同時控制 JSONP 和 CORS 請求。 為了更靈活,所有 CORS 支援都從 SignalR 的伺服器元件中刪除(如果檢測到瀏覽器支援它,JAVAScript 用戶端仍通常使用 CORS),並且新的 OWIN 中間件已可用於支援這些方案。

在 SignalR 2.0 中,如果用戶端上需要 JSONP(以支援舊瀏覽器中的跨域請求),`EnableJSONP``HubConfiguration`則`true`需要通過在 物件 上設置為 (如下所示)顯式啟用它。 默認情況下禁用 JSONP,因為它的安全性低於 CORS。

要在 SignalR 2.0 中添加`Microsoft.Owin.Cors`新的 CORS 中間件,`UseCors`請將庫添加到 專案中,並在 SignalR 中間件之前調用,如下節所示。

**將 Microsoft.Owin.Cors 新增到您的專案**:要安裝此庫,請在套件管理員控制台中執行以下指令:

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

此命令會將包的 2.0.0 版本添加到專案中。

**呼叫使用參數**

以下代碼段演示如何在 SignalR 1.x 和 2.0 中實現跨域連接。

**在 SignalR 1.x 中實現跨網域要求 (來自全域應用程式檔案)**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**在 SignalR 2.0 中實現跨網域要求 (來自 C# 代碼檔案)**

以下代碼展示如何在 SignalR 2.0 專案中啟用 CORS 或 JSONP。 此代碼示例使用`Map``RunSignalR``MapSignalR`而不是 ,以便 CORS 中間件僅運行需要 CORS 支援的 SignalR 請求(而不是針對中`MapSignalR`指定的路徑上的所有流量)。`Map`還可用於需要為特定 URL 首碼運行的任何其他中間件,而不是整個應用程式。

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>透過單點觸控和單體機器人支援 iOS 和 Android

已使用[Xamarin 庫中](https://xamarin.com/)的 MonoTouch 和 MonoDroid 元件為 iOS 和 Android 用戶端添加了支援。 有關如何使用它們的詳細資訊,請參閱[使用 Xamarin 元件](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)。 當 SignalR RTW 版本可用時,這些元件將在[Xamarin 儲存](https://store.xamarin.com/)中可用。

<a id="portable"></a>• 可移植 .NET 用戶端

為了更好地促進跨平台開發,Silverlight、WinRT 和 Windows Phone 用戶端已替換為支援以下平臺的單個可攜式 .NET 用戶端:

- 淨 4.5
- Silverlight 5
- WinRT (.NET 用於 Windows 應用商店應用)
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>新的自主機包

現在有一個 NuGet 套件,以便更輕鬆地開始使用 SignalR 自主機(託管在行程或其他應用程式中的 SignalR 應用程式,而不是託管在 Web 伺服器中)。 要升級使用 SignalR 1.x 構建的自主機專案,請刪除 Microsoft.AspNet.SignalR.Owin 包,然後添加 Microsoft.AspNet.SignalR.SelfHost 包。 有關開始使用自主機包的詳細資訊,請參閱[教程:SignalR 自主機](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>向後相容的伺服器支援

在早期版本的 SignalR 中,用戶端和伺服器中使用的 SignalR 套件版本需要相同。 為了支援難以更新的粗用戶端應用程式,SignalR 2.0 現在支援使用較新的伺服器版本與較舊的用戶端。 **注意:SignalR 2.0 不支援使用較舊版本的較舊用戶端構建的伺服器。**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>已移除此.NET 4.0 的伺服器支援

SignalR 2.0 已放棄對伺服器與 .NET 4.0 的互通性的支援。 .NET 4.5 必須與 SignalR 2.0 伺服器一起使用。 信號R 2.0 仍有 .NET 4.0 用戶端。

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>將訊息傳送到客戶端及群組清單

在 SignalR 2.0 中,可以使用用戶端和組 IT 的清單發送消息。 以下代碼段演示如何執行此操作。

**使用持久連線將訊息傳送到客戶端及群組清單**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**使用中心向客戶端及群組清單傳送訊息**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>傳送使用者傳送訊息

此功能允許使用者透過新介面 IUserIdProvider 指定使用者 Id 基於 IRequest 的內容:

**IUserId 提供者介面**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

默認情況下,將有一個使用使用者IPrincipal.Identity.Name作為使用者名的實現。

在集線器中,您可以透過新的 API 向這些使用者傳送訊息:

**使用用戶端.使用者 API**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>更好的錯誤處理支援

用戶現在可以從任何中心調用中引發**HubException。** **HubException**的建構函數可以獲取字串訊息和物件額外的錯誤資料。 SignalR 將自動序列化異常並將其發送到用戶端,其中它將用於拒絕/拒絕中心方法調用。

**顯示詳細的集線器異常**設置與**HubException**被發送回客戶端無關;它總是發送。

**顯示傳送到客戶端傳送 Hubexception 的伺服器端碼**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**顯示回應從伺服器傳送的 HubException 的 JavaScript 客戶端碼**

[!code-html[Main](release-notes/samples/sample16.html)]

**.NET 用戶端代碼,用於回應從伺服器傳送的 HubException**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>更簡便的集線器單元測試

SignalR 2.0`IHubCallerConnectionContext`包括一 個在集線器上調用的介面,該介面使創建類比用戶端調用變得更加容易。 以下程式碼段展示使用此介面與流行的測試工具[xUnit.net](https://github.com/xunit/xunit)與[moq](https://code.google.com/p/moq/)。

**帶xUnit.net的單元測試訊號R**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**使用 moq 進行單元測試訊號R**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>JavaScript 錯誤處理

在 SignalR 2.0 中,所有 JavaScript 錯誤處理回調返回 JavaScript 錯誤物件,而不是原始字串。 這允許 SignalR 將更豐富的資訊流向錯誤處理程式。 可以從錯誤的`source`屬性中獲取內部異常。

**處理 Start.Fail 異常的 JavaScript 客戶端碼**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET Identity

### <a name="new-aspnet-membership-system"></a>新的ASP.NET會員制

ASP.NET身份是ASP.NET應用程式的新成員資格系統。 ASP.NET識別使用戶特定的配置檔數據與應用程序資料整合變得容易。 ASP.NET識別還允許您為應用程式中的使用者配置檔選擇持久性模型。 您可以將資料儲存在 SQL Server 資料庫或其他資料存放區中，包括 NoSQL 資料存放區 (例如 Azure 儲存體資料表)。 有關詳細資訊,請參閱**可視化工作室 2013 中創建ASP.NET Web 專案的**[單個使用者帳戶](creating-web-projects-in-visual-studio.md#indauth)。

### <a name="claims-based-authentication"></a>宣告架構驗證

ASP.NET現在支援基於聲明的身份驗證,其中使用者的身份表示為來自受信任頒發者的一組聲明。 使用者可以使用應用程式資料庫中維護的使用者名稱和密碼進行身份驗證,或使用社交身份提供者(例如:微軟帳戶、Facebook、Google、Twitter),或者透過 Azure 活動目錄或活動目錄聯合服務 (ADFS) 使用組織帳戶。

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>與 Azure 的目錄與 Windows 伺服器活動目錄整合

現在,您可以創建ASP.NET使用Azure活動目錄或Windows伺服器活動目錄 (AD) 進行身份驗證的專案。 有關詳細資訊,請參閱在**Visual Studio 2013 中建立 ASP.NET Web 專案的**[組織帳戶](creating-web-projects-in-visual-studio.md#orgauth)。

### <a name="owin-integration"></a>OWIN 整合

ASP.NET身份驗證現在基於OWIN中間件,可用於任何基於OWIN的主機。 有關 OWIN 的詳細資訊,請參閱以下[Microsoft OWIN 元件](#TOC7)部分。

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN 元件

[.NET](http://owin.org/) (OWIN) 的開放 Web 介面定義 .NET Web 伺服器和 Web 應用程式之間的抽象。 OWIN 將 Web 應用程式與伺服器分離,使 Web 應用程式與主機無關。 例如,您可以在 IIS 中託管基於 OWIN 的 Web 應用程式,也可以在自訂進程中自承載它。

Microsoft OWIN 元件(也稱為 Katana 專案)中引入的更改包括新的伺服器和主機組件、新的幫助器庫和中間件以及新的身份驗證中間件。

有關 OWIN 和卡塔納的更多資訊,請參閱[OWIN 和卡塔納中的新增功能](../../../aspnet/overview/owin-and-katana/index.md)。

**注意[:OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)應用程式無法在 IIS 經典模式下運行;它們必須在集成模式下運行。**

**注意[:OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)應用程式必須完全信任地運行。**

### <a name="new-servers-and-hosts"></a>新伺服器和主機

使用此版本,添加了新的元件以啟用自承載方案。 這些元件包括以下 NuGet 套件:

- **微軟.Owin.Host.HTTPListener**. 提供一個 OWIN 伺服器,該伺服器使用**HttpListener**偵聽 HTTP 請求並將其定向到 OWIN 管道中。
- **Microsoft.Owin.Hosting**為希望在自定義進程中自承載 OWIN 管道(如控制台應用程式或 Windows 服務)的開發人員提供一個庫。
- **奧溫霍斯**。 提供一個獨立的可執行檔,用於包裝`Microsoft.Owin.Hosting`並允許您自承載 OWIN 管道,而無需編寫自定義主機應用程式。

此外,`Microsoft.Owin.Host.SystemWeb`該包現在使中間件能夠向**SystemWeb**伺服器提供提示,指示應在特定的 ASP.NET 管道階段調用中間件。 此功能對於身份驗證中間件特別有用,該中間件應在ASP.NET管道中早期運行。

### <a name="helper-libraries-and-middleware"></a>說明庫和中間件

儘管只能使用 OWIN 規範中的函數和類型定義編寫 OWIN 元件`Microsoft.Owin`,但新 包提供了一組更使用者友好的抽象。 此包將幾個較早的包(例如 ,)`Owin.Extensions``Owin.Types`合併到單個結構良好的物件模型中,然後其他 OWIN 元件可以輕鬆地使用該模型。 事實上,大多數 Microsoft OWIN 元件現在都使用此包。

> [!NOTE]
> [OWIN](http://www.owin.org)應用程式無法在IIS經典模式下運行;它們必須在集成模式下運行。

> [!NOTE]
> [OWIN](http://www.owin.org)應用程式必須完全信任地運行。

此版本還包括 Microsoft.Owin.診斷包,其中包括用於驗證正在運行的 OWIN 應用程式的中間件,以及幫助調查故障的錯誤頁中間件。

### <a name="authentication-components"></a>驗證元件

以下身份驗證元件可用。

- **微軟.Owin.安全.主動目錄**. 使用內部部署或基於雲端的目錄服務啟用身份驗證。
- **微軟.Owin.Security.cookies**支援使用Cookie進行身份驗證。 此套件以前命名為`Microsoft.Owin.Security.Forms`。
- **微軟.Owin.Security.Facebook**使用Facebook基於OAuth的服務啟用身份驗證。
- **微軟.Owin.Security.谷歌**使用谷歌基於OpenID的服務啟用身份驗證。
- **微軟.Owin.Security.Jwt**啟用使用 JWT 令牌的身份驗證。
- **微軟.Owin.Security.微軟帳戶**啟用使用微軟帳戶進行身份驗證。
- **微軟.奧溫.安全.奧烏斯**. 提供 OAuth 授權伺服器以及用於驗證無記名權杖的中間件。
- **微軟.Owin.Security.Twitter**使用Twitter基於OAuth的服務進行身份驗證。

此版本還包括包`Microsoft.Owin.Cors`,其中包含用於處理跨源 HTTP 請求的中間件。

> [!NOTE]
> 在 Visual Studio 2013 的最終版本中刪除了對 JWT 簽名的支援。

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

有關實體框架 6 中的新功能和其他更改的清單,請參閱[實體框架版本歷史記錄](https://msdn.com/data/jj574253)。

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET剃刀 3

ASP.NET Razor 3 包括以下新功能:

- 支援選項卡編輯。 以前,使用「**保留選項卡**」選項時,Visual Studio 中的 **「格式文檔**」指令、自動縮進和自動格式設定無法正常工作。 此更改糾正了用於選項卡格式的 Razor 代碼的可視化工作室格式。
- 生成連結時支援 URL 重寫規則。
- 刪除安全透明屬性。
  > [!NOTE]
  > 這是一個重大更改,使 Razor 3 與 MVC4 和更早版本不相容,而 Razor 2 與 MVC5 或針對 MVC5 編譯的程式集不相容。

Razor 3 問題修復在 Visual Studio 2013 從預發行版本可以[在這裡](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)找到.

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET應用程式掛起

ASP.NET應用程式掛起是 .NET Framework 4.5.1 中的一項改變遊戲規則的功能,它從根本上改變了在一台電腦上託管大量ASP.NET網站的使用者體驗和經濟模型。 有關詳細資訊,請參閱[ASP.NET 應用程式掛起 – 回應式共用 .NET Web 託管](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)。

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>已知問題和重大變更

本節介紹視覺工作室 2013 ASP.NET和 Web 工具中的已知問題和重大更改。

### <a name="nuget"></a>NuGet

- [使用 SLN 檔時,新包還原在 Mono 上不起作用](https://nuget.codeplex.com/workitem/3596), 將在即將進行的 nuget.exe 下載和[NuGet.CommandLine 套件](http://www.nuget.org/packages/NuGet.CommandLine/)更新中修復。
- [新的包還原與 Wix 專案不起作用](https://nuget.codeplex.com/workitem/3598)- 將在即將進行的 nuget.exe 下載和[NuGet.CommandLine 包](http://www.nuget.org/packages/NuGet.CommandLine/)更新中修復。
- [自動包還原在解決方案資料夾下的專案不起作用](https://nuget.codeplex.com/workitem/3625), 將在 NuGet 2.8 中修復。

### <a name="aspnet-web-api"></a>ASP.NET Web API

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)`不會總是返回`IQueryable<T>`,因為我們添加了`$select``$expand`對和的支援。

    我們以前的樣本`ODataQueryOptions<T>`總是將傳回值`ApplyTo`從`IQueryable<T>`轉換為 。 這在早期`$filter`起作用,因為我們支援之前的查詢選項 (、、、、)`$orderby``$skip``$top`不會更改查詢的形狀。 `$select`現在,我們支援`$expand`,並`ApplyTo`從返回值`IQueryable<T>`將 並不總是。

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    如果使用之前的範例代碼,則如果用戶端未發送`$select`和`$expand`,它將繼續工作。 但是,如果您希望支援`$select`,`$expand`並且必須將該代碼更改為此代碼。

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **要求.網址或要求上下文.網址在批次處理請求期間為空**

    在批次處理方案中 **,UrlHelper**從**請求.Url**或**請求上下文.網址**存取時為空。

    此問題目前在此處追蹤[:BatchRequestContext.網址 對於批次處理請求為空](http://aspnetwebstack.codeplex.com/workitem/1301)。

    此問題的解決方法是建立**UrlHelper**的新實體,如以下範例所示:

    **建立 UrlHelper 的新實體**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. 使用 MVC5 與 OrgAuth 時,如果您有執行 AntiForgerToken 驗證的檢視,則當您將資料發布到檢視時,可能會遇到以下錯誤:

    **錯誤**：

    *'/' 應用程式中有伺服器錯誤。*

    <em>所提供的索賠身份上不存在<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>類型"<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>或""的索賠。要使用基於聲明的身份驗證啟用反偽造權杖支援,請驗證已配置的聲明提供者是否在它生成的聲明標識實例上同時提供這兩種聲明。如果配置的聲明提供者使用不同的聲明類型作為唯一識別碼,則可以透過設定靜態屬性 AntiForgeryConfig.唯一ClaimType標識符來配置它。</em>

    **因應措施**：

    在 Global.asax 中新增以下行以修復它:

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    這將在下一個版本中修復。
2. 將 MVC4 應用升級到 MVC5 後,生成解決方案並啟動它。 您應該會看到以下錯誤:

    [A]系統.Web.WebPages.Razor.配置.Host節不能強制轉換為 [B_system.Web.Web.WebPages.Razor.配置.主機節。 類型 A 源自 "系統.Web.WebPages.Razor" 版本=2.0.0.0,區域性=中性,PublicKeyToken=31bf3856ad364e35"在上下文\_"預設"的位置 "C:_windows.Net_大會_GAC MSIL_System.WebPages.Razor_v4.0.0\_\_\_31bf3856ad36e35_系統.WebPages.剃鬚刀.剃鬚刀。" 類型 B 源自 'System.Web.WebPages.Razor, 版本=3.0.0.0, 區域性= 中性, PublicKeyToken_31bf3856ad364e35"在上下文"預設"的位置"C:_Windows_Microsoft.NET_Framework_v4.0.30319\臨時ASP.NET檔\root_6d 05bbd0_e8b5908e_assembly_dl3_c9cbca63_f8910382\_6273ce01_System.WebPages.Razor.dll'。

    要修復上述錯誤,請開啟項目中*的所有*Web.config 檔(包括"檢視'資料夾中的檔案),並執行以下操作:

   1. 將"System.Web.Mvc"版本"4.0.0.0"的所有匹配項更新為"5.0.0.0"。
   2. 更新&quot;系統.Web.Helpers"、系統.Web.WebPages&quot;和&quot;系統.Web.WebPages.Razor&quot;到"3.0.0.0"版本的所有匹配項

      例如,在進行上述更改後,程式集綁定應如下所示:

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      有關將 MVC 4 專案升級到 MVC 5 的資訊,請參閱[如何將 ASP.NET MVC 4 和 Web API 專案升級到 ASP.NET MVC 5 和 Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)。
3. 當將客戶端驗證與 jQuery 不顯眼驗證一起使用時,對於類型="數位"的 HTML 輸入元素,驗證消息有時不正確。 輸入無效號碼時將顯示所需值的驗證錯誤("需要"年齡欄位),而不是需要有效編號的正確消息。

    在"創建"和"編輯"檢視中具有整數屬性的模型的腳手架代碼通常會產生此問題。

    要解決此問題,從以下方面更改編輯器説明程式:

    `@Html.EditorFor(person => person.Age)`

    變更為：

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 不再支援部分信任。 連結到 MVC 或 WebAPI 二進位檔案的專案應刪除[安全透明](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx)屬性和[「允許部分受信任的呼叫者」](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx)屬性。 刪除這些屬性將消除編譯器錯誤,如下所示。

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > 請注意,作為副作用,您不能在同一應用程式中使用 4.0 和 5.0 程式集。 您需要將所有它們更新為 5.0。

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>具有 Facebook 授權的 SPA 樣本可能會導致 IE 不穩定,而網站託管在 Intranet 區域中

SPA 模板提供帶 Facebook 的外部登錄。 當使用範本創建的專案在本地運行時,登錄可能會導致 IE 崩潰。

解決方案：

1. 在互聯網區域託管網站;或

2. 在 IE 以外的瀏覽器中測試方案。

### <a name="web-forms-scaffolding"></a>Web Forms Scaffolding

Web 窗體基架已從 VS2013 中刪除,將來將更新為 Visual Studio。 但是,您仍可以通過添加 MVC 依賴項和生成 MVC 基架來在 Web 窗體專案中使用基架。 您的專案將包含 Web 窗體和 MVC 的組合。

要將 MVC 新增到 Web 窗體專案,請新增新的文手架項目,然後選擇**MVC 5 相依項 。** 根據是否需要所有內容檔(如腳本)選擇"最小"或"完整" 然後,為 MVC 添加一個基架項,這將在專案中創建檢視和控制器。

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 與 Web API 基架 - HTTP 404,找不到錯誤

如果在向專案添加基架項時遇到錯誤,則專案可能會處於不一致狀態。 對基架所做的一些更改將回滾,但其他更改(如已安裝的 NuGet 包)將不會回滾。 如果路由配置更改回滾,則使用者在導航到基架專案時將收到 HTTP 404 錯誤。

因應措施：

- 要修復 MVC 的此錯誤,請添加新的腳手架項並選擇 MVC 5 依賴項(最小或完整)。 此過程將添加專案所需的所有更改。
- 要修復 Web API 的此錯誤,本文:

  1. 將 WebApiConfig 類添加到專案中。

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. 在 Global.asax\_中的應用程式 啟動方法中設定 WebApiConfig.註冊,如下所示:

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
