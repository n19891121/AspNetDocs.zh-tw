---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
title: 瞭解 ASP.NET AJAX Web 服務 |Microsoft Docs
author: scottcate
description: Web 服務是 .NET framework 不可或缺的一部分，可提供跨平臺的解決方案，以便在分散式系統之間交換資料。 雖然 Web .。。
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 3332d6e7-e2e1-4144-b805-e71d51e7e415
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-web-services
msc.type: authoredcontent
ms.openlocfilehash: eac3d53fd871d0cb5a2870488ce752c057cc5b1a
ms.sourcegitcommit: 45754124123403520b9fa2e706a4d1292494159b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/12/2020
ms.locfileid: "86162762"
---
# <a name="understanding-aspnet-ajax-web-services"></a>了解 ASP.NET AJAX Web 服務

[Scott Cate](https://github.com/scottcate)

[下載 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial05_Web_Services_with_MS_Ajax_cs.pdf)

> Web 服務是 .NET framework 不可或缺的一部分，可提供跨平臺的解決方案，以便在分散式系統之間交換資料。 雖然 Web 服務通常是用來允許不同的作業系統、物件模型和程式設計語言來傳送和接收資料，但它們也可以用來以動態方式將資料插入 ASP.NET AJAX 頁面，或將資料從頁面傳送至後端系統。 這一切都可以在不需要回傳作業的情況下完成。

## <a name="calling-web-services-with-aspnet-ajax"></a>使用 ASP.NET AJAX 呼叫 Web 服務

Dan Wahlin

Web 服務是 .NET framework 不可或缺的一部分，可提供跨平臺的解決方案，以便在分散式系統之間交換資料。 雖然 Web 服務通常是用來允許不同的作業系統、物件模型和程式設計語言來傳送和接收資料，但它們也可以用來以動態方式將資料插入 ASP.NET AJAX 頁面，或將資料從頁面傳送至後端系統。 這一切都可以在不需要回傳作業的情況下完成。

雖然 ASP.NET AJAX UpdatePanel 控制項提供簡單的方法來讓 AJAX 啟用任何 ASP.NET 網頁，但有時候您可能需要以動態方式存取伺服器上的資料，而不需要使用 UpdatePanel。 在本文中，您將瞭解如何藉由在 ASP.NET AJAX 頁面內建立和使用 Web 服務來完成這項工作。

本文將著重于 core ASP.NET AJAX Extensions 中提供的功能，以及 ASP.NET AJAX 工具組中稱為 AutoCompleteExtender 的 Web 服務啟用的控制項。 涵蓋的主題包括定義具備 AJAX 功能的 Web 服務、建立用戶端 proxy，以及使用 JavaScript 呼叫 Web 服務。 您也將瞭解如何直接對 ASP.NET 網頁方法進行 Web 服務呼叫。

## <a name="web-services-configuration"></a>Web 服務設定

使用 Visual Studio 2008 建立新的網站專案時，web.config 檔有一些新的新增專案，可能不熟悉舊版 Visual Studio 的使用者。 其中某些修改會將 "asp" 前置詞對應至 ASP.NET AJAX 控制項，讓它們可以在頁面中使用，而有些則會定義必要的 HttpHandlers 和 HttpModules。 [清單 1] 顯示對 `<httpHandlers>` web.config 中影響 Web 服務呼叫之元素所做的修改。 用來處理 .asmx 呼叫的預設 HttpHandler 會被移除，並取代為位於 System.Web.Extensions.dll 元件中的 ScriptHandlerFactory 類別。 System.Web.Extensions.dll 包含 ASP.NET AJAX 所使用的所有核心功能。

**[清單 1]。ASP.NET AJAX Web 服務處理常式設定**

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample1.xml)]

