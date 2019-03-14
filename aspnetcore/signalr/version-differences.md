---
title: SignalR 和 ASP.NET Core SignalR 之間的差異
author: bradygaster
description: SignalR 和 ASP.NET Core SignalR 之間的差異
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.date: 11/14/2018
uid: signalr/version-differences
ms.openlocfilehash: 091fc44fccf820a394e7c6f775700c85bebc9101
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046895"
---
# <a name="differences-between-aspnet-signalr-and-aspnet-core-signalr"></a><span data-ttu-id="37012-103">ASP.NET SignalR 及 ASP.NET Core SignalR 之間的差異</span><span class="sxs-lookup"><span data-stu-id="37012-103">Differences between ASP.NET SignalR and ASP.NET Core SignalR</span></span>

<span data-ttu-id="37012-104">ASP.NET Core SignalR 與不相容用戶端或為 ASP.NET SignalR 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="37012-104">ASP.NET Core SignalR isn't compatible with clients or servers for ASP.NET SignalR.</span></span> <span data-ttu-id="37012-105">本文詳細說明已經被移除，或在 ASP.NET Core SignalR 中變更的功能。</span><span class="sxs-lookup"><span data-stu-id="37012-105">This article details features which have been removed or changed in ASP.NET Core SignalR.</span></span>

## <a name="how-to-identify-the-signalr-version"></a><span data-ttu-id="37012-106">如何找出 SignalR 版本</span><span class="sxs-lookup"><span data-stu-id="37012-106">How to identify the SignalR version</span></span>

