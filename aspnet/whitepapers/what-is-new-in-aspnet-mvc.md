---
uid: whitepapers/what-is-new-in-aspnet-mvc
title: ASP.NET MVC 2 的新功能 |Microsoft Docs
author: rick-anderson
description: 本檔說明 ASP.NET MVC 2 中引進的新功能和增強功能。 這份檔也可供下載。
ms.author: riande
ms.date: 04/20/2010
ms.assetid: 69a8d6f8-4b10-4602-8822-2d6c05fc432b
msc.legacyurl: /whitepapers/what-is-new-in-aspnet-mvc
msc.type: content
ms.openlocfilehash: ecc840c33714aa04bebcd9e413cb548eca8cc058
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045035"
---
# <a name="whats-new-in-aspnet-mvc-2"></a>ASP.NET MVC 2 的新功能

> 本檔說明 ASP.NET MVC 2 中引進的新功能和增強功能。 這份檔也可供 [下載](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/WhatIsNewInMVC_2.pdf)

[介紹](#_TOC1)   
[將 ASP.NET MVC 1.0 專案升級為 ASP.NET MVC 2](#_TOC2)   
[新功能](#_TOC3)   
[樣板化協助程式](#_TOC3_1)   
[地區](#_TOC3_2)   
[支援非同步控制器](#_TOC3_3)   
[在動作方法參數中支援 DefaultValueAttribute](#_TOC3_4)   
[支援使用模型系結器來系結二進位資料](#_TOC3_5)   
[ModelMetadata 和 ModelMetadataProvider 類別](#_TOC3_6)   
[DataAnnotations 屬性的支援](#_TOC3_7)   
[模型驗證程式提供者](#_TOC3_8)   
[用戶端驗證](#_TOC3_9)   
[Visual Studio 2010 的新程式碼片段](#_TOC3_10)   
[新增 RequireHttpsAttribute 動作篩選](#_TOC3_11)   
[覆寫 HTTP 方法動詞](#_TOC3_12)   
[樣板化 helper 的新 HiddenInputAttribute 類別](#_TOC3_13)   
[ValidationSummary Helper 方法可顯示模型層級錯誤](#_TOC3_14)   
[Visual Studio 中的 T4 範本會產生適用于 .NET Framework](#_TOC3_15)[API 改進](#_TOC4)目標版本的程式碼  
[重大變更](#_TOC5)  
[免責聲明](#_TOC6)  

## <a name="introduction"></a><a id="_TOC1"></a>  介紹

ASP.NET MVC 2 建置於 ASP.NET MVC 1.0，並引進一組大量的增強功能和功能，著重于提升生產力。 此版本與 ASP.NET MVC 1.0 相容，因此您所有適用于 ASP.NET MVC 1.0 的知識、技能、程式碼和延伸模組都會繼續套用。

如需有關 ASP.NET MVC 的詳細資訊，請造訪下列資源：

- [MSDN 上的 ASP.NET MVC 檔](https://go.microsoft.com/fwlink/?LinkId=159758)
- [ASP.NET MVC 網站](https://asp.net/mvc/)
- [ASP.NET MVC 論壇](https://forums.asp.net/1146.aspx)

## <a name="upgrading-an-aspnet-mvc-10-project-to-aspnet-mvc-2"></a><a id="_TOC2"></a>  將 ASP.NET MVC 1.0 專案升級為 ASP.NET MVC 2

ASP.NET MVC 2 可以與 ASP.NET MVC 1.0 並存安裝在同一部伺服器上，如此可讓應用程式開發人員選擇何時將 ASP.NET MVC 1.0 應用程式升級至 ASP.NET MVC 2。 如需有關如何升級的詳細資訊，請參閱將 [ASP.NET mvc 1.0 應用程式升級至 ASP.NET mvc 2](https://go.microsoft.com/fwlink/?LinkID=185459)的檔。

## <a name="new-features"></a><a id="_TOC3"></a>  新功能

本節說明 MVC 2 版本中引進的功能。

### <a name="templated-helpers"></a><a id="_TOC3_1"></a>  樣板化協助程式

樣板化協助程式可讓您自動建立 HTML 專案的關聯，以便編輯和顯示資料類型。 例如，當 view 中顯示 system.string 類型的資料時，可以自動轉譯日期選擇器 UI 元素。 這類似于欄位範本在 ASP.NET 動態資料中的運作方式。 如需詳細資訊，請參閱使用樣板化 helper 在 MSDN 網站上 [顯示資料](https://go.microsoft.com/fwlink/?LinkId=159062) 。

### <a name="areas"></a><a id="_TOC3_2"></a>  地區

區域可讓您將大型專案組織成多個較小的區段，以便管理大型 Web 應用程式的複雜度。 每個區段 ( 「區域」 ) 通常代表大型網站的個別區段，並可用來將相關聯的控制器和 views 集合分組。 如需詳細資訊，請參閱 MSDN 網站上的逐步解說 [：依區域組織 ASP.NET MVC 應用程式](https://go.microsoft.com/fwlink/?LinkId=158978) 。

若要建立新的區域，請在 [方案總管中，以滑鼠右鍵按一下專案，按一下 [新增]，然後按一下 [區域]。 這會顯示一個對話方塊，提示您輸入區功能變數名稱稱。 輸入區功能變數名稱稱之後，Visual Studio 會將新區域新增至專案。

下圖顯示具有兩個區域、系統管理員和 Blog 的專案範例版面配置。

![](what-is-new-in-aspnet-mvc/_static/image1.png)

當您建立區域時，Visual Studio 會將衍生自 AreaRegistration 的類別加入至每個區域。 此類別是必要的，才能註冊區域和其路由，如下列範例所示：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample1.cs)]

ASP.NET MVC 2 的預設專案範本包含對 global.asax 檔案程式碼中 RegisterAllAreas 方法的呼叫。 這個方法會藉由尋找衍生自 AreaRegistration 類別的所有類型、具現化類型的實例，然後在實例上呼叫 RegisterArea 方法，來註冊專案中的每個區域。 下列範例顯示如何完成這項操作。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample2.cs)]

如果您未藉由呼叫內容來指定 RegisterArea 方法中的命名空間。命名空間： Add 方法，預設會使用註冊類別的命名空間。

### <a name="support-for-asynchronous-controllers"></a><a id="_TOC3_3"></a>  支援非同步控制器

ASP.NET MVC 2 現在允許控制器以非同步方式處理要求。 這可能會讓經常呼叫封鎖作業的伺服器 (例如網路要求) 來改為呼叫非封鎖的對應專案，進而提升效能。 如需詳細資訊，請參閱 MSDN 上的 [使用 ASP.NET MVC 中的非同步控制器](https://msdn.microsoft.com/library/ee728598(v=VS.100).aspx) 主題。

### <a name="support-for-defaultvalueattribute-in-action-method-parameters"></a><a id="_TOC3_4"></a>  在動作方法參數中支援 DefaultValueAttribute

ComponentModel. DefaultValueAttribute 類別允許將引數參數的預設值提供給動作方法。 例如，假設已定義下列預設路由：

[!code-json[Main](what-is-new-in-aspnet-mvc/samples/sample3.txt)]

也假設已定義下列控制器和動作方法：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample4.cs)]

下列任何一個要求 Url 都會叫用上述範例中所定義的 View 動作方法。

- /Article/View/123
- /Article/View/123？ page = 1 (與先前的要求有效) 
- /Article/View/123？ page = 2

如果沒有 DefaultValueAttribute 屬性，則上述清單中的第一個 URL 將無法運作，因為頁面引數是未提供值的不可為 null 實值型別。

如果您的程式碼是以 Visual Basic 2010 或 Visual c # 2010 撰寫，您可以使用選擇性參數，而不是 DefaultValueAttribute 屬性，如下列範例所示：

[!code-vb[Main](what-is-new-in-aspnet-mvc/samples/sample5.vb)]

### <a name="support-for-binding-binary-data-with-model-binders"></a><a id="_TOC3_5"></a>  支援使用模型系結器來系結二進位資料

Html 會有兩個新的多載，可將二進位值編碼為 base-64 編碼的字串：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample6.cs)]

一般用途是在視圖中内嵌物件的時間戳記。 例如，您的應用程式可能包含下列產品物件：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample7.cs)]

編輯表單可以轉譯表單中的時間戳記屬性，如下列範例所示：

[!code-aspx[Main](what-is-new-in-aspnet-mvc/samples/sample8.aspx)]

這項標記會轉譯隱藏的輸入專案，其時間戳記值為 base-64 編碼的字串，類似于下列範例：

[!code-html[Main](what-is-new-in-aspnet-mvc/samples/sample9.html)]

此表單可能會張貼至具有 Product 類型引數的動作方法，如下列範例所示：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample10.cs)]

在動作方法中，TimeStamp 屬性已正確填入，因為張貼的 base-64 編碼的字串會轉換為位元組陣列。

### <a name="modelmetadata-and-modelmetadataprovider-classes"></a><a id="_TOC3_6"></a>  ModelMetadata 和 ModelMetadataProvider 類別

ModelMetadataProvider 類別會提供一個抽象概念，讓您能夠在視圖內取得模型的中繼資料。 MVC 2 包含的預設提供者，可讓 ComponentModel. DataAnnotations 命名空間中的屬性所公開的中繼資料。 您可以建立中繼資料提供者，以提供來自其他資料存放區的中繼資料，例如資料庫或 XML 檔案。

>viewdatadictionary 類別會公開 ModelMetadata 物件，其中包含由 ModelMetadataProvider 類別從模型中解壓縮的中繼資料。 這可讓樣板化協助程式取用此中繼資料，並據以調整其輸出。

如需詳細資訊，請參閱 [ModelMetadata](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) 和 [ModelMetadataProvider](https://msdn.microsoft.com/library/system.web.mvc.modelmetadataprovider(VS.100).aspx) 類別的檔。

### <a name="support-for-dataannotations-attributes"></a><a id="_TOC3_7"></a>  DataAnnotations 屬性的支援

ASP.NET MVC 2 支援使用 RangeAttribute、RequiredAttribute、StringLengthAttribute 和 RegexAttribute 驗證屬性 (在 ComponentModel. DataAnnotations 命名空間中定義，) 當您系結至模型以便提供輸入驗證時。

如需詳細資訊，請參閱 MSDN 網站上的 how [to：使用 DataAnnotations 屬性來驗證模型資料](https://go.microsoft.com/fwlink/?LinkId=159063) 。 您可以從下載說明如何使用這些屬性的範例專案 [https://go.microsoft.com/fwlink/?LinkId=157753](https://go.microsoft.com/fwlink/?LinkId=157753) 。

### <a name="model-validator-providers"></a><a id="_TOC3_8"></a>  模型驗證程式提供者

模型驗證提供者類別表示提供模型之驗證邏輯的抽象概念。 ASP.NET MVC 包含以 ComponentModel DataAnnotations 命名空間中包含的驗證屬性為基礎的預設提供者。 您也可以建立自己的驗證提供者，來定義自訂驗證規則，以及對模型進行驗證規則的自訂對應。 如需詳細資訊，請參閱 [ModelValidatorProvider](https://msdn.microsoft.com/library/system.web.mvc.ModelValidatorProvider(VS.100).aspx) 類別的檔。

### <a name="client-side-validation"></a><a id="_TOC3_9"></a>  用戶端驗證

模型驗證程式提供者類別會將驗證中繼資料以 JSON 序列化資料的形式公開給瀏覽器，以供用戶端驗證程式庫使用。 ASP.NET MVC 2 包含用戶端驗證程式庫和介面卡，可支援先前所述的 DataAnnotations 命名空間驗證屬性。 提供者類別也可讓您使用其他用戶端驗證程式庫，方法是撰寫可處理 JSON 資料和呼叫替代程式庫的介面卡。

### <a name="new-code-snippets-for-visual-studio-2010"></a><a id="_TOC3_10"></a>  Visual Studio 2010 的新程式碼片段

ASP.NET MVC 2 的一組 HTML 程式碼片段會隨 Visual Studio 2010 安裝。 若要查看這些程式碼片段的清單，請選取 [工具] 功能表中的 [程式碼片段管理員]。 針對 [語言] 選取 [HTML]，並針對 [位置] 選取 [ASP.NET MVC 2]。 如需有關如何使用程式碼片段的詳細資訊，請參閱 Visual Studio 檔。

### <a name="new-requirehttpsattribute-action-filter"></a><a id="_TOC3_11"></a>  新增 RequireHttpsAttribute 動作篩選

ASP.NET MVC 2 包含新的 RequireHttpsAttribute 類別，可套用至動作方法和控制器。 根據預設，篩選器會將非 SSL (HTTP) 要求重新導向至啟用 SSL 的 (HTTPS) 對等專案。

### <a name="overriding-the-http-method-verb"></a><a id="_TOC3_12"></a>  覆寫 HTTP 方法動詞

當您使用 REST 架構樣式來建立網站時，會使用 HTTP 指令動詞來判斷要對資源執行的動作。 REST 要求應用程式支援完整範圍的一般 HTTP 動詞命令，包括 GET、PUT、POST 和 DELETE。

ASP.NET MVC 2 包含新的屬性，您可以將這些屬性套用至動作方法和該功能精簡語法。 這些屬性可讓 ASP.NET MVC 根據 HTTP 指令動詞選取動作方法。 在下列範例中，POST 要求會呼叫第一個動作方法，而 PUT 要求會呼叫第二個動作方法。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample11.cs)]

在舊版的 ASP.NET MVC 中，這些動作方法需要更詳細的語法，如下列範例所示：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample12.cs)]

因為瀏覽器僅支援 GET 和 POST HTTP 動詞命令，所以不可能張貼到需要不同動詞的動作。 因此，您無法以原生方式支援所有的 RESTful 要求。

不過，若要在 POST 作業期間支援 RESTful 要求，ASP.NET MVC 2 引進了新的 HttpMethodOverride HTML helper 方法。 這個方法會轉譯隱藏的輸入專案，讓表單有效地模擬任何 HTTP 方法。 例如，藉由使用 HttpMethodOverride HTML helper 方法，您可以將表單提交顯示為 PUT 或 DELETE 要求。 HttpMethodOverride 的行為會影響下列屬性：

- HttpPostAttribute
- HttpPutAttribute
- HttpGetAttribute
- HttpDeleteAttribute
- AcceptVerbsAttribute

隱藏的輸入專案的名稱為 X-HTTP-方法-覆寫，且其值設定為要模擬的 HTTP 動詞。 您也可以在 HTTP 標頭中指定覆寫值，或以名稱/值組的形式在查詢字串值中指定覆寫值。

只有當真正的要求是 POST 要求時，才能使用覆寫。 使用任何其他 HTTP 動詞命令的要求將會忽略覆寫值。

### <a name="new-hiddeninputattribute-class-for-templated-helpers"></a><a id="_TOC3_13"></a>  樣板化 helper 的新 HiddenInputAttribute 類別

您可以將新的 HiddenInputAttribute 屬性套用至模型屬性，以指出在編輯器範本中顯示模型時是否應該轉譯隱藏的輸入元素。  (屬性會設定 HiddenInput) 的隱含 UIHint 值。 屬性的 DisplayValue 屬性可讓您指定值是否顯示在編輯器和顯示模式中。 當 DisplayValue 設定為 false 時，不會顯示任何內容，甚至是通常會在欄位周圍的 HTML 標籤。 DisplayValue 的預設值為 true。

您可以在下列案例中使用 HiddenInputAttribute 屬性：

- 當某個視圖可讓使用者編輯物件的識別碼時，必須顯示此值以及提供隱藏的輸入專案（包含舊識別碼），以便將它傳回給控制器。
- 當某個視圖可讓使用者編輯永遠不會顯示的二進位屬性，例如 timestamp 屬性。 在此情況下，不會顯示值和周圍的 HTML 標籤 (例如標籤和值) 。

下列範例顯示如何使用 HiddenInputAttribute 類別。

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample13.cs)]

當屬性設定為 true (或未) 指定參數時，就會發生下列情況：

- 在 [顯示範本] 中，會轉譯標籤，並向使用者顯示值。
- 在編輯器範本中，會轉譯標籤，並在隱藏的輸入元素中轉譯值。

當屬性設定為 false 時，會發生下列情況：

- 在 [顯示範本] 中，不會針對該欄位轉譯任何內容。
- 在編輯器範本中，不會轉譯任何標籤，而是在隱藏的輸入元素中轉譯值。

### <a name="htmlvalidationsummary-helper-method-can-display-model-level-errors"></a><a id="_TOC3_14"></a>  ValidationSummary Helper 方法可顯示模型層級錯誤

ValidationSummary helper 方法的新選項只顯示模型層級錯誤，而不是一律顯示所有驗證錯誤。 這可讓模型層級的錯誤顯示在驗證摘要中，並在每個欄位旁顯示欄位特定的錯誤。

### <a name="t4-templates-in-visual-studio-generate-code-that-is-specific-to-the-target-version-of-the-net-framework"></a><a id="_TOC3_15"></a>  Visual Studio 中的 T4 範本會產生特定于目標版本的程式碼 .NET Framework

ASP.NET MVC T4 主機中的 T4 檔案可使用新的屬性，指定應用程式所使用的 .NET Framework 版本。 這可讓 T4 範本產生 .NET Framework 版本專用的程式碼和標記。 在 Visual Studio 2008 中，此值一律為 .NET 3.5。 在 Visual Studio 2010 中，此值為 .NET 3.5 或 .NET 4。

## <a name="api-improvements"></a><a id="_TOC4"></a>  API 改進

本節描述現有 ASP.NET MVC 類型和成員的變更。

- 在控制器類別中新增受保護的虛擬 CreateActionInvoker 方法。 此方法是由控制器的 ActionInvoker 屬性所叫用，如果尚未設定任何啟動程式，則可讓啟動程式的延遲具現化。
- 在 AuthorizeAttribute 類別中新增受保護的虛擬 HandleUnauthorizedRequest 方法。 這會啟用衍生自 AuthorizeAttribute 的篩選器，以控制授權失敗時的行為。
- 在 ValueProviderDictionary 類別中加入新增 (字串索引鍵、物件值) 方法。 這可讓您使用 ValueProviderDictionary 的字典初始化運算式語法，如下列範例所示：

[!code-csharp[Main](what-is-new-in-aspnet-mvc/samples/sample14.cs)]

- \_在 Sys. AjaxCoNtext 類別中加入 get 物件方法。 這是類似于 get data 方法的 JavaScript 方法 \_ ，但如果回應的內容類型為 application/json，get 物件就會傳回 \_ json 物件。
- 在 AuthorizationCoNtext 類別中新增 ActionDescriptor 屬性。
- 加入 UrlParameter。選擇性標記，可用來解決當表單貼文中沒有屬性時，系結至包含 ID 屬性的模型時，所發生的問題。 如需詳細資訊，請參閱 Phil Haack 的 blog 上的專案 [ASP.NET MVC 2 選擇性 URL 參數](http://haacked.com/archive/2010/02/12/asp-net-mvc-2-optional-url-parameters.aspx) 。

## <a name="breaking-changes"></a><a id="_TOC5"></a>  重大變更

下列變更可能會導致現有的 ASP.NET MVC 1.0 應用程式發生錯誤。

#### <a name="change-in-property-validation-behavior-for-classes-that-implement-idataerrorinfo"></a>執行 IDataErrorInfo 之類別的屬性驗證行為變更

針對使用 IDataErrorInfo 來執行驗證的模型物件，不論是否已設定新值，都會驗證每個屬性。 在 ASP.NET MVC 1.0 中，只會驗證具有新值集的屬性。 在 ASP.NET MVC 2 中，只有在所有屬性驗證程式都成功時，才會呼叫 IDataErrorInfo 的 Error 屬性。

#### <a name="iis-script-mapping-script-is-no-longer-available-in-the-installer"></a>安裝程式中已不再提供 IIS 腳本對應腳本

IIS 腳本對應腳本是命令列腳本，用來為 IIS 6 和傳統模式的 IIS 7 設定腳本對應。 如果您使用 Visual Studio 程式開發伺服器或在整合模式中使用 IIS 7，則不需要腳本對應腳本。 這些腳本在 [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)上可作為個別不支援的下載。

#### <a name="the-htmlsubstitute-helper-method-in-mvc-futures-is-no-longer-available"></a>無法再使用 MVC 中的 Html 替代 helper 方法

由於 MVC 視圖引擎轉譯行為的變更，因此，Html. 替代 helper 方法無法運作且已移除。

#### <a name="the-ivalueprovider-interface-replaces-all-uses-of-idictionary"></a>IValueProvider 介面會取代 IDictionary 的所有用途

在 MVC 1.0 中接受 IDictionary 的每個屬性或方法引數現在都接受 IValueProvider。 這種變更只會影響包含自訂值提供者或自訂模型系結器的應用程式。 受此變更影響的屬性和方法的範例包括下列各項：

- ControllerBase 和 ModelBindingCoNtext 類別的 ValueProvider 屬性。
- Controller 類別的 TryUpdateModel 方法。

#### <a name="new-css-classes-were-added-in-the-sitecss-file"></a>已在網站 .css 檔案中新增 CSS 類別

ASP.NET MVC 專案範本中的網站 .css 檔案已更新，可包含驗證功能和樣板化協助程式所使用的新樣式。

#### <a name="helpers-now-return-an-mvchtmlstring-object"></a>Helper 現在會傳回 MvcHtmlString 物件

為了充分利用 ASP.NET 4 中的新 HTML 編碼運算式語法，HTML 協助程式的傳回型別現在是 MvcHtmlString，而不是字串。 如果您使用 ASP.NET MVC 2 和 ASP.NET 3.5 上的新協助程式，您將無法利用 HTML 編碼語法;只有當您在 ASP.NET 4 上執行 ASP.NET MVC 2 時，才可使用新的語法。

#### <a name="jsonresult-now-responds-only-to-http-post-requests"></a>JsonResult 現在只會回應 HTTP POST 要求

為了減輕可能洩漏資訊的 JSON 劫持攻擊，JsonResult 類別預設只會回應 HTTP POST 要求。 傳回 JsonResult 物件之動作方法的 Ajax GET 呼叫，應改為使用 POST。 如有必要，您可以藉由設定 JsonResult 的新 JsonRequestBehavior 屬性來覆寫此行為。 如需有關潛在惡意探索的詳細資訊，請參閱 Phil Haack 的 blog 上的 blog 文章 [JSON 劫持](http://haacked.com/archive/2009/06/25/json-hijacking.aspx) 。

#### <a name="model-and-modeltype-property-setters-on-modelbindingcontext-are-obsolete"></a>ModelBindingCoNtext 上的模型和 ModelType 屬性 setter 已淘汰

新的可設定 ModelMetadata 屬性已新增至 ModelBindingCoNtext 類別。 新屬性會封裝模型和 ModelType 屬性。 雖然模型和 ModelType 屬性已過時，但為了回溯相容性，屬性 getter 仍可運作;它們會委派給 ModelMetadata 屬性以取得值。

#### <a name="changes-to-the-defaultcontrollerfactory-class-break-custom-controller-factories-that-derive-from-it"></a>DefaultControllerFactory 類別的變更會中斷從其衍生的自訂控制器 factory

DefaultControllerFactory 類別是藉由移除 RequestCoNtext 屬性來修正。 為了取代這個屬性，要求內容實例會傳遞至受保護的虛擬 GetControllerInstance 和 GetControllerType 方法。 此變更會影響衍生自 DefaultControllerFactory 的自訂控制器 factory。

自訂控制器工廠通常用來提供 ASP.NET MVC 應用程式的相依性插入。 若要更新自訂控制器 factory 以支援 ASP.NET MVC 2，請將方法簽章或簽章變更為符合新的簽章，並使用要求內容參數，而非屬性。

#### <a name="area-is-a-now-a-reserved-route-value-key"></a>「Area」現在是保留的路由值索引鍵

路由值中的字串 "area" 現在在 ASP.NET MVC 中具有特殊意義，方法與「控制器」和「動作」相同。 其中一種方式是，如果 HTML 協助程式是以包含「區域」的路由值字典提供，則協助專家將不再于查詢字串中附加「區域」。

如果您使用區域功能，請務必不要使用 {area} 做為路由 URL 的一部分。

## <a name="disclaimer"></a><a id="_TOC6"></a>  免責 聲明

這是一份初稿，內容在本文所述的軟體於正式商業發行前都可能有所更動。

本文件所含的資訊代表 Microsoft Corporation 在發行日當下對問題的看法。 由於 Microsoft 必須因應不斷變化的市場狀況，因此不應將此解讀為 Microsoft 方面所作出的承諾，且 Microsoft 也無法保證在發行日之後所提出任何資訊的正確性。

本技術白皮書僅供參考。 MICROSOFT 對本文件中的資訊不提供任何明示、暗示或法定擔保。

遵守所有適用之著作權法係使用者的責任。 在不限制任何依著作權本得享有之權利，未經 Microsoft Corporation 書面許可， 貴用戶不得為任何目的使用任何形式或方法 (電子形式、機械形式、影印、記錄或其他方式) 複製或傳送本文件的任何部份，也不得將本文件的任何部份儲存或放入檢索系統 (a retrieval system)。

在本文件所提述之內容中，可能包括 Microsoft 的專利、申請專利案件、商標、著作權，或其他智慧財產權等。 除非於 Microsoft 提出的任何書面授權條約中明確規定者外，提供本文件並不表示賦予台端上述專利、商標、著作權或其他智慧財產權等之任何授權。

除非另有說明，否則此處所描述的範例公司、組織、產品、功能變數名稱、電子郵件地址、標誌、人員、地點及事件均屬虛構，且不會與任何真實的公司、組織、產品、功能變數名稱、電子郵件地址、標誌、人員、地點或事件相關。

© 2010 Microsoft Corporation。 著作權所有，並保留一切權利。

Microsoft 和 Windows 是 Microsoft Corporation 在美國及/或其他國家/地區的註冊商標或商標。

本文件中所提實際公司和產品，可能為各所有人所有之商標。