這項 HttpHandler 取代的目的是為了讓您可以使用 JavaScript Web 服務 proxy，從 ASP.NET AJAX 頁面 AJAX 頁面，到 .NET Web 服務進行 JavaScript 物件標記法的)  (。 ASP.NET AJAX 會將 JSON 訊息傳送至 Web 服務，而非標準的簡單物件存取通訊協定， (通常與 Web 服務相關聯的 SOAP) 呼叫。 這會導致整體的要求和回應訊息更小。 它也可讓用戶端更有效率地處理資料，因為 ASP.NET AJAX JavaScript 程式庫已經過優化，可以使用 JSON 物件。 [清單 2] 和 [清單 3] 顯示序列化為 JSON 格式的 Web 服務要求和回應訊息範例。 [清單 2] 所示的要求訊息會傳遞值為 "比利時" 的國家/地區參數，而 [清單 3] 中的回應訊息則會傳遞客戶物件的陣列與其相關聯的屬性。

**[清單 2]。Web 服務要求訊息已序列化為 JSON**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample2.json)]

> *>作業 [!NOTE] 名稱定義為 web 服務 URL 的一部分; 此外，要求訊息不一定會透過 JSON 提交。Web 服務可以使用 ScriptMethod 屬性，並將 UseHttpGet 參數設為 true，這會導致透過查詢字串參數傳遞參數。*

**[清單 3]。Web 服務回應訊息已序列化為 JSON**

[!code-json[Main](understanding-asp-net-ajax-web-services/samples/sample3.json)]

在下一節中，您將瞭解如何建立可處理 JSON 要求訊息，以及同時回應簡單和複雜類型的 Web 服務。

## <a name="creating-ajax-enabled-web-services"></a>建立啟用 AJAX 的 Web 服務

ASP.NET AJAX framework 提供數種不同的方式來呼叫 Web 服務。 您可以使用 ASP.NET AJAX 工具組) 或 JavaScript 中提供的 AutoCompleteExtender 控制項 (。 不過，在呼叫服務之前，您必須啟用 AJAX，才能由用戶端腳本程式碼呼叫。

無論您是 ASP.NET Web 服務的新手，您都可以直接建立和啟用 AJAX 的服務。 .NET framework 已支援在2002的初始版本之後建立 ASP.NET Web 服務，而 ASP.NET AJAX Extensions 提供以 .NET framework 的預設功能集為基礎的其他 AJAX 功能。 Visual Studio .NET 2008 Beta 2 有內建的支援，可讓您建立 .asmx Web 服務檔案，並自動從 system.servicemodel 類別的類別旁衍生相關聯的程式碼。 當您將方法加入至類別時，您必須套用 WebMethod 屬性，才能由 Web 服務取用者呼叫它們。

[清單 4] 顯示將 WebMethod 屬性套用至名為 GetCustomersByCountry ( # A1 的方法的範例。

**[清單 4]。在 Web 服務中使用 WebMethod 屬性**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample4.cs)]

GetCustomersByCountry ( # A1 方法會接受 country 參數，並傳回客戶物件陣列。 傳入方法的國家/地區值會轉送至商務層級類別，然後再呼叫資料層類別以從資料庫取出資料、以資料填滿客戶物件屬性，並傳回陣列。

## <a name="using-the-scriptservice-attribute"></a>使用 ScriptService 屬性

雖然新增 WebMethod 屬性可讓用戶端呼叫 GetCustomersByCountry ( # A1 方法，而用戶端會將標準的 SOAP 訊息傳送至 Web 服務，但不允許從現成的 ASP.NET AJAX 應用程式進行 JSON 呼叫。 若要允許進行 JSON 呼叫，您必須將 ASP.NET AJAX 延伸模組的 `ScriptService` 屬性套用至 Web 服務類別。 這可讓 Web 服務傳送使用 JSON 格式化的回應訊息，並允許用戶端腳本藉由傳送 JSON 訊息來呼叫服務。

[清單 5] 顯示將 ScriptService 屬性套用至名為 CustomersService 的 Web 服務類別的範例。

**[清單 5]。使用 ScriptService 屬性啟用 AJAX 的 Web 服務**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample5.cs)]

