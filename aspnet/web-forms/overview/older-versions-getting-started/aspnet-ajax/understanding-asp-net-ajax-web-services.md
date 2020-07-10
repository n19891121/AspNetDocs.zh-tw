---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
title: 瞭解 ASP.NET AJAX Web 服務 |Microsoft Docs
author: scottcate
description: Web 服務是 .NET framework 不可或缺的一部分，可提供跨平臺的解決方案，在分散式系統之間交換資料。 雖然 Web .。。
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 3332d6e7-e2e1-4144-b805-e71d51e7e415
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
msc.type: authoredcontent
ms.openlocfilehash: eac3d53fd871d0cb5a2870488ce752c057cc5b1a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "86162762"
---
# <a name="understanding-aspnet-ajax-web-services"></a>了解 ASP.NET AJAX Web 服務

由[Scott Cate](https://github.com/scottcate)

[下載 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial05_Web_Services_with_MS_Ajax_cs.pdf)

> Web 服務是 .NET framework 不可或缺的一部分，可提供跨平臺的解決方案，在分散式系統之間交換資料。 雖然 Web 服務通常用來允許不同的作業系統、物件模型和程式語言傳送和接收資料，它們也可以用來以動態方式將資料插入 ASP.NET AJAX 頁面，或將資料從頁面傳送到後端系統。 這一切都可以完成，而不需要進行回傳作業。

## <a name="calling-web-services-with-aspnet-ajax"></a>使用 ASP.NET AJAX 呼叫 Web 服務

Dan Wahlin

Web 服務是 .NET framework 不可或缺的一部分，可提供跨平臺的解決方案，在分散式系統之間交換資料。 雖然 Web 服務通常用來允許不同的作業系統、物件模型和程式語言傳送和接收資料，它們也可以用來以動態方式將資料插入 ASP.NET AJAX 頁面，或將資料從頁面傳送到後端系統。 這一切都可以完成，而不需要進行回傳作業。

雖然 ASP.NET AJAX UpdatePanel 控制項提供簡單的方式來啟用任何 ASP.NET 網頁，但有時您可能需要在不使用 UpdatePanel 的情況下動態存取伺服器上的資料。 在本文中，您將瞭解如何藉由在 ASP.NET AJAX 頁面中建立及使用 Web 服務來完成這項工作。

本文將著重于核心 ASP.NET AJAX 延伸模組中提供的功能，以及在 ASP.NET AJAX 工具組中啟用的 Web 服務控制項，稱為 AutoCompleteExtender。 涵蓋的主題包括定義啟用 AJAX 的 Web 服務、建立用戶端 proxy，以及使用 JavaScript 呼叫 Web 服務。 您也會看到 Web 服務呼叫如何直接進行 ASP.NET 網頁方法。

## <a name="web-services-configuration"></a>Web 服務設定

當使用 Visual Studio 2008 建立新的網站專案時，web.config 檔案有一些新新增功能，可能不熟悉舊版 Visual Studio 的使用者。 其中一些修改會將 "asp" 前置詞對應至 ASP.NET AJAX 控制項，讓它們可以在頁面中使用，而有些則會定義必要的 HttpHandlers 和 HttpModules。 [清單 1] 顯示對 `<httpHandlers>` web.config 影響 Web 服務呼叫的元素所做的修改。 用來處理 .asmx 呼叫的預設 HttpHandler 會被移除，並取代為位於 System.Web.Extensions.dll 元件中的 ScriptHandlerFactory 類別。 System.Web.Extensions.dll 包含 ASP.NET AJAX 所使用的所有核心功能。

**[清單 1]。ASP.NET AJAX Web 服務處理常式設定**

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample1.xml)]

