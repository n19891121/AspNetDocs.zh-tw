---
uid: webhooks/receiving/handlers
title: ASP.NET WebHook 處理程式 |微軟文件
author: rick-anderson
description: 如何處理ASP.NET WebHook 中的請求。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: a55b0d20-9c90-4bd3-a471-20da6f569f0c
ms.openlocfilehash: ff12dd8df167eca17ecbd9f03a71807d44af2b30
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675222"
---
# <a name="aspnet-webhooks-handlers"></a><span data-ttu-id="2da5e-103">ASP.NET WebHook 處理程式</span><span class="sxs-lookup"><span data-stu-id="2da5e-103">ASP.NET WebHooks handlers</span></span>

<span data-ttu-id="2da5e-104">WebHooks 請求由 WebHook 接收器驗證後,即可由使用者代碼處理。</span><span class="sxs-lookup"><span data-stu-id="2da5e-104">Once WebHooks requests has been validated by a WebHook receiver, it is ready to be processed by user code.</span></span> <span data-ttu-id="2da5e-105">這是*處理程式*的來向。</span><span class="sxs-lookup"><span data-stu-id="2da5e-105">This is where *handlers* come in.</span></span> <span data-ttu-id="2da5e-106">處理程式派生自[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)介面,但通常使用[WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)類,而不是直接從該介面派生。</span><span class="sxs-lookup"><span data-stu-id="2da5e-106">Handlers derive from the [IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) interface but typically uses the [WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs) class instead of deriving directly from the interface.</span></span>

<span data-ttu-id="2da5e-107">WebHook 請求可以由一個或多個處理程序處理。</span><span class="sxs-lookup"><span data-stu-id="2da5e-107">A WebHook request can be processed by one or more handlers.</span></span> <span data-ttu-id="2da5e-108">處理程式根據各自的*Order*屬性從最低到最高的順序調用,其中 Order 是一個簡單的整數(建議介於 1 和 100 之間):</span><span class="sxs-lookup"><span data-stu-id="2da5e-108">Handlers are called in order based on their respective *Order* property going from lowest to highest where Order is a simple integer (suggested to be between 1 and 100):</span></span>

![WebHook 處理程式順序屬性圖](_static/Handlers.png)

<span data-ttu-id="2da5e-110">處理程式可以選擇在 WebHookHandlerContext 上設定*回應*屬性,這將導致處理停止,並將回應作為對 WebHook 的 HTTP 回應發送回來。</span><span class="sxs-lookup"><span data-stu-id="2da5e-110">A handler can optionally set the *Response* property on the WebHookHandlerContext which will lead the processing to stop and the response to be sent back as the HTTP response to the WebHook.</span></span> <span data-ttu-id="2da5e-111">在上面的案例中,不會調用處理程式 C,因為它的順序高於 B,B 設置回應。</span><span class="sxs-lookup"><span data-stu-id="2da5e-111">In the case above, Handler C won't get called because it has a higher order than B and B sets the response.</span></span>

<span data-ttu-id="2da5e-112">設置回應通常只與 WebHook 相關,回應可以將資訊回源 API。</span><span class="sxs-lookup"><span data-stu-id="2da5e-112">Setting the response is typically only relevant for WebHooks where the response can carry information back to the originating API.</span></span> <span data-ttu-id="2da5e-113">例如,Slack WebHooks 的回應被發回 WebHook 的通道。</span><span class="sxs-lookup"><span data-stu-id="2da5e-113">This is for example the case with Slack WebHooks where the response is posted back to the channel where the WebHook came from.</span></span> <span data-ttu-id="2da5e-114">如果處理程式只想從該特定接收器接收 WebHook,則可以設置 Receiver 屬性。</span><span class="sxs-lookup"><span data-stu-id="2da5e-114">Handlers can set the Receiver property if they only want to receive WebHooks from that particular receiver.</span></span> <span data-ttu-id="2da5e-115">如果他們不設置接收器,他們被要求所有這些。</span><span class="sxs-lookup"><span data-stu-id="2da5e-115">If they don't set the receiver they are called for all of them.</span></span>

<span data-ttu-id="2da5e-116">回應的另一個常見用途是使用*410 Gone*回應來指示 WebHook 不再處於活動狀態,並且不應提交進一步的請求。</span><span class="sxs-lookup"><span data-stu-id="2da5e-116">One other common use of a response is to use a *410 Gone* response to indicate that the WebHook no longer is active and no further requests should be submitted.</span></span>

