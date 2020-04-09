---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: ASP.NET Web API 2 中的全域錯誤處理 - ASP.NET 4.x
author: davidmatson
description: ASP.NET 4.x ASP.NET Web API 2 中的全域錯誤處理概述。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 5ff54d2e4ed881ce927d0a401fb79d9b8bc5b8a1
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675421"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的全域錯誤處理

由[大衛·馬特森](https://github.com/davidmatson),[里克·安德森](https://twitter.com/RickAndMSFT)

本主題概述了ASP.NET web API 2 中針對ASP.NET 4.x 的全域錯誤處理。 如今,Web API 中沒有簡單的方法來全域記錄或處理錯誤。 某些未處理的異常可以通過[異常篩選器](exception-handling.md)進行處理,但有許多異常篩選器無法處理的情況。 例如：

1. 從控制器建構函式擲回的例外狀況。
2. 從訊息處理常式擲回的例外狀況。
3. 在路由期間擲回的例外狀況。
4. 在回應內容序列化期間擲回的例外狀況。

我們希望提供一種簡單、一致的方式來記錄和處理這些異常(如果可能)。 

處理異常有兩個主要情況,即我們能夠發送錯誤回應的情況,以及我們所能做的就是記錄異常的情況。 后一種情況的一個示例是在流式回應內容中間引發異常時;在流式回應內容中引發異常時,則為後一種情況。在這種情況下,發送新的回應消息為時已晚,因為狀態代碼、標頭和部分內容已經通過導線,因此我們只需中止連接即可。 即使無法處理異常以生成新的回應消息,我們仍支持記錄異常。 在可以檢測到錯誤的情況下,我們可以返回適當的錯誤回應,如下所示:

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>現有選項

除了[異常篩選器](exception-handling.md)之外,[消息處理程式](../advanced/http-message-handlers.md)今天還可用於觀察所有 500 級回應,但對這些回應進行操作很困難,因為它們缺少有關原始錯誤的上下文。 消息處理程式也有一些與異常篩選器相同的限制,涉及它們可以處理的情況。 雖然 Web API 確實具有捕獲錯誤條件的追蹤基礎結構,但追蹤基礎結構用於診斷目的,並且不適合在生產環境中運行。 全域異常處理和日誌記錄應該是可在生產期間運行並插入現有監視解決方案(例如[ELMAH)](https://code.google.com/p/elmah/)的服務。

### <a name="solution-overview"></a>方案概觀

 我們提供兩種新的用戶可替換服務[,IexceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md)和IexceptionHandler,用於記錄和處理未處理的異常。 服務非常相似,主要有兩個區別:

1. 我們支援註冊多個異常記錄器,但僅支援單個異常處理程式。
2. 異常記錄器總是被調用,即使我們即將中止連接。 只有在我們仍可以選擇要發送的回應消息時,才會調用異常處理程式。

這兩個服務都提供從檢測到異常點包含相關信息的異常上下文的訪問,特別是[HttpRequestMessage、HttpRequestContext、](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx)引發異常和異常源(詳情見下文[HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx))。

### <a name="design-principles"></a>設計原則

1. **沒有變更**由於此功能是在次要版本中添加的,因此影響解決方案的一個重要約束是,對於類型協定或行為,沒有重大更改。 此約束排除了我們希望在現有 catch 塊方面進行的一些清理,將異常轉換為 500 個回應。 對於後續的主要版本,我們可以考慮此附加清理。 如果這對你很重要,請[ASP.NETWeb API 用戶語音](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)投。
2. **與 Web API 建構保持一致性**Web API 的篩選器管道是處理跨領域問題的絕佳方法,它可靈活地將邏輯應用於特定於操作、特定於控制器或全域的範圍。 篩選器(包括異常篩選器)始終具有操作和控制器上下文,即使在全域作用域中註冊也是如此。 該協定對篩選器有意義,但它意味著異常篩選器(即使是全域範圍篩選器)不適合某些異常處理情況,例如消息處理程序的異常,其中不存在操作或控制器上下文。 如果我們想要使用篩選器提供的靈活範圍來處理異常處理,我們仍然需要異常篩選器。 但是,如果需要在控制器上下文之外處理異常,我們還需要一個單獨的構造來進行完整的全域錯誤處理(沒有控制器上下文和操作上下文約束)。

### <a name="when-to-use"></a>使用時機

- 異常記錄器是查看 Web API 捕獲的所有未處理異常的解決方案。
- 異常處理程式是自訂 Web API 捕獲的未處理異常的所有可能回應的解決方案。
- 異常篩選器是處理與特定操作或控制器相關的子集未處理異常的最簡單解決方案。

### <a name="service-details"></a>服務詳細資料

 例外紀錄器與處理程式服務介面是採用相應上下文的簡單非同步方法: 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 我們還為這兩個介面提供基類。 重寫核心(同步或非同步)方法是在建議的時間記錄或處理所需的全部方法。 對於日誌記錄,`ExceptionLogger`基類將確保每個異常只調用一次核心日誌記錄方法(即使它稍後在調用堆棧上傳播並進一步傳播並再次捕獲)。 基`ExceptionHandler`類將僅針對調用堆疊頂部的異常調用核心處理方法,而忽略舊嵌套 catch 塊。 (這些基類的簡化版本見下面的附錄。與`IExceptionLogger``IExceptionHandler`都透過接收有關的`ExceptionContext`資訊 。

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

當框架呼叫例外紀錄器或例外處理程式時,它會始終提供與`Exception` `Request` 。 除了單元測試外,它還會始終提供`RequestContext`。 它很少提供`ControllerContext``ActionContext`和 (僅在從異常篩選器的 catch 塊調用時)。 它很少提供`Response`(僅在某些 IIS 情況下,當嘗試編寫回應時)。 請注意,由於其中一些屬性可能`null`由消費者在訪問異常類的`null`成員 之前進行檢查。`CatchBlock` 是指示哪個 catch 塊看到異常的字串。 catch 塊字串如下所示:

- HttpServer(傳送同步方法)
- HTTPController 調度程式 (傳送同步方法)
- HTTPBatchhandler(傳送同步方法)
- IExceptionFilter(ApiController 在 ExecuteAsync 中處理異常篩選器導管)
- OWIN 主機:

    - HTTPMessageHandlerAdapter.緩衝區回應內容同步(用於緩衝輸出)
    - HTTPMessageHandlerAdapter.複製回應內容同步(用於流式處理輸出)
- 網路主機:

    - HTTPControllerHandler.寫入緩衝回應內容同步(用於緩衝輸出)
    - HTTPControllerHandler.寫入流式回應內容同步(用於流式處理輸出)
    - HTTPControllerHandler.寫入錯誤回應內容同步(對於緩衝輸出模式下錯誤復原失敗)

catch 塊字串的清單也可通過靜態唯讀屬性提供。 (核心 catch 塊字串位於靜態異常捕獲塊上;其餘字串出現在一個靜態類中,每個靜態類用於 OWIN 和 Web 主機)。`IsTopLevelCatchBlock` 有助於遵循僅在調用堆疊頂部處理異常的建議模式。 異常處理程式可以允許異常傳播到主機即將看到之前,而不是將異常轉換為 500 個回應。

除了`ExceptionContext`, 記錄器`ExceptionLoggerContext`通過完整 獲取了一條資訊:

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

第二個屬性`CanBeHandled`允許記錄器標識無法處理的異常。 當連線即將中止,並且無法傳送新的回應訊息時,將呼叫紀錄器,但不會呼叫處理程式,並且記錄器可以從此屬性識別此***not***方案 。

在`ExceptionContext`除 中,處理程式還可以獲取一個可以設置在`ExceptionHandlerContext`full 上處理異常的屬性:

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

`Result`例外處理程式透過設定為操作結果(例如,[異常結果](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx),[內部伺服器錯誤結果](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx),[狀態代碼結果](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)或自訂結果)來指示它已處理異常。 如果`Result`屬性為 null,則異常將未處理,並且將重新引發原始異常。

對於調用堆疊頂部的異常,我們採取了額外的步驟,以確保回應適合 API 調用方。 如果異常傳播到主機,調用方將看到死亡黃色螢幕或其他一些主機提供的回應,這些回應通常是 HTML,通常不是適當的 API 錯誤回應。 在這些情況下,結果開始為非空,只有當自定義異常處理程式顯式將其設置回`null`(未處理)時,異常才會傳播到主機。 在這種情況下`Result`,`null`設定為 可用於以下兩種情況:

1. OWIN 託管 Web API,具有在 Web API 之前 / 外部註冊的自訂異常處理中間件。
2. 通過瀏覽器進行本地調試,其中死亡黃色螢幕實際上是對未處理異常的有用回應。

對於異常記錄器和異常處理程式,如果記錄器或處理程式本身引發異常,則不執行任何恢復操作。 (除了讓異常傳播外,如果您有更好的方法,請將反饋保留在此頁面的底部。異常記錄器和處理程式的協定是,它們不應讓異常傳播到其調用方;否則,異常將只傳播到主機,導致 HTML 錯誤(如 ASP)。NET 的黃色螢幕)被發送回用戶端(對於希望 JSON 或 XML 的 API 調用方來說,這通常不是首選選項)。

## <a name="examples"></a>範例

### <a name="tracing-exception-logger"></a>追蹤例外記錄器

下面的異常記錄器將異常數據發送到配置的跟蹤源(包括 Visual Studio 中的調試輸出視窗)。

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>自訂錯誤訊息異常處理程式

下面的異常處理程式生成對用戶端的自定義錯誤回應,包括用於聯繫支援的電子郵寄地址。

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>註冊例外篩選器

如果使用「ASP.NET MVC 4 Web 應用程式」專案範本建立專案,請將`WebApiConfig`Web API 設定代碼 放入類別中,放入*App_Start*資料夾中:

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>附錄:基本課程詳細資訊

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
