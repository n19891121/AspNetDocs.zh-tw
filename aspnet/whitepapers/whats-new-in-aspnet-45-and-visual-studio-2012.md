---
uid: whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
title: ASP.NET 4.5 和 Visual Studio 2012 的新功能 |Microsoft Docs
author: rick-anderson
description: 本檔說明 ASP.NET 4.5 中引進的新功能和增強功能。 此外，也會說明針對網頁程式開發所做的改進 .。。
ms.author: riande
ms.date: 02/29/2012
ms.assetid: ba1fabb4-31a3-4ebf-8327-41a6bbba6eaf
msc.legacyurl: /whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012
msc.type: content
ms.openlocfilehash: 32fbf7c25b00f3f0796c4c3fdd38ca2a86c89199
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345410"
---
# <a name="whats-new-in-aspnet-45-and-visual-studio-2012"></a>ASP.NET 4.5 與 Visual Studio 2012 的新功能

> 本檔說明 ASP.NET 4.5 中引進的新功能和增強功能。 此外也說明在 Visual Studio 2012 中進行 web 程式開發的改進。 這份檔最初是在2012年2月29日發佈。

- [ASP.NET Core 執行時間和架構](#_Toc318097372)

    - [非同步讀取和寫入 HTTP 要求和回應](#_Toc318097373)
    - [HttpRequest 處理的改進](#_Toc318097374)
    - [以非同步方式清除回應](#_Toc318097375)
    - [支援 *await* 和以 *工作為基礎的非同步*模組和處理常式](#_Toc318097376)
    - [非同步 HTTP 模組](#_Toc318097377)
    - [非同步 HTTP 處理常式](#_Toc318097378)
    - [新的 ASP.NET 要求驗證功能](#_Toc318097379)
    - [延遲 ( 「延遲」 ) 要求驗證](#_Toc318097380)
    - [未經驗證要求的支援](#_Toc318097381)
    - [AntiXSS 程式庫](#_Toc318097382)
    - [Websocket 通訊協定的支援](#_Toc318097383)
    - [統合和縮製](#_Toc318097384)
    - [Web 裝載的效能改進](#_Toc_perf)

        - [關鍵效能因素](#_Toc_perf_1)
        - [新效能功能的需求](#_Toc_perf_2)
        - [共用萬用群組件](#_Toc_perf_3)
        - [使用多重核心 JIT 編譯以加快啟動速度](#_Toc_perf_4)
        - [調整垃圾收集以針對記憶體優化](#_Toc_perf_5)
        - [針對 web 應用程式預先提取](#_Toc_perf_6)
- [ASP.NET Web Forms](#_Toc318097385)

    - [強型別資料控制項](#_Toc318097386)
    - [模型系結](#_Toc318097387)

        - [選取資料](#_Toc318097388)
        - [值提供者](#_Toc318097389)
        - [依控制項的值篩選](#_Toc318097390)
    - [HTML 編碼 Data-Binding 運算式](#_Toc318097391)
    - [不顯眼的驗證](#_Toc318097392)
    - [HTML5 更新](#_Toc318097393)
- [ASP.NET MVC 4](#_Toc318097394)
- [ASP.NET Web Pages 2](#_Toc318097395)
- [Visual Studio 2012 候選版](#_Toc318097396)

    - [Visual Studio 2010 與 Visual Studio 2012 候選版之間的專案共用 (專案相容性) ](#project-compatibility)
    - [ASP.NET 4.5 網站範本中的設定變更](#Configuration_Changes_In_ASPNET45_Website_Templates)
    - [適用于 ASP.NET 路由的 IIS 7 原生支援](#Native_Support_In_IIS7_For_ASPNET_Routine)
    - [HTML 編輯器](#_Toc318097397)

        - [智慧型工作](#_Toc318097398)
        - [WAI-ARIA 支援](#_Toc318097399)
        - [新的 HTML5 程式碼片段](#_Toc318097400)
        - [解壓縮至使用者控制項](#_Toc318097401)
        - [在屬性中區塊程式碼的 IntelliSense](#_Toc318097402)
        - [當您重新命名開頭或結束記號時，自動重新命名相符的標記](#_Toc318097403)
        - [產生事件處理常式](#_Toc318097404)
        - [智慧縮排](#_Toc318097405)
        - [自動減少語句完成](#_Toc318097406)
    - [JavaScript 編輯器](#_Toc318097407)

        - [程式碼大綱](#_Toc318097408)
        - [括號對稱](#_Toc318097409)
        - [移至定義](#_Toc318097410)
        - [ECMAScript5 支援](#_Toc318097411)
        - [DOM IntelliSense](#_Toc318097412)
        - [VSDOC 簽章多載](#_Toc318097413)
        - [隱含參考](#_Toc318097414)
    - [CSS 編輯器](#_Toc318097415)

        - [自動減少語句完成](#_Toc318097416)
        - [階層式縮排。](#_Toc318097417)
        - [CSS 的駭客支援](#_Toc318097418)
        - [廠商特定架構 (-moz-,-webkit) ](#_Toc318097419)
        - [批註和取消批註支援](#_Toc318097420)
        - [色彩選擇器](#_Toc318097421)
        - [程式碼片段](#_Toc318097422)
        - [自訂區域](#_Toc318097423)
    - [Page Inspector](#_Toc318097424)
    - [發佈](#_Toc318097425)

        - [發佈設定檔](#_Toc318097426)
        - [ASP.NET 先行編譯和合併](#_Toc318097427)
- [IIS Express](#_Toc318097428)
- [免責聲明](#_Toc318097429)

<a id="_Toc318097372"></a>
## <a name="aspnet-core-runtime-and-framework"></a>ASP.NET Core 執行時間和架構

<a id="_Toc318097373"></a>
### <a name="asynchronously-reading-and-writing-http-requests-and-responses"></a>非同步讀取和寫入 HTTP 要求和回應

ASP.NET 4 引進了使用 *HttpRequest GetBufferlessInputStream* 方法將 HTTP 要求實體讀取為數據流的功能。 這個方法提供對要求實體的串流存取。 不過，它會以同步方式執行，這會在要求的持續時間內系結執行緒。

ASP.NET 4.5 支援以非同步方式讀取 HTTP 要求實體上的資料流程，以及非同步排清的能力。 ASP.NET 4.5 也可讓您對 HTTP 要求實體進行雙重緩衝，讓您更輕鬆地與下游的 HTTP 處理常式（例如 .aspx 頁面處理常式和 ASP.NET MVC 控制器）整合。

<a id="_Toc318097374"></a>
#### <a name="improvements-to-httprequest-handling"></a>HttpRequest 處理的改進

ASP.NET 4.5 從 HttpRequest 傳回的資料流程參考 *。 GetBufferlessInputStream* 支援同步和非同步讀取方法。 從*GetBufferlessInputStream*傳回的*資料流程*物件現在會同時執行 BeginRead 和 EndRead 方法。 非同步 *資料流程* 方法可讓您以區塊方式非同步讀取要求實體，而 ASP.NET 會在非同步讀取迴圈的每個反復專案之間釋放目前的執行緒。

ASP.NET 4.5 也加入了以緩衝方式讀取要求實體的隨附方法： *HttpRequest. GetBufferedInputStream*。 這個新的多載運作方式類似 *GetBufferlessInputStream*，同時支援同步和非同步讀取。 不過，在讀取時， *GetBufferedInputStream* 也會將實體位元組複製到 ASP.NET 內部緩衝區，讓下游模組和處理常式仍然可以存取要求實體。 例如，如果管線中的某些上游程式碼已經使用 *GetBufferedInputStream*讀取要求實體，您仍然可以使用 *HttpRequest* 或 *HttpRequest*檔案。 這可讓您對要求執行非同步處理 (例如，將大型檔案上傳至資料庫) ，但之後仍會執行 .aspx 頁面和 MVC ASP.NET 控制器。

<a id="_Toc318097375"></a>
#### <a name="asynchronously-flushing-a-response"></a>以非同步方式清除回應

將回應傳送至 HTTP 用戶端可能需要相當長的時間，因為用戶端遠離或具有低頻寬連接。 一般來說，ASP.NET 會緩衝應用程式所建立的回應位元組。 然後，ASP.NET 會在處理要求時，執行一次累計緩衝區的傳送作業。

如果緩衝的回應很大 (例如，將大型檔案串流至用戶端) ，您必須定期呼叫 *HttpResponse* ，以將緩衝的輸出傳送至用戶端，並讓記憶體使用量維持在控制之下。 不過，因為 *Flush* 是同步呼叫，所以反復呼叫 *flush* 仍會在可能長時間執行的要求期間，耗用執行緒。

ASP.NET 4.5 新增了使用*HttpResponse*類別的*BeginFlush*和*EndFlush*方法，以非同步方式執行清除的支援。 您可以使用這些方法來建立異步模組和非同步處理常式，以累加方式將資料傳送至用戶端，而不需要佔用作業系統執行緒。 在 *BeginFlush* 與 *EndFlush* 呼叫之間，ASP.NET 會釋放目前的執行緒。 這可大幅減少為了支援長時間執行的 HTTP 下載所需的作用中線程總數。

<a id="_Toc318097376"></a>
### <a name="support-for-await-and-task---based-asynchronous-modules-and-handlers"></a>支援 *await* 和以 *工作為基礎的非同步* 模組和處理常式

.NET Framework 4 引進了一種非同步程式設計概念，稱為「工作」（ *task*）。 工作會以*工作命名空間*中*的工作類型*和相關類型來表示。 .NET Framework 4.5 以編譯器增強功能為基礎來建立*工作物件。* 在 .NET Framework 4.5 中，編譯器支援兩個新的關鍵字： *await* 和 *async*。 *Await*關鍵字是語法速記，表示某段程式碼應該以非同步方式等候其他部分的程式碼。 *Async*關鍵字代表一個提示，可讓您用來將方法標示為以工作為基礎的非同步方法。

*Await*、 *async*和*Task*物件的組合可讓您更輕鬆地在 .net 4.5 中撰寫非同步程式碼。 ASP.NET 4.5 以新的 Api 支援這些簡化，可讓您使用新的編譯器增強功能來撰寫非同步 HTTP 模組和非同步 HTTP 處理常式。

<a id="_Toc318097377"></a>
#### <a name="asynchronous-http-modules"></a>非同步 HTTP 模組

假設您想要在傳回 *Task* 物件的方法內執行非同步工作。 下列程式碼範例會定義非同步呼叫以下載 Microsoft 首頁的非同步方法。 請注意在方法簽章中使用*async*關鍵字和*DownloadStringTaskAsync*的*await*呼叫。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample1.cs)]

這就是您必須撰寫的，.NET Framework 會在等候下載完成時，自動處理呼叫堆疊的回溯，以及在下載完成後自動還原呼叫堆疊。

現在假設您想要在非同步 ASP.NET HTTP 模組中使用這個非同步方法。 ASP.NET 4.5 包含 helper 方法 (*EventHandlerTaskAsyncHelper*) 和新的委派型別 (*TaskEventHandler*) ，您可以用來將以工作為基礎的非同步方法與 ASP.NET HTTP 管線所公開的舊版非同步程式設計模型整合。 此範例顯示如何：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample2.cs)]

<a id="_Toc318097378"></a>
#### <a name="asynchronous-http-handlers"></a>非同步 HTTP 處理常式

在 ASP.NET 中撰寫非同步處理常式的傳統方法是執行 *IHttpAsyncHandler* 介面。 ASP.NET 4.5 引進了可從中衍生的 *HttpTaskAsyncHandler* 非同步基底類型，可讓您更輕鬆地撰寫非同步處理常式。

*HttpTaskAsyncHandler*型別是抽象的，需要您覆寫*ProcessRequestAsync*方法。 內部 ASP.NET 會負責將傳回簽章與 ASP.NET 管線所使用的舊版非同步程式設計模型整合 * (的工作物件) * *ProcessRequestAsync* 。

下列範例示範如何在非同步 HTTP 處理常式的執行過程中，使用 *Task* 和 *await* ：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample3.cs)]

<a id="_Toc318097379"></a>
### <a name="new-aspnet-request-validation-features"></a>新的 ASP.NET 要求驗證功能

根據預設，ASP.NET 會執行要求驗證，它會檢查在欄位、標頭、cookie 等中尋找標記或腳本的要求。 如果偵測到任何，ASP.NET 會擲回例外狀況。 這可作為防禦潛在跨網站腳本攻擊的第一道防線。

ASP.NET 4.5 可讓您輕鬆地選擇性地讀取未經驗證要求資料。 ASP.NET 4.5 也會整合熱門的 AntiXSS 程式庫，此程式庫先前是外部程式庫。

開發人員經常會要求能夠選擇性地關閉其應用程式的要求驗證。 例如，如果您的應用程式是論壇軟體，您可能會想要允許使用者提交 HTML 格式的論壇貼文和批註，但仍請確認要求驗證正在檢查其他所有專案。

ASP.NET 4.5 引進兩個功能，可讓您輕鬆地選擇性地使用未經驗證輸入：延遲的 ( 「延遲」 ) 要求驗證和存取未經驗證要求資料。

<a id="_Toc318097380"></a>
#### <a name="deferred-lazy-request-validation"></a>延遲 ( 「延遲」 ) 要求驗證

在 ASP.NET 4.5 中，依預設，所有要求資料都會受到要求驗證的要求。 不過，您可以將應用程式設定為延遲要求驗證，直到實際存取要求資料為止。  (這種情況有時也稱為延遲要求驗證，這是根據某些資料案例的消極式載入。 ) 您可以將*HTTPRUntime*專案中的*requestValidationMode*屬性設定為4.5，以將應用程式設定為使用 Web.config 檔中的延遲驗證，如下列範例所示：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample4.xml)]

當要求驗證模式設定為4.5 時，只會針對特定要求值觸發要求驗證，而且只有在您的程式碼存取該值時才會觸發。 例如，如果您的程式碼取得 [要求] 的值。表單 ["論壇 \_ 文章"]，則只會針對表單集合中的該元素叫用要求驗證。 *表單*集合中的其他元素都不會進行驗證。 在舊版的 ASP.NET 中，當存取集合中的任何專案時，會針對整個要求集合觸發要求驗證。 新的行為讓不同的應用程式元件可以更輕鬆地查看不同的要求資料片段，而不會觸發其他部分的要求驗證。

<a id="_Toc318097381"></a>
#### <a name="support-for-unvalidated-requests"></a>未經驗證要求的支援

延遲的要求驗證單獨無法解決選擇性略過要求驗證的問題。 要求的呼叫. 表單 ["論壇 \_ 貼文"] 仍會觸發該特定要求值的要求驗證。 不過，您可能會想要在不觸發驗證的情況下存取此欄位，因為您想要允許該欄位中的標記。

為允許此情況，ASP.NET 4.5 現在支援未經驗證存取要求資料。 ASP.NET 4.5 在*HttpRequest*類別中包含新的*未經驗證*集合屬性。 此集合可讓您存取所有要求資料的一般值，例如 *表單*、 *查詢字串*、 *cookie*和 *Url*。

使用論壇範例，若要能夠讀取未經驗證要求資料，您必須先將應用程式設定為使用新的要求驗證模式：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample5.xml)]

然後，您可以使用 *HttpRequest 未經驗證* 屬性來讀取未經驗證表單值：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample6.cs)]

> [!WARNING]
> 安全性- *請小心使用未經驗證要求資料！* ASP.NET 4.5 已新增未經驗證要求屬性和集合，讓您更輕鬆地存取非常特定的未經驗證要求資料。 不過，您仍然必須對原始要求資料執行自訂驗證，以確保不會對使用者呈現危險的文字。

<a id="_Toc318097382"></a>
### <a name="antixss-library"></a>AntiXSS 程式庫

由於 Microsoft AntiXSS Library 的普及，ASP.NET 4.5 現在結合了該程式庫4.0 版的核心編碼常式。

編碼常式是由新的*AntiXss*命名空間中的*AntiXssEncoder*類型所執行。 您可以藉由呼叫任何在類型中執行的靜態編碼方法，直接使用 *AntiXssEncoder* 類型。 不過，使用新的防 XSS 常式最簡單的方法，就是將 ASP.NET 應用程式設定為預設使用 *AntiXssEncoder* 類別。 若要這樣做，請將下列屬性新增至 Web.config 檔案：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample7.xml)]

當 *encoderType* 屬性設定為使用 *AntiXssEncoder* 類型時，ASP.NET 中的所有輸出編碼都會自動使用新的編碼常式。

以下是已併入 ASP.NET 4.5 的外部 AntiXSS 程式庫部分：

- *HtmlEncode*、 *HtmlFormUrlEncode*和 *HtmlAttributeEncode*
- *XmlAttributeEncode* 和 *XmlEncode*
- *UrlEncode* 和 *UrlPathEncode* (新) 
- *CssEncode*

<a id="_Toc318097383"></a>
### <a name="support-for-websockets-protocol"></a>Websocket 通訊協定的支援

Websocket 通訊協定是以標準為基礎的網路通訊協定，可定義如何透過 HTTP 在用戶端與伺服器之間建立安全、即時的雙向通訊。 Microsoft 已使用 IETF 和 W3C 標準主體來協助定義通訊協定。 任何用戶端都支援 Websocket 通訊協定， (不只是瀏覽器) ，因為 Microsoft 在用戶端和行動作業系統上投資了支援 Websocket 通訊協定的大量資源。

Websocket 通訊協定可讓您更輕鬆地在用戶端與伺服器之間建立長時間執行的資料傳輸。 例如，撰寫聊天應用程式很容易，因為您可以在用戶端與伺服器之間建立真正的長時間執行連接。 您不需要利用定期輪詢或 HTTP 長時間輪詢等因應措施來模擬通訊端的行為。

ASP.NET 4.5 和 IIS 8 包含低層級 Websocket 支援，可讓 ASP.NET 開發人員使用受控 Api，以非同步方式讀取和寫入 Websocket 物件上的字串和二進位資料。 針對 ASP.NET 4.5，有 *一個新的* system.servicemodel 命名空間，其中包含使用 websocket 通訊協定的類型。

瀏覽器用戶端會建立一個在 ASP.NET 應用程式中指向 URL 的 DOM *WebSocket* 物件來建立 websocket 連線，如下列範例所示：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample8.cs)]

您可以使用任何一種模組或處理常式，在 ASP.NET 中建立 Websocket 端點。 在上述範例中，使用了 ashx 檔案，因為 ashx 檔是快速建立處理常式的方法。

根據 Websocket 通訊協定，ASP.NET 應用程式會藉由指示應將要求從 HTTP GET 要求升級至 Websocket 要求，來接受用戶端的 Websocket 要求。 以下是範例：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample9.cs)]

*AcceptWebSocketRequest*方法會接受函數委派，因為 ASP.NET 會回溯目前的 HTTP 要求，然後將控制權傳輸至函式委派。 就概念而言，這個方法與您使用 *thread*的方式類似，您可以在其中定義執行背景工作的執行緒啟動委派。

在 ASP.NET 且用戶端已成功完成 Websocket 交握之後，ASP.NET 會呼叫您的委派，而 Websocket 應用程式就會開始執行。 下列程式碼範例顯示使用 ASP.NET 中內建 Websocket 支援的簡單回應應用程式：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample10.cs)]

適用于 *await* 關鍵字和非同步工作型作業的 .net 4.5 支援非常適合用來撰寫 websocket 應用程式。 此程式碼範例顯示 Websocket 要求在 ASP.NET 內完全以非同步方式執行。 應用程式會以非同步方式等候訊息，藉由呼叫 await 通訊端從用戶端傳送 *。ReceiveAsync*。 同樣地，您可以藉由呼叫 await 通訊端，將非同步訊息傳送至用戶端 *。SendAsync*。

在瀏覽器中，應用程式會透過 *>onmessage* 函數接收 websocket 訊息。 若要從瀏覽器傳送訊息，您可以呼叫*WebSocket* DOM 類型的*傳送*方法，如下列範例所示：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample11.cs)]

未來，我們可能會發行這項功能的更新，以抽象化此版本中 Websocket 應用程式所需的一些低層級編碼。

<a id="_Toc318097384"></a>
### <a name="bundling-and-minification"></a>統合和縮製

組合可讓您將個別的 JavaScript 和 CSS 檔案結合成可視為單一檔案的組合。 縮制會藉由移除不必要的空白字元和其他字元，來總是 JavaScript 和 CSS 檔案。 這些功能適用于 Web Form、ASP.NET MVC 和網頁。

套件組合是使用套件組合類別或其中一個子類別（ScriptBundle 和 StyleBundle）所建立。 在設定組合的實例之後，只要將組合新增至全域 BundleCollection 實例，就能將組合提供給傳入的要求。 在預設範本中，會在 >bundleconfig.cs 檔案中執行套件組合設定。 此預設設定會針對範本所使用的所有核心腳本和 css 檔案，建立配套。

您可以使用其中一種可能的 helper 方法，從視圖內參考組合。 為了支援在 debug 和 release 模式中針對組合呈現不同的標記，ScriptBundle 和 StyleBundle 類別具有 helper 方法（轉譯）。 在偵測模式中，轉譯會針對組合中的每個資源產生標記。 在發行模式中，轉譯會產生整個組合的單一標記元素。 在 web.config 中修改編譯專案的 debug 屬性，即可完成 debug 和 release 模式之間的切換，如下所示：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample12.xml)]

此外，您可以直接透過當 EnableOptimizations 屬性設定啟用或停用優化。

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample13.cs)]

當檔案已配套時，它們會先依字母順序排序， (在 **方案總管**) 中顯示這些檔案的方式。 然後會組織它們，以便先載入 (的已知程式庫和自訂延伸模組，例如 jQuery、MooTools 和 Dojo) 。 例如，如上所示的 [腳本] 資料夾的組合最終順序將是：

1. jquery-1.6.2.js
2. jquery-ui.js
3. jquery.tools.js
4. a.js

CSS 檔案也會依字母順序排序，然後再進行重新組織，以便重設 .css 和正規化 .css 都在任何其他檔案之前。 如上所示的 [樣式] 資料夾的組合最終排序會是：

1. 重設 .css
2. content .css
3. forms .css
4. globals
5. menu .css
6. 樣式 .css

<a id="_Toc_perf"></a>
### <a name="performance-improvements-for-web-hosting"></a>Web 裝載的效能改進

.NET Framework 4.5 和 Windows 8 引進的功能，可協助您大幅提升 web 伺服器工作負載的效能。 這包括在啟動時間和使用 ASP.NET 之 web 主控網站的記憶體使用量中，最高可達 35% ) 的縮減 (。

<a id="_Toc_perf_1"></a>
#### <a name="key-performance-factors"></a>關鍵效能因素

在理想的情況下，所有網站都應該是作用中且在記憶體中，以確保每次都能快速回應下一個要求。 可能會影響網站回應性的因素包括：

- 在應用程式集區回收之後，網站重新開機所需的時間。 當網站元件不再存在於記憶體中時，這是啟動網站的 web 伺服器進程所需的時間。  (平臺元件仍在記憶體中，因為它們是由其他網站使用。 ) 這種情況稱為「冷網站、暖架構啟動」或單純的「冷網站啟動」。
- 網站所佔用的記憶體數量。 這項作業的條款包括「每個網站的記憶體耗用量」或「未共用的工作集」。

新的效能改進著重于這兩個因素。

<a id="_Toc_perf_2"></a>
#### <a name="requirements-for-new-performance-features"></a>新效能功能的需求

新功能的需求可細分為下列類別：

- 在 .NET Framework 4 上執行的改良功能。
- 需要 .NET Framework 4.5 但可以在任何版本的 Windows 上執行的改良功能。
- 僅適用于 Windows 8 上執行的 .NET Framework 4.5 的改進。

效能會隨著您能夠啟用的每個改進層級而增加。

部分 .NET Framework 4.5 的改進功能可充分利用適用于其他案例的更廣泛效能功能。

<a id="_Toc_perf_3"></a>
#### <a name="sharing-common-assemblies"></a>共用萬用群組件

**需求**： .NET Framework 4 和 Visual Studio 11 開發人員預覽 SDK

伺服器上的不同網站通常會使用相同的協助程式元件 (例如，來自入門套件或範例應用程式) 的元件。 每個網站在其 Bin 目錄中都有自己的這些元件複本。 雖然元件的物件程式碼完全相同，但它們實際上是個別的元件，因此在冷網站啟動時，每個元件都必須個別讀取，並在記憶體中分開保存。

新的暫存功能可解決這種效率，同時減少 RAM 需求和載入時間。 暫存可讓 Windows 保留檔案系統中每個元件的單一複本，而網站 Bin 資料夾中的個別元件則會取代為單一複本的符號連結。 如果個別網站需要元件的不同版本，則符號連結會取代為新版本的元件，而且只會影響該網站。

使用符號連結共用元件需要名為 aspnetintern.exe 的新工具 \_ ，可讓您建立和管理留用元件的存放區。 它是 Visual Studio 11 開發人員預覽 SDK 的一部分。  (不過，如果您已安裝最新的 [更新](https://support.microsoft.com/kb/2468871)，它將會在只安裝 .NET Framework 4 的系統上運作。 ) 

為了確保所有符合資格的元件都已暫留，您可以定期執行 aspnet \_intern.exe (例如，每週一次作為排程工作) 。 一般用途如下所示：

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample14.cmd)]

若要查看所有選項，請執行不含引數的工具。

<a id="_Toc_perf_4"></a>
#### <a name="using-multi-core-jit-compilation-for-faster-startup"></a>使用多重核心 JIT 編譯以加快啟動速度

**需求**： .NET Framework 4。5

若為冷網站啟動，則不只需要從磁片讀取元件，但必須以 JIT 編譯網站。 對於複雜的網站來說，這可能會增加重大延遲。 .NET Framework 4.5 中的新一般用途技術可將 JIT 編譯分散到可用的處理器核心，以減少這些延遲。 它會使用先前的網站啟動期間所收集的資訊，盡可能儘早地執行此作業。 這項功能是由 [ProfileOptimization. StartProfile](https://msdn.microsoft.com/library/system.runtime.profileoptimization.startprofile(VS.110).aspx) 方法所執行。

ASP.NET 中預設會啟用使用多個核心的 JIT 編譯，因此您不需要執行任何動作就能利用這項功能。 如果您想要停用此功能，請在 Web.config 檔案中進行下列設定：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample15.xml)]

<a id="_Toc_perf_5"></a>
#### <a name="tuning-garbage-collection-to-optimize-for-memory"></a>調整垃圾收集以針對記憶體優化

**需求**： .NET Framework 4。5

一旦網站正在執行，使用垃圾收集行程 (GC) 堆積可以是其記憶體耗用量的重要因素。 就像任何垃圾收集行程一樣，.NET Framework GC 也會在 CPU 時間 (頻率和集合的重要性之間做出取捨) 和記憶體耗用量， (用於新的、釋出或可免費物件) 的額外空間。 在先前的版本中，我們已提供有關如何設定 GC 以達到適當平衡 (例如，請參閱 [ASP.NET 2.0/3.5 共用裝載](https://www.iis.net/learn/web-hosting/web-server-for-shared-hosting/aspnet-20-35-shared-hosting-configuration) 設定) 。

針對 .NET Framework 4.5 （而不是多個獨立設定），可使用工作負載定義的設定，以啟用所有先前建議的 GC 設定，以及為每個網站工作集提供額外效能的新調整。

若要啟用 GC 記憶體微調，請將下列設定新增至 Windows\Microsoft.NET\Framework\v4.0.30319\aspnet.config 檔案：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample16.xml)]

 (如果您熟悉先前的 aspnet.config 變更指引，請注意，此設定會取代舊的設定，例如，不需要設定 >gcserver>、>gcconcurrent> 等。您不需要移除舊的設定。 ) 

<a id="_Toc_perf_6"></a>
#### <a name="prefetching-for-web-applications"></a>針對 web 應用程式預先提取

**需求**： Windows 8 上執行 .NET Framework 4。5

在數個版本中，Windows 已包含稱為 [prefetcher](http://en.wikipedia.org/wiki/Prefetcher) 的技術，可減少應用程式啟動的磁片讀取成本。 因為冷啟動是主要用於用戶端應用程式的問題，所以這項技術並不包含在 Windows Server 中，只包含伺服器的必要元件。 最新版本的 Windows Server 現在提供預先提取功能，可讓您優化個別網站的啟動。

若為 Windows Server，則預設不會啟用 prefetcher。 若要啟用並設定高密度 web 裝載的 prefetcher，請在命令列執行下列命令集：

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample17.cmd)]

然後，若要整合 prefetcher 與 ASP.NET 應用程式，請將下列內容新增至 Web.config 檔案：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample18.xml)]

<a id="_Toc318097385"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

<a id="_Toc318097386"></a>
### <a name="strongly-typed-data-controls"></a>強型別資料控制項

在 ASP.NET 4.5 中，Web Form 包含一些使用資料的增強功能。 第一個改善是強型別資料控制項。 針對舊版 ASP.NET 中的 Web Form 控制項，您可以使用 *Eval* 和資料系結運算式來顯示資料系結值：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample19.aspx)]

針對雙向資料系結，您可以使用 *Bind*：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample20.aspx)]

在執行時間，這些呼叫會使用反映來讀取指定成員的值，然後將結果顯示在標記中。 這種方法可讓您輕鬆地針對任意的 unshaped 資料進行資料系結。

不過，像這樣的資料系結運算式不支援成員名稱的 IntelliSense、流覽 (例如 [移至定義]) ，或針對這些名稱進行編譯時間檢查等功能。

為了解決這個問題，ASP.NET 4.5 新增了宣告控制項所系結之資料類型的能力。 您可以使用新的 *ItemType* 屬性來完成此動作。 當您設定這個屬性時，資料系結運算式的範圍中會有兩個新的具類型變數： *Item* 和 *BindItem*。 因為變數是強型別，所以您可以獲得 Visual Studio 開發經驗的完整優勢。

針對雙向資料系結運算式，請使用 *BindItem* 變數：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample21.aspx)]

ASP.NET Web Forms framework 中支援資料系結的大部分控制項都已更新為支援 *ItemType* 屬性。

<a id="_Toc318097387"></a>
### <a name="model-binding"></a>模型繫結

模型系結會在 ASP.NET Web Forms 控制項中擴充資料系結，以使用以程式碼為主的資料存取。 它結合了 *ObjectDataSource* 控制項的概念，以及 ASP.NET MVC 中的模型系結。

<a id="_Toc318097388"></a>
#### <a name="selecting-data"></a>選取資料

若要將資料控制項設定為使用模型系結來選取資料，請將控制項的 [ *SelectMethod* ] 屬性設定為頁面程式碼中的方法名稱。 資料控制項會在頁面生命週期中的適當時間呼叫方法，並自動系結傳回的資料。 不需要明確地呼叫 *DataBind* 方法。

在下列範例中， *GridView* 控制項設定為使用名為 *GetCategories*的方法：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample22.aspx)]

您可以在頁面的程式碼中建立 *GetCategories* 方法。 針對簡單的選取作業，方法不需要任何參數，而且應該傳回 *IEnumerable* 或 *IQueryable* 物件。 如果已設定新的*ItemType*屬性 (啟用強型別資料系結運算式（如稍早) 的強型別[資料控制](#_Toc318097386)項所述），則應該傳回這些介面的泛型版本（ *IEnumerable &lt; &gt; t*或*IQueryable &lt; &gt; t*），其中*T*參數符合*ItemType*屬性的類型 (例如， *IQueryable &lt; 類別 &gt; *) 。

下列範例顯示 *GetCategories* 方法的程式碼。 此範例會使用 Entity Framework Code First 模型與 Northwind 範例資料庫。 程式碼可確保查詢會透過 *Include* 方法來傳回每個類別的相關產品詳細資料。  (這可確保標記中的 *TemplateField* 專案會顯示每個類別中的產品計數，而不需要 [n + 1 選取](http://stackoverflow.com/questions/97197/what-is-the-n1-selects-problem)。 ) 

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample23.cs)]

當頁面執行時， *GridView* 控制項會自動呼叫 *GetCategories* 方法，並使用設定的欄位轉譯傳回的資料：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.png)

由於 select 方法會傳回 *IQueryable* 物件，因此 *GridView* 控制項可以在執行查詢之前進一步操作查詢。 例如， *GridView* 控制項可以在執行之前，將排序和分頁的查詢運算式加入至傳回的 *IQueryable* 物件，以便這些作業是由基礎 LINQ 提供者執行。 在此情況下，Entity Framework 可確保在資料庫中執行這些作業。

下列範例顯示已修改成允許排序和分頁的 *GridView* 控制項：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample24.aspx)]

現在當頁面執行時，控制項可以確保只會顯示目前的資料頁面，並依選取的資料行排序：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.png)

若要篩選傳回的資料，必須將參數加入至 select 方法。 這些參數將會在執行時間由模型系結填入，而您可以使用它們來改變查詢，然後再傳回資料。

例如，假設您想要讓使用者在查詢字串中輸入關鍵字來篩選產品。 您可以將參數加入至方法，並更新程式碼以使用參數值：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample25.cs)]

如果為*關鍵字*提供了值，則此程式碼會包含*Where*運算式，然後傳回查詢結果。

<a id="_Toc318097389"></a>
#### <a name="value-providers"></a>值提供者

先前的範例並不是 *關鍵字* 參數值的來源所特有的。 若要指出此資訊，您可以使用參數屬性。 在此範例中，您可以使用*ModelBinding*命名空間中的*QueryStringAttribute*類別：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample26.cs)]

這會指示模型系結在執行時間嘗試將查詢字串中的值系結至 *關鍵字* 參數。  (這可能牽涉到執行類型轉換，但在此情況下並不會發生。 ) 如果無法提供值，且類型不可為 null，則會擲回例外狀況。

這些方法的值來源稱為「值提供者」，而參數屬性（attribute）會指出要使用的值提供者稱為「值提供者」屬性。 Web Form 將會針對 Web Form 應用程式中使用者輸入的所有一般來源（例如查詢字串、cookie、表單值、控制項、檢視狀態、會話狀態和配置檔案屬性），包含值提供者和對應的屬性。 您也可以撰寫自訂值提供者。

預設會使用參數名稱做為索引鍵，以在值提供者集合中尋找值。 在此範例中，程式碼會尋找名為關鍵字的查詢字串值 (例如 ~/default.aspx？關鍵字 = chef) 。 您可以藉由將引數傳遞為參數屬性的引數，來指定自訂索引鍵。 例如，若要使用名為 q 的查詢字串變數值，您可以執行下列動作：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample27.cs)]

如果這個方法是在頁面的程式碼中，使用者可以使用查詢字串傳遞關鍵字來篩選結果：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.png)

模型系結會完成許多您需要手動編寫程式碼的工作：讀取值、檢查 null 值、嘗試將它轉換成適當的類型、檢查轉換是否成功，最後使用查詢中的值。 模型系結會產生更少的程式碼，以及在整個應用程式中重複使用功能的能力。

<a id="_Toc318097390"></a>
#### <a name="filtering-by-values-from-a-control"></a>依控制項的值篩選

假設您想要擴充範例，讓使用者從下拉式清單中選擇篩選值。 將下列下拉式清單新增至標記，並將它設定為使用 *SelectMethod* 屬性從另一個方法取得其資料：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample28.aspx)]

一般而言，您也會將 *EmptyDataTemplate* 專案新增至 *GridView* 控制項，如此當找不到相符的產品時，控制項就會顯示訊息：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample29.aspx)]

在頁面程式碼中，為下拉式清單加入新的 select 方法：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample30.cs)]

最後，更新 *GetProducts* select 方法以採用新的參數，其中包含從下拉式清單中選取之類別的識別碼：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample31.cs)]

現在當頁面執行時，使用者可以從下拉式清單中選取類別，然後將 *GridView* 控制項自動重新系結以顯示篩選過的資料。 這是可能的，因為模型系結會追蹤 select 方法的參數值，並偵測回回傳之後是否有任何參數值變更。 如果是，模型系結會強制關聯的資料控制重新系結至資料。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.png)

<a id="_Toc318097391"></a>
### <a name="html-encoded-data-binding-expressions"></a>HTML 編碼 Data-Binding 運算式

您現在可以對資料系結運算式的結果進行 HTML 編碼。 將冒號 (： ) 至 &lt; 標示資料系結運算式的% # 前置詞結尾：

[!code-aspx[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample32.aspx)]

<a id="_Toc318097392"></a>
### <a name="unobtrusive-validation"></a>不顯眼的驗證

您現在可以設定內建的驗證器控制項，以針對用戶端驗證邏輯使用不顯眼的 JavaScript。 這可大幅減少網頁標記中以內嵌方式呈現的 JavaScript 數量，並減少整體頁面大小。 您可以利用下列任何一種方式，為驗證器控制項設定不顯眼的 JavaScript：

- 藉由將下列設定加入至 Web.config 檔案中的* &lt; appSettings &gt; *元素，以全域方式進行： 

    [!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample33.xml)]
- 藉由將靜態 *ValidationSettings UnobtrusiveValidationMode* 屬性設定為 (*UnobtrusiveValidationMode* ，通常會在 Global.asax 檔案) 的 *應用程式 \_ 啟動* 方法中，以全域方式進行。
- 針對頁面的個別設定，方法是將*頁面*類別的新*UnobtrusiveValidationMode*屬性設定為*UnobtrusiveValidationMode. WebForms*。

<a id="_Toc318097393"></a>
### <a name="html5-updates"></a>HTML5 更新

Web Form 的伺服器控制項有一些改進，可利用 HTML5 的新功能：

- *TextBox*控制項的*TextMode*屬性已更新，可支援新的 HTML5 輸入類型，例如*電子郵件*、*日期時間*等等。
- *FileUpload*控制項現在支援從支援此 HTML5 功能的瀏覽器進行多個檔案上傳。
- 驗證器控制項現在支援驗證 HTML5 輸入元素。
- 具有代表 URL 之屬性的新 HTML5 元素現在支援 runat = "server"。 因此，您可以在 URL 路徑中使用 ASP.NET 慣例（例如 ~ 運算子）來代表應用程式根目錄 (例如， &lt; video runat = "server" src = "~/myVideo.wmv"/ &gt;) 。
- 已修正 *UpdatePanel* 控制項，以支援張貼 HTML5 輸入欄位。

<a id="_Toc318097394"></a>
## <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

ASP.NET MVC 4 Beta 現在隨附于 Visual Studio 11 Beta 版。 ASP.NET MVC 是一種架構，可利用模型-視圖控制器 (MVC) 模式來開發高測試性和可維護的 Web 應用程式。 ASP.NET MVC 4 可讓您輕鬆地建立適用于行動網路的應用程式，並包含 ASP.NET Web API，協助您建立可連接到任何裝置的 HTTP 服務。 如需詳細資訊，請參閱 [ASP.NET MVC 4 版本](mvc4-release-notes.md)資訊。

<a id="_Toc318097395"></a>
## <a name="aspnet-web-pages-2"></a>ASP.NET Web Pages 2

新功能包括下列各項：

- 新的和更新的網站範本。
- 使用 *驗證* 協助程式加入伺服器端和用戶端驗證。
- 使用資產管理員來註冊腳本的能力。
- 使用 OAuth 和 OpenID 從 Facebook 和其他網站啟用登入。
- 使用 *maps* helper 來新增對應。
- 並存執行 Web Pages 應用程式。
- 行動裝置的轉譯頁面。

如需這些功能和整頁程式碼範例的詳細資訊，請參閱 [Web Pages 2 Beta 的最上層功能](https://go.microsoft.com/fwlink/?LinkID=227824)。

<a id="_Toc318097396"></a>
## <a name="visual-web-developer-11-beta"></a>Visual Web Developer 11 Beta 版

本節提供 Visual Web Developer 11 Beta 和 Visual Studio 2012 候選版中的 web 程式開發改良功能的相關資訊。

<a id="project-compatibility"></a>
### <a name="project-sharing-between-visual-studio-2010-and-visual-studio-2012-release-candidate-project-compatibility"></a>Visual Studio 2010 與 Visual Studio 2012 候選版之間的專案共用 (專案相容性) 

在 Visual Studio 2012 候選版之前，請在較新版本的中開啟現有的專案，Visual Studio 啟動轉換 Wizard。 這會強制將專案的內容 (資產) ，以及解決方案的內容升級為無法回溯相容的新格式。 因此，轉換之後，您就無法在舊版 Visual Studio 中開啟專案。

許多客戶告訴我們這不是正確的方法。 在 Visual Studio 11 Beta 版中，我們現在支援 Visual Studio 2010 SP1 共用專案和解決方案。 這表示，如果您在 Visual Studio 2012 候選版中開啟2010專案，您仍然可以在 Visual Studio 2010 SP1 中開啟專案。

> [!NOTE]
> 有幾種類型的專案無法在 Visual Studio 2010 SP1 和 Visual Studio 2012 發行候選版本之間共用。 這些專案包括一些較舊的專案 (例如 ASP.NET MVC 2 專案) 或專案，以供特殊用途 (例如) 安裝專案。

當您第一次在 Visual Studio 11 Beta 中開啟 Visual Studio 2010 SP1 Web 專案時，會將下列屬性新增至專案檔：

- FileUpgradeFlags
- UpgradeBackupLocation
- OldToolsVersion
- VisualStudioVersion
- VSToolsPath

升級專案檔的進程會使用 FileUpgradeFlags、UpgradeBackupLocation 和 OldToolsVersion。 它們不會影響 Visual Studio 2010 中的專案使用。

VisualStudioVersion 是 MSBuild 4.5 所使用的新屬性，表示目前專案的 Visual Studio 版本。 因為這個屬性不存在於 MSBuild 4.0 (Visual Studio 2010 SP1 使用) 的 MSBuild 版本，所以我們會將預設值插入專案檔中。

VSToolsPath 屬性是用來判斷要從 MSBuildExtensionsPath32 設定所代表之路徑匯入的正確 .targets 檔案。

此外，也有一些與匯入元素相關的變更。 必須進行這些變更，才能支援兩種版本 Visual Studio 之間的相容性。

> [!NOTE]
> 如果專案在兩部不同的電腦上 Visual Studio 2010 SP1 和 Visual Studio 11 Beta 之間共用，而且如果專案在應用程式資料夾中包含本機資料庫， \_ 則您必須確定這兩部電腦上都已安裝資料庫所使用的 SQL Server 版本。

<a id="Configuration_Changes_In_ASPNET45_Website_Templates"></a>
### <a name="configuration-changes-in-aspnet-45-website-templates"></a>ASP.NET 4.5 網站範本中的設定變更

使用 Visual Studio 2012 候選版中的網站範本建立的網站預設 *Web.config* 檔案已進行下列變更：

- 在 `<httpRuntime>` 元素中， `encoderType` 現在預設會將屬性設定為使用已加入至 ASP.NET 的 AntiXSS 類型。 如需詳細資訊，請參閱 [AntiXSS 程式庫](#_Toc318097382)。
- 此外，在專案中 `<httpRuntime>` ， `requestValidationMode` 屬性會設為 "4.5"。 這表示根據預設，要求驗證設定為使用延後的 ( 「延遲」 ) 驗證。 如需詳細資訊，請參閱 [新的 ASP.NET 要求驗證功能](#_Toc318097379)。
- `<modules>`區段的元素不 `<system.webServer>` 包含 `runAllManagedModulesForAllRequests` 屬性。  (預設值為 false。 ) 這表示如果您使用的 IIS 7 版本尚未更新為 SP1，您可能會在新網站中遇到路由問題。 如需詳細資訊，請參閱 [IIS 7 中適用于 ASP.NET 路由的原生支援](#Native_Support_In_IIS7_For_ASPNET_Routine)。

這些變更不會影響現有的應用程式。 不過，它們可能代表現有網站與您使用新範本為 ASP.NET 4.5 建立的新網站之間的行為差異。

<a id="Native_Support_In_IIS7_For_ASPNET_Routine"></a>
### <a name="native-support-in-iis-7-for-aspnet-routing"></a>適用于 ASP.NET 路由的 IIS 7 原生支援

這並不是 ASP.NET 的變更，但如果您使用的是未套用 SP1 更新的 IIS 7 版本，可能會影響新網站專案的範本變更。

在 ASP.NET 中，您可以將下列設定設定新增至應用程式，以便支援路由：

[!code-xml[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample34.xml?highlight=3)]

當 **runAllManagedModulesForAllRequests** 為 true 時，url 之類的 url 就 `http://mysite/myapp/home` 會移至 ASP.NET，即使 url 上沒有 *.aspx*、 *mvc*或類似的副檔名。

針對 IIS 7 所做的更新會使 **runAllManagedModulesForAllRequests** 設定不必要，並以原生方式支援 ASP.NET 路由。  (需有關更新的詳細資訊，請參閱 Microsoft 支援服務文章， [其中有可用的更新，可讓特定的 IIS 7.0 或 IIS 7.5 處理常式處理 url 不是以句點結束的要求](https://support.microsoft.com/kb/980368)。 ) 

如果您的網站是在 IIS 7 上執行，而且 IIS 已更新，您就不需要將 **runAllManagedModulesForAllRequests** 設定為 true。 事實上，不建議將它設定為 true，因為它會增加要求的不必要處理負荷。 若此設定為 true，則所有要求（包括 *.htm*、 *.jpg*和其他靜態檔案的要求）也會經歷 ASP.NET 的要求管線。

如果您使用 Visual Studio 2012 RC 中提供的範本來建立新的 ASP.NET 4.5 網站，則網站的設定不會包含 **runAllManagedModulesForAllRequests** 設定。 這表示根據預設，此設定為 false。

如果您接著在未安裝 SP1 的 Windows 7 上執行網站，IIS 7 將不會包含必要的更新。 因此，路由將無法運作，而且您會看到錯誤。 如果您有路由無法運作的問題，您可以執行下列其中一項：

- 將 Windows 7 更新為 SP1，這會將更新新增至 IIS 7。
- 安裝之前所列的 Microsoft 支援服務文章中所述的更新。
- 將該網站的 Web.config 檔案中的 **runAllManagedModulesForAllRequests** 設定為 true。 請注意，這會增加一些要求的負擔。

<a id="_Toc318097397"></a>
### <a name="html-editor"></a>HTML 編輯器

<a id="_Toc318097398"></a>
#### <a name="smart-tasks"></a>智慧型工作

在設計檢視中，伺服器控制項的複雜屬性通常會有相關聯的對話方塊和嚮導，讓您輕鬆地設定它們。 例如，您可以使用特殊的對話方塊，將資料來源新增至 *中繼器* 控制項，或將資料行加入至 *GridView* 控制項。

不過，此類型的複雜屬性 UI 說明尚未在來源視圖中提供。 因此，Visual Studio 11 為來源視圖引進智慧型工作。 智慧型工作是 c # 和 Visual Basic 編輯器中常用功能的內容感知快捷方式。

針對 ASP.NET Web Forms 控制項，當插入點位於元素內部時，智慧型工作會在伺服器標記上顯示為小型圖像：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.png)

當您按一下圖像或按下 CTRL + 時，智慧工作提示展開。  (點) ，就像在程式碼編輯器中一樣。 然後，它會顯示類似設計檢視中智慧工作的快捷方式。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image7.png)

例如，上圖中的智慧工作提示會顯示 GridView 工作選項。 如果您選擇 [編輯資料行]，則會顯示下列對話方塊：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image8.png)

填入對話方塊會設定您可以在設計檢視中設定的相同屬性。 當您按一下 [確定] 時，就會使用新的設定來更新控制項的標記：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image9.png)

<a id="_Toc318097399"></a>
#### <a name="wai-aria-support"></a>WAI-ARIA 支援

撰寫可存取的網站日益重要。 [WAI-ARIA 協助工具標準](http://www.w3.org/WAI/intro/aria)定義開發人員應該如何撰寫可存取的網站。 這項標準現在已在 Visual Studio 中受到完整支援。

例如， *role* 屬性現在具有完整的 IntelliSense：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image10.png)

WAI-ARIA 標準也引進了前面加上 *aria* 的屬性，可讓您將語義新增至 HTML5 檔。 Visual Studio 也完全支援這些 *aria* 屬性：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image11.png) ![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image12.png)

<a id="_Toc318097400"></a>
#### <a name="new-html5-snippets"></a>新的 HTML5 程式碼片段

為了讓您更快速且更輕鬆地撰寫常用的 HTML5 標記，Visual Studio 包含數個程式碼片段。 影片程式碼片段為範例：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image13.png)

若要叫用程式碼片段，請在 IntelliSense 中選取專案時，按 Tab 鍵兩次：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image14.png)

這會產生您可以自訂的程式碼片段。

<a id="_Toc318097401"></a>
#### <a name="extract-to-user-control"></a>解壓縮至使用者控制項

在大型的網頁中，將個別的部分移至使用者控制項可能是個不錯的主意。 這種形式的重構有助於提高頁面的可讀性，並且可以簡化頁面的結構。

若要簡化此作業，當您編輯原始檔視圖中的 Web Form 頁面時，您現在可以選取頁面中的文字，以滑鼠右鍵按一下它，然後選擇 [解壓縮至使用者控制項：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image2.jpg)

<a id="_Toc318097402"></a>
#### <a name="intellisense-for-code-nuggets-in-attributes"></a>在屬性中區塊程式碼的 IntelliSense

Visual Studio 一直都在任何頁面或控制項中提供區塊伺服器端程式碼的 IntelliSense。 現在 Visual Studio 也包含 HTML 屬性中區塊程式碼的 IntelliSense。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image15.png)

這可讓您更輕鬆地建立資料系結運算式：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image16.png)

<a id="_Toc318097403"></a>
#### <a name="automatic-renaming-of-matching-tag-when-you-rename-an-opening-or-closing-tag"></a>當您重新命名開頭或結束記號時，自動重新命名相符的標記

如果您重新命名 HTML 元素 (例如，您將 *div* 標記變更為 *標頭* 標記) ，則對應的開頭或結束記號也會即時變更。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image17.png)

這有助於避免您忘記變更結束記號或變更錯誤的錯誤。

<a id="_Toc318097404"></a>
#### <a name="event-handler-generation"></a>產生事件處理常式

Visual Studio 現在包含來源視圖中的功能，可協助您撰寫事件處理常式，並以手動方式進行系結。 如果您正在編輯來源視圖中的事件名稱，IntelliSense &lt; 會顯示 [建立新事件] &gt; ，這會在頁面的程式碼中建立具有正確簽章的事件處理常式：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image3.jpg)

根據預設，事件處理常式會使用控制項的識別碼作為事件處理方法的名稱：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image4.jpg)

在此案例中，產生的事件處理常式看起來會像這樣 (在 c # ) 中：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image18.png)

<a id="_Toc318097405"></a>
#### <a name="smart-indent"></a>智慧縮排

當您在空白 HTML 元素內部按下 Enter 時，編輯器會將插入點放在正確的位置：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image19.png)

如果您在此位置按下 Enter，則會向下移動並縮排結束記號，以符合開頭標記。 插入點也會縮排：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image20.png)

<a id="_Toc318097406"></a>
#### <a name="auto-reduce-statement-completion"></a>自動減少語句完成

Visual Studio 中的 IntelliSense 清單現在會根據您所輸入的內容進行篩選，使其只顯示相關的選項：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image21.png)

IntelliSense 也會根據 IntelliSense 清單中個別單字的標題案例進行篩選。 例如，如果您輸入 "dl"，則會顯示 dl 和 asp： DataList：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image22.png)

這項功能可讓您更快速地取得已知元素的語句完成。

<a id="_Toc318097407"></a>
### <a name="javascript-editor"></a>JavaScript 編輯器

Visual Studio 2012 候選版中的 JavaScript 編輯器是全新的，可大幅改善在 Visual Studio 中使用 JavaScript 的體驗。

<a id="_Toc318097408"></a>
#### <a name="code-outlining"></a>程式碼大綱

現在會自動為所有的函式建立大綱區域，讓您可以折迭與目前焦點無關的檔案部分。

<a id="_Toc318097409"></a>
#### <a name="brace-matching"></a>括號對稱

當您將插入點放在左或右大括弧時，編輯器會反白顯示相符的括弧。

<a id="_Toc318097410"></a>
#### <a name="go-to-definition"></a>移至定義

[移至定義] 命令可讓您跳到函式或變數的來源。

<a id="_Toc318097411"></a>
#### <a name="ecmascript5-support"></a>ECMAScript5 支援

編輯器支援 ECMAScript5 中的新語法和 Api，這是描述 JavaScript 語言的最新標準版本。

<a id="_Toc318097412"></a>
#### <a name="dom-intellisense"></a>DOM IntelliSense

已改進適用于 DOM Api 的 IntelliSense，並支援許多新的 HTML5 Api，包括 *querySelector*、DOM 儲存、跨檔訊息和 *畫布*。 DOM IntelliSense 現在是由單一簡單的 JavaScript 檔案所驅動，而不是原生類型程式庫定義。 這可讓您輕鬆地擴充或取代。

<a id="_Toc318097413"></a>
#### <a name="vsdoc-signature-overloads"></a>VSDOC 簽章多載

您現在可以使用* &lt; &gt; 新的*簽章元素，針對 JavaScript 函式的個別多載宣告詳細的 IntelliSense 批註，如下列範例所示：

[!code-csharp[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample35.cs)]

<a id="_Toc318097414"></a>
#### <a name="implicit-references"></a>隱含參考

您現在可以將 JavaScript 檔案新增至中央清單，此清單會隱含地包含在任何指定的 JavaScript 檔案或區塊參考的檔案清單中，這表示您會取得其內容的 IntelliSense。 例如，您可以將 jQuery 檔案加入檔案的中央清單中，而且您將會在任何 JavaScript 區塊中取得 jQuery 函式的 IntelliSense，不論您是否已使用///reference/) 明確地 (參考 &lt; &gt; 。

<a id="_Toc318097415"></a>
### <a name="css-editor"></a>CSS 編輯器

<a id="_Toc318097416"></a>
#### <a name="auto-reduce-statement-completion"></a>自動減少語句完成

CSS 的 IntelliSense 清單現在會根據所選架構所支援的 CSS 屬性和值進行篩選。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image23.png)

