---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: 加入模型 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 453a55bd9f16c7b33525de18bc49493d22776f47
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045113"
---
# <a name="adding-a-model"></a><span data-ttu-id="6392a-102">新增模型</span><span class="sxs-lookup"><span data-stu-id="6392a-102">Adding a Model</span></span>

<span data-ttu-id="6392a-103">依 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6392a-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](~/includes/razor.md)]

<span data-ttu-id="6392a-104">在本節中，您將新增一些類別來管理資料庫中的電影。</span><span class="sxs-lookup"><span data-stu-id="6392a-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="6392a-105">這些類別將會是 &quot; &quot; ASP.NET MVC 應用程式的模型部分。</span><span class="sxs-lookup"><span data-stu-id="6392a-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="6392a-106">您將使用稱為 [Entity Framework](https://docs.microsoft.com/ef/) 的 .NET Framework 資料存取技術來定義和使用這些模型類別。</span><span class="sxs-lookup"><span data-stu-id="6392a-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="6392a-107">Entity Framework (通常稱為 EF) 支援稱為 *Code First*的開發範例。</span><span class="sxs-lookup"><span data-stu-id="6392a-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="6392a-108">Code First 可讓您撰寫簡單的類別來建立模型物件。</span><span class="sxs-lookup"><span data-stu-id="6392a-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="6392a-109"> (這些也稱為 POCO 類別，來自于單純 &quot; 的 CLR 物件。 &quot;) 您接著就可以從類別即時建立資料庫，以實現非常乾淨且快速的開發工作流程。</span><span class="sxs-lookup"><span data-stu-id="6392a-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="6392a-110">如果您需要先建立資料庫，您仍然可以遵循本教學課程來瞭解如何開發 MVC 和 EF 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6392a-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="6392a-111">接著，您可以遵循 Tom Fizmakens [ASP.NET](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) 樣板教學課程，其中涵蓋資料庫的第一種方法。</span><span class="sxs-lookup"><span data-stu-id="6392a-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="6392a-112">新增模型類別</span><span class="sxs-lookup"><span data-stu-id="6392a-112">Adding Model Classes</span></span>

<span data-ttu-id="6392a-113">在 **方案總管**中，以滑鼠右鍵按一下 [ *模型* ] 資料夾，選取 [ **新增**]，然後選取 [ **類別**]。</span><span class="sxs-lookup"><span data-stu-id="6392a-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="6392a-114">輸入 *類別* 名稱 &quot; 電影 &quot; 。</span><span class="sxs-lookup"><span data-stu-id="6392a-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="6392a-115">將下列五個屬性新增至 `Movie` 類別：</span><span class="sxs-lookup"><span data-stu-id="6392a-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="6392a-116">我們將使用 `Movie` 類別來代表資料庫中的電影。</span><span class="sxs-lookup"><span data-stu-id="6392a-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="6392a-117">物件的每個實例 `Movie` 都會對應至資料庫資料表中的資料列，而類別的每個屬性 `Movie` 都會對應到資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="6392a-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="6392a-118">注意：若要使用 system.string 和相關類別，您必須安裝 [Entity Framework NuGet 套件](https://www.nuget.org/packages/EntityFramework/)。</span><span class="sxs-lookup"><span data-stu-id="6392a-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="6392a-119">請遵循連結以取得進一步的指示。</span><span class="sxs-lookup"><span data-stu-id="6392a-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="6392a-120">在相同的檔案中，新增下列 `MovieDBContext` 類別：</span><span class="sxs-lookup"><span data-stu-id="6392a-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="6392a-121">`MovieDBContext`類別代表 Entity Framework movie 資料庫內容，它會處理在資料庫中提取、儲存和更新 `Movie` 類別實例的工作。</span><span class="sxs-lookup"><span data-stu-id="6392a-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="6392a-122">`MovieDBContext`衍生自 Entity Framework 所 `DbContext` 提供的基類。</span><span class="sxs-lookup"><span data-stu-id="6392a-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="6392a-123">您必須在檔案 `DbContext` `DbSet` 的最上方加入下列語句，才能夠參考和 `using` ：</span><span class="sxs-lookup"><span data-stu-id="6392a-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="6392a-124">若要這麼做，您可以手動加入 using 語句，也可以將滑鼠停留在紅色的波浪線上， `Show potential fixes` 然後按一下並按一下 `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="6392a-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="6392a-125">注意：已移除數個未使用的 `using` 語句。</span><span class="sxs-lookup"><span data-stu-id="6392a-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="6392a-126">Visual Studio 將會以灰色顯示未使用的相依性。</span><span class="sxs-lookup"><span data-stu-id="6392a-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="6392a-127">若要移除未使用的相依性，您可以將滑鼠停留在灰色相依性上，按一下 [ `Show potential fixes` **移除未使用的 using** ]</span><span class="sxs-lookup"><span data-stu-id="6392a-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="6392a-128">我們最後在 MVC) 中加入了 (M 的模型。</span><span class="sxs-lookup"><span data-stu-id="6392a-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="6392a-129">在下一節中，您將會使用資料庫連接字串。</span><span class="sxs-lookup"><span data-stu-id="6392a-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6392a-130">[上一個](adding-a-view.md) 
> [下一步](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="6392a-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>
