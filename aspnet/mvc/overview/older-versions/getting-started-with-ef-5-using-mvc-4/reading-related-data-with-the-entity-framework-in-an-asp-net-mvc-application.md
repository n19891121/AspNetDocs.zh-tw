---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 應用程式中使用 Entity Framework 讀取相關資料 (5/10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 6a3a4978a718ba56446463373ad3525e8b6f0d4a
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2021
ms.locfileid: "99984883"
---
# <a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a><span data-ttu-id="dae0e-103">在 ASP.NET MVC 應用程式中使用 Entity Framework 讀取相關資料 (5/10) </span><span class="sxs-lookup"><span data-stu-id="dae0e-103">Reading Related Data with the Entity Framework in an ASP.NET MVC Application (5 of 10)</span></span>

<span data-ttu-id="dae0e-104">由 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="dae0e-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="dae0e-105">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dae0e-105">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="dae0e-106">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="dae0e-106">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="dae0e-107">如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。</span><span class="sxs-lookup"><span data-stu-id="dae0e-107">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="dae0e-108">您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="dae0e-108">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="dae0e-109">針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。</span><span class="sxs-lookup"><span data-stu-id="dae0e-109">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="dae0e-110">在上一個教學課程中，您已完成 School 資料模型。</span><span class="sxs-lookup"><span data-stu-id="dae0e-110">In the previous tutorial you completed the School data model.</span></span> <span data-ttu-id="dae0e-111">在本教學課程中，您將讀取並顯示相關資料，也就是 Entity Framework 載入導覽屬性中的資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-111">In this tutorial you'll read and display related data — that is, data that the Entity Framework loads into navigation properties.</span></span>

<span data-ttu-id="dae0e-112">下列圖例顯示了您將操作的頁面。</span><span class="sxs-lookup"><span data-stu-id="dae0e-112">The following illustrations show the pages that you'll work with.</span></span>

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a><span data-ttu-id="dae0e-114">相關資料的延遲、積極且明確的載入</span><span class="sxs-lookup"><span data-stu-id="dae0e-114">Lazy, Eager, and Explicit Loading of Related Data</span></span>

<span data-ttu-id="dae0e-115">Entity Framework 可以透過數種方式將相關資料載入到實體的導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="dae0e-115">There are several ways that the Entity Framework can load related data into the navigation properties of an entity:</span></span>

- <span data-ttu-id="dae0e-116">*延遲載入*。</span><span class="sxs-lookup"><span data-stu-id="dae0e-116">*Lazy loading*.</span></span> <span data-ttu-id="dae0e-117">第一次讀取實體時，不會擷取相關資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-117">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="dae0e-118">不過，第一次嘗試存取導覽屬性時，將會自動擷取該導覽屬性所需的資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-118">However, the first time you attempt to access a navigation property, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="dae0e-119">這會導致多個查詢傳送至資料庫，一個用於實體本身，每次都必須抓取實體的相關資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-119">This results in multiple queries sent to the database — one for the entity itself and one each time that related data for the entity must be retrieved.</span></span> 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- <span data-ttu-id="dae0e-121">*積極式載入*。</span><span class="sxs-lookup"><span data-stu-id="dae0e-121">*Eager loading*.</span></span> <span data-ttu-id="dae0e-122">讀取實體時，將會同時擷取其相關資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-122">When the entity is read, related data is retrieved along with it.</span></span> <span data-ttu-id="dae0e-123">這通常會導致單一聯結查詢，其可擷取所有需要的資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-123">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="dae0e-124">您可以使用方法指定積極式載入 `Include` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-124">You specify eager loading by using the `Include` method.</span></span>

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- <span data-ttu-id="dae0e-126">*明確載入*。</span><span class="sxs-lookup"><span data-stu-id="dae0e-126">*Explicit loading*.</span></span> <span data-ttu-id="dae0e-127">這類似于消極式載入，不同之處在于您明確地在程式碼中取出相關的資料。當您存取導覽屬性時，不會自動進行。</span><span class="sxs-lookup"><span data-stu-id="dae0e-127">This is similar to lazy loading, except that you explicitly retrieve the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="dae0e-128">您可以藉由取得實體的物件狀態管理員專案，並呼叫 `Collection.Load` 集合的方法或 `Reference.Load` 保留單一實體的屬性方法，以手動方式載入相關資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-128">You load related data manually by getting the object state manager entry for an entity and calling the `Collection.Load` method for collections or the `Reference.Load` method for properties that hold a single entity.</span></span> <span data-ttu-id="dae0e-129"> (在下列範例中，如果您想要載入系統管理員導覽屬性，您必須將取代 `Collection(x => x.Courses)` 為 `Reference(x => x.Administrator)` 。 ) </span><span class="sxs-lookup"><span data-stu-id="dae0e-129">(In the following example, if you wanted to load the Administrator navigation property, you'd replace `Collection(x => x.Courses)` with `Reference(x => x.Administrator)`.)</span></span>

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

<span data-ttu-id="dae0e-131">因為它們不會立即取得屬性值，所以消極式載入和明確載入也稱為 *延後載入*。</span><span class="sxs-lookup"><span data-stu-id="dae0e-131">Because they don't immediately retrieve the property values, lazy loading and explicit loading are also both known as *deferred loading*.</span></span>

<span data-ttu-id="dae0e-132">一般情況下，如果您知道每個抓取實體都需要相關資料，積極式載入會提供最佳效能，因為傳送到資料庫的單一查詢通常比抓取每個實體的個別查詢更有效率。</span><span class="sxs-lookup"><span data-stu-id="dae0e-132">In general, if you know you need related data for every entity retrieved, eager loading offers the best performance, because a single query sent to the database is typically more efficient than separate queries for each entity retrieved.</span></span> <span data-ttu-id="dae0e-133">例如，在上述範例中，假設每個部門都有十個相關的課程。</span><span class="sxs-lookup"><span data-stu-id="dae0e-133">For example, in the above examples, suppose that each department has ten related courses.</span></span> <span data-ttu-id="dae0e-134">積極式載入範例只會產生單一 (聯結) 查詢，以及對資料庫進行單次往返。</span><span class="sxs-lookup"><span data-stu-id="dae0e-134">The eager loading example would result in just a single (join) query and a single round trip to the database.</span></span> <span data-ttu-id="dae0e-135">消極式載入和明確的載入範例都會產生11個查詢和資料庫的十次往返。</span><span class="sxs-lookup"><span data-stu-id="dae0e-135">The lazy loading and explicit loading examples would both result in eleven queries and eleven round trips to the database.</span></span> <span data-ttu-id="dae0e-136">當延遲很高時，資料庫的額外來回行程對效能特別不利。</span><span class="sxs-lookup"><span data-stu-id="dae0e-136">The extra round trips to the database are especially detrimental to performance when latency is high.</span></span>

<span data-ttu-id="dae0e-137">相反地，在某些情況下，消極式載入較有效率。</span><span class="sxs-lookup"><span data-stu-id="dae0e-137">On the other hand, in some scenarios lazy loading is more efficient.</span></span> <span data-ttu-id="dae0e-138">積極式載入可能會產生非常複雜的聯結，SQL Server 無法有效率地處理。</span><span class="sxs-lookup"><span data-stu-id="dae0e-138">Eager loading might cause a very complex join to be generated, which SQL Server can't process efficiently.</span></span> <span data-ttu-id="dae0e-139">或者，如果您只需要針對您正在處理的一組實體子集存取實體的導覽屬性，則消極式載入可能會更好，因為積極式載入會抓取超過您需要的資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-139">Or if you need to access an entity's navigation properties only for a subset of a set of entities you're processing, lazy loading might perform better because eager loading would retrieve more data than you need.</span></span> <span data-ttu-id="dae0e-140">如果效能嚴重不足，最好先測試這兩種方式的效能，才能做出最好的選擇。</span><span class="sxs-lookup"><span data-stu-id="dae0e-140">If performance is critical, it's best to test performance both ways in order to make the best choice.</span></span>

<span data-ttu-id="dae0e-141">一般來說，只有當您關閉消極式載入時，才會使用明確的載入。</span><span class="sxs-lookup"><span data-stu-id="dae0e-141">Typically you'd use explicit loading only when you've turned lazy loading off.</span></span> <span data-ttu-id="dae0e-142">當您在序列化期間關閉消極式載入時，會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="dae0e-142">One scenario when you should turn lazy loading off is during serialization.</span></span> <span data-ttu-id="dae0e-143">消極式載入和序列化不會有很大的混淆，如果您不小心，在啟用消極式載入時，查詢的資料會比您預期的還要多。</span><span class="sxs-lookup"><span data-stu-id="dae0e-143">Lazy loading and serialization don't mix well, and if you aren't careful you can end up querying significantly more data than you intended when lazy loading is enabled.</span></span> <span data-ttu-id="dae0e-144">序列化的運作方式通常是存取型別實例上的每個屬性。</span><span class="sxs-lookup"><span data-stu-id="dae0e-144">Serialization generally works by accessing each property on an instance of a type.</span></span> <span data-ttu-id="dae0e-145">屬性存取會觸發消極式載入，並序列化這些延遲載入的實體。</span><span class="sxs-lookup"><span data-stu-id="dae0e-145">Property access triggers lazy loading, and those lazy loaded entities are serialized.</span></span> <span data-ttu-id="dae0e-146">然後，序列化程式會存取延遲載入之實體的每個屬性，這可能會導致更多延遲載入和序列化。</span><span class="sxs-lookup"><span data-stu-id="dae0e-146">The serialization process then accesses each property of the lazy-loaded entities, potentially causing even more lazy loading and serialization.</span></span> <span data-ttu-id="dae0e-147">若要避免這種回合鏈的反應，請在序列化實體之前關閉消極式載入。</span><span class="sxs-lookup"><span data-stu-id="dae0e-147">To prevent this run-away chain reaction, turn lazy loading off before you serialize an entity.</span></span>

<span data-ttu-id="dae0e-148">根據預設，資料庫內容類別會執行消極式載入。</span><span class="sxs-lookup"><span data-stu-id="dae0e-148">The database context class performs lazy loading by default.</span></span> <span data-ttu-id="dae0e-149">有兩種方式可以停用延遲載入：</span><span class="sxs-lookup"><span data-stu-id="dae0e-149">There are two ways to disable lazy loading:</span></span>

- <span data-ttu-id="dae0e-150">若為特定導覽屬性，請在宣告 `virtual` 屬性時省略關鍵字。</span><span class="sxs-lookup"><span data-stu-id="dae0e-150">For specific navigation properties, omit the `virtual` keyword when you declare the property.</span></span>
- <span data-ttu-id="dae0e-151">若為所有導覽屬性，請將設定 `LazyLoadingEnabled` 為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-151">For all navigation properties, set `LazyLoadingEnabled` to `false`.</span></span> <span data-ttu-id="dae0e-152">例如，您可以將下列程式碼放在內容類別的函式中：</span><span class="sxs-lookup"><span data-stu-id="dae0e-152">For example, you can put the following code in the constructor of your context class:</span></span> 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="dae0e-153">消極式載入可以遮罩造成效能問題的程式碼。</span><span class="sxs-lookup"><span data-stu-id="dae0e-153">Lazy loading can mask code that causes performance problems.</span></span> <span data-ttu-id="dae0e-154">例如，不指定積極或明確載入的程式碼，但會處理大量的實體，並且在每個反復專案中使用數個導覽屬性， (因為許多往返于資料庫) 的往返。</span><span class="sxs-lookup"><span data-stu-id="dae0e-154">For example, code that doesn't specify eager or explicit loading but processes a high volume of entities and uses several navigation properties in each iteration might be very inefficient (because of many round trips to the database).</span></span> <span data-ttu-id="dae0e-155">當應用程式在使用內部部署 SQL server 進行開發時，可能會因為延遲和消極式載入的增加而移至 Azure SQL Database，所以會發生效能問題。</span><span class="sxs-lookup"><span data-stu-id="dae0e-155">An application that performs well in development using an on premise SQL server might have performance problems when moved to Azure SQL Database due to the increased latency and lazy loading.</span></span> <span data-ttu-id="dae0e-156">使用實際的測試負載來分析資料庫查詢，可協助您判斷是否有適當的延遲載入。</span><span class="sxs-lookup"><span data-stu-id="dae0e-156">Profiling the database queries with a realistic test load will help you determine if lazy loading is appropriate.</span></span> <span data-ttu-id="dae0e-157">如需詳細資訊，請參閱 [揭開 Entity Framework 策略：載入相關資料](https://msdn.microsoft.com/magazine/hh205756.aspx) 和 [使用 Entity Framework，以降低 SQL Azure 的網路延遲](https://msdn.microsoft.com/magazine/gg309181.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dae0e-157">For more information see [Demystifying Entity Framework Strategies: Loading Related Data](https://msdn.microsoft.com/magazine/hh205756.aspx) and [Using the Entity Framework to Reduce Network Latency to SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).</span></span>

## <a name="create-a-courses-index-page-that-displays-department-name"></a><span data-ttu-id="dae0e-158">建立顯示部門名稱的課程索引頁面</span><span class="sxs-lookup"><span data-stu-id="dae0e-158">Create a Courses Index Page That Displays Department Name</span></span>

<span data-ttu-id="dae0e-159">`Course`實體包含導覽屬性，其中包含 `Department` 指派給課程的部門實體。</span><span class="sxs-lookup"><span data-stu-id="dae0e-159">The `Course` entity includes a navigation property that contains the `Department` entity of the department that the course is assigned to.</span></span> <span data-ttu-id="dae0e-160">若要在課程清單中顯示所指派部門的名稱，您需要 `Name` 從 `Department` 導覽屬性中的實體取得屬性 `Course.Department` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-160">To display the name of the assigned department in a list of courses, you need to get the `Name` property from the `Department` entity that is in the `Course.Department` navigation property.</span></span>

<span data-ttu-id="dae0e-161">`CourseController` `Course` 使用您稍早為控制器執行的相同選項來建立名為實體類型的控制器， `Student` 如下圖所示 (（不同于影像），您的內容類別會在 DAL 命名空間中，而不是模型命名空間) ：</span><span class="sxs-lookup"><span data-stu-id="dae0e-161">Create a controller named `CourseController` for the `Course` entity type, using the same options that you did earlier for the `Student` controller, as shown in the following illustration (except unlike the image, your context class is in the DAL namespace, not the Models namespace):</span></span>

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

<span data-ttu-id="dae0e-163">開啟 *Controllers\CourseController.cs* ，並查看 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="dae0e-163">Open *Controllers\CourseController.cs* and look at the `Index` method:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="dae0e-164">自動 Scaffolding 已使用 `Include` 方法，針對 `Department` 導覽屬性指定積極式載入。</span><span class="sxs-lookup"><span data-stu-id="dae0e-164">The automatic scaffolding has specified eager loading for the `Department` navigation property by using the `Include` method.</span></span>

<span data-ttu-id="dae0e-165">開啟 *Views\Course\Index.cshtml* ，並以下列程式碼取代現有的程式碼。</span><span class="sxs-lookup"><span data-stu-id="dae0e-165">Open *Views\Course\Index.cshtml* and replace the existing code with the following code.</span></span> <span data-ttu-id="dae0e-166">所做的變更已醒目提示：</span><span class="sxs-lookup"><span data-stu-id="dae0e-166">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

<span data-ttu-id="dae0e-167">您已對包含 Scaffold 的程式碼進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="dae0e-167">You've made the following changes to the scaffolded code:</span></span>

- <span data-ttu-id="dae0e-168">已將標題從 **索引** 變更為 **課程**。</span><span class="sxs-lookup"><span data-stu-id="dae0e-168">Changed the heading from **Index** to **Courses**.</span></span>
- <span data-ttu-id="dae0e-169">將資料列連結移至左側。</span><span class="sxs-lookup"><span data-stu-id="dae0e-169">Moved the row links to the left.</span></span>
- <span data-ttu-id="dae0e-170">在顯示內容值的標題 **編號** 底下加入資料行 `CourseID` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-170">Added a column under the heading **Number** that shows the `CourseID` property value.</span></span> <span data-ttu-id="dae0e-171"> (預設不會 scaffold 主鍵，因為它們通常對使用者而言沒有意義。</span><span class="sxs-lookup"><span data-stu-id="dae0e-171">(By default, primary keys aren't scaffolded because normally they are meaningless to end users.</span></span> <span data-ttu-id="dae0e-172">不過，在此情況下，主鍵有意義，而您想要加以顯示。 ) </span><span class="sxs-lookup"><span data-stu-id="dae0e-172">However, in this case the primary key is meaningful and you want to show it.)</span></span>
- <span data-ttu-id="dae0e-173">將 **DepartmentID** 中的最後一個資料行標題變更 (的外鍵名稱加入至 `Department` **部門** 的實體) 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-173">Changed the last column heading from **DepartmentID** (the name of the foreign key to the `Department` entity) to **Department**.</span></span>

<span data-ttu-id="dae0e-174">請注意，在最後一個資料行中，scaffold 程式碼會顯示已 `Name` `Department` 載入導覽屬性之實體的屬性 `Department` ：</span><span class="sxs-lookup"><span data-stu-id="dae0e-174">Notice that for the last column, the scaffolded code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

<span data-ttu-id="dae0e-175">執行頁面 (在 Contoso 大學首頁上選取 [ **課程** ] 索引標籤，) 以查看具有部門名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="dae0e-175">Run the page (select the **Courses** tab on the Contoso University home page) to see the list with department names.</span></span>

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a><span data-ttu-id="dae0e-177">建立顯示課程和註冊的講師索引頁面</span><span class="sxs-lookup"><span data-stu-id="dae0e-177">Create an Instructors Index Page That Shows Courses and Enrollments</span></span>

<span data-ttu-id="dae0e-178">在本節中，您將建立實體的控制器和查看， `Instructor` 以顯示講師索引頁面：</span><span class="sxs-lookup"><span data-stu-id="dae0e-178">In this section you'll create a controller and view for the `Instructor` entity in order to display the Instructors Index page:</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="dae0e-180">此頁面將以下列方式讀取和顯示相關資料：</span><span class="sxs-lookup"><span data-stu-id="dae0e-180">This page reads and displays related data in the following ways:</span></span>

- <span data-ttu-id="dae0e-181">講師清單會顯示實體中的相關資料 `OfficeAssignment` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-181">The list of instructors displays related data from the `OfficeAssignment` entity.</span></span> <span data-ttu-id="dae0e-182">`Instructor` 與 `OfficeAssignment` 實體具有一對零或一關聯性。</span><span class="sxs-lookup"><span data-stu-id="dae0e-182">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="dae0e-183">您將針對實體使用積極式載入 `OfficeAssignment` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-183">You'll use eager loading for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="dae0e-184">如上所述，當您需要主要資料表中所有擷取資料列的相關資料時，積極式載入通常更有效率。</span><span class="sxs-lookup"><span data-stu-id="dae0e-184">As explained earlier, eager loading is typically more efficient when you need the related data for all retrieved rows of the primary table.</span></span> <span data-ttu-id="dae0e-185">在此情況下，您可能想要顯示所有已呈現講師的辦公室指派。</span><span class="sxs-lookup"><span data-stu-id="dae0e-185">In this case, you want to display office assignments for all displayed instructors.</span></span>
- <span data-ttu-id="dae0e-186">當使用者選取講師時，將會顯示相關的 `Course` 實體。</span><span class="sxs-lookup"><span data-stu-id="dae0e-186">When the user selects an instructor, related `Course` entities are displayed.</span></span> <span data-ttu-id="dae0e-187">`Instructor` 與 `Course` 實體具有多對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="dae0e-187">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="dae0e-188">您將針對 `Course` 實體及其相關實體使用積極式載入 `Department` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-188">You'll use eager loading for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="dae0e-189">在此情況下，消極式載入可能更有效率，因為您只需要選取的講師的課程。</span><span class="sxs-lookup"><span data-stu-id="dae0e-189">In this case, lazy loading might be more efficient because you need courses only for the selected instructor.</span></span> <span data-ttu-id="dae0e-190">不過，這個範例會示範如何在本身處於導覽屬性內的實體中，針對導覽屬性使用積極式載入。</span><span class="sxs-lookup"><span data-stu-id="dae0e-190">However, this example shows how to use eager loading for navigation properties within entities that are themselves in navigation properties.</span></span>
- <span data-ttu-id="dae0e-191">當使用者選取課程時， `Enrollments` 會顯示來自實體集的相關資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-191">When the user selects a course, related data from the `Enrollments` entity set is displayed.</span></span> <span data-ttu-id="dae0e-192">`Course` 與 `Enrollment` 實體具有一對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="dae0e-192">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span> <span data-ttu-id="dae0e-193">您將為 `Enrollment` 實體及其相關實體新增明確的載入 `Student` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-193">You'll add explicit loading for `Enrollment` entities and their related `Student` entities.</span></span> <span data-ttu-id="dae0e-194"> (明確的載入並不是必要的，因為已啟用消極式載入，但這會顯示如何執行明確的載入。 ) </span><span class="sxs-lookup"><span data-stu-id="dae0e-194">(Explicit loading isn't necessary because lazy loading is enabled, but this shows how to do explicit loading.)</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="dae0e-195">建立講師索引視圖的視圖模型</span><span class="sxs-lookup"><span data-stu-id="dae0e-195">Create a View Model for the Instructor Index View</span></span>

<span data-ttu-id="dae0e-196">講師索引頁面會顯示三個不同的資料表。</span><span class="sxs-lookup"><span data-stu-id="dae0e-196">The Instructor Index page shows three different tables.</span></span> <span data-ttu-id="dae0e-197">因此，您將建立包含三個屬性的檢視模型，每個保留其中一個資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-197">Therefore, you'll create a view model that includes three properties, each holding the data for one of the tables.</span></span>

<span data-ttu-id="dae0e-198">在 *viewmodel* 資料夾中，建立 *InstructorIndexData.cs* ，並使用下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="dae0e-198">In the *ViewModels* folder, create *InstructorIndexData.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a><span data-ttu-id="dae0e-199">為選取的資料列加入樣式</span><span class="sxs-lookup"><span data-stu-id="dae0e-199">Adding a Style for Selected Rows</span></span>

<span data-ttu-id="dae0e-200">若要標記選取的資料列，您需要不同的背景色彩。</span><span class="sxs-lookup"><span data-stu-id="dae0e-200">To mark selected rows you need a different background color.</span></span> <span data-ttu-id="dae0e-201">若要為此 UI 提供樣式，請將下列反白顯示的程式碼新增至 `/* info and errors */` *Content\Site.css* 中的區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dae0e-201">To provide a style for this UI, add the following highlighted code to the section `/* info and errors */` in *Content\Site.css*, as shown below:</span></span>

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a><span data-ttu-id="dae0e-202">建立講師控制器和 Views</span><span class="sxs-lookup"><span data-stu-id="dae0e-202">Creating the Instructor Controller and Views</span></span>

<span data-ttu-id="dae0e-203">建立 `InstructorController` 控制器，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="dae0e-203">Create an `InstructorController` controller as shown in the following illustration:</span></span>

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

<span data-ttu-id="dae0e-205">開啟 *Controllers\InstructorController.cs* ，並加入 `using` `ViewModels` 命名空間的語句：</span><span class="sxs-lookup"><span data-stu-id="dae0e-205">Open *Controllers\InstructorController.cs* and add a `using` statement for the `ViewModels` namespace:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="dae0e-206">方法中的 scaffold 程式碼 `Index` 只會針對導覽屬性指定積極式載入 `OfficeAssignment` ：</span><span class="sxs-lookup"><span data-stu-id="dae0e-206">The scaffolded code in the `Index` method specifies eager loading only for the `OfficeAssignment` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="dae0e-207">`Index`以下列程式碼取代方法，以載入其他相關資料，並將其放在 view 模型中：</span><span class="sxs-lookup"><span data-stu-id="dae0e-207">Replace the `Index` method with the following code to load additional related data and put it in the view model:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="dae0e-208">方法會接受選擇性的路由資料 (`id`) 和查詢字串參數 (`courseID`) ，提供所選講師和所選課程的識別碼值，並將所有必要的資料傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="dae0e-208">The method accepts optional route data (`id`) and a query string parameter (`courseID`) that provide the ID values of the selected instructor and selected course, and passes all of the required data to the view.</span></span> <span data-ttu-id="dae0e-209">這些參數由頁面上的 **選取** 超連結提供。</span><span class="sxs-lookup"><span data-stu-id="dae0e-209">The parameters are provided by the **Select** hyperlinks on the page.</span></span>

> [!TIP]
> 
> <span data-ttu-id="dae0e-210">**路由傳送資料**</span><span class="sxs-lookup"><span data-stu-id="dae0e-210">**Route data**</span></span>
> 
> <span data-ttu-id="dae0e-211">路由資料是模型系結器在路由表中指定的 URL 區段中找到的資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-211">Route data is data that the model binder found in a URL segment specified in the routing table.</span></span> <span data-ttu-id="dae0e-212">例如，預設路由會指定 `controller` 、 `action` 和 `id` 區段：</span><span class="sxs-lookup"><span data-stu-id="dae0e-212">For example, the default route specifies `controller`, `action`, and `id` segments:</span></span>
> 
> ```csharp
> routes.MapRoute(  
>  name: "Default",  
>  url: "{controller}/{action}/{id}",  
>  defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }  
> );
> ```
> 
> <span data-ttu-id="dae0e-213">在下列 URL 中，預設路由會對應 `Instructor` 為 `controller` ， `Index` 如 `action` 和1一樣， `id` 這些都是路由資料值。</span><span class="sxs-lookup"><span data-stu-id="dae0e-213">In the following URL, the default route maps `Instructor` as the `controller`, `Index` as the `action` and 1 as the `id`; these are route data values.</span></span>
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> <span data-ttu-id="dae0e-214">"？ courseID = 2021" 是查詢字串值。</span><span class="sxs-lookup"><span data-stu-id="dae0e-214">"?courseID=2021" is a query string value.</span></span> <span data-ttu-id="dae0e-215">如果您傳遞 `id` 做為查詢字串值，模型系結器也會運作：</span><span class="sxs-lookup"><span data-stu-id="dae0e-215">The model binder will also work if you pass the `id` as a query string value:</span></span>
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> <span data-ttu-id="dae0e-216">這些 Url 是由 `ActionLink` Razor view 中的語句所建立。</span><span class="sxs-lookup"><span data-stu-id="dae0e-216">The URLs are created by `ActionLink` statements in the Razor view.</span></span> <span data-ttu-id="dae0e-217">在下列程式碼中， `id` 參數會符合預設路由，因此 `id` 會新增至路由資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-217">In the following code, the `id` parameter matches the default route, so `id` is added to the route data.</span></span>
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> <span data-ttu-id="dae0e-218">在下列程式碼中，與 `courseID` 預設路由中的參數不相符，因此會將它新增為查詢字串。</span><span class="sxs-lookup"><span data-stu-id="dae0e-218">In the following code, `courseID` doesn't match a parameter in the default route, so it's added as a query string.</span></span>
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

<span data-ttu-id="dae0e-219">此程式碼是從建立檢視模型的執行個體，並將其置於講師清單開始。</span><span class="sxs-lookup"><span data-stu-id="dae0e-219">The code begins by creating an instance of the view model and putting in it the list of instructors.</span></span> <span data-ttu-id="dae0e-220">程式碼會為 `Instructor.OfficeAssignment` 和導覽屬性指定積極式載入 `Instructor.Courses` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-220">The code specifies eager loading for the `Instructor.OfficeAssignment` and the `Instructor.Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

<span data-ttu-id="dae0e-221">第二 `Include` 種方法會載入課程，且每個載入的課程都會針對導覽屬性執行積極式載入 `Course.Department` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-221">The second `Include` method loads Courses, and for each Course that is loaded it does eager loading for the `Course.Department` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="dae0e-222">如先前所述，不需要積極式載入，而是為了改善效能。</span><span class="sxs-lookup"><span data-stu-id="dae0e-222">As mentioned previously, eager loading is not required but is done to improve performance.</span></span> <span data-ttu-id="dae0e-223">由於視圖一律需要 `OfficeAssignment` 實體，因此在相同的查詢中提取該實體會更有效率。</span><span class="sxs-lookup"><span data-stu-id="dae0e-223">Since the view always requires the `OfficeAssignment` entity, it's more efficient to fetch that in the same query.</span></span> <span data-ttu-id="dae0e-224">`Course` 當您在網頁中選取講師時，需要實體，因此只有在選取的課程比 [沒有] 時，積極式載入才會比延遲載入更好。</span><span class="sxs-lookup"><span data-stu-id="dae0e-224">`Course` entities are required when an instructor is selected in the web page, so eager loading is better than lazy loading only if the page is displayed more often with a course selected than without.</span></span>

<span data-ttu-id="dae0e-225">如果選取了講師識別碼，就會從視圖模型中的講師清單抓取選取的講師。</span><span class="sxs-lookup"><span data-stu-id="dae0e-225">If an instructor ID was selected, the selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="dae0e-226">`Courses`然後，會使用 `Course` 來自該講師導覽屬性的實體載入視圖模型的屬性 `Courses` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-226">The view model's `Courses` property is then loaded with the `Course` entities from that instructor's `Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="dae0e-227">`Where`方法會傳回集合，但在此情況下，傳遞至該方法的準則會導致只 `Instructor` 傳回單一實體。</span><span class="sxs-lookup"><span data-stu-id="dae0e-227">The `Where` method returns a collection, but in this case the criteria passed to that method result in only a single `Instructor` entity being returned.</span></span> <span data-ttu-id="dae0e-228">`Single`方法會將集合轉換成單一 `Instructor` 實體，讓您存取該實體的 `Courses` 屬性。</span><span class="sxs-lookup"><span data-stu-id="dae0e-228">The `Single` method converts the collection into a single `Instructor` entity, which gives you access to that entity's `Courses` property.</span></span>

<span data-ttu-id="dae0e-229">當您知道集合只會有一個專案時，您會在集合上使用 [單一](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) 方法。</span><span class="sxs-lookup"><span data-stu-id="dae0e-229">You use the [Single](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) method on a collection when you know the collection will have only one item.</span></span> <span data-ttu-id="dae0e-230">`Single`如果傳遞給它的集合是空的，或有多個專案，方法會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="dae0e-230">The `Single` method throws an exception if the collection passed to it is empty or if there's more than one item.</span></span> <span data-ttu-id="dae0e-231">替代方法是 [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，在此情況下會傳回預設值 (`null`) 如果集合是空的。</span><span class="sxs-lookup"><span data-stu-id="dae0e-231">An alternative is [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), which returns a default value (`null` in this case) if the collection is empty.</span></span> <span data-ttu-id="dae0e-232">不過，在這種情況下，仍會導致例外狀況 (嘗試在 `Courses` 參考) 上尋找屬性 `null` ，而例外狀況訊息會不清楚地指出問題的原因。</span><span class="sxs-lookup"><span data-stu-id="dae0e-232">However, in this case that would still result in an exception (from trying to find a `Courses` property on a `null` reference), and the exception message would less clearly indicate the cause of the problem.</span></span> <span data-ttu-id="dae0e-233">當您呼叫 `Single` 方法時，您也可以傳入條件， `Where` 而不是分別呼叫 `Where` 方法：</span><span class="sxs-lookup"><span data-stu-id="dae0e-233">When you call the `Single` method, you can also pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="dae0e-234">不要這樣撰寫：</span><span class="sxs-lookup"><span data-stu-id="dae0e-234">Instead of:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="dae0e-235">接下來，如果已選取課程，則會從檢視模型的課程清單中擷取選取的課程。</span><span class="sxs-lookup"><span data-stu-id="dae0e-235">Next, if a course was selected, the selected course is retrieved from the list of courses in the view model.</span></span> <span data-ttu-id="dae0e-236">然後， `Enrollments` 會使用 `Enrollment` 該課程導覽屬性中的實體載入視圖模型的屬性 `Enrollments` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-236">Then the view model's `Enrollments` property is loaded with the `Enrollment` entities from that course's `Enrollments` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a><span data-ttu-id="dae0e-237">修改講師索引視圖</span><span class="sxs-lookup"><span data-stu-id="dae0e-237">Modifying the Instructor Index View</span></span>

<span data-ttu-id="dae0e-238">在 *Views\Instructor\Index.cshtml* 中，將現有的程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="dae0e-238">In *Views\Instructor\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="dae0e-239">所做的變更已醒目提示：</span><span class="sxs-lookup"><span data-stu-id="dae0e-239">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

<span data-ttu-id="dae0e-240">您已對現有程式碼進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="dae0e-240">You've made the following changes to the existing code:</span></span>

- <span data-ttu-id="dae0e-241">已將模型類別變更為 `InstructorIndexData`。</span><span class="sxs-lookup"><span data-stu-id="dae0e-241">Changed the model class to `InstructorIndexData`.</span></span>
- <span data-ttu-id="dae0e-242">已將頁面標題從 **索引** 變更為 **講師**。</span><span class="sxs-lookup"><span data-stu-id="dae0e-242">Changed the page title from **Index** to **Instructors**.</span></span>
- <span data-ttu-id="dae0e-243">將資料列連結資料行向左移動。</span><span class="sxs-lookup"><span data-stu-id="dae0e-243">Moved the row link columns to the left.</span></span>
- <span data-ttu-id="dae0e-244">已移除 **FullName** 資料行。</span><span class="sxs-lookup"><span data-stu-id="dae0e-244">Removed the **FullName** column.</span></span>
- <span data-ttu-id="dae0e-245">加入 `item.OfficeAssignment.Location` 只有當不是 null 時才會顯示的 Office 資料行 `item.OfficeAssignment` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-245">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` is not null.</span></span> <span data-ttu-id="dae0e-246"> (，因為這是一對零或一關聯性，所以可能不會有相關的 `OfficeAssignment` 實體。 ) </span><span class="sxs-lookup"><span data-stu-id="dae0e-246">(Because this is a one-to-zero-or-one relationship, there might not be a related `OfficeAssignment` entity.)</span></span> 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- <span data-ttu-id="dae0e-247">已新增程式碼，以動態方式新增 `class="selectedrow"` 至 `tr` 所選講師的元素。</span><span class="sxs-lookup"><span data-stu-id="dae0e-247">Added code that will dynamically add `class="selectedrow"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="dae0e-248">這會使用您稍早建立的 CSS 類別，設定所選取資料列的背景色彩。</span><span class="sxs-lookup"><span data-stu-id="dae0e-248">This sets a background color for the selected row using the CSS class that you created earlier.</span></span> <span data-ttu-id="dae0e-249"> (`valign` 當您將多個資料列資料行加入至資料表時，屬性將在下列教學課程中有用。 ) </span><span class="sxs-lookup"><span data-stu-id="dae0e-249">(The `valign` attribute will be useful in the following tutorial when you add a multi-row column to the table.)</span></span> 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- <span data-ttu-id="dae0e-250">在 `ActionLink` 每個資料列中的其他連結之前，立即新增加上標籤的 **Select** ，這會導致選取的講師識別碼傳送至 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="dae0e-250">Added a new `ActionLink` labeled **Select** immediately before the other links in each row, which causes the selected instructor ID to be sent to the `Index` method.</span></span>

<span data-ttu-id="dae0e-251">執行應用程式，然後選取 [ **講師** ] 索引標籤。當沒有相關實體時，此頁面會顯示 `Location` 相關實體的屬性 `OfficeAssignment` ，以及空白的資料表單元格 `OfficeAssignment` 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-251">Run the application and select the **Instructors** tab. The page displays the `Location` property of related `OfficeAssignment` entities and an empty table cell when there's no related `OfficeAssignment` entity.</span></span>

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="dae0e-253">在 *Views\Instructor\Index.cshtml* 檔案中，在 `table`) 檔案結尾 (結尾元素之後，新增下列反白顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="dae0e-253">In the *Views\Instructor\Index.cshtml* file, after the closing `table` element (at the end of the file), add the following highlighted code.</span></span> <span data-ttu-id="dae0e-254">當選取講師時，這會顯示與講師相關的課程清單。</span><span class="sxs-lookup"><span data-stu-id="dae0e-254">This displays a list of courses related to an instructor when an instructor is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

<span data-ttu-id="dae0e-255">此程式碼會讀取檢視模型的 `Courses` 屬性以顯示課程清單。</span><span class="sxs-lookup"><span data-stu-id="dae0e-255">This code reads the `Courses` property of the view model to display a list of courses.</span></span> <span data-ttu-id="dae0e-256">它也會提供 `Select` 超連結，將所選課程的識別碼傳送至 `Index` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="dae0e-256">It also provides a `Select` hyperlink that sends the ID of the selected course to the `Index` action method.</span></span>

> [!NOTE]
> <span data-ttu-id="dae0e-257">*.Css* 檔案是由瀏覽器快取。</span><span class="sxs-lookup"><span data-stu-id="dae0e-257">The *.css* file is cached by browsers.</span></span> <span data-ttu-id="dae0e-258">如果您在執行應用程式時看不到變更，請執行硬重新整理 (按住 CTRL 鍵同時按一下 [重新整理 **] 按鈕，** 或按 Ctrl + F5) 。</span><span class="sxs-lookup"><span data-stu-id="dae0e-258">If you don't see the changes when you run the application, do a hard refresh (hold down the CTRL key while clicking the **Refresh** button, or press CTRL+F5).</span></span>

<span data-ttu-id="dae0e-259">執行頁面並選取講師。</span><span class="sxs-lookup"><span data-stu-id="dae0e-259">Run the page and select an instructor.</span></span> <span data-ttu-id="dae0e-260">現在您會看到一個方格，其中顯示指派給所選取講師的課程，而且在每個課程中，您可以看到指派的部門名稱。</span><span class="sxs-lookup"><span data-stu-id="dae0e-260">Now you see a grid that displays courses assigned to the selected instructor, and for each course you see the name of the assigned department.</span></span>

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="dae0e-262">在您剛才新增的程式碼區塊之後，新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="dae0e-262">After the code block you just added, add the following code.</span></span> <span data-ttu-id="dae0e-263">這會在選取課程時，顯示已註冊該課程的學生清單。</span><span class="sxs-lookup"><span data-stu-id="dae0e-263">This displays a list of the students who are enrolled in a course when that course is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

<span data-ttu-id="dae0e-264">此程式碼會讀取 `Enrollments` 視圖模型的屬性，以便顯示在課程中註冊的學生清單。</span><span class="sxs-lookup"><span data-stu-id="dae0e-264">This code reads the `Enrollments` property of the view model in order to display a list of students enrolled in the course.</span></span>

<span data-ttu-id="dae0e-265">執行頁面並選取講師。</span><span class="sxs-lookup"><span data-stu-id="dae0e-265">Run the page and select an instructor.</span></span> <span data-ttu-id="dae0e-266">接著選取課程，以查看已註冊學生和其年級的清單。</span><span class="sxs-lookup"><span data-stu-id="dae0e-266">Then select a course to see the list of enrolled students and their grades.</span></span>

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a><span data-ttu-id="dae0e-268">新增明確的載入</span><span class="sxs-lookup"><span data-stu-id="dae0e-268">Adding Explicit Loading</span></span>

<span data-ttu-id="dae0e-269">開啟 *InstructorController.cs* ，並查看方法如何 `Index` 取得所選課程的註冊清單：</span><span class="sxs-lookup"><span data-stu-id="dae0e-269">Open *InstructorController.cs* and look at how the `Index` method gets the list of enrollments for a selected course:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="dae0e-270">當您取出講師清單時，就是針對導覽屬性指定積極式載入， `Courses` 並為 `Department` 每個課程的屬性指定積極式載入。</span><span class="sxs-lookup"><span data-stu-id="dae0e-270">When you retrieved the list of instructors, you specified eager loading for the `Courses` navigation property and for the `Department` property of each course.</span></span> <span data-ttu-id="dae0e-271">然後，將 `Courses` 集合放在 view 模型中，現在您要 `Enrollments` 從該集合中的一個實體存取導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="dae0e-271">Then you put the `Courses` collection in the view model, and now you're accessing the `Enrollments` navigation property from one entity in that collection.</span></span> <span data-ttu-id="dae0e-272">因為您未指定導覽屬性的積極式載入 `Course.Enrollments` ，所以來自該屬性的資料會因為消極式載入而出現在頁面中。</span><span class="sxs-lookup"><span data-stu-id="dae0e-272">Because you didn't specify eager loading for the `Course.Enrollments` navigation property, the data from that property is appearing in the page as a result of lazy loading.</span></span>

<span data-ttu-id="dae0e-273">如果您停用消極式載入，而不以任何其他方式變更程式碼，則 `Enrollments` 不論課程實際有多少註冊，屬性都是 null。</span><span class="sxs-lookup"><span data-stu-id="dae0e-273">If you disabled lazy loading without changing the code in any other way, the `Enrollments` property would be null regardless of how many enrollments the course actually had.</span></span> <span data-ttu-id="dae0e-274">在此情況下，若要載入 `Enrollments` 屬性，您必須指定立即載入或明確載入。</span><span class="sxs-lookup"><span data-stu-id="dae0e-274">In that case, to load the `Enrollments` property, you'd have to specify either eager loading or explicit loading.</span></span> <span data-ttu-id="dae0e-275">您已經看過如何進行積極式載入。</span><span class="sxs-lookup"><span data-stu-id="dae0e-275">You've already seen how to do eager loading.</span></span> <span data-ttu-id="dae0e-276">若要查看明確載入的範例，請以下列程式 `Index` 代碼取代方法，以明確載入 `Enrollments` 屬性。</span><span class="sxs-lookup"><span data-stu-id="dae0e-276">In order to see an example of explicit loading, replace the `Index` method with the following code, which explicitly loads the `Enrollments` property.</span></span> <span data-ttu-id="dae0e-277">變更的程式碼會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="dae0e-277">The code changed are highlighted.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

<span data-ttu-id="dae0e-278">取得選取的 `Course` 實體之後，新的程式碼會明確地載入該課程的 `Enrollments` 導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="dae0e-278">After getting the selected `Course` entity, the new code explicitly loads that course's `Enrollments` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="dae0e-279">然後，它會明確載入每個 `Enrollment` 實體的相關 `Student` 實體：</span><span class="sxs-lookup"><span data-stu-id="dae0e-279">Then it explicitly loads each `Enrollment` entity's related `Student` entity:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="dae0e-280">請注意，您可以使用 `Collection` 方法來載入集合屬性，但對於只保留一個實體的屬性，您可以使用 `Reference` 方法。</span><span class="sxs-lookup"><span data-stu-id="dae0e-280">Notice that you use the `Collection` method to load a collection property, but for a property that holds just one entity, you use the `Reference` method.</span></span> <span data-ttu-id="dae0e-281">您現在可以執行講師索引頁面，而在頁面上顯示的內容中看不到任何差異，不過您已經變更了資料的抓取方式。</span><span class="sxs-lookup"><span data-stu-id="dae0e-281">You can run the Instructor Index page now and you'll see no difference in what's displayed on the page, although you've changed how the data is retrieved.</span></span>

## <a name="summary"></a><span data-ttu-id="dae0e-282">摘要</span><span class="sxs-lookup"><span data-stu-id="dae0e-282">Summary</span></span>

<span data-ttu-id="dae0e-283">您現在已使用這三種方法 (消極式、積極且明確的) 將相關資料載入導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="dae0e-283">You've now used all three ways (lazy, eager, and explicit) to load related data into navigation properties.</span></span> <span data-ttu-id="dae0e-284">在下一個教學課程中，您將了解如何更新相關資料。</span><span class="sxs-lookup"><span data-stu-id="dae0e-284">In the next tutorial you'll learn how to update related data.</span></span>

<span data-ttu-id="dae0e-285">您可以在 [ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="dae0e-285">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dae0e-286">[上一個](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) 
> [下一步](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="dae0e-286">[Previous](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
[Next](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