IntelliSense 也支援標題案例搜尋：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image24.png)

<a id="_Toc318097417"></a>
#### <a name="hierarchical-indentation"></a>階層式縮排

CSS 編輯器會使用縮排來顯示階層式規則，讓您概述如何以邏輯方式組織串聯規則。 在下列範例中，#list 選取器是清單的串聯式子系，因此會縮排。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image25.png)

下列範例顯示更複雜的繼承：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image26.png)

規則的縮排取決於其父規則。 依預設會啟用階層式縮排，但您可以在 [選項] 對話方塊中停用 [選項] 對話方塊， (工具]、功能表列的選項) ：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image27.png)

<a id="_Toc318097418"></a>
#### <a name="css-hacks-support"></a>CSS 的駭客支援

分析數百個真實世界的 CSS 檔案，顯示 CSS 的駭客攻擊很常見，現在 Visual Studio 支援最廣泛使用的 CSS。 這項支援包括 IntelliSense，以及星級 (\*) 和底線 (\_) 屬性的駭客驗證：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image28.png)

此外，也支援一般選取器的駭客，以便即使套用階層縮排，也會維持階層式縮排。 用來以 Internet Explorer 7 為目標的一般選擇器，是在選取器前面加上* \* ： first-child + html*。 使用該規則將會維持階層式縮排：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image29.png)

