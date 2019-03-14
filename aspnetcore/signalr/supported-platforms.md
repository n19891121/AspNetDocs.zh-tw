---
title: ASP.NET Core SignalR 支援的平台
author: bradygaster
description: 了解支援的平台 ASP.NET Core SignalR。
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 11/12/2018
uid: signalr/supported-platforms
ms.openlocfilehash: e4e84baf0120036b473eac256107b46a4accfe37
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57053385"
---
# <a name="aspnet-core-signalr-supported-platforms"></a><span data-ttu-id="ba6c8-103">ASP.NET Core SignalR 支援的平台</span><span class="sxs-lookup"><span data-stu-id="ba6c8-103">ASP.NET Core SignalR supported platforms</span></span>

## <a name="server-system-requirements"></a><span data-ttu-id="ba6c8-104">伺服器系統需求</span><span class="sxs-lookup"><span data-stu-id="ba6c8-104">Server system requirements</span></span>

<span data-ttu-id="ba6c8-105">適用於 ASP.NET Core SignalR 支援 ASP.NET Core 支援的任何伺服器平台。</span><span class="sxs-lookup"><span data-stu-id="ba6c8-105">SignalR for ASP.NET Core supports any server platform that ASP.NET Core supports.</span></span>

## <a name="javascript-client"></a><span data-ttu-id="ba6c8-106">JavaScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="ba6c8-106">JavaScript client</span></span>

<span data-ttu-id="ba6c8-107">[JavaScript 用戶端](https://www.npmjs.com/package/@aspnet/signalr)NodeJS 8 和更新版本與下列瀏覽器上執行：</span><span class="sxs-lookup"><span data-stu-id="ba6c8-107">The [JavaScript client](https://www.npmjs.com/package/@aspnet/signalr) runs on NodeJS 8 and later versions and the following browsers:</span></span>

| <span data-ttu-id="ba6c8-108">瀏覽器</span><span class="sxs-lookup"><span data-stu-id="ba6c8-108">Browser</span></span>                         | <span data-ttu-id="ba6c8-109">版本</span><span class="sxs-lookup"><span data-stu-id="ba6c8-109">Version</span></span> |
| ------------------------------- | ------- |
| <span data-ttu-id="ba6c8-110">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="ba6c8-110">Microsoft Edge</span></span>                  | <span data-ttu-id="ba6c8-111">目前的</span><span class="sxs-lookup"><span data-stu-id="ba6c8-111">current</span></span> |
| <span data-ttu-id="ba6c8-112">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="ba6c8-112">Mozilla Firefox</span></span>                 | <span data-ttu-id="ba6c8-113">目前的</span><span class="sxs-lookup"><span data-stu-id="ba6c8-113">current</span></span> |
| <span data-ttu-id="ba6c8-114">Google Chrome;包含 Android</span><span class="sxs-lookup"><span data-stu-id="ba6c8-114">Google Chrome; includes Android</span></span> | <span data-ttu-id="ba6c8-115">目前的</span><span class="sxs-lookup"><span data-stu-id="ba6c8-115">current</span></span> |
| <span data-ttu-id="ba6c8-116">Safari;包含 iOS</span><span class="sxs-lookup"><span data-stu-id="ba6c8-116">Safari; includes iOS</span></span>            | <span data-ttu-id="ba6c8-117">目前的</span><span class="sxs-lookup"><span data-stu-id="ba6c8-117">current</span></span> |
| <span data-ttu-id="ba6c8-118">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="ba6c8-118">Microsoft Internet Explorer</span></span>     | <span data-ttu-id="ba6c8-119">11</span><span class="sxs-lookup"><span data-stu-id="ba6c8-119">11</span></span>      |
 
## <a name="net-client"></a><span data-ttu-id="ba6c8-120">.NET 用戶端</span><span class="sxs-lookup"><span data-stu-id="ba6c8-120">.NET client</span></span>

<span data-ttu-id="ba6c8-121">[.NET 用戶端](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/)ASP.NET Core 支援的任何平台上執行。</span><span class="sxs-lookup"><span data-stu-id="ba6c8-121">The [.NET client](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) runs on any platform supported by ASP.NET Core.</span></span> <span data-ttu-id="ba6c8-122">例如， [Xamarin 開發人員可以使用 SignalR](https://github.com/aspnet/Announcements/issues/305)建置 Android 應用程式使用 Xamarin.Android 8.4.0.1 和更新版本 」 與 「 使用 Xamarin.iOS 11.14.0.4 的 iOS 應用程式和更新版本。</span><span class="sxs-lookup"><span data-stu-id="ba6c8-122">For example, [Xamarin developers can use SignalR](https://github.com/aspnet/Announcements/issues/305) for building Android apps using Xamarin.Android 8.4.0.1 and later and iOS apps using Xamarin.iOS 11.14.0.4 and later.</span></span>

<span data-ttu-id="ba6c8-123">如果伺服器是執行 IIS，Websocket 傳輸需要 IIS 8.0 或更新版本的 Windows Server 2012 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ba6c8-123">If the server runs IIS, the WebSockets transport requires IIS 8.0 or higher on Windows Server 2012 or higher.</span></span> <span data-ttu-id="ba6c8-124">所有平台都支援其他傳輸。</span><span class="sxs-lookup"><span data-stu-id="ba6c8-124">Other transports are supported on all platforms.</span></span>

## <a name="java-client"></a><span data-ttu-id="ba6c8-125">Java 用戶端</span><span class="sxs-lookup"><span data-stu-id="ba6c8-125">Java client</span></span>

<span data-ttu-id="ba6c8-126">[Java 用戶端](https://search.maven.org/artifact/com.microsoft.aspnet/signalr)支援 Java 8 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="ba6c8-126">The [Java client](https://search.maven.org/artifact/com.microsoft.aspnet/signalr) supports Java 8 and later versions.</span></span>

## <a name="unsupported-clients"></a><span data-ttu-id="ba6c8-127">不支援的用戶端</span><span class="sxs-lookup"><span data-stu-id="ba6c8-127">Unsupported clients</span></span>

<span data-ttu-id="ba6c8-128">下列用戶端可用，但會實驗性或非官方。</span><span class="sxs-lookup"><span data-stu-id="ba6c8-128">The following clients are available but are experimental or unofficial.</span></span> <span data-ttu-id="ba6c8-129">它們目前不支援，且可能永遠無法。</span><span class="sxs-lookup"><span data-stu-id="ba6c8-129">They aren't currently supported and may never be.</span></span>

* [<span data-ttu-id="ba6c8-130">C + + 用戶端</span><span class="sxs-lookup"><span data-stu-id="ba6c8-130">C++ client</span></span>](https://github.com/aspnet/SignalR/tree/master/clients/cpp)

* [<span data-ttu-id="ba6c8-131">Swift 的用戶端</span><span class="sxs-lookup"><span data-stu-id="ba6c8-131">Swift client</span></span>](https://github.com/moozzyk/SignalR-Client-Swift)