ScriptService 屬性可作為標記，表示可以從 AJAX 腳本呼叫它。 它實際上不會處理在幕後發生的任何 JSON 序列化或還原序列化工作。 在 web.config) 和其他相關類別中設定的 ScriptHandlerFactory (會進行大量的 JSON 處理。

## <a name="using-the-scriptmethod-attribute"></a>使用 ScriptMethod 屬性

ScriptService 屬性是唯一必須在 .NET Web 服務中定義的 ASP.NET AJAX 屬性，以便 ASP.NET AJAX 頁面使用。 但是，另一個名為 ScriptMethod 的屬性也可以直接套用至服務中的 Web 方法。 ScriptMethod 會定義三個屬性 `UseHttpGet` ，包括、 `ResponseFormat` 和 `XmlSerializeString` 。 當 web 方法需要以或物件的形式傳回未經處理的 XML 資料， `XmlDocument` `XmlElement` 或是從服務傳回的資料應該一律序列化為 XML 而不是 JSON 時，變更這些屬性的值可能會很有用，因為這種情況下，web 方法所接受的要求類型需要變更為 GET。

當 Web 方法應該接受 GET 要求而非 POST 要求時，就可以使用 UseHttpGet 屬性。 要求是使用已轉換成 QueryString 參數之 Web 方法輸入參數的 URL 來傳送。 UseHttpGet 屬性預設為 false，而且只有 `true` 在已知為安全的作業，以及敏感性資料未傳遞至 Web 服務時，才會設定為。 [清單 6] 顯示搭配 UseHttpGet 屬性使用 ScriptMethod 屬性的範例。

**[清單 6]。搭配 UseHttpGet 屬性使用 ScriptMethod 屬性。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample6.cs)]

在 [清單 6] 中所示的 HttpGetEcho Web 方法被呼叫時，所傳送的標頭範例如下所示：

`GET /CustomerViewer/DemoService.asmx/HttpGetEcho?input=%22Input Value%22 HTTP/1.1`

除了允許 Web 方法接受 HTTP GET 要求之外，當 XML 回應需要從服務而非 JSON 傳回時，也可以使用 ScriptMethod 屬性。 例如，Web 服務可能會從遠端網站抓取 RSS 摘要，並將其傳回為您的已處理或 XmlElement 物件。 然後可以在用戶端上進行 XML 資料的處理。

[清單 7] 顯示使用 ResponseFormat 屬性來指定應該從 Web 方法傳回 XML 資料的範例。

**[清單 7]。搭配 ResponseFormat 屬性使用 ScriptMethod 屬性。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample7.cs)]

ResponseFormat 屬性也可以搭配 XmlSerializeString 屬性使用。 XmlSerializeString 屬性的預設值為 false，這表示當屬性設定為時，除了從 Web 方法傳回的字串以外的所有傳回型別都會序列化為 XML `ResponseFormat` `ResponseFormat.Xml` 。 當 `XmlSerializeString` 設定為時 `true` ，從 Web 方法傳回的所有型別都會序列化為 XML，包括字串類型。 如果 ResponseFormat 屬性的值為，則 `ResponseFormat.Json` 會忽略 XmlSerializeString 屬性的值。

[清單 8] 顯示使用 XmlSerializeString 屬性來強制將字串序列化為 XML 的範例。

**[清單 8]。搭配 XmlSerializeString 屬性使用 ScriptMethod 屬性**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample8.cs)]

在 [清單 8] 中呼叫 GetXmlString Web 方法所傳回的值如下所示：

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample9.cs)]

雖然預設的 JSON 格式可將要求和回應訊息的整體大小降至最低，而且 ASP.NET AJAX 用戶端會更容易取用跨瀏覽器的方式，但是當用戶端應用程式（例如 Internet Explorer 5 或更高版本）預期從 Web 方法傳回 XML 資料時，就可以使用 ResponseFormat 和 XmlSerializeString 屬性。

## <a name="working-with-complex-types"></a>使用複雜類型

[清單 5] 顯示從 Web 服務傳回名為 Customer 的複雜型別範例。 Customer 類別會在內部定義數種不同的簡單類型，作為 FirstName 和 LastName 等屬性。 在啟用 AJAX 的 Web 方法上做為輸入參數或傳回類型的複雜類型，會在傳送至用戶端之前自動序列化為 JSON。 不過， (的嵌套複雜) 型別，則預設不會提供給用戶端做為獨立物件。

如果 Web 服務使用的嵌套複雜型別也必須在用戶端頁面中使用，則可以將 ASP.NET AJAX GenerateScriptType 屬性加入至 Web 服務。 例如，[清單 9] 所示的 CustomerDetails 類別包含***表示嵌套複雜***型別的位址和性別屬性。

