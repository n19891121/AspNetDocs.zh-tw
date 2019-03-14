---
title: ASP.NET Core SignalR 中的安全性考量
author: bradygaster
description: 了解如何在 ASP.NET Core SignalR 使用驗證和授權。
monikerRange: '>= aspnetcore-2.1'
ms.author: anurse
ms.custom: mvc
ms.date: 11/06/2018
uid: signalr/security
ms.openlocfilehash: 6e9f849ed856cf1cbf989b8b16cab5209c465471
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059925"
---
# <a name="security-considerations-in-aspnet-core-signalr"></a><span data-ttu-id="f8bba-103">ASP.NET Core SignalR 中的安全性考量</span><span class="sxs-lookup"><span data-stu-id="f8bba-103">Security considerations in ASP.NET Core SignalR</span></span>

<span data-ttu-id="f8bba-104">藉由[Andrew Stanton-nurse](https://twitter.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="f8bba-104">By [Andrew Stanton-Nurse](https://twitter.com/anurse)</span></span>

<span data-ttu-id="f8bba-105">這篇文章會提供資訊保護 SignalR。</span><span class="sxs-lookup"><span data-stu-id="f8bba-105">This article provides information on securing SignalR.</span></span>

## <a name="cross-origin-resource-sharing"></a><span data-ttu-id="f8bba-106">跨原始資源共用</span><span class="sxs-lookup"><span data-stu-id="f8bba-106">Cross-origin resource sharing</span></span>

<span data-ttu-id="f8bba-107">[跨原始資源共用 (CORS)](https://www.w3.org/TR/cors/)可用來允許跨原始來源 SignalR 連線的瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="f8bba-107">[Cross-origin resource sharing (CORS)](https://www.w3.org/TR/cors/) can be used to allow cross-origin SignalR connections in the browser.</span></span> <span data-ttu-id="f8bba-108">如果 JavaScript 程式碼裝載在不同的網域從 SignalR 應用程式[CORS 中介軟體](xref:security/cors)必須允許 JavaScript 才可連線到 SignalR 應用程式啟用。</span><span class="sxs-lookup"><span data-stu-id="f8bba-108">If JavaScript code is hosted on a different domain from the SignalR app, [CORS middleware](xref:security/cors) must be enabled to allow the JavaScript to connect to the SignalR app.</span></span> <span data-ttu-id="f8bba-109">允許跨原始來源要求，只能從您信任的網域或控制項。</span><span class="sxs-lookup"><span data-stu-id="f8bba-109">Allow cross-origin requests only from domains you trust or control.</span></span> <span data-ttu-id="f8bba-110">例如: </span><span class="sxs-lookup"><span data-stu-id="f8bba-110">For example:</span></span>

* <span data-ttu-id="f8bba-111">您的網站裝載於 `http://www.example.com`</span><span class="sxs-lookup"><span data-stu-id="f8bba-111">Your site is hosted on `http://www.example.com`</span></span>
* <span data-ttu-id="f8bba-112">您的 SignalR 應用程式裝載於 `http://signalr.example.com`</span><span class="sxs-lookup"><span data-stu-id="f8bba-112">Your SignalR app is hosted on `http://signalr.example.com`</span></span>

<span data-ttu-id="f8bba-113">應該只允許原點的 SignalR 應用程式中設定 CORS `www.example.com`。</span><span class="sxs-lookup"><span data-stu-id="f8bba-113">CORS should be configured in the SignalR app to only allow the origin `www.example.com`.</span></span>

<span data-ttu-id="f8bba-114">如需有關如何設定 CORS 的詳細資訊，請參閱 <<c0> [ 啟用跨源要求 (CORS)](xref:security/cors)。</span><span class="sxs-lookup"><span data-stu-id="f8bba-114">For more information on configuring CORS, see [Enable Cross-Origin Requests (CORS)](xref:security/cors).</span></span> <span data-ttu-id="f8bba-115">SignalR**需要**下列的 CORS 原則：</span><span class="sxs-lookup"><span data-stu-id="f8bba-115">SignalR **requires** the following CORS policies:</span></span>

* <span data-ttu-id="f8bba-116">允許特定的預期的來源。</span><span class="sxs-lookup"><span data-stu-id="f8bba-116">Allow the specific expected origins.</span></span> <span data-ttu-id="f8bba-117">允許任何來源可以但**不**安全或建議。</span><span class="sxs-lookup"><span data-stu-id="f8bba-117">Allowing any origin is possible but is **not** secure or recommended.</span></span>
* <span data-ttu-id="f8bba-118">HTTP 方法`GET`和`POST`必須允許。</span><span class="sxs-lookup"><span data-stu-id="f8bba-118">HTTP methods `GET` and `POST` must be allowed.</span></span>
* <span data-ttu-id="f8bba-119">必須啟用認證，即使在不使用驗證。</span><span class="sxs-lookup"><span data-stu-id="f8bba-119">Credentials must be enabled, even when authentication is not used.</span></span>

<span data-ttu-id="f8bba-120">例如，下列的 CORS 原則允許 SignalR 瀏覽器的用戶端，裝載於`https://example.com`存取 SignalR 應用程式裝載於`https://signalr.example.com`:</span><span class="sxs-lookup"><span data-stu-id="f8bba-120">For example, the following CORS policy allows a SignalR browser client hosted on `https://example.com` to access the SignalR app hosted on `https://signalr.example.com`:</span></span>

[!code-csharp[Main](security/sample/Startup.cs?name=snippet1)]

> [!NOTE]
> <span data-ttu-id="f8bba-121">SignalR 與不相容的內建的 CORS 功能在 Azure App Service 中。</span><span class="sxs-lookup"><span data-stu-id="f8bba-121">SignalR is not compatible with the built-in CORS feature in Azure App Service.</span></span>

## <a name="websocket-origin-restriction"></a><span data-ttu-id="f8bba-122">WebSocket Origin Restriction</span><span class="sxs-lookup"><span data-stu-id="f8bba-122">WebSocket Origin Restriction</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="f8bba-123">CORS 所提供的保護不套用至 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="f8bba-123">The protections provided by CORS don't apply to WebSockets.</span></span> <span data-ttu-id="f8bba-124">如原始 WebSockets 限制，請參閱[WebSockets 原始限制](xref:fundamentals/websockets#websocket-origin-restriction)。</span><span class="sxs-lookup"><span data-stu-id="f8bba-124">For origin restriction on WebSockets, read [WebSockets origin restriction](xref:fundamentals/websockets#websocket-origin-restriction).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="f8bba-125">CORS 所提供的保護不套用至 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="f8bba-125">The protections provided by CORS don't apply to WebSockets.</span></span> <span data-ttu-id="f8bba-126">瀏覽器**不**會：</span><span class="sxs-lookup"><span data-stu-id="f8bba-126">Browsers do **not**:</span></span>

* <span data-ttu-id="f8bba-127">執行 CORS 的事前要求。</span><span class="sxs-lookup"><span data-stu-id="f8bba-127">Perform CORS pre-flight requests.</span></span>
* <span data-ttu-id="f8bba-128">進行 WebSocket 要求時，採用 `Access-Control` 標頭中所指定的限制。</span><span class="sxs-lookup"><span data-stu-id="f8bba-128">Respect the restrictions specified in `Access-Control` headers when making WebSocket requests.</span></span>

<span data-ttu-id="f8bba-129">不過，瀏覽器會在發出 WebSocket 要求時，傳送 `Origin` 標頭。</span><span class="sxs-lookup"><span data-stu-id="f8bba-129">However, browsers do send the `Origin` header when issuing WebSocket requests.</span></span> <span data-ttu-id="f8bba-130">應設定應用程式驗證這些標頭，以確保只允許來自預期來源的 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="f8bba-130">Applications should be configured to validate these headers to ensure that only WebSockets coming from the expected origins are allowed.</span></span>

<span data-ttu-id="f8bba-131">在 ASP.NET Core 2.1 和更新版本，標頭驗證，可透過自訂的中介軟體放**之前`UseSignalR`，並驗證中介軟體**在`Configure`:</span><span class="sxs-lookup"><span data-stu-id="f8bba-131">In ASP.NET Core 2.1 and later, header validation can be achieved using a custom middleware placed **before `UseSignalR`, and authentication middleware** in `Configure`:</span></span>

[!code-csharp[Main](security/sample/Startup.cs?name=snippet2)]

> [!NOTE]
> <span data-ttu-id="f8bba-132">因為 `Origin` 由用戶端控制，所以和 `Referer` 標頭一樣可能受到偽造。</span><span class="sxs-lookup"><span data-stu-id="f8bba-132">The `Origin` header is controlled by the client and, like the `Referer` header, can be faked.</span></span> <span data-ttu-id="f8bba-133">這些標頭應該**不**用作為驗證機制。</span><span class="sxs-lookup"><span data-stu-id="f8bba-133">These headers should **not** be used as an authentication mechanism.</span></span>

::: moniker-end

## <a name="access-token-logging"></a><span data-ttu-id="f8bba-134">存取權杖的記錄</span><span class="sxs-lookup"><span data-stu-id="f8bba-134">Access token logging</span></span>

<span data-ttu-id="f8bba-135">使用 WebSockets 或 Server-Sent 事件時，瀏覽器用戶端會查詢字串中傳送存取權杖。</span><span class="sxs-lookup"><span data-stu-id="f8bba-135">When using WebSockets or Server-Sent Events, the browser client sends the access token in the query string.</span></span> <span data-ttu-id="f8bba-136">接收存取權杖，透過查詢字串是使用標準通常一樣安全`Authorization`標頭。</span><span class="sxs-lookup"><span data-stu-id="f8bba-136">Receiving the access token via query string is generally as secure as using the standard `Authorization` header.</span></span> <span data-ttu-id="f8bba-137">您應該一律使用 HTTPS，若要確保安全的端對端連線的用戶端與伺服器之間。</span><span class="sxs-lookup"><span data-stu-id="f8bba-137">You should always use HTTPS to ensure a secure end-to-end connection between the client and the server.</span></span> <span data-ttu-id="f8bba-138">許多網頁伺服器會記錄每個要求，包括查詢字串的 URL。</span><span class="sxs-lookup"><span data-stu-id="f8bba-138">Many web servers log the URL for each request, including the query string.</span></span> <span data-ttu-id="f8bba-139">記錄的 Url 可能會記錄的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="f8bba-139">Logging the URLs may log the access token.</span></span> <span data-ttu-id="f8bba-140">ASP.NET Core 記錄每個要求的 URL，根據預設，會包含查詢字串。</span><span class="sxs-lookup"><span data-stu-id="f8bba-140">ASP.NET Core logs the URL for each request by default, which will include the query string.</span></span> <span data-ttu-id="f8bba-141">例如: </span><span class="sxs-lookup"><span data-stu-id="f8bba-141">For example:</span></span>

```
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[1]
      Request starting HTTP/1.1 GET http://localhost:5000/myhub?access_token=1234
```

<span data-ttu-id="f8bba-142">如果您有關於使用您的伺服器記錄檔中記錄這項資料的考量，您可以停用此記錄完全設定`Microsoft.AspNetCore.Hosting`記錄器`Warning`層級或更高版本 (這些訊息全都寫入於`Info`層級)。</span><span class="sxs-lookup"><span data-stu-id="f8bba-142">If you have concerns about logging this data with your server logs, you can disable this logging entirely by configuring the `Microsoft.AspNetCore.Hosting` logger to the `Warning` level or above (these messages are written at `Info` level).</span></span> <span data-ttu-id="f8bba-143">請參閱文件[記錄檔篩選](xref:fundamentals/logging/index#log-filtering)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f8bba-143">See the documentation on [Log Filtering](xref:fundamentals/logging/index#log-filtering) for more information.</span></span> <span data-ttu-id="f8bba-144">如果您仍然想要記錄特定的要求資訊，您可以[撰寫的中介軟體](xref:fundamentals/middleware/write)來記錄的資料要求，並篩選出`access_token`查詢字串值 （如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="f8bba-144">If you still want to log certain request information, you can [write a middleware](xref:fundamentals/middleware/write) to log the data you require and filter out the `access_token` query string value (if present).</span></span>

## <a name="exceptions"></a><span data-ttu-id="f8bba-145">例外狀況</span><span class="sxs-lookup"><span data-stu-id="f8bba-145">Exceptions</span></span>

<span data-ttu-id="f8bba-146">例外狀況訊息通常會被認為不應該洩漏給用戶端的敏感性資料。</span><span class="sxs-lookup"><span data-stu-id="f8bba-146">Exception messages are generally considered sensitive data that shouldn't be revealed to a client.</span></span> <span data-ttu-id="f8bba-147">根據預設，SignalR 不會傳送至用戶端中樞方法擲回的例外狀況詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f8bba-147">By default, SignalR doesn't send the details of an exception thrown by a hub method to the client.</span></span> <span data-ttu-id="f8bba-148">相反地，用戶端會收到一般的訊息，指出發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="f8bba-148">Instead, the client receives a generic message indicating an error occurred.</span></span> <span data-ttu-id="f8bba-149">例外狀況訊息傳遞至用戶端可以覆寫 （例如在開發或測試） 與[ `EnableDetailedErrors` ](xref:signalr/configuration#configure-server-options)。</span><span class="sxs-lookup"><span data-stu-id="f8bba-149">Exception message delivery to the client can be overridden (for example in development or test) with [`EnableDetailedErrors`](xref:signalr/configuration#configure-server-options).</span></span> <span data-ttu-id="f8bba-150">例外狀況訊息不應該在生產環境應用程式中的用戶端上公開。</span><span class="sxs-lookup"><span data-stu-id="f8bba-150">Exception messages should not be exposed to the client in production apps.</span></span>

## <a name="buffer-management"></a><span data-ttu-id="f8bba-151">緩衝區管理</span><span class="sxs-lookup"><span data-stu-id="f8bba-151">Buffer management</span></span>

<span data-ttu-id="f8bba-152">SignalR 使用來管理內送和外寄訊息的每個連線的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="f8bba-152">SignalR uses per-connection buffers to manage incoming and outgoing messages.</span></span> <span data-ttu-id="f8bba-153">根據預設，SignalR 會限制為 32 KB 的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="f8bba-153">By default, SignalR limits these buffers to 32 KB.</span></span> <span data-ttu-id="f8bba-154">用戶端或伺服器可以傳送的最大訊息為 32 KB。</span><span class="sxs-lookup"><span data-stu-id="f8bba-154">The largest message a client or server can send is 32 KB.</span></span> <span data-ttu-id="f8bba-155">訊息的連線所耗用的記憶體上限為 32 KB。</span><span class="sxs-lookup"><span data-stu-id="f8bba-155">The maximum memory consumed by a connection for messages is 32 KB.</span></span> <span data-ttu-id="f8bba-156">如果您的訊息永遠小於 32 KB，您可以減少此限制，其中：</span><span class="sxs-lookup"><span data-stu-id="f8bba-156">If your messages are always smaller than 32 KB, you can reduce the limit, which:</span></span>

* <span data-ttu-id="f8bba-157">用戶端可防止傳送較大的訊息。</span><span class="sxs-lookup"><span data-stu-id="f8bba-157">Prevents a client from being able to send a larger message.</span></span>
* <span data-ttu-id="f8bba-158">伺服器會永遠不需要配置大型緩衝區來接受訊息。</span><span class="sxs-lookup"><span data-stu-id="f8bba-158">The server will never need to allocate large buffers to accept messages.</span></span>

<span data-ttu-id="f8bba-159">如果您的訊息大於 32 KB，您可以提高限制。</span><span class="sxs-lookup"><span data-stu-id="f8bba-159">If your messages are larger than 32 KB, you can increase the limit.</span></span> <span data-ttu-id="f8bba-160">增加此限制表示：</span><span class="sxs-lookup"><span data-stu-id="f8bba-160">Increasing this limit means:</span></span>

* <span data-ttu-id="f8bba-161">用戶端可能會導致伺服器配置大量記憶體緩衝區。</span><span class="sxs-lookup"><span data-stu-id="f8bba-161">The client can cause the server to allocate large memory buffers.</span></span>
* <span data-ttu-id="f8bba-162">Server 配置大型緩衝區可能會降低並行連線數目。</span><span class="sxs-lookup"><span data-stu-id="f8bba-162">Server allocation of large buffers may reduce the number of concurrent connections.</span></span>

<span data-ttu-id="f8bba-163">有內送和外寄訊息的限制，都可以在設定成[ `HttpConnectionDispatcherOptions` ](xref:signalr/configuration#configure-server-options)物件中設定`MapHub`:</span><span class="sxs-lookup"><span data-stu-id="f8bba-163">There are limits for incoming and outgoing messages, both can be configured on the [`HttpConnectionDispatcherOptions`](xref:signalr/configuration#configure-server-options) object configured in `MapHub`:</span></span>

* <span data-ttu-id="f8bba-164">`ApplicationMaxBufferSize` 表示從用戶端的最大位元組數，伺服器緩衝區。</span><span class="sxs-lookup"><span data-stu-id="f8bba-164">`ApplicationMaxBufferSize` represents the maximum number of bytes from the client that the server buffers.</span></span> <span data-ttu-id="f8bba-165">如果用戶端會嘗試傳送訊息的大小超過此限制，可能會關閉連線。</span><span class="sxs-lookup"><span data-stu-id="f8bba-165">If the client attempts to send a message larger than this limit, the connection may be closed.</span></span>
* <span data-ttu-id="f8bba-166">`TransportMaxBufferSize` 代表伺服器可以傳送的位元組的數目上限。</span><span class="sxs-lookup"><span data-stu-id="f8bba-166">`TransportMaxBufferSize` represents the maximum number of bytes the server can send.</span></span> <span data-ttu-id="f8bba-167">如果伺服器會嘗試傳送訊息 （從中樞方法的包括傳回值） 的大小超過此限制，將會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f8bba-167">If the server attempts to send a message (including return values from hub methods) larger than this limit, an exception will be thrown.</span></span>

<span data-ttu-id="f8bba-168">若要設定的限制`0`停用限制。</span><span class="sxs-lookup"><span data-stu-id="f8bba-168">Setting the limit to `0` disables the limit.</span></span> <span data-ttu-id="f8bba-169">移除此限制可讓用戶端傳送任何大小的訊息。</span><span class="sxs-lookup"><span data-stu-id="f8bba-169">Removing the limit allows a client to send a message of any size.</span></span> <span data-ttu-id="f8bba-170">惡意用戶端傳送大型訊息可能會導致過多的記憶體配置。</span><span class="sxs-lookup"><span data-stu-id="f8bba-170">Malicious clients sending large messages can cause excess memory to be allocated.</span></span> <span data-ttu-id="f8bba-171">過多的記憶體使用量可以大幅減少並行連線數目。</span><span class="sxs-lookup"><span data-stu-id="f8bba-171">Excess memory usage can significantly reduce the number of concurrent connections.</span></span>