|                      | <span data-ttu-id="37012-107">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="37012-107">ASP.NET SignalR</span></span> | <span data-ttu-id="37012-108">ASP.NET Core SignalR</span><span class="sxs-lookup"><span data-stu-id="37012-108">ASP.NET Core SignalR</span></span> |
| -------------------- | --------------- | -------------------- |
| <span data-ttu-id="37012-109">伺服器 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="37012-109">Server NuGet Package</span></span> | [<span data-ttu-id="37012-110">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="37012-110">Microsoft.AspNet.SignalR</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR/) | <span data-ttu-id="37012-111">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)</span><span class="sxs-lookup"><span data-stu-id="37012-111">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)</span></span><br><span data-ttu-id="37012-112">[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="37012-112">[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework)</span></span> |
| <span data-ttu-id="37012-113">用戶端 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="37012-113">Client NuGet Packages</span></span> | [<span data-ttu-id="37012-114">Microsoft.AspNet.SignalR.Client</span><span class="sxs-lookup"><span data-stu-id="37012-114">Microsoft.AspNet.SignalR.Client</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Client/)<br>[<span data-ttu-id="37012-115">Microsoft.AspNet.SignalR.JS</span><span class="sxs-lookup"><span data-stu-id="37012-115">Microsoft.AspNet.SignalR.JS</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.JS/) | [<span data-ttu-id="37012-116">Microsoft.AspNetCore.SignalR.Client</span><span class="sxs-lookup"><span data-stu-id="37012-116">Microsoft.AspNetCore.SignalR.Client</span></span>](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR.Client/) |
| <span data-ttu-id="37012-117">用戶端 npm 套件</span><span class="sxs-lookup"><span data-stu-id="37012-117">Client npm Package</span></span> | [<span data-ttu-id="37012-118">signalr</span><span class="sxs-lookup"><span data-stu-id="37012-118">signalr</span></span>](https://www.npmjs.com/package/signalr) | [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) |
| <span data-ttu-id="37012-119">Java 用戶端</span><span class="sxs-lookup"><span data-stu-id="37012-119">Java Client</span></span> | <span data-ttu-id="37012-120">[GitHub 存放庫](https://github.com/SignalR/java-client)（已過時）</span><span class="sxs-lookup"><span data-stu-id="37012-120">[GitHub Repository](https://github.com/SignalR/java-client) (deprecated)</span></span>  | <span data-ttu-id="37012-121">Maven 套件[com.microsoft.signalr](https://search.maven.org/artifact/com.microsoft.signalr/signalr)</span><span class="sxs-lookup"><span data-stu-id="37012-121">Maven package [com.microsoft.signalr](https://search.maven.org/artifact/com.microsoft.signalr/signalr)</span></span> |
| <span data-ttu-id="37012-122">伺服器應用程式類型</span><span class="sxs-lookup"><span data-stu-id="37012-122">Server App Type</span></span> | <span data-ttu-id="37012-123">ASP.NET (System.Web) 或 OWIN 自我裝載</span><span class="sxs-lookup"><span data-stu-id="37012-123">ASP.NET (System.Web) or OWIN Self-Host</span></span> | <span data-ttu-id="37012-124">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="37012-124">ASP.NET Core</span></span> |
| <span data-ttu-id="37012-125">支援的伺服器平台</span><span class="sxs-lookup"><span data-stu-id="37012-125">Supported Server Platforms</span></span> | <span data-ttu-id="37012-126">.NET framework 4.5 或更新版本</span><span class="sxs-lookup"><span data-stu-id="37012-126">.NET Framework 4.5 or later</span></span> | <span data-ttu-id="37012-127">.NET Framework 4.6.1 或更新版本</span><span class="sxs-lookup"><span data-stu-id="37012-127">.NET Framework 4.6.1 or later</span></span><br><span data-ttu-id="37012-128">.NET core 2.1 或更新版本</span><span class="sxs-lookup"><span data-stu-id="37012-128">.NET Core 2.1 or later</span></span> |

## <a name="feature-differences"></a><span data-ttu-id="37012-129">功能差異</span><span class="sxs-lookup"><span data-stu-id="37012-129">Feature differences</span></span>

### <a name="automatic-reconnects"></a><span data-ttu-id="37012-130">自動重新連線</span><span class="sxs-lookup"><span data-stu-id="37012-130">Automatic reconnects</span></span>

<span data-ttu-id="37012-131">ASP.NET Core SignalR 並不支援自動重新連線。</span><span class="sxs-lookup"><span data-stu-id="37012-131">Automatic reconnects aren't supported in ASP.NET Core SignalR.</span></span> <span data-ttu-id="37012-132">如果用戶端已中斷連接，使用者必須明確啟動新的連線如果他們想要重新連線。</span><span class="sxs-lookup"><span data-stu-id="37012-132">If the client is disconnected, the user must explicitly start a new connection if they want to reconnect.</span></span> <span data-ttu-id="37012-133">在 ASP.NET SignalR、 SignalR 會嘗試重新連線到伺服器，如果連接已卸除。</span><span class="sxs-lookup"><span data-stu-id="37012-133">In ASP.NET SignalR, SignalR attempts to reconnect to the server if the connection is dropped.</span></span> 

### <a name="protocol-support"></a><span data-ttu-id="37012-134">通訊協定支援</span><span class="sxs-lookup"><span data-stu-id="37012-134">Protocol support</span></span>

<span data-ttu-id="37012-135">ASP.NET Core SignalR 支援 JSON，以及新的二進位通訊協定，以根據[MessagePack](xref:signalr/messagepackhubprotocol)。</span><span class="sxs-lookup"><span data-stu-id="37012-135">ASP.NET Core SignalR supports JSON, as well as a new binary protocol based on [MessagePack](xref:signalr/messagepackhubprotocol).</span></span> <span data-ttu-id="37012-136">此外，您可以建立自訂通訊協定。</span><span class="sxs-lookup"><span data-stu-id="37012-136">Additionally, custom protocols can be created.</span></span>

### <a name="transports"></a><span data-ttu-id="37012-137">傳輸</span><span class="sxs-lookup"><span data-stu-id="37012-137">Transports</span></span>

<span data-ttu-id="37012-138">在 ASP.NET Core SignalR 中不支援永久框架傳輸。</span><span class="sxs-lookup"><span data-stu-id="37012-138">The Forever Frame transport is not supported in ASP.NET Core SignalR.</span></span>

## <a name="differences-on-the-server"></a><span data-ttu-id="37012-139">在伺服器上的差異</span><span class="sxs-lookup"><span data-stu-id="37012-139">Differences on the server</span></span>

<span data-ttu-id="37012-140">ASP.NET Core SignalR 的伺服器端程式庫都會納入[Microsoft.AspNetCore.App 中繼套件](xref:fundamentals/metapackage-app)封裝的一部分**ASP.NET Core Web 應用程式**Razor 和 MVC 範本專案。</span><span class="sxs-lookup"><span data-stu-id="37012-140">The ASP.NET Core SignalR server-side libraries are included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) package that's part of the **ASP.NET Core Web Application** template for both Razor and MVC projects.</span></span>

<span data-ttu-id="37012-141">ASP.NET Core SignalR 是 ASP.NET Core 中介軟體，因此必須由呼叫[AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr)在`Startup.ConfigureServices`。</span><span class="sxs-lookup"><span data-stu-id="37012-141">ASP.NET Core SignalR is an ASP.NET Core middleware, so it must be configured by calling [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) in `Startup.ConfigureServices`.</span></span>

```csharp
services.AddSignalR()
```

<span data-ttu-id="37012-142">若要設定路由，請將路由對應至中樞內[UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr)方法呼叫中`Startup.Configure`方法。</span><span class="sxs-lookup"><span data-stu-id="37012-142">To configure routing, map routes to hubs inside the [UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr) method call in the `Startup.Configure` method.</span></span>

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions"></a><span data-ttu-id="37012-143">黏性工作階段</span><span class="sxs-lookup"><span data-stu-id="37012-143">Sticky sessions</span></span>

<span data-ttu-id="37012-144">ASP.NET SignalR 的向外延展模型可讓用戶端重新連線，並將訊息傳送至伺服器陣列中的任何伺服器。</span><span class="sxs-lookup"><span data-stu-id="37012-144">The scaleout model for ASP.NET SignalR allows clients to reconnect and send messages to any server in the farm.</span></span> <span data-ttu-id="37012-145">在 ASP.NET Core SignalR 用戶端必須連線的持續時間與相同的伺服器互動。</span><span class="sxs-lookup"><span data-stu-id="37012-145">In ASP.NET Core SignalR, the client must interact with the same server for the duration of the connection.</span></span> <span data-ttu-id="37012-146">使用 Redis 範圍外，這表示黏性工作階段所需。</span><span class="sxs-lookup"><span data-stu-id="37012-146">For scaleout using Redis, that means sticky sessions are required.</span></span> <span data-ttu-id="37012-147">使用向外延展[Azure SignalR 服務](/azure/azure-signalr/)，因為此服務會處理用戶端連線，不需要黏性工作階段。</span><span class="sxs-lookup"><span data-stu-id="37012-147">For scaleout using [Azure SignalR Service](/azure/azure-signalr/), sticky sessions are not required because the service handles connections to clients.</span></span> 

### <a name="single-hub-per-connection"></a><span data-ttu-id="37012-148">每個連線單一中樞</span><span class="sxs-lookup"><span data-stu-id="37012-148">Single hub per connection</span></span>

<span data-ttu-id="37012-149">在 ASP.NET Core SignalR 連線模型已簡化。</span><span class="sxs-lookup"><span data-stu-id="37012-149">In ASP.NET Core SignalR, the connection model has been simplified.</span></span> <span data-ttu-id="37012-150">連線會對直接單一中樞中，而不是正在使用共用存取權的多個中樞單一連接。</span><span class="sxs-lookup"><span data-stu-id="37012-150">Connections are made directly to a single hub, rather than a single connection being used to share access to multiple hubs.</span></span>

### <a name="streaming"></a><span data-ttu-id="37012-151">資料流</span><span class="sxs-lookup"><span data-stu-id="37012-151">Streaming</span></span>

<span data-ttu-id="37012-152">ASP.NET Core SignalR 現在支援[串流資料](xref:signalr/streaming)從用戶端中樞。</span><span class="sxs-lookup"><span data-stu-id="37012-152">ASP.NET Core SignalR now supports [streaming data](xref:signalr/streaming) from the hub to the client.</span></span>

### <a name="state"></a><span data-ttu-id="37012-153">狀況</span><span class="sxs-lookup"><span data-stu-id="37012-153">State</span></span>

<span data-ttu-id="37012-154">能夠將任意的狀態傳遞用戶端與中樞 （通常稱為 HubState） 之間已移除，以及支援進度訊息。</span><span class="sxs-lookup"><span data-stu-id="37012-154">The ability to pass arbitrary state between clients and the hub (often called HubState) has been removed, as well as support for progress messages.</span></span> <span data-ttu-id="37012-155">目前沒有任何對應的中樞 proxy。</span><span class="sxs-lookup"><span data-stu-id="37012-155">There is no counterpart of hub proxies at the moment.</span></span>

### <a name="persistentconnection-removal"></a><span data-ttu-id="37012-156">PersistentConnection 移除</span><span class="sxs-lookup"><span data-stu-id="37012-156">PersistentConnection removal</span></span>

<span data-ttu-id="37012-157">在 ASP.NET Core SignalR [PersistentConnection](https://docs.microsoft.com/previous-versions/aspnet/jj919047(v%3dvs.118))類別已移除。</span><span class="sxs-lookup"><span data-stu-id="37012-157">In ASP.NET Core SignalR, the [PersistentConnection](https://docs.microsoft.com/previous-versions/aspnet/jj919047(v%3dvs.118)) class has been removed.</span></span> 

### <a name="globalhost"></a><span data-ttu-id="37012-158">GlobalHost</span><span class="sxs-lookup"><span data-stu-id="37012-158">GlobalHost</span></span>

<span data-ttu-id="37012-159">ASP.NET Core 具有內建於 framework 的相依性插入 (DI)。</span><span class="sxs-lookup"><span data-stu-id="37012-159">ASP.NET Core has dependency injection (DI) built into the framework.</span></span> <span data-ttu-id="37012-160">服務可以存取使用 DI [HubContext](xref:signalr/hubcontext)。</span><span class="sxs-lookup"><span data-stu-id="37012-160">Services can use DI to access the [HubContext](xref:signalr/hubcontext).</span></span> <span data-ttu-id="37012-161">`GlobalHost`物件，以取得用於 ASP.NET SignalR`HubContext`不存在於 ASP.NET Core SignalR。</span><span class="sxs-lookup"><span data-stu-id="37012-161">The `GlobalHost` object that is used in ASP.NET SignalR to get a `HubContext` doesn't exist in ASP.NET Core SignalR.</span></span>

### <a name="hubpipeline"></a><span data-ttu-id="37012-162">HubPipeline</span><span class="sxs-lookup"><span data-stu-id="37012-162">HubPipeline</span></span>

<span data-ttu-id="37012-163">ASP.NET Core SignalR 沒有支援`HubPipeline`模組。</span><span class="sxs-lookup"><span data-stu-id="37012-163">ASP.NET Core SignalR doesn't have support for `HubPipeline` modules.</span></span>

## <a name="differences-on-the-client"></a><span data-ttu-id="37012-164">在用戶端上的差異</span><span class="sxs-lookup"><span data-stu-id="37012-164">Differences on the client</span></span>

### <a name="typescript"></a><span data-ttu-id="37012-165">TypeScript</span><span class="sxs-lookup"><span data-stu-id="37012-165">TypeScript</span></span>

<span data-ttu-id="37012-166">ASP.NET Core SignalR 用戶端以[TypeScript](https://www.typescriptlang.org/)。</span><span class="sxs-lookup"><span data-stu-id="37012-166">The ASP.NET Core SignalR client is written in [TypeScript](https://www.typescriptlang.org/).</span></span> <span data-ttu-id="37012-167">使用時，您可以撰寫以 JavaScript 或 TypeScript [JavaScript 用戶端](xref:signalr/javascript-client)。</span><span class="sxs-lookup"><span data-stu-id="37012-167">You can write in JavaScript or TypeScript when using the [JavaScript client](xref:signalr/javascript-client).</span></span>

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a><span data-ttu-id="37012-168">JavaScript 用戶端裝載於[npm](https://www.npmjs.com/)</span><span class="sxs-lookup"><span data-stu-id="37012-168">The JavaScript client is hosted at [npm](https://www.npmjs.com/)</span></span>

<span data-ttu-id="37012-169">在舊版中，JavaScript 用戶端已取得透過 Visual Studio 中的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="37012-169">In previous versions, the JavaScript client was obtained through a NuGet package in Visual Studio.</span></span> <span data-ttu-id="37012-170">如需核心版本中， [ @aspnet/signalr ](https://www.npmjs.com/package/@aspnet/signalr) npm 套件所包含的 JavaScript 程式庫。</span><span class="sxs-lookup"><span data-stu-id="37012-170">For the Core versions, the [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) npm package contains the JavaScript libraries.</span></span> <span data-ttu-id="37012-171">此套件不會包含於**ASP.NET Core Web 應用程式**範本。</span><span class="sxs-lookup"><span data-stu-id="37012-171">This package isn't included in the **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="37012-172">使用 npm 來取得並安裝`@aspnet/signalr`npm 套件。</span><span class="sxs-lookup"><span data-stu-id="37012-172">Use npm to obtain and install the `@aspnet/signalr` npm package.</span></span>

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a><span data-ttu-id="37012-173">jQuery</span><span class="sxs-lookup"><span data-stu-id="37012-173">jQuery</span></span>

<span data-ttu-id="37012-174">已移除對 jQuery 的相依性，但專案仍然可以使用 jQuery。</span><span class="sxs-lookup"><span data-stu-id="37012-174">The dependency on jQuery has been removed, however projects can still use jQuery.</span></span>

### <a name="internet-explorer-support"></a><span data-ttu-id="37012-175">Internet Explorer 支援</span><span class="sxs-lookup"><span data-stu-id="37012-175">Internet Explorer support</span></span>

<span data-ttu-id="37012-176">ASP.NET Core SignalR 需要 Microsoft Internet Explorer 11 或更新版本 （ASP.NET SignalR 支援 Microsoft Internet Explorer 8 和更新版本）。</span><span class="sxs-lookup"><span data-stu-id="37012-176">ASP.NET Core SignalR requires Microsoft Internet Explorer 11 or later (ASP.NET SignalR supported Microsoft Internet Explorer 8 and later).</span></span>

### <a name="javascript-client-method-syntax"></a><span data-ttu-id="37012-177">JavaScript 用戶端方法語法</span><span class="sxs-lookup"><span data-stu-id="37012-177">JavaScript client method syntax</span></span>

<span data-ttu-id="37012-178">JavaScript 語法已從舊版 SignalR 的變更。</span><span class="sxs-lookup"><span data-stu-id="37012-178">The JavaScript syntax has changed from the previous version of SignalR.</span></span> <span data-ttu-id="37012-179">而不是使用`$connection`物件，請建立連線，使用[HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API。</span><span class="sxs-lookup"><span data-stu-id="37012-179">Rather than using the `$connection` object, create a connection using the [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API.</span></span>

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

<span data-ttu-id="37012-180">使用[上](/javascript/api/@aspnet/signalr/HubConnection#on)方法，以指定用戶端中樞可以呼叫的方法。</span><span class="sxs-lookup"><span data-stu-id="37012-180">Use the [on](/javascript/api/@aspnet/signalr/HubConnection#on) method to specify client methods that the hub can call.</span></span>

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

<span data-ttu-id="37012-181">建立用戶端方法之後, 啟動中樞連線。</span><span class="sxs-lookup"><span data-stu-id="37012-181">After creating the client method, start the hub connection.</span></span> <span data-ttu-id="37012-182">鏈結[攔截](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)記錄或處理錯誤的方法。</span><span class="sxs-lookup"><span data-stu-id="37012-182">Chain a [catch](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch) method to log or handle errors.</span></span>

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a><span data-ttu-id="37012-183">中樞 proxy</span><span class="sxs-lookup"><span data-stu-id="37012-183">Hub proxies</span></span>

<span data-ttu-id="37012-184">中樞 proxy 不會再自動產生。</span><span class="sxs-lookup"><span data-stu-id="37012-184">Hub proxies are no longer automatically generated.</span></span> <span data-ttu-id="37012-185">相反地，在方法名稱會傳遞至[叫用](/javascript/api/%40aspnet/signalr/hubconnection#invoke)API 做為字串。</span><span class="sxs-lookup"><span data-stu-id="37012-185">Instead, the method name is passed into the [invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke) API as a string.</span></span>

### <a name="net-and-other-clients"></a><span data-ttu-id="37012-186">.NET 和其他用戶端</span><span class="sxs-lookup"><span data-stu-id="37012-186">.NET and other clients</span></span>

<span data-ttu-id="37012-187">`Microsoft.AspNetCore.SignalR.Client` NuGet 套件包含.NET 用戶端程式庫的 ASP.NET Core SignalR。</span><span class="sxs-lookup"><span data-stu-id="37012-187">The `Microsoft.AspNetCore.SignalR.Client` NuGet package contains the .NET client libraries for ASP.NET Core SignalR.</span></span>

<span data-ttu-id="37012-188">使用[HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)來建立及建置連接到中樞執行個體。</span><span class="sxs-lookup"><span data-stu-id="37012-188">Use the [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder) to create and build an instance of a connection to a hub.</span></span>

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="scaleout-differences"></a><span data-ttu-id="37012-189">向外延展的差異</span><span class="sxs-lookup"><span data-stu-id="37012-189">Scaleout differences</span></span>

<span data-ttu-id="37012-190">ASP.NET SignalR 支援 SQL Server 和 Redis。</span><span class="sxs-lookup"><span data-stu-id="37012-190">ASP.NET SignalR supports SQL Server and Redis.</span></span> <span data-ttu-id="37012-191">ASP.NET Core SignalR 支援 Azure SignalR 服務和 Redis。</span><span class="sxs-lookup"><span data-stu-id="37012-191">ASP.NET Core SignalR supports Azure SignalR Service and Redis.</span></span>

### <a name="aspnet"></a><span data-ttu-id="37012-192">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="37012-192">ASP.NET</span></span>

* [<span data-ttu-id="37012-193">SignalR 向外延展與 Azure 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="37012-193">SignalR scaleout with Azure Service Bus</span></span>](/aspnet/signalr/overview/performance/scaleout-with-windows-azure-service-bus)
* [<span data-ttu-id="37012-194">使用 Redis 的 SignalR 向外延展</span><span class="sxs-lookup"><span data-stu-id="37012-194">SignalR scaleout with Redis</span></span>](/aspnet/signalr/overview/performance/scaleout-with-redis)
* [<span data-ttu-id="37012-195">SignalR 向外延展與 SQL Server</span><span class="sxs-lookup"><span data-stu-id="37012-195">SignalR scaleout with SQL Server</span></span>](/aspnet/signalr/overview/performance/scaleout-with-sql-server)

### <a name="aspnet-core"></a><span data-ttu-id="37012-196">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="37012-196">ASP.NET Core</span></span>

* [<span data-ttu-id="37012-197">Azure SignalR Service</span><span class="sxs-lookup"><span data-stu-id="37012-197">Azure SignalR Service</span></span>](/azure/azure-signalr/)

## <a name="additional-resources"></a><span data-ttu-id="37012-198">其他資源</span><span class="sxs-lookup"><span data-stu-id="37012-198">Additional resources</span></span>

* [<span data-ttu-id="37012-199">中樞</span><span class="sxs-lookup"><span data-stu-id="37012-199">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="37012-200">JavaScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="37012-200">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="37012-201">.NET 用戶端</span><span class="sxs-lookup"><span data-stu-id="37012-201">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="37012-202">支援的平台</span><span class="sxs-lookup"><span data-stu-id="37012-202">Supported platforms</span></span>](xref:signalr/supported-platforms)