**[清單 9]。此處所示的 CustomerDetails 類別包含兩個嵌套的複雜類型。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample10.cs)]

在 [清單 9] 所示的 CustomerDetails 類別中定義的位址和性別物件不會透過 JavaScript 自動提供給用戶端使用，因為它們是巢狀型別， (位址是類別，而性別是列舉) 。 在 Web 服務中使用的嵌套型別必須可在用戶端上使用的情況下，可以使用稍早提及的 GenerateScriptType 屬性 (參閱清單 10) 。 當服務傳回不同的嵌套複雜型別時，可以多次新增此屬性。 它可以直接套用至 Web 服務類別或更高的特定 Web 方法。

**清單10。使用 GenerateScriptService 屬性來定義可供用戶端使用的巢狀型別。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample11.cs)]

藉由將 `GenerateScriptType` 屬性套用至 Web 服務，就會自動將位址和性別類型提供給用戶端 ASP.NET AJAX JavaScript 程式碼使用。 在 Web 服務上新增 GenerateScriptType 屬性，自動產生並傳送至用戶端的 JavaScript 範例如 [清單 11] 所示。 您將在稍後的文章中瞭解如何使用嵌套複雜類型。

**[清單 11]。ASP.NET AJAX 頁面提供的嵌套複雜類型。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample12.cs)]

現在您已瞭解如何建立 Web 服務，並使其可供 ASP.NET AJAX 頁面，讓我們看看如何建立和使用 JavaScript proxy，以便將資料取出或傳送至 Web 服務。

## <a name="creating-javascript-proxies"></a>建立 JavaScript proxy

呼叫標準 Web 服務 ( .NET 或另一個平臺) 通常需要建立 proxy 物件，讓您免于傳送 SOAP 要求和回應訊息的複雜度。 使用 ASP.NET AJAX Web 服務呼叫，可以建立並使用 JavaScript proxy 來輕鬆地呼叫服務，而不必擔心序列化和還原序列化 JSON 訊息。 您可以使用 ASP.NET AJAX ScriptManager 控制項自動產生 JavaScript proxy。

您可以使用 ScriptManager 的 [服務] 屬性來建立可呼叫 Web 服務的 JavaScript proxy。 這個屬性可讓您定義一個或多個服務，讓 ASP.NET AJAX 頁面可以非同步方式呼叫以傳送或接收資料，而不需要回傳作業。 您可以使用 ASP.NET AJAX 控制項來定義服務 `ServiceReference` ，並將 Web 服務 URL 指派給控制項的 `Path` 屬性。 [清單 12] 顯示參考名為 CustomersService 的服務範例。

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample13.aspx)]

**清單12。定義在 ASP.NET AJAX 頁面中使用的 Web 服務。**

透過 ScriptManager 控制項加入 CustomersService 的參考，會使 JavaScript proxy 動態產生並由頁面參考。 您可以使用腳本標記來內嵌 &lt; proxy &gt; ，並透過呼叫 CustomersService .asmx 檔案並將/js 附加至結尾，以動態方式載入 proxy。 下列範例顯示在 web.config 中停用偵錯工具時，如何將 JavaScript proxy 內嵌在頁面中：

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample14.html)]

> *>[!NOTE]如果您想要查看產生的實際 JavaScript proxy 程式碼，您可以將所需的 .Net Web 服務 URL 輸入 Internet Explorer 的位址方塊中，並將/js 附加到其結尾。*

如果在 web.config 中啟用了偵錯工具，則會將 JavaScript proxy 的 debug 版本內嵌在頁面中，如下所示：

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample15.html)]

ScriptManager 所建立的 JavaScript proxy 也可以直接內嵌到網頁中，而不是使用 &lt; 腳本 &gt; 標記的 src 屬性參考。 這可以藉由將 ServiceReference 控制項的 InlineScript 屬性設定為 true 來完成， (預設值為 false) 。 當 proxy 未在多個頁面之間共用，而且您想要減少對伺服器所做的網路呼叫時，這會很有用。 當 InlineScript 設定為 true 時，瀏覽器不會快取 proxy 腳本，因此在 ASP.NET AJAX 應用程式中的多個頁面使用 proxy 時，建議使用預設值 false。 以下顯示使用 InlineScript 屬性的範例：

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample16.aspx)]