這項 HttpHandler 取代的目的是為了讓 JavaScript 物件標記法 (JSON) 呼叫使用 JavaScript Web 服務 proxy 從 ASP.NET AJAX 頁面進行到 .NET Web 服務。 ASP.NET AJAX 會將 JSON 訊息傳送至 Web 服務，而不是標準的簡單物件存取通訊協定， (SOAP) 呼叫通常與 Web 服務相關聯。 這會導致整體的要求和回應訊息變小。 它也可讓用戶端更有效率地處理資料，因為 ASP.NET AJAX JavaScript 程式庫已優化，可搭配 JSON 物件使用。 [清單 2] 和 [清單 3] 顯示序列化為 JSON 格式的 Web 服務要求和回應訊息的範例。 [清單 2] 中顯示的要求訊息會傳遞值為「比利時」的國家（地區）參數，而 [清單 3] 中的回應訊息則會傳遞客戶物件的陣列及其相關聯的屬性。

**[清單 2]。序列化為 JSON 的 Web 服務要求訊息**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample2.json)]

> *>作業 [!NOTE] 名稱會定義為 web 服務 URL 的一部分; 此外，要求訊息不一定會透過 JSON 提交。Web 服務可以利用 ScriptMethod 屬性，並將 UseHttpGet 參數設定為 true，這會導致透過查詢字串參數傳遞參數。*

**[清單 3]。序列化為 JSON 的 Web 服務回應訊息**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample3.json)]

在下一節中，您將瞭解如何建立能夠處理 JSON 要求訊息的 Web 服務，並同時回應簡單和複雜類型。

## <a name="creating-ajax-enabled-web-services"></a>建立啟用 AJAX 的 Web 服務

ASP.NET AJAX 架構提供數種不同的方式來呼叫 Web 服務。 您可以使用 ASP.NET AJAX 工具組中所提供的 AutoCompleteExtender 控制項 () 或 JavaScript。 不過，在呼叫服務之前，您必須先啟用 AJAX，讓用戶端腳本能夠呼叫它。

無論您是否熟悉 ASP.NET Web 服務，都可以直接建立和啟用 AJAX 的服務。 .NET framework 已支援建立 ASP.NET Web 服務，因為它在2002中的初始版本，而 ASP.NET AJAX Extensions 則提供以 .NET framework 的預設功能集為基礎的其他 AJAX 功能。 Visual Studio .NET 2008 Beta 2 提供建立 .asmx Web 服務檔案的內建支援，並自動從 System.web 類別衍生類別旁的相關程式碼。 當您將方法加入至類別時，您必須套用 WebMethod 屬性，才能讓 Web 服務取用者呼叫它們。

[清單 4] 顯示將 WebMethod 屬性套用至名為 GetCustomersByCountry ( # A1 之方法的範例。

**[清單 4]。在 Web 服務中使用 WebMethod 屬性**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample4.cs)]

GetCustomersByCountry ( # A1 方法會接受 country 參數，並傳回 Customer 物件陣列。 傳入方法的國家（地區）值會轉送到商業層類別，然後再呼叫資料層類別來抓取資料庫中的資料、以資料填入 Customer 物件屬性，並傳回陣列。

## <a name="using-the-scriptservice-attribute"></a>使用 ScriptService 屬性

加入 WebMethod 屬性時，可讓用戶端呼叫 GetCustomersByCountry ( # A1 方法，以將標準的 SOAP 訊息傳送至 Web 服務，而不允許從現成的 ASP.NET AJAX 應用程式進行 JSON 呼叫。 若要允許進行 JSON 呼叫，您必須將 ASP.NET AJAX 延伸模組的 `ScriptService` 屬性套用至 Web 服務類別。 這可讓 Web 服務傳送使用 JSON 格式化的回應訊息，並允許用戶端腳本藉由傳送 JSON 訊息來呼叫服務。

[清單 5] 顯示將 ScriptService 屬性套用至名為 CustomersService 的 Web 服務類別的範例。

**[清單 5]。使用 ScriptService 屬性來啟用 Web 服務的 AJAX**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample5.cs)]

ScriptService 屬性會作為標記，表示可以從 AJAX 腳本呼叫它。 它實際上不會處理幕後發生的任何 JSON 序列化或還原序列化工作。 web.config) 和其他相關類別中設定的 ScriptHandlerFactory (會執行大量的 JSON 處理。

## <a name="using-the-scriptmethod-attribute"></a>使用 ScriptMethod 屬性

ScriptService 屬性是唯一必須在 .NET Web 服務中定義的 ASP.NET AJAX 屬性，以便 ASP.NET AJAX 頁面使用。 不過，另一個名為 ScriptMethod 的屬性也可以直接套用至服務中的 Web 方法。 ScriptMethod 會定義三個屬性 `UseHttpGet` ，包括、 `ResponseFormat` 和 `XmlSerializeString` 。 變更這些屬性的值，對於當 web 方法所接受的要求類型需要變更為 GET 時，如果 Web 方法需要以或物件的形式傳回未經處理的 XML 資料， `XmlDocument` `XmlElement` 或是從服務傳回的資料一律序列化為 XML 而非 JSON，則會很有用。

當 Web 方法應該接受 GET 要求，而不是 POST 要求時，可以使用 UseHttpGet 屬性。 系統會使用 URL 來傳送要求，而 Web 方法輸入參數會轉換成 QueryString 參數。 UseHttpGet 屬性預設為 false，而且只有 `true` 在已知的作業是安全的，而且機密資料未傳遞至 Web 服務時，才會設定為。 [清單 6] 顯示使用 ScriptMethod 屬性搭配 UseHttpGet 屬性的範例。

**[清單 6]。搭配 UseHttpGet 屬性使用 ScriptMethod 屬性。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample6.cs)]

接下來會顯示在 [清單 6] 中所示的 HttpGetEcho Web 方法所傳送的標頭範例：

`GET /CustomerViewer/DemoService.asmx/HttpGetEcho?input=%22Input Value%22 HTTP/1.1`

除了允許 Web 方法接受 HTTP GET 要求之外，當需要從服務（而非 JSON）傳回 XML 回應時，也可以使用 ScriptMethod 屬性。 例如，Web 服務可能會從遠端網站抓取 RSS 摘要，並將其傳回為 Xml 形式或 XmlElement 物件。 接著，用戶端就可以處理 XML 資料。

[清單 7] 顯示使用 ResponseFormat 屬性指定應該從 Web 方法傳回 XML 資料的範例。

**[清單 7]。搭配 ResponseFormat 屬性使用 ScriptMethod 屬性。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample7.cs)]

ResponseFormat 屬性也可以與 XmlSerializeString 屬性一起使用。 XmlSerializeString 屬性的預設值為 false，表示當屬性設定為時，除了從 Web 方法傳回的字串以外的所有傳回類型都會序列化為 XML `ResponseFormat` `ResponseFormat.Xml` 。 當 `XmlSerializeString` 設定為時 `true` ，從 Web 方法傳回的所有類型都會序列化為包含字串類型的 XML。 如果 ResponseFormat 屬性具有 XmlSerializeString 屬性的值， `ResponseFormat.Json` 則會忽略。

[清單 8] 顯示使用 XmlSerializeString 屬性強制將字串序列化為 XML 的範例。

**[清單 8]。搭配 XmlSerializeString 屬性使用 ScriptMethod 屬性**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample8.cs)]

從呼叫 [清單 8] 所示的 GetXmlString Web 方法傳回的值如下所示：

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample9.cs)]

雖然預設的 JSON 格式會將要求和回應訊息的整體大小降至最低，而且 ASP.NET AJAX 用戶端更容易使用跨瀏覽器的方式，但當 Internet Explorer 5 或更高版本的用戶端應用程式需要從 Web 方法傳回 XML 資料時，可以使用 ResponseFormat 和 XmlSerializeString 屬性。

## <a name="working-with-complex-types"></a>使用複雜類型

[清單 5] 顯示的範例會從 Web 服務傳回名為 Customer 的複雜型別。 Customer 類別會在內部定義數個不同的簡單類型做為屬性（例如 FirstName 和 LastName）。 在啟用 AJAX 的 Web 方法上做為輸入參數或傳回類型的複雜類型，會在傳送至用戶端之前自動序列化為 JSON。 不過，內部部署的複雜類型 (在另一個類型內定義的) 不會做為獨立物件提供給用戶端使用。

如果 Web 服務所使用的嵌套複雜型別也必須在用戶端頁面中使用，則可以將 ASP.NET AJAX GenerateScriptType 屬性新增至 Web 服務。 例如，[清單 9] 中顯示的 CustomerDetails 類別包含***代表嵌套複雜類型***的位址和性別屬性。

