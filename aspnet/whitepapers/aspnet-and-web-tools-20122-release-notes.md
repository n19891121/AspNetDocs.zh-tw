---
uid: whitepapers/aspnet-and-web-tools-20122-release-notes
title: ASP.NET 和 Web 工具 2012.2 版本資訊 |Microsoft Docs
author: rick-anderson
description: 適用於 ASP.NET 和 Web 工具 2012.2 版本資訊。
ms.author: riande
ms.date: 02/14/2013
ms.assetid: bdb18d02-9f61-4676-836d-6fdea94f9282
msc.legacyurl: /whitepapers/aspnet-and-web-tools-20122-release-notes
msc.type: content
ms.openlocfilehash: 50e96251f8add00f70193977e73f9af194571c49
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038905"
---
<a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET 和 Web 工具 2012.2 版本資訊
====================
> 本文件說明 ASP.NET 和 Web 工具 2012.2 版本。 它是 Visual Studio Web 工具和 ASP.NET 的更新。


- [安裝注意事項](#_Installation)
- [文件](#_Documentation)
- [支援](#_Support)
- [軟體需求](#_Software_Requirements)
- [在 ASP.NET 和 Web 工具 2012.2 中的新功能](#_New_Features_in)

    - [工具](#_Tooling)
    - [Web 發行](#_Web_Publishing)
    - [ASP.NET MVC 範本](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET 易記 Url](#_ASP.NET_Friendly_URLs)
- [已知的問題和重大變更](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>安裝注意事項

ASP.NET 和 Web 工具 2012.2 適用於 Visual Studio 2012 可以使用來安裝[Web Platform installer](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)。 這是 Visual Studio 2012 或 Visual Studio Express 2012 for Web，也就是必要的更新。 如果您沒有安裝 Visual Studio，將會安裝 Visual Studio Express 2012 for Web。

您也可以安裝 ASP.NET 和 Web 工具 2012.2 以手動方式。 您必須擁有 Visual Studio 2012 或 Visual Studio Express 2012 for Web 安裝。 然後使用下列指示： 

1. 下載[ASP.NET 和 Web Frameworks 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe)從下載中心安裝程式。
2. 當提示按一下 [執行]。 您也可以儲存檔案，以供日後執行。
3. 請確認您要將更新的 Visual Studio 的版本。 您可以啟動您想要更新 Visual Studio 來執行這項操作。 然後按一下 [說明] 功能表項目。   
    ![](aspnet-and-web-tools-20122-release-notes/_static/image1.jpg)
4. 如果您看到的功能表項目&quot;關於 Microsoft Visual Studio 2012 for Web&quot;然後下載[Web 開發人員工具 2012.2-Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkID=282228)。 否則下載[Web 開發人員工具 2012.2-Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228)。
5. 當提示按一下 [執行]。 您也可以儲存檔案，以供日後執行。

> [!NOTE]
> ASP.NET 和 Web 工具 2012.2 版本不包含 SQL Server Data Tools。 SQL Server 和 Windows Azure SQL Database 提供一組豐富的工具包括離線專案為基礎的開發、 結構描述比較和增強的資料庫部署功能的資料庫。 如需詳細資訊，或要安裝 SQL Server Data Tools 請造訪[ https://go.microsoft.com/fwlink/?LinkID=237127 ](https://go.microsoft.com/fwlink/?LinkID=237127)。

<a id="_Documentation"></a>
## <a name="documentation"></a>文件

教學課程和其他資訊，關於 ASP.NET 和 Web 工具 2012.2 都是從 ASP.NET 網站 ( https://www.asp.net)。

<a id="_Support"></a>
## <a name="support"></a>支援

ASP.NET 和 Web 工具 2012.2 正式釋出並支援。 您可以使用您的標準支援通道。 您也可以將問題張貼至 ASP.NET 論壇 ([https://forums.asp.net/](https://forums.asp.net/))，其中的 ASP.NET 社群成員可經常提供非正式的支援。

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>軟體需求

ASP.NET 和 Web 工具 2012.2 vyžaduje Visual Studio 2012 或 Visual Studio Express 2012 for Web。

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>在 ASP.NET 和 Web 工具 2012.2 中的新功能

本節說明在 ASP.NET 和 Web 工具 2012.2 版本中已引進的功能。

<a id="_Tooling"></a>
### <a name="tooling"></a>Tooling

- Page Inspector 

    - 支援允許將頁面回傳至相對應的 JavaScript 程式碼以動態方式加入的項目對應至 Page Inspector 的 JavaScript 選取項目對應。
    - 若要查看即時 CSS 更新能力。
    - 如需詳細資訊，請參閱[CSS 自動同步處理和 Page Inspector 中的 JavaScript 選取項目對應](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)。
- 編輯器 

    - 支援的 CoffeeScript、 Mustache、 Handlebars、 和 JsRender 語法醒目提示。
    - HTML 編輯器會提供 Intellisense Knockout 繫結。
    - 較少的 「 編輯 」 和編譯器支援以啟用建置動態使用較少的 CSS。
    - 貼上 JSON 做為.NET 類別。 使用這個特殊的貼上命令來將 JSON 貼到 C# 或 VB.NET 程式碼檔案和 Visual Studio 會自動產生.NET 類別，從 JSON 推斷而來。
- 行動裝置版模擬器支援將擴充性攔截程序，以便在第三方模擬器可以安裝為 VSIX。 已安裝的模擬器會顯示在 [F5] 下拉式清單中，以便開發人員可以預覽他們在各種不同的行動裝置上的網站。 深入了解這項功能在 Scott Hanselman 的部落格文章[使用 Visual Studio 的新 BrowserStack 整合](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)。

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Web 發行

- 網站專案現在會有與 Web 應用程式專案，包括發行至 Windows Azure 網站相同的發佈體驗。
- 選擇性發行&#8211;的一或多個檔案可以執行下列動作 （在發行至 Web Deploy 的端點）： 

    - 發行選取的檔案。
    - 請參閱本機檔案與遠端的檔案之間的差異。
    - 更新遠端檔案的本機檔案，或使用本機檔案來更新遠端的檔案。

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC 範本

- 新的 Facebook 應用程式範本可讓撰寫 Facebook Canvas 簡單的應用程式。 在幾個簡單步驟中，您可以建立 Facebook 應用程式，從登入的使用者取得資料，並與他的朋友可以整合。 此範本包括新的程式庫，來處理建置 Facebook 應用程式，包括驗證、 權限、 存取 Facebook 資料等等所涉及的所有配管。 如需使用 Facebook 應用程式範本的詳細資訊，請參閱[ https://go.microsoft.com/fwlink/?LinkID=269921 ](https://go.microsoft.com/fwlink/?LinkID=269921)。
- 新的單一頁面應用程式 MVC 範本可讓開發人員建置互動式用戶端 web 應用程式使用 HTML 5、 CSS 3 和熱門的 Knockout 與 jQuery JavaScript 程式庫，在 ASP.NET Web API 之上。 此範本包括"todo"清單應用程式，示範如何建置使用 RESTful 伺服器 API 的 JavaScript HTML5 應用程式的常見做法。 您可以深入了解[ https://www.asp.net/single-page-application ](../single-page-application/index.md)。
- 您現在可以建立 ASP.NET MVC 新增專案 對話方塊中加入新範本的 VSIX。 了解詳情： [https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- FixedDisplayModes 封裝&#8211;的 MVC 專案範本已更新成包含新的 'FixedDisplayModes' NuGet 套件，其中包含 MVC 4 中的錯誤的因應措施。 如需有關封裝中包含的修正程式的詳細資訊，請參閱此部落格文章 ([https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)) 從 MVC 團隊。

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET Web API 的增強提供幾項新功能：

- ASP.NET Web API OData
- ASP.NET Web API 追蹤
- ASP.NET Web API 說明頁面

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Web API OData 可讓您透過任何資料來源建置具有豐富的商務邏輯的 OData 端點所需的彈性。 與 ASP.NET Web API OData 中，您控制您想要公開的 OData 語意的數量。 ASP.NET Web API OData 隨附的 ASP.NET MVC 4 專案範本，而且也會提供從 NuGet ([http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata))。

ASP.NET Web API OData 目前支援下列功能：

- 藉由套用 [Queryable] 屬性中啟用 OData 查詢語意。
- 輕鬆地驗證 OData 查詢，並限制的一組支援的查詢選項、 運算子和函式。
- 參數繫結 ODataQueryOptions 直接可取得的查詢，然後進行驗證並套用到 IEnumerable 或 IQueryable 的抽象語法樹狀結構表示法。
- 指定 [Queryable] 屬性的結果限制來啟用服務導向的分頁和新一代的頁面連結。
- 要求的比對資源使用 $inlinecount 總數的內嵌的計數。
- 控制 null 傳播。
- $Filter 中任何/所有運算子。
- 依照慣例推斷實體資料模型或明確地自訂類似以 Entity Framework Code First 模型。
- 公開實體集藉由衍生自 EntitySetController。
- 公開的導覽屬性、 操作連結和實作 OData 動作的簡單、 可自訂慣例。
- 簡化路由使用 MapODataRoute 擴充方法。
- 藉由公開多個 EDM 模型的版本控制支援。
- 公開 （expose) 服務文件和 $metadata 讓您可以產生用戶端 （.NET、 Windows Phone、 Windows 市集等） 為您的 Web API。
- 支援 OData Atom、 JSON 和 JSON verbose 格式。
- 建立、 更新、 部分更新 (PATCH) 和刪除實體。
- 查詢並管理實體之間的關聯性。
- 建立連接到您的路由的關聯性連結。
- 複雜類型。
- 實體類型的繼承。
- 集合屬性。
- 列舉。
- OData 動作。
- 建置於相同的基礎為 WCF 資料服務，也就是 ODataLib ([http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata))。

如需有關 ASP.NET Web API OData [ https://go.microsoft.com/fwlink/?LinkId=271141 ](https://go.microsoft.com/fwlink/?LinkId=271141)。

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web API 追蹤

ASP.NET Web API 追蹤會將追蹤資料，從您的 web Api 與.NET 追蹤。 它現在會啟用預設會在 Web API 專案範本。 追蹤資料，您的 web Api 會傳送至 [輸出] 視窗，並可透過 IntelliTrace。 ASP.NET Web API 追蹤功能可讓您追蹤您的 Web API 裝載在 Windows Azure 上透過與整合時的資訊[Windows Azure 診斷](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)。 您也可以安裝並啟用 使用 ASP.NET Web API 追蹤的 NuGet 套件的任何應用程式中的 ASP.NET Web API 追蹤 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing))。

如需設定及使用 ASP.NET Web API 追蹤的詳細資訊，請參閱[ https://go.microsoft.com/fwlink/?LinkID=269874 ](https://go.microsoft.com/fwlink/?LinkID=269874)。

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web API 說明頁面

預設會在 Web API 專案範本現在包含 ASP.NET Web API 說明頁面。 ASP.NET Web API 說明頁面會自動產生 web Api 包括 HTTP 端點、 支援的 HTTP 方法、 參數和範例要求和回應訊息內容的文件。 文件會自動提取程式碼中的註解中。 您也可以使用 ASP.NET Web API 說明頁面 NuGet 套件的任何應用程式來新增 ASP.NET Web API 說明頁面 ([http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage))。

如需有關設定和自訂 ASP.NET Web API 說明頁面，請參閱[ https://go.microsoft.com/fwlink/?LinkId=271140 ](https://go.microsoft.com/fwlink/?LinkId=271140)。

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR 輕鬆地將即時 web 功能新增至您的 ASP.NET 應用程式，使用可用的 Websocket，並自動切換回其他技術時也不。

如需有關使用 ASP.NET SignalR [ https://go.microsoft.com/fwlink/?LinkId=271271 ](https://go.microsoft.com/fwlink/?LinkId=271271)。

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET 易記 Url

ASP.NET FriendlyURLs 非常容易供 web form 開發人員產生清除器 （不含副檔名的.aspx） 中尋找的 Url。 它需要不到組態設定少，並且可以搭配現有的 ASP.NET v4.0 應用程式。 FriendlyURLs 功能也可讓支援桌上型電腦和行動裝置檢視之間切換，將行動裝置的支援新增至他們的應用程式的開發人員更容易。

如需安裝和使用 ASP.NET 易記 Url 的詳細資訊，請參閱[ http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx ](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)。

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>已知的問題和重大變更

本章節描述的已知的問題和 ASP.NET 和 Web 工具 2012.2 版本中的重大變更。

### <a name="installation-issues"></a>安裝問題

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>次序會安裝 Visual Studio 2012

安裝 ASP.NET 和 Web 工具 2012.2 會需要修復作業之後，請安裝其他 SKU 的 Visual Studio 2012。 請考量以下發生順序：

1. 安裝 Visual Studio 2012 Express for Web
2. 安裝 ASP.NET 和 Web 工具 2012.2
3. 安裝 Visual Studio 2012 Professional、 Premium 或 Ultimate

步驟 2 只會導致安裝 Express for Web 的更新。 若要確定其他 SKU 在步驟 3 中安裝包含更新，您必須修復安裝的更新安裝的最後一個 sku 的 ASP.NET 和 Web 工具 2012.2。 這也適用於在步驟 1 中的 Sku 和 3 會反轉。

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>開啟 Visual Studio 時，安裝 Microsoft ASP.NET 和 Web 工具 2012.2

VS 安裝 Microsoft ASP.NET 和 Web 工具 2012.2 期間是開啟的如果 Visual Studio 可能會得到不正確的狀態。 建議使用者關閉後再繼續進行安裝的 Visual Studio 的所有執行個體。

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>安裝期間取消的 ASP.NET 和 Web 工具 2012.2 安裝程式

ASP.NET 和 Web 工具 2012.2 取消安裝程式安裝期間會讓 Visual Studio 處於不正常的狀態。 若要解決此問題遵循下列步驟： 

- 移至 新增移除程式
- 解除安裝 Microsoft ASP.NET 和 Web 工具 2012.2，如果有的話。
- 重新安裝 Microsoft ASP.NET 和 Web 工具 2012.2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>如果之後解除安裝 ASP.NET 和 Web 工具 2012.2 ASP.NET MVC 4 範本和 Razor v2 的網站範本是遺漏

解除安裝 ASP.NET 和 Web 工具 2012.2 會也解除安裝所有的 ASP.NET MVC 4 和 Razor v2 的網站範本從 Visual Studio 2012。

因應措施是修復您的 Visual Studio 2012 安裝，以重新安裝 ASP.NET MVC 4 和 Razor v2 的網站範本。

### <a name="tooling-issues"></a>工具問題

#### <a name="nuget-error-reported-during-project-creation"></a>NuGet 專案建立期間所回報的錯誤

在安裝 ASP.NET 和 Web 工具 2012.2 後您可能會看到下列錯誤時建立的 MVC 4 專案

![](aspnet-and-web-tools-20122-release-notes/_static/image1.png)

ASP.NET 和 Web 工具 2012.2 附隨 NuGet 2.1，並將升級 Visual Studio 2012 中的擴充功能。 在某些情況下，VSIX 安裝程式將無法正確更新 VSIX。 下列步驟可讓您解決這個問題：

1. 系統管理員身分啟動 Visual Studio 2012
2. 移至工具-&gt;擴充功能和更新及解除安裝 NuGet。
3. 關閉 Visual Studio
4. 瀏覽至 ASP.NET 和 Web 工具 2012.2 的安裝資料夾：

    1. 適用於 Visual Studio 2012:**Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio 2012**
    2. 針對 Visual Studio 2012 Express for Web:**Program Files\Microsoft ASP.NET\ASP.NET Web Stack\Visual Studio Express 2012 for Web**
5. 若要重新安裝 NuGet NuGet.Tools.vsix 按兩下

### <a name="web-api-issues"></a>Web API 的問題

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>剖析 $filter 和日期時間常值中的問題

OData URI 剖析器無法正確地剖析部分的日期時間常值。 比方說，$filter = 開始 eq datetime' 2012年-12-31T12:00' 無法正確地剖析。 因應措施為使用完整常值，$filter = 開始 eq datetime' 2012年-12-31T12:00:00'。

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData 並不支援不區分大小寫的屬性名稱。

OData 不支援不區分大小寫的屬性名稱中的 OData 查詢和 odata 路徑。 請參閱工作項目：

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

如果使用者有 javascript 用戶端和伺服器端上的大小寫不同，它們可能會發生這個問題。 此問題是依據 odata 通訊協定中的設計。 不過，許多使用者報告此問題。 若要解決之道，使用者必須更正它們的大小寫，在 URL 中。

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>預設 OData 路由慣例不支援 POST/PUT 上瀏覽屬性。

預設 OData 路由慣例不支援 POST/PUT 上瀏覽屬性。 請參閱工作項目[ http://aspnetwebstack.codeplex.com/workitem/366 ](http://aspnetwebstack.codeplex.com/workitem/366)。 我們沒有這個常用的慣例，在預設慣例。

若要解決之道，使用者必須擴充新的路由慣例，來支援它。

### <a name="facebook-template-issues"></a>Facebook 範本問題

#### <a name="facebook-application-template-only-works-using-net-45"></a>Facebook 應用程式範本僅適用於使用.NET 4.5

您必須選取.NET 4.5 framework 下拉式清單中看到的 Facebook 應用程式範本，在 ASP.NET MVC 4 中的 [新增專案] 對話方塊中。

#### <a name="real-time-update-controller"></a>即時更新控制站

Facebook 應用程式範本可讓使用者輕鬆地建立 Web API 控制器，以處理 Facebook 即時更新。 如果您的開發電腦位於 NAT 後面，您的控制器可能無法運作而不需要進一步的網路設定。 如需詳細資訊，請參閱這裡： [http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>查詢字串值，則與 Facebook OAuth 參數發生衝突

下列欄位衝突與 Facebook OAuth 對話方塊的呼叫傳回 URL。 無法新增您自己的查詢字串值，以下列名稱： 程式碼、 錯誤、 錯誤\_描述、 錯誤\_原因。

#### <a name="using-page-inspector-with-facebook-template"></a>使用 Facebook 範本中使用 Page Inspector

您無法在偵錯您的 Facebook 應用程式時，Visual Studio 2012 中使用 Page Inspector 功能。 Page Inspector 目前不支援 iframe。

### <a name="single-page-application-template-issues"></a>單一頁面應用程式範本問題

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>與 JQuery 1.9/Knockout 2.2.1 更新時執行預設 MVC SPA 專案，新的 todo 項目編輯輸入焦點處理事件，是不正確。

與 JQuery 1.9/Knockout 2.2.1 更新中，執行預設 MVC SPA 專案時，新的 todo 項目編輯輸入不再焦點回到新的 todo 項目編輯方塊至 todo 清單中輸入新的 todo 項目之後。

因應措施參考[ http://knockoutjs.com/documentation/hasfocus-binding.html ](http://knockoutjs.com/documentation/hasfocus-binding.html)，並對下列的範例程式碼進行類似的修正程式：

檔案 todo.model.js  
 函式 todolist(data) 中，新增下列：  
 **self.isSelected = ko.observable(false);**

函式 todoList.prototype.addTodo 中，加入下列 blacked 的文字：  
 **self.isSelected(true);**  
 self.newTodoTitle(&quot;&quot;);

檔案 index.cshtml 中，新增下列 blacked 的文字：  
 &lt;表單資料繫結 =&quot;提交： addTodo&quot;&gt;  
 &lt;input class=&quot;addTodo&quot; type=&quot;text&quot; data-bind=&quot;value: newTodoTitle, placeholder:'Type 這裡以新增'、 blurOnEnter: 0、1、true **hasfocus: isSelected**，事件: {模糊： addTodo}&quot; /&gt;  
 &lt;/form&gt;