## <a name="using-javascript-proxies"></a>使用 JavaScript proxy

一旦使用 ScriptManager 控制項 ASP.NET AJAX 頁面參考 Web 服務之後，就可以對 Web 服務進行呼叫，而且可以使用回呼函式來處理傳回的資料。 藉由參考其命名空間 (（如果有) 、類別名稱和 Web 方法名稱）來呼叫 Web 服務。 可以定義任何傳遞至 Web 服務的參數，以及處理傳回資料的回呼函式。

清單13中顯示使用 JavaScript proxy 呼叫名為 GetCustomersByCountry 之 Web 方法 ( # A1 的範例。 當終端使用者按一下頁面上的按鈕時，會呼叫 GetCustomersByCountry ( # A1 函式。

**[清單 13]。使用 JavaScript proxy 呼叫 Web 服務。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample17.js)]

此呼叫會參考服務中定義的 InterfaceTraining 命名空間、CustomersService 類別和 GetCustomersByCountry Web 方法。 它會傳遞從 textbox 取得的國家/地區值，以及一個名為 OnWSRequestComplete 的回呼函式，當非同步 Web 服務呼叫傳回時，應叫用此函式。 OnWSRequestComplete 會處理從服務傳回的客戶物件陣列，並將其轉換成頁面中顯示的資料表。 [圖 1] 顯示從呼叫產生的輸出。

[![藉由對 Web 服務進行非同步 AJAX 呼叫來系結所取得的資料。](understanding-asp-net-ajax-web-services/_static/image2.png)](understanding-asp-net-ajax-web-services/_static/image1.png)

**圖 1**：對 Web 服務進行非同步 AJAX 呼叫所取得的系結資料。   ([按一下以查看完整大小的影像](understanding-asp-net-ajax-web-services/_static/image3.png)) 

如果應該呼叫 Web 方法，但是 proxy 不應等候回應，則 JavaScript proxy 也可以對 Web 服務進行單向呼叫。 例如，您可能想要呼叫 Web 服務來啟動處理常式（例如工作流程），但不等候服務的傳回值。 如果需要對服務進行單向呼叫，則可以直接省略 [清單 13] 所示的回呼函數。 由於未定義回呼函式，因此 proxy 物件不會等候 Web 服務傳回資料。

## <a name="handling-errors"></a>處理錯誤

Web 服務的非同步回呼可能會遇到不同類型的錯誤，例如網路已關閉、Web 服務無法使用或傳回例外狀況。 幸運的是，ScriptManager 所產生的 JavaScript proxy 物件允許定義多個回呼，以處理之前顯示的成功回呼以外的錯誤和失敗。 在呼叫 Web 方法的標準回呼函式之後，可以立即定義錯誤回呼函式，如 [清單 14] 所示。

**清單14。定義錯誤回呼函式並顯示錯誤。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample18.js)]