<a id="_Toc318097419"></a>
#### <a name="vendor-specific-schemas--moz---webkit"></a>廠商特定架構 (-moz-,-webkit) 

CSS3 導入了許多由不同瀏覽器在不同時間執行的屬性。 這先前強制開發人員使用廠商特定的語法來撰寫特定瀏覽器的程式碼。 這些瀏覽器特定屬性現在包含在 IntelliSense 中。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image30.png)

<a id="_Toc318097420"></a>
#### <a name="commenting-and-uncommenting-support"></a>批註和取消批註支援

您現在可以使用程式碼編輯器中使用的相同快速鍵來批註和取消批註 CSS 規則 (Ctrl + K、C to comment 和 Ctrl + K，以取消批註) 。

<a id="_Toc318097421"></a>
#### <a name="color-picker"></a>色彩選擇器

在舊版的 Visual Studio 中，色彩相關屬性的 IntelliSense 是由命名的色彩值的下拉式清單所組成。 該清單已由全功能色彩選擇器取代。

當您輸入色彩值時，色彩選擇器會自動顯示，並顯示先前使用過的色彩清單，後面接著預設的色調色板。 您可以使用滑鼠或鍵盤來選取色彩。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image31.png)

清單可以展開為完整的色彩選擇器。 選擇器可讓您在移動不透明度滑杆時，自動將任何色彩轉換成 RGBA，藉以控制 Alpha 色板：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image32.png)

