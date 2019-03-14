---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: 新增模型 (VB) |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將教導您建置使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，也就是 ASP.NET MVC Web 應用程式的基本概念...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: b1370148018faa8c6c884251bfa86761f45d7e49
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058045"
---
<a name="adding-a-model-vb"></a><span data-ttu-id="7f530-103">新增模型 (VB)</span><span class="sxs-lookup"><span data-stu-id="7f530-103">Adding a Model (VB)</span></span>
====================
<span data-ttu-id="7f530-104">藉由[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="7f530-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="7f530-105">本教學課程將教導您建置使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，也就是 Microsoft Visual Studio 的免費版本的 ASP.NET MVC Web 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="7f530-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="7f530-106">在開始之前，請確定您已安裝符合下列先決條件。</span><span class="sxs-lookup"><span data-stu-id="7f530-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="7f530-107">您可以安裝所有人都按下列連結：[Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="7f530-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="7f530-108">或者，您可以個別安裝的必要條件，使用下列連結：</span><span class="sxs-lookup"><span data-stu-id="7f530-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="7f530-109">Visual Studio Web Developer Express SP1 必要條件</span><span class="sxs-lookup"><span data-stu-id="7f530-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="7f530-110">ASP.NET MVC 3 Tools Update</span><span class="sxs-lookup"><span data-stu-id="7f530-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="7f530-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行階段 + 工具支援）</span><span class="sxs-lookup"><span data-stu-id="7f530-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="7f530-112">如果您使用 Visual Studio 2010，而不 Visual Web Developer 2010，請按一下下列連結安裝必要條件：[Visual Studio 2010 的必要元件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="7f530-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="7f530-113">使用本主題隨附了 VB.NET 原始程式碼的 Visual Web Developer 專案。</span><span class="sxs-lookup"><span data-stu-id="7f530-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="7f530-114">[下載 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="7f530-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="7f530-115">如果您偏好 C#，切換至[C# 版本](../cs/adding-a-model.md)本教學課程。</span><span class="sxs-lookup"><span data-stu-id="7f530-115">If you prefer C#, switch to the [C# version](../cs/adding-a-model.md) of this tutorial.</span></span>


## <a name="adding-a-model"></a><span data-ttu-id="7f530-116">新增模型</span><span class="sxs-lookup"><span data-stu-id="7f530-116">Adding a Model</span></span>

<span data-ttu-id="7f530-117">在本節中，您將新增一些類別來管理資料庫中的電影。</span><span class="sxs-lookup"><span data-stu-id="7f530-117">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="7f530-118">這些類別是 ASP.NET MVC 應用程式的 「 模型 」 部分。</span><span class="sxs-lookup"><span data-stu-id="7f530-118">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="7f530-119">您將使用稱為 Entity Framework 的.NET Framework 資料存取技術，來定義和使用這些模型類別。</span><span class="sxs-lookup"><span data-stu-id="7f530-119">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="7f530-120">Entity Framework （通常稱為 EF） 支援，開發架構稱為*Code First*。</span><span class="sxs-lookup"><span data-stu-id="7f530-120">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="7f530-121">程式碼第一次可讓您撰寫簡單的類別來建立模型物件。</span><span class="sxs-lookup"><span data-stu-id="7f530-121">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="7f530-122">（這些也稱為是 POCO 類別，來自 「 純舊 CLR 物件 」。）然後您可以在即時從您的類別，可讓非常精簡且快速的開發工作流程所建立的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f530-122">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="7f530-123">新增模型類別</span><span class="sxs-lookup"><span data-stu-id="7f530-123">Adding Model Classes</span></span>

<span data-ttu-id="7f530-124">在 [**方案總管] 中**，以滑鼠右鍵按一下 *模型* 資料夾中，選取**新增**，然後選取**類別**。</span><span class="sxs-lookup"><span data-stu-id="7f530-124">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="7f530-125">將類別命名為"Movie"。</span><span class="sxs-lookup"><span data-stu-id="7f530-125">Name the class "Movie".</span></span>

<span data-ttu-id="7f530-126">加入下列五個屬性，以`Movie`類別：</span><span class="sxs-lookup"><span data-stu-id="7f530-126">Add the following five properties to the `Movie` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

<span data-ttu-id="7f530-127">我們將使用`Movie`類別來代表資料庫中的電影。</span><span class="sxs-lookup"><span data-stu-id="7f530-127">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="7f530-128">每個執行個體`Movie`物件會對應至資料庫資料表，以及每個屬性中的資料列`Movie`類別會對應至資料表的資料行。</span><span class="sxs-lookup"><span data-stu-id="7f530-128">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="7f530-129">在相同的檔案中，新增下列`MovieDBContext`類別：</span><span class="sxs-lookup"><span data-stu-id="7f530-129">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

<span data-ttu-id="7f530-130">`MovieDBContext`類別代表會處理擷取、 儲存及更新的 Entity Framework 電影資料庫內容`Movie`類別執行個體在資料庫中的。</span><span class="sxs-lookup"><span data-stu-id="7f530-130">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="7f530-131">`MovieDBContext`衍生自`DbContext`基底 Entity Framework 所提供的類別。</span><span class="sxs-lookup"><span data-stu-id="7f530-131">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="7f530-132">如需詳細資訊`DbContext`並`DbSet`，請參閱[Entity Framework 的產能改進](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)。</span><span class="sxs-lookup"><span data-stu-id="7f530-132">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="7f530-133">為了能夠參考`DbContext`並`DbSet`，您需要新增下列`imports`陳述式在檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="7f530-133">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `imports` statement at the top of the file:</span></span>

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

<span data-ttu-id="7f530-134">完整*Movie.vb*檔案如下所示。</span><span class="sxs-lookup"><span data-stu-id="7f530-134">The complete *Movie.vb* file is shown below.</span></span>

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="7f530-135">建立連接字串和使用 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="7f530-135">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="7f530-136">`MovieDBContext`您所建立的類別會處理連接到資料庫和對應的工作`Movie`資料庫記錄的物件。</span><span class="sxs-lookup"><span data-stu-id="7f530-136">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="7f530-137">您可能會問的一個問題，是如何指定要連線到哪一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f530-137">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="7f530-138">您將的做法是將連接資訊*Web.config*應用程式檔案。</span><span class="sxs-lookup"><span data-stu-id="7f530-138">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="7f530-139">開啟應用程式根目錄*Web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="7f530-139">Open the application root *Web.config* file.</span></span> <span data-ttu-id="7f530-140">(沒有*Web.config*中的檔案*檢視*資料夾。)下圖顯示兩者*Web.config*檔案; 開啟*Web.config*以紅色圈起的檔案。</span><span class="sxs-lookup"><span data-stu-id="7f530-140">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image2.png)

## 

<span data-ttu-id="7f530-141">加入下列連接字串`<connectionStrings>`中的項目*Web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="7f530-141">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="7f530-142">下列範例示範的一部分*Web.config*檔案以加入新的連接字串：</span><span class="sxs-lookup"><span data-stu-id="7f530-142">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="7f530-143">此少量的程式碼和 XML 是您要撰寫以代表，並將電影資料儲存在資料庫中的所有項目。</span><span class="sxs-lookup"><span data-stu-id="7f530-143">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="7f530-144">接下來，您將建立新`MoviesController`類別可用來顯示電影資料，並允許使用者建立新的電影清單。</span><span class="sxs-lookup"><span data-stu-id="7f530-144">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7f530-145">[上一頁](adding-a-view.md)
> [下一頁](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="7f530-145">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
