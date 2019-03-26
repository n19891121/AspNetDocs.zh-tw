---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: 使用 OWIN 自我裝載 ASP.NET Web API |Microsoft Docs
author: rick-anderson
description: 本教學課程會示範如何使用 OWIN 自我裝載 Web API 架構的主控台應用程式中裝載 ASP.NET Web API。 Open Web Interface for.NET (OWIN) d...
ms.author: riande
ms.date: 07/09/2013
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: a83d1350c2e984acd3c115afd27adfe2b05adb2f
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/25/2019
ms.locfileid: "58424545"
---
<a name="use-owin-to-self-host-aspnet-web-api"></a><span data-ttu-id="51405-104">使用 OWIN 自我裝載 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="51405-104">Use OWIN to Self-Host ASP.NET Web API</span></span> 
====================

> <span data-ttu-id="51405-105">本教學課程會示範如何使用 OWIN 自我裝載 Web API 架構的主控台應用程式中裝載 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="51405-105">This tutorial shows how to host ASP.NET Web API in a console application, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="51405-106">[Open Web Interface for.NET](http://owin.org) (OWIN) 定義.NET web 伺服器和 web 應用程式之間的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="51405-106">[Open Web Interface for .NET](http://owin.org) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="51405-107">OWIN 可分隔的伺服器，讓 OWIN 很適合用於自我裝載的 web 應用程式，在您自己的程序，IIS 外部的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51405-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="51405-108">在本教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="51405-108">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="51405-109">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="51405-109">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/) 
> - <span data-ttu-id="51405-110">Web API 5.2.7</span><span class="sxs-lookup"><span data-stu-id="51405-110">Web API 5.2.7</span></span>


> [!NOTE]
> <span data-ttu-id="51405-111">您可以在本教學課程中找到完整的原始程式碼[github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample)。</span><span class="sxs-lookup"><span data-stu-id="51405-111">You can find the complete source code for this tutorial at [github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).</span></span>


## <a name="create-a-console-application"></a><span data-ttu-id="51405-112">建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="51405-112">Create a console application</span></span>

<span data-ttu-id="51405-113">在 [**檔案**] 功能表**新增**，然後選取**專案**。</span><span class="sxs-lookup"><span data-stu-id="51405-113">On the **File** menu,  **New**, then select **Project**.</span></span> <span data-ttu-id="51405-114">從**已安裝**下方**視覺化C#** ，選取**Windows Desktop** ，然後選取**主控台應用程式 (.Net Framework)**。</span><span class="sxs-lookup"><span data-stu-id="51405-114">From **Installed**, under **Visual C#**, select **Windows Desktop** and then select **Console App (.Net Framework)**.</span></span> <span data-ttu-id="51405-115">將專案命名為"OwinSelfhostSample 」，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="51405-115">Name the project "OwinSelfhostSample" and select **OK**.</span></span>

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="51405-116">新增 Web API 和 OWIN 套件</span><span class="sxs-lookup"><span data-stu-id="51405-116">Add the Web API and OWIN packages</span></span>

<span data-ttu-id="51405-117">從**工具**功能表上，選取**NuGet 套件管理員**，然後選取**Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="51405-117">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="51405-118">在 [套件管理員主控台] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="51405-118">In the Package Manager Console window, enter the following command:</span></span>

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

<span data-ttu-id="51405-119">這會安裝 WebAPI OWIN selfhost 封裝和所有必要的 OWIN 套件。</span><span class="sxs-lookup"><span data-stu-id="51405-119">This will install the WebAPI OWIN selfhost package and all the required OWIN packages.</span></span>

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="51405-120">設定 Web API 的自我裝載</span><span class="sxs-lookup"><span data-stu-id="51405-120">Configure Web API for self-host</span></span>

<span data-ttu-id="51405-121">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取**新增** / **類別**若要加入新的類別。</span><span class="sxs-lookup"><span data-stu-id="51405-121">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="51405-122">將類別命名為 `Startup` 。</span><span class="sxs-lookup"><span data-stu-id="51405-122">Name the class `Startup`.</span></span>

![](use-owin-to-self-host-web-api/_static/image5.png)

<span data-ttu-id="51405-123">您可以將所有未定案程式碼，此檔案中取代為下列：</span><span class="sxs-lookup"><span data-stu-id="51405-123">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="51405-124">新增 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="51405-124">Add a Web API controller</span></span>

<span data-ttu-id="51405-125">接下來，新增 Web API 控制器類別。</span><span class="sxs-lookup"><span data-stu-id="51405-125">Next, add a Web API controller class.</span></span> <span data-ttu-id="51405-126">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取**新增** / **類別**若要加入新的類別。</span><span class="sxs-lookup"><span data-stu-id="51405-126">In Solution Explorer, right-click the project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="51405-127">將類別命名為 `ValuesController` 。</span><span class="sxs-lookup"><span data-stu-id="51405-127">Name the class `ValuesController`.</span></span>

<span data-ttu-id="51405-128">您可以將所有未定案程式碼，此檔案中取代為下列：</span><span class="sxs-lookup"><span data-stu-id="51405-128">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a><span data-ttu-id="51405-129">啟動 OWIN 主機和 HttpClient 要求</span><span class="sxs-lookup"><span data-stu-id="51405-129">Start the OWIN Host and make a request with HttpClient</span></span>

<span data-ttu-id="51405-130">您可以將所有的 Program.cs 檔案中的未定案程式碼取代為下列：</span><span class="sxs-lookup"><span data-stu-id="51405-130">Replace all of the boilerplate code in the Program.cs file with the following:</span></span>

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a><span data-ttu-id="51405-131">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="51405-131">Run the application</span></span>

<span data-ttu-id="51405-132">若要執行應用程式，請在 Visual Studio 中按 F5。</span><span class="sxs-lookup"><span data-stu-id="51405-132">To run the application, press F5 in Visual Studio.</span></span> <span data-ttu-id="51405-133">輸出看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="51405-133">The output should look like the following:</span></span>

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a><span data-ttu-id="51405-134">其他資源</span><span class="sxs-lookup"><span data-stu-id="51405-134">Additional resources</span></span>

[<span data-ttu-id="51405-135">Katana 專案概觀</span><span class="sxs-lookup"><span data-stu-id="51405-135">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[<span data-ttu-id="51405-136">裝載的 Azure 背景工作角色中的 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="51405-136">Host ASP.NET Web API in an Azure Worker Role</span></span>](host-aspnet-web-api-in-an-azure-worker-role.md)