<a id="_Toc318097422"></a>
#### <a name="snippets"></a>程式碼片段

CSS 編輯器中的程式碼片段可讓您更輕鬆快速地建立跨瀏覽器樣式。 許多需要瀏覽器特定設定的 CSS3 屬性現在已轉換成程式碼片段。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image33.png)

CSS 程式碼片段支援 advanced 案例 (例如 CSS3 媒體查詢) 透過輸入符號 ( @ ) ，它會顯示 IntelliSense 清單。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image34.png)

當您選取 [ @media 值] 並按下 tab 鍵時，CSS 編輯器會插入下列程式碼片段：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image5.jpg)

如同程式碼的程式碼片段，您可以建立自己的 CSS 程式碼片段。

<a id="_Toc318097423"></a>
#### <a name="custom-regions"></a>自訂區域

現在已可在程式碼編輯器中使用的命名程式碼區域，現在可用於 CSS 編輯。 這可讓您輕鬆地將相關的樣式區塊分組。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image35.png)

當區域處於折迭狀態時，會顯示區域的名稱：

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image36.png)

<a id="_Toc318097424"></a>
### <a name="page-inspector"></a>Page Inspector

Page Inspector 是在 Visual Studio IDE 中 (HTML、Web Form、ASP.NET MVC 或網頁) 轉譯網頁的工具，可讓您檢查原始程式碼和產生的輸出。 針對 ASP.NET 網頁，Page Inspector 可讓您判斷哪些伺服器端程式碼已產生轉譯至瀏覽器的 HTML 標籤。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image37.png)

