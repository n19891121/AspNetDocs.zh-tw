---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 和視覺工作室 2012 中的新增功能 |微軟文件
author: rick-anderson
description: 本文檔介紹 ASP.NET 4.5 中引入的新功能和增強功能。 它描述了為網頁開發所做的改進...
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676283"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>ASP.NET 4.5 與 Visual Studio 2012 的新功能

> 本文檔介紹 ASP.NET 4.5 中引入的新功能和增強功能。 它還描述了在 Visual Studio 2012 中為 Web 開發所做的改進。 本文檔最初發佈於 2012 年 2 月 29 日。

- [ASP.NET核心執行時和框架](#_Toc318097372)

    - [非音子讀取與寫入 HTTP 要求與回應](#_Toc318097373)
    - [HTTPRequest 處理的改進](#_Toc318097374)
    - [同步刷新回應](#_Toc318097375)
    - [支援*與*系統*建立工作的*非同步模組與處理程式](#_Toc318097376)
    - [非同步 HTTP 模組](#_Toc318097377)
    - [非同步 HTTP 處理程式](#_Toc318097378)
    - [新的ASP.NET要求驗證功能](#_Toc318097379)
    - [延遲("延遲")請求驗證](#_Toc318097380)
    - [支援未經認證的要求](#_Toc318097381)
    - [AntiXSS 函式庫](#_Toc318097382)
    - [支援 WebSocket 協定](#_Toc318097383)
    - [捆綁和最小化](#_Toc318097384)
    - [Web 託管的效能改進](#_Toc_perf)

        - [關鍵性能因素](#_Toc_perf_1)
        - [對新效能功能的要求](#_Toc_perf_2)
        - [共用公共程式集](#_Toc_perf_3)
        - [使用多核 JIT 編譯,加快啟動速度](#_Toc_perf_4)
        - [調整垃圾資源以最佳化記憶體](#_Toc_perf_5)
        - [為 Web 應用程式預取](#_Toc_perf_6)
- [ASP.NET Web 表單](#_Toc318097385)

    - [強型別資料控制項](#_Toc318097386)
    - [模型繫結](#_Toc318097387)

        - [選擇資料](#_Toc318097388)
        - [價值提供者](#_Toc318097389)
        - [依控制項的值篩選](#_Toc318097390)
    - [HTML 編碼資料繫結表示式](#_Toc318097391)
    - [不顯眼的驗證](#_Toc318097392)
    - [HTML5 更新](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET Web Pages 2](#_Toc318097395)
- [視覺工作室 2012 發佈候選](#_Toc318097396)

    - [Visual Studio 2010 和 Visual Studio 2012 版本候選版本之間的項目共享(專案相容性)](#project-compatibility)
    - [ASP.NET 4.5 網站樣本中的設定變更](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [IIS 7 中用於ASP.NET路由的本機支援](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML 編輯器](#_Toc318097397)

        - [智慧任務](#_Toc318097398)
        - [WAI-ARIA 支援](#_Toc318097399)
        - [新的 HTML5 碼段](#_Toc318097400)
        - [擷取使用者控制項](#_Toc318097401)
        - [屬性中片段的 IntelliSense](#_Toc318097402)
        - [重新命名開啟或關閉標籤時自動重新命名符合標記](#_Toc318097403)
        - [事件處理程式產生](#_Toc318097404)
        - [智慧縮排](#_Toc318097405)
        - [自動減少敘述完成](#_Toc318097406)
    - [JavaScript 編輯器](#_Toc318097407)

        - [代碼概述](#_Toc318097408)
        - [括號對稱](#_Toc318097409)
        - [跳到訂](#_Toc318097410)
        - [ECMAScript5 支援](#_Toc318097411)
        - [DOM 感知](#_Toc318097412)
        - [VSDOC 簽署重載](#_Toc318097413)
        - [隱含參考](#_Toc318097414)
    - [CSS 編輯器](#_Toc318097415)

        - [自動減少敘述完成](#_Toc318097416)
        - [分層縮進。](#_Toc318097417)
        - [CSS 駭客支援](#_Toc318097418)
        - [供應商指定的架構(-moz-,-webkit)](#_Toc318097419)
        - [評論和非評論支援](#_Toc318097420)
        - [Color picker](#_Toc318097421)
        - [程式碼片段](#_Toc318097422)
        - [自訂區域](#_Toc318097423)
    - [Page Inspector](#_Toc318097424)
    - [出版](#_Toc318097425)

        - [發佈設定檔](#_Toc318097426)
        - [ASP.NET 預寫和合併](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [免責聲明](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET核心執行時和框架

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>非音子讀取與寫入 HTTP 要求與回應

ASP.NET 4 引入了使用*HTTPRequest.Get 無緩衝區輸入流*方法將 HTTP 請求實體作為流讀取的功能。 此方法提供了對請求實體的流式訪問。 但是,它同步執行,在請求的持續時間內將線程捆綁在一起。

ASP.NET 4.5 支援在 HTTP 請求實體上非同步讀取流的功能,以及非同步刷新的能力。 ASP.NET 4.5 還使您能夠對 HTTP 請求實體進行雙緩衝,從而更輕鬆地與下游 HTTP 處理程式(如 .aspx 頁處理程式和 ASP.NET MVC 控制器)集成。

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>HTTPRequest 處理的改進

ASP.NET 4.5 從 HTTPRequest 返回的流引用 *.Get無緩衝區輸入流*支援同步和非同步讀取方法。 從*Get 無緩衝區輸入流*返回的*流*物件現在實現了 BeginRead 和 EndRead 方法。 非同步*的流*方法允許您以塊非同步讀取請求實體,而ASP.NET在非同步讀取迴圈的每個反覆運算之間釋放當前線程。

ASP.NET 4.5 還添加了一種以緩衝方式讀取請求實體的配套方法 *:HTTPRequest.GetBufferedInputStream*。 這種新的重載工作類似於*Get 無緩衝區輸入流*,支援同步讀取和異步讀取。 但是,在讀取時 *,GetBufferedInputStream*還會將實體位元組複製到ASP.NET內部緩衝區中,以便下游模組和處理程式仍可以訪問請求實體。 例如,如果導管中的一些上游程式碼已經使用*GetBufferedInputStream*讀取了請求實體,您仍可以使用*HttpRequest.Form*或*HTTPRequest.Files*。 這允許您對請求執行非同步處理(例如,將大型檔上載流式傳輸到資料庫),但之後仍運行 .aspx 頁和 MVC ASP.NET控制器。

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>同步刷新回應

當用戶端距離遙遠或具有低頻寬連接時,向 HTTP 客戶端發送回應可能需要相當長的時間。 通常ASP.NET緩衝回應位元組,因為它們是由應用程式創建的。 然後ASP.NET然後在請求處理的末尾執行累積緩衝區的單個發送操作。

如果緩衝回應很大(例如,將大型檔流式傳輸到用戶端),則必須定期調用*HttpResponse.Flush,* 以便向用戶端發送緩衝輸出並保持記憶體使用方式控制。 但是,由於*Flush*是同步調用,因此反覆運算調用*Flush*仍會在可能長時間運行的請求的持續時間內使用線程。

ASP.NET 4.5 添加了使用*HttpResponse*類的*BeginFlush*和*endFlush*方法非同步執行刷新的支援。 使用這些方法,您可以創建非同步模組和非同步處理程式,這些模組和非同步處理程式在不捆綁作業系統線程的情況下將資料增量發送到用戶端。 在*BeginFlush*和*結束刷新*調用之間,ASP.NET釋放當前線程。 這大大減少了支援長時間運行的 HTTP 下載所需的活動線程總數。

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>支援*await*與*工作*- 基於非非非同步模組與處理程式

.NET 框架 4 引入了一個非同步程式設計概念,稱為*工作*。 工作由系統中的*工作*型態與相關類型表示 *。* .NET Framework 4.5 基於此功能,具有編譯器增強功能,使使用*Task*物件變得簡單。 在 .NET 架構 4.5 中,編譯器支援兩個新關鍵字:*等待*與*非同步*。 *await*關鍵字是語法速記,用於指示代碼段應異步等待其他代碼段。 *非同步*關鍵字表示可用於將方法標記為基於任務的非同步方法的提示。

*await、**非同步*和*工作*物件的組合使您在 .NET 4.5 中編寫異步代碼變得更加容易。 ASP.NET 4.5 支援這些簡化與新的 API,允許您編寫非同步 HTTP 模組和異步 HTTP 處理程式使用新的編譯器增強功能。

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>非同步 HTTP 模組

假設您要在返回*任務*物件的方法內執行非同步工作。 以下代碼示例定義了一個非同步方法,該方法進行非同步調用以下載 Microsoft 主頁。 請注意在方法簽名中使用*非同步*關鍵字,並注意對*下載StringTaskAsync*的*等待*呼叫。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

這就是您需要編寫的 - .NET Framework 將自動處理在等待下載完成時展開調用堆疊,以及在下載完成後自動還原調用堆疊。

現在假設您要在非同步ASP.NET HTTP 模組中使用此非同步方法。 ASP.NET 4.5 包括幫助器方法 *(EventHandlerTaskAsyncHelper*) 和新的委託類型 *(TaskEventHandler),* 可用於將基於任務的異步方法與 ASP.NET HTTP 管道公開的較舊的非同步程式設計模型集成。 此範例展示如何:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>非同步 HTTP 處理程式

在ASP.NET中編寫非同步處理程式的傳統方法是實現*IHttpAsyncHandler*介面。 ASP.NET 4.5 引入了可以從派生的*HttpTaskSyncHandler*非同步基類型,這使得編寫異步處理程式變得更加容易。

*HttpTaskAsyncHandler*類型是抽象的,需要您重寫*ProcessRequestAsync*方法。 內部ASP.NET負責將*ProcessRequestAsync*的返回簽名(*任務*物件)與ASP.NET管道使用的舊異步程式設計模型整合。

下面的範例展示如何使用*Task*和*等待*做為非同步 HTTP 處理程式實現的一部分:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>新的ASP.NET要求驗證功能

預設情況下,ASP.NET執行請求驗證 - 它會檢查在欄位、標頭、Cookie 等中尋找標記或腳本的請求。 如果檢測到任何異常,ASP.NET將引發異常。 這是抵禦潛在跨網站腳本攻擊的第一道防線。

ASP.NET 4.5 使選擇性讀取未經驗證的請求數據變得容易。 ASP.NET 4.5 還集成了流行的 AntiXSS 庫,該庫以前是外部庫。

開發人員經常要求能夠有選擇地關閉其應用程式的請求驗證。 例如,如果您的應用程式是論壇軟體,您可能希望允許使用者提交 HTML 格式的論壇帖子和評論,但仍要確保請求驗證檢查所有其他內容。

ASP.NET 4.5 引入了兩個功能,使您能夠輕鬆有選擇地處理未驗證的輸入:延遲("延遲")請求驗證和對未驗證請求數據的訪問。

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>延遲("延遲")請求驗證

在 ASP.NET 4.5 中,默認情況下,所有請求數據都需接受請求驗證。 但是,您可以將應用程式配置為延遲請求驗證,直到實際訪問請求數據。 (這有時稱為延遲請求驗證,具體取決於某些數據方案的延遲載入等術語。以將*要求驗證模式*屬性設定為*httpRUntime*元素中的 4.5,可以將應用程式設定為在 Web.config 檔中使用延遲驗證,如以下範例所示:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

當請求驗證模式設置為 4.5 時,請求驗證僅針對特定請求值觸發,並且僅在代碼訪問該值時觸發。 例如,如果代碼獲取了"Request.Form_"論壇\_帖子"的值,則僅針對窗體集合中該元素調用請求驗證。 *窗體*集合中的其他元素均未經過驗證。 在ASP.NET的早期版本中,當訪問集合中的任何元素時,將觸發整個請求集合的請求驗證。 新的行為使不同的應用程式元件能夠更輕鬆地查看不同的請求數據,而不會觸發其他部分的請求驗證。

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>支援未經認證的要求

僅延遲請求驗證並不能解決選擇性繞過請求驗證的問題。 對"請求.Form_"論壇\_帖子"的調用仍觸發該特定請求值的請求驗證。 但是,您可能希望在不觸發驗證的情況下訪問此欄位,因為您希望允許該欄位中的標記。

為此,ASP.NET 4.5 現在支援對請求數據的未經驗證的訪問。 ASP.NET 4.5 在*HttpRequest*類中包括一個新的*未驗證*集合屬性。 此集合提供對請求數據的所有常見值(如*窗體*、*查詢字串**、Cookie*和*Url)* 的存取。

使用論壇示例,為了能夠讀取未經驗證的請求數據,首先需要將應用程式配置為使用新的請求驗證模式:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

然後,您可以使用*HTTPRequest.未驗證*的屬性讀取未驗證的表單值:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> 安全性 -*小心使用未經驗證的請求數據!* ASP.NET 4.5 添加了未經驗證的請求屬性和集合,以便您更輕鬆地訪問非常具體的未驗證請求數據。 但是,您仍必須對原始請求數據執行自定義驗證,以確保不會向使用者呈現危險文本。

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>AntiXSS 函式庫

由於 Microsoft AntiXSS 庫的普及,ASP.NET 4.5 現在包含該庫版本 4.0 的核心編碼例程式。

程式碼例設計由新*系統.Web.Security.AntiXs*命名空間中的*AntiXsEncoder*類型實現。 您可以通過調用類型中實現的任何靜態編碼方法直接使用*AntiXsEncoder*類型。 但是,使用新的反 XSS 例程的最簡單方法是將 ASP.NET 應用程式設定為預設使用*AntiXsEncoder*類。 此,從 Web.config 檔案加入以下屬性:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

當*編碼器類型*屬性設置為使用*AntiXsEncoder*類型時,ASP.NET中的所有輸出編碼將自動使用新的編碼例程。

這些是外部 AntiXSS 函式庫中已整合到 ASP.NET 4.5 中的部分:

- *Html 編碼* *,HtmlFormUrl 編碼*, 與*html 屬性編碼*
- *XmlAttributeEncode*和*XmlEncode*
- *網址Encode*與*網址Path 編碼*(新)
- *CsEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>支援 WebSocket 協定

WebSockets 協定是基於標準的網路協定,它定義了如何通過 HTTP 在用戶端和伺服器之間建立安全的即時雙向通信。 Microsoft 與 IETF 和 W3C 標準機構合作,説明定義該協定。 WebSockets 協定由任何用戶端(而不僅僅是瀏覽器)支援,Microsoft 在用戶端和行動作業系統上投入大量資源支援 WebSocket 協定。

WebSockets 協定使在用戶端和伺服器之間創建長時間運行的數據傳輸變得更加容易。 例如,編寫聊天應用程式要容易得多,因為您可以在用戶端和伺服器之間建立真正的長時間運行的連接。 您不必使用定期輪詢或 HTTP 長輪詢等解決方法來類比套接字的行為。

ASP.NET 4.5 和 IIS 8 都支援低級 WebSocket,使 ASP.NET 開發人員能夠使用託管 API 在 WebSocket 物件上異步讀取和寫入字串和二進位數據。 對於ASP.NET 4.5,有一個新的*System.Web.WebSockets*命名空間,其中包含用於使用 WebSockets 協定的類型。

瀏覽器客戶端透過建立 DOM WebSocket 物件來建立*WebSocket*連接,該物件指向 ASP.NET 應用程式中的網址,如以下範例所示:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

您可以使用任何類型的模組或處理程式在ASP.NET創建 WebSockets 終結點。 在前面的範例中,使用了 .ashx 檔,因為 .ashx 檔是創建處理程式的快速方法。

根據 WebSocket 協定,ASP.NET 應用程式透過指示請求應從 HTTP GET 請求升級到 WebSockets 請求來接受用戶端的 WebSockets 請求。 以下是範例：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

*AcceptWebSocketRequest 方法*接受函數委託,因為ASP.NET解除當前 HTTP 請求,然後將控制權傳輸到函數委託。 從概念上講,這種方法類似於您使用*System.Threading.Thread*的方式,在其中定義執行後台工作的線程啟動委託。

ASP.NET和用戶端成功完成 WebSocket 握手後,ASP.NET調用您的委託,WebSockets 應用程式開始運行。 以下代碼範例顯示了一個簡單的回聲應用程式,該應用程式在ASP.NET中使用內建 WebSocket 支援:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

.NET 4.5 中支援*await*關鍵字和基於異步任務的操作自然適合編寫 WebSockets 應用程式。 代碼示例顯示 WebSockets 請求完全非同步地在 ASP.NET 內部執行。 應用程式通過調用*await 套接字以非同步等待從用戶端發送消息。接收Async*。 同樣,您可以通過調用*await 套接字向客戶端發送非同步訊息。森步同步*。

在瀏覽器中,應用程式通過*onmessage*功能接收 WebSocket 消息。 要從瀏覽器傳送訊息,請呼叫*WebSocket* DOM 類型的*送出*方法,如以下範例所示:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

將來,我們可能會發佈此功能的更新,以抽象掉 WebSocket 應用程式在此版本中所需的一些低級編碼。

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>統合和縮製

捆綁允許您將單個 JavaScript 和 CSS 檔合併到可以視為單個檔的捆綁包中。 Min化透過刪除空白和其他不需要的字元來壓縮 JavaScript 和 CSS 檔。 這些功能與 Web 窗體、ASP.NET MVC 和網頁配合使用。

捆綁包是使用捆綁類或其子類之一的腳本捆綁包和樣式捆綁包創建的。 配置捆綁包的實例后,只需將其添加到全域捆綁收集實例,即可向傳入請求提供該捆綁包。 在預設範本中,捆綁配置在 Bundle Config 檔中執行。 此預設設定為範本使用的所有核心文本和 css 檔案建立捆綁套件。

通過使用幾個可能的説明方法之一,從視圖中引用捆綁包。 為了支援在調試與發佈模式下呈現捆綁包的不同標記,ScriptBundle 和 StyleBundle 類具有幫助器方法 Render。 在調試模式下,渲染將為捆綁包中的每個資源生成標記。 在發佈模式下,渲染將為整個捆綁包生成單個標記元素。 通過修改 Web.config 中編譯元素的調試屬性,可以在調試和發佈模式之間切換,如下所示:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

此外,可以直接通過 BundleTable 設定啟用或禁用優化。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

當檔捆綁時,它們首先按字母順序排序(它們在**解決方案資源管理器**中顯示的方式)。 然後組織它們,以便首先載入已知的庫及其自定義擴展(如 jQuery、MooTools 和 Dojo)。 例如,如上所述,捆綁腳本資料夾的最終順序為:

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a.js

CSS 檔也按字母順序排序,然後重新組織,以便重置.css 和規範化.css 在任何其他檔之前出現。 上面顯示的樣式資料夾捆綁的最終排序是:

1. 重置.css
2. 內容.css
3. 表單.css
4. globals.css
5. 選單.css
6. 樣式.css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>Web 託管的效能改進

.NET 框架 4.5 和 Windows 8 引入了可説明您為 Web 伺服器工作負載實現顯著性能提升的功能。 這包括減少(高達 35%)在啟動時間和使用ASP.NET的網站託管網站的記憶體佔用量中。

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>關鍵性能因素

理想情況下,所有網站都應處於活動狀態且處於記憶體中,以確保隨時對下一個請求做出快速回應。 可能影響網站回應能力的因素包括:

- 應用池回收后站點重新啟動所需的時間。 當網站程式集不再在記憶體中時,此時需要啟動網站的 Web 伺服器進程。 (平臺程式集仍在記憶體中,因為它們被其他網站使用。這種情況稱為「冷網站,暖框架啟動」或只是「冷網站啟動」。
- 網站佔用的內存量。 其術語是「每個網站記憶體消耗」或「非共用工作集」。

新的性能改進側重於這兩個因素。

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>對新效能功能的要求

新功能的要求可以分為以下幾類:

- 在 .NET 框架 4 上運行的改進。
- 需要 .NET 框架 4.5 但可在任何版本的 Windows 上運行的改進。
- 僅在 Windows 8 上運行 .NET 框架 4.5 時可用的改進。

性能隨您能夠啟用的每個改進級別而提高。

一些 .NET Framework 4.5 改進還利用了適用於其他方案的更廣泛的性能功能。

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>共用公共程式集

**要求**: .NET 框架 4 與視覺化工作室 11 開發人員預覽 SDK

伺服器上的不同網站通常使用相同的幫助器程式集(例如,來自初學者工具組或範例應用程式的程式集)。 每個網站在其 Bin 目錄中都有自己的程式集副本。 即使程式集的物件代碼相同,但它們是物理上獨立的程式集,因此在冷網站啟動期間必須單獨讀取每個程式集,並單獨保存在記憶體中。

新的實習功能解決了這種低效率,減少了 RAM 要求和載入時間。 使用允許 Windows 在檔案系統中保留每個程式集的單個副本,網站 Bin 資料夾中的各個程式集將替換為指向單個複本的符號連結。 如果單個網站需要程式集的不同版本,則符號連結將被程式集的新版本替換,並且只有該網站受到影響。

使用符號連結共用程式集需要一個名為 aspnet\_intern.exe 的新工具,該工具允許您創建和管理已處理程式集的存儲。 它是作為可視化工作室 11 開發人員預覽 SDK 的一部分提供的。 (但是,假定已安裝最新的[更新](https://support.microsoft.com/kb/2468871),它將在僅安裝 .NET 框架 4 的系統上工作。

為了確保所有符合條件的程式集都已暫留,您定期運行 aspnet\_intern.exe(例如,每週一次作為計劃任務)。 典型用途如下:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

要查看所有選項,運行沒有參數的工具。

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>使用多核 JIT 編譯,加快啟動速度

**要求**: .NET 框架 4.5

對於冷網站啟動,不僅必須從磁碟讀取程式集,而且必須編譯網站。 對於複雜的網站,這可能會增加明顯的延遲。 .NET Framework 4.5 中的一種新的通用技術通過在可用的處理器內核中擴展 JIT 編譯來減少這些延遲。 它通過使用在以前發佈網站期間收集的信息,盡可能早地這樣做。 此功能由[系統.運行時.配置檔優化.啟動配置檔](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx)方法實現。

默認情況下,使用多個內核進行 JIT 編譯 ASP.NET,因此您無需執行任何操作來利用此功能。 如果要關閉此功能,請在 Web.config 檔中進行以下設定:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>調整垃圾資源以最佳化記憶體

**要求**: .NET 框架 4.5

網站運行后,其使用垃圾回收器 (GC) 堆可能是其記憶體消耗的重要因素。 與任何垃圾回收器一樣,.NET框架 GC 在 CPU 時間(集合的頻率和重要性)和記憶體消耗(用於新、釋放或自由的物件的額外空間)之間進行權衡。 對於以前的版本,我們提供了有關如何配置 GC 以實現適當平衡的指導(例如,請參閱[ASP.NET 2.0/3.5 共享主機配置](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration))。

對於 .NET Framework 4.5,提供工作負載定義的配置設置,該設置支援以前建議的所有 GC 設置以及為每個網站工作集提供額外性能的新調優。

要啟用 GC 記憶體調優,請向 Windows_Microsoft.NET_Framework_v4.0.30319_aspnet.config 檔添加以下設置:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

(如果您熟悉之前對 aspnet.config 的更改指南,請注意此設置將替換舊設置,例如,無需設置 gcServer、gc併發等。您不必刪除舊設定。

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>為 Web 應用程式預取

**要求**: .NET 架構 4.5 在 Windows 8 上執行

對於多個版本,Windows 包含一種稱為[預取器](http://en.wikipedia.org/wiki/Prefetcher)的技術,可降低應用程式啟動的磁碟讀取成本。 由於冷啟動主要針對用戶端應用程式,因此此技術未包含在 Windows Server 中,該伺服器僅包含對伺服器至關重要的元件。 預取現已在最新版本的 Windows Server 中提供,它可以優化單個網站的啟動。

對於 Windows 伺服器,預設情況下未啟用預取器。 要啟用與設定高密度 Web 託管的預取器,請在命令列上執行以下命令集:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

然後,要將預取器與ASP.NET應用程式整合,請向 Web.config 檔案新增以下內容:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>強型別資料控制項

在 ASP.NET 4.5 中,Web 窗體包括一些用於處理數據的改進。 第一個改進是強類型數據控制。 對於早期版本的 ASP.NET 中的 Web 窗體控制項,使用*Eval*和資料繫式顯示資料繫結度值:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

對雙向資料繫結,請使用*連結 :*

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

在運行時,這些調用使用反射讀取指定成員的值,然後在標記中顯示結果。 此方法使數據與任意、未成形的數據綁定變得容易。

但是,像這樣的數據綁定表達式不支援諸如成員名稱的 IntelliSense、導航(如轉到定義)或對這些名稱的編譯時間檢查等功能。

為了解決此問題,ASP.NET 4.5 添加了聲明控制件綁定到的數據的數據類型的能力。 使用新的*ItemType*屬性執行此操作。 設定此屬性時,資料繫式的作用區中有兩個新的類型變數 *:Item*和*BindItem*。 由於變數是強類型,因此您可以獲得 Visual Studio 開發體驗的全部優勢。

對於雙向資料繫式,請使用*BindItem*變數:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

ASP.NET Web 窗體框架中支援數據綁定的大多數控制項都已更新以支援*ItemType*屬性。

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>模型繫結

模型綁定擴展了ASP.NET Web 窗體控件中的數據綁定,以便使用以代碼為中心的數據訪問。 它包含*了 ObjectDataSource*控制項和模型綁定中的概念ASP.NET MVC。

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>選擇資料

要將數據控制項配置為使用模型綁定來選擇資料,請將控制項的*SelectMethod*屬性設定為頁面代碼中的方法的名稱。 數據控件在頁面生命週期中的適當時間調用該方法,並自動綁定返回的數據。 無需顯式調用*DataBind*方法。

在下面的範例中 *,GridView*控制項組設定為使用名為*GetCategories*的方法 :

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

在頁面的代碼中創建*GetCategories*方法。 對於簡單的選擇操作,該方法不需要任何參數,並且應返回*IE50 或* *IQuery 物件*。 如果設置了新的*ItemType*屬性(啟用強類型數據綁定表達式,如前面在[強類型數據控件](#_Toc318097386)中所述),則應返回這些介面的泛型版本 - *&lt;&gt;IE5500t*或*IQuery&lt;&gt;T,T**參數匹配* *ItemType*屬性的類型(例如 *,IQuery&lt;類別&gt;*)。

下面的範例顯示了*GetCategories*方法的代碼。 本示例使用實體框架代碼第一模型與北風示例資料庫。 代碼確保查詢通過 *「包括」* 方法傳回每個類別的相關產品的詳細資訊。 (這可確保標記中的*樣本欄位*元素顯示每個類別中的產品計數,而無需[n+1 選擇](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem).)

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

當頁面執行時 *,GridView*控制檔會自動呼叫*GetCategories*方法,並使用設定的欄位呈現傳回的資料:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

由於選擇方法返回*IQuery 物件*,因此*GridView*控件可以在執行查詢之前進一步操作查詢。 例如 *,GridView*控件可以在執行返回*的 IQuery 物件*之前將用於排序和分頁的查詢表達式添加到返回的 IQuery 物件,以便這些操作由基礎 LINQ 提供程式執行。 在這種情況下,實體框架將確保在資料庫中執行這些操作。

下面的範例顯示已修改的*GridView*控制項以允許排序和分頁:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

現在,當頁面運行時,控制項可以確保只顯示當前資料頁,並且數據按所選列排序:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

要篩選返回的數據,必須將參數添加到選擇方法。 這些參數將在執行時由模型綁定填充,您可以在返回數據之前使用它們來更改查詢。

例如,假設您要通過在查詢字串中輸入關鍵字來允許使用者篩選產品。 您可以將參數加入方法並更新代碼以使用參數值:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

如果為*關鍵字*提供了值,然後返回查詢結果,則此代碼包括*Where*表達式。

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>價值提供者

前面的範例沒有具體說明*關鍵字*參數的值來自何處。 要指示此資訊,可以使用參數屬性。 在此範例中,可以使用*System.Web.Model 綁定*命名空間中的*QueryStringattribute*類:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

這指示模型綁定嘗試在運行時將值從查詢字串綁定到*關鍵字*參數。 (這可能涉及執行類型轉換,儘管在這種情況下不執行。如果無法提供值且類型不可為空,則引發異常。

這些方法的值源稱為值提供程式,指示要使用的值提供程式的參數屬性稱為值提供程式屬性。 Web 表單組會包括 Web 窗體應用程式中所有典型使用者輸入來源的值提供程式和相應屬性,例如查詢字串、Cookie、窗體值、控制件、檢視狀態、工作階段狀態和設定檔屬性。 您還可以編寫自定義值提供程式。

預設情況下,參數名稱用作在值提供程式集合中查找值的鍵。 在此示例中,代碼將查找名為關鍵字的查詢字串值(例如,*/default.aspx?關鍵字_chef)。 可以通過將自定義鍵作為參數傳遞給參數屬性來指定它。 例如,要使用名為 q 的查詢字串變數的值,可以執行此操作:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

如果此方法位於頁面的代碼中,使用者可以透過使用查詢字串傳遞關鍵字來篩選結果:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

模型繫結完成許多工作,否則您必須手動編寫代碼:讀取值、檢查空值、嘗試將其轉換為適當的類型、檢查轉換是否成功,最後使用查詢中的值。 模型綁定導致的代碼少得多,並且能夠在整個應用程式中重用該功能。

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>依控制項的值篩選

假設您要擴展示例,以便使用者從下拉清單中選擇篩選器值。 將以下下拉清單加入到標記中,並將其設定為使用*SelectMethod*屬性從其他方法取得其資料:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

通常,您還會向*GridView*控制件添加*EmptyDataTemplate*元素,以便在找不到符合的產品時,控制項將顯示一條訊息:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

在頁面代碼中,為下拉清單添加新的 select 方法:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

最後,更新*GetProducts*選擇方法,從下拉清單中獲取包含所選類別 ID 的新參數:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

現在,當頁面運行時,用戶可以從下拉清單中選擇一個類別,並且*GridView*控件將自動重新綁定以顯示篩選的資料。 這是可能的,因為模型綁定跟蹤選定方法的參數值,並檢測任何參數值在回退後是否已更改。 如果是這樣,模型綁定強制關聯的數據控件重新綁定到數據。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML 編碼資料繫結表示式

現在,您可以對資料綁定表達式的結果進行 HTML 編碼。 新增冒號(:)標記資料繫結表示式的&lt;%# 前置字尾的尾尾:

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>不顯眼的驗證

現在,您可以將內建驗證器控制項配置為對用戶端驗證邏輯使用不顯眼的 JavaScript。 這大大減少了頁面標記中內聯呈現的 JavaScript 量,並減小了整個頁面大小。 您可以透過以下任何方式為驗證器控制項設定不顯眼的 JavaScript:

- 以從 Web.config 檔案*&lt;中&gt;的應用程式設定*元素新增以下設定,從而全域: 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- 通過將靜態*System.Web.UI.驗證設置.無顯眼驗證模式*屬性設置為 *"無顯眼驗證模式.WebForms"(* 通常在 Global.asax 檔中*的應用程式\_啟動*方法中),在全球範圍內。
- 使用頁面類別的新 *「不顯眼驗證模式」* 屬性設定為 *「不顯眼驗證模式.WebForms」 ,* 單獨為*頁面*。

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5 更新

為了利用 HTML5 的新功能,對 Web 窗體伺服器控制件進行了一些改進:

- *TextBox*控制項的*TextMode*屬性已更新以支援新的 HTML5 輸入類型,如*電子郵件*、*日期時間*等。
- *FileUpload*控制項現在支援從支援此 HTML5 功能的瀏覽器上載多個檔。
- 驗證器控制項支援驗證 HTML5 輸入元素。
- 具有表示 URL 屬性的新 HTML5 元素現在支援 runat_"server"。 因此,您可以在 URL 路徑中使用 ASP.NET 約定,例如 * 運算符來表示&lt;應用程式根(例如, 視頻 runat_" 伺服器 「 src_&gt;」 my Video.wmv"
- *UpdatePanel*控制件已修復,以支援過帳 HTML5 輸入欄位。

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 測試版現在包含在 Visual Studio 11 測試版中。 ASP.NET MVC 是利用模型檢視控制器 (MVC) 模式開發高度可測試和可維護的 Web 應用程式的框架。 ASP.NET MVC 4 使建置行動 Web 應用程式變得容易,並且包括 ASP.NET Web API,這有助於建構可覆寫任何設備的 HTTP 服務。 有關詳細資訊,請參閱 ASP.NET [MVC 4 發行說明](mvc4-release-notes.md)。

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET Web Pages 2

新功能包括以下內容:

- 新建和更新的網站範本。
- 使用*驗證*幫助程式添加伺服器端和客戶端驗證。
- 使用資產管理註冊腳本的功能。
- 使用 OAuth 和 OpenID 啟用來自 Facebook 和其他網站的登錄。
- 使用地圖說明器新增*地圖*。
- 並排運行網頁應用程式。
- 移動設備的呈現頁面。

有關這些功能和整頁代碼範例的詳細資訊,請參閱[網頁 2 Beta 中的頂部功能](https://go.microsoft.com/fwlink/?LinkID=227824)。

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>視覺化 Web 開發人員 11 測試版

本節提供有關可視化 Web 開發人員 11 Beta 和可視化工作室 2012 版本候選版中 Web 開發改進的資訊。

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Visual Studio 2010 和 Visual Studio 2012 版本候選版本之間的項目共享(專案相容性)

在 Visual Studio 2012 發佈候選版之前,在較新版本的 Visual Studio 中打開現有項目啟動了轉換嚮導。 這迫使專案的內容(資產)和解決方案升級到不向後相容的新格式。 因此,轉換後,您無法在舊版本的 Visual Studio 中打開專案。

許多客戶告訴我們,這不是正確的方法。 在 Visual Studio 11 Beta 中,我們現在支援與 Visual Studio 2010 SP1 共用專案和解決方案。 這意味著,如果您在 Visual Studio 2012 版本候選版中打開 2010 年專案,您仍然可以在 Visual Studio 2010 SP1 中打開該專案。

> [!NOTE]
> 幾種類型的專案不能在 Visual Studio 2010 SP1 和 Visual Studio 2012 版本候選版之間共用。 其中包括一些較舊的專案(如ASP.NET MVC 2 專案)或用於特殊目的的專案(如安裝程式專案)。

首次在 Visual Studio 11 Beta 開啟 Visual Studio 2010 SP1 Web 專案時,以下屬性將新增到專案檔中:

- 檔案升級標誌
- 升級備份位置
- 舊工具版本
- VisualStudioVersion
- VSToolsPath

檔升級標誌、升級備份位置和舊工具版本由升級專案檔的過程使用。 它們對在 Visual Studio 2010 中使用該專案沒有任何影響。

VisualStudioVersion 是 MSBuild 4.5 使用的新屬性,用於指示當前專案的 Visual Studio 版本。 由於此屬性在 MSBuild 4.0 中不存在(Visual Studio 2010 SP1 使用的 MSBuild 版本),因此我們將預設值注入到專案檔中。

VSToolsPath 屬性用於確定要從 MSBuild 擴展器Path32 設置表示的路徑導入的正確 .target 檔。

還有一些與導入元素相關的更改。 為了支援兩個版本的 Visual Studio 之間的相容性,需要進行這些更改。

> [!NOTE]
> 如果 Visual Studio 2010 SP1 和 Visual Studio 11 Beta 在兩台\_不同電腦上共用專案,並且該專案在應用 數據資料夾中包含本地資料庫,則必須確保資料庫使用的 SQL Server 版本安裝在兩台電腦上。

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>ASP.NET 4.5 網站樣本中的設定變更

使用 Visual Studio 2012 版本候選版中的網站樣本建立的網站的預設*Web.config*檔進行了以下變更:

- 在元素`<httpRuntime>`中,`encoderType`屬性現在預設設定為使用添加到ASP.NET的 AntiXSS 類型。 有關詳細資訊,請參閱[AntiXSS 函式庫](#_Toc318097382)。
- 此外,在`<httpRuntime>`元素中,`requestValidationMode`屬性設置為"4.5"。 這意味著默認情況下,請求驗證配置為使用延遲("延遲")驗證。 有關詳細資訊,請參閱[新ASP.NET請求驗證功能](#_Toc318097379)。
- 節`<modules>`元素`<system.webServer>`不包含屬性`runAllManagedModulesForAllRequests`。 (其預設值為 false。這意味著,如果您使用的 IIS 7 版本尚未更新到 SP1,則新網站中的路由可能有問題。 有關詳細資訊,請參閱[IIS 7 中的本機支援,瞭解 ASP.NET 路由](#Native_Support_In_IIS7_For_ASPNET_Routine)。

這些更改不會影響現有應用程式。 但是,它們可能表示現有網站與您使用新範本為 ASP.NET 4.5 創建的新網站的行為差異。

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>IIS 7 中用於ASP.NET路由的本機支援

這不是對ASP.NET的更改,而是新網站項目的範本更改,如果您正在使用未應用SP1更新的IIS7版本,可能會影響您。

在ASP.NET中,您可以將以下設定設定新增到應用程式中,以支援路由:

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

當**RunAll管理ModuleAll 請求**為`http://mysite/myapp/home`true 時, 即使 URL 上沒有 *.aspx、.mvc*或類似擴展,也可以 *.mvc*將類似 URL 轉到 ASP.NET。

對 IIS 7 所做的更新使**runAll管理模組所有請求**設置變得不必要,並支援本機路由ASP.NET路由。 (有關更新的資訊,請參閱 Microsoft 支援文章[一個可用更新,使某些 IIS 7.0 或 IIS 7.5 處理程式能夠處理 URL 未以句點結尾的請求](https://support.microsoft.com/kb/980368)。

如果您的網站在IIS 7上運行,並且IIS已更新,則無需將**執行All管理模組全部請求**設置為 true。 事實上,不建議將其設置為 true,因為它會增加不必要的處理開銷。 當此設置為 true 時,所有請求(包括 *.htm、.jpg*和其他靜態檔的請求)也會通過請求管道 *.jpg*ASP.NET。

如果使用 Visual Studio 2012 RC 中提供的範本建立新 ASP.NET 4.5 網站,則網站的配置不包括**RunAll 管理模組全部請求**設置。 這意味著默認情況下,該設置為 false。

如果隨後在 Windows 7 上運行網站而不安裝 SP1,則 IIS 7 將不包含所需的更新。 因此,路由將不起作用,您將看到錯誤。 如果路由不起作用,可以執行以下任一操作:

- 將 Windows 7 更新為 SP1,這將將更新添加到 IIS 7。
- 安裝前面列出的 Microsoft 支援文章中所述的更新。
- 將**執行All管理模組所有請求**設置為 true,在該網站的 Web.config 檔中。 請注意,這將為請求增加一些開銷。

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML 編輯器

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>智慧任務

在"設計"檢視中,伺服器控制項的複雜屬性通常具有關聯的對話框和嚮導,以便輕鬆設置它們。 例如,可以使用特殊的對話框向*中繼器*控制項添加資料源或向*GridView*控制件添加列。

但是,針對複雜屬性的這種類型的 UI 説明在源視圖中不可用。 因此,Visual Studio 11 引入了源視圖的智慧任務。 智慧任務是 C# 和 Visual Basic 編輯器中常用功能的上下文感知快捷方式。

對於ASP.NET Web 表單控制項,當插入點位於元素內部時,智慧任務在伺服器標記上顯示為一個小字形:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

按下字形或按 CTRL+時,智慧任務將展開。 (點),就像代碼編輯器一樣。 然後,它顯示類似於"設計"視圖中的智慧任務的快捷方式。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

例如,上圖中的智慧任務顯示了 GridView 任務選項。 如果選擇「編輯列」,將顯示以下對話框:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

填寫對話框將設置可在「設計」檢視中設置的相同屬性。 按下「確定」時,控制項的標記將使用新設定更新:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>WAI-ARIA 支援

編寫可訪問的網站變得越來越重要。 [WAI-ARIA 輔助功能標準](http://www.w3.org/WAI/intro/aria)定義了開發人員應如何編寫可訪問的網站。 此標準現在完全支援在視覺工作室。

例如,*角色*屬性現在具有完整的 IntelliSense:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

WAI-ARIA 標準還引入了以*aria-* 預先碼的屬性,這些屬性允許您向 HTML5 文件添加語義。 Visual Studio 還完全支援這些*aria 屬性*:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>新的 HTML5 碼段

為了使編寫常用的 HTML5 標籤更快、更容易,Visual Studio 包含許多代碼段。 例如視訊片段:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

要呼叫代碼段,請在 IntelliSense 中選擇元素時按 Tab 兩次:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

這將生成可以自定義的代碼段。

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>擷取使用者控制項

在大型網頁中,最好將單個片段移動到使用者控件中。 這種重構形式有助於提高頁面的可讀性,並可以簡化頁面結構。

為了簡化此功能,當您在「源」檢視中編輯「Web 窗體」頁時,您現在可以選擇頁面中的文字,右鍵按一下它,然後選擇「提取到使用者控制」:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>屬性中片段的 IntelliSense

Visual Studio 始終為任何頁面或控制項中的伺服器端代碼塊提供 IntelliSense。 現在,Visual Studio 還包括用於 HTML 屬性中的代碼塊的 IntelliSense。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

這樣可以更輕鬆地建立資料繫式:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>重新命名開啟或關閉標籤時自動重新命名符合標記

如果重新命名 HTML 元素(例如,將*div*標記更改為*標頭*標記),相應的打開或關閉標記也會即時更改。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

這有助於避免忘記更改結束標記或更改錯誤標記的錯誤。

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>事件處理程式產生

Visual Studio 現在包括在「源」檢視中的功能,以説明您編寫事件處理程式並手動綁定它們。 如果要在原始檢視中編輯事件名稱,IntelliSense 將顯示&lt;「建立新事件&gt;」,這將在具有正確簽名的頁面代碼中建立事件處理程式:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

預設情況下,事件處理程式將使用控制項的 ID 來表示事件處理方法的名稱:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

生成的事件處理程式將如下所示(在本例中,在 C#中):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>智慧縮排

當您在空的 HTML 元素內按 Enter 時,編輯器將插入點放在正確的位置:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

如果在此位置按 Enter,則關閉標記將向下移動並縮進以匹配打開標記。 插入點也縮進:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>自動減少敘述完成

Visual Studio 中的 IntelliSense 清單現在根據您鍵入的內容進行篩選,以便僅顯示相關選項:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

IntelliSense 還會根據 IntelliSense 清單中單一單字的標題大小寫進行篩選。 例如,如果您鍵入「dl」,則將顯示 dl 和 asp:DataList:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

此功能使獲取已知元素的語句完成速度更快。

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript 編輯器

Visual Studio 2012 版本候選版中的 JAvaScript 編輯器是全新的,它極大地改善了在可視化工作室中使用 JAVAScript 的體驗。

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>程式碼大綱

現在會自動為所有函數創建大綱區域,從而可以摺疊與當前焦點無關的檔部分。

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>括號對稱

將插入點放在開括弧或關閉大括弧上時,編輯器將突出顯示匹配的支撐。

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>移至定義

"轉到定義"命令允許您跳轉到函數或變數的源。

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAScript5 支援

編輯器支援 ECMAScript5 中的新語法和 API,ECMAScript5 是描述 JavaScript 語言的標準的最新版本。

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM 感知

DOM API 的智慧感知得到了改進,支援許多新的 HTML5 API,包括*查詢選擇器*、DOM 儲存、跨文件訊息傳遞和*畫佈*。 DOM IntelliSense 現在由單個簡單的 JavaScript 檔案驅動,而不是由本機類型庫定義驅動。 這使得擴展或更換變得容易。

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC 簽署重載

現在可以使用新的*&lt;&gt;簽名*元素聲明詳細的 IntelliSense 註解,以便單獨重載 JavaScript 函數,如以下範例所示:

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>隱含參考

現在,您可以將 JavaScript 檔添加到一個中心清單中,該清單將隱式包含在任何給定的 JavaScript 檔或阻止引用的檔案清單中,這意味著您將獲得 IntelliSense 的內容。 例如,您可以將 jQuery 檔添加到檔案的中心清單中,並且無論是否已顯式引用它(使用&lt;// /&gt;引用 /), 您都將在任何 JavaScript 檔案塊中獲取 jQuery 函數的 IntelliSense。

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS 編輯器

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>自動減少敘述完成

CSS 的 IntelliSense 清單現在根據選取架構支援的 CSS 屬性和值進行篩選。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense 還支援標題案例搜尋:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>階層式縮排

CSS 編輯器使用縮進來顯示分層規則,這為您提供了級聯規則邏輯組織方式的概述。 在下面的範例中,選擇器#list是列表的級聯子級,因此縮進。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

下面的範例顯示了更複雜的繼承:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

規則的縮進由其父規則決定。 預設情況下啟用分層縮進,但您可以關閉「選項」對話框(選單欄中的工具、選項):

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS 駭客支援

對數百個真實 CSS 檔的分析表明,CSS 駭客非常常見,現在 Visual Studio 支援使用最廣泛的駭客。 這種支援包括IntelliSense和驗證的明星\*( )\_和下 劃線 ( ) 屬性駭客:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

還支援典型的選擇器駭客,以便即使應用分層縮進,也能保持分層縮進。 典型的選擇器駭客用於目標網際網路瀏覽器7是準備一個選擇器與*\*:第一個孩子 + html*。 使用該規則將保持分層縮排:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>供應商指定的架構(-moz-, -webkit)

CSS3 引入了許多由不同瀏覽器在不同時間實現的屬性。 這以前迫使開發人員使用特定於供應商的語法為特定瀏覽器編寫代碼。 這些特定於瀏覽器的屬性現在包含在 IntelliSense 中。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>評論和非評論支援

現在,您可以使用代碼編輯器中使用的快捷方式(Ctrl_K、C註釋和 Ctrl_K,您取消註釋)對 CSS 規則進行註釋和取消註解。

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>Color picker

在早期版本的 Visual Studio 中,與顏色相關的屬性的 IntelliSense 由命名顏色值的下拉列表組成。 該清單已被全功能顏色選取器替換。

輸入顏色值時,顏色選取器將自動顯示,並顯示以前使用的顏色清單,後跟預設調色板。 您可以使用滑鼠或鍵盤選擇顏色。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

該清單可以展開為完整的顏色選取器。 選取器允許您在移動不協調性滑動時自動將任何顏色轉換為 RGBA 來控制 Alpha 通道:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>程式碼片段

CSS 編輯器中的代碼段使創建跨瀏覽器樣式變得更加簡單和快速。 許多需要特定於瀏覽器設置的 CSS3 屬性現已滾入代碼段。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS 程式碼段透過鍵入在符號 (#) 中顯示 IntelliSense 清單來支援進階方案(如 CSS3 媒體查詢)。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

當您選擇@media值並按選項卡時,CSS 編輯器將插入以下代碼段:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

與代碼代碼段一樣,您可以創建自己的 CSS 代碼段。

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>自訂區域

命名代碼區域(已在代碼編輯器中提供)現在可用於 CSS 編輯。 這使您可以輕鬆對相關的樣式塊進行分組。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

當區域折疊時,將顯示區域的名稱:

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Page Inspector

頁面檢查器是一種工具,用於在 Visual Studio IDE 中呈現網頁(HTML、Web 窗體、ASP.NET MVC 或網頁),並允許您檢查原始碼和生成的輸出。 對於ASP.NET頁,頁面檢查器允許您確定哪些伺服器端代碼已生成呈現到瀏覽器的 HTML 標記。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

有關頁面檢查器的詳細資訊,請參閱以下教程:

- 在[mVC 中使用 ASP.NET](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)網頁檢查器
- 在[ASP.NET Web 窗體](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)中使用網頁檢查器

<a id="_Toc318097425"></a>
### <a name="publishing"></a>發佈

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>發佈設定檔

在 Visual Studio 2010 中,Web 應用程式專案的發佈資訊不存儲在版本控制中,並且不設計為與他人共用。 在 Visual Studio 2012 版本候選版中,發佈配置檔的格式已更改。 它已成為團隊工件,現在很容易從基於 MSBuild 的生成中利用。 生成配置資訊位於"發佈"對話框中,以便在發佈之前輕鬆切換生成配置。

發佈設定檔儲存在「發布設定檔」資料夾中。 資料夾的位置取決於您使用的程式設計語言:

- C#:屬性\發行設定檔
- 視覺化基礎知識:我的項目\發行設定檔

每個配置檔都是一個 MSBuild 檔。 在發佈期間,此檔將導入到專案的 MSBuild 檔中。 在 Visual Studio 2010 中,如果要對發佈或包過程進行更改,則必須將自定義項放在名為**ProjectName**.wpp.target 的檔中。 這仍然受支援,但現在可以將自定義項放在發佈配置檔本身中。 這樣,自定義將僅用於該配置檔。

您現在還可以利用 MSBuild 的發佈配置檔。 為此,在產生專案時使用以下命令:

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

project.csproj 值是專案的路徑,而配置檔名稱是要發布的設定檔的名稱。 或者,您可以傳入發佈配置檔的完整路徑,而不是傳遞*PublishProfile*屬性的設定檔名稱。

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET 預寫和合併

對於 Web 應用程式專案,Visual Studio 2012 發佈候選版在「包/發佈 Web 屬性」頁上添加了一個選項,允許您在發佈或打包專案時預編譯和合併網站的內容。 要查看這些選項,請右鍵單擊解決方案資源管理器中的項目,選擇"屬性",然後選擇"包/發佈 Web 屬性頁"。 下圖顯示了發佈選項之前預編譯此應用程式。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

選擇此選項後,每當發佈或打包 Web 應用程式時,Visual Studio 都會預編譯應用程式。 如果要控制網站的預編譯方式或程式集的合併方式,請單擊「高級」按鈕以配置這些選項。

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

用於在 Visual Studio 中測試 Web 專案的預設 Web 伺服器現在是 IIS Express。 可視化工作室開發伺服器仍然是開發過程中本地 Web 伺服器的選項,但 IIS Express 現在是推薦的伺服器。 在 Visual Studio 11 Beta 中使用 IIS Express 的經驗與在 Visual Studio 2010 SP1 中使用它非常相似。

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>免責聲明

這是一份初稿，內容在本文所述的軟體於正式商業發行前都可能有所更動。

本文件所含的資訊代表 Microsoft Corporation 在發行日當下對問題的看法。 由於 Microsoft 必須因應不斷變化的市場狀況，因此不應將此解讀為 Microsoft 方面所作出的承諾，且 Microsoft 也無法保證在發行日之後所提出任何資訊的正確性。

本技術白皮書僅供參考。 MICROSOFT 對本文件中的資訊不提供任何明示、暗示或法定擔保。

遵守所有適用之著作權法係使用者的責任。 在不限制任何依著作權本得享有之權利，未經 Microsoft Corporation 書面許可， 貴用戶不得為任何目的使用任何形式或方法 (電子形式、機械形式、影印、記錄或其他方式) 複製或傳送本文件的任何部份，也不得將本文件的任何部份儲存或放入檢索系統 (a retrieval system)。

在本文件所提述之內容中，可能包括 Microsoft 的專利、申請專利案件、商標、著作權，或其他智慧財產權等。 除非於 Microsoft 提出的任何書面授權條約中明確規定者外，提供本文件並不表示賦予台端上述專利、商標、著作權或其他智慧財產權等之任何授權。

除非另有說明,否則此處描述的示例公司、組織、產品、域名、電子郵件地址、徽標、人員、地點和事件均屬虛構,且無意或不應推斷與任何真實的公司、組織、產品、功能變數名稱、電子郵寄地址、徽標、人員、地點或事件有任何關聯。

(C) 2012 Microsoft Corporation. 著作權所有，並保留一切權利。

Microsoft 和 Windows 是 Microsoft Corporation 在美國及/或其他國家/地區的註冊商標或商標。

本文件中所提實際公司和產品，可能為各所有人所有之商標。
