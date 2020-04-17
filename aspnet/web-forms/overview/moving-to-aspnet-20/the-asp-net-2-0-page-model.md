---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 頁型號 |微軟文件
author: rick-anderson
description: 在ASP.NET 1.x 中,開發人員可以選擇內聯代碼模型和代碼背後的代碼模型。 代碼後面可以使用 Src attr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: 6c2435a06d04209db21fb8e075f68ff0b7a9ef7e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542855"
---
# <a name="the-aspnet-20-page-model"></a>ASP.NET 2.0 頁型號

由[微軟](https://github.com/microsoft)

> 在ASP.NET 1.x 中,開發人員可以選擇內聯代碼模型和代碼背後的代碼模型。 可以使用 Src@Page屬性或 指令的 Code 背後屬性實現代碼後面。 在ASP.NET 2.0中,開發人員在內聯代碼和代碼後面之間仍有選擇,但代碼背後的模型有顯著的增強功能。

在ASP.NET 1.x 中,開發人員可以選擇內聯代碼模型和代碼背後的代碼模型。 可以使用 Src@Page屬性或 指令的 Code 背後屬性實現代碼後面。 在ASP.NET 2.0中,開發人員在內聯代碼和代碼後面之間仍有選擇,但代碼背後的模型有顯著的增強功能。

## <a name="improvements-in-the-code-behind-model"></a>程式碼後模型的改進

為了充分理解ASP.NET 2.0 中代碼背後的更改,最好快速查看模型,因為它存在於ASP.NET 1.x 中。

## <a name="the-code-behind-model-in-aspnet-1x"></a>ASP.NET 1.x 中的代碼後模型

在ASP.NET 1.x 中,代碼後面模型由 ASPX 檔(Webform)和包含程式設計代碼的代碼後檔組成。 兩個檔使用 ASPX@Page檔中的指令連接。 ASPX 頁面上的每個控制器在代碼後面的檔中都有相應的聲明作為實例變數。 代碼背後的檔還包含事件綁定的代碼和 Visual Studio 設計器所需的生成代碼。 此模型工作相當良好,但由於 ASPX 頁中的每個 ASP.NET 元素都需要代碼背後的檔中的相應代碼,因此代碼和內容沒有真正的分離。 例如,如果設計器向 Visual Studio IDE 外部的 ASPX 檔添加了新的伺服器控制項,則應用程式將由於代碼背後的檔中缺少該控制項的聲明而中斷。

## <a name="the-code-behind-model-in-aspnet-20"></a>ASP.NET 2.0 中的代碼後模型

ASP.NET 2.0 大大改進了此模型。 在 ASP.NET 2.0 中,使用 ASP.NET 2.0 中提供的新*部分類*實現代碼後面。 ASP.NET 2.0 中的代碼後面類定義為部分類,這意味著它只包含類定義的一部分。 類定義的其餘部分由 ASP.NET 2.0 在運行時或使用 ASPX 頁或預編譯網站時動態生成。 代碼背後的檔案和 ASPX 頁之間的連結仍使用 @ Page 指令建立。 但是,ASP.NET 2.0 現在使用 CodeFile 屬性,而不是代碼背後或 Src 屬性。 繼承屬性還用於指定頁面的類名稱。

典型的 @ 頁面指令可能如下所示:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

ASP.NET 2.0 代碼背後的檔中的典型類定義可能如下所示:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C# 和 Visual Basic 是當前支援部分類的唯一託管語言。 因此,使用 J# 的開發人員將無法在 ASP.NET 2.0 中使用代碼後面模型。

新模型增強了代碼背後的模型,因為開發人員現在將具有僅包含他們創建的代碼的代碼檔。 它還提供了代碼和內容的真正分離,因為代碼後面的檔中沒有實例變數聲明。

> [!NOTE]
> 由於 ASPX 頁的部分類是事件綁定發生的位置,因此 Visual Basic 開發人員可以通過在代碼後面中使用 Handles 關鍵字綁定事件來實現輕微的性能提升。 C# 沒有等效關鍵字。

## <a name="new--page-directive-attributes"></a>新增 = 頁面指令屬性

ASP.NET 2.0 向 @ Page 指令添加了許多新屬性。 以下屬性在ASP.NET 2.0 中是新的。

## <a name="async"></a>非同步處理

Async 屬性允許您配置要非同步執行的頁面。 本模組稍後將介紹異步頁面。

## <a name="asynctimeout"></a>同步逾時

指定非同步頁面的超時。 默認值為 45 秒。

## <a name="codefile"></a>代碼檔案

CodeFile 屬性是 Visual Studio 2002/2003 中 CodeForin 屬性的替換。

### <a name="codefilebaseclass"></a>程式碼檔案基礎類別

在希望多個頁面從單個基類派生的情況下,使用 CodeFileBaseClass 屬性。 由於在ASP.NET中實現部分類,如果沒有此屬性,使用共用公共欄位引用在 ASPX 頁中聲明的控制項的基類將無法正常工作,因為 ASP.NETs 編譯引擎將根據頁面中的控件自動創建新成員。 因此,如果要在ASP.NET中為兩個或多個頁面定義一個公共基類,則需要在CodeFileBaseClass 屬性中定義指定基類,然後從該基類派生每個頁面類。 使用此屬性時,也需要 CodeFile 屬性。

## <a name="compilationmode"></a>編譯模式

此屬性允許您設置 ASPX 頁的編譯模式屬性。 "編譯模式"屬性是包含值 **"始終**、**自動**"和 **"從不"** 的枚舉。 默認值為 **「始終**」。 如果可能,**自動**設置將阻止ASP.NET動態編譯頁面。 從動態編譯中排除頁面可提高性能。 但是,如果排除的頁面包含必須編譯的代碼,則在流覽頁面時將引發錯誤。

## <a name="enableeventvalidation"></a>開啟事件驗證

此屬性指定是否驗證回退和回調事件。 啟用此功能後,將檢查用於回退或回調事件的參數,以確保它們源自最初呈現這些事件的伺服器控制項。

## <a name="enabletheming"></a>啟用"啟用"

此屬性指定ASP.NET主題是否在頁面上使用。 預設值為**false**。 ASP.NET主題在第[10單元](profiles-themes-and-web-parts.md)中介紹。

## <a name="linepragmas"></a>線普拉格瑪斯

此屬性指定是否應在編譯期間添加行雜注。 行雜注是調試器用於標記代碼特定部分的選項。

## <a name="maintainscrollpositiononpostback"></a>保持捲動位置後回

此屬性指定是否將 JAVAScript 注入頁面以保持回退之間的滾動位置。 默認情況下,此屬性**為 false。**

當此屬性為**true**時,ASP.NET&lt;將在&gt;回退後添加如下所示的腳本塊:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

請注意,此腳本塊的 src 是 WebResource.axd。 此資源不是物理路徑。 請求此文本時,ASP.NET動態生成腳本。

### <a name="masterpagefile"></a>母版頁面檔案

此屬性指定目前的頁面的主頁檔。 路徑可為相對路徑或絕對路徑。 母版頁在[單元 4](master-pages.md)中介紹。

## <a name="stylesheettheme"></a>樣式表主題

此屬性允許您覆蓋由ASP.NET 2.0 主題定義的使用者介面外觀屬性。 主題在第[10 單元](profiles-themes-and-web-parts.md)中介紹。

## <a name="theme"></a>佈景主題

指定頁面的主題。 如果未為 StyleSheetTheme 屬性指定值,則主題屬性將覆蓋應用於頁面上控制件的所有樣式。

## <a name="title"></a>Title

設置頁面的標題。 這裡指定的值會顯示在呈現頁面&lt;的標題&gt;元素中。

### <a name="viewstateencryptionmode"></a>檢視狀態加密模式

設置檢視狀態加密模式枚舉的值。 可用值為 **「始終**、**自動**」和 **「從不**」。 默認值為 **"自動**"。當此屬性設置為 **「自動」** 的值時,檢視狀態被加密是控制項透過調用**註冊需求視點狀態加密**方法請求它。

## <a name="setting-public-property-values-via-the--page-directive"></a>透過 @ 頁面指令設定公共財產值

ASP.NET 2.0 中 @ Page 指令的另一個新功能是設置基類公共屬性的初始值的能力。 例如,假設您的基類中具有名為 **「SomeText」** 的公共屬性,並且您希望在載入頁面時將其初始化為**Hello。** 只設定值值在 @ Page 指令中設定值即可實現此目的:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

@Page 指令的 **「一些文字」** 屬性將基類別中的「SomeText」屬性的初始值設定為*Hello!*。 以下視訊是使用 @ Page 指令設定基類別中公共屬性的初始值的演練。

![](the-asp-net-2-0-page-model/_static/image1.png)

[開啟全螢幕視訊](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>頁面類別的新公共屬性

以下公共屬性是 ASP.NET 2.0 中的新屬性。

## <a name="apprelativetemplatesourcedirectory"></a>套用相關樣本來源目錄

返回與應用程式相關的路徑到頁面或控制項。 例如,對於位於的http://app/folder/page.aspx頁面,屬性返回 */資料夾/。

## <a name="apprelativevirtualpath"></a>套用相對虛擬路徑

將相對虛擬目錄路徑返回到頁面或控制項。 例如,對於位於的http://app/folder/page.aspx頁面,屬性返回 */資料夾/頁.aspx。

## <a name="asynctimeout"></a>同步逾時

獲取或設置用於異步頁面處理的超時。 (此模組稍後將介紹異步頁面。

## <a name="clientquerystring"></a>客戶端查詢字串

返回請求網址的查詢字串部分的唯讀屬性。 此值是 URL 編碼的。 您可以使用 Hthterver 實用程式類的網址解碼方法對其進行解碼。

## <a name="clientscript"></a>用戶端文稿

此屬性返回一個用戶端ScriptManager物件,該物件可用於管理用戶端腳本的ASP.NET發射。 (本模組稍後將介紹用戶端腳本管理器類。

## <a name="enableeventvalidation"></a>開啟事件驗證

此屬性控制是否為回退和回調事件啟用事件驗證。 啟用後,將驗證用於回退或回調事件的參數,以確保它們源自最初呈現這些事件的伺服器控制件。

## <a name="enabletheming"></a>啟用"啟用"

此屬性獲取或設置布林,用於指定ASP.NET 2.0 主題是否應用於頁面。

## <a name="form"></a>表單

此屬性將 ASPX 頁上的 HTML 窗體作為 HtmlForm 物件返回。

## <a name="header"></a>頁首

此屬性返回對包含頁面標題的 HtmlHead 物件的引用。 您可以使用傳回的 HtmlHead 物件獲取/設定樣式表、符標記等。

## <a name="idseparator"></a>IdSe 參數

當ASP.NET為頁面上的控制項建構唯一ID時,此唯讀屬性獲取用於分隔控制項識別碼的字元。 但並不是針對直接從程式碼使用而設計。

## <a name="isasync"></a>IsAsync

此屬性允許異步頁面。 本模組稍後將討論異步頁面。

## <a name="iscallback"></a>IsCallback

如果頁面是回電的結果,則此唯讀屬性將**返回 true。** 本模組稍後將討論回電。

## <a name="iscrosspagepostback"></a>是交叉頁面後傳回

如果頁面是跨頁回郵的一部分,則此唯讀屬性將**返回 true。** 本模組稍後將介紹跨頁回郵。

## <a name="items"></a>項目

返回對 I字典實例的引用,該實例包含存儲在頁面上下文中的所有物件。 您可以將項添加到此 I字典物件,它們將在上下文的整個生存期內可供您使用。

## <a name="maintainscrollpositiononpostback"></a>保持捲動位置後回

此屬性控制ASP.NET是否發出 JavaScript,該 JavaScript 在回退後在瀏覽器中維護頁面滾動位置。 (本模組前面討論了此屬性的詳細資訊。

## <a name="master"></a>Master

此唯讀屬性返回對已應用母版頁的頁面的 MasterPage 實例的引用。

## <a name="masterpagefile"></a>母版頁面檔案

獲取或設置頁面的主頁檔名。 此屬性只能在 PreInit 方法中設置。

## <a name="maxpagestatefieldlength"></a>最大頁面狀態長度

此屬性獲取或設置以位元組為單位的頁面狀態的最大長度。 如果屬性設置為正數,則頁面視圖狀態將分解為多個隱藏欄位,以便不超過指定的位元組數。 如果屬性為負數,則視圖狀態不會分解為塊。

## <a name="pageadapter"></a>頁面配接器

返回對 PageAdapter 物件的引用,該物件修改請求流覽器的頁面。

## <a name="previouspage"></a>上一頁

在伺服器.傳輸或跨頁回發的情況下返回對上一頁的引用。

## <a name="skinid"></a>皮膚代碼

指定要應用於頁面的ASP.NET 2.0 外觀。

## <a name="stylesheettheme"></a>樣式表主題

此屬性獲取或設置應用於頁面的樣式表。

## <a name="templatecontrol"></a>樣本控制

返回對頁面的包含控制項的引用。

## <a name="theme"></a>佈景主題

獲取或設置應用於頁面的ASP.NET 2.0 主題的名稱。 此值必須在 PreInit 方法之前設置。

## <a name="title"></a>Title

此屬性獲取或設置從頁眉獲取的頁面的標題。

## <a name="viewstateencryptionmode"></a>檢視狀態加密模式

獲取或設定頁面的 ViewState 加密模式。 在本模組前面查看對此屬性的詳細討論。

## <a name="new-protected-properties-of-the-page-class"></a>頁面類別的新受保護屬性

以下是 ASP.NET 2.0 中 Page 類的新受保護屬性。

## <a name="adapter"></a>配接器

返回對在請求該頁面的設備上呈現該頁的 ControlAdapter 的引用。

## <a name="asyncmode"></a>非同步模式

此屬性指示頁面是否非同步處理。 它供運行時使用,而不是直接在代碼中使用。

## <a name="clientidseparator"></a>用戶端識別碼

此屬性返回在為控制項創建唯一客戶端 ID 時用作分隔符的字元。 它供運行時使用,而不是直接在代碼中使用。

## <a name="pagestatepersister"></a>佩奇·邦斯特

此屬性返回頁面的 Page StatePersister 物件。 此屬性主要由ASP.NET控件開發人員使用。

## <a name="uniquefilepathsuffix"></a>唯一的檔案路徑修復

此屬性返回一個唯一的後綴,該後綴追加到緩存瀏覽器的檔路徑上。 預設值為\_\_ufps* 和 6 位元數位。

## <a name="new-public-methods-for-the-page-class"></a>頁面類別的新公共方法

以下公共方法是 ASP.NET 2.0 中的 Page 類的新增方法。

## <a name="addonprerendercompleteasync"></a>額外預先成同步

此方法註冊事件處理程式委託以進行非同步頁面執行。 本模組稍後將討論異步頁面。

## <a name="applystylesheetskin"></a>套用樣式表外觀

將頁面樣式表中的屬性應用於頁面。

## <a name="executeregisteredasynctasks"></a>執行已註冊的同步工作

此方法是異步任務。

### <a name="getvalidators"></a>取得驗證器

如果未指定任何驗證組或默認驗證組,則返回驗證器的集合。

## <a name="registerasynctask"></a>註冊同步工作

此方法註冊新的異步任務。 本模組稍後將介紹異步頁面。

## <a name="registerrequirescontrolstate"></a>註冊需要控制狀態

此方法告訴ASP.NET必須保留頁面控件狀態。

## <a name="registerrequiresviewstateencryption"></a>註冊需要檢視狀態加密

此方法告訴ASP.NET頁面檢視狀態需要加密。

## <a name="resolveclienturl"></a>解析用戶端

返回可用於圖像等用戶端請求的相對 URL。

## <a name="setfocus"></a>SetFocus

此方法將焦點設置為最初載入頁面時指定的控制項。

## <a name="unregisterrequirescontrolstate"></a>取消註冊需要控制狀態

此方法將取消註冊傳遞給它的控制項,因為不再需要控制項狀態持久性。

## <a name="changes-to-the-page-lifecycle"></a>變更頁面生命循環

ASP.NET 2.0 中的頁面生命週期沒有顯著變化,但您應該知道一些新方法。 下面概述了ASP.NET 2.0 頁生命週期。

## <a name="preinit-new-in-aspnet-20"></a>PreInit(ASP.NET 2.0 中的新增功能)

PreInit 事件是開發人員可以訪問的生命週期中最早的階段。 通過添加此事件,可以以程式設計方式更改ASP.NET 2.0 主題、母版頁、ASP.NET 2.0 配置檔的訪問屬性等。如果您處於後回狀態,則實現Viewstate尚未應用於生命週期的此時控件非常重要。 因此,如果開發人員在此階段更改控件的屬性,則在頁面生命週期的稍後版本中可能會覆蓋該控制項的屬性。

## <a name="init"></a>Init

Init 事件未從 ASP.NET 1.x 更改。 這是您希望讀取或初始化頁面上控制項屬性的位置。 在此階段,母版頁、主題等已應用於該頁。

## <a name="initcomplete-new-in-20"></a>InitComplete(2.0 新增)

InitComplete 事件在頁面初始化階段結束時調用。 在生命週期的此時,可以訪問頁面上的控件,但尚未填充其狀態。

## <a name="preload-new-in-20"></a>預載入(2.0 中新增)

此事件是在應用所有回郵數據后,並在頁面\_載入之前調用的。

## <a name="load"></a>載入

載入事件未從 ASP.NET 1.x 更改。

## <a name="loadcomplete-new-in-20"></a>載入完成(2.0 中新增)

LoadComplete 事件是頁面載入階段的最後一個事件。 在此階段,所有回退和視圖狀態數據已應用於頁面。

## <a name="prerender"></a>預算

如果希望對動態添加到頁面的控制項正確維護檢視狀態,則 PreRender 事件是添加它們的最後機會。

## <a name="prerendercomplete-new-in-20"></a>預成成成(2.0中新增)

在預渲染完成階段,所有控制項都已添加到頁面,並且頁面已準備好呈現。 預渲染完成事件是保存頁面檢視狀態之前引發的最後一個事件。

## <a name="savestatecomplete-new-in-20"></a>儲存狀態完成(2.0 中的新增功能)

保存所有頁面檢視狀態和控制狀態后,將立即調用"保存狀態完成"事件。 這是頁面實際呈現到瀏覽器之前的最後一個事件。

## <a name="render"></a>轉譯

自 1.x ASP.NET 以來,渲染方法未更改。 這是 HtmlTextWriter 初始化並將頁面呈現到瀏覽器的位置。

## <a name="cross-page-postback-in-aspnet-20"></a>ASP.NET 2.0 中的跨頁回郵

在ASP.NET 1.x 中,需要回郵後貼到同一頁。 不允許進行跨頁回郵。 ASP.NET 2.0 添加了透過 IButtonControl 介面發回其他頁面的功能。 實現新的 IButtonControl 介面的任何控制項(除了第三方自定義控制件之外,還可以利用此新功能,使用 PostBackUrl 屬性。 以下代碼顯示將回發回第二頁的 Button 控制件。

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

當頁面被發回時,啟動回郵的頁面可通過第二頁上的「上頁」屬性訪問。 此功能通過新的 WebForm\_DoPostBackOptions 用戶端功能實現,該功能 ASP.NET 2.0 在控制項回退回其他頁面時呈現到頁面。 此 JAVAScript 函數由向用戶端發出腳本的新 WebResource.axd 處理程式提供。

下面的視頻是跨頁回帖的演練。

![](the-asp-net-2-0-page-model/_static/image2.png)

[開啟全螢幕視訊](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>有關跨頁回郵的更多詳細資訊

### <a name="viewstate"></a>檢視狀態

您可能已經問自己,在跨頁回退方案中,從第一頁中查看狀態會發生什麼情況。 畢竟,任何不實現 IPostBackDataHandler 的控制項都將透過檢視狀態保持其狀態,因此,要造訪跨頁後回的第二頁上該控制項的屬性,您必須有權訪問該頁的視圖狀態。 ASP.NET 2.0 使用第二頁\_\_中稱為 「上頁」的新隱藏欄位處理此方案。 「\_\_上一頁」 的檢視狀態,以便您可以存取第二頁中所有控制項的屬性。

### <a name="circumventing-findcontrol"></a>繞過尋找控制

在跨頁回發的影片演練中,我使用 FindControl 方法獲取對第一頁上的 TextBox 控制件的引用。 該方法適用於此目的,但 FindControl 成本高昂,需要編寫其他代碼。 幸運的是,ASP.NET 2.0 為此提供了 FindControl 的替代方法,這在很多方案中都不起作用。 使用「上一頁類型」指令允許您使用 TypeName 或 VirtualPath 屬性對上一頁進行強類型引用。 TypeName 屬性允許您指定上一頁的類型,而 VirtualPath 屬性允許您使用虛擬路徑引用上一頁。 設置上一頁類型指令後,必須公開要允許使用公共屬性訪問的控制項等。

## <a name="lab-1-cross-page-postback"></a>實驗室 1 跨頁回郵

在本實驗中,您將創建一個應用程式,該應用程式使用ASP.NET2.0的新跨頁回郵功能。

1. 打開 Visual Studio 2005 並創建新 ASP.NET 網站。
2. 添加新的 Web 表單,稱為頁 2.aspx。
3. 在「設計」檢視中打開預設.aspx 並添加按鈕控制項和 TextBox 控制件。 

    1. 為按鈕控制項指定 **「提交按鈕**」的 ID,而文字框控制件為**使用者名**ID。
    2. 將按鈕的 PostBackUrl 屬性設置為頁 2.aspx。
4. 在源檢視中打開頁面 2.aspx。
5. 新增 # 上一頁類型指令,如下所示:
6. 將以下代碼加入頁面 2.aspx 的代碼後面的\_頁面 載入: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. 單擊"生成"功能表上的"生成"功能表生成專案。
8. 將以下代碼加入 Default.aspx 的代碼後面: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. 將頁\_2.aspx 中的頁面載入變更為以下內容: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. 建置專案。
11. 執行專案。
12. 在文字框中輸入您的姓名,然後按一下這個按鈕。
13. 結果如何?

## <a name="asynchronous-pages-in-aspnet-20"></a>ASP.NET 2.0 中的非同步頁面

ASP.NET中的許多爭用問題是由外部調用(如 Web 服務或資料庫調用)的延遲、檔 IO 延遲等引起的。當針對ASP.NET應用程式發出請求時,ASP.NET使用其工作線程之一來為該請求提供服務。 該請求擁有該線程,直到請求完成並發送回應。 ASP.NET 2.0 尋求通過添加非同步執行頁面的功能來解決此類問題的延遲問題。 這意味著工作線程可以啟動請求,然後將其他執行交給另一個線程,從而快速返回到可用的線程池。 當檔 IO、資料庫調用等完成時,將從線程池獲取一個新線程以完成請求。

使頁面非同步執行的第一步是設定頁面指令的**Async**屬性,如下所示:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

此屬性告訴ASP.NET實現頁面的IHttpAsyncHandler。

下一步是在預渲染之前在頁面生命週期的某一點調用 AddOnPreRenderCompleteAsync 方法。 (此方法通常在頁面\_載入中呼叫。AddOnPreRenderCompleteasync方法採用兩個參數;a BeginEventHandler 和 endEventHandler。 BeginEventHandler 傳回 IAsyncResult,然後將該結果作為參數傳遞給 EndEventHandler。

下面的視頻是異步頁面請求的演練。

![](the-asp-net-2-0-page-model/_static/image3.png)

[開啟全螢幕視訊](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> 在結束事件處理程式完成之前,非同步頁面不會呈現給瀏覽器。 毫無疑問,但一些開發人員會認為非同步請求類似於異步回調。 重要的是要意識到他們不是。 非同步請求的好處是,可以將第一個輔助線程返回到線程池以服務新請求,從而減少由於受 IO 綁定等原因引起的爭用。

## <a name="script-callbacks-in-aspnet-20"></a>ASP.NET 2.0 中的文本回調

Web 開發人員一直在尋找防止與回調關聯的閃爍的方法。 在ASP.NET 1.x 中,智慧導航是避免閃爍的最常見方法,但智慧導航由於在用戶端上實現的複雜性而給一些開發人員帶來了問題。 ASP.NET 2.0 使用腳本回調解決此問題。 文本回調利用 XMLHTTP 通過 JavaScript 對 Web 伺服器發出請求。 XMLHTTP 請求返回 XML 數據,然後可以通過瀏覽器的 DOM 進行操作。 XMLHttp 代碼由新的 WebResource.axd 處理程式對使用者隱藏。

為了在 2.0 ASP.NET 配置腳本回調,需要執行幾個步驟。

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>步驟 1 : 實現 IcallbackEventHandler 介面

為了ASP.NET識別您的頁面參與腳本回調,必須實現ICallbackEventHandler介面。 您可以在代碼後面的檔案中執行此操作,如下所示:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

您還可以使用 # 執行指令執行此操作,如下所示:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

在使用內聯ASP.NET代碼時,通常可以使用 @ 實現指令。

## <a name="step-2--call-getcallbackeventreference"></a>第二步 : 呼叫傳回事件參考

如前所述,XMLHTTP調用封裝在 WebResource.axd 處理程式中。 呈現頁面時,ASP.NET將添加對 WebForm DoCallback\_的調用,WebForm DoCallback 是 WebResource.axd 提供的用戶端腳本。 WebForm\_DoCallback 函數\_\_將替換 回調的 doPostBack 函數。 請記住,\_\_以程式設計方式提交頁面上的表單。 在回調方案中,您希望防止回退,因此\_\_PostBack 是不夠的。

> [!NOTE]
> \_\_doPostBack 仍呈現在用戶端文本回調方案中的頁面。 但是,它不用於回調。

WebForm\_DoCallback 用戶端函數的參數通過伺服器端函數 GetCallbackEventReference 提供,該函\_數通常在頁面載入中調用。 對 GetbackEvent 參考的典型調用可能如下所示:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> 在這種情況下,cm 是用戶端腳本管理器的實例。 本模組稍後將介紹用戶端腳本管理器類。

有幾個重載版本的 GetbackEvent 參考。 在這種情況下,參數如下所示:

`this`

對調用 GetbackEvent參照的控制件的引用。 在這種情況下,它是頁面本身。

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

將從用戶端代碼傳遞到伺服器端事件的字串參數。 在這種情況下,我傳遞名為 ddlCompany 的下拉的值。

`ShowCompanyName`

用戶端函數的名稱,該函數將接受伺服器端回調事件的返回值(作為字串)。 僅當伺服器端回調成功時,才會調用此功能。 因此,為了魯棒性,通常建議使用重載版本的 GetCallbackEventReference,該版本需要一個額外的字串參數,指定用戶端函數的名稱,在發生錯誤時執行。

`null`

表示在回調到伺服器之前啟動的用戶端函數的字串。 在這種情況下,沒有這樣的腳本,因此參數為 null。

`true`

指定是否非同步執行回調的布林。

用戶端上對 WebForm\_DoCallback 的調用將傳遞這些參數。 因此,在用戶端上呈現此頁面時,該代碼將如下所示:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

請注意,用戶端上函數的簽名有點不同。 用戶端函數傳遞 5 個字串和一個布爾。 附加字串(在上例中為空)包含用戶端函數,該函數將處理來自伺服器端回調的任何錯誤。

## <a name="step-3--hook-the-client-side-control-event"></a>步驟 3 : 鉤用戶端控制事件

請注意,上面 GetCallbackEventReference 的返回值已分配給字串變數。 該字串用於鉤接啟動回調的控制項的用戶端事件。 在此示例中,回調由頁面上的下拉展開,因此我想掛接*OnChange*事件。

要掛接用戶端事件,只需將處理程式添加到客戶端標記,如下所示:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

回想一下*cbRef*是從調用 GetbackEvent 參考的返回值。 它包含上面顯示的對 WebForm\_DoCallback 的調用。

## <a name="step-4--register-the-client-side-script"></a>步驟 4 : 註冊用戶端文稿

回想一下,對 GetCallbackEventReference 的呼叫指定在伺服器端回檔成功時將執行名為**ShowCompanyName**的用戶端文稿。 需要使用 ClientScriptManager 實例將該文本添加到頁面。 (本模組稍後將討論用戶端腳本管理器類。你這樣做,像這樣:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>步驟 5 : 呼叫 ICallbackEventHandler 介面的方法

ICallbackEventHandler 包含需要在代碼中實現的兩種方法。 它們是 **「提高回調事件**」和 **「獲取回調事件**」。

**RaiseCallbackEvent**將字串作為參數,不返回任何內容。 字串參數從用戶端呼叫傳遞到 WebForm\_DoCallback。 在這種情況下,該值是名為 ddlCompany 的下拉*的值*屬性。 伺服器端代碼應放在「提高回調事件」方法中。 例如,如果您的回調針對外部資源發出 Web 請求,則應將該代碼放在「提高回調事件」 中。

**GetCallbackEvent**負責處理回調返回給客戶端的問題。 它不需要參數並返回字串。 傳回的字串會傳回為參數傳回客戶端函數,在本例*中為 ShowCompanyName*。

完成上述步驟後,即可在 2.0 ASP.NET 執行腳本回調。

![](the-asp-net-2-0-page-model/_static/image4.png)

[開啟全螢幕視訊](the-asp-net-2-0-page-model/_static/callback1.wmv)

ASP.NET文稿回調在支援進行 XMLHTTP 調用的任何瀏覽器中都受支援。 這包括當今使用的所有現代瀏覽器。 Internet Explorer 使用 XMLHttp ActiveX 物件,而其他現代瀏覽器(包括即將推出的 IE 7)使用內部 XMLHTTP 物件。 要以程式設計方式確定瀏覽器是否支援回調,可以使用 **「請求.Browser.支援回撥」** 屬性。 如果請求的用戶端支援腳本回調,則此屬性將返回**true。**

## <a name="working-with-client-script-in-aspnet-20"></a>在 ASP.NET 2.0 中使用用戶端文稿

ASP.NET 2.0 中的用戶端腳本是使用用戶端腳本管理員類管理的。 用戶端文稿管理器類使用類型和名稱跟蹤用戶端腳本。 這樣可以防止同一腳本多次以程式設計方式插入到頁面上。

> [!NOTE]
> 在頁面上成功註冊腳本后,任何後續註冊同一腳本的嘗試都將導致腳本無法第二次註冊。 不添加重複的腳本,也不會發生異常。 為了避免不必要的計算,可以使用一些方法來確定腳本是否已註冊,以便不要嘗試多次註冊腳本。

用戶端文本管理員的方法應對所有當前ASP.NET開發人員都熟悉:

## <a name="registerclientscriptblock"></a>註冊用戶端文稿塊

此方法將腳本添加到呈現頁面的頂部。 這對於添加將在用戶端上顯式調用的函數非常有用。

此方法有兩個重載版本。 四個參數中有三個在它們中很常見。 其中包括：

`type (string)`

***類型***參數標識腳本的類型。 通常最好使用頁面的類型(這。獲取類型的類型。

`key (string)`

***鍵***參數是腳本的使用者定義的密鑰。 對於每個腳本來說,這應該是唯一的。 如果嘗試添加具有相同鍵和已添加腳本類型的腳本,則不會添加該腳本。

`script (string)`

***文本***參數是包含要添加的實際文本的字串。 建議使用 StringBuilder 創建腳本,然後在 StringBuilder 上使用 ToString() 方法分配***腳本***參數。

如果使用載入的註冊用戶端腳本塊,該參數僅包含三個參數,則必須在腳本中包含腳本元素&lt;&gt;(&lt;腳&gt;本 和 /腳本)。

您可以選擇使用採用第四個參數的註冊用戶端腳本塊的重載。 第四個參數是布爾,它指定ASP.NET是否應該為您添加腳本元素。 如果此參數**為 true,** 則文本不應顯式包含文稿元素。

使用 IsClientScriptBlock 註冊方法確定腳本是否已註冊。 這允許您避免嘗試重新註冊已註冊的腳本。

### <a name="registerclientscriptinclude-new-in-20"></a>註冊用戶端文稿包括(2.0 中的新增功能)

註冊用戶端文稿包含標記創建連結到外部文稿檔的腳本塊。 它有兩個過載。 一個需要一個鍵和一個URL。 第二個參數添加第三個參數,指定類型。

例如,以下代碼產生一個腳本塊,該文本塊連結到應用程式文本資料夾的根目錄中的 js 函數.js:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

此代碼在呈現的頁面中產生以下代碼:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> 腳本塊呈現在頁面底部。

使用 IsClientScript 包括註冊方法確定文本是否已註冊。 這允許您避免嘗試重新註冊腳本。

## <a name="registerstartupscript"></a>註冊啟動文稿

註冊啟動腳本方法採用與註冊用戶端腳本塊方法相同的參數。 註冊到註冊啟動腳本的腳本在頁面載入後在 OnLoad 用戶端事件之前執行。 在 1.X 中,註冊&lt;到的 腳本位於關閉&gt;/窗體 標記之前,而註冊到 RegisterClientScriptBlock&lt;的腳&gt;本則緊隨打開 表單 標記之後放置。 在 ASP.NET 2.0 中,兩&lt;者&gt;都放在 關閉 /窗體標記之前。

> [!NOTE]
> 如果向註冊啟動腳本註冊函數,則在客戶端代碼中顯式調用該函數之前,該函數不會執行。

使用 IsStartupScript 註冊方法確定腳本是否已註冊,並避免嘗試重新註冊腳本。

## <a name="other-clientscriptmanager-methods"></a>其他用戶端文稿管理員方法

下面是用戶端ScriptManager 類的其他一些有用方法。

|  <strong>取得回撥事件參考</strong>   |                                                 請參閱本模組前面的腳本回調。                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>取得後回用戶端超連結</strong>  |                獲取可用於從用戶端事件發回的 JavaScript 引用&lt;(javascript:&gt;呼叫 )。                 |
|  <strong>取得後回活動參考</strong>   |                                   獲取可用於從用戶端發起回帖子的字串。                                    |
|      <strong>取得 Web 資源網址</strong>       | 返回嵌入在程式集中的資源的 URL。 必須與<strong>註冊用戶端腳本資源</strong>結合使用。 |
| <strong>註冊用戶端文稿資源</strong> |     將 Web 資源註冊到該頁。 這些資源嵌入到程式集中並由新的 WebResource.axd 處理程式處理。      |
|     <strong>註冊隱藏欄位</strong>      |                                                 將隱藏的表單欄段與頁面註冊。                                                 |
|  <strong>註冊提交聲明</strong>   |                                  註冊提交 HTML 窗體時執行的用戶端代碼。                                   |
