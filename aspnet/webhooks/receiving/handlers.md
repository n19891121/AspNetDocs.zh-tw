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
# <a name="aspnet-webhooks-handlers"></a>ASP.NET WebHook 處理程式

WebHooks 請求由 WebHook 接收器驗證後,即可由使用者代碼處理。 這是*處理程式*的來向。 處理程式派生自[IWebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)介面,但通常使用[WebHookHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandler.cs)類,而不是直接從該介面派生。

WebHook 請求可以由一個或多個處理程序處理。 處理程式根據各自的*Order*屬性從最低到最高的順序調用,其中 Order 是一個簡單的整數(建議介於 1 和 100 之間):

![WebHook 處理程式順序屬性圖](_static/Handlers.png)

處理程式可以選擇在 WebHookHandlerContext 上設定*回應*屬性,這將導致處理停止,並將回應作為對 WebHook 的 HTTP 回應發送回來。 在上面的案例中,不會調用處理程式 C,因為它的順序高於 B,B 設置回應。

設置回應通常只與 WebHook 相關,回應可以將資訊回源 API。 例如,Slack WebHooks 的回應被發回 WebHook 的通道。 如果處理程式只想從該特定接收器接收 WebHook,則可以設置 Receiver 屬性。 如果他們不設置接收器,他們被要求所有這些。

回應的另一個常見用途是使用*410 Gone*回應來指示 WebHook 不再處於活動狀態,並且不應提交進一步的請求。

默認情況下,所有 WebHook 接收器都將調用處理程式。 但是,如果*Receiver*屬性設置為處理程式的名稱,則該處理程式將僅接收來自該接收者的 WebHook 請求。

## <a name="processing-a-webhook"></a>處理 WebHook

呼叫處理程式時,它會獲取包含有關 WebHook 請求的資訊的[WebHook 處理程式。](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookHandlerContext.cs) 數據(通常是 HTTP 請求正文)可從*Data*屬性獲得。

數據類型通常是 JSON 或 HTML 表單數據,但如果需要,可以強制轉換為更具體的類型。 例如,ASP.NET WebHooks 生成的自訂 WebHook 可以轉換為[「自訂通知」](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers.Custom/WebHooks/CustomNotifications.cs)類型,如下所示:

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

  ## <a name="queued-processing"></a>佇列處理

如果在幾秒鐘內未生成回應,大多數 WebHook 發送方將重新發送 WebHook。 這意味著處理程序必須在該時間範圍內完成處理,以便不要再次調用它。

如果處理時間較長,或者最好單獨處理,則[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)可用於將 WebHook 請求提交到佇列,例如 Azure[儲存佇列](https://msdn.microsoft.com/library/azure/dd179353.aspx)。

此處提供[WebHookQueueHandler](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/WebHookQueueHandler.cs)的概要:

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
