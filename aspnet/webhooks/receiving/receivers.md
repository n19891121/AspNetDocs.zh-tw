---
uid: webhooks/receiving/receivers
title: ASP.NET WebHook 接收器 |微軟文件
author: rick-anderson
description: ASP.NET WebHook 接收器
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: 60f46141b59fc3888a6480d8201160420469d1a7
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675159"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="38edd-103">ASP.NET WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="38edd-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="38edd-104">接收 WebHook 取決於寄件者是誰。</span><span class="sxs-lookup"><span data-stu-id="38edd-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="38edd-105">有時,還有其他步驟註冊 WebHook,驗證訂閱者是否真正在偵聽。</span><span class="sxs-lookup"><span data-stu-id="38edd-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="38edd-106">某些 WebHook 提供推送到拉取模型,其中 HTTP POST 請求僅包含對事件資訊的引用,然後由該引用獨立檢索。</span><span class="sxs-lookup"><span data-stu-id="38edd-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="38edd-107">通常,安全模型差異很大。</span><span class="sxs-lookup"><span data-stu-id="38edd-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="38edd-108">Microsoft ASP.NET WebHooks 的目的是使連接 API 更簡單、更一致,而無需花費大量時間來瞭解如何處理 WebHook 的任何特定變體。</span><span class="sxs-lookup"><span data-stu-id="38edd-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="38edd-109">WebHook 接收器負責接受和驗證來自特定寄件者的 WebHook。</span><span class="sxs-lookup"><span data-stu-id="38edd-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="38edd-110">WebHook 接收器可以支援任意數量的 WebHook,每個 WebHook 都有自己的配置。</span><span class="sxs-lookup"><span data-stu-id="38edd-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="38edd-111">例如,GitHub WebHook 接收器可以接受來自任意數量的 GitHub 儲存庫的 WebHook。</span><span class="sxs-lookup"><span data-stu-id="38edd-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="38edd-112">WebHook 接收器 URI</span><span class="sxs-lookup"><span data-stu-id="38edd-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="38edd-113">通過安裝 Microsoft ASP.NET WebHooks,您可以獲得一個常規 WebHook 控制器,該控制器接受來自開源服務數量的 WebHook 請求。</span><span class="sxs-lookup"><span data-stu-id="38edd-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="38edd-114">請求到達時,它會選擇已安裝的用於處理特定 WebHook 發送方的相應接收器。</span><span class="sxs-lookup"><span data-stu-id="38edd-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="38edd-115">此控制器的 URI 是您向服務註冊的 WebHook URI,其形式為:</span><span class="sxs-lookup"><span data-stu-id="38edd-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="38edd-116">出於安全原因,許多 WebHook 接收器要求 URI 是*Htcript,* 在某些情況下,它還必須包含一個額外的查詢參數,用於強制只有目標方才能將 WebHook 發送到上述 URI。</span><span class="sxs-lookup"><span data-stu-id="38edd-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="38edd-117">元件`<receiver>`是接收器名稱,例如`github`或`slack`。</span><span class="sxs-lookup"><span data-stu-id="38edd-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="38edd-118">*{id}* 是一個可選識別碼,可用於識別特定的 WebHook 接收器設定。</span><span class="sxs-lookup"><span data-stu-id="38edd-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="38edd-119">這可用於向特定接收器註冊 N WebHook。</span><span class="sxs-lookup"><span data-stu-id="38edd-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="38edd-120">例如,以下三個 URI 可用於註冊三個獨立的 WebHook:</span><span class="sxs-lookup"><span data-stu-id="38edd-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="38edd-121">安裝 WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="38edd-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="38edd-122">要使用 Microsoft ASP.NET WebHook 接收 WebHook,請首先為要接收 WebHook 的 WebHook 提供者或提供者安裝 Nuget 包。</span><span class="sxs-lookup"><span data-stu-id="38edd-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="38edd-123">Nuget 包名為[Microsoft.AspNet.WebHooks.Receivers.\*,](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers)其中最後一部分表示支援的服務。</span><span class="sxs-lookup"><span data-stu-id="38edd-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="38edd-124">例如：</span><span class="sxs-lookup"><span data-stu-id="38edd-124">For example</span></span>

<span data-ttu-id="38edd-125">[微軟.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub)支援接收來自GitHub和[微軟的WebHook.AspNet.WebHooks.Receivers.Customs.Customs](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom)為接收由ASP.NETWebHooks生成的WebHook提供支援。</span><span class="sxs-lookup"><span data-stu-id="38edd-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="38edd-126">開箱即用,您可以找到對 Dropbox、GitHub、MailChimp、PayPal、Pusher、Salesforce、Slack、Stripe、Trello 和 WordPress 的支援,但可以支援任意數量的其他供應商。</span><span class="sxs-lookup"><span data-stu-id="38edd-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="38edd-127">設定 WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="38edd-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="38edd-128">WebHook 接收器透過[IWebHookReceiverConfig 整](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs)面進行配置,該介面的特定實現可以使用任何依賴項注入模型進行註冊。</span><span class="sxs-lookup"><span data-stu-id="38edd-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="38edd-129">預設實現使用應用程式設置,可以在 Web.config 檔中設置,或者,如果使用 Azure Web 應用,可以通過[Azure 門戶](https://portal.azure.com/)進行設置。</span><span class="sxs-lookup"><span data-stu-id="38edd-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![API 應用程式設定](_static/AzureAppSettings.png)

<span data-ttu-id="38edd-131">應用程式設定鍵的格式如下:</span><span class="sxs-lookup"><span data-stu-id="38edd-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="38edd-132">該值是與已註冊 WebHook 的 *[id]* 值符合的逗號分隔的值清單,例如:</span><span class="sxs-lookup"><span data-stu-id="38edd-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="38edd-133">初始化 WebHook 接收器</span><span class="sxs-lookup"><span data-stu-id="38edd-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="38edd-134">WebHook 接收器透過註冊來初始化,通常在*WebApiConfig*靜態類別中,例如:</span><span class="sxs-lookup"><span data-stu-id="38edd-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

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