如需 Page Inspector 的詳細資訊，請參閱下列教學課程：

- 在[ASP.NET MVC](../mvc/overview/views/using-page-inspector-in-aspnet-mvc.md)中使用 Page Inspector
- 在[ASP.NET Web Forms](../web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project.md)中使用 Page Inspector

<a id="_Toc318097425"></a>
### <a name="publishing"></a>發佈

<a id="_Toc318097426"></a>
#### <a name="publish-profiles"></a>發佈設定檔

在 Visual Studio 2010 中，Web 應用程式專案的發行資訊不會儲存在版本控制中，且不會設計為與其他人共用。 在 Visual Studio 2012 候選版中，發行設定檔的格式已變更。 它已成為 team 成品，現在可以輕鬆地根據 MSBuild 來利用組建。 組建設定資訊是在 [發行] 對話方塊中，因此您可以在發佈之前輕鬆地切換組建配置。

發行設定檔會儲存在 PublishProfiles 資料夾中。 資料夾的位置取決於您使用的程式設計語言：

- C #： Properties\PublishProfiles
- Visual Basic：我的 Project\PublishProfiles

每個設定檔都是 MSBuild 檔案。 在發佈期間，會將這個檔案匯入到專案的 MSBuild 檔案中。 在 Visual Studio 2010 中，如果您想要變更發行或封裝程式，則必須將您的自訂放在名為 **專案名稱**的檔案中。 這仍然受支援，但您現在可以將自訂內容放在發行設定檔本身。 如此一來，就只會針對該設定檔使用自訂。

