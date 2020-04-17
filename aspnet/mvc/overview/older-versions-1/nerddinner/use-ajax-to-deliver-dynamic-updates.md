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
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="11ff7-103">使用 AJAX 傳送動態更新</span><span class="sxs-lookup"><span data-stu-id="11ff7-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="11ff7-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="11ff7-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="11ff7-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="11ff7-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="11ff7-106">這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第10步,該教學示範如何使用ASP.NETmVC 1構建小型但完整的Web應用程式。</span><span class="sxs-lookup"><span data-stu-id="11ff7-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="11ff7-107">步驟 10 使用在晚餐詳細資訊頁中集成的基於 Ajax 的方法,實現對登錄使用者的支援,以便 RSVP 讓他們對參加晚宴感興趣。</span><span class="sxs-lookup"><span data-stu-id="11ff7-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="11ff7-108">如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。</span><span class="sxs-lookup"><span data-stu-id="11ff7-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="11ff7-109">神經晚餐步驟 10: AJAX 啟用 RSV 接受</span><span class="sxs-lookup"><span data-stu-id="11ff7-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="11ff7-110">現在,讓我們對登錄用戶實施支援,以便 RSVP 對參加晚宴感興趣。</span><span class="sxs-lookup"><span data-stu-id="11ff7-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="11ff7-111">我們將使用在晚餐詳細資訊頁中集成的基於 AJAX 的方法啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="11ff7-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="11ff7-112">指示使用者是否為 RSVP'd</span><span class="sxs-lookup"><span data-stu-id="11ff7-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="11ff7-113">使用者可以造訪 */Dinners/詳細資訊/[id]* 網址 以查看有關特定晚餐的詳細資訊:</span><span class="sxs-lookup"><span data-stu-id="11ff7-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="11ff7-114">詳細資訊()操作方法的實現方式是這樣的:</span><span class="sxs-lookup"><span data-stu-id="11ff7-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="11ff7-115">實現 RSVP 支援的第一步是向我們的 Dinner 物件(在之前構建的 Dinner.cs 部分類中)添加「IsUser 註冊(使用者名)」幫助器方法。</span><span class="sxs-lookup"><span data-stu-id="11ff7-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="11ff7-116">此說明程式方法傳回 true 或 false,具體取決於使用者當前是晚餐的 RSVP d:</span><span class="sxs-lookup"><span data-stu-id="11ff7-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="11ff7-117">然後,我們可以向 Details.aspx 檢視範本添加以下代碼,以顯示指示使用者是否已註冊的事件的適當消息:</span><span class="sxs-lookup"><span data-stu-id="11ff7-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="11ff7-118">現在,當使用者訪問他們註冊的晚餐時,他們會看到此消息:</span><span class="sxs-lookup"><span data-stu-id="11ff7-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="11ff7-119">當他們訪問晚餐時,他們沒有註冊,他們會看到以下消息:</span><span class="sxs-lookup"><span data-stu-id="11ff7-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="11ff7-120">實現寄存器操作方法</span><span class="sxs-lookup"><span data-stu-id="11ff7-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="11ff7-121">現在,讓我們添加必要的功能,使用戶能夠從詳細資訊頁面到 RSVP 共進晚餐。</span><span class="sxs-lookup"><span data-stu-id="11ff7-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="11ff7-122">為了實現這一點,我們將通過右鍵單擊 \控制器目錄並選擇"添加控制&gt;器 "功能表命令創建新的"RSVPController"類。</span><span class="sxs-lookup"><span data-stu-id="11ff7-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="11ff7-123">我們將在新的 RSVPController 類中實現「註冊」操作方法,該方法以 Dinner 的 ID 作為參數,檢索相應的 Dinner 物件,檢查登錄使用者當前是否位於已註冊的使用者清單中,如果沒有為其添加 RSVP 物件:</span><span class="sxs-lookup"><span data-stu-id="11ff7-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="11ff7-124">請注意,我們如何返回一個簡單的字串作為操作方法的輸出。</span><span class="sxs-lookup"><span data-stu-id="11ff7-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="11ff7-125">我們本可以將此消息嵌入到視圖範本中,但由於它非常小,我們只需在控制器基類上使用 Content() 幫助器方法,並返回如下所示的字串消息。</span><span class="sxs-lookup"><span data-stu-id="11ff7-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="11ff7-126">使用 AJAX 呼叫 RSVPForEvent 操作方法</span><span class="sxs-lookup"><span data-stu-id="11ff7-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="11ff7-127">我們將使用 AJAX 從「詳細資訊」檢視中調用註冊操作方法。</span><span class="sxs-lookup"><span data-stu-id="11ff7-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="11ff7-128">實現這一點非常簡單。</span><span class="sxs-lookup"><span data-stu-id="11ff7-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="11ff7-129">首先,我們將添加兩個腳本庫引用:</span><span class="sxs-lookup"><span data-stu-id="11ff7-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="11ff7-130">第一個庫引用 ASP.NET AJAX 用戶端文本庫的核心。</span><span class="sxs-lookup"><span data-stu-id="11ff7-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="11ff7-131">此檔的大小約為 24k(壓縮),包含核心用戶端 AJAX 功能。</span><span class="sxs-lookup"><span data-stu-id="11ff7-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="11ff7-132">第二個庫包含與ASP.NET MVC 的內建 AJAX 幫助器方法集成的實用程式函數(我們稍後會使用)。</span><span class="sxs-lookup"><span data-stu-id="11ff7-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="11ff7-133">然後,我們可以更新我們之前添加的檢視範本代碼,以便我們不是提供"您未註冊此事件"消息,而是呈現一個連結,當推送時執行 AJAX 調用時,該連結會調用我們的 RSVPForEvent 操作方法,並在使用者中調用 RSVP:</span><span class="sxs-lookup"><span data-stu-id="11ff7-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="11ff7-134">上面使用的Ajax.ActionLink() 幫助器方法內置於mVCASP.NET,與 Html.ActionLink() 説明器方法類似,只不過,在單擊連結時,它不是執行標準導航,而是對操作方法發出 AJAX 調用。</span><span class="sxs-lookup"><span data-stu-id="11ff7-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="11ff7-135">上面我們調用"RSVP"控制器上的"註冊"操作方法,並將 DinnerID 作為"id"參數傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="11ff7-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="11ff7-136">我們傳遞的最終 AjaxOptions 參數表示,我們希望獲取從操作方法返回的內容,並更新 ID 為"rsvpmsg"&lt;的頁面&gt;上的 HTML div 元素。</span><span class="sxs-lookup"><span data-stu-id="11ff7-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="11ff7-137">現在,當用戶流覽到尚未註冊的晚餐時,他們會看到指向 RSVP 的連結:</span><span class="sxs-lookup"><span data-stu-id="11ff7-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="11ff7-138">如果他們按下「此事件的 RSVP」連結,他們將對 RSVP 控制器上的註冊操作方法進行 AJAX 調用,並且當它完成後,他們將看到如下更新的消息:</span><span class="sxs-lookup"><span data-stu-id="11ff7-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="11ff7-139">進行此 AJAX 調用時所涉及的網路頻寬和流量非常輕量。</span><span class="sxs-lookup"><span data-stu-id="11ff7-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="11ff7-140">當使用者按下「此事件的 RSVP」連結時,將針對線上路上如下所示的 */Dinners/Register/1* URL 發出小型 HTTP POST 網路請求:</span><span class="sxs-lookup"><span data-stu-id="11ff7-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="11ff7-141">我們的註冊操作方法的回應很簡單:</span><span class="sxs-lookup"><span data-stu-id="11ff7-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="11ff7-142">此輕量級呼叫速度很快,即使在速度較慢的網路上也能正常工作。</span><span class="sxs-lookup"><span data-stu-id="11ff7-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="11ff7-143">新增 jQuery 動畫</span><span class="sxs-lookup"><span data-stu-id="11ff7-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="11ff7-144">我們實現的AJAX功能工作良好,速度快。</span><span class="sxs-lookup"><span data-stu-id="11ff7-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="11ff7-145">但是,有時發生得如此之快,以至於使用者可能沒有注意到 RSVP 連結已被新文本替換。</span><span class="sxs-lookup"><span data-stu-id="11ff7-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="11ff7-146">為了使結果更加明顯一點,我們可以添加一個簡單的動畫來吸引對更新消息的注意。</span><span class="sxs-lookup"><span data-stu-id="11ff7-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="11ff7-147">預設ASP.NET MVC 專案範本包括 jQuery - 一個出色的(非常受歡迎的)開源 JavaScript 庫,也受 Microsoft 支援。</span><span class="sxs-lookup"><span data-stu-id="11ff7-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="11ff7-148">jQuery 提供了許多功能,包括不錯的 HTML DOM 選擇和效果庫。</span><span class="sxs-lookup"><span data-stu-id="11ff7-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="11ff7-149">要使用 jQuery,我們將首先向其添加腳本引用。</span><span class="sxs-lookup"><span data-stu-id="11ff7-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="11ff7-150">由於我們將在網站內的各種位置使用 jQuery,因此我們將在 Site.master 頁面檔中添加文本引用,以便所有頁面都可以使用它。</span><span class="sxs-lookup"><span data-stu-id="11ff7-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="11ff7-151">*提示:請確保您已為 VS 2008 SP1 安裝了 JavaScript 智慧感知修補程式,從而能夠對 JavaScript 檔(包括 jQuery)提供更豐富的對講義支援。您可以透過以下位置下載:http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="11ff7-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="11ff7-152">使用 JQuery 編寫的代碼通常使用全域"$()"JavaScript 方法,該方法使用 CSS 選擇器檢索一個或多個 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="11ff7-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="11ff7-153">例如 *,$("#rsvpmsg")* 選擇任何具有 rsvpmsg ID 的 HTML 元素,而 *$(".某事")* 將選擇具有「某物」CSS 類名稱的所有元素。</span><span class="sxs-lookup"><span data-stu-id="11ff7-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="11ff7-154">您還可以使用選擇器查詢編寫更高級的查詢,如"返回所有已檢查的單選按鈕",例如 \*:$("輸入="@type收音機\*\*)"。@checked \*</span><span class="sxs-lookup"><span data-stu-id="11ff7-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="11ff7-155">選擇元素后,可以調用方法對它們執行操作,例如隱藏它們 *:$("#rsvpmsg")。"隱藏";*</span><span class="sxs-lookup"><span data-stu-id="11ff7-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="11ff7-156">對於我們的 RSVP 方案,我們將定義一個名為"AnimateRSVPMessage"的簡單 JavaScript 函數,該函數選擇"rsvpmsg"div&lt;&gt;並為其文本內容的大小設置動畫。</span><span class="sxs-lookup"><span data-stu-id="11ff7-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="11ff7-157">下面的代碼將文字啟動較小,然後使其在 400 毫秒的時間內增加:</span><span class="sxs-lookup"><span data-stu-id="11ff7-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="11ff7-158">然後,我們可以透過將其名稱傳遞給我們的Ajax.ActionLink() 幫助器方法(透過AjaxOptions"OnSuccess"事件屬性)來連接此 JavaScript 函數,以在 AJAX 調用成功完成後呼叫它:</span><span class="sxs-lookup"><span data-stu-id="11ff7-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="11ff7-159">現在,當單擊「此事件的 RSVP」連結並成功完成我們的 AJAX 呼叫時,發回的內容消息將設置動畫並變大:</span><span class="sxs-lookup"><span data-stu-id="11ff7-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="11ff7-160">除了提供"On成功"事件外,AjaxOptions 物件還公開了您可以處理的 OnBegin、OnOn 失敗和 OnComplete 事件(以及各種其他屬性和有用的選項)。</span><span class="sxs-lookup"><span data-stu-id="11ff7-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="11ff7-161">清除 - 重構 RSVP 部份檢視</span><span class="sxs-lookup"><span data-stu-id="11ff7-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="11ff7-162">我們的詳細信息視圖範本開始變得有點長,加班會使它很難理解。</span><span class="sxs-lookup"><span data-stu-id="11ff7-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="11ff7-163">為了説明提高代碼的可讀性,讓我們通過創建一個部分檢視 ( RSVPStatus.ascx) 來完成,該視圖封裝了我們詳細資訊頁的所有 RSVP 視圖代碼。</span><span class="sxs-lookup"><span data-stu-id="11ff7-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="11ff7-164">我們可以通過右鍵按下 [Views_Dinners] 資料夾,然後選擇"&gt;添加- 視圖"功能表命令來執行此操作。</span><span class="sxs-lookup"><span data-stu-id="11ff7-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="11ff7-165">我們將它採用晚餐物件作為其強類型視圖模型。</span><span class="sxs-lookup"><span data-stu-id="11ff7-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="11ff7-166">然後,我們可以複製/粘貼從我們的細節.aspx 視圖的 RSVP 內容到它。</span><span class="sxs-lookup"><span data-stu-id="11ff7-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="11ff7-167">完成此操作後,我們還要創建另一個部分檢視 - EditAndDeleteLinks.ascx - 封裝我們的"編輯"和"刪除"鏈接檢視代碼。</span><span class="sxs-lookup"><span data-stu-id="11ff7-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="11ff7-168">我們還將它將一個 Dinner 物件作為其強類型視圖模型,並將"編輯"和"刪除"邏輯從"詳細資訊.aspx"視圖中複製/粘貼到該物件中。</span><span class="sxs-lookup"><span data-stu-id="11ff7-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="11ff7-169">然後,我們的詳細資訊檢視範本可以只包括底部的兩個 Html.Render 部分() 方法調用:</span><span class="sxs-lookup"><span data-stu-id="11ff7-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="11ff7-170">這使得代碼的讀取和維護更簡潔。</span><span class="sxs-lookup"><span data-stu-id="11ff7-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="11ff7-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11ff7-171">Next Step</span></span>

<span data-ttu-id="11ff7-172">現在,讓我們來看看如何進一步使用AJAX,並將互動式映射支援添加到我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="11ff7-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="11ff7-173">[前一個](secure-applications-using-authentication-and-authorization.md)
> [下一個](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="11ff7-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