**[清單 9]。此處顯示的 CustomerDetails 類別包含兩個嵌套的複雜類型。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample10.cs)]

在 [清單 9] 所示的 CustomerDetails 類別中定義的位址和性別物件，將不會自動提供給用戶端透過 JavaScript 使用，因為它們是巢狀型別 (位址是類別，而性別則是列舉) 。 在 Web 服務內使用的嵌套型別必須可在用戶端上使用的情況下，您可以使用稍早所述的 GenerateScriptType 屬性 (參閱清單 10) 。 當從服務傳回不同的嵌套複雜型別時，可以多次加入這個屬性。 它可以直接套用至 Web 服務類別或特定的 Web 方法。

**[清單 10]。使用 GenerateScriptService 屬性來定義應該可供用戶端使用的巢狀型別。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample11.cs)]

藉由將 `GenerateScriptType` 屬性套用至 Web 服務，位址和性別類型將會自動提供給用戶端 ASP.NET AJAX JavaScript 程式碼使用。 在 Web 服務上新增 GenerateScriptType 屬性會自動產生並傳送至用戶端的 JavaScript 範例，如 [清單 11] 所示。 您會在本文稍後看到如何使用嵌套的複雜類型。

**[清單 11]可供 ASP.NET AJAX 頁面使用的嵌套複雜型別。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample12.cs)]

既然您已瞭解如何建立 Web 服務，並讓它們可供 ASP.NET AJAX 頁面，讓我們看看如何建立和使用 JavaScript proxy，以便資料可以抓取或傳送至 Web 服務。

## <a name="creating-javascript-proxies"></a>建立 JavaScript proxy

 ( .NET 或另一個) 平臺呼叫標準 Web 服務時，通常會牽涉到建立 proxy 物件，讓您免于傳送 SOAP 要求和回應訊息的複雜性。 有了 ASP.NET AJAX Web 服務呼叫，您就可以建立 JavaScript proxy 並用來輕鬆地呼叫服務，而不必擔心序列化和還原序列化 JSON 訊息。 您可以使用 ASP.NET AJAX ScriptManager 控制項自動產生 JavaScript proxy。

建立可呼叫 Web 服務的 JavaScript proxy 是使用 ScriptManager 的服務屬性來完成。 這個屬性可讓您定義一個或多個服務，ASP.NET AJAX 頁面可以透過非同步方式呼叫來傳送或接收資料，而不需要回傳作業。 您可以使用 ASP.NET AJAX 控制項來定義服務 `ServiceReference` ，並將 Web 服務 URL 指派給控制項的 `Path` 屬性。 [清單 12] 顯示參考名為 CustomersService 之服務的範例。

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample13.aspx)]

**[清單 12]定義在 ASP.NET AJAX 頁面中使用的 Web 服務。**

透過 ScriptManager 控制項加入 CustomersService 的參考，會使 JavaScript proxy 動態產生並由頁面參考。 Proxy 是使用 &lt; 腳本 &gt; 標記內嵌，並藉由呼叫 CustomersService 並以動態方式載入，並將/js 附加至它的結尾。 下列範例顯示在 web.config 中停用了調試功能時，如何將 JavaScript proxy 內嵌在頁面中：

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample14.html)]

> *>[!NOTE]如果您想要查看產生的實際 JavaScript proxy 程式碼，您可以在 Internet Explorer 的 [位址] 方塊中輸入所需 .Net Web 服務的 URL，並將/js 附加至它的結尾。*

如果已在中啟用調試 web.config 則 JavaScript proxy 的 debug 版本將會內嵌在頁面中，如下所示：

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample15.html)]

ScriptManager 所建立的 JavaScript proxy 也可以直接內嵌在頁面中，而不是使用 &lt; 腳本 &gt; 標記的 src 屬性來參考。 這可以藉由將 ServiceReference 控制項的 InlineScript 屬性設為 true 來完成， (預設值為 false) 。 當 proxy 不是跨多個頁面共用，而且您想要減少對伺服器所做的網路呼叫數時，這會很有用。 當 InlineScript 設定為 true 時，瀏覽器將不會快取 proxy 腳本，因此，在 ASP.NET AJAX 應用程式中的多個頁面使用 proxy 的情況下，建議您使用預設值 false。 以下顯示使用 InlineScript 屬性的範例：

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample16.aspx)]

