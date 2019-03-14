---
title: 在 ASP.NET 4.x 和 ASP.NET Core 之間進行選擇
author: rick-anderson
description: 說明 ASP.NET Core 與ASP.NET 4.x，以及如何在兩者之間進行選擇。
ms.author: riande
ms.custom: seodec18
ms.date: 09/11/2018
uid: fundamentals/choose-between-aspnet-and-aspnetcore
ms.openlocfilehash: eb216bdac7dd029c3d985f2edd9e70eb91f42883
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040985"
---
# <a name="choose-between-aspnet-4x-and-aspnet-core"></a><span data-ttu-id="91603-103">在 ASP.NET 4.x 和 ASP.NET Core 之間進行選擇</span><span class="sxs-lookup"><span data-stu-id="91603-103">Choose between ASP.NET 4.x and ASP.NET Core</span></span>

<span data-ttu-id="91603-104">ASP.NET Core 是 ASP.NET 4.x 的重新設計。</span><span class="sxs-lookup"><span data-stu-id="91603-104">ASP.NET Core is a redesign of ASP.NET 4.x.</span></span> <span data-ttu-id="91603-105">本文列出兩者之間的差異。</span><span class="sxs-lookup"><span data-stu-id="91603-105">This article lists the differences between them.</span></span>

## <a name="aspnet-core"></a><span data-ttu-id="91603-106">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="91603-106">ASP.NET Core</span></span>

<span data-ttu-id="91603-107">ASP.NET Core 是一種開放原始碼、跨平台的架構，用於在 Windows、macOS 或 Linux 上建置現代化的雲端式 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91603-107">ASP.NET Core is an open-source, cross-platform framework for building modern, cloud-based web apps on Windows, macOS, or Linux.</span></span>

[!INCLUDE[](~/includes/benefits.md)]

## <a name="aspnet-4x"></a><span data-ttu-id="91603-108">ASP.NET 4.x</span><span class="sxs-lookup"><span data-stu-id="91603-108">ASP.NET 4.x</span></span>

<span data-ttu-id="91603-109">ASP.NET 4.x 是一個成熟的架構，其提供在 Windows 上建置企業級伺服器端 Web 應用程式所需的服務。</span><span class="sxs-lookup"><span data-stu-id="91603-109">ASP.NET 4.x is a mature framework that provides the services needed to build enterprise-grade, server-based web apps on Windows.</span></span>

## <a name="framework-selection"></a><span data-ttu-id="91603-110">選取 Framework</span><span class="sxs-lookup"><span data-stu-id="91603-110">Framework selection</span></span>

<span data-ttu-id="91603-111">下表將比較 ASP.NET Core 與 ASP.NET 4.x。</span><span class="sxs-lookup"><span data-stu-id="91603-111">The following table compares ASP.NET Core to ASP.NET 4.x.</span></span>

