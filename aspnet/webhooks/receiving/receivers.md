---
uid: webhooks/receiving/receivers
title: ASP.NET Webhook 接收器 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 接收器
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: d771a588b23abcd7b1b33e694af17b219683fc48
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038975"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="29c0c-103">ASP.NET Webhook 接收器</span><span class="sxs-lookup"><span data-stu-id="29c0c-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="29c0c-104">接收 Webhook 寄件者是誰而定。</span><span class="sxs-lookup"><span data-stu-id="29c0c-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="29c0c-105">有時會註冊 WebHook，驗證 「 訂閱者 」 心聲的額外步驟。</span><span class="sxs-lookup"><span data-stu-id="29c0c-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="29c0c-106">某些 Webhook 提供推播到提取模型的 HTTP POST 要求只包含且獨立擷取已將事件資訊的參考。</span><span class="sxs-lookup"><span data-stu-id="29c0c-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="29c0c-107">通常的安全性模型而稍微有所不同。</span><span class="sxs-lookup"><span data-stu-id="29c0c-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="29c0c-108">Microsoft ASP.NET Webhook 的目的是使其更簡單和更一致，才能接到您的 API，而不需花費大量時間找出如何處理 Webhook 的任何特定變數。</span><span class="sxs-lookup"><span data-stu-id="29c0c-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="29c0c-109">WebHook 的接收者負責認可和驗證來自特定寄件者的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="29c0c-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="29c0c-110">WebHook 接收器可支援任意數目的 Webhook，每個都有自己的組態。</span><span class="sxs-lookup"><span data-stu-id="29c0c-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="29c0c-111">比方說，GitHub WebHook 接收器可以接受任意數目的 GitHub 存放庫中的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="29c0c-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="29c0c-112">WebHook 接收器 Uri</span><span class="sxs-lookup"><span data-stu-id="29c0c-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="29c0c-113">藉由安裝 Microsoft ASP.NET Webhook，您會取得一般的 WebHook 控制器可接受來自服務的開放式數目的 WebHook 要求。</span><span class="sxs-lookup"><span data-stu-id="29c0c-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="29c0c-114">當要求抵達時，它會挑選適當的接收者，您已安裝用於處理特定的 WebHook 寄件者。</span><span class="sxs-lookup"><span data-stu-id="29c0c-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="29c0c-115">此控制器的 URI 是您向服務註冊的 WebHook URI，並屬於表單：</span><span class="sxs-lookup"><span data-stu-id="29c0c-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="29c0c-116">基於安全性理由，需要的 URI 是許多的 WebHook 接收器*https* URI 且在某些情況下也必須包含的其他查詢參數來強制執行，只有預定的合作對象可以傳送給上述 URI 的 Webhook.</span><span class="sxs-lookup"><span data-stu-id="29c0c-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="29c0c-117">`<receiver>`元件是名稱的接收者，例如`github`或`slack`。</span><span class="sxs-lookup"><span data-stu-id="29c0c-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="29c0c-118">*{Id}* 是選擇性的識別碼，可用來識別特定的 WebHook 接收器組態。</span><span class="sxs-lookup"><span data-stu-id="29c0c-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="29c0c-119">這可用來向特定接收者的 n 個 Webhook。</span><span class="sxs-lookup"><span data-stu-id="29c0c-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="29c0c-120">比方說，下列三個 Uri 可用來對三個獨立的 Webhook 註冊：</span><span class="sxs-lookup"><span data-stu-id="29c0c-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="29c0c-121">安裝 WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="29c0c-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="29c0c-122">若要接收使用 Microsoft ASP.NET Webhook 的 Webhook，您會先安裝 WebHook 提供者或您想要接收從 Webhook 提供者 Nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="29c0c-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="29c0c-123">Nuget 封裝的名稱[Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)的最後一個部分指示服務支援的位置。</span><span class="sxs-lookup"><span data-stu-id="29c0c-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="29c0c-124">例如</span><span class="sxs-lookup"><span data-stu-id="29c0c-124">For example</span></span>

<span data-ttu-id="29c0c-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)提供支援 Webhook 接收 GitHub 並[Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)接收 ASP 所產生的 Webhook 提供支援。NET Webhook。</span><span class="sxs-lookup"><span data-stu-id="29c0c-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="29c0c-126">內建中，您可以找到 Dropbox、 GitHub、 MailChimp、 PayPal、 Pusher、 Salesforce、 Slack、 等量磁碟區、 Trello 和 WordPress 的支援，但可支援任意數目的其他提供者。</span><span class="sxs-lookup"><span data-stu-id="29c0c-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="29c0c-127">設定 WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="29c0c-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="29c0c-128">已透過 WebHook 接收器[IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)介面和特定實作該介面可以使用註冊任何相依性插入模式。</span><span class="sxs-lookup"><span data-stu-id="29c0c-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="29c0c-129">預設實作會使用應用程式設定可以在 Web.config 檔案中，設定，或如果使用 Azure Web 應用程式，可以透過設定[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="29c0c-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Azure 應用程式設定](_static/AzureAppSettings.png)

<span data-ttu-id="29c0c-131">應用程式設定索引鍵的格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="29c0c-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="29c0c-132">值是逗號分隔的清單相符的值 *{id}* 值的 Webhook 已註冊，例如：</span><span class="sxs-lookup"><span data-stu-id="29c0c-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="29c0c-133">初始化 WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="29c0c-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="29c0c-134">通常在中註冊它們，會初始化的 WebHook 接收器*WebApiConfig*靜態類別，例如：</span><span class="sxs-lookup"><span data-stu-id="29c0c-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```