呼叫 Web 服務時所發生的任何錯誤都會觸發 OnWSRequestFailed ( # A1 回呼函式，以接受以參數表示錯誤的物件。 Error 物件會公開數個不同的函式，以判斷錯誤的原因，以及呼叫是否超時。[清單 14] 顯示使用不同錯誤函式的範例，而 [圖 2] 顯示函數所產生的輸出範例。

[![藉由呼叫 ASP.NET AJAX 錯誤函式所產生的輸出。](understanding-asp-net-ajax-web-services/_static/image5.png)](understanding-asp-net-ajax-web-services/_static/image4.png)

**圖 2**：透過呼叫 ASP.NET AJAX 錯誤函式所產生的輸出。   ([按一下以查看完整大小的影像](understanding-asp-net-ajax-web-services/_static/image6.png)) 

## <a name="handling-xml-data-returned-from-a-web-service"></a>處理從 Web 服務傳回的 XML 資料

稍早，您已瞭解 Web 方法如何使用 ScriptMethod 屬性以及其 ResponseFormat 屬性來傳回原始 XML 資料。 當 ResponseFormat 設定為 ResponseFormat.Xml 時，從 Web 服務傳回的資料會序列化為 XML，而不是 JSON。 當 XML 資料必須直接傳遞至用戶端以使用 JavaScript 或 XSLT 進行處理時，這會很有用。 目前，Internet Explorer 5 或更高版本提供最佳的用戶端物件模型，可用於剖析和篩選 XML 資料，因為其內建的 MSXML 支援。

從 Web 服務抓取 XML 資料與抓取其他資料類型並無不同。 首先叫用 JavaScript proxy 來呼叫適當的函式，並定義回呼函數。 一旦呼叫傳回之後，您就可以處理回呼函數中的資料。

[清單 15] 顯示一個範例，說明如何呼叫名為 GetRssFeed ( # A1 的 Web 方法，以傳回 XmlElement 物件。 GetRssFeed ( # A1 接受單一參數，代表要取出的 RSS 摘要 URL。

**[清單 15]。使用從 Web 服務傳回的 XML 資料。**

[!code-html[Main](understanding-asp-net-ajax-web-services/samples/sample19.html)]

此範例會將 URL 傳遞至 RSS 摘要，並在 OnWSRequestComplete ( # A1 函式中處理傳回的 XML 資料。 OnWSRequestComplete ( # A1 會先檢查瀏覽器是否 Internet Explorer，以瞭解是否有 MSXML 剖析器可供使用。 如果是，則會使用 XPath 語句來找 &lt; &gt; 出 rss 摘要內的所有專案標記。 然後會逐一查看每個專案，並且 &lt; 會尋找並處理相關聯的標題 &gt; 和 &lt; 連結 &gt; 標記，以顯示每個專案的資料。 [圖 3] 顯示透過 JavaScript proxy 對 GetRssFeed ( # A1 Web 方法進行 ASP.NET AJAX 呼叫所產生的輸出範例。

## <a name="handling-complex-types"></a>處理複雜類型

Web 服務接受或傳回的複雜類型會透過 JavaScript proxy 自動公開。 不過，除非已將 GenerateScriptType 屬性套用至先前所討論的服務，否則無法在用戶端上直接存取嵌套的複雜類型。 為什麼您想要在用戶端上使用嵌套複雜型別？

若要回答這個問題，請假設 ASP.NET AJAX 頁面顯示客戶資料，並允許終端使用者更新客戶的位址。 如果 Web 服務指定的網址類別型 (在 CustomerDetails 類別內定義的複雜型別) 可以傳送給用戶端，則更新程式可以分成不同的函式，以便更妥善地重複使用程式碼。

[![從呼叫傳回 RSS 資料的 Web 服務所產生的輸出。](understanding-asp-net-ajax-web-services/_static/image8.png)](understanding-asp-net-ajax-web-services/_static/image7.png)

**圖 3**：從呼叫傳回 RSS 資料的 Web 服務來建立輸出。   ([按一下以查看完整大小的影像](understanding-asp-net-ajax-web-services/_static/image9.png)) 

[清單 16] 顯示用戶端程式代碼的範例，該程式碼會叫用模型命名空間中定義的位址物件、將更新的資料填入其中，然後將它指派給 CustomerDetails 物件的 Address 屬性。 然後，CustomerDetails 物件會傳遞至 Web 服務進行處理。

**清單16：使用嵌套複雜類型**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample20.js)]

## <a name="creating-and-using-page-methods"></a>建立和使用頁面方法

Web 服務提供了一種絕佳的方式，可將重複使用的服務公開給各種用戶端，包括 ASP.NET AJAX 頁面。 不過，在某些情況下，頁面可能需要取出其他頁面不會使用或共用的資料。 在此情況下，建立 .asmx 檔案以允許頁面存取資料可能看起來像麻煩，因為服務只會由單一頁面使用。

ASP.NET AJAX 提供另一種機制來進行類似 Web 服務的呼叫，而不需建立獨立的 .asmx 檔案。 這是使用稱為「頁面方法」的技術來完成。 頁面方法是靜態 (共用在內嵌于頁面的 VB.NET) 方法中，或是已套用 WebMethod 屬性的程式碼旁的檔案中。 藉由套用 WebMethod 屬性，您可以使用名為 PageMethods 的特殊 JavaScript 物件（其會在執行時間動態建立）來呼叫。 PageMethods 物件會作為 proxy，讓您免于 JSON 序列化/還原序列化程式。 請注意，為了使用 PageMethods 物件，您必須將 ScriptManager 的 EnablePageMethods 屬性設定為 true。

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample21.aspx)]

