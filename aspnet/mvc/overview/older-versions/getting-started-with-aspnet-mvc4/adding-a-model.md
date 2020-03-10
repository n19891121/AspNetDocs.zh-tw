---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: 加入模型 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540303"
---
# <a name="adding-a-model"></a><span data-ttu-id="459eb-104">新增模型</span><span class="sxs-lookup"><span data-stu-id="459eb-104">Adding a Model</span></span>

<span data-ttu-id="459eb-105">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="459eb-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="459eb-106">本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="459eb-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="459eb-107">它更安全、更容易遵循，並示範更多功能。</span><span class="sxs-lookup"><span data-stu-id="459eb-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="459eb-108">在本節中，您將新增一些類別來管理資料庫中的電影。</span><span class="sxs-lookup"><span data-stu-id="459eb-108">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="459eb-109">這些類別會是 ASP.NET MVC 應用程式&quot; 部分的 &quot;模型。</span><span class="sxs-lookup"><span data-stu-id="459eb-109">These classes will be the &quot;model&quot; part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="459eb-110">您將使用稱為[Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx)的 .NET Framework 資料存取技術，來定義和使用這些模型類別。</span><span class="sxs-lookup"><span data-stu-id="459eb-110">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) to define and work with these model classes.</span></span> <span data-ttu-id="459eb-111">Entity Framework （通常稱為 EF）支援稱為*Code First*的開發範例。</span><span class="sxs-lookup"><span data-stu-id="459eb-111">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="459eb-112">Code First 可讓您藉由撰寫簡單的類別來建立模型物件。</span><span class="sxs-lookup"><span data-stu-id="459eb-112">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="459eb-113">（這些也稱為 POCO 類別，從 &quot;純舊 CLR 物件。&quot;）接著，您可以從類別中即時建立資料庫，以實現非常乾淨快速的開發工作流程。</span><span class="sxs-lookup"><span data-stu-id="459eb-113">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="459eb-114">新增模型類別</span><span class="sxs-lookup"><span data-stu-id="459eb-114">Adding Model Classes</span></span>

<span data-ttu-id="459eb-115">在**方案總管**中，以滑鼠右鍵按一下 [*模型*] 資料夾，選取 [**新增**]，然後選取 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="459eb-115">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="459eb-116">輸入 &quot;電影&quot;的*類別*名稱。</span><span class="sxs-lookup"><span data-stu-id="459eb-116">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="459eb-117">將下列五個屬性新增至 `Movie` 類別：</span><span class="sxs-lookup"><span data-stu-id="459eb-117">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="459eb-118">我們會使用 `Movie` 類別來代表資料庫中的電影。</span><span class="sxs-lookup"><span data-stu-id="459eb-118">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="459eb-119">`Movie` 物件的每個實例都會對應至資料庫資料表中的資料列，而 `Movie` 類別的每個屬性都會對應到資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="459eb-119">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="459eb-120">在相同的檔案中，新增下列 `MovieDBContext` 類別：</span><span class="sxs-lookup"><span data-stu-id="459eb-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="459eb-121">`MovieDBContext` 類別代表 Entity Framework 的電影資料庫內容，它會處理資料庫中的 `Movie` 類別實例的提取、儲存和更新。</span><span class="sxs-lookup"><span data-stu-id="459eb-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="459eb-122">`MovieDBContext` 衍生自 Entity Framework 所提供的 `DbContext` 基類。</span><span class="sxs-lookup"><span data-stu-id="459eb-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="459eb-123">為了能夠參考 `DbContext` 和 `DbSet`，您必須在檔案頂端新增下列 `using` 語句：</span><span class="sxs-lookup"><span data-stu-id="459eb-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="459eb-124">完整的*Movie.cs*檔案如下所示。</span><span class="sxs-lookup"><span data-stu-id="459eb-124">The complete *Movie.cs* file is shown below.</span></span> <span data-ttu-id="459eb-125">（已移除數個不需要的 using 語句）。</span><span class="sxs-lookup"><span data-stu-id="459eb-125">(Several using statements that are not needed have been removed.)</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="459eb-126">建立連接字串以及使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="459eb-126">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="459eb-127">您所建立的 `MovieDBContext` 類別會處理連接到資料庫的工作，並將 `Movie` 物件對應至資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="459eb-127">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="459eb-128">不過，您可能會問的一個問題，就是如何指定要連接的資料庫。</span><span class="sxs-lookup"><span data-stu-id="459eb-128">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="459eb-129">您*會在應用程式的 web.config*檔案中加入連接資訊來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="459eb-129">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="459eb-130">開啟應用*程式根目錄的 web.config 檔案*。</span><span class="sxs-lookup"><span data-stu-id="459eb-130">Open the application root *Web.config* file.</span></span> <span data-ttu-id="459eb-131">（不是*Views*資料夾中*的 web.config 檔案*）。開啟以紅色*概述的 web.config 檔案。*</span><span class="sxs-lookup"><span data-stu-id="459eb-131">(Not the *Web.config* file in the *Views* folder.) Open the *Web.config* file outlined in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="459eb-132">將下列連接字串新增*至 web.config 檔案*中的 `<connectionStrings>` 元素。</span><span class="sxs-lookup"><span data-stu-id="459eb-132">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="459eb-133">下列範例會顯示已新增連接字串的*web.config*檔案的一部分：</span><span class="sxs-lookup"><span data-stu-id="459eb-133">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

<span data-ttu-id="459eb-134">這小段的程式碼和 XML 就是您需要撰寫的所有專案，以便在資料庫中呈現及儲存電影資料。</span><span class="sxs-lookup"><span data-stu-id="459eb-134">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="459eb-135">接下來，您將建立新的 `MoviesController` 類別，您可以用它來顯示電影資料，並允許使用者建立新的電影清單。</span><span class="sxs-lookup"><span data-stu-id="459eb-135">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="459eb-136">[上一頁](adding-a-view.md)
> [下一頁](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="459eb-136">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
