---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
title: ASP.NET和網络工具 2012.2 發行說明 |微軟文件
author: rick-anderson
description: ASP.NET和網路工具 2012.2 的發行說明。
ms.author: riande
ms.date: 02/14/2013
ms.assetid: 9534e58b-1d15-4f1d-b04c-10c79b9d8227
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw
msc.type: content
ms.openlocfilehash: abd6d8ce0646852a194369589cb730fc98ecb3ad
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676304"
---
# <a name="aspnet-and-web-tools-20122-release-notes"></a>ASP.NET 和 Web 工具 2012.2 版本資訊

> 本文件介紹 ASP.NET 和 Web 工具 2012.2 的發布。 它是可視化工作室 Web 工具和 ASP.NET 的更新。

- [安裝說明](#_Installation)
- [文件](#_Documentation)
- [支援](#_Support)
- [軟體要求](#_Software_Requirements)
- [ASP.NET和 Web 工具中的新功能 2012.2](#_New_Features_in)

    - [Tooling](#_Tooling)
    - [Web Publishing](#_Web_Publishing)
    - [ASP.NET MVC 樣本](#_Templates)
    - [ASP.NET Web API](#_ASP.NET_Web_API)

    - [ASP.NET SignalR](#_ASP.NET_SignalR)
    - [ASP.NET 易記 URL](#_ASP.NET_Friendly_URLs)
- [已知問題和重大變更](#_Known_Issues_and)

<a id="_Installation"></a>
## <a name="installation-notes"></a>安裝注意事項

ASP.NET和Web工具2012.2為可視化工作室2012可以使用[Web平臺安裝程式](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)安裝。 這是 Visual Studio 2012 或 Visual Studio Express 2012 Web 的更新,這是必要的。 如果您未安裝 Visual Studio,則將安裝適用於 Web 的 Visual Studio Express 2012。

您還可以手動安裝ASP.NET和 Web 工具 2012.2。 您必須安裝 Visual Studio 2012 或 Visual Studio Express 2012 以安裝 Web。 然後使用以下說明: 

1. 從下載中心下載[ASP.NET和 Web 框架 2012.2](https://download.microsoft.com/download/6/5/6/6562AFBE-9503-4E64-970C-1427133FCD73/AspNetWebTools2012Setup.exe)安裝程式。
2. 當提示時,按一下「運行」。 您還可以保存該檔以稍後運行該檔。
3. 驗證您將要更新的可視化工作室版本。 您可以通過啟動要更新的可視化工作室來執行此操作。 然後單擊"幫助"功能表項。   
    ![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.jpg)
4. 如果你看到關於微軟視覺工作室&quot;2012網頁的功能表&quot;項 ,然後下載[網路開發人員工具2012.2 - Visual Studio Express 2012為Web。](https://go.microsoft.com/fwlink/?LinkID=282228) 否則下載[網路開發人員工具 2012.2 - 視覺工作室 2012](https://go.microsoft.com/fwlink/?LinkID=282228).
5. 當提示時,按一下「運行」。 您還可以保存該檔以稍後運行該檔。

> [!NOTE]
> ASP.NET和 Web 工具 2012.2 版本不包括 SQL Server 資料工具。 SQL Server 和 Windows Azure SQL 資料庫提供了一組更豐富的資料庫工具,包括離線專案支援的開發、架構比較和擴增的資料庫部署功能。 關於詳細資訊或安裝 SQL 伺服器資料工具,[https://go.microsoft.com/fwlink/?LinkID=237127](https://go.microsoft.com/fwlink/?LinkID=237127)請造訪 。

<a id="_Documentation"></a>
## <a name="documentation"></a>文件

有關ASP.NET和 Web 工具 2012.2 的教程和其他資訊可從ASP.NET網站https://www.asp.net)() 獲得。

<a id="_Support"></a>
## <a name="support"></a>支援

ASP.NET和網路工具 2012.2 正式發佈和支援。 您可以使用正常的支援通道。 您還可以向ASP.NET論壇 ()[https://forums.asp.net/](https://forums.asp.net/)發佈問題,ASP.NET社區成員經常能夠提供非正式支援。

<a id="_Software_Requirements"></a>
## <a name="software-requirements"></a>軟體需求

ASP.NET和網路工具 2012.2 要求 Visual Studio 2012 或 Visual Studio Express 2012 用於 Web。

<a id="_New_Features_in"></a>
## <a name="new-features-in-aspnet-and-web-tools-20122"></a>ASP.NET和 Web 工具中的新功能 2012.2

本節介紹在ASP.NET和Web工具 2012.2 版本中引入的功能。

<a id="_Tooling"></a>
### <a name="tooling"></a>Tooling

- Page Inspector 

    - 支援 JavaScript 選擇映射,允許頁面檢查器將動態添加到頁面的專案映射回相應的 JavaScript 代碼。
    - 即時查看 CSS 更新的能力。
    - 關於詳細資訊,請閱讀[網頁檢查器 中的 CSS 自動同步與 JavaScript 選擇對應](https://blogs.msdn.com/b/webdev/archive/2012/12/14/css-auto-sync-and-javascript-selection-mapping-in-page-inspector.aspx)。
- 編輯器 

    - 支援咖啡腳本、鬍鬚、手柄和 JsRender 的語法突出顯示。
    - HTML 編輯器為挖空綁定提供"感知"。
    - 減少編輯和編譯器支援,以便使用 LESS 構建動態 CSS。
    - 將 JSON 貼上為 .NET 類。 使用此特殊貼上指令將 JSON 貼上到 C# 或VB.NET代碼檔中,Visual Studio 將自動生成從 JSON 推斷的 .NET 類。
- 移動模擬器支援增加了擴充性掛鉤,以便第三方模擬器可以作為 VSIX 安裝。 已安裝的模擬器將顯示在 F5 下拉清單中,以便開發人員可以在各種行動裝置上預覽其網站。 閱讀更多有關此功能在斯科特漢塞爾曼的部落格目與[視覺工作室新的瀏覽器堆疊集成](http://www.hanselman.com/blog/CrossBrowserDebuggingIntegratedIntoVisualStudioWithBrowserStack.aspx)。

<a id="_Web_Publishing"></a>
### <a name="web-publishing"></a>Web Publishing

- 網站專案現在具有與 Web 應用程式專案相同的發表體驗,包括發表到 Windows Azure 網站。
- 選擇性發佈&#8211;一個或多個檔案,您可以執行以下操作(發佈到 Web 部署終結點後): 

    - 發佈選定的檔。
    - 查看本地檔和遠端檔之間的區別。
    - 使用遠端檔案更新本地檔案或使用本地檔案更新遠端檔案。

<a id="_Templates"></a>
### <a name="aspnet-mvc-templates"></a>ASP.NET MVC 樣本

- 全新的 Facebook 應用程式範本可讓撰寫 Facebook Canvas 應用程式再容易不過了。 只需幾個簡單的步驟，您便可建立 Facebook 應用程式，進而取得已登入使用者的資料並將資料與他的朋友進行整合。 此範本包括一個新程式庫，處理建置 Facebook 應用程式時所涉及的所有連結，包括授權、權限、存取 Facebook 資料等等。 有關使用 Facebook 應用程式樣本的詳細資訊,請參[https://go.microsoft.com/fwlink/?LinkID=269921](https://go.microsoft.com/fwlink/?LinkID=269921)閱 。
- 全新的單一網頁應用程式 MVC 範本可讓開發人員使用 HTML 5、CSS 3 和熱門的 Knockout 與 jQuery JavaScript 程式庫，在 ASP.NET Web API 的基礎上建置互動式用戶端 Web 應用程式。 該範本包括一個"待辦事項"列表應用程式,該應用程式演示了構建使用 RESTful 伺服器 API 的 JavaScript HTML5 應用程式的常見做法。 您可以在 上閱讀更多[https://www.asp.net/single-page-application](../../../single-page-application/index.md)內容 。
- 您現在可以創建一個 VSIX,將新範本添加到 ASP.NET MVC 新項目對話方塊。 瞭解如何在此處:[https://go.microsoft.com/fwlink/?LinkId=275019](https://go.microsoft.com/fwlink/?LinkId=275019)
- 已更新 &#8211; MVC 專案樣本的固定顯示模式包,以包括新的「固定顯示模式」NuGet 包,該包包含 MVC 4 中 Bug 的解決方法。 有關包中包含的修復程式的詳細資訊,請參閱 MVC 團隊的此部[https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)落格文章 ( )。

<a id="_ASP.NET_Web_API"></a>
### <a name="aspnet-web-api"></a>ASP.NET Web API

ASP.NET Web API 已通過以下幾個新功能進行了增強:

- ASP.NET Web API OData
- ASP.NET Web API 追蹤
- ASP.NET Web API 說明頁

#### <a name="aspnet-web-api-odata"></a>ASP.NET Web API OData

ASP.NET Web API OData 使您能夠靈活地建構具有豐富業務邏輯的 OData 終結點,而不是任何資料來源。 使用ASP.NET Web API OData,您可以控制要公開的 OData 語意量。 ASP.NET Web API OData 包含在 mVC 4ASP.NET 專案樣本[http://www.nuget.org/packages/microsoft.aspnet.webapi.odata](http://www.nuget.org/packages/microsoft.aspnet.webapi.odata)中,也可從 NuGet () 獲得。

ASP.NET Web API OData 目前支援以下功能:

- 通過應用 [可查詢] 屬性啟用 OData 查詢語義。
- 輕鬆驗證 OData 查詢並限制支援的查詢選項、運算子和函數集。
- 參數直接綁定到 ODataQueryOptions,以獲得查詢的抽象語法樹表示形式,然後可以驗證並應用於可查詢或 IE500。
- 通過在 [可查詢] 屬性上指定結果限制,啟用服務驅動的分頁和下一頁連結生成。
- 使用$inlinecount請求匹配資源總數的內聯計數。
- 控制無效傳播。
- $filter中的任何/所有運算符。
- 按約定推斷實體數據模型,或以類似於實體框架代碼優先的方式顯式自定義模型。
- 通過從實體集控制器派生來公開實體集。
- 用於公開導航屬性、操作連結和實現 OData 操作的簡單可自定義約定。
- 使用 MapODataRoute 擴充方法簡化路由。
- 通過公開多個 EDM 模型來支援版本控制。
- 公開服務文檔和$metadata,以便為 Web API 生成用戶端(.NET、Windows Phone、Windows 應用商店等)。
- 支援 OData Atom、JSON 和 JSON 詳細格式。
- 建立、更新、部分更新(PATCH)和刪除實體。
- 查詢和操作實體之間的關係。
- 建立連接到您的路線的關係連結。
- 複雜類型。
- 實體類型繼承。
- 集合屬性。
- 枚舉。
- OData 操作。
- 建立與 WCF 資料服務相同的基礎,即 ODataLib[http://www.nuget.org/packages/microsoft.data.odata](http://www.nuget.org/packages/microsoft.data.odata)()。

有關web API OData ASP.NET[https://go.microsoft.com/fwlink/?LinkId=271141](https://go.microsoft.com/fwlink/?LinkId=271141)的詳細資訊 ,請參閱。

#### <a name="aspnet-web-api-tracing"></a>ASP.NET Web API 追蹤

ASP.NET Web API 追蹤將從 Web API 的追蹤資料整合到 .NET 追蹤中。 默認情況下,它在 Web API 專案樣本中啟用。 Web API 的追蹤數據將發送到輸出視窗,並透過 IntelliTrace 提供。 ASP.NET Web API 追蹤使您能夠透過與[Windows Azure 診斷](https://msdn.microsoft.com/library/windowsazure/hh411529.aspx)整合在 Windows Azure 上託管時追蹤有關 Web API 的資訊。 您還可以使用ASP.NET Web API 追蹤 NuGet 套件 ()[http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing](http://www.nuget.org/packages/microsoft.aspnet.webapi.tracing)在任何應用程式中安裝和啟用ASP.NET Web API 追蹤。

有關設定和使用ASP.NET Web API 追蹤的詳細資訊,[https://go.microsoft.com/fwlink/?LinkID=269874](https://go.microsoft.com/fwlink/?LinkID=269874)請參閱 。

#### <a name="aspnet-web-api-help-page"></a>ASP.NET Web API 說明頁

默認情況下,Web API 幫助頁ASP.NET包含在 Web API 專案範本中。 ASP.NET Web API 協助頁面會自動為 Web API 產生文件,包括 HTTP 終結點、支援的 HTTP 方法、參數以及示例請求和回應消息負載。 文檔會自動從代碼中的註釋中提取。 您還可以使用ASP.NET Web API 幫助頁 NuGet 套件 ()[http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage](http://www.nuget.org/packages/microsoft.aspnet.webapi.helppage)將ASP.NET Web API 幫助頁添加到任何應用程式。

有關設定和自訂ASP.NET Web API 說明頁的詳細資訊,[https://go.microsoft.com/fwlink/?LinkId=271140](https://go.microsoft.com/fwlink/?LinkId=271140)請參閱 。

<a id="_ASP.NET_SignalR"></a>
### <a name="aspnet-signalr"></a>ASP.NET SignalR

ASP.NET SignalR 使將即時 Web 功能添加到 ASP.NET 應用程式中變得簡單,如果使用 WebSocket(如果可用),則在不可用時自動回歸到其他技術。

有關使用ASP.NET訊號R的詳細資訊,請參[https://go.microsoft.com/fwlink/?LinkId=271271](https://go.microsoft.com/fwlink/?LinkId=271271)閱 。

<a id="_ASP.NET_Friendly_URLs"></a>
### <a name="aspnet-friendly-urls"></a>ASP.NET 易記 URL

ASP.NET友好 URL 使 Web 表單開發人員能夠非常輕鬆地生成外觀更簡潔的 URL(沒有 .aspx 擴展)。 它只需要很少或不需要配置,並且可用於現有的ASP.NET v4.0 應用程式。 友好 URL 功能還支援桌面檢視和行動視圖之間的切換,使開發人員能夠更輕鬆地向其應用程式添加行動支援。

有關安裝和使用ASP.NET友好 URL 的詳細資訊,請[http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)參閱 。

<a id="_Known_Issues_and"></a>
## <a name="known-issues-and-breaking-changes"></a>已知問題和重大變更

本節介紹 ASP.NET 和 Web 工具 2012.2 版本中的已知問題和重大更改。

### <a name="installation-issues"></a>安裝問題

#### <a name="out-of-order-installs-of-visual-studio-2012"></a>視覺工作室 2012 的有序安裝

安裝ASP.NET和 Web 工具 2012.2 後安裝 Visual Studio 2012 的額外 SKU 將需要修復操作。 考量以下發生順序：

1. 安裝視覺化工作室 2012 快速網頁
2. 安裝ASP.NET和 Web 工具 2012.2
3. 安裝視覺工作室 2012 專業, 高級或終極

步驟 2 僅會導致為 Web 安裝 Express 的更新。 為了確保在步驟 3 中安裝的其他 SKU 包含更新,您需要修復 ASP.NET和 Web 工具 2012.2 才能安裝上次安裝的 SKU 的更新。 如果步驟 1 和步驟 3 中的 SKU 顛倒,則這也適用於。

#### <a name="installing-microsoft-aspnet-and-web-tools-20122-when-visual-studio-is-open"></a>安裝微軟ASP.NET和網路工具 2012.2 當可視化工作室打開

如果在安裝 Microsoft ASP.NET 和 Web 工具 2012.2 期間打開 VS,則 Visual Studio 可能最終處於不良狀態。 建議使用者在繼續安裝之前關閉 Visual Studio 的所有實例。

#### <a name="canceling-aspnet-and-web-tools-20122-setup-in-the-middle-of-installation"></a>在安裝中取消ASP.NET和 Web 工具 2012.2 設定

取消ASP.NET和 Web 工具 2012.2 安裝將會使 Visual Studio 處於不良狀態。 要解決此問題,請執行以下步驟: 

- 移至 [新增或移除程式]
- 卸載 Microsoft ASP.NET 和 Web 工具 2012.2(如果存在)。
- 重新安裝微軟ASP.NET和網路工具 2012.2

#### <a name="after-uninstalling-aspnet-and-web-tools-20122-the-aspnet-mvc-4-templates-and-razor-v2-web-site-templates-are-missing"></a>卸載ASP.NET和 Web 工具 2012.2 後,缺少ASP.NET MVC 4 範本和 Razor v2 網站範本

卸載ASP.NET和 Web 工具 2012.2 還將從 Visual Studio 2012 卸載所有ASP.NET MVC 4 和 Razor v2 網站範本。

解決方法是修復 Visual Studio 2012 安裝,以重新安裝ASP.NET MVC 4 和 Razor v2 網站範本。

### <a name="tooling-issues"></a>工具問題

#### <a name="nuget-error-reported-during-project-creation"></a>專案建立期間回報的 NuGet 錯誤

安裝ASP.NET和 Web 工具 2012.2 後,在建立 MVC 4 專案時可能會看到以下錯誤

![](aspnet-and-web-tools-20122-release-notes-rtw/_static/image1.png)

ASP.NET和網路工具 2012.2 船舶 NuGet 2.1,並將升級 Visual Studio 2012 中的擴展。 在某些情況下,VSIX 安裝程式將無法正確更新 VSIX。 以下步驟將允許您解決此問題:

1. 以管理員身份開始視覺工作室 2012
2. 跳到工具&gt;- 擴充和更新,卸載 NuGet。
3. 關閉 Visual Studio
4. 導覽到ASP.NET和 Web 工具 2012.2 安裝資料夾:

    1. 對於視覺工作室 2012:**程式檔_微軟 ASP.NET_ASP.NET 網路堆疊_視覺工作室 2012**
    2. 對於 Visual Studio 2012 Web 快訊:**程式檔案_微軟 ASP.NET_ASP.NET Web 堆疊_Visual Studio Express 2012 網頁**
5. 雙擊 NuGet.Tools.vsix 重新安裝 NuGet

### <a name="web-api-issues"></a>Web API 問題

#### <a name="parsing-issues-in-filter-and-datetime-literals"></a>分析$filter和 DateTime 文字中的問題

OData URI 解析器無法正確解析部分日期時間文本。 例如,$filter_開始 eq 日期時間『2012-12-31T12:00』 無法正確解析。 解決方法是使用完整的文本,$filter_開始 eq 日期時間『2012-12-31T12:00:00』。

#### <a name="odata-doesnt-support-case-insensitive-property-names"></a>OData 不支援不區分大小寫的屬性名稱。

OData 不支援 OData 查詢和 odata 路徑中不區分大小寫的屬性名稱。 請參考工作項目:

- [http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)
- [http://aspnetwebstack.codeplex.com/workitem/704](http://aspnetwebstack.codeplex.com/workitem/704)

如果使用者在 javascript 用戶端和伺服器端具有不同的大小寫,他們可能會遇到此問題。 此問題是在 odata 協定中設計的問題。 但是,許多用戶報告此問題。 要解決此問題,用戶必須更正 URL 中的情況。

#### <a name="default-odata-routing-conventions-doesnt-support-postput-on-navigation-property"></a>默認 OData 路由約定不支援導航屬性上的 POST/PUT。

默認 OData 路由約定不支援導航屬性上的 POST/PUT。 請參考工作項目[http://aspnetwebstack.codeplex.com/workitem/366](http://aspnetwebstack.codeplex.com/workitem/366)。 在默認約定中,我們缺少此常用約定。

要解決它,使用者需要擴展新的路由約定來支援它。

### <a name="facebook-template-issues"></a>Facebook 樣本問題

#### <a name="facebook-application-template-only-works-using-net-45"></a>Facebook 應用程式樣本僅適用於 .NET 4.5

您必須在"新項目"對話框的框架下拉清單中選擇 .NET 4.5,才能在 mVC 4 ASP.NET中查看 Facebook 應用程式範本。

#### <a name="real-time-update-controller"></a>即時更新控制器

Facebook 應用程式樣本允許使用者輕鬆創建 Web API 控制器來處理來自 Facebook 的即時更新。 如果開發計算機位於 NAT 之後,則如果沒有進一步的網路配置,控制器可能無法工作。 有關詳細資訊,請參閱此處:[http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook](http://facebook.stackoverflow.com/questions/5259467/can-a-computer-behind-a-nat-router-receive-realtime-updates-from-facebook)

#### <a name="query-string-values-conflict-with-facebook-oauth-parameters"></a>查詢字串值與 Facebook OAuth 參數衝突

以下欄位與 Facebook OAuth 對話框的回調 URL 衝突。 不要添加具有以下名稱的查詢字串值:代碼、錯誤、錯誤\_描述、錯誤\_原因。

#### <a name="using-page-inspector-with-facebook-template"></a>使用帶有 Facebook 樣本的頁面檢查器

除錯 Facebook 應用程式時,不能在 Visual Studio 2012 中使用頁面檢查器功能。 頁面檢查器當前不支援 iframe。

### <a name="single-page-application-template-issues"></a>單頁應用程式樣本問題

#### <a name="with-jquery-19knockout-221-update-when-running-default-mvc-spa-project-new-todo-item-edit-enter-focus-event-is-not-handled-properly"></a>使用 JQuery 1.9/挖空 2.2.1 更新時,在運行預設 MVC SPA 專案時,新的 todo 項編輯輸入焦點事件處理不正確。

使用 JQuery 1.9/挖空 2.2.1 更新,在運行預設 MVC SPA 專案時,新待辦事項編輯在進入待辦事項清單的新待辦事項後不再聚焦到新的待辦事項編輯框。

要進行解決方法引用[http://knockoutjs.com/documentation/hasfocus-binding.html](http://knockoutjs.com/documentation/hasfocus-binding.html),並針對以下範例代碼進行類似的修復:

檔案 todo.model.js  
 函數待辦事項(資料),添加以下內容:  
 **自我.is選定 = ko.可觀察(假);**

函數 todoList.原型.addTodo,添加以下黑色文字:  
 **自我.是選擇(真);**  
 自我.新托多標題();&quot; &quot;

檔案索引.cshtml,新增以下黑色文字:  
 &lt;表單資料繫結檔&quot;檔:新增Todo&quot;&gt;  
 &lt;輸入類=&quot;addTodo&quot;&quot;類型&quot;&quot;= 文字資料 綁定= 值:newTodoTitle,占位符:"在此處鍵入添加",模糊OnEnter:true,**有焦點:是選定**,事件:[模糊:添加Todo]&quot; /&gt;  
 &lt;/形式&gt;