清單17顯示在 ASP.NET 程式碼旁類別中定義兩個頁面方法的範例。 這些方法會從網站的 [應用程式程式碼] 資料夾中的商務層類別取得資料 \_ 。

**清單17。定義頁面方法。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample22.cs)]

當 ScriptManager 在頁面上偵測到 Web 方法存在時，會產生稍早所述之 PageMethods 物件的動態參考。 藉由參考 PageMethods 類別，並在後面加上方法名稱和任何應傳遞的必要參數資料，即可完成呼叫 Web 方法。 [清單 18] 顯示呼叫稍早所示之兩個頁面方法的範例。

**清單18。使用 PageMethods JavaScript 物件呼叫頁面方法。**

[!code-javascript[Main](understanding-asp-net-ajax-web-services/samples/sample23.js)]

使用 PageMethods 物件與使用 JavaScript proxy 物件非常類似。 您會先指定應傳遞至頁面方法的所有參數資料，然後定義非同步呼叫傳回時應呼叫的回呼函數。 也可以指定失敗回呼 (請參閱 [清單 14]，以取得處理失敗的範例) 。

## <a name="the-autocompleteextender-and-the-aspnet-ajax-toolkit"></a>AutoCompleteExtender 和 ASP.NET AJAX 工具組

) 提供的 ASP.NET AJAX 工具組 ([http://ajax.asp.net](http://ajax.asp.net) 提供數個可用於存取 Web 服務的控制項。 具體來說，此工具組包含一個名為的實用控制項 `AutoCompleteExtender` ，可用來呼叫 Web 服務並在頁面中顯示資料，而不需要撰寫任何 JavaScript 程式碼。

AutoCompleteExtender 控制項可用來擴充文字方塊的現有功能，並協助使用者更輕鬆地找到他們所要尋找的資料。 當使用者在文字方塊中輸入時，控制項可以用來查詢 Web 服務，並以動態方式在文字方塊下方顯示結果。 [圖 4] 顯示使用 AutoCompleteExtender 控制項來顯示支援應用程式之客戶識別碼的範例。 當使用者在文字方塊中輸入不同的字元時，不同的專案會根據其輸入顯示在下方。 然後，使用者可以選取所需的客戶識別碼。

在 ASP.NET AJAX 頁面內使用 AutoCompleteExtender 需要將 AjaxControlToolkit.dll 元件新增至網站的 bin 資料夾。 加入工具組元件之後，您會想要在 web.config 中參考它，讓應用程式中的所有頁面都可以使用它所包含的控制項。 這可以藉由在 web.config 的 controls 標記內新增下列標記來完成 &lt; &gt; ：

[!code-xml[Main](understanding-asp-net-ajax-web-services/samples/sample24.xml)]

如果您只需要在特定頁面中使用控制項，則可以藉由在頁面的頂端加入參考指示詞來參考它，如下所示，而不是更新 web.config：

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample25.aspx)]

[![使用 AutoCompleteExtender 控制項。](understanding-asp-net-ajax-web-services/_static/image11.png)](understanding-asp-net-ajax-web-services/_static/image10.png)

**圖 4**：使用 AutoCompleteExtender 控制項。   ([按一下以查看完整大小的影像](understanding-asp-net-ajax-web-services/_static/image12.png)) 

一旦將網站設定為使用 ASP.NET AJAX 工具組之後，就可以將 AutoCompleteExtender 控制項新增至頁面，就像新增一般 ASP.NET 伺服器控制項一樣。 清單19顯示使用控制項來呼叫 Web 服務的範例。

**清單19。使用 ASP.NET AJAX 工具組 AutoCompleteExtender 控制項。**

[!code-aspx[Main](understanding-asp-net-ajax-web-services/samples/sample26.aspx)]