<span data-ttu-id="2da5e-117">默認情況下,所有 WebHook 接收器都將調用處理程式。</span><span class="sxs-lookup"><span data-stu-id="2da5e-117">By default a handler will be called by all WebHook receivers.</span></span> <span data-ttu-id="2da5e-118">但是,如果*Receiver*屬性設置為處理程式的名稱,則該處理程式將僅接收來自該接收者的 WebHook 請求。</span><span class="sxs-lookup"><span data-stu-id="2da5e-118">However, if the *Receiver* property is set to the name of a handler then that handler will only receive WebHook requests from that receiver.</span></span>

## <a name="processing-a-webhook"></a><span data-ttu-id="2da5e-119">處理 WebHook</span><span class="sxs-lookup"><span data-stu-id="2da5e-119">Processing a WebHook</span></span>

<span data-ttu-id="2da5e-120">呼叫處理程式時,它會獲取包含有關 WebHook 請求的資訊的[WebHook 處理程式。](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs)</span><span class="sxs-lookup"><span data-stu-id="2da5e-120">When a handler is called, it gets a [WebHookHandlerContext](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) containing information about the WebHook request.</span></span> <span data-ttu-id="2da5e-121">數據(通常是 HTTP 請求正文)可從*Data*屬性獲得。</span><span class="sxs-lookup"><span data-stu-id="2da5e-121">The data, typically the HTTP request body, is available from the *Data* property.</span></span>

<span data-ttu-id="2da5e-122">數據類型通常是 JSON 或 HTML 表單數據,但如果需要,可以強制轉換為更具體的類型。</span><span class="sxs-lookup"><span data-stu-id="2da5e-122">The type of the data is typically JSON or HTML form data, but it is possible to cast to a more specific type if desired.</span></span> <span data-ttu-id="2da5e-123">例如,ASP.NET WebHooks 生成的自訂 WebHook 可以轉換為[「自訂通知」](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs)類型,如下所示:</span><span class="sxs-lookup"><span data-stu-id="2da5e-123">For example, the custom WebHooks generated by ASP.NET WebHooks can be cast to the type [CustomNotifications](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs) as follows:</span></span>

```csharp
public class MyWebHookHandler : WebHookHandler
{
    public MyWebHookHandler()
    {
        this.Receiver = "custom";
    }

    public override Task ExecuteAsync(string generator, WebHookHandlerContext context)
    {
        CustomNotifications notifications = context.GetDataOrDefault<CustomNotifications>();
        foreach (var notification in notifications.Notifications)
        {
            ...
        }
        return Task.FromResult(true);
    }
}
```

  ## <a name="queued-processing"></a><span data-ttu-id="2da5e-124">佇列處理</span><span class="sxs-lookup"><span data-stu-id="2da5e-124">Queued Processing</span></span>

<span data-ttu-id="2da5e-125">如果在幾秒鐘內未生成回應,大多數 WebHook 發送方將重新發送 WebHook。</span><span class="sxs-lookup"><span data-stu-id="2da5e-125">Most WebHook senders will resend a WebHook if a response is not generated within a handful of seconds.</span></span> <span data-ttu-id="2da5e-126">這意味著處理程序必須在該時間範圍內完成處理,以便不要再次調用它。</span><span class="sxs-lookup"><span data-stu-id="2da5e-126">This means that your handler must complete the processing within that time frame in order not for it to be called again.</span></span>

<span data-ttu-id="2da5e-127">如果處理時間較長,或者最好單獨處理,則[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)可用於將 WebHook 請求提交到佇列,例如 Azure[儲存佇列](https://msdn.microsoft.com/library/azure/dd179353.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2da5e-127">If the processing takes longer, or is better handled separately then the [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) can be used to submit the WebHook request to a queue, for example [Azure Storage Queue](https://msdn.microsoft.com/library/azure/dd179353.aspx).</span></span>

<span data-ttu-id="2da5e-128">此處提供[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)的概要:</span><span class="sxs-lookup"><span data-stu-id="2da5e-128">An outline of a [WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs) implementation is provided here:</span></span>

```csharp
public class QueueHandler : WebHookQueueHandler
{
    public override Task EnqueueAsync(WebHookQueueContext context)
    {

        // Enqueue WebHookQueueContext to your queuing system of choice

        return Task.FromResult(true);
    }
}
```
