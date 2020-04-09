---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: (包括 2011 年 4 月工具更新)ASP.NET MVC 3 是一個框架,用於使用成熟的設計模式建譯可擴充的、基於標準的 Web 應用程式...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 6fe734dc0d0106bb346df154e1e03f97b307567a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675144"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *(包括 2011 年 4 月工具更新)*
> 
> ASP.NET MVC 3 是一個框架,用於使用成熟的設計模式以及 ASP.NET 和 .NET 框架的強大功能建構可擴展的、基於標準的 Web 應用程式。
> 
> 它與mVC ASP.NET並行安裝,所以立即開始使用它!
> 
> 在此處下載[安裝程式](https://microsoft.com/download/details.aspx?id=4211)

## <a name="top-features"></a>熱門功能

- 整合式腳手架系統可透過 NuGet 進行擴充
- 開啟 HTML 5 的項目樣本
- 表現性檢視,包括新的剃刀檢視引擎
- 具有相依項碼和全域操作篩選器的強大掛鉤
- 具有不顯眼的 JavaScript、jQuery 驗證和 JSON 綁定的豐富 JAvaScript 支援
- *閱讀[下面的](#overview)完整功能清單*

## <a name="top-links"></a>熱門連結

ASP.NET MVC 3 中的新增功能

- 菲爾·哈克[:ASP.NET MVC 3 發佈](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- 斯科特·漢塞爾曼[:ASP.NET MVC3、WebMatrix、NuGet、IIS 快遞和果園發佈 - 微軟 1 月 Web 發布上下文](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- 斯科特·古斯裡:[宣佈發佈ASP.NET MVC 3,IIS 快遞,SQL CE 4,網路農場框架,果園,WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [ASP.NET MVC 3 的發行說明](../whitepapers/mvc3-release-notes.md)

安裝並説明

- 使用 Web 平台安裝程式安裝 ASP.NET MVC [3(建議)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- 使用[安裝程式執行檔](https://go.microsoft.com/fwlink/?LinkID=208140)安裝ASP.NET MVC 3
- 安裝[ASP.NET MVC 3 用於視覺化工作室 11 開發人員預覽](https://go.microsoft.com/fwlink/?LinkID=208140)
- 閱讀[簡介以ASP.NET MVC 3 教程](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)
- 在[論壇](https://forums.asp.net/1146.aspx)中獲取有關 MVC 3 ASP.NET幫助和討論

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 概觀 (英文)

ASP.NET MVC 3 建立在 ASP.NET MVC 1 和 2 的基礎上,增加了既簡化了代碼又允許更深度擴展性的偉大功能。 本主題概述了此版本中包括的許多新功能,這些功能分為以下各節:

- [透過 Mvc Scaffold 整合式延伸腳手架](#BM_MvcScaffolding)
- [開啟 HTML 5 的項目樣本](#BM_HTML5)
- [剃刀檢視引擎](#BM_TheRazorViewEngine)
- [支援多檢視引擎](#BM_Support_for_Multiple_View_Engines)
- [控制器改進](#BM_Controller_Improvements)
- [JavaScript 和 Ajax](#BM_JavaScript_and_Ajax_Improvements)
- [模型驗證改進](#BM_Model_Validation_Improvements)
- [相依項改進](#BM_Dependency_Injection_Improvements)
- [其他新功能](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>透過 Mvc Scaffold 整合式延伸腳手架

新的 Scaffoldsing 系統使您能夠更輕鬆地拿起並開始高效使用,如果您是框架的完全新,並且如果您經驗豐富且已經知道正在做什麼,則自動執行常見開發任務。

這是由新的NuGet*腳手架*包支援,稱為**Mvc 腳手架**。 許多軟體技術使用術語「Scaffolding」表示「快速生成軟體的基本大綱,然後您可以編輯和自定義」。 我們為ASP.NET MVC 創建的腳手架包在幾個方案中非常有用:

- **如果你第一次學習ASP.NETMVC,** 因為它為您提供了一種快速的方式來獲得一些有用的工作代碼,然後你可以根據您的需要進行編輯和調整。 它為您從看著空白頁面的創傷中拯救,並且不知道從哪裡開始!
- **如果您對 MVC ASP.NET非常瞭解,並且正在探索一些新的附加技術**,如對象關係映射器、視圖引擎、測試庫等,因為該技術的創建者可能也為它創建了一個基架包。
- **如果工作涉及重複創建類似類或某種檔**,因為您可以創建自定義基架,以輸出測試夾具、部署腳本或其他任何需要。 團隊中的每個人都可以使用自定義腳手架。

MvcScaffoldsing 中的其他功能包括:

- 支援 C# 與 VB 專案
- 支援剃刀與 ASPX 檢視引擎
- 支援將腳手架放入ASP.NET MVC 區域並使用自訂檢視佈局/主機
- 您可以透過編輯 T4 樣本輕鬆自訂輸出
- 您可以使用自定義 PowerShell 邏輯和自訂 T4 範本添加全新的基架。 這些參數(以及您提供給它們的任何自定義參數)會自動顯示在控制台選項卡完成清單中。
- 您可以取得包含不同技術的其他基架支架的 NuGet 套件(例如,現在 LINQ 到 SQL 都有一個概念驗證套件),並將它們混合並符合在一起

ASP.NET MVC 3 工具更新包括針對此基架系統的巨大 Visual Studio 支援,例如:

- 新增控制器對話框現在支援建立、讀取、更新和刪除控制器操作和相應檢視的完整自動基架。 預設情況下,此基架數據存取代碼使用 EF 代碼優先。
- 新增控制器對話框支援透過 NuGet 套件(如*MvcScaffold)**進行擴充基架*。 這允許將自定義基架插入對話框中,這樣,如果您傾向於的話,您可以為其他數據訪問技術(如 NHibernate)創建基架,甚至使用 ODBCDirect 的 JET!

有關 ASP.NET MVC 3 中的基架的詳細資訊,請參閱以下資源:

- 史蒂夫·桑德森的系列帖子,包括: 

    1. [簡介: 使用 MvcScaffoldss 封裝,ASP.NET MVC 3 專案腳手架](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [標準用法:典型用例和選項](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [一對多關係](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [文手架操作和單元測試](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [覆寫 T4 樣本](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [這篇文章:建立自訂腳手架](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- 斯科特·漢塞爾曼的帖子從他的PDC 2010會話[建立博客與微軟"未命名的網络愛包"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)
- [MVC 3 發行說明](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>HTML 5 專案範本

"新項目"對話框包括一個複選框,該複選框啟用 HTML 5 版本的項目範本。 這些樣本利用 Modernizr 1.7 在低級瀏覽器中為 HTML 5 和 CSS 3 提供相容性支援。

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>剃刀檢視引擎

ASP.NET MVC 3 附帶了名為 Razor 的新檢視引擎,具有以下優點:

- 剃刀語法簡潔簡潔,需要最少的擊鍵次數。
- Razor 易於學習,部分原因在於它基於現有語言(如 C# 和 Visual Basic)。
- 可視化工作室包括用於 Razor 語法的 IntelliSense 和代碼著色。
- Razor 檢視可以進行單元測試,而無需運行應用程式或啟動 Web 伺服器。

一些新的 Razor 功能包括:

- `@model`用於指定傳遞給檢視的類型的語法。
- `@* *@`註釋語法。
- 為整個網站指定預設值(如`layoutpage`) 一次的能力。
- 顯示`Html.Raw`文字而不進行 HTML 編碼的方法。
- 支援在多個檢視之間共享代碼(*\_檢視 start.cshtml*或*\_viewstart.vbhtml*檔案)。

Razor 還包括新的 HTML 說明器,如下所示:

- `Chart`. 渲染圖表,提供與 ASP.NET 4 中的圖表控件相同的要素。
- `WebGrid`. 渲染數據網格,完成分頁和排序功能。
- `Crypto`. 使用哈希演演演算法創建正確加鹽和哈希密碼。
- `WebImage`. 渲染圖像。
- `WebMail`. 傳送電子郵件訊息。

有關 Razor 的詳細資訊,請參閱以下資源:

- [斯科特·古斯裡的博客文章介紹剃刀](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [斯科特·古斯裡的博客文章介紹關鍵字@model](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [斯科特·古斯裡的博客文章介紹剃刀佈局](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [剃刀 API 快速參考](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [MVC 3 發行說明](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>支援多檢視引擎

ASP.NET MVC 3 中的 **「新增檢視」** 對話框允許您選擇要使用的檢視引擎,而 **「新專案**」對話框允許您為專案指定預設檢視引擎。 您可以選擇 Web 窗體檢視引擎 (ASPX)、Razor 或開源檢視引擎(如[Spark、NHaml](https://code.google.com/p/nhaml/)或[Spark](http://sparkviewengine.com/)[NDjango)。](http://ndjango.org/)

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>控制器改進

### <a name="global-action-filters"></a>全域操作篩選器

有時,您希望在操作方法運行之前或操作方法運行之前執行邏輯。 為了支援這一點,ASP.NET MVC 2 提供了操作篩選器。 操作篩選器是自定義屬性,提供聲明性方法,將操作前和操作後行為添加到特定的控制器操作方法。 但是,在某些情況下,您可能希望指定適用於所有操作方法的操作前或行動後行為。 MVC 3 允許您通過將全域篩選器添加`GlobalFilters`到 集合來指定全域篩選器。 有關全域操作篩選器的詳細資訊,請參閱以下資源:

- [斯科特·古斯裡在MVC 3預覽的博客](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [ASP.NET MVC 中的篩選](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>新的「檢視袋」屬性

MVC 2`ViewData`控制器 支援一個屬性,該屬性使您能夠使用後期綁定字典 API 將數據傳遞到檢視範本。 在 MVC 3 中,還可以對屬性`ViewBag`使用更簡單 的語法來實現相同的目的。 例如,可以寫入`ViewData["Message"]="text"`而不是`ViewBag.Message="text"`寫入 。 不需要定義任何強型態類別使用`ViewBag`屬性 。 因為它是動態屬性,因此只需獲取或設置屬性,它將在運行時動態解析它們。 在內部`ViewBag`,屬性`ViewData`在字典中存儲為名稱/值對。 (注意:在大多數預發行版本的 MVC 3`ViewBag`中, 屬性`ViewModel`被命名為屬性 。

### <a name="new-actionresult-types"></a>新的「動作結果」類型

以下`ActionResult`類型與相應的說明器方法在 MVC 3 中是新的或增強的:

- [HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx)。 將 404 HTTP 狀態代碼返回給用戶端。
- [重定向結果](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)。 返回臨時重定向 (HTTP 302 狀態代碼) 或永久重定向 (HTTP 301 狀態代碼),具體取決於布爾參數。 結合此變更[,Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx)類別現在有三種執行永久重定向的方法`RedirectPermanent``RedirectToRoutePermanent`:、 和`RedirectToActionPermanent`。 這些方法返回`RedirectResult``Permanent`屬性設置`true`為 的實例。
- [HTTPStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx). 返回使用者指定的 HTTP 狀態代碼。

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>JavaScript 和 Ajax 改進

默認情況下,MVC 3 中的 Ajax 和驗證説明程式使用不顯眼的 JavaScript 方法。 不顯眼的 JavaScript 避免將內聯 JAvaScript 注入 HTML。 這使得您的 HTML 更小且不太混亂,並且更易於交換或自定義 JavaScript 庫。 默認情況下,MVC `jQueryValidate` 3 中的驗證説明程式也使用該外掛程式。 如果需要 MVC 2 行為,可以使用*Web.config*檔設置禁用不顯眼的 JavaScript。 有關 JavaScript 和 Ajax 改進的詳細資訊,請參閱以下資源:

- [維琪百科網站上不顯眼的JAVAScript的基本介紹](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [布拉德·威爾遜的《不顯眼的JAVAScript》帖子](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [布拉德·威爾遜的《不顯眼的JAVA腳本驗證帖》](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [使用 Razor 與不顯眼的 JavaScript 建立 MVC 3 應用程式](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md)(ASP.NET網站上的教程)
- [MVC 3 發行說明](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>預設使用客戶端驗證

在早期版本的 MVC 中,需要從檢視中顯式調`Html.EnableClientValidation`用方法,以便啟用客戶端驗證。 在 MVC 3 中,這不再需要,因為默認情況下啟用客戶端驗證。 (您可以使用*Web.config*檔中的設定禁用此功能。

為了使客戶端驗證正常工作,您仍然需要引用網站中相應的 jQuery 和 jQuery 驗證庫。 您可以在自己的伺服器上託管這些庫,也可以從內容交付網路 (CDN)(如 Microsoft 或 Google 的 CDN)中引用它們。

### <a name="remote-validator"></a>遠端驗證器

ASP.NET MVC 3 支援新的[RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx)類,使您能夠利用 jQuery 驗證外掛程式的遠端驗證器支援。 這使客戶端驗證庫能夠自動呼叫您在伺服器上定義的自訂方法,以便執行只能執行伺服器端的驗證邏輯。

`Remote`在下面的範例中,該屬性指定客戶端驗證將調`UserNameAvailable``UsersController`用 類上命名的操作以`UserName`驗證該 欄位。

[!code-csharp[Main](mvc3/samples/sample1.cs)]

下面的示例顯示了相應的控制器。

[!code-csharp[Main](mvc3/samples/sample2.cs)]

有關如何使用`Remote`該屬性的詳細資訊,請參閱如何:在 MSDN 函式庫中[ASP.NET MVC 中實現遠端驗證](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)。

### <a name="json-binding-support"></a>JSON 繫結支援

ASP.NET MVC 3 包括內建的 JSON 綁定支援,使操作方法能夠接收 JSON 編碼的數據,並將其模型綁定到操作方法參數。 此功能在涉及用戶端範本和數據綁定的方案中非常有用。 (用戶端範本使您能夠使用在用戶端上執行的範本格式化和顯示單個資料項或資料項集。MVC 3 使您能夠輕鬆地將用戶端範本與發送和接收 JSON 數據的伺服器上的操作方法連接。 有關 JSON 綁定支援的詳細資訊,請參閱[Scott Guthrie 的 MVC 3 預覽部落格文章的](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx) **JavaScript 和 AJAX 改進**部分。

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>模型驗證改進

### <a name="dataannotations-metadata-attributes"></a>「資料註解」中繼資料屬性

ASP.NET MVC `DataAnnotations` 3`DisplayAttribute`支援中繼資料屬性,如 。

### <a name="validationattribute-class"></a>『驗證屬性』類別

在`ValidationAttribute`.NET 框架 4 中`IsValid`改進了該類,以支援新的重載,該重載提供有關當前驗證上下文的詳細資訊,例如正在驗證的物件。 這支援更豐富的方案,您可以在其中根據模型的另一個屬性驗證當前值。 例如,新`CompareAttribute`屬性允許您比較模型的兩個屬性的值。 在下面的範例中,`ComparePassword`屬性必須`Password`符合 該欄位才能有效。

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>驗證介面

[IValidaobject 介面](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx)使您能夠執行模型級驗證,並且它使您能夠提供特定於整個模型狀態的驗證錯誤消息,或在模型中的兩個屬性之間。 MVC 3`IValidatableObject`現在從 模型綁定時從介面檢索錯誤,並使用內置的 HTML 表單説明器自動標記或突出顯示視圖中受影響的欄位。

[IClientValidaa 可介面](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx)使ASP.NET MVC 能夠在運行時發現驗證器是否支援客戶端驗證。 此介面的設計使其可以與各種驗證框架集成。

有關驗證介面的詳細資訊,請參閱[Scott Guthrie 的 MVC 3 預覽部落格文章的](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)**模型驗證改進**部分。 (但是,請注意,博客中對"IValidateObject"的引用應為"IValidaaobject"。

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>相依項改進

ASP.NET MVC 3 為應用依賴項注入 (DI) 和與依賴項注入或控制反轉 (IOC) 容器集成提供更好的支援。 在以下領域新增了對 DI 的支援:

- 控制器(註冊和注入控制器工廠,注入控制器)。
- 視圖(註冊和注入視圖引擎,將依賴項注入視圖頁)。
- 操作篩選器(定位和注入篩檢程式)。
- 模型活頁夾(註冊和注入)。
- 模型驗證提供程式(註冊和注入)。
- 建模元數據提供程式(註冊和注入)。
- 價值提供者(註冊和注入)。

MVC 3 支援[通用服務定位器](https://github.com/unitycontainer/commonservicelocator)庫`IServiceLocator`和支援該庫 介面的任何 DI 容器。 它還支援一個新的`IDependencyResolver`介面,使集成 DI 框架變得更加容易。

有關 MVC 3 中的 DI 的詳細資訊,請參閱以下資源:

- [布拉德·威爾遜關於服務地點的一系列博客文章](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [MVC 3 發行說明](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>其他新功能

### <a name="nuget-integration"></a>NuGet 整合

ASP.NET MVC 3 自動安裝並啟用 NuGet 作為其設置的一部分。 NuGet 是免費的開源套件管理員,可讓您在專案中輕鬆搜尋、安裝和使用.NET庫和工具。 它適用於所有 Visual Studio 專案類型(包括ASP.NET Web 窗體和ASP.NET MVC)。

NuGet 使維護開源專案的開發人員(例如,像 Moq、NHibernate、Ninject、結構映射、NUnit、溫莎、RhinoMocks 和 Elmah)的專案)能夠打包其庫並將其註冊到線上庫中。 然後,想要使用這些庫之一的 .NET 開發人員可以輕鬆查找包並將其安裝在他們正在處理的專案中。

通過ASP.NET 3 工具更新,專案範本包括預安裝的 NuGet 包的 JavaScript 庫,因此它們可以通過 NuGet 進行更新。 實體框架代碼優先也預裝為 NuGet 包。

如需 NuGet 的詳細資訊，請參閱 [NuGet 文件](https://docs.microsoft.com/nuget/) (英文)。

### <a name="partial-page-output-caching"></a>部份頁面輸出快取

自版本 1 以來ASP.NET MVC 都支援整頁回應的輸出緩存。 MVC 3 還支援部分頁面輸出緩存,這允許您輕鬆緩存回應的區域或片段。 有關緩存的詳細資訊,請參閱[Scott Guthrie 在 MVC 3 版本候選版和 MVC](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) [3 發行說明](../whitepapers/mvc3-release-notes.md)的 **「子操作輸出緩存**」部分部分頁面**輸出緩存**部分。

### <a name="granular-control-over-request-validation"></a>對要求驗證的精細控制

ASP.NET MVC 具有內置請求驗證,可自動幫助抵禦 XSS 和 HTML 注入攻擊。 但是,有時您希望顯式禁用請求驗證,例如,如果您希望允許使用者發佈 HTML 內容(例如,在部落格條目或 CMS 內容中)。 現在,您可以將[AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx)屬性添加到模型或視圖模型,以便在模型綁定期間禁用基於每個屬性的請求驗證。 有關請求驗證的詳細資訊,請參閱以下資源:

- [斯科特·古斯裡關於MVC 3版本候選的博客文章](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)中的 **「不顯眼的JavaScript和驗證**」部分。
- [MVC 3 發行說明](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>可擴充的「新項目」對話框

在 mVC 3 ASP.NET,您可以將專案範本、檢視引擎和單元測試專案框架添加到 **「新項目**」對話框中。

### <a name="template-scaffolding-improvements"></a>樣本基架改進

ASP.NET MVC 3 基架範本比早期版本的 MVC 更好地識別模型上的主鍵屬性並適當地處理它們。 (例如,基架範本現在確保主鍵不是基架作為可編輯的表單欄位。

默認情況下,"創建和編輯"基架現在使用`Html.EditorFor`幫助器而不是`Html.TextBoxFor`幫助程式。 這在 **「添加檢視」** 對話框生成檢視時,改進了對模型上以數據註釋屬性形式對元數據的支援。

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>"Html.Labelfor"和"Html.LabelFormodel"的新重載

已為`LabelFor`和`LabelForModel`幫助器方法添加了新方法重載。 新的重載讓您能夠指定或覆蓋分頁文本。

### <a name="sessionless-controller-support"></a>無工作階段控制器支援

在 mVC 3 ASP.NET 中,可以指示是否希望控制器類使用會話狀態,如果是,會話狀態應是讀/寫還是只讀。 有關無會話控制器支援的詳細資訊,請參閱[MVC 3 發行說明](../whitepapers/mvc3-release-notes.md)。

### <a name="new-additionalmetadataattribute-class"></a>新的「附加元資料屬性」 類別

可以使用[「附加元數據」](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx)屬性填充模型`ModelMetadata.AdditionalValues`屬性的 字典。 例如,如果檢視模型具有僅應向管理員顯示的屬性,則可以對該屬性進行加帶,如以下示例所示:

[!code-csharp[Main](mvc3/samples/sample4.cs)]

呈現產品檢視模型時,此元數據可用於任何顯示或編輯器範本。 由您解釋元數據資訊。

### <a name="accountcontroller-improvements"></a>帳號控制器改進

互聯網專案範本中的帳戶控制器已大為改善。

### <a name="new-intranet-project-template"></a>新的內聯網項目範本

包含新的 Intranet 專案樣本,該範本啟用 Windows 身份驗證並刪除帳戶控制器。