AutoCompleteExtender 有數個不同的屬性，包括在伺服器控制項上找到的標準識別碼和 runat 屬性。 此外，它還可讓您定義在 Web 服務查詢資料之前，終端使用者所輸入的字元數。 在 [清單 19] 中顯示的 [MinimumPrefixLength] 屬性，會在每次將字元輸入 textbox 時呼叫服務。 您會想要小心設定這個值，因為每次使用者輸入一個字元時，就會呼叫 Web 服務來搜尋符合文字方塊中字元的值。 要呼叫的 Web 服務以及目標 Web 方法，分別使用 ServicePath 和 ServiceMethod 屬性來定義。 最後，TargetControlID 屬性會識別要將 AutoCompleteExtender 控制項連結至哪一個文字方塊。

正在呼叫的 Web 服務必須套用 ScriptService 屬性，如先前所述，而且目標 Web 方法必須接受名為 prefixText 和 count 的兩個參數。 PrefixText 參數代表使用者輸入的字元，而 count 參數代表 (預設值為 10) 所要傳回的專案數目。 [清單 20] 顯示稍早在 [清單 19] 中所示之 AutoCompleteExtender 控制項所呼叫的 GetCustomerIDs Web 方法範例。 Web 方法會呼叫商務層方法，該方法接著會呼叫資料層方法來處理篩選資料並傳回相符的結果。 資料層方法的程式碼如 [清單 21] 所示。

**清單20。篩選從 AutoCompleteExtender 控制項傳送的資料。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample27.cs)]

**清單21。依據使用者輸入篩選結果。**

[!code-csharp[Main](understanding-asp-net-ajax-web-services/samples/sample28.cs)]

## <a name="conclusion"></a>結論

ASP.NET AJAX 為呼叫 Web 服務提供絕佳的支援，而不需要撰寫大量的自訂 JavaScript 程式碼來處理要求和回應訊息。 在本文中，您已瞭解如何啟用 AJAX 的 .NET Web 服務，使其能夠處理 JSON 訊息，以及如何使用 ScriptManager 控制項定義 JavaScript proxy。 您也已瞭解如何使用 JavaScript proxy 來呼叫 Web 服務、處理簡單和複雜類型，以及處理失敗。 最後，您已瞭解如何使用頁面方法來簡化建立和進行 Web 服務呼叫的程式，以及 AutoCompleteExtender 控制項如何在使用者輸入時提供協助給終端使用者。 雖然 ASP.NET AJAX 中提供的 UpdatePanel 當然是許多 AJAX 程式設計人員的選擇，但由於其簡易性，瞭解如何透過 JavaScript proxy 呼叫 Web 服務對許多應用程式都很有用。

## <a name="bio"></a>簡歷

Dan Wahlin (Microsoft 最有價值的 ASP.NET 和 XML Web 服務專業人員) 是 .NET 開發講師和架構顧問，在介面技術訓練 ([http://www.interfacett.com](http://www.interfacett.com)) 。 Dan 成立了 XML for ASP.NET 開發人員網站 ([www.XMLforASP.NET](http://www.XMLforASP.NET)) ，是在 INETA 講師的部門，並在幾場研討會發表演講。 Dan 共同撰寫的專業 Windows DNA (Wrox) 、ASP.NET：秘訣、教學課程和程式碼 (Sams) 、ASP.NET 1.1 Insider 解決方案、Professional ASP.NET 2.0 AJAX (Wrox) 、ASP.NET 2.0 MVP 駭客和針對 ASP.NET 開發人員撰寫的 XML (Sams) 。 當他未撰寫程式碼、文章或書籍時，Dan 會喜歡撰寫和錄製音樂，以及透過他的妻子和小孩播放高爾夫球和籃球。

Scott Cate 從1997開始一直在使用 Microsoft Web 技術，而且是 myKB.com ([www.myKB.com](http://www.myKB.com)) 的總裁，他專門撰寫以知識庫軟體解決方案為基礎的 ASP.NET 型應用程式。 Scott 可透過電子郵件聯絡， [scott.cate@myKB.com](mailto:scott.cate@myKB.com) 或他的 blog，網址為 [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [上一個](understanding-asp-net-ajax-localization.md) 
> [下一步](understanding-asp-net-ajax-debugging-capabilities.md)