## <a name="using-javascript-proxies"></a>使用 JavaScript proxy

一旦使用 ScriptManager 控制項的 ASP.NET AJAX 頁面參考 Web 服務，就可以對 Web 服務進行呼叫，而傳回的資料則可使用回呼函數來處理。 Web 服務的呼叫方式是參考其命名空間， (如果存在) 、類別名稱和 Web 方法名稱。 傳遞至 Web 服務的任何參數都可以與處理傳回資料的回呼函數一起定義。

如需使用 JavaScript proxy 呼叫名為 GetCustomersByCountry 之 Web 方法的範例，請 ( # A1，如 [清單 13] 所示。 當終端使用者按一下頁面上的按鈕時，會呼叫 GetCustomersByCountry ( # A1 函式。

**[清單 13]。使用 JavaScript proxy 呼叫 Web 服務。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample17.js)]

此呼叫會參考服務中定義的 InterfaceTraining 命名空間、CustomersService 類別和 GetCustomersByCountry Web 方法。 它會傳遞從 textbox 取得的國家（地區）值，以及名為 OnWSRequestComplete 的回呼函式，該函式應該在非同步 Web 服務呼叫傳回時叫用。 OnWSRequestComplete 會處理從服務傳回的 Customer 物件陣列，並將其轉換成頁面中顯示的資料表。 從呼叫產生的輸出會顯示在 [圖 1] 中。

[![藉由對 Web 服務進行非同步 AJAX 呼叫來取得系結的資料。](understanding-asp-net-ajax-web-services/_static/image2.png)](understanding-asp-net-ajax-web-services/_static/image1.png)

**圖 1**：透過對 Web 服務進行非同步 AJAX 呼叫來取得系結的資料。   ([按一下以查看完整大小的影像](understanding-asp-net-ajax-web-services/_static/image3.png)) 

JavaScript proxy 也可以對 Web 服務進行單向呼叫，以便在應該呼叫 Web 方法但 proxy 不應等候回應的情況下進行。 例如，您可能會想要呼叫 Web 服務來啟動工作流程之類的進程，但不等候來自服務的傳回值。 在需要對服務進行單向呼叫的情況下，可以直接省略 [清單 13] 中所示的回呼函數。 因為未定義回呼函式，所以 proxy 物件不會等待 Web 服務傳回資料。

## <a name="handling-errors"></a>處理錯誤

對 Web 服務的非同步回呼可能會遇到不同類型的錯誤，例如網路關閉、Web 服務無法使用或傳回例外狀況。 幸運的是，ScriptManager 所產生的 JavaScript proxy 物件允許定義多個回呼來處理錯誤和失敗，以及稍早所示的成功回呼。 您可以在呼叫 Web 方法之後，立即定義錯誤回呼函式，如 [清單 14] 所示。

**[清單 14]。定義錯誤回呼函數並顯示錯誤。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample18.js)]