| <span data-ttu-id="91603-112">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="91603-112">ASP.NET Core</span></span> | <span data-ttu-id="91603-113">ASP.NET 4.x</span><span class="sxs-lookup"><span data-stu-id="91603-113">ASP.NET 4.x</span></span> |
|---|---|
|<span data-ttu-id="91603-114">為 Windows、macOS 或 Linux 建置</span><span class="sxs-lookup"><span data-stu-id="91603-114">Build for Windows, macOS, or Linux</span></span>|<span data-ttu-id="91603-115">為 Windows 建置</span><span class="sxs-lookup"><span data-stu-id="91603-115">Build for Windows</span></span>|
|<span data-ttu-id="91603-116">從 ASP.NET Core 2.x 開始，[Razor 頁面](xref:razor-pages/index)是建立 Web UI 的建議方法。</span><span class="sxs-lookup"><span data-stu-id="91603-116">[Razor Pages](xref:razor-pages/index) is the recommended approach to create a Web UI as of ASP.NET Core 2.x.</span></span> <span data-ttu-id="91603-117">另請參閱 [MVC](xref:mvc/overview)、[Web API](xref:tutorials/first-web-api) 和 [SignalR](xref:signalr/introduction)。</span><span class="sxs-lookup"><span data-stu-id="91603-117">See also [MVC](xref:mvc/overview), [Web API](xref:tutorials/first-web-api), and [SignalR](xref:signalr/introduction).</span></span>|<span data-ttu-id="91603-118">使用 [Web Forms](/aspnet/web-forms)、[SignalR](/aspnet/signalr)、[MVC](/aspnet/mvc)、[Web API](/aspnet/web-api/)、[WebHooks](/aspnet/webhooks/) 或 [Web Pages](/aspnet/web-pages)</span><span class="sxs-lookup"><span data-stu-id="91603-118">Use [Web Forms](/aspnet/web-forms), [SignalR](/aspnet/signalr), [MVC](/aspnet/mvc), [Web API](/aspnet/web-api/), [WebHooks](/aspnet/webhooks/), or [Web Pages](/aspnet/web-pages)</span></span>|
|<span data-ttu-id="91603-119">每部電腦多個版本</span><span class="sxs-lookup"><span data-stu-id="91603-119">Multiple versions per machine</span></span>|<span data-ttu-id="91603-120">每部電腦一個版本</span><span class="sxs-lookup"><span data-stu-id="91603-120">One version per machine</span></span>|
|<span data-ttu-id="91603-121">在 Visual Studio、[Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/) 或 [Visual Studio Code](https://code.visualstudio.com/) 中使用 C# 或 F# 進行開發</span><span class="sxs-lookup"><span data-stu-id="91603-121">Develop with Visual Studio, [Visual Studio for Mac](https://www.visualstudio.com/vs/visual-studio-mac/), or [Visual Studio Code](https://code.visualstudio.com/) using C# or F#</span></span>|<span data-ttu-id="91603-122">在 Visual Studio 中使用 C#、VB 或 F# 進行開發</span><span class="sxs-lookup"><span data-stu-id="91603-122">Develop with Visual Studio using C#, VB, or F#</span></span>|
|<span data-ttu-id="91603-123">效能比 ASP.NET 4.x 更高</span><span class="sxs-lookup"><span data-stu-id="91603-123">Higher performance than ASP.NET 4.x</span></span>|<span data-ttu-id="91603-124">效能良好</span><span class="sxs-lookup"><span data-stu-id="91603-124">Good performance</span></span>|
|[<span data-ttu-id="91603-125">選擇 .NET Framework 或.NET Core 執行階段</span><span class="sxs-lookup"><span data-stu-id="91603-125">Choose .NET Framework or .NET Core runtime</span></span>](/dotnet/standard/choosing-core-framework-server)|<span data-ttu-id="91603-126">使用 .NET Framework 執行階段</span><span class="sxs-lookup"><span data-stu-id="91603-126">Use .NET Framework runtime</span></span>|

<span data-ttu-id="91603-127">如需 .NET Framework 上的 ASP.NET Core 2.x 支援資訊，請參閱[將目標指向 .NET Framework 的 ASP.NET Core](xref:index#target-framework)。</span><span class="sxs-lookup"><span data-stu-id="91603-127">See [ASP.NET Core targeting .NET Framework](xref:index#target-framework) for information on ASP.NET Core 2.x support on .NET Framework.</span></span>

## <a name="aspnet-core-scenarios"></a><span data-ttu-id="91603-128">ASP.NET Core 案例</span><span class="sxs-lookup"><span data-stu-id="91603-128">ASP.NET Core scenarios</span></span>

* <span data-ttu-id="91603-129">從 ASP.NET Core 2.x 開始，[Razor 頁面](xref:razor-pages/index)是建立 Web UI 的建議方法。</span><span class="sxs-lookup"><span data-stu-id="91603-129">[Razor Pages](xref:razor-pages/index) is the recommended approach to create a Web UI as of ASP.NET Core 2.x.</span></span>
* [<span data-ttu-id="91603-130">網站</span><span class="sxs-lookup"><span data-stu-id="91603-130">Websites</span></span>](xref:tutorials/first-mvc-app/index)
* [<span data-ttu-id="91603-131">API</span><span class="sxs-lookup"><span data-stu-id="91603-131">APIs</span></span>](xref:tutorials/first-web-api)
* [<span data-ttu-id="91603-132">即時</span><span class="sxs-lookup"><span data-stu-id="91603-132">Real-time</span></span>](xref:signalr/index)
* [<span data-ttu-id="91603-133">將 ASP.NET Core 應用程式部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="91603-133">Deploy an ASP.NET Core app to Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet)

## <a name="aspnet-4x-scenarios"></a><span data-ttu-id="91603-134">ASP.NET 4.x 案例</span><span class="sxs-lookup"><span data-stu-id="91603-134">ASP.NET 4.x scenarios</span></span>

* [<span data-ttu-id="91603-135">網站</span><span class="sxs-lookup"><span data-stu-id="91603-135">Websites</span></span>](/aspnet/mvc)
* [<span data-ttu-id="91603-136">API</span><span class="sxs-lookup"><span data-stu-id="91603-136">APIs</span></span>](/aspnet/web-api)
* [<span data-ttu-id="91603-137">即時</span><span class="sxs-lookup"><span data-stu-id="91603-137">Real-time</span></span>](/aspnet/signalr)
* [<span data-ttu-id="91603-138">在 Azure 中建立 ASP.NET 4.x Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="91603-138">Create an ASP.NET 4.x web app in Azure</span></span>](/azure/app-service/app-service-web-get-started-dotnet-framework)

## <a name="additional-resources"></a><span data-ttu-id="91603-139">其他資源</span><span class="sxs-lookup"><span data-stu-id="91603-139">Additional resources</span></span>

* [<span data-ttu-id="91603-140">ASP.NET 簡介</span><span class="sxs-lookup"><span data-stu-id="91603-140">Introduction to ASP.NET</span></span>](/aspnet/overview)
* [<span data-ttu-id="91603-141">ASP.NET Core 簡介</span><span class="sxs-lookup"><span data-stu-id="91603-141">Introduction to ASP.NET Core</span></span>](xref:index)
* <xref:host-and-deploy/azure-apps/index>
