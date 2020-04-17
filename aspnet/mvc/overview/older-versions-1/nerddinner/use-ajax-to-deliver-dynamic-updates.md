---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: 使用 AJAX 提供動態更新 |微軟文件
author: rick-anderson
description: 步驟 10 支援登錄使用者 RSVP,他們有興趣參加晚宴,使用基於 Ajax 的方法集成在晚餐詳細資訊中...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541243"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a>使用 AJAX 傳送動態更新

由[微軟](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第10步,該教學示範如何使用ASP.NETmVC 1構建小型但完整的Web應用程式。
> 
> 步驟 10 使用在晚餐詳細資訊頁中集成的基於 Ajax 的方法,實現對登錄使用者的支援,以便 RSVP 讓他們對參加晚宴感興趣。
> 
> 如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>神經晚餐步驟 10: AJAX 啟用 RSV 接受

現在,讓我們對登錄用戶實施支援,以便 RSVP 對參加晚宴感興趣。 我們將使用在晚餐詳細資訊頁中集成的基於 AJAX 的方法啟用此功能。

### <a name="indicating-whether-the-user-is-rsvpd"></a>指示使用者是否為 RSVP'd

使用者可以造訪 */Dinners/詳細資訊/[id]* 網址 以查看有關特定晚餐的詳細資訊:

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

詳細資訊()操作方法的實現方式是這樣的:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

實現 RSVP 支援的第一步是向我們的 Dinner 物件(在之前構建的 Dinner.cs 部分類中)添加「IsUser 註冊(使用者名)」幫助器方法。 此說明程式方法傳回 true 或 false,具體取決於使用者當前是晚餐的 RSVP d:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

然後,我們可以向 Details.aspx 檢視範本添加以下代碼,以顯示指示使用者是否已註冊的事件的適當消息:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

現在,當使用者訪問他們註冊的晚餐時,他們會看到此消息:

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

當他們訪問晚餐時,他們沒有註冊,他們會看到以下消息:

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>實現寄存器操作方法

現在,讓我們添加必要的功能,使用戶能夠從詳細資訊頁面到 RSVP 共進晚餐。

為了實現這一點,我們將通過右鍵單擊 \控制器目錄並選擇"添加控制&gt;器 "功能表命令創建新的"RSVPController"類。

我們將在新的 RSVPController 類中實現「註冊」操作方法,該方法以 Dinner 的 ID 作為參數,檢索相應的 Dinner 物件,檢查登錄使用者當前是否位於已註冊的使用者清單中,如果沒有為其添加 RSVP 物件:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

請注意,我們如何返回一個簡單的字串作為操作方法的輸出。 我們本可以將此消息嵌入到視圖範本中,但由於它非常小,我們只需在控制器基類上使用 Content() 幫助器方法,並返回如下所示的字串消息。

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>使用 AJAX 呼叫 RSVPForEvent 操作方法

我們將使用 AJAX 從「詳細資訊」檢視中調用註冊操作方法。 實現這一點非常簡單。 首先,我們將添加兩個腳本庫引用:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

第一個庫引用 ASP.NET AJAX 用戶端文本庫的核心。 此檔的大小約為 24k(壓縮),包含核心用戶端 AJAX 功能。 第二個庫包含與ASP.NET MVC 的內建 AJAX 幫助器方法集成的實用程式函數(我們稍後會使用)。

然後,我們可以更新我們之前添加的檢視範本代碼,以便我們不是提供"您未註冊此事件"消息,而是呈現一個連結,當推送時執行 AJAX 調用時,該連結會調用我們的 RSVPForEvent 操作方法,並在使用者中調用 RSVP:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

上面使用的Ajax.ActionLink() 幫助器方法內置於mVCASP.NET,與 Html.ActionLink() 説明器方法類似,只不過,在單擊連結時,它不是執行標準導航,而是對操作方法發出 AJAX 調用。 上面我們調用"RSVP"控制器上的"註冊"操作方法,並將 DinnerID 作為"id"參數傳遞給它。 我們傳遞的最終 AjaxOptions 參數表示,我們希望獲取從操作方法返回的內容,並更新 ID 為"rsvpmsg"&lt;的頁面&gt;上的 HTML div 元素。

現在,當用戶流覽到尚未註冊的晚餐時,他們會看到指向 RSVP 的連結:

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

如果他們按下「此事件的 RSVP」連結,他們將對 RSVP 控制器上的註冊操作方法進行 AJAX 調用,並且當它完成後,他們將看到如下更新的消息:

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

進行此 AJAX 調用時所涉及的網路頻寬和流量非常輕量。 當使用者按下「此事件的 RSVP」連結時,將針對線上路上如下所示的 */Dinners/Register/1* URL 發出小型 HTTP POST 網路請求:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

我們的註冊操作方法的回應很簡單:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

此輕量級呼叫速度很快,即使在速度較慢的網路上也能正常工作。

### <a name="adding-a-jquery-animation"></a>新增 jQuery 動畫

我們實現的AJAX功能工作良好,速度快。 但是,有時發生得如此之快,以至於使用者可能沒有注意到 RSVP 連結已被新文本替換。 為了使結果更加明顯一點,我們可以添加一個簡單的動畫來吸引對更新消息的注意。

預設ASP.NET MVC 專案範本包括 jQuery - 一個出色的(非常受歡迎的)開源 JavaScript 庫,也受 Microsoft 支援。 jQuery 提供了許多功能,包括不錯的 HTML DOM 選擇和效果庫。

要使用 jQuery,我們將首先向其添加腳本引用。 由於我們將在網站內的各種位置使用 jQuery,因此我們將在 Site.master 頁面檔中添加文本引用,以便所有頁面都可以使用它。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*提示:請確保您已為 VS 2008 SP1 安裝了 JavaScript 智慧感知修補程式,從而能夠對 JavaScript 檔(包括 jQuery)提供更豐富的對講義支援。您可以透過以下位置下載:http://tinyurl.com/vs2008javascripthotfix*

使用 JQuery 編寫的代碼通常使用全域"$()"JavaScript 方法,該方法使用 CSS 選擇器檢索一個或多個 HTML 元素。 例如 *,$("#rsvpmsg")* 選擇任何具有 rsvpmsg ID 的 HTML 元素,而 *$(".某事")* 將選擇具有「某物」CSS 類名稱的所有元素。 您還可以使用選擇器查詢編寫更高級的查詢,如"返回所有已檢查的單選按鈕",例如 *:$("輸入="@type收音機**)"。@checked *

選擇元素后,可以調用方法對它們執行操作,例如隱藏它們 *:$("#rsvpmsg")。"隱藏";*

對於我們的 RSVP 方案,我們將定義一個名為"AnimateRSVPMessage"的簡單 JavaScript 函數,該函數選擇"rsvpmsg"div&lt;&gt;並為其文本內容的大小設置動畫。 下面的代碼將文字啟動較小,然後使其在 400 毫秒的時間內增加:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

然後,我們可以透過將其名稱傳遞給我們的Ajax.ActionLink() 幫助器方法(透過AjaxOptions"OnSuccess"事件屬性)來連接此 JavaScript 函數,以在 AJAX 調用成功完成後呼叫它:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

現在,當單擊「此事件的 RSVP」連結並成功完成我們的 AJAX 呼叫時,發回的內容消息將設置動畫並變大:

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

除了提供"On成功"事件外,AjaxOptions 物件還公開了您可以處理的 OnBegin、OnOn 失敗和 OnComplete 事件(以及各種其他屬性和有用的選項)。

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>清除 - 重構 RSVP 部份檢視

我們的詳細信息視圖範本開始變得有點長,加班會使它很難理解。 為了説明提高代碼的可讀性,讓我們通過創建一個部分檢視 ( RSVPStatus.ascx) 來完成,該視圖封裝了我們詳細資訊頁的所有 RSVP 視圖代碼。

我們可以通過右鍵按下 [Views_Dinners] 資料夾,然後選擇"&gt;添加- 視圖"功能表命令來執行此操作。 我們將它採用晚餐物件作為其強類型視圖模型。 然後,我們可以複製/粘貼從我們的細節.aspx 視圖的 RSVP 內容到它。

完成此操作後,我們還要創建另一個部分檢視 - EditAndDeleteLinks.ascx - 封裝我們的"編輯"和"刪除"鏈接檢視代碼。 我們還將它將一個 Dinner 物件作為其強類型視圖模型,並將"編輯"和"刪除"邏輯從"詳細資訊.aspx"視圖中複製/粘貼到該物件中。

然後,我們的詳細資訊檢視範本可以只包括底部的兩個 Html.Render 部分() 方法調用:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

這使得代碼的讀取和維護更簡潔。

### <a name="next-step"></a>後續步驟

現在,讓我們來看看如何進一步使用AJAX,並將互動式映射支援添加到我們的應用程式。

> [!div class="step-by-step"]
> [前一個](secure-applications-using-authentication-and-authorization.md)
> [下一個](use-ajax-to-implement-mapping-scenarios.md)