呼叫 Web 服務時所發生的任何錯誤將會觸發 OnWSRequestFailed ( # A1 回呼函式，以接受代表錯誤的物件做為參數。 錯誤物件會公開數個不同的函式，以判斷錯誤的原因，以及呼叫是否已超時。[清單 14] 顯示使用不同錯誤函式的範例，[圖 2] 顯示了函式所產生的輸出範例。

[![呼叫 ASP.NET AJAX error 函數所產生的輸出。](understanding-asp-net-ajax-web-services/_static/image5.png)](understanding-asp-net-ajax-web-services/_static/image4.png)

**圖 2**：藉由呼叫 ASP.NET AJAX error 函式所產生的輸出。   ([按一下以查看完整大小的影像](understanding-asp-net-ajax-web-services/_static/image6.png)) 

## <a name="handling-xml-data-returned-from-a-web-service"></a>處理從 Web 服務傳回的 XML 資料

您先前已看到 Web 方法如何使用 ScriptMethod 屬性及其 ResponseFormat 屬性來傳回原始 XML 資料。 當 ResponseFormat 設定為 ResponseFormat.Xml 時，從 Web 服務傳回的資料會序列化為 XML，而不是 JSON。 當 XML 資料需要直接傳遞給用戶端以使用 JavaScript 或 XSLT 進行處理時，這會很有用。 目前，Internet Explorer 5 或更新版本提供最佳的用戶端物件模型，可用於剖析和篩選 XML 資料，因為它內建的 MSXML 支援。

從 Web 服務抓取 XML 資料與抓取其他資料類型並無不同。 一開始先叫用 JavaScript proxy 呼叫適當的函式，並定義回呼函數。 一旦呼叫傳回之後，您就可以處理回呼函數中的資料。

[清單 15] 顯示的範例會呼叫名為 GetRssFeed 的 Web 方法， ( # A1 會傳回 XmlElement 物件。 GetRssFeed ( # A1 接受單一參數，代表要取得之 RSS 摘要的 URL。

**[清單 15]使用從 Web 服務傳回的 XML 資料。**

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample19.html)]

這個範例會將 URL 傳遞至 RSS 摘要，並處理 OnWSRequestComplete ( # A1 函數中傳回的 XML 資料。 OnWSRequestComplete ( # A1 會先檢查瀏覽器是否為 Internet Explorer，以瞭解 MSXML 剖析器是否可供使用。 如果是，就會使用 XPath 語句來尋找 RSS 摘要 &lt; &gt; 中的所有專案標記。 然後會逐一查看每個專案，並 &lt; 找出並處理相關聯的標題 &gt; 和 &lt; 連結 &gt; 標記，以顯示每個專案的資料。 [圖 3] 顯示透過 JavaScript proxy 對 GetRssFeed ( # A1 Web 方法進行 ASP.NET AJAX 呼叫所產生的輸出範例。

## <a name="handling-complex-types"></a>處理複雜類型

Web 服務接受或傳回的複雜類型會透過 JavaScript proxy 自動公開。 不過，除非已將 GenerateScriptType 屬性套用至服務（如先前所述），否則用戶端無法直接存取嵌套的複雜類型。 為什麼您要在用戶端上使用嵌套複雜型別？

若要回答這個問題，請假設 ASP.NET AJAX 頁面顯示客戶資料，並允許使用者更新客戶的位址。 如果 Web 服務指定的網址類別型 (在 CustomerDetails 類別內定義的複雜類型) 可以傳送至用戶端，則更新程式可以分割成不同的函式，以更有效率地重複使用程式碼。

[![從呼叫傳回 RSS 資料的 Web 服務建立的輸出。](understanding-asp-net-ajax-web-services/_static/image8.png)](understanding-asp-net-ajax-web-services/_static/image7.png)

**圖 3**：從呼叫傳回 RSS 資料的 Web 服務所建立的輸出。   ([按一下以查看完整大小的影像](understanding-asp-net-ajax-web-services/_static/image9.png)) 

[清單 16] 顯示用戶端程式代碼的範例，其會叫用在模型命名空間中定義的位址物件、將更新的資料填滿，並將其指派給 CustomerDetails 物件的位址屬性。 接著，CustomerDetails 物件會傳遞至 Web 服務進行處理。

**[清單 16]。使用嵌套的複雜類型**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample20.js)]

## <a name="creating-and-using-page-methods"></a>建立和使用頁面方法

Web 服務提供一種絕佳的方式，將可重複使用的服務公開給各種用戶端，包括 ASP.NET AJAX 頁面。 不過，在某些情況下，頁面可能需要捕獲其他頁面不會使用或共用的資料。 在此情況下，建立 .asmx 檔案以允許頁面存取資料看起來可能像是大材小用，因為服務僅供單一頁面使用。

