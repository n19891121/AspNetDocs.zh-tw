---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：閱讀 ASP.NET MVC 應用程式中使用 EF 的相關的資料
description: 在本教學課程中，您將讀取並顯示相關的資料-也就是 Entity Framework 載入到導覽屬性的資料。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 61bd7cd9be2fbf83f72382c8e94505222295bdbb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038135"
---
[<span data-ttu-id="7046e-103">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="7046e-103">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> <span data-ttu-id="7046e-104">Contoso 大學範例 web 應用程式會示範如何建立使用 Entity Framework 6 Code First 和 Visual Studio 的 ASP.NET MVC 5 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7046e-104">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio.</span></span> <span data-ttu-id="7046e-105">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="7046e-105">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

# <a name="tutorial-read-related-data-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="7046e-106">教學課程：閱讀 ASP.NET MVC 應用程式中使用 EF 的相關的資料</span><span class="sxs-lookup"><span data-stu-id="7046e-106">Tutorial: Read related data with EF in an ASP.NET MVC app</span></span>

<span data-ttu-id="7046e-107">在上一個教學課程，您已完成 School 資料模型的內容。</span><span class="sxs-lookup"><span data-stu-id="7046e-107">In the previous tutorial you completed the School data model.</span></span> <span data-ttu-id="7046e-108">在本教學課程中，您將讀取並顯示相關的資料-也就是 Entity Framework 載入到導覽屬性的資料。</span><span class="sxs-lookup"><span data-stu-id="7046e-108">In this tutorial you'll read and display related data — that is, data that the Entity Framework loads into navigation properties.</span></span>

<span data-ttu-id="7046e-109">下列圖例顯示了您將操作的頁面。</span><span class="sxs-lookup"><span data-stu-id="7046e-109">The following illustrations show the pages that you'll work with.</span></span>

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="7046e-111">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="7046e-111">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7046e-112">了解如何載入相關資料</span><span class="sxs-lookup"><span data-stu-id="7046e-112">Learn how to load related data</span></span>
> * <span data-ttu-id="7046e-113">建立 Courses 頁面</span><span class="sxs-lookup"><span data-stu-id="7046e-113">Create a Courses page</span></span>
> * <span data-ttu-id="7046e-114">建立 Instructors 頁面</span><span class="sxs-lookup"><span data-stu-id="7046e-114">Create an Instructors page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7046e-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="7046e-115">Prerequisites</span></span>

* [<span data-ttu-id="7046e-116">建立更複雜的資料模型</span><span class="sxs-lookup"><span data-stu-id="7046e-116">Create a more complex data model</span></span>](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="learn-how-to-load-related-data"></a><span data-ttu-id="7046e-117">了解如何載入相關資料</span><span class="sxs-lookup"><span data-stu-id="7046e-117">Learn how to load related data</span></span>

<span data-ttu-id="7046e-118">有數種方式，Entity Framework，可將相關的資料載入實體的導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="7046e-118">There are several ways that the Entity Framework can load related data into the navigation properties of an entity:</span></span>

- <span data-ttu-id="7046e-119">*消極式載入*。</span><span class="sxs-lookup"><span data-stu-id="7046e-119">*Lazy loading*.</span></span> <span data-ttu-id="7046e-120">第一次讀取實體時，不會擷取相關資料。</span><span class="sxs-lookup"><span data-stu-id="7046e-120">When the entity is first read, related data isn't retrieved.</span></span> <span data-ttu-id="7046e-121">不過，第一次嘗試存取導覽屬性時，將會自動擷取該導覽屬性所需的資料。</span><span class="sxs-lookup"><span data-stu-id="7046e-121">However, the first time you attempt to access a navigation property, the data required for that navigation property is automatically retrieved.</span></span> <span data-ttu-id="7046e-122">這會導致多個查詢傳送至資料庫，一個用於實體本身，一個必須擷取每個相關實體資料的時間。</span><span class="sxs-lookup"><span data-stu-id="7046e-122">This results in multiple queries sent to the database — one for the entity itself and one each time that related data for the entity must be retrieved.</span></span> <span data-ttu-id="7046e-123">`DbContext`類別預設會啟用消極式載入。</span><span class="sxs-lookup"><span data-stu-id="7046e-123">The `DbContext` class enables lazy loading by default.</span></span>

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- <span data-ttu-id="7046e-125">*積極式載入*。</span><span class="sxs-lookup"><span data-stu-id="7046e-125">*Eager loading*.</span></span> <span data-ttu-id="7046e-126">讀取實體時，將會同時擷取其相關資料。</span><span class="sxs-lookup"><span data-stu-id="7046e-126">When the entity is read, related data is retrieved along with it.</span></span> <span data-ttu-id="7046e-127">這通常會導致單一聯結查詢，其可擷取所有需要的資料。</span><span class="sxs-lookup"><span data-stu-id="7046e-127">This typically results in a single join query that retrieves all of the data that's needed.</span></span> <span data-ttu-id="7046e-128">使用指定積極式載入`Include`方法。</span><span class="sxs-lookup"><span data-stu-id="7046e-128">You specify eager loading by using the `Include` method.</span></span>

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- <span data-ttu-id="7046e-130">*明確式載入*。</span><span class="sxs-lookup"><span data-stu-id="7046e-130">*Explicit loading*.</span></span> <span data-ttu-id="7046e-131">這是類似於消極式載入，不同之處在於您明確地擷取相關的資料，在程式碼當您存取導覽屬性時，它不會發生自動。</span><span class="sxs-lookup"><span data-stu-id="7046e-131">This is similar to lazy loading, except that you explicitly retrieve the related data in code; it doesn't happen automatically when you access a navigation property.</span></span> <span data-ttu-id="7046e-132">您載入相關的資料手動藉由取得物件狀態管理員項目實體和呼叫[Collection.Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx)集合的方法或[Reference.Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx)保存屬性的方法單一實體。</span><span class="sxs-lookup"><span data-stu-id="7046e-132">You load related data manually by getting the object state manager entry for an entity and calling the [Collection.Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx) method for collections or the [Reference.Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx) method for properties that hold a single entity.</span></span> <span data-ttu-id="7046e-133">(在下列範例中，如果您想要載入 [管理員] 瀏覽屬性中，您會取代`Collection(x => x.Courses)`與`Reference(x => x.Administrator)`。)通常您會使用您已開啟消極式載入關閉時，只明確載入。</span><span class="sxs-lookup"><span data-stu-id="7046e-133">(In the following example, if you wanted to load the Administrator navigation property, you'd replace `Collection(x => x.Courses)` with `Reference(x => x.Administrator)`.) Typically you'd use explicit loading only when you've turned lazy loading off.</span></span>

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

<span data-ttu-id="7046e-135">因為它們不立即擷取的屬性值，消極式載入和明確式載入同時所謂*延後載入*。</span><span class="sxs-lookup"><span data-stu-id="7046e-135">Because they don't immediately retrieve the property values, lazy loading and explicit loading are also both known as *deferred loading*.</span></span>

### <a name="performance-considerations"></a><span data-ttu-id="7046e-136">效能考量</span><span class="sxs-lookup"><span data-stu-id="7046e-136">Performance considerations</span></span>

<span data-ttu-id="7046e-137">如果您知道擷取的每個實體需要相關資料，積極式載入通常可以提供最佳效能，因為傳送至資料庫的單一查詢通常比所擷取每個實體的個別查詢更有效率。</span><span class="sxs-lookup"><span data-stu-id="7046e-137">If you know you need related data for every entity retrieved, eager loading often offers the best performance, because a single query sent to the database is typically more efficient than separate queries for each entity retrieved.</span></span> <span data-ttu-id="7046e-138">例如，在上述範例中，假設每個部門有十個相關的課程。</span><span class="sxs-lookup"><span data-stu-id="7046e-138">For example, in the above examples, suppose that each department has ten related courses.</span></span> <span data-ttu-id="7046e-139">積極式載入範例都只是單一 （聯結） 查詢和單一來回行程到資料庫。</span><span class="sxs-lookup"><span data-stu-id="7046e-139">The eager loading example would result in just a single (join) query and a single round trip to the database.</span></span> <span data-ttu-id="7046e-140">消極式載入和明確式載入範例會同時產生十一個查詢和十一個來回行程到資料庫。</span><span class="sxs-lookup"><span data-stu-id="7046e-140">The lazy loading and explicit loading examples would both result in eleven queries and eleven round trips to the database.</span></span> <span data-ttu-id="7046e-141">當延遲很高時，資料庫的額外來回行程對效能特別不利。</span><span class="sxs-lookup"><span data-stu-id="7046e-141">The extra round trips to the database are especially detrimental to performance when latency is high.</span></span>

<span data-ttu-id="7046e-142">相反地，在某些情況下會更有效率消極式載入。</span><span class="sxs-lookup"><span data-stu-id="7046e-142">On the other hand, in some scenarios lazy loading is more efficient.</span></span> <span data-ttu-id="7046e-143">積極式載入可能會導致非常複雜的聯結產生的 SQL Server 無法有效率地處理。</span><span class="sxs-lookup"><span data-stu-id="7046e-143">Eager loading might cause a very complex join to be generated, which SQL Server can't process efficiently.</span></span> <span data-ttu-id="7046e-144">或者如果您需要存取實體的導覽屬性，只會針對一組實體的子集正在處理，消極式載入可能會比較好，因為積極式載入會擷取比您所需的更多資料。</span><span class="sxs-lookup"><span data-stu-id="7046e-144">Or if you need to access an entity's navigation properties only for a subset of a set of the entities you're processing, lazy loading might perform better because eager loading would retrieve more data than you need.</span></span> <span data-ttu-id="7046e-145">如果效能嚴重不足，最好先測試這兩種方式的效能，才能做出最好的選擇。</span><span class="sxs-lookup"><span data-stu-id="7046e-145">If performance is critical, it's best to test performance both ways in order to make the best choice.</span></span>

<span data-ttu-id="7046e-146">消極式載入可加上遮罩會造成效能問題的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7046e-146">Lazy loading can mask code that causes performance problems.</span></span> <span data-ttu-id="7046e-147">例如，未指定積極式或明確載入，但處理大量的實體，而且每個反覆項目中使用數個導覽屬性的程式碼可能會非常沒有效率 （因為許多往返資料庫）。</span><span class="sxs-lookup"><span data-stu-id="7046e-147">For example, code that doesn't specify eager or explicit loading but processes a high volume of entities and uses several navigation properties in each iteration might be very inefficient (because of many round trips to the database).</span></span> <span data-ttu-id="7046e-148">在開發使用在內部部署 SQL server 中正常執行的應用程式可能會遇到效能問題移到 Azure SQL Database，因為增加的延遲和消極式載入時。</span><span class="sxs-lookup"><span data-stu-id="7046e-148">An application that performs well in development using an on premise SQL server might have performance problems when moved to Azure SQL Database due to the increased latency and lazy loading.</span></span> <span data-ttu-id="7046e-149">分析實際的測試負載的資料庫查詢，可協助您判斷是否適當消極式載入。</span><span class="sxs-lookup"><span data-stu-id="7046e-149">Profiling the database queries with a realistic test load will help you determine if lazy loading is appropriate.</span></span> <span data-ttu-id="7046e-150">如需詳細資訊，請參閱[揭密 Entity Framework 策略：載入相關的資料](https://msdn.microsoft.com/magazine/hh205756.aspx)並[使用 Entity Framework 降低 SQL Azure 的網路延遲](https://msdn.microsoft.com/magazine/gg309181.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7046e-150">For more information see [Demystifying Entity Framework Strategies: Loading Related Data](https://msdn.microsoft.com/magazine/hh205756.aspx) and [Using the Entity Framework to Reduce Network Latency to SQL Azure](https://msdn.microsoft.com/magazine/gg309181.aspx).</span></span>

### <a name="disable-lazy-loading-before-serialization"></a><span data-ttu-id="7046e-151">停用消極式載入，序列化之前</span><span class="sxs-lookup"><span data-stu-id="7046e-151">Disable lazy loading before serialization</span></span>

<span data-ttu-id="7046e-152">如果您離開消極式載入已啟用在序列化期間，您可以得到查詢比您想要更多的資料。</span><span class="sxs-lookup"><span data-stu-id="7046e-152">If you leave lazy loading enabled during serialization, you can end up querying significantly more data than you intended.</span></span> <span data-ttu-id="7046e-153">序列化通常適用於藉由存取類型的執行個體上的每個屬性。</span><span class="sxs-lookup"><span data-stu-id="7046e-153">Serialization generally works by accessing each property on an instance of a type.</span></span> <span data-ttu-id="7046e-154">屬性存取就會觸發消極式載入，並會序列化這些消極式載入的實體。</span><span class="sxs-lookup"><span data-stu-id="7046e-154">Property access triggers lazy loading, and those lazy loaded entities are serialized.</span></span> <span data-ttu-id="7046e-155">序列化程序之後即可存取的消極式載入的實體，而可能造成更多的消極式載入及序列化的每個屬性。</span><span class="sxs-lookup"><span data-stu-id="7046e-155">The serialization process then accesses each property of the lazy-loaded entities, potentially causing even more lazy loading and serialization.</span></span> <span data-ttu-id="7046e-156">若要避免 run-away 鏈結反應，請開啟消極式載入關閉之前序列化實體。</span><span class="sxs-lookup"><span data-stu-id="7046e-156">To prevent this run-away chain reaction, turn lazy loading off before you serialize an entity.</span></span>

<span data-ttu-id="7046e-157">序列化也變得複雜的 Entity Framework 使用時，proxy 類別中所述[進階案例的教學課程](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies)。</span><span class="sxs-lookup"><span data-stu-id="7046e-157">Serialization can also be complicated by the proxy classes that the Entity Framework uses, as explained in the [Advanced Scenarios tutorial](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies).</span></span>

<span data-ttu-id="7046e-158">若要避免發生序列化問題的一個方式是序列化而不是實體物件的資料傳輸物件 (Dto) 中所示[使用 Web API 和 Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="7046e-158">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects, as shown in the [Using Web API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md) tutorial.</span></span>

<span data-ttu-id="7046e-159">如果您未使用 Dto，您可以停用消極式載入，並避免 proxy 問題，依[停用 proxy 建立](https://msdn.microsoft.com/data/jj592886.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7046e-159">If you don't use DTOs, you can disable lazy loading and avoid proxy issues by [disabling proxy creation](https://msdn.microsoft.com/data/jj592886.aspx).</span></span>

<span data-ttu-id="7046e-160">以下是一些其他[如何停用消極式載入](https://msdn.microsoft.com/data/jj574232):</span><span class="sxs-lookup"><span data-stu-id="7046e-160">Here are some other [ways to disable lazy loading](https://msdn.microsoft.com/data/jj574232):</span></span>

- <span data-ttu-id="7046e-161">針對特定的導覽屬性，請省略`virtual`關鍵字宣告的屬性。</span><span class="sxs-lookup"><span data-stu-id="7046e-161">For specific navigation properties, omit the `virtual` keyword when you declare the property.</span></span>
- <span data-ttu-id="7046e-162">對於所有導覽屬性，來設定`LazyLoadingEnabled`至`false`，置於您的內容類別的建構函式中的下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="7046e-162">For all navigation properties, set `LazyLoadingEnabled` to `false`, put the following code in the constructor of your context class:</span></span>

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page"></a><span data-ttu-id="7046e-163">建立 Courses 頁面</span><span class="sxs-lookup"><span data-stu-id="7046e-163">Create a Courses page</span></span>

<span data-ttu-id="7046e-164">`Course`實體包含導覽屬性，其中包含`Department`指派課程的部門實體。</span><span class="sxs-lookup"><span data-stu-id="7046e-164">The `Course` entity includes a navigation property that contains the `Department` entity of the department that the course is assigned to.</span></span> <span data-ttu-id="7046e-165">若要在課程清單中顯示所指派部門的名稱，您需要取得`Name`屬性從`Department`中的實體`Course.Department`導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="7046e-165">To display the name of the assigned department in a list of courses, you need to get the `Name` property from the `Department` entity that is in the `Course.Department` navigation property.</span></span>

<span data-ttu-id="7046e-166">建立的控制器命名為`CourseController`(不 CoursesController) 的`Course`實體類型，使用的相同選項**使用 MVC 5 控制器與檢視，Entity Framework**您先前為的框架`Student`控制器：</span><span class="sxs-lookup"><span data-stu-id="7046e-166">Create a controller named `CourseController` (not CoursesController) for the `Course` entity type, using the same options for the **MVC 5 Controller with views, using Entity Framework** scaffolder that you did earlier for the `Student` controller:</span></span>

| <span data-ttu-id="7046e-167">設定</span><span class="sxs-lookup"><span data-stu-id="7046e-167">Setting</span></span> | <span data-ttu-id="7046e-168">值</span><span class="sxs-lookup"><span data-stu-id="7046e-168">Value</span></span> |
| ------- | ----- |
| <span data-ttu-id="7046e-169">模型類別</span><span class="sxs-lookup"><span data-stu-id="7046e-169">Model class</span></span> | <span data-ttu-id="7046e-170">選取 **課程 (ContosoUniversity.Models)**。</span><span class="sxs-lookup"><span data-stu-id="7046e-170">Select **Course (ContosoUniversity.Models)**.</span></span> |
| <span data-ttu-id="7046e-171">資料內容類別</span><span class="sxs-lookup"><span data-stu-id="7046e-171">Data context class</span></span> | <span data-ttu-id="7046e-172">選取  **SchoolContext (ContosoUniversity.DAL)**。</span><span class="sxs-lookup"><span data-stu-id="7046e-172">Select **SchoolContext (ContosoUniversity.DAL)**.</span></span> |
| <span data-ttu-id="7046e-173">控制器名稱</span><span class="sxs-lookup"><span data-stu-id="7046e-173">Controller name</span></span> | <span data-ttu-id="7046e-174">請輸入*CourseController*。</span><span class="sxs-lookup"><span data-stu-id="7046e-174">Enter *CourseController*.</span></span> <span data-ttu-id="7046e-175">同樣地，未*CoursesController*具有*s*。</span><span class="sxs-lookup"><span data-stu-id="7046e-175">Again, not *CoursesController* with an *s*.</span></span> <span data-ttu-id="7046e-176">當您選取**課程 (ContosoUniversity.Models)**，則**控制站名稱**自動填入值。</span><span class="sxs-lookup"><span data-stu-id="7046e-176">When you selected **Course (ContosoUniversity.Models)**, the **Controller name** value was automatically populated.</span></span> <span data-ttu-id="7046e-177">您不必變更值。</span><span class="sxs-lookup"><span data-stu-id="7046e-177">You have to change the value.</span></span> |

<span data-ttu-id="7046e-178">保留其他預設值，然後新增控制器。</span><span class="sxs-lookup"><span data-stu-id="7046e-178">Leave the other default values and add the controller.</span></span>

<span data-ttu-id="7046e-179">開啟*Controllers\CourseController.cs*並查看`Index`方法：</span><span class="sxs-lookup"><span data-stu-id="7046e-179">Open *Controllers\CourseController.cs* and look at the `Index` method:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="7046e-180">自動 Scaffolding 已使用 `Include` 方法，針對 `Department` 導覽屬性指定積極式載入。</span><span class="sxs-lookup"><span data-stu-id="7046e-180">The automatic scaffolding has specified eager loading for the `Department` navigation property by using the `Include` method.</span></span>

<span data-ttu-id="7046e-181">開啟*Views\Course\Index.cshtml*並以下列程式碼取代範本程式碼。</span><span class="sxs-lookup"><span data-stu-id="7046e-181">Open *Views\Course\Index.cshtml* and replace the template code with the following code.</span></span> <span data-ttu-id="7046e-182">所做的變更已醒目提示：</span><span class="sxs-lookup"><span data-stu-id="7046e-182">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

<span data-ttu-id="7046e-183">您已對包含 Scaffold 的程式碼進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="7046e-183">You've made the following changes to the scaffolded code:</span></span>

- <span data-ttu-id="7046e-184">變更從標題**Index**要**課程**。</span><span class="sxs-lookup"><span data-stu-id="7046e-184">Changed the heading from **Index** to **Courses**.</span></span>
- <span data-ttu-id="7046e-185">新增顯示 `CourseID` 屬性值的 [編號] 資料行。</span><span class="sxs-lookup"><span data-stu-id="7046e-185">Added a **Number** column that shows the `CourseID` property value.</span></span> <span data-ttu-id="7046e-186">根據預設，主索引鍵不會進行 scaffold 因為它們通常是使用者沒有任何意義。</span><span class="sxs-lookup"><span data-stu-id="7046e-186">By default, primary keys aren't scaffolded because normally they are meaningless to end users.</span></span> <span data-ttu-id="7046e-187">不過，在此情況下主索引鍵有意義，因此您想要顯示它。</span><span class="sxs-lookup"><span data-stu-id="7046e-187">However, in this case the primary key is meaningful and you want to show it.</span></span>
- <span data-ttu-id="7046e-188">移動**部門**右側的資料行並變更其標題。</span><span class="sxs-lookup"><span data-stu-id="7046e-188">Moved the **Department** column to the right side and changed its heading.</span></span> <span data-ttu-id="7046e-189">正確選擇要顯示的框架`Name`屬性從`Department`實體，但這裡的 [課程] 頁面的資料行標題應該**部門**而非**名稱**。</span><span class="sxs-lookup"><span data-stu-id="7046e-189">The scaffolder correctly chose to display the `Name` property from the `Department` entity, but here in the Course page the column heading should be **Department** rather than **Name**.</span></span>

<span data-ttu-id="7046e-190">請注意，[部門] 欄中，針對包含 scaffold 的程式碼會顯示`Name`的屬性`Department`載入的實體`Department`導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="7046e-190">Notice that for the Department column, the scaffolded code displays the `Name` property of the `Department` entity that's loaded into the `Department` navigation property:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="7046e-191">執行網頁 (選取**課程**的 Contoso 大學首頁上的索引標籤) 以查看含有部門名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="7046e-191">Run the page (select the **Courses** tab on the Contoso University home page) to see the list with department names.</span></span>

## <a name="create-an-instructors-page"></a><span data-ttu-id="7046e-192">建立 Instructors 頁面</span><span class="sxs-lookup"><span data-stu-id="7046e-192">Create an Instructors page</span></span>

<span data-ttu-id="7046e-193">在本節中，您會建立控制器並檢視`Instructor`實體以顯示 Instructors 頁面。</span><span class="sxs-lookup"><span data-stu-id="7046e-193">In this section you'll create a controller and view for the `Instructor` entity in order to display the Instructors page.</span></span> <span data-ttu-id="7046e-194">此頁面將以下列方式讀取和顯示相關資料：</span><span class="sxs-lookup"><span data-stu-id="7046e-194">This page reads and displays related data in the following ways:</span></span>

- <span data-ttu-id="7046e-195">講師清單會顯示相關的資料，從`OfficeAssignment`實體。</span><span class="sxs-lookup"><span data-stu-id="7046e-195">The list of instructors displays related data from the `OfficeAssignment` entity.</span></span> <span data-ttu-id="7046e-196">`Instructor` 與 `OfficeAssignment` 實體具有一對零或一關聯性。</span><span class="sxs-lookup"><span data-stu-id="7046e-196">The `Instructor` and `OfficeAssignment` entities are in a one-to-zero-or-one relationship.</span></span> <span data-ttu-id="7046e-197">您將使用積極式載入`OfficeAssignment`實體。</span><span class="sxs-lookup"><span data-stu-id="7046e-197">You'll use eager loading for the `OfficeAssignment` entities.</span></span> <span data-ttu-id="7046e-198">如上所述，當您需要主要資料表中所有擷取資料列的相關資料時，積極式載入通常更有效率。</span><span class="sxs-lookup"><span data-stu-id="7046e-198">As explained earlier, eager loading is typically more efficient when you need the related data for all retrieved rows of the primary table.</span></span> <span data-ttu-id="7046e-199">在此情況下，您可能想要顯示所有已呈現講師的辦公室指派。</span><span class="sxs-lookup"><span data-stu-id="7046e-199">In this case, you want to display office assignments for all displayed instructors.</span></span>
- <span data-ttu-id="7046e-200">當使用者選取講師，相關`Course`實體便會顯示。</span><span class="sxs-lookup"><span data-stu-id="7046e-200">When the user selects an instructor, related `Course` entities are displayed.</span></span> <span data-ttu-id="7046e-201">`Instructor` 與 `Course` 實體具有多對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="7046e-201">The `Instructor` and `Course` entities are in a many-to-many relationship.</span></span> <span data-ttu-id="7046e-202">您將使用積極式載入`Course`實體和其相關`Department`實體。</span><span class="sxs-lookup"><span data-stu-id="7046e-202">You'll use eager loading for the `Course` entities and their related `Department` entities.</span></span> <span data-ttu-id="7046e-203">在此情況下，消極式載入可能會更有效率因為您需要只會針對所選講師的課程。</span><span class="sxs-lookup"><span data-stu-id="7046e-203">In this case, lazy loading might be more efficient because you need courses only for the selected instructor.</span></span> <span data-ttu-id="7046e-204">不過，這個範例會示範如何在本身處於導覽屬性內的實體中，針對導覽屬性使用積極式載入。</span><span class="sxs-lookup"><span data-stu-id="7046e-204">However, this example shows how to use eager loading for navigation properties within entities that are themselves in navigation properties.</span></span>
- <span data-ttu-id="7046e-205">當使用者選取課程時，相關資料`Enrollments`顯示實體集。</span><span class="sxs-lookup"><span data-stu-id="7046e-205">When the user selects a course, related data from the `Enrollments` entity set is displayed.</span></span> <span data-ttu-id="7046e-206">`Course` 與 `Enrollment` 實體具有一對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="7046e-206">The `Course` and `Enrollment` entities are in a one-to-many relationship.</span></span> <span data-ttu-id="7046e-207">您將新增的明確式載入`Enrollment`實體和其相關`Student`實體。</span><span class="sxs-lookup"><span data-stu-id="7046e-207">You'll add explicit loading for `Enrollment` entities and their related `Student` entities.</span></span> <span data-ttu-id="7046e-208">（明確式載入不必要的因為已啟用消極式載入，但這會顯示如何執行明確式載入函式）。</span><span class="sxs-lookup"><span data-stu-id="7046e-208">(Explicit loading isn't necessary because lazy loading is enabled, but this shows how to do explicit loading.)</span></span>

### <a name="create-a-view-model-for-the-instructor-index-view"></a><span data-ttu-id="7046e-209">建立 Instructor [索引] 檢視的檢視模型</span><span class="sxs-lookup"><span data-stu-id="7046e-209">Create a View Model for the Instructor Index View</span></span>

<span data-ttu-id="7046e-210">Instructors 頁面會顯示三個不同的資料表。</span><span class="sxs-lookup"><span data-stu-id="7046e-210">The Instructors page shows three different tables.</span></span> <span data-ttu-id="7046e-211">因此，您將建立包含三個屬性的檢視模型，每個保留其中一個資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="7046e-211">Therefore, you'll create a view model that includes three properties, each holding the data for one of the tables.</span></span>

<span data-ttu-id="7046e-212">在  *Viewmodel*資料夾中，建立*InstructorIndexData.cs*並以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="7046e-212">In the *ViewModels* folder, create *InstructorIndexData.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a><span data-ttu-id="7046e-213">建立 Instructor 控制器和檢視</span><span class="sxs-lookup"><span data-stu-id="7046e-213">Create the Instructor Controller and Views</span></span>

<span data-ttu-id="7046e-214">建立`InstructorController`(不 InstructorsController) 使用 EF 讀取/寫入動作的控制器：</span><span class="sxs-lookup"><span data-stu-id="7046e-214">Create an `InstructorController` (not InstructorsController) controller with EF read/write action:</span></span>

| <span data-ttu-id="7046e-215">設定</span><span class="sxs-lookup"><span data-stu-id="7046e-215">Setting</span></span> | <span data-ttu-id="7046e-216">值</span><span class="sxs-lookup"><span data-stu-id="7046e-216">Value</span></span> |
| ------- | ----- |
| <span data-ttu-id="7046e-217">模型類別</span><span class="sxs-lookup"><span data-stu-id="7046e-217">Model class</span></span> | <span data-ttu-id="7046e-218">選取 **講師 (ContosoUniversity.Models)**。</span><span class="sxs-lookup"><span data-stu-id="7046e-218">Select **Instructor (ContosoUniversity.Models)**.</span></span> |
| <span data-ttu-id="7046e-219">資料內容類別</span><span class="sxs-lookup"><span data-stu-id="7046e-219">Data context class</span></span> | <span data-ttu-id="7046e-220">選取  **SchoolContext (ContosoUniversity.DAL)**。</span><span class="sxs-lookup"><span data-stu-id="7046e-220">Select **SchoolContext (ContosoUniversity.DAL)**.</span></span> |
| <span data-ttu-id="7046e-221">控制器名稱</span><span class="sxs-lookup"><span data-stu-id="7046e-221">Controller name</span></span> | <span data-ttu-id="7046e-222">請輸入*InstructorController*。</span><span class="sxs-lookup"><span data-stu-id="7046e-222">Enter *InstructorController*.</span></span> <span data-ttu-id="7046e-223">同樣地，未*InstructorsController*具有*s*。</span><span class="sxs-lookup"><span data-stu-id="7046e-223">Again, not *InstructorsController* with an *s*.</span></span> <span data-ttu-id="7046e-224">當您選取**課程 (ContosoUniversity.Models)**，則**控制站名稱**自動填入值。</span><span class="sxs-lookup"><span data-stu-id="7046e-224">When you selected **Course (ContosoUniversity.Models)**, the **Controller name** value was automatically populated.</span></span> <span data-ttu-id="7046e-225">您不必變更值。</span><span class="sxs-lookup"><span data-stu-id="7046e-225">You have to change the value.</span></span> |

<span data-ttu-id="7046e-226">保留其他預設值，然後新增控制器。</span><span class="sxs-lookup"><span data-stu-id="7046e-226">Leave the other default values and add the controller.</span></span>

<span data-ttu-id="7046e-227">開啟*Controllers\InstructorController.cs*並加入`using`陳述式`ViewModels`命名空間：</span><span class="sxs-lookup"><span data-stu-id="7046e-227">Open *Controllers\InstructorController.cs* and add a `using` statement for the `ViewModels` namespace:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="7046e-228">中的 scaffold 程式碼`Index`方法指定積極式載入，僅適用於`OfficeAssignment`導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="7046e-228">The scaffolded code in the `Index` method specifies eager loading only for the `OfficeAssignment` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="7046e-229">取代`Index`方法具有下列的程式碼，以載入其他相關資料，並將它放在檢視模型中：</span><span class="sxs-lookup"><span data-stu-id="7046e-229">Replace the `Index` method with the following code to load additional related data and put it in the view model:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="7046e-230">方法會接受選擇性的路由資料 (`id`) 和查詢字串參數 (`courseID`)，提供所選取的講師和所選的課程的識別碼值，並將所有必要的資料傳遞至檢視。</span><span class="sxs-lookup"><span data-stu-id="7046e-230">The method accepts optional route data (`id`) and a query string parameter (`courseID`) that provide the ID values of the selected instructor and selected course, and passes all of the required data to the view.</span></span> <span data-ttu-id="7046e-231">這些參數由頁面上的**選取**超連結提供。</span><span class="sxs-lookup"><span data-stu-id="7046e-231">The parameters are provided by the **Select** hyperlinks on the page.</span></span>

<span data-ttu-id="7046e-232">此程式碼是從建立檢視模型的執行個體，並將其置於講師清單開始。</span><span class="sxs-lookup"><span data-stu-id="7046e-232">The code begins by creating an instance of the view model and putting in it the list of instructors.</span></span> <span data-ttu-id="7046e-233">程式碼會指定積極式載入`Instructor.OfficeAssignment`而`Instructor.Courses`導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="7046e-233">The code specifies eager loading for the `Instructor.OfficeAssignment` and the `Instructor.Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

<span data-ttu-id="7046e-234">第二個`Include`方法載入課程，並針對每個載入的課程會積極式載入`Course.Department`導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="7046e-234">The second `Include` method loads Courses, and for each Course that is loaded it does eager loading for the `Course.Department` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="7046e-235">如先前所述，不需要積極式載入，但是為了改善效能。</span><span class="sxs-lookup"><span data-stu-id="7046e-235">As mentioned previously, eager loading is not required but is done to improve performance.</span></span> <span data-ttu-id="7046e-236">由於檢視一律需要`OfficeAssignment`實體，它是擷取該相同的查詢更有效率。</span><span class="sxs-lookup"><span data-stu-id="7046e-236">Since the view always requires the `OfficeAssignment` entity, it's more efficient to fetch that in the same query.</span></span> <span data-ttu-id="7046e-237">`Course` 因此積極式載入是優於消極式載入，而不需要選取比更常顯示頁面時，才在網頁上，選取講師時，所需的實體。</span><span class="sxs-lookup"><span data-stu-id="7046e-237">`Course` entities are required when an instructor is selected in the web page, so eager loading is better than lazy loading only if the page is displayed more often with a course selected than without.</span></span>

<span data-ttu-id="7046e-238">如果選取的講師識別碼，所選取的講師會從檢視模型中的講師清單中。</span><span class="sxs-lookup"><span data-stu-id="7046e-238">If an instructor ID was selected, the selected instructor is retrieved from the list of instructors in the view model.</span></span> <span data-ttu-id="7046e-239">檢視模型`Courses`屬性然後充滿`Course`實體從該講師`Courses`導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="7046e-239">The view model's `Courses` property is then loaded with the `Course` entities from that instructor's `Courses` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="7046e-240">`Where`方法會傳回集合，但準則在此情況下傳遞至該方法的結果中只有一個`Instructor`所傳回的實體。</span><span class="sxs-lookup"><span data-stu-id="7046e-240">The `Where` method returns a collection, but in this case the criteria passed to that method result in only a single `Instructor` entity being returned.</span></span> <span data-ttu-id="7046e-241">`Single`方法會將集合轉換成單一`Instructor`可讓您存取與該實體的實體`Courses`屬性。</span><span class="sxs-lookup"><span data-stu-id="7046e-241">The `Single` method converts the collection into a single `Instructor` entity, which gives you access to that entity's `Courses` property.</span></span>

<span data-ttu-id="7046e-242">您使用[單一](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx)集合，當您知道集合上的方法必須只有一個項目。</span><span class="sxs-lookup"><span data-stu-id="7046e-242">You use the [Single](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) method on a collection when you know the collection will have only one item.</span></span> <span data-ttu-id="7046e-243">`Single`方法擲回例外狀況，如果是空的集合傳遞給它，或是否有多個項目。</span><span class="sxs-lookup"><span data-stu-id="7046e-243">The `Single` method throws an exception if the collection passed to it is empty or if there's more than one item.</span></span> <span data-ttu-id="7046e-244">替代方法是[SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)，它會傳回預設值 (`null`在此情況下) 如果集合是空的。</span><span class="sxs-lookup"><span data-stu-id="7046e-244">An alternative is [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx), which returns a default value (`null` in this case) if the collection is empty.</span></span> <span data-ttu-id="7046e-245">不過，在此情況下，仍然會造成例外狀況 (由於嘗試尋找`Courses`屬性上的`null`參考)，和例外狀況訊息會不太清楚地指出問題的原因。</span><span class="sxs-lookup"><span data-stu-id="7046e-245">However, in this case that would still result in an exception (from trying to find a `Courses` property on a `null` reference), and the exception message would less clearly indicate the cause of the problem.</span></span> <span data-ttu-id="7046e-246">當您呼叫`Single`方法中，您也可以傳入`Where`條件，而不是呼叫`Where`方法分開：</span><span class="sxs-lookup"><span data-stu-id="7046e-246">When you call the `Single` method, you can also pass in the `Where` condition instead of calling the `Where` method separately:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="7046e-247">而非：</span><span class="sxs-lookup"><span data-stu-id="7046e-247">Instead of:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="7046e-248">接下來，如果已選取課程，則會從檢視模型的課程清單中擷取選取的課程。</span><span class="sxs-lookup"><span data-stu-id="7046e-248">Next, if a course was selected, the selected course is retrieved from the list of courses in the view model.</span></span> <span data-ttu-id="7046e-249">然後，檢視模型的`Enrollments`屬性已載入`Enrollment`實體從該課程`Enrollments`導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="7046e-249">Then the view model's `Enrollments` property is loaded with the `Enrollment` entities from that course's `Enrollments` navigation property.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a><span data-ttu-id="7046e-250">修改 Instructor [索引] 檢視</span><span class="sxs-lookup"><span data-stu-id="7046e-250">Modify the Instructor Index View</span></span>

<span data-ttu-id="7046e-251">在  *Views\Instructor\Index.cshtml*，以下列程式碼取代範本程式碼。</span><span class="sxs-lookup"><span data-stu-id="7046e-251">In *Views\Instructor\Index.cshtml*, replace the template code with the following code.</span></span> <span data-ttu-id="7046e-252">所做的變更已醒目提示：</span><span class="sxs-lookup"><span data-stu-id="7046e-252">The changes are highlighted:</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

<span data-ttu-id="7046e-253">您已對現有程式碼進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="7046e-253">You've made the following changes to the existing code:</span></span>

- <span data-ttu-id="7046e-254">已將模型類別變更為 `InstructorIndexData`。</span><span class="sxs-lookup"><span data-stu-id="7046e-254">Changed the model class to `InstructorIndexData`.</span></span>
- <span data-ttu-id="7046e-255">已將頁面標題從**索引**變更為**講師**。</span><span class="sxs-lookup"><span data-stu-id="7046e-255">Changed the page title from **Index** to **Instructors**.</span></span>
- <span data-ttu-id="7046e-256">新增**辦公室**會顯示的資料行`item.OfficeAssignment.Location`只有當`item.OfficeAssignment`不是 null。</span><span class="sxs-lookup"><span data-stu-id="7046e-256">Added an **Office** column that displays `item.OfficeAssignment.Location` only if `item.OfficeAssignment` is not null.</span></span> <span data-ttu-id="7046e-257">(因為這是一對零-或-一關聯性時，可能不會有相關`OfficeAssignment`實體。)</span><span class="sxs-lookup"><span data-stu-id="7046e-257">(Because this is a one-to-zero-or-one relationship, there might not be a related `OfficeAssignment` entity.)</span></span>

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- <span data-ttu-id="7046e-258">新增程式碼，將會以動態方式新增`class="success"`至`tr`所選取講師的項目。</span><span class="sxs-lookup"><span data-stu-id="7046e-258">Added code that will dynamically add `class="success"` to the `tr` element of the selected instructor.</span></span> <span data-ttu-id="7046e-259">這會將選取的資料列使用的背景色彩[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)類別。</span><span class="sxs-lookup"><span data-stu-id="7046e-259">This sets a background color for the selected row using a [Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap) class.</span></span>

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- <span data-ttu-id="7046e-260">已新增`ActionLink`標示**選取**正前方中每個資料列的其他連結，這會讓選取的講師識別碼傳送至`Index`方法。</span><span class="sxs-lookup"><span data-stu-id="7046e-260">Added a new `ActionLink` labeled **Select** immediately before the other links in each row, which causes the selected instructor ID to be sent to the `Index` method.</span></span>

<span data-ttu-id="7046e-261">執行應用程式，然後選取**講師** 索引標籤。此頁面會顯示`Location`屬性的相關`OfficeAssignment`實體和空的資料表資料格時有無相關`OfficeAssignment`實體。</span><span class="sxs-lookup"><span data-stu-id="7046e-261">Run the application and select the **Instructors** tab. The page displays the `Location` property of related `OfficeAssignment` entities and an empty table cell when there's no related `OfficeAssignment` entity.</span></span>

<span data-ttu-id="7046e-262">在  *Views\Instructor\Index.cshtml*檔案之後則會在結尾,`table`項目 （在檔案結尾），新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="7046e-262">In the *Views\Instructor\Index.cshtml* file, after the closing `table` element (at the end of the file), add the following code.</span></span> <span data-ttu-id="7046e-263">當選取講師時，此程式碼會顯示與講師相關的課程。</span><span class="sxs-lookup"><span data-stu-id="7046e-263">This code displays a list of courses related to an instructor when an instructor is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

<span data-ttu-id="7046e-264">此程式碼會讀取檢視模型的 `Courses` 屬性以顯示課程清單。</span><span class="sxs-lookup"><span data-stu-id="7046e-264">This code reads the `Courses` property of the view model to display a list of courses.</span></span> <span data-ttu-id="7046e-265">它也會提供`Select`超連結，會傳送至所選取課程的識別碼`Index`動作方法。</span><span class="sxs-lookup"><span data-stu-id="7046e-265">It also provides a `Select` hyperlink that sends the ID of the selected course to the `Index` action method.</span></span>

<span data-ttu-id="7046e-266">執行網頁，然後選取講師。</span><span class="sxs-lookup"><span data-stu-id="7046e-266">Run the page and select an instructor.</span></span> <span data-ttu-id="7046e-267">現在您會看到一個方格，其中顯示指派給所選取講師的課程，而且在每個課程中，您可以看到指派的部門名稱。</span><span class="sxs-lookup"><span data-stu-id="7046e-267">Now you see a grid that displays courses assigned to the selected instructor, and for each course you see the name of the assigned department.</span></span>

<span data-ttu-id="7046e-268">在您剛才新增的程式碼區塊之後，新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="7046e-268">After the code block you just added, add the following code.</span></span> <span data-ttu-id="7046e-269">這會在選取課程時，顯示已註冊該課程的學生清單。</span><span class="sxs-lookup"><span data-stu-id="7046e-269">This displays a list of the students who are enrolled in a course when that course is selected.</span></span>

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

<span data-ttu-id="7046e-270">此程式碼會讀取`Enrollments`屬性以顯示學生的清單檢視模型的註冊過程中。</span><span class="sxs-lookup"><span data-stu-id="7046e-270">This code reads the `Enrollments` property of the view model in order to display a list of students enrolled in the course.</span></span>

<span data-ttu-id="7046e-271">執行網頁，然後選取講師。</span><span class="sxs-lookup"><span data-stu-id="7046e-271">Run the page and select an instructor.</span></span> <span data-ttu-id="7046e-272">接著選取課程，以查看已註冊學生和其年級的清單。</span><span class="sxs-lookup"><span data-stu-id="7046e-272">Then select a course to see the list of enrolled students and their grades.</span></span>

### <a name="adding-explicit-loading"></a><span data-ttu-id="7046e-273">新增明確式載入</span><span class="sxs-lookup"><span data-stu-id="7046e-273">Adding Explicit Loading</span></span>

<span data-ttu-id="7046e-274">開啟*InstructorController.cs*並查看如何`Index`方法會取得所選取課程的註冊清單：</span><span class="sxs-lookup"><span data-stu-id="7046e-274">Open *InstructorController.cs* and look at how the `Index` method gets the list of enrollments for a selected course:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="7046e-275">當您擷取講師清單時，您會指定積極式載入`Courses`導覽屬性和`Department`屬性的每個課程。</span><span class="sxs-lookup"><span data-stu-id="7046e-275">When you retrieved the list of instructors, you specified eager loading for the `Courses` navigation property and for the `Department` property of each course.</span></span> <span data-ttu-id="7046e-276">然後您將放`Courses`在檢視模型中，而您正在存取的集合`Enrollments`從該集合中的某個實體的導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="7046e-276">Then you put the `Courses` collection in the view model, and now you're accessing the `Enrollments` navigation property from one entity in that collection.</span></span> <span data-ttu-id="7046e-277">因為您沒有指定積極式載入`Course.Enrollments`導覽屬性，該屬性的資料出現在頁面中，由於消極式載入。</span><span class="sxs-lookup"><span data-stu-id="7046e-277">Because you didn't specify eager loading for the `Course.Enrollments` navigation property, the data from that property is appearing in the page as a result of lazy loading.</span></span>

<span data-ttu-id="7046e-278">如果您不需要變更任何其他方式中的程式碼停用消極式載入`Enrollments`屬性將會是 null，不論課程實際上有多少的註冊項目。</span><span class="sxs-lookup"><span data-stu-id="7046e-278">If you disabled lazy loading without changing the code in any other way, the `Enrollments` property would be null regardless of how many enrollments the course actually had.</span></span> <span data-ttu-id="7046e-279">在此情況下，載入`Enrollments`屬性，您必須指定積極式載入或明確式載入。</span><span class="sxs-lookup"><span data-stu-id="7046e-279">In that case, to load the `Enrollments` property, you'd have to specify either eager loading or explicit loading.</span></span> <span data-ttu-id="7046e-280">您已經看到如何進行積極式載入。</span><span class="sxs-lookup"><span data-stu-id="7046e-280">You've already seen how to do eager loading.</span></span> <span data-ttu-id="7046e-281">若要查看的明確式載入範例，取代`Index`方法，明確地載入為下列程式碼`Enrollments`屬性。</span><span class="sxs-lookup"><span data-stu-id="7046e-281">In order to see an example of explicit loading, replace the `Index` method with the following code, which explicitly loads the `Enrollments` property.</span></span> <span data-ttu-id="7046e-282">變更的程式碼會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="7046e-282">The code changed are highlighted.</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

<span data-ttu-id="7046e-283">取得所選之後`Course`實體，新的程式碼，明確地載入該課程`Enrollments`導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="7046e-283">After getting the selected `Course` entity, the new code explicitly loads that course's `Enrollments` navigation property:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

<span data-ttu-id="7046e-284">然後它會明確地載入每個`Enrollment`實體的相關`Student`實體：</span><span class="sxs-lookup"><span data-stu-id="7046e-284">Then it explicitly loads each `Enrollment` entity's related `Student` entity:</span></span>

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

<span data-ttu-id="7046e-285">請注意，您使用`Collection`方法來載入集合屬性，但會保留一個實體的屬性，您使用`Reference`方法。</span><span class="sxs-lookup"><span data-stu-id="7046e-285">Notice that you use the `Collection` method to load a collection property, but for a property that holds just one entity, you use the `Reference` method.</span></span>

<span data-ttu-id="7046e-286">立即執行 Instructor 索引 頁面，您會看到任何差異，在頁面上，顯示的內容，雖然您已變更資料擷取的方式。</span><span class="sxs-lookup"><span data-stu-id="7046e-286">Run the Instructor Index page now and you'll see no difference in what's displayed on the page, although you've changed how the data is retrieved.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="7046e-287">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="7046e-287">Get the code</span></span>

[<span data-ttu-id="7046e-288">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="7046e-288">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="7046e-289">其他資源</span><span class="sxs-lookup"><span data-stu-id="7046e-289">Additional resources</span></span>

<span data-ttu-id="7046e-290">其他 Entity Framework 資源連結可在[ASP.NET 資料存取-建議資源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="7046e-290">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7046e-291">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7046e-291">Next steps</span></span>

<span data-ttu-id="7046e-292">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="7046e-292">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7046e-293">了解如何載入相關資料</span><span class="sxs-lookup"><span data-stu-id="7046e-293">Learned how to load related data</span></span>
> * <span data-ttu-id="7046e-294">建立 Courses 頁面</span><span class="sxs-lookup"><span data-stu-id="7046e-294">Created a Courses page</span></span>
> * <span data-ttu-id="7046e-295">建立 Instructors 頁面</span><span class="sxs-lookup"><span data-stu-id="7046e-295">Created an Instructors page</span></span>

<span data-ttu-id="7046e-296">若要了解如何更新相關資料，請前往下一篇文章。</span><span class="sxs-lookup"><span data-stu-id="7046e-296">Advance to the next article to learn how to update related data.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7046e-297">更新相關資料</span><span class="sxs-lookup"><span data-stu-id="7046e-297">Update related data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)