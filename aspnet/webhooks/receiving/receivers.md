---
uid: webhooks/receiving/receivers
title: ASP.NET Webhook 接收器 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 接收者
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: d771a588b23abcd7b1b33e694af17b219683fc48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574190"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="0739e-103">ASP.NET Webhook 接收者</span><span class="sxs-lookup"><span data-stu-id="0739e-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="0739e-104">接收 Webhook 取決於寄件者是誰。</span><span class="sxs-lookup"><span data-stu-id="0739e-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="0739e-105">有時候註冊 WebHook 的額外步驟會確認訂閱者確實正在接聽。</span><span class="sxs-lookup"><span data-stu-id="0739e-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="0739e-106">有些 Webhook 會提供推播到提取模型，其中 HTTP POST 要求只包含事件資訊的參考，然後獨立抓取。</span><span class="sxs-lookup"><span data-stu-id="0739e-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="0739e-107">安全性模型通常會有相當大的差異。</span><span class="sxs-lookup"><span data-stu-id="0739e-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="0739e-108">Microsoft ASP.NET Webhook 的目的是要讓它更簡單且更一致，以連線到您的 API，而不需要花太多時間來瞭解如何處理任何特定的 Webhook 變體。</span><span class="sxs-lookup"><span data-stu-id="0739e-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="0739e-109">WebHook 接收者會負責接受和驗證來自特定寄件者的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="0739e-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="0739e-110">WebHook 接收者可以支援任意數量的 Webhook，每個都有自己的設定。</span><span class="sxs-lookup"><span data-stu-id="0739e-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="0739e-111">例如，GitHub WebHook 接收器可以接受來自任意數目之 GitHub 存放庫的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="0739e-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="0739e-112">WebHook 接收者 Uri</span><span class="sxs-lookup"><span data-stu-id="0739e-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="0739e-113">藉由安裝 Microsoft ASP.NET Webhook，您會取得一般 WebHook 控制器，它會接受來自開放式服務數目的 WebHook 要求。</span><span class="sxs-lookup"><span data-stu-id="0739e-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="0739e-114">當要求抵達時，它會挑選您已安裝的適當接收者來處理特定的 WebHook 傳送者。</span><span class="sxs-lookup"><span data-stu-id="0739e-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="0739e-115">此控制器的 URI 是您向服務註冊的 WebHook URI，其格式如下：</span><span class="sxs-lookup"><span data-stu-id="0739e-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="0739e-116">基於安全性理由，許多 WebHook 接收者需要 URI 為*HTTPs* uri，而在某些情況下，它也必須包含額外的查詢參數，用來強制只有預定的合作物件可以將 webhook 傳送至上述 URI。</span><span class="sxs-lookup"><span data-stu-id="0739e-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="0739e-117">`<receiver>` 元件是接收者的名稱，例如 `github` 或 `slack`。</span><span class="sxs-lookup"><span data-stu-id="0739e-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="0739e-118">*{Id}* 是選擇性的識別碼，可以用來識別特定的 WebHook 接收者設定。</span><span class="sxs-lookup"><span data-stu-id="0739e-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="0739e-119">這可以用來向特定接收者註冊 N Webhook。</span><span class="sxs-lookup"><span data-stu-id="0739e-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="0739e-120">例如，下列三個 Uri 可以用來註冊三個獨立的 Webhook：</span><span class="sxs-lookup"><span data-stu-id="0739e-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="0739e-121">安裝 WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="0739e-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="0739e-122">若要使用 Microsoft ASP.NET Webhook 接收 Webhook，您必須先安裝 WebHook 提供者的 Nuget 套件，或您想要接收 Webhook 的來源提供者。</span><span class="sxs-lookup"><span data-stu-id="0739e-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="0739e-123">Nuget 套件的名稱為[webhook](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) ，其中最後一個部分指出支援的服務。</span><span class="sxs-lookup"><span data-stu-id="0739e-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="0739e-124">例如</span><span class="sxs-lookup"><span data-stu-id="0739e-124">For example</span></span>

<span data-ttu-id="0739e-125">[Webhook](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)會提供從 GitHub 和 Webhook 接收 webhook 的支援。[自訂](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)會提供接收 ASP.NET webhook 所產生 webhook 的支援。</span><span class="sxs-lookup"><span data-stu-id="0739e-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="0739e-126">您可以在這裡找到 Dropbox、GitHub、MailChimp、PayPal、Pusher、Salesforce、時差、Stripe、Trello 和 WordPress 的支援，但可支援任何數目的其他提供者。</span><span class="sxs-lookup"><span data-stu-id="0739e-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="0739e-127">設定 WebHook 接收者</span><span class="sxs-lookup"><span data-stu-id="0739e-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="0739e-128">WebHook 接收者是透過[IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)介面來設定，而且可以使用任何相依性插入模型來註冊該介面的特定實現。</span><span class="sxs-lookup"><span data-stu-id="0739e-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="0739e-129">預設的執行會使用可在 web.config 檔案中設定的應用程式設定，或者，如果使用 Azure Web Apps，可以透過[Azure 入口網站](https://portal.azure.com/)來設定。</span><span class="sxs-lookup"><span data-stu-id="0739e-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![API 應用程式設定](_static/AzureAppSettings.png)

<span data-ttu-id="0739e-131">應用程式設定金鑰的格式如下：</span><span class="sxs-lookup"><span data-stu-id="0739e-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="0739e-132">值是以逗號分隔的值清單，其中包含已註冊 Webhook 的 *{id}* 值，例如：</span><span class="sxs-lookup"><span data-stu-id="0739e-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="0739e-133">初始化 WebHook 接收者</span><span class="sxs-lookup"><span data-stu-id="0739e-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="0739e-134">藉由登錄 WebHook 接收器，通常是在*WebApiConfig*靜態類別中進行初始化，例如：</span><span class="sxs-lookup"><span data-stu-id="0739e-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

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
