---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: 將 ASP.NET MVC 應用程式中的存放庫和工作單元模式 (9 的 10) 中執行 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5bcdf32f1aa48e0d4950f59ff7841413f6990812
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2021
ms.locfileid: "99984708"
---
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a><span data-ttu-id="65b1b-103">將 ASP.NET MVC 應用程式中的存放庫和工作單元模式 (9 （共10個）中執行) </span><span class="sxs-lookup"><span data-stu-id="65b1b-103">Implementing the Repository and Unit of Work Patterns in an ASP.NET MVC Application (9 of 10)</span></span>

<span data-ttu-id="65b1b-104">由 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="65b1b-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>


> <span data-ttu-id="65b1b-105">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="65b1b-105">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="65b1b-106">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="65b1b-106">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="65b1b-107">如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。</span><span class="sxs-lookup"><span data-stu-id="65b1b-107">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="65b1b-108">您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="65b1b-108">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="65b1b-109">針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。</span><span class="sxs-lookup"><span data-stu-id="65b1b-109">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="65b1b-110">在上一個教學課程中，您使用了繼承來減少 `Student` 和實體類別中的多餘程式碼 `Instructor` 。</span><span class="sxs-lookup"><span data-stu-id="65b1b-110">In the previous tutorial you used inheritance to reduce redundant code in the `Student` and `Instructor` entity classes.</span></span> <span data-ttu-id="65b1b-111">在本教學課程中，您會看到一些使用儲存機制和工作單位模式來進行 CRUD 作業的方式。</span><span class="sxs-lookup"><span data-stu-id="65b1b-111">In this tutorial you'll see some ways to use the repository and unit of work patterns for CRUD operations.</span></span> <span data-ttu-id="65b1b-112">如先前的教學課程所示，您將變更程式碼使用已建立的頁面，而不是建立新頁面的方式。</span><span class="sxs-lookup"><span data-stu-id="65b1b-112">As in the previous tutorial, in this one you'll change the way your code works with pages you already created rather than creating new pages.</span></span>

## <a name="the-repository-and-unit-of-work-patterns"></a><span data-ttu-id="65b1b-113">存放庫和工作單元模式</span><span class="sxs-lookup"><span data-stu-id="65b1b-113">The Repository and Unit of Work Patterns</span></span>

<span data-ttu-id="65b1b-114">存放庫和工作單元模式的目的是要在應用程式的資料存取層和商務邏輯層之間建立抽象層。</span><span class="sxs-lookup"><span data-stu-id="65b1b-114">The repository and unit of work patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="65b1b-115">實作這些模式可協助隔離您的應用程式與資料存放區中的變更，並可促進自動化單元測試或測試驅動開發 (TDD)。</span><span class="sxs-lookup"><span data-stu-id="65b1b-115">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span>

<span data-ttu-id="65b1b-116">在本教學課程中，您將會為每個實體類型執行存放庫類別。</span><span class="sxs-lookup"><span data-stu-id="65b1b-116">In this tutorial you'll implement a repository class for each entity type.</span></span> <span data-ttu-id="65b1b-117">針對 `Student` 實體類型，您將建立存放庫介面和儲存機制類別。</span><span class="sxs-lookup"><span data-stu-id="65b1b-117">For the `Student` entity type you'll create a repository interface and a repository class.</span></span> <span data-ttu-id="65b1b-118">當您在控制器中具現化存放庫時，您將會使用介面，讓控制器接受任何可執行存放庫介面之物件的參考。</span><span class="sxs-lookup"><span data-stu-id="65b1b-118">When you instantiate the repository in your controller, you'll use the interface so that the controller will accept a reference to any object that implements the repository interface.</span></span> <span data-ttu-id="65b1b-119">當控制器在 web 伺服器下執行時，它會收到可搭配 Entity Framework 使用的存放庫。</span><span class="sxs-lookup"><span data-stu-id="65b1b-119">When the controller runs under a web server, it receives a repository that works with the Entity Framework.</span></span> <span data-ttu-id="65b1b-120">當控制器在單元測試類別下執行時，它會接收使用儲存資料的儲存機制，您可以輕鬆地操作測試，例如記憶體中的集合。</span><span class="sxs-lookup"><span data-stu-id="65b1b-120">When the controller runs under a unit test class, it receives a repository that works with data stored in a way that you can easily manipulate for testing, such as an in-memory collection.</span></span>

<span data-ttu-id="65b1b-121">稍後在教學課程中，您將針對 `Course` 控制器中的和實體類型使用多個存放庫和工作單元類別 `Department` `Course` 。</span><span class="sxs-lookup"><span data-stu-id="65b1b-121">Later in the tutorial you'll use multiple repositories and a unit of work class for the `Course` and `Department` entity types in the `Course` controller.</span></span> <span data-ttu-id="65b1b-122">工作單位類別會建立由所有儲存機制所共用的單一資料庫內容類別，以協調多個存放庫的工作。</span><span class="sxs-lookup"><span data-stu-id="65b1b-122">The unit of work class coordinates the work of multiple repositories by creating a single database context class shared by all of them.</span></span> <span data-ttu-id="65b1b-123">如果您想要能夠執行自動化單元測試，您可以使用與存放庫相同的方式來建立和使用這些類別的介面 `Student` 。</span><span class="sxs-lookup"><span data-stu-id="65b1b-123">If you wanted to be able to perform automated unit testing, you'd create and use interfaces for these classes in the same way you did for the `Student` repository.</span></span> <span data-ttu-id="65b1b-124">不過，為了讓教學課程保持簡單，您將建立並使用這些類別，而不需要介面。</span><span class="sxs-lookup"><span data-stu-id="65b1b-124">However, to keep the tutorial simple, you'll create and use these classes without interfaces.</span></span>