您現在也可以利用 MSBuild 的發行設定檔。 若要這樣做，當您建立專案時，請使用下列命令：

[!code-console[Main](whats-new-in-aspnet-45-and-visual-studio-2012/samples/sample36.cmd)]

專案 .csproj 值是專案的路徑，而 ProfileName 則是要發行的設定檔名稱。 或者，您可以傳遞發行設定檔的完整路徑，而不是傳遞 *PublishProfile* 屬性的設定檔名稱。

<a id="_Toc318097427"></a>
#### <a name="aspnet-precompilation-and-merge"></a>ASP.NET 先行編譯和合併

針對 Web 應用程式專案，Visual Studio 2012 候選版會在 [封裝/發佈 Web 屬性] 頁面上加入選項，可讓您在發行或封裝專案時先行編譯和合併網站的內容。 若要查看這些選項，請在方案總管中的專案上按一下滑鼠右鍵，選擇 [屬性]，然後選擇 [封裝/發行 Web] 屬性頁。 下圖顯示在發佈選項之前先行編譯此應用程式。

![](whats-new-in-aspnet-45-and-visual-studio-2012/_static/image6.jpg)

選取此選項時，Visual Studio 會在您發行或封裝 web 應用程式時，預先編譯應用程式。 如果您想要控制如何先行編譯網站或合併元件的方式，請按一下 [Advanced] 按鈕來設定這些選項。