ASP.NET AJAX 提供另一種機制來進行類似 Web 服務的呼叫，而不需要建立獨立的 .asmx 檔案。 這是藉由使用稱為「頁面方法」的技術來完成。 頁面方法是靜態 (共用在 VB.NET) 方法中，直接內嵌在頁面或程式碼除外的檔案中，該檔案會套用 WebMethod 屬性。 藉由套用 WebMethod 屬性，可以使用名為 PageMethods 的特殊 JavaScript 物件來呼叫它們，以在執行時間動態建立。 PageMethods 物件會作為 proxy，讓您免于 JSON 序列化/還原序列化程式。 請注意，為了使用 PageMethods 物件，您必須將 ScriptManager 的 EnablePageMethods 屬性設定為 true。

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample21.aspx)]

[清單 17] 顯示在 ASP.NET 程式碼旁邊的類別中定義兩個頁面方法的範例。 這些方法會從位於網站的應用程式 Code 資料夾中的商務層類別取得資料 \_ 。

**[清單 17]定義頁面方法。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample22.cs)]

當 ScriptManager 偵測到頁面中出現 Web 方法時，它會產生稍早所述 PageMethods 物件的動態參考。 呼叫 Web 方法的方式是參考 PageMethods 類別，後面接著方法的名稱以及應該傳遞的任何必要參數資料。 [清單 18] 顯示呼叫稍早所示之兩頁方法的範例。

**[清單 18]。使用 PageMethods JavaScript 物件呼叫頁面方法。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample23.js)]

使用 PageMethods 物件與使用 JavaScript proxy 物件非常類似。 您必須先指定應傳遞至頁面方法的所有參數資料，然後定義非同步呼叫傳回時應該呼叫的回呼函式。 也可以指定失敗回呼 (如需處理失敗) 範例，請參閱 [清單 14]。

## <a name="the-autocompleteextender-and-the-aspnet-ajax-toolkit"></a>AutoCompleteExtender 和 ASP.NET AJAX 工具組

從) 提供的 ASP.NET AJAX 工具組 ([http://ajax.asp.net](http://ajax.asp.net) 提供數個可用於存取 Web 服務的控制項。 具體而言，此工具組包含名為的實用控制項， `AutoCompleteExtender` 可用來呼叫 Web 服務並在頁面中顯示資料，而不需要撰寫任何 JavaScript 程式碼。

AutoCompleteExtender 控制項可用來擴充 textbox 的現有功能，並協助使用者更輕鬆地找出所需的資料。 當他們輸入文字方塊時，可以使用控制項來查詢 Web 服務，並以動態方式在文字方塊下方顯示結果。 [圖 4] 顯示使用 AutoCompleteExtender 控制項來顯示支援應用程式之客戶識別碼的範例。 當使用者在文字方塊中輸入不同的字元時，會根據其輸入在其底下顯示不同的專案。 然後，使用者可以選取所需的客戶識別碼。

在 ASP.NET AJAX 頁面中使用 AutoCompleteExtender，需要將 AjaxControlToolkit.dll 元件新增至網站的 bin 資料夾。 新增工具組元件之後，您會想要在 web.config 中加以參考，讓應用程式中的所有頁面都可以使用它所包含的控制項。 這可以藉由在 web.config 的 controls 標記內新增下列標記來完成 &lt; &gt; ：

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample24.xml)]

在您只需要在特定頁面中使用控制項的情況下，您可以將 Reference 指示詞加入至頁面的頂端，而不是更新 web.config 來參考它：

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample25.aspx)]

[![使用 AutoCompleteExtender 控制項。](understanding-asp-net-ajax-web-services/_static/image11.png)](understanding-asp-net-ajax-web-services/_static/image10.png)

**圖 4**：使用 AutoCompleteExtender 控制項。   ([按一下以查看完整大小的影像](understanding-asp-net-ajax-web-services/_static/image12.png)) 

一旦網站已設定為使用 ASP.NET AJAX 工具組，就可以將 AutoCompleteExtender 控制項加入頁面中，就像加入一般的 ASP.NET 伺服器控制項一樣。 [清單 19] 顯示使用控制項呼叫 Web 服務的範例。

**[清單 19]。使用 ASP.NET AJAX 工具組 AutoCompleteExtender 控制項。**

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample26.aspx)]