<span data-ttu-id="65b1b-125">下圖顯示將控制器和內容類別之間的關聯性概念化的一種方法，相較于根本不使用儲存機制或工作單位模式。</span><span class="sxs-lookup"><span data-stu-id="65b1b-125">The following illustration shows one way to conceptualize the relationships between the controller and context classes compared to not using the repository or unit of work pattern at all.</span></span>

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

<span data-ttu-id="65b1b-127">您不會在此教學課程系列中建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="65b1b-127">You won't create unit tests in this tutorial series.</span></span> <span data-ttu-id="65b1b-128">如需使用使用存放庫模式的 MVC 應用程式進行 TDD 的簡介，請參閱逐步解說：搭配使用 [TDD 與 ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx)。</span><span class="sxs-lookup"><span data-stu-id="65b1b-128">For an introduction to TDD with an MVC application that uses the repository pattern, see [Walkthrough: Using TDD with ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx).</span></span> <span data-ttu-id="65b1b-129">如需有關存放庫模式的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="65b1b-129">For more information about the repository pattern, see the following resources:</span></span>

- <span data-ttu-id="65b1b-130">MSDN 上[的存放庫模式](https://msdn.microsoft.com/library/ff649690.aspx)。</span><span class="sxs-lookup"><span data-stu-id="65b1b-130">[The Repository Pattern](https://msdn.microsoft.com/library/ff649690.aspx) on MSDN.</span></span>
- <span data-ttu-id="65b1b-131">使用 Entity Framework team blog 上[Entity Framework 4.0 的儲存機制和工作單位模式](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx)。</span><span class="sxs-lookup"><span data-stu-id="65b1b-131">[Using Repository and Unit of Work patterns with Entity Framework 4.0](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) on the Entity Framework team blog.</span></span>
- <span data-ttu-id="65b1b-132">[Agile Entity Framework 4](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) Julie Lerman 的 blog 系列文章。</span><span class="sxs-lookup"><span data-stu-id="65b1b-132">[Agile Entity Framework 4 Repository](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) series of posts on Julie Lerman's blog.</span></span>
- <span data-ttu-id="65b1b-133">在 Dan Wahlin 的 blog 上，[以一目了然的 HTML5/JQuery 應用程式建立帳戶](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx)。</span><span class="sxs-lookup"><span data-stu-id="65b1b-133">[Building the Account at a Glance HTML5/jQuery Application](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) on Dan Wahlin's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="65b1b-134">有許多方式可以執行存放庫和工作單元模式。</span><span class="sxs-lookup"><span data-stu-id="65b1b-134">There are many ways to implement the repository and unit of work patterns.</span></span> <span data-ttu-id="65b1b-135">您可以使用具有或不含工作單位類別的儲存機制類別。</span><span class="sxs-lookup"><span data-stu-id="65b1b-135">You can use repository classes with or without a unit of work class.</span></span> <span data-ttu-id="65b1b-136">您可以為所有實體類型或每種類型各執行一個儲存機制。</span><span class="sxs-lookup"><span data-stu-id="65b1b-136">You can implement a single repository for all entity types, or one for each type.</span></span> <span data-ttu-id="65b1b-137">如果您針對每個類型執行一個，則可以使用不同的類別、泛型基類和衍生類別，或抽象基類和衍生類別。</span><span class="sxs-lookup"><span data-stu-id="65b1b-137">If you implement one for each type, you can use separate classes, a generic base class and derived classes, or an abstract base class and derived classes.</span></span> <span data-ttu-id="65b1b-138">您可以在存放庫中包含商務邏輯，或將它限制為數據存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="65b1b-138">You can include business logic in your repository or restrict it to data access logic.</span></span> <span data-ttu-id="65b1b-139">您也可以使用 [idbset 會](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) 介面（而不是實體集的 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 類型），在資料庫內容類別中建立抽象層。</span><span class="sxs-lookup"><span data-stu-id="65b1b-139">You can also build an abstraction layer into your database context class by using [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) interfaces there instead of [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) types for your entity sets.</span></span> <span data-ttu-id="65b1b-140">執行本教學課程中所示之抽象層的方法，是您可以考慮的選項之一，而不是所有案例和環境的建議。</span><span class="sxs-lookup"><span data-stu-id="65b1b-140">The approach to implementing an abstraction layer shown in this tutorial is one option for you to consider, not a recommendation for all scenarios and environments.</span></span>

## <a name="creating-the-student-repository-class"></a><span data-ttu-id="65b1b-141">建立 Student 存放庫類別</span><span class="sxs-lookup"><span data-stu-id="65b1b-141">Creating the Student Repository Class</span></span>

<span data-ttu-id="65b1b-142">在 *DAL* 資料夾中，建立名為 *IStudentRepository.cs* 的類別檔案，並以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="65b1b-142">In the *DAL* folder, create a class file named *IStudentRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="65b1b-143">此程式碼會宣告一組一般的 CRUD 方法，包括兩個讀取方法：一個會傳回所有實體，另一個則 `Student` 會 `Student` 依識別碼尋找單一實體。</span><span class="sxs-lookup"><span data-stu-id="65b1b-143">This code declares a typical set of CRUD methods, including two read methods — one that returns all `Student` entities, and one that finds a single `Student` entity by ID.</span></span>

<span data-ttu-id="65b1b-144">在 *DAL* 資料夾中，建立名為 *StudentRepository.cs* file 的類別檔案。</span><span class="sxs-lookup"><span data-stu-id="65b1b-144">In the *DAL* folder, create a class file named *StudentRepository.cs* file.</span></span> <span data-ttu-id="65b1b-145">以下列程式碼取代現有的程式碼，此程式碼會 `IStudentRepository` 執行介面：</span><span class="sxs-lookup"><span data-stu-id="65b1b-145">Replace the existing code with the following code, which implements the `IStudentRepository` interface:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="65b1b-146">資料庫內容定義于類別變數中，而此函式需要呼叫的物件傳入內容的實例：</span><span class="sxs-lookup"><span data-stu-id="65b1b-146">The database context is defined in a class variable, and the constructor expects the calling object to pass in an instance of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="65b1b-147">您可以在存放庫中具現化新的內容，但如果您在一個控制器中使用多個存放庫，則每個都有個別的內容。</span><span class="sxs-lookup"><span data-stu-id="65b1b-147">You could instantiate a new context in the repository, but then if you used multiple repositories in one controller, each would end up with a separate context.</span></span> <span data-ttu-id="65b1b-148">稍後您將在控制器中使用多個存放庫 `Course` ，您會看到工作單位類別如何確保所有存放庫都使用相同的內容。</span><span class="sxs-lookup"><span data-stu-id="65b1b-148">Later you'll use multiple repositories in the `Course` controller, and you'll see how a unit of work class can ensure that all repositories use the same context.</span></span>

<span data-ttu-id="65b1b-149">存放庫會執行 [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) ，並處置您稍早在控制器中看到的資料庫內容，而其 CRUD 方法會以您稍早所見的相同方式來呼叫資料庫內容。</span><span class="sxs-lookup"><span data-stu-id="65b1b-149">The repository implements [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) and disposes the database context as you saw earlier in the controller, and its CRUD methods make calls to the database context in the same way that you saw earlier.</span></span>

## <a name="change-the-student-controller-to-use-the-repository"></a><span data-ttu-id="65b1b-150">變更學生控制器以使用儲存機制</span><span class="sxs-lookup"><span data-stu-id="65b1b-150">Change the Student Controller to Use the Repository</span></span>

<span data-ttu-id="65b1b-151">在 *StudentController.cs* 中，以下列程式碼取代目前在類別中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="65b1b-151">In *StudentController.cs*, replace the code currently in the class with the following code.</span></span> <span data-ttu-id="65b1b-152">所做的變更已醒目提示。</span><span class="sxs-lookup"><span data-stu-id="65b1b-152">The changes are highlighted.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

<span data-ttu-id="65b1b-153">控制器現在會針對實 `IStudentRepository` 介面而非 coNtext 類別的物件，宣告類別變數：</span><span class="sxs-lookup"><span data-stu-id="65b1b-153">The controller now declares a class variable for an object that implements the `IStudentRepository` interface instead of the context class:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="65b1b-154">預設 (無參數) 的函式會建立新的內容實例，而選擇性的函式可讓呼叫端傳入內容實例。</span><span class="sxs-lookup"><span data-stu-id="65b1b-154">The default (parameterless) constructor creates a new context instance, and an optional constructor allows the caller to pass in a context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="65b1b-155"> (如果您使用的是相依性 *插入* 或 di，就不需要預設的函式，因為 DI 軟體可確保一律會提供正確的存放庫物件。 ) </span><span class="sxs-lookup"><span data-stu-id="65b1b-155">(If you were using *dependency injection*, or DI, you wouldn't need the default constructor because the DI software would ensure that the correct repository object would always be provided.)</span></span>

<span data-ttu-id="65b1b-156">在 CRUD 方法中，現在會呼叫存放庫而非內容：</span><span class="sxs-lookup"><span data-stu-id="65b1b-156">In the CRUD methods, the repository is now called instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="65b1b-157">`Dispose`方法現在會處置存放庫，而非內容：</span><span class="sxs-lookup"><span data-stu-id="65b1b-157">And the `Dispose` method now disposes the repository instead of the context:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="65b1b-158">執行網站並按一下 [ **學生** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="65b1b-158">Run the site and click the **Students** tab.</span></span>

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="65b1b-160">頁面的外觀和運作方式與您變更程式碼以使用儲存機制之前相同，其他的學生頁面也相同。</span><span class="sxs-lookup"><span data-stu-id="65b1b-160">The page looks and works the same as it did before you changed the code to use the repository, and the other Student pages also work the same.</span></span> <span data-ttu-id="65b1b-161">不過， `Index` 控制器的方法進行篩選和排序的方式有很大的差異。</span><span class="sxs-lookup"><span data-stu-id="65b1b-161">However, there's an important difference in the way the `Index` method of the controller does filtering and ordering.</span></span> <span data-ttu-id="65b1b-162">此方法的原始版本包含下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="65b1b-162">The original version of this method contained the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

<span data-ttu-id="65b1b-163">更新的 `Index` 方法包含下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="65b1b-163">The updated `Index` method contains the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

<span data-ttu-id="65b1b-164">只有反白顯示的程式碼已變更。</span><span class="sxs-lookup"><span data-stu-id="65b1b-164">Only the highlighted code has changed.</span></span>

<span data-ttu-id="65b1b-165">在原始版本的程式碼中， `students` 輸入為 `IQueryable` 物件。</span><span class="sxs-lookup"><span data-stu-id="65b1b-165">In the original version of the code, `students` is typed as an `IQueryable` object.</span></span> <span data-ttu-id="65b1b-166">查詢不會傳送至資料庫，直到使用像這樣的方法將它轉換成集合為止 `ToList` ，除非索引視圖存取 student 模型，否則不會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="65b1b-166">The query isn't sent to the database until it's converted into a collection using a method such as `ToList`, which doesn't occur until the Index view accesses the student model.</span></span> <span data-ttu-id="65b1b-167">`Where`上述原始程式碼中的方法會成為 `WHERE` SQL 查詢中傳送至資料庫的子句。</span><span class="sxs-lookup"><span data-stu-id="65b1b-167">The `Where` method in the original code above becomes a `WHERE` clause in the SQL query that is sent to the database.</span></span> <span data-ttu-id="65b1b-168">也就是說，資料庫只會傳回選取的實體。</span><span class="sxs-lookup"><span data-stu-id="65b1b-168">That in turn means that only the selected entities are returned by the database.</span></span> <span data-ttu-id="65b1b-169">不過，由於變更 `context.Students` 為 `studentRepository.GetStudents()` ， `students` 這個語句之後的變數就是 `IEnumerable` 包含資料庫中所有學生的集合。</span><span class="sxs-lookup"><span data-stu-id="65b1b-169">However, as a result of changing `context.Students` to `studentRepository.GetStudents()`, the `students` variable after this statement is an `IEnumerable` collection that includes all students in the database.</span></span> <span data-ttu-id="65b1b-170">套用方法的最終結果 `Where` 是相同的，但現在工作是在 web 伺服器的記憶體中完成，而不是由資料庫完成。</span><span class="sxs-lookup"><span data-stu-id="65b1b-170">The end result of applying the `Where` method is the same, but now the work is done in memory on the web server and not by the database.</span></span> <span data-ttu-id="65b1b-171">針對傳回大量資料的查詢，這可能沒有效率。</span><span class="sxs-lookup"><span data-stu-id="65b1b-171">For queries that return large volumes of data, this can be inefficient.</span></span>

> [!TIP]
> 
> <span data-ttu-id="65b1b-172">**IQueryable 與 IEnumerable 的比較**</span><span class="sxs-lookup"><span data-stu-id="65b1b-172">**IQueryable vs. IEnumerable**</span></span>
> 
> <span data-ttu-id="65b1b-173">如這裡所示，執行存放庫之後，即使您在 [ **搜尋** ] 方塊中輸入某個內容，傳送至 SQL Server 的查詢會傳回所有的學生資料列，因為它不包含您的搜尋條件：</span><span class="sxs-lookup"><span data-stu-id="65b1b-173">After you implement the repository as shown here, even if you enter something in the **Search** box the query sent to SQL Server returns all Student rows because it doesn't include your search criteria:</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> <span data-ttu-id="65b1b-174">此查詢會傳回所有的學生資料，因為存放庫執行查詢時，不會知道搜尋準則。</span><span class="sxs-lookup"><span data-stu-id="65b1b-174">This query returns all of the student data because the repository executed the query without knowing about the search criteria.</span></span> <span data-ttu-id="65b1b-175">在此情況下，排序、套用搜尋準則，以及選取資料子集以進行分頁 (僅顯示3個數據列的程式) 會在稍後於 `ToPagedList` 集合上呼叫方法時于記憶體中完成 `IEnumerable` 。</span><span class="sxs-lookup"><span data-stu-id="65b1b-175">The process of sorting, applying search criteria, and selecting a subset of the data for paging (showing only 3 rows in this case) is done in memory later when the `ToPagedList` method is called on the `IEnumerable` collection.</span></span>
> 
> <span data-ttu-id="65b1b-176">在您執行存放庫) 之前的舊版程式碼 (中，除非您在套用搜尋準則之後，才將查詢傳送至資料庫，而在 `ToPagedList` 物件上呼叫時 `IQueryable` 。</span><span class="sxs-lookup"><span data-stu-id="65b1b-176">In the previous version of the code (before you implemented the repository), the query is not sent to the database until after you apply the search criteria, when `ToPagedList` is called on the `IQueryable` object.</span></span>
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> <span data-ttu-id="65b1b-177">在物件上呼叫 ToPagedList 時 `IQueryable` ，傳送至 SQL Server 的查詢會指定搜尋字串，因此只會傳回符合搜尋條件的資料列，而且不需要在記憶體中進行任何篩選。</span><span class="sxs-lookup"><span data-stu-id="65b1b-177">When ToPagedList is called on an `IQueryable` object, the query sent to SQL Server specifies the search string, and as a result only rows that meet the search criteria are returned, and no filtering needs to be done in memory.</span></span>
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> <span data-ttu-id="65b1b-178"> (下列教學課程說明如何檢查傳送至 SQL Server 的查詢。 ) </span><span class="sxs-lookup"><span data-stu-id="65b1b-178">(The following tutorial explains how to examine queries sent to SQL Server.)</span></span>

<span data-ttu-id="65b1b-179">下一節將說明如何執行儲存機制方法，讓您指定此工作應該由資料庫完成。</span><span class="sxs-lookup"><span data-stu-id="65b1b-179">The following section shows how to implement repository methods that enable you to specify that this work should be done by the database.</span></span>

<span data-ttu-id="65b1b-180">您現在已在控制器與 Entity Framework 資料庫內容之間建立抽象層。</span><span class="sxs-lookup"><span data-stu-id="65b1b-180">You've now created an abstraction layer between the controller and the Entity Framework database context.</span></span> <span data-ttu-id="65b1b-181">如果您要使用此應用程式執行自動化單元測試，您可以在執行的單元測試專案中建立替代的儲存機制類別 `IStudentRepository` *。*</span><span class="sxs-lookup"><span data-stu-id="65b1b-181">If you were going to perform automated unit testing with this application, you could create an alternative repository class in a unit test project that implements `IStudentRepository`*.*</span></span> <span data-ttu-id="65b1b-182">這個 mock 存放庫類別可以操作記憶體中的集合，以測試控制器函式，而不是呼叫內容來讀取和寫入資料。</span><span class="sxs-lookup"><span data-stu-id="65b1b-182">Instead of calling the context to read and write data, this mock repository class could manipulate in-memory collections in order to test controller functions.</span></span>

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a><span data-ttu-id="65b1b-183">執行泛型存放庫和工作單位類別</span><span class="sxs-lookup"><span data-stu-id="65b1b-183">Implement a Generic Repository and a Unit of Work Class</span></span>

<span data-ttu-id="65b1b-184">為每個實體類型建立存放庫類別可能會導致大量多餘的程式碼，而且可能會導致部分更新。</span><span class="sxs-lookup"><span data-stu-id="65b1b-184">Creating a repository class for each entity type could result in a lot of redundant code, and it could result in partial updates.</span></span> <span data-ttu-id="65b1b-185">例如，假設您必須將兩個不同的實體類型更新為相同交易的一部分。</span><span class="sxs-lookup"><span data-stu-id="65b1b-185">For example, suppose you have to update two different entity types as part of the same transaction.</span></span> <span data-ttu-id="65b1b-186">如果每個都使用不同的資料庫內容實例，則可能會成功，而另一個實例可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="65b1b-186">If each uses a separate database context instance, one might succeed and the other might fail.</span></span> <span data-ttu-id="65b1b-187">將多餘的程式碼降至最低的其中一種方式是使用一般儲存機制，以及確保所有存放庫都使用相同的資料庫內容 (，進而協調所有更新) 是使用工作單位類別的方式。</span><span class="sxs-lookup"><span data-stu-id="65b1b-187">One way to minimize redundant code is to use a generic repository, and one way to ensure that all repositories use the same database context (and thus coordinate all updates) is to use a unit of work class.</span></span>

<span data-ttu-id="65b1b-188">在本教學課程的這一節中，您將建立 `GenericRepository` 類別和 `UnitOfWork` 類別，並在控制器中使用它們 `Course` 來存取 `Department` 和 `Course` 實體集。</span><span class="sxs-lookup"><span data-stu-id="65b1b-188">In this section of the tutorial, you'll create a `GenericRepository` class and a `UnitOfWork` class, and use them in the `Course` controller to access both the `Department` and the `Course` entity sets.</span></span> <span data-ttu-id="65b1b-189">如先前所述，若要讓教學課程的這個部分保持簡單，您不會建立這些類別的介面。</span><span class="sxs-lookup"><span data-stu-id="65b1b-189">As explained earlier, to keep this part of the tutorial simple, you aren't creating interfaces for these classes.</span></span> <span data-ttu-id="65b1b-190">但是，如果您要使用它們來協助 TDD，您通常會使用與存放庫相同的方式來執行這些介面 `Student` 。</span><span class="sxs-lookup"><span data-stu-id="65b1b-190">But if you were going to use them to facilitate TDD, you'd typically implement them with interfaces the same way you did the `Student` repository.</span></span>

### <a name="create-a-generic-repository"></a><span data-ttu-id="65b1b-191">建立一般儲存機制</span><span class="sxs-lookup"><span data-stu-id="65b1b-191">Create a Generic Repository</span></span>

<span data-ttu-id="65b1b-192">在 *DAL* 資料夾中，建立 *GenericRepository.cs* ，並以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="65b1b-192">In the *DAL* folder, create *GenericRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="65b1b-193">系統會為資料庫內容和儲存機制具現化的實體集宣告類別變數：</span><span class="sxs-lookup"><span data-stu-id="65b1b-193">Class variables are declared for the database context and for the entity set that the repository is instantiated for:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="65b1b-194">此函數會接受資料庫內容實例，並初始化實體集變數：</span><span class="sxs-lookup"><span data-stu-id="65b1b-194">The constructor accepts a database context instance and initializes the entity set variable:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="65b1b-195">`Get`方法會使用 lambda 運算式來允許呼叫程式碼指定篩選準則和資料行來排序結果，而字串參數則可讓呼叫端提供以逗號分隔的導覽屬性清單，以便進行積極式載入：</span><span class="sxs-lookup"><span data-stu-id="65b1b-195">The `Get` method uses lambda expressions to allow the calling code to specify a filter condition and a column to order the results by, and a string parameter lets the caller provide a comma-delimited list of navigation properties for eager loading:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="65b1b-196">此程式碼 `Expression<Func<TEntity, bool>> filter` 表示呼叫端會根據類型提供 lambda 運算式 `TEntity` ，而此運算式會傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="65b1b-196">The code `Expression<Func<TEntity, bool>> filter` means the caller will provide a lambda expression based on the `TEntity` type, and this expression will return a Boolean value.</span></span> <span data-ttu-id="65b1b-197">例如，如果為實體型別具現化存放庫 `Student` ，則呼叫方法中的程式碼可能會 `student => student.LastName == "Smith` &quot; 為 `filter` 參數指定。</span><span class="sxs-lookup"><span data-stu-id="65b1b-197">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `student => student.LastName == "Smith`&quot; for the `filter` parameter.</span></span>

<span data-ttu-id="65b1b-198">此程式碼 `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` 也表示呼叫端會提供 lambda 運算式。</span><span class="sxs-lookup"><span data-stu-id="65b1b-198">The code `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` also means the caller will provide a lambda expression.</span></span> <span data-ttu-id="65b1b-199">但是在此情況下，運算式的輸入是型別的 `IQueryable` 物件 `TEntity` 。</span><span class="sxs-lookup"><span data-stu-id="65b1b-199">But in this case, the input to the expression is an `IQueryable` object for the `TEntity` type.</span></span> <span data-ttu-id="65b1b-200">運算式會傳回該物件的排序版本 `IQueryable` 。</span><span class="sxs-lookup"><span data-stu-id="65b1b-200">The expression will return an ordered version of that `IQueryable` object.</span></span> <span data-ttu-id="65b1b-201">例如，如果為實體型別具現化存放庫 `Student` ，則呼叫方法中的程式碼可能會 `q => q.OrderBy(s => s.LastName)` 為 `orderBy` 參數指定。</span><span class="sxs-lookup"><span data-stu-id="65b1b-201">For example, if the repository is instantiated for the `Student` entity type, the code in the calling method might specify `q => q.OrderBy(s => s.LastName)` for the `orderBy` parameter.</span></span>

<span data-ttu-id="65b1b-202">方法中的 `Get` 程式碼會建立 `IQueryable` 物件，然後套用篩選運算式（如果有的話）：</span><span class="sxs-lookup"><span data-stu-id="65b1b-202">The code in the `Get` method creates an `IQueryable` object and then applies the filter expression if there is one:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="65b1b-203">接著，它會在剖析以逗號分隔的清單之後，套用立即載入的運算式：</span><span class="sxs-lookup"><span data-stu-id="65b1b-203">Next it applies the eager-loading expressions after parsing the comma-delimited list:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

<span data-ttu-id="65b1b-204">最後，它會套用 `orderBy` 運算式（如果有的話），並傳回結果，否則會傳回未排序查詢的結果：</span><span class="sxs-lookup"><span data-stu-id="65b1b-204">Finally, it applies the `orderBy` expression if there is one and returns the results; otherwise it returns the results from the unordered query:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="65b1b-205">當您呼叫 `Get` 方法時，您可以針對方法所傳回的集合進行篩選和排序， `IEnumerable` 而不是為這些函數提供參數。</span><span class="sxs-lookup"><span data-stu-id="65b1b-205">When you call the `Get` method, you could do filtering and sorting on the `IEnumerable` collection returned by the method instead of providing parameters for these functions.</span></span> <span data-ttu-id="65b1b-206">但是排序和篩選工作接著會在 web 伺服器的記憶體中完成。</span><span class="sxs-lookup"><span data-stu-id="65b1b-206">But the sorting and filtering work would then be done in memory on the web server.</span></span> <span data-ttu-id="65b1b-207">藉由使用這些參數，您可以確保工作是由資料庫而不是 web 伺服器來完成。</span><span class="sxs-lookup"><span data-stu-id="65b1b-207">By using these parameters, you ensure that the work is done by the database rather than the web server.</span></span> <span data-ttu-id="65b1b-208">替代方式是建立特定實體類型的衍生類別，並新增特殊 `Get` 方法，例如 `GetStudentsInNameOrder` 或 `GetStudentsByName` 。</span><span class="sxs-lookup"><span data-stu-id="65b1b-208">An alternative is to create derived classes for specific entity types and add specialized `Get` methods, such as `GetStudentsInNameOrder` or `GetStudentsByName`.</span></span> <span data-ttu-id="65b1b-209">不過，在複雜的應用程式中，這可能會導致大量的這類衍生類別和特殊方法，這可能更適合維護。</span><span class="sxs-lookup"><span data-stu-id="65b1b-209">However, in a complex application, this can result in a large number of such derived classes and specialized methods, which could be more work to maintain.</span></span>

<span data-ttu-id="65b1b-210">`GetByID`、和方法中的 `Insert` 程式碼與 `Update` 您在非泛型存放庫中看到的程式碼類似。</span><span class="sxs-lookup"><span data-stu-id="65b1b-210">The code in the `GetByID`, `Insert`, and `Update` methods is similar to what you saw in the non-generic repository.</span></span> <span data-ttu-id="65b1b-211"> (您未在簽章中提供積極的載入參數 `GetByID` ，因為您無法使用方法來進行積極式載入 `Find` 。 ) </span><span class="sxs-lookup"><span data-stu-id="65b1b-211">(You aren't providing an eager loading parameter in the `GetByID` signature, because you can't do eager loading with the `Find` method.)</span></span>

<span data-ttu-id="65b1b-212">針對方法提供兩個多載 `Delete` ：</span><span class="sxs-lookup"><span data-stu-id="65b1b-212">Two overloads are provided for the `Delete` method:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

<span data-ttu-id="65b1b-213">其中一項可讓您只傳入要刪除之實體的識別碼，而其中一個會接受實體實例。</span><span class="sxs-lookup"><span data-stu-id="65b1b-213">One of these lets you pass in just the ID of the entity to be deleted, and one takes an entity instance.</span></span> <span data-ttu-id="65b1b-214">如您在 [處理並行](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 存取教學課程中所見，針對並行處理，您需要一個 `Delete` 方法，該方法會採用包含追蹤屬性之原始值的實體實例。</span><span class="sxs-lookup"><span data-stu-id="65b1b-214">As you saw in the [Handling Concurrency](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial, for concurrency handling you need a `Delete` method that takes an entity instance that includes the original value of a tracking property.</span></span>

<span data-ttu-id="65b1b-215">此一般存放庫將處理一般的 CRUD 需求。</span><span class="sxs-lookup"><span data-stu-id="65b1b-215">This generic repository will handle typical CRUD requirements.</span></span> <span data-ttu-id="65b1b-216">當特定實體類型具有特殊需求（例如更複雜的篩選或排序）時，您可以建立具有該型別之其他方法的衍生類別。</span><span class="sxs-lookup"><span data-stu-id="65b1b-216">When a particular entity type has special requirements, such as more complex filtering or ordering, you can create a derived class that has additional methods for that type.</span></span>

## <a name="creating-the-unit-of-work-class"></a><span data-ttu-id="65b1b-217">建立工作單位類別</span><span class="sxs-lookup"><span data-stu-id="65b1b-217">Creating the Unit of Work Class</span></span>

<span data-ttu-id="65b1b-218">工作單位類別有一個用途：為了確保當您使用多個存放庫時，它們會共用單一資料庫內容。</span><span class="sxs-lookup"><span data-stu-id="65b1b-218">The unit of work class serves one purpose: to make sure that when you use multiple repositories, they share a single database context.</span></span> <span data-ttu-id="65b1b-219">如此一來，當工作單位完成時，您就可以 `SaveChanges` 在該內容實例上呼叫方法，並確保所有相關的變更都將會協調。</span><span class="sxs-lookup"><span data-stu-id="65b1b-219">That way, when a unit of work is complete you can call the `SaveChanges` method on that instance of the context and be assured that all related changes will be coordinated.</span></span> <span data-ttu-id="65b1b-220">類別需要的所有方法都是 `Save` 方法和每個存放庫的屬性。</span><span class="sxs-lookup"><span data-stu-id="65b1b-220">All that the class needs is a `Save` method and a property for each repository.</span></span> <span data-ttu-id="65b1b-221">每個存放庫屬性都會傳回已使用與其他存放庫實例相同的資料庫內容實例來具現化的儲存機制實例。</span><span class="sxs-lookup"><span data-stu-id="65b1b-221">Each repository property returns a repository instance that has been instantiated using the same database context instance as the other repository instances.</span></span>

<span data-ttu-id="65b1b-222">在 *DAL* 資料夾中，建立名為 *UnitOfWork.cs* 的類別檔案，並以下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="65b1b-222">In the *DAL* folder, create a class file named *UnitOfWork.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="65b1b-223">程式碼會為資料庫內容和每個存放庫建立類別變數。</span><span class="sxs-lookup"><span data-stu-id="65b1b-223">The code creates class variables for the database context and each repository.</span></span> <span data-ttu-id="65b1b-224">若為 `context` 變數，則會具現化新的內容：</span><span class="sxs-lookup"><span data-stu-id="65b1b-224">For the `context` variable, a new context is instantiated:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="65b1b-225">每個存放庫屬性都會檢查存放庫是否已存在。</span><span class="sxs-lookup"><span data-stu-id="65b1b-225">Each repository property checks whether the repository already exists.</span></span> <span data-ttu-id="65b1b-226">如果沒有，則會具現化存放庫，並在內容實例中傳遞。</span><span class="sxs-lookup"><span data-stu-id="65b1b-226">If not, it instantiates the repository, passing in the context instance.</span></span> <span data-ttu-id="65b1b-227">因此，所有存放庫都會共用相同的內容實例。</span><span class="sxs-lookup"><span data-stu-id="65b1b-227">As a result, all repositories share the same context instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="65b1b-228">`Save`方法會 `SaveChanges` 在資料庫內容上呼叫。</span><span class="sxs-lookup"><span data-stu-id="65b1b-228">The `Save` method calls `SaveChanges` on the database context.</span></span>

<span data-ttu-id="65b1b-229">就像任何在類別變數中具現化資料庫內容的類別一樣，該類別會實 `UnitOfWork` `IDisposable` 和處置內容。</span><span class="sxs-lookup"><span data-stu-id="65b1b-229">Like any class that instantiates a database context in a class variable, the `UnitOfWork` class implements `IDisposable` and disposes the context.</span></span>

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a><span data-ttu-id="65b1b-230">變更課程式控制制器以使用 UnitOfWork 類別和儲存機制</span><span class="sxs-lookup"><span data-stu-id="65b1b-230">Changing the Course Controller to use the UnitOfWork Class and Repositories</span></span>

<span data-ttu-id="65b1b-231">以下列程式碼取代您目前在 *CourseController.cs* 中所擁有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="65b1b-231">Replace the code you currently have in *CourseController.cs* with the following code:</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

<span data-ttu-id="65b1b-232">這段程式碼會加入類別的類別變數 `UnitOfWork` 。</span><span class="sxs-lookup"><span data-stu-id="65b1b-232">This code adds a class variable for the `UnitOfWork` class.</span></span> <span data-ttu-id="65b1b-233"> (如果您在這裡使用介面，則不會在此初始化變數;相反地，您會執行兩個函式的模式，就像您對存放庫所做的一樣 `Student` 。 ) </span><span class="sxs-lookup"><span data-stu-id="65b1b-233">(If you were using interfaces here, you wouldn't initialize the variable here; instead, you'd implement a pattern of two constructors just as you did for the `Student` repository.)</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

<span data-ttu-id="65b1b-234">在類別的其餘部分，對適當存放庫的參考會取代資料庫內容的所有參考，並使用 `UnitOfWork` 屬性來存取存放庫。</span><span class="sxs-lookup"><span data-stu-id="65b1b-234">In the rest of the class, all references to the database context are replaced by references to the appropriate repository, using `UnitOfWork` properties to access the repository.</span></span> <span data-ttu-id="65b1b-235">`Dispose`方法會處置 `UnitOfWork` 實例。</span><span class="sxs-lookup"><span data-stu-id="65b1b-235">The `Dispose` method disposes the `UnitOfWork` instance.</span></span>

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

<span data-ttu-id="65b1b-236">執行網站並按一下 [ **課程** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="65b1b-236">Run the site and click the **Courses** tab.</span></span>

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="65b1b-238">頁面的外觀和運作方式與您的變更之前相同，其他課程頁面也相同。</span><span class="sxs-lookup"><span data-stu-id="65b1b-238">The page looks and works the same as it did before your changes, and the other Course pages also work the same.</span></span>

## <a name="summary"></a><span data-ttu-id="65b1b-239">摘要</span><span class="sxs-lookup"><span data-stu-id="65b1b-239">Summary</span></span>

<span data-ttu-id="65b1b-240">您現在已實作為存放庫和工作單元模式。</span><span class="sxs-lookup"><span data-stu-id="65b1b-240">You have now implemented both the repository and unit of work patterns.</span></span> <span data-ttu-id="65b1b-241">您已使用 lambda 運算式作為一般存放庫中的方法參數。</span><span class="sxs-lookup"><span data-stu-id="65b1b-241">You have used lambda expressions as method parameters in the generic repository.</span></span> <span data-ttu-id="65b1b-242">如需有關如何搭配物件使用這些運算式的詳細資訊 `IQueryable` ，請參閱 MSDN Library 中的 [IQueryable (T) 介面 (System. Linq) ](https://msdn.microsoft.com/library/bb351562.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="65b1b-242">For more information about how to use these expressions with an `IQueryable` object, see [IQueryable(T) Interface (System.Linq)](https://msdn.microsoft.com/library/bb351562.aspx) in the MSDN Library.</span></span> <span data-ttu-id="65b1b-243">在下一個教學課程中，您將瞭解如何處理一些 advanced 案例。</span><span class="sxs-lookup"><span data-stu-id="65b1b-243">In the next tutorial you'll learn how to handle some advanced scenarios.</span></span>

<span data-ttu-id="65b1b-244">您可以在 [ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="65b1b-244">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="65b1b-245">[上一個](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) 
> [下一步](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="65b1b-245">[Previous](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)</span></span>