<a id="_Toc318097428"></a>
### <a name="iis-express"></a>IIS Express

現在會 IIS Express Visual Studio 中用於測試 Web 專案的預設 web 伺服器。 在開發期間，Visual Studio 程式開發伺服器仍然是本機網頁伺服器的選項，但是 IIS Express 現在是建議的伺服器。 在 Visual Studio 11 Beta 版中使用 IIS Express 的經驗，與在 Visual Studio 2010 SP1 中使用很類似。

<a id="_Toc318097429"></a>
## <a name="disclaimer"></a>免責聲明

這是一份初稿，內容在本文所述的軟體於正式商業發行前都可能有所更動。

本文件所含的資訊代表 Microsoft Corporation 在發行日當下對問題的看法。 由於 Microsoft 必須因應不斷變化的市場狀況，因此不應將此解讀為 Microsoft 方面所作出的承諾，且 Microsoft 也無法保證在發行日之後所提出任何資訊的正確性。

本技術白皮書僅供參考。 MICROSOFT 對本文件中的資訊不提供任何明示、暗示或法定擔保。

遵守所有適用之著作權法係使用者的責任。 在不限制任何依著作權本得享有之權利，未經 Microsoft Corporation 書面許可， 貴用戶不得為任何目的使用任何形式或方法 (電子形式、機械形式、影印、記錄或其他方式) 複製或傳送本文件的任何部份，也不得將本文件的任何部份儲存或放入檢索系統 (a retrieval system)。

在本文件所提述之內容中，可能包括 Microsoft 的專利、申請專利案件、商標、著作權，或其他智慧財產權等。 除非於 Microsoft 提出的任何書面授權條約中明確規定者外，提供本文件並不表示賦予台端上述專利、商標、著作權或其他智慧財產權等之任何授權。

除非另有說明，否則此處所描述的範例公司、組織、產品、功能變數名稱、電子郵件地址、標誌、人員、地點及事件均屬虛構，且不會與任何真實的公司、組織、產品、功能變數名稱、電子郵件地址、標誌、人員、地點或事件相關。

(C) 2012 Microsoft Corporation. 著作權所有，並保留一切權利。

Microsoft 和 Windows 是 Microsoft Corporation 在美國及/或其他國家/地區的註冊商標或商標。

本文件中所提實際公司和產品，可能為各所有人所有之商標。