AutoCompleteExtender 有數個不同的屬性，包括在伺服器控制項上找到的標準識別碼和 runat 屬性。 除了這些以外，它還可讓您定義使用者在 Web 服務查詢資料之前輸入的字元數。 [清單 19] 中所顯示的 MinimumPrefixLength 屬性會導致每次在文字方塊中輸入一個字元時呼叫服務。 您會想要小心設定此值，因為每次使用者輸入一個字元時，就會呼叫 Web 服務來搜尋符合文字方塊中字元的值。 要呼叫的 Web 服務以及目標 Web 方法，分別使用 ServicePath 和 ServiceMethod 屬性來定義。 最後，TargetControlID 屬性會識別要將 AutoCompleteExtender 控制項連結至哪一個文字方塊。

所呼叫的 Web 服務必須先套用 ScriptService 屬性，如前文所述，而目標 Web 方法必須接受兩個名為 prefixText 和 count 的參數。 PrefixText 參數代表使用者輸入的字元，而 count 參數代表要傳回的專案數 (預設值為 10) 。 [清單 20] 顯示 GetCustomerIDs Web 方法的範例，其由前面的 [清單 19] 所示的 AutoCompleteExtender 控制項所呼叫。 Web 方法會呼叫商務層方法，然後再呼叫資料層方法來處理篩選資料並傳回相符的結果。 資料層方法的程式碼如 [清單 21] 所示。

**清單20。篩選從 AutoCompleteExtender 控制項傳送的資料。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample27.cs)]

**[清單 21]。依據使用者輸入來篩選結果。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample28.cs)]

## <a name="conclusion"></a>結論

ASP.NET AJAX 提供呼叫 Web 服務的絕佳支援，而不需要撰寫許多自訂 JavaScript 程式碼來處理要求和回應訊息。 在本文中，您已瞭解如何使用 AJAX 啟用 .NET Web 服務，使其能夠處理 JSON 訊息，以及如何使用 ScriptManager 控制項定義 JavaScript proxy。 您也已瞭解如何使用 JavaScript proxy 來呼叫 Web 服務、處理簡單和複雜的類型，以及處理失敗。 最後，您已瞭解如何使用頁面方法來簡化建立和進行 Web 服務呼叫的程式，以及 AutoCompleteExtender 控制項如何在使用者輸入時提供協助。 雖然 ASP.NET AJAX 中提供的 UpdatePanel 當然可以控制許多 AJAX 程式設計人員的選擇，因為它的簡易性，知道如何透過 JavaScript proxy 呼叫 Web 服務，對於許多應用程式都很有用。

## <a name="bio"></a>生物

Dan Wahlin (Microsoft 最有價值的 ASP.NET 和 XML Web Service 專業人員) 是 .NET 開發講師和架構顧問，位於介面技術訓練 ([http://www.interfacett.com](http://www.interfacett.com)) 。 Dan 成立了 XML for ASP.NET 開發人員網站 ([www.XMLforASP.NET](http://www.XMLforASP.NET)) ，這是 INETA 講師的部門，並在幾場會議中發表。 Dan 共同撰寫的專業 Windows DNA (Wrox) 、ASP.NET：秘訣、教學課程和程式碼 (Sam) 、ASP.NET 1.1 Insider 解決方案、Professional ASP.NET 2.0 AJAX (Wrox) 、ASP.NET 2.0 MVP 的攻擊，以及為 ASP.NET 開發人員撰寫的 XML (Sams) 。 當他不寫程式碼、文章或書籍時，Dan 就能在他的妻子和小孩中撰寫和錄製音樂，以及玩高爾夫球和籃球。

Scott Cate 自1997起開始使用 Microsoft Web 技術，而且是 myKB.com ([www.myKB.com](http://www.myKB.com)) 的總裁，他專門用來撰寫著重于知識庫軟體解決方案的 ASP.NET 型應用程式。 Scott 可以透過電子郵件聯絡， [scott.cate@myKB.com](mailto:scott.cate@myKB.com) 或他在[ScottCate.com](http://ScottCate.com)的 blog

> [!div class="step-by-step"]
> [上一個](understanding-asp-net-ajax-localization.md) 
> [下一步](understanding-asp-net-ajax-debugging-capabilities.md)
