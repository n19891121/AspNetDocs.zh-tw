---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: 適用于 MVC Web 應用程式的 Advanced Entity Framework 案例 (10/10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: 4b49ae0bee2a5ceb41dbf040dc6ea7c8d2d0dea2
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2021
ms.locfileid: "99985111"
---
# <a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a><span data-ttu-id="8f864-103">適用于 MVC Web 應用程式的 Advanced Entity Framework 案例 (10/10) </span><span class="sxs-lookup"><span data-stu-id="8f864-103">Advanced Entity Framework Scenarios for an MVC Web Application (10 of 10)</span></span>

<span data-ttu-id="8f864-104">由 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8f864-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="8f864-105">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f864-105">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="8f864-106">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="8f864-106">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="8f864-107">如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。</span><span class="sxs-lookup"><span data-stu-id="8f864-107">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="8f864-108">您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="8f864-108">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="8f864-109">針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。</span><span class="sxs-lookup"><span data-stu-id="8f864-109">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="8f864-110">在上一個教學課程中，您已實作為存放庫和工作單元模式。</span><span class="sxs-lookup"><span data-stu-id="8f864-110">In the previous tutorial you implemented the repository and unit of work patterns.</span></span> <span data-ttu-id="8f864-111">本教學課程涵蓋下列主題：</span><span class="sxs-lookup"><span data-stu-id="8f864-111">This tutorial covers the following topics:</span></span>

- <span data-ttu-id="8f864-112">執行原始 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="8f864-112">Performing raw SQL queries.</span></span>
- <span data-ttu-id="8f864-113">執行無追蹤查詢。</span><span class="sxs-lookup"><span data-stu-id="8f864-113">Performing no-tracking queries.</span></span>
- <span data-ttu-id="8f864-114">檢查傳送至資料庫的查詢。</span><span class="sxs-lookup"><span data-stu-id="8f864-114">Examining queries sent to the database.</span></span>
- <span data-ttu-id="8f864-115">使用 proxy 類別。</span><span class="sxs-lookup"><span data-stu-id="8f864-115">Working with proxy classes.</span></span>
- <span data-ttu-id="8f864-116">停用自動偵測變更。</span><span class="sxs-lookup"><span data-stu-id="8f864-116">Disabling automatic detection of changes.</span></span>
- <span data-ttu-id="8f864-117">在儲存變更時停用驗證。</span><span class="sxs-lookup"><span data-stu-id="8f864-117">Disabling validation when saving changes.</span></span>
- [<span data-ttu-id="8f864-118">錯誤和解決辦法</span><span class="sxs-lookup"><span data-stu-id="8f864-118">Errors and Work Arounds</span></span>](#errors)

<span data-ttu-id="8f864-119">在這些主題中，您將會使用已建立的頁面。</span><span class="sxs-lookup"><span data-stu-id="8f864-119">For most of these topics, you'll work with pages that you already created.</span></span> <span data-ttu-id="8f864-120">若要使用原始 SQL 進行大量更新，您將會建立新的頁面，以更新資料庫中所有課程的信用額度數目：</span><span class="sxs-lookup"><span data-stu-id="8f864-120">To use raw SQL to do bulk updates you'll create a new page that updates the number of credits of all courses in the database:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="8f864-122">若要使用無追蹤查詢，您可以將新的驗證邏輯新增至 [部門編輯] 頁面：</span><span class="sxs-lookup"><span data-stu-id="8f864-122">And to use a no-tracking query you'll add new validation logic to the Department Edit page:</span></span>

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a><span data-ttu-id="8f864-124">執行原始 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="8f864-124">Performing Raw SQL Queries</span></span>

<span data-ttu-id="8f864-125">Entity Framework Code First API 包含可讓您將 SQL 命令直接傳遞至資料庫的方法。</span><span class="sxs-lookup"><span data-stu-id="8f864-125">The Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="8f864-126">下列選項可供您選擇：</span><span class="sxs-lookup"><span data-stu-id="8f864-126">You have the following options:</span></span>

- <span data-ttu-id="8f864-127">針對傳回實體類型的查詢使用 `DbSet.SqlQuery` 方法。</span><span class="sxs-lookup"><span data-stu-id="8f864-127">Use the `DbSet.SqlQuery` method for queries that return entity types.</span></span> <span data-ttu-id="8f864-128">傳回的物件必須是物件所預期的型別 `DbSet` ，而且除非您關閉追蹤功能，否則資料庫內容會自動追蹤這些物件。</span><span class="sxs-lookup"><span data-stu-id="8f864-128">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you turn tracking off.</span></span> <span data-ttu-id="8f864-129"> (請參閱下一節中的 `AsNoTracking` 方法。 ) </span><span class="sxs-lookup"><span data-stu-id="8f864-129">(See the following section about the `AsNoTracking` method.)</span></span>
- <span data-ttu-id="8f864-130">針對傳回非 `Database.SqlQuery` 實體之類型的查詢，請使用方法。</span><span class="sxs-lookup"><span data-stu-id="8f864-130">Use the `Database.SqlQuery` method for queries that return types that aren't entities.</span></span> <span data-ttu-id="8f864-131">即使您使用這個方法來擷取實體類型，資料庫內容也不會追蹤傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="8f864-131">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>
- <span data-ttu-id="8f864-132">針對非查詢命令使用 [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) 。</span><span class="sxs-lookup"><span data-stu-id="8f864-132">Use the [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) for non-query commands.</span></span>

<span data-ttu-id="8f864-133">使用 Entity Framework 的優點之一，是它可避免將程式碼繫結至太接近儲存資料之特定方法的位置。</span><span class="sxs-lookup"><span data-stu-id="8f864-133">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="8f864-134">它可透過產生 SQL 查詢和命令來達成此目的，同時這也可讓您不必自行撰寫。</span><span class="sxs-lookup"><span data-stu-id="8f864-134">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="8f864-135">但是當您需要執行手動建立的特定 SQL 查詢時，有一些例外狀況，而這些方法可以讓您處理這類例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8f864-135">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created, and these methods make it possible for you to handle such exceptions.</span></span>

<span data-ttu-id="8f864-136">如同在 Web 應用程式中執行 SQL 命令一樣，您必須採取一些預防措施，以保護您的網站免於遭受 SQL 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="8f864-136">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="8f864-137">執行這項操作的方法之一是使用參數化查詢，以確定網頁所提交的字串無法解譯為 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="8f864-137">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="8f864-138">在本教學課程中，您會在將使用者輸入整合到查詢時，使用參數化查詢。</span><span class="sxs-lookup"><span data-stu-id="8f864-138">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

### <a name="calling-a-query-that-returns-entities"></a><span data-ttu-id="8f864-139">呼叫傳回實體的查詢</span><span class="sxs-lookup"><span data-stu-id="8f864-139">Calling a Query that Returns Entities</span></span>

<span data-ttu-id="8f864-140">假設您希望 `GenericRepository` 類別提供額外的篩選和排序彈性，而不需要使用其他方法建立衍生類別。</span><span class="sxs-lookup"><span data-stu-id="8f864-140">Suppose you want the `GenericRepository` class to provide additional filtering and sorting flexibility without requiring that you create a derived class with additional methods.</span></span> <span data-ttu-id="8f864-141">達成此目標的其中一種方法是新增可接受 SQL 查詢的方法。</span><span class="sxs-lookup"><span data-stu-id="8f864-141">One way to achieve that would be to add a method that accepts a SQL query.</span></span> <span data-ttu-id="8f864-142">然後，您可以在控制器中指定想要的任何一種篩選或排序，例如 `Where` 相依于聯結或子查詢的子句。</span><span class="sxs-lookup"><span data-stu-id="8f864-142">You could then specify any kind of filtering or sorting you want in the controller, such as a `Where` clause that depends on a joins or a subquery.</span></span> <span data-ttu-id="8f864-143">在本節中，您將瞭解如何執行這類方法。</span><span class="sxs-lookup"><span data-stu-id="8f864-143">In this section you'll see how to implement such a method.</span></span>

<span data-ttu-id="8f864-144">藉 `GetWithRawSql` 由將下列程式碼新增至 *GenericRepository.cs* 來建立方法：</span><span class="sxs-lookup"><span data-stu-id="8f864-144">Create the `GetWithRawSql` method by adding the following code to *GenericRepository.cs*:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

<span data-ttu-id="8f864-145">在 *CourseController.cs* 中，從方法呼叫新的方法 `Details` ，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8f864-145">In *CourseController.cs*, call the new method from the `Details` method, as shown in the following example:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

<span data-ttu-id="8f864-146">在此情況下，您可以使用 `GetByID` 方法，但您會使用 `GetWithRawSql` 方法來驗證 `GetWithRawSQL` 方法是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="8f864-146">In this case you could have used the `GetByID` method, but you're using the `GetWithRawSql` method to verify that the `GetWithRawSQL` method works.</span></span>

<span data-ttu-id="8f864-147">執行 [詳細資料] 頁面，確認選取查詢可正常運作 (選取 [ **課程** ] 索引標籤，然後選取一個課程) 的 **詳細資料** 。</span><span class="sxs-lookup"><span data-stu-id="8f864-147">Run the Details page to verify that the select query works (select the **Course** tab and then **Details** for one course).</span></span>

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a><span data-ttu-id="8f864-149">呼叫傳回其他類型之物件的查詢</span><span class="sxs-lookup"><span data-stu-id="8f864-149">Calling a Query that Returns Other Types of Objects</span></span>

<span data-ttu-id="8f864-150">先前您已針對顯示每個註冊日期之學生數目的 About 頁面，建立學生統計資料方格。</span><span class="sxs-lookup"><span data-stu-id="8f864-150">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="8f864-151">在 *HomeController.cs* 中執行此動作的程式碼會使用 LINQ：</span><span class="sxs-lookup"><span data-stu-id="8f864-151">The code that does this in *HomeController.cs* uses LINQ:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

<span data-ttu-id="8f864-152">假設您想要撰寫程式碼，以直接在 SQL 中取出此資料，而不是使用 LINQ。</span><span class="sxs-lookup"><span data-stu-id="8f864-152">Suppose you want to write the code that retrieves this data directly in SQL rather than using LINQ.</span></span> <span data-ttu-id="8f864-153">若要這樣做，您必須執行查詢來傳回實體物件以外的內容，這表示您需要使用 `Database.SqlQuery` 方法。</span><span class="sxs-lookup"><span data-stu-id="8f864-153">To do that you need to run a query that returns something other than entity objects, which means you need to use the `Database.SqlQuery` method.</span></span>

<span data-ttu-id="8f864-154">在 *HomeController.cs* 中，將方法中的 LINQ 語句取代為 `About` 下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="8f864-154">In *HomeController.cs*, replace the LINQ statement in the `About` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

<span data-ttu-id="8f864-155">執行 [關於] 頁面。</span><span class="sxs-lookup"><span data-stu-id="8f864-155">Run the About page.</span></span> <span data-ttu-id="8f864-156">它會顯示與之前相同的資料。</span><span class="sxs-lookup"><span data-stu-id="8f864-156">It displays the same data it did before.</span></span>

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a><span data-ttu-id="8f864-158">呼叫更新查詢</span><span class="sxs-lookup"><span data-stu-id="8f864-158">Calling an Update Query</span></span>

<span data-ttu-id="8f864-159">假設 Contoso 大學系統管理員想要能夠在資料庫中執行大量變更，例如變更每個課程的信用額度數目。</span><span class="sxs-lookup"><span data-stu-id="8f864-159">Suppose Contoso University administrators want to be able to perform bulk changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="8f864-160">如果該大學有大量的課程，擷取全部課程作為實體並個別進行變更的效率不佳。</span><span class="sxs-lookup"><span data-stu-id="8f864-160">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="8f864-161">在這一節中，您將會執行一個網頁，讓使用者指定一個因素來變更所有課程的點數，而您將藉由執行 SQL 語句來進行變更 `UPDATE` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-161">In this section you'll implement a web page that allows the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL `UPDATE` statement.</span></span> <span data-ttu-id="8f864-162">網頁看起來將如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="8f864-162">The web page will look like the following illustration:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

<span data-ttu-id="8f864-164">在上一個教學課程中，您已使用一般儲存機制來讀取和更新 `Course` 控制器中的實體 `Course` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-164">In the previous tutorial you used the generic repository to read and update `Course` entities in the `Course` controller.</span></span> <span data-ttu-id="8f864-165">針對此大量更新作業，您需要建立不在一般存放庫中的新存放庫方法。</span><span class="sxs-lookup"><span data-stu-id="8f864-165">For this bulk update operation, you need to create a new repository method that isn't in the generic repository.</span></span> <span data-ttu-id="8f864-166">若要這樣做，您將建立 `CourseRepository` 衍生自類別的專用類別 `GenericRepository` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-166">To do that, you'll create a dedicated `CourseRepository` class that derives from the `GenericRepository` class.</span></span>

<span data-ttu-id="8f864-167">在 *DAL* 資料夾中，建立 *CourseRepository.cs* ，並以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="8f864-167">In the *DAL* folder, create *CourseRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

<span data-ttu-id="8f864-168">在 *UnitOfWork.cs* 中，將存放 `Course` 庫類型從變更 `GenericRepository<Course>` 為 `CourseRepository:`</span><span class="sxs-lookup"><span data-stu-id="8f864-168">In *UnitOfWork.cs*, change the `Course` repository type from `GenericRepository<Course>` to `CourseRepository:`</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

<span data-ttu-id="8f864-169">在 *CourseController.cs* 中，新增 `UpdateCourseCredits` 方法：</span><span class="sxs-lookup"><span data-stu-id="8f864-169">In *CourseController.cs*, add an `UpdateCourseCredits` method:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

<span data-ttu-id="8f864-170">和都將使用這個方法 `HttpGet` `HttpPost` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-170">This method will be used for both `HttpGet` and `HttpPost`.</span></span> <span data-ttu-id="8f864-171">當 `HttpGet` `UpdateCourseCredits` 方法執行時， `multiplier` 變數會是 null，而視圖會顯示空白的文字方塊和提交按鈕，如上圖所示。</span><span class="sxs-lookup"><span data-stu-id="8f864-171">When the `HttpGet` `UpdateCourseCredits` method runs, the `multiplier` variable will be null and the view will display an empty text box and a submit button, as shown in the preceding illustration.</span></span>

<span data-ttu-id="8f864-172">當您按一下 [ **更新** ] 按鈕並 `HttpPost` 執行此方法時， `multiplier` 將會在文字方塊中輸入值。</span><span class="sxs-lookup"><span data-stu-id="8f864-172">When the **Update** button is clicked and the `HttpPost` method runs, `multiplier` will have the value entered in the text box.</span></span> <span data-ttu-id="8f864-173">然後，程式碼會呼叫 `UpdateCourseCredits` 存放庫方法，它會傳回受影響的資料列數目，而該值會儲存在 `ViewBag` 物件中。</span><span class="sxs-lookup"><span data-stu-id="8f864-173">The code then calls the repository `UpdateCourseCredits` method, which returns the number of affected rows, and that value is stored in the `ViewBag` object.</span></span> <span data-ttu-id="8f864-174">當 view 收到物件中受影響的資料列數目時 `ViewBag` ，它會顯示該數位，而不是文字方塊和提交按鈕，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="8f864-174">When the view receives the number of affected rows in the `ViewBag` object, it displays that number instead of the text box and submit button, as shown in the following illustration:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

<span data-ttu-id="8f864-176">在 [更新課程點數] 頁面的 [ *Views\Course* ] 資料夾中建立一個 view：</span><span class="sxs-lookup"><span data-stu-id="8f864-176">Create a view in the *Views\Course* folder for the Update Course Credits page:</span></span>

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

<span data-ttu-id="8f864-178">在 *Views\Course\UpdateCourseCredits.cshtml* 中，將範本程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="8f864-178">In *Views\Course\UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

<span data-ttu-id="8f864-179">藉由選取 [課程]  索引標籤，然後將 "/UpdateCourseCredits" 新增至瀏覽器位址列中的 URL 結尾 (例如：`http://localhost:50205/Course/UpdateCourseCredits`)，以執行 `UpdateCourseCredits` 方法。</span><span class="sxs-lookup"><span data-stu-id="8f864-179">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:50205/Course/UpdateCourseCredits`).</span></span> <span data-ttu-id="8f864-180">在文字方塊中輸入數目：</span><span class="sxs-lookup"><span data-stu-id="8f864-180">Enter a number in the text box:</span></span>

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

<span data-ttu-id="8f864-182">按一下 [更新]  。</span><span class="sxs-lookup"><span data-stu-id="8f864-182">Click **Update**.</span></span> <span data-ttu-id="8f864-183">您會看到受影響的資料列數目：</span><span class="sxs-lookup"><span data-stu-id="8f864-183">You see the number of rows affected:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

<span data-ttu-id="8f864-185">按一下 [回到清單]，以查看課程與已修訂學分數的清單。</span><span class="sxs-lookup"><span data-stu-id="8f864-185">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

<span data-ttu-id="8f864-187">如需有關原始 SQL 查詢的詳細資訊，請參閱 Entity Framework team blog 上的 [原始 Sql 查詢](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="8f864-187">For more information about raw SQL queries, see [Raw SQL Queries](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) on the Entity Framework team blog.</span></span>

## <a name="no-tracking-queries"></a><span data-ttu-id="8f864-188">不追蹤的查詢</span><span class="sxs-lookup"><span data-stu-id="8f864-188">No-Tracking Queries</span></span>

<span data-ttu-id="8f864-189">當資料庫內容抓取資料庫資料列並建立代表它們的實體物件時，根據預設，它會追蹤記憶體中的實體是否與資料庫中的實體同步。</span><span class="sxs-lookup"><span data-stu-id="8f864-189">When a database context retrieves database rows and creates entity objects that represent them, by default it keeps track of whether the entities in memory are in sync with what's in the database.</span></span> <span data-ttu-id="8f864-190">記憶體中的資料所扮演的角色是一個快取，並會在您更新實體時使用。</span><span class="sxs-lookup"><span data-stu-id="8f864-190">The data in memory acts as a cache and is used when you update an entity.</span></span> <span data-ttu-id="8f864-191">這個快取通常在 Web 應用程式當中是不需要的，因為內容執行個體通常壽命都很短 (每次要求都會建立一個新的並進行處置)，並且通常讀取實體的內容都會在實體重新獲得利用前遭到處置。</span><span class="sxs-lookup"><span data-stu-id="8f864-191">This caching is often unnecessary in a web application because context instances are typically short-lived (a new one is created and disposed for each request) and the context that reads an entity is typically disposed before that entity is used again.</span></span>

<span data-ttu-id="8f864-192">您可以使用方法，指定內容是否追蹤查詢的實體物件 `AsNoTracking` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-192">You can specify whether the context tracks entity objects for a query by using the `AsNoTracking` method.</span></span> <span data-ttu-id="8f864-193">您會想要進行這項操作的常見案例包括下列情況：</span><span class="sxs-lookup"><span data-stu-id="8f864-193">Typical scenarios in which you might want to do that include the following:</span></span>

- <span data-ttu-id="8f864-194">此查詢會抓取關閉追蹤的大量資料，可能會明顯地提升效能。</span><span class="sxs-lookup"><span data-stu-id="8f864-194">The query retrieves such a large volume of data that turning off tracking might noticeably enhance performance.</span></span>
- <span data-ttu-id="8f864-195">您想要附加實體以進行更新，但先前已針對不同用途抓取相同的實體。</span><span class="sxs-lookup"><span data-stu-id="8f864-195">You want to attach an entity in order to update it, but you earlier retrieved the same entity for a different purpose.</span></span> <span data-ttu-id="8f864-196">由於實體已由資料庫內容進行追蹤，您無法連結到您想要變更的實體。</span><span class="sxs-lookup"><span data-stu-id="8f864-196">Because the entity is already being tracked by the database context, you can't attach the entity that you want to change.</span></span> <span data-ttu-id="8f864-197">防止這種情況發生的其中一種方法，就是使用 `AsNoTracking` 選項搭配先前的查詢。</span><span class="sxs-lookup"><span data-stu-id="8f864-197">One way to prevent this from happening is to use the `AsNoTracking` option with the earlier query.</span></span>

<span data-ttu-id="8f864-198">在本節中，您將會執行商務邏輯，以說明這些案例的第二個。</span><span class="sxs-lookup"><span data-stu-id="8f864-198">In this section you'll implement business logic that illustrates the second of these scenarios.</span></span> <span data-ttu-id="8f864-199">具體來說，您將強制執行一個商務規則，指出講師不能是一個以上部門的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="8f864-199">Specifically, you'll enforce a business rule that says that an instructor can't be the administrator of more than one department.</span></span>

<span data-ttu-id="8f864-200">在 *DepartmentController.cs* 中，新增可從和方法呼叫的新方法 `Edit` ， `Create` 以確定沒有兩個部門具有相同的系統管理員：</span><span class="sxs-lookup"><span data-stu-id="8f864-200">In *DepartmentController.cs*, add a new method that you can call from the `Edit` and `Create` methods to make sure that no two departments have the same administrator:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

<span data-ttu-id="8f864-201">如果沒有任何驗證錯誤，請在方法的區塊中新增程式碼 `try` `HttpPost` `Edit` ，以呼叫這個新的方法。</span><span class="sxs-lookup"><span data-stu-id="8f864-201">Add code in the `try` block of the `HttpPost` `Edit` method to call this new method if there are no validation errors.</span></span> <span data-ttu-id="8f864-202">`try`區塊現在看起來如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8f864-202">The `try` block now looks like the following example:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

<span data-ttu-id="8f864-203">執行 [部門編輯] 頁面，然後嘗試將部門的系統管理員變更為另一個部門的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="8f864-203">Run the Department Edit page and try to change a department's administrator to an instructor who is already the administrator of a different department.</span></span> <span data-ttu-id="8f864-204">您會收到預期的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="8f864-204">You get the expected error message:</span></span>

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

<span data-ttu-id="8f864-206">現在，再次執行部門編輯頁面，這次變更 **預算** 金額。</span><span class="sxs-lookup"><span data-stu-id="8f864-206">Now run the Department Edit page again and this time change the **Budget** amount.</span></span> <span data-ttu-id="8f864-207">當您按一下 [ **儲存**] 時，會看到錯誤頁面：</span><span class="sxs-lookup"><span data-stu-id="8f864-207">When you click **Save**, you see an error page:</span></span>

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

<span data-ttu-id="8f864-209">例外狀況錯誤訊息是「」 `An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.` 因為下列事件順序而發生：</span><span class="sxs-lookup"><span data-stu-id="8f864-209">The exception error message is "`An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.`" This happened because of the following sequence of events:</span></span>

- <span data-ttu-id="8f864-210">`Edit`方法 `ValidateOneAdministratorAssignmentPerInstructor` 會呼叫方法，此方法會抓取以 Kim Abercrombie 為其系統管理員的所有部門。</span><span class="sxs-lookup"><span data-stu-id="8f864-210">The `Edit` method calls the `ValidateOneAdministratorAssignmentPerInstructor` method, which retrieves all departments that have Kim Abercrombie as their administrator.</span></span> <span data-ttu-id="8f864-211">這會導致讀取英文部門。</span><span class="sxs-lookup"><span data-stu-id="8f864-211">That causes the English department to be read.</span></span> <span data-ttu-id="8f864-212">因為這是正在編輯的部門，所以不會回報任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="8f864-212">Because that's the department being edited, no error is reported.</span></span> <span data-ttu-id="8f864-213">不過，這項讀取作業的結果是，資料庫內容現在正在追蹤從資料庫讀取的英文部門實體。</span><span class="sxs-lookup"><span data-stu-id="8f864-213">As a result of this read operation, however, the English department entity that was read from the database is now being tracked by the database context.</span></span>
- <span data-ttu-id="8f864-214">`Edit`方法會嘗試在 `Modified` MVC 模型系結器所建立的英文部門實體上設定旗標，但因為內容已經在追蹤英文部門的實體，所以會失敗。</span><span class="sxs-lookup"><span data-stu-id="8f864-214">The `Edit` method tries to set the `Modified` flag on the English department entity created by the MVC model binder, but that fails because the context is already tracking an entity for the English department.</span></span>

<span data-ttu-id="8f864-215">這個問題的解決方法之一，是讓內容不能追蹤驗證查詢所抓取的記憶體中部門實體。</span><span class="sxs-lookup"><span data-stu-id="8f864-215">One solution to this problem is to keep the context from tracking in-memory department entities retrieved by the validation query.</span></span> <span data-ttu-id="8f864-216">這樣做並沒有任何缺點，因為您不會更新此實體，也不會以它在記憶體中快取的方式來讀取它。</span><span class="sxs-lookup"><span data-stu-id="8f864-216">There's no disadvantage to doing this, because you won't be updating this entity or reading it again in a way that would benefit from it being cached in memory.</span></span>

<span data-ttu-id="8f864-217">在 *DepartmentController.cs* 中，于 `ValidateOneAdministratorAssignmentPerInstructor` 方法中指定 [無追蹤]，如下列所示：</span><span class="sxs-lookup"><span data-stu-id="8f864-217">In *DepartmentController.cs*, in the `ValidateOneAdministratorAssignmentPerInstructor` method, specify no tracking, as shown in the following:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

<span data-ttu-id="8f864-218">請重複嘗試編輯部門的 **預算** 金額。</span><span class="sxs-lookup"><span data-stu-id="8f864-218">Repeat your attempt to edit the **Budget** amount of a department.</span></span> <span data-ttu-id="8f864-219">這次作業成功時，網站會如預期般傳回至 [部門索引] 頁面，以顯示修改過的預算值。</span><span class="sxs-lookup"><span data-stu-id="8f864-219">This time the operation is successful, and the site returns as expected to the Departments Index page, showing the revised budget value.</span></span>

## <a name="examining-queries-sent-to-the-database"></a><span data-ttu-id="8f864-220">檢查傳送至資料庫的查詢</span><span class="sxs-lookup"><span data-stu-id="8f864-220">Examining Queries Sent to the Database</span></span>

<span data-ttu-id="8f864-221">有時能夠看到傳送至資料庫的實際 SQL 查詢很有幫助。</span><span class="sxs-lookup"><span data-stu-id="8f864-221">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="8f864-222">若要這樣做，您可以在偵錯工具中檢查查詢變數，或呼叫查詢的 `ToString` 方法。</span><span class="sxs-lookup"><span data-stu-id="8f864-222">To do this, you can examine a query variable in the debugger or call the query's `ToString` method.</span></span> <span data-ttu-id="8f864-223">若要試試看，您將會看到一個簡單的查詢，然後查看當您新增諸如立即載入、篩選和排序等選項時，會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="8f864-223">To try this out, you'll look at a simple query and then look at what happens to it as you add options such eager loading, filtering, and sorting.</span></span>

<span data-ttu-id="8f864-224">在 *控制器/CourseController* 中，以 `Index` 下列程式碼取代方法：</span><span class="sxs-lookup"><span data-stu-id="8f864-224">In *Controllers/CourseController*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

<span data-ttu-id="8f864-225">現在在的 *GenericRepository.cs* 中設定中斷點 `return query.ToList();` ，並在方法的語句上設定中斷點 `return orderBy(query).ToList();` `Get` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-225">Now set a breakpoint in *GenericRepository.cs* on the `return query.ToList();` and the `return orderBy(query).ToList();` statements of the `Get` method.</span></span> <span data-ttu-id="8f864-226">在「偵測模式」中執行專案，然後選取 [課程索引] 頁面。</span><span class="sxs-lookup"><span data-stu-id="8f864-226">Run the project in debug mode and select the Course Index page.</span></span> <span data-ttu-id="8f864-227">當程式碼到達中斷點時，檢查 `query` 變數。</span><span class="sxs-lookup"><span data-stu-id="8f864-227">When the code reaches the breakpoint, examine the `query` variable.</span></span> <span data-ttu-id="8f864-228">您會看到傳送給 SQL Server 的查詢。</span><span class="sxs-lookup"><span data-stu-id="8f864-228">You see the query that's sent to SQL Server.</span></span> <span data-ttu-id="8f864-229">這是簡單的 `Select` 語句：</span><span class="sxs-lookup"><span data-stu-id="8f864-229">It's a simple `Select` statement:</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.sql)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

<span data-ttu-id="8f864-230">查詢可能太長，無法在 Visual Studio 的調試時間視窗中顯示。</span><span class="sxs-lookup"><span data-stu-id="8f864-230">Queries can be too long to display in the debugging windows in Visual Studio.</span></span> <span data-ttu-id="8f864-231">若要查看整個查詢，您可以複製變數值，並將它貼到文字編輯器中：</span><span class="sxs-lookup"><span data-stu-id="8f864-231">To see the entire query, you can copy the variable value and paste it into a text editor:</span></span>

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

<span data-ttu-id="8f864-233">現在您要將下拉式清單新增至課程索引頁面，讓使用者可以篩選特定部門。</span><span class="sxs-lookup"><span data-stu-id="8f864-233">Now you'll add a drop-down list to the Course Index page so that users can filter for a particular department.</span></span> <span data-ttu-id="8f864-234">您將依標題排序課程，並指定導覽屬性的積極式載入 `Department` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-234">You'll sort the courses by title, and you'll specify eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="8f864-235">在 *CourseController.cs* 中，以 `Index` 下列程式碼取代方法：</span><span class="sxs-lookup"><span data-stu-id="8f864-235">In *CourseController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

<span data-ttu-id="8f864-236">方法會在參數中接收選取的下拉式清單值 `SelectedDepartment` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-236">The method receives the selected value of the drop-down list in the `SelectedDepartment` parameter.</span></span> <span data-ttu-id="8f864-237">如果未選取任何專案，此參數將會是 null。</span><span class="sxs-lookup"><span data-stu-id="8f864-237">If nothing is selected, this parameter will be null.</span></span>

<span data-ttu-id="8f864-238">`SelectList`包含所有部門的集合會傳遞至下拉式清單的 [view]。</span><span class="sxs-lookup"><span data-stu-id="8f864-238">A `SelectList` collection containing all departments is passed to the view for the drop-down list.</span></span> <span data-ttu-id="8f864-239">傳遞給此函式的參數會 `SelectList` 指定值功能變數名稱、文字功能變數名稱和選取的專案。</span><span class="sxs-lookup"><span data-stu-id="8f864-239">The parameters passed to the `SelectList` constructor specify the value field name, the text field name, and the selected item.</span></span>

<span data-ttu-id="8f864-240">針對存放 `Get` 庫的方法 `Course` ，程式碼會指定篩選運算式、排序次序，以及導覽屬性的積極式載入 `Department` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-240">For the `Get` method of the `Course` repository, the code specifies a filter expression, a sort order, and eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="8f864-241">如果下拉式清單中沒有選取任何專案，則篩選運算式一律會傳回 `true` (也就是 `SelectedDepartment` null) 。</span><span class="sxs-lookup"><span data-stu-id="8f864-241">The filter expression always returns `true` if nothing is selected in the drop-down list (that is, `SelectedDepartment` is null).</span></span>

<span data-ttu-id="8f864-242">在 *Views\Course\Index.cshtml* 中，緊接在開頭 `table` 標記之前，加入下列程式碼以建立下拉式清單和 [提交] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="8f864-242">In *Views\Course\Index.cshtml*, immediately before the opening `table` tag, add the following code to create the drop-down list and a submit button:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

<span data-ttu-id="8f864-243">在類別中仍設定中斷點的情況 `GenericRepository` 下，執行課程索引頁面。</span><span class="sxs-lookup"><span data-stu-id="8f864-243">With the breakpoints still set in the `GenericRepository` class, run the Course Index page.</span></span> <span data-ttu-id="8f864-244">繼續進行程式碼叫用中斷點的前兩次，以便在瀏覽器中顯示頁面。</span><span class="sxs-lookup"><span data-stu-id="8f864-244">Continue through the first two times that the code hits a breakpoint, so that the page is displayed in the browser.</span></span> <span data-ttu-id="8f864-245">從下拉式清單中選取部門，然後按一下 [ **篩選**]：</span><span class="sxs-lookup"><span data-stu-id="8f864-245">Select a department from the drop-down list and click **Filter**:</span></span>

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

<span data-ttu-id="8f864-247">這次第一個中斷點將是針對下拉式清單中的部門查詢。</span><span class="sxs-lookup"><span data-stu-id="8f864-247">This time the first breakpoint will be for the departments query for the drop-down list.</span></span> <span data-ttu-id="8f864-248">略過該變數，並 `query` 在程式碼下一次到達中斷點時查看變數，以查看 `Course` 查詢現在的樣子。</span><span class="sxs-lookup"><span data-stu-id="8f864-248">Skip that and view the `query` variable the next time the code reaches the breakpoint in order to see what the `Course` query now looks like.</span></span> <span data-ttu-id="8f864-249">您會看到如下所示的內容：</span><span class="sxs-lookup"><span data-stu-id="8f864-249">You'll see something like the following:</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.sql)]

<span data-ttu-id="8f864-250">您可以看到查詢現在是一項查詢，它會 `JOIN` 載入 `Department` 資料以及 `Course` 資料，並且包含 `WHERE` 子句。</span><span class="sxs-lookup"><span data-stu-id="8f864-250">You can see that the query is now a `JOIN` query that loads `Department` data along with the `Course` data, and that it includes a `WHERE` clause.</span></span>

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a><span data-ttu-id="8f864-251">使用 Proxy 類別</span><span class="sxs-lookup"><span data-stu-id="8f864-251">Working with Proxy Classes</span></span>

<span data-ttu-id="8f864-252">當 Entity Framework 建立實體實例時 (例如，當您執行) 的查詢時，通常會將其建立為動態產生的衍生型別實例，作為實體的 proxy。</span><span class="sxs-lookup"><span data-stu-id="8f864-252">When the Entity Framework creates entity instances (for example, when you execute a query), it often creates them as instances of a dynamically generated derived type that acts as a proxy for the entity.</span></span> <span data-ttu-id="8f864-253">此 proxy 會覆寫實體的一些虛擬屬性，以便在存取屬性時自動插入用來執行動作的勾點。</span><span class="sxs-lookup"><span data-stu-id="8f864-253">This proxy overrides some virtual properties of the entity to insert hooks for performing actions automatically when the property is accessed.</span></span> <span data-ttu-id="8f864-254">例如，這項機制可用來支援關聯性的延遲載入。</span><span class="sxs-lookup"><span data-stu-id="8f864-254">For example, this mechanism is used to support lazy loading of relationships.</span></span>

<span data-ttu-id="8f864-255">大部分的情況下，您不需要察覺 proxy 的使用，但有一些例外狀況：</span><span class="sxs-lookup"><span data-stu-id="8f864-255">Most of the time you don't need to be aware of this use of proxies, but there are exceptions:</span></span>

- <span data-ttu-id="8f864-256">在某些情況下，您可能會想要防止 Entity Framework 建立 proxy 實例。</span><span class="sxs-lookup"><span data-stu-id="8f864-256">In some scenarios you might want to prevent the Entity Framework from creating proxy instances.</span></span> <span data-ttu-id="8f864-257">例如，序列化非 proxy 實例可能比序列化 proxy 實例更有效率。</span><span class="sxs-lookup"><span data-stu-id="8f864-257">For example, serializing non-proxy instances might be more efficient than serializing proxy instances.</span></span>
- <span data-ttu-id="8f864-258">當您使用運算子具現化實體類別時 `new` ，您不會取得 proxy 實例。</span><span class="sxs-lookup"><span data-stu-id="8f864-258">When you instantiate an entity class using the `new` operator, you don't get a proxy instance.</span></span> <span data-ttu-id="8f864-259">這表示您不會取得延遲載入和自動變更追蹤等功能。</span><span class="sxs-lookup"><span data-stu-id="8f864-259">This means you don't get functionality such as lazy loading and automatic change tracking.</span></span> <span data-ttu-id="8f864-260">這通常是正常的;您通常不需要消極式載入，因為您要建立的新實體不在資料庫中，而且如果您將實體明確標示為，通常不需要變更追蹤 `Added` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-260">This is typically okay; you generally don't need lazy loading, because you're creating a new entity that isn't in the database, and you generally don't need change tracking if you're explicitly marking the entity as `Added`.</span></span> <span data-ttu-id="8f864-261">但是，如果您需要消極式載入，而且需要變更追蹤，您可以使用類別的方法，以 proxy 建立新的實體實例 `Create` `DbSet` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-261">However, if you do need lazy loading and you need change tracking, you can create new entity instances with proxies using the `Create` method of the `DbSet` class.</span></span>
- <span data-ttu-id="8f864-262">您可能會想要從 proxy 類型取得實際的實體類型。</span><span class="sxs-lookup"><span data-stu-id="8f864-262">You might want to get an actual entity type from a proxy type.</span></span> <span data-ttu-id="8f864-263">您可以使用 `GetObjectType` 類別的方法 `ObjectContext` 來取得 proxy 型別實例的實際實體型別。</span><span class="sxs-lookup"><span data-stu-id="8f864-263">You can use the `GetObjectType` method of the `ObjectContext` class to get the actual entity type of a proxy type instance.</span></span>

<span data-ttu-id="8f864-264">如需詳細資訊， [請參閱 Entity Framework](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) team blog 上的使用 proxy。</span><span class="sxs-lookup"><span data-stu-id="8f864-264">For more information, see [Working with Proxies](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) on the Entity Framework team blog.</span></span>

## <a name="disabling-automatic-detection-of-changes"></a><span data-ttu-id="8f864-265">停用自動偵測變更</span><span class="sxs-lookup"><span data-stu-id="8f864-265">Disabling Automatic Detection of Changes</span></span>

<span data-ttu-id="8f864-266">Entity Framework 藉由比較實體的目前值與原始值，判斷實體如何變更 (以及因此需要將哪些更新傳送至資料庫)。</span><span class="sxs-lookup"><span data-stu-id="8f864-266">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="8f864-267">當查詢或附加實體時，會儲存原始的值。</span><span class="sxs-lookup"><span data-stu-id="8f864-267">The original values are stored when the entity was queried or attached.</span></span> <span data-ttu-id="8f864-268">會導致自動變更偵測的一些方法如下：</span><span class="sxs-lookup"><span data-stu-id="8f864-268">Some of the methods that cause automatic change detection are the following:</span></span>

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

<span data-ttu-id="8f864-269">如果您要追蹤大量的實體，並且在迴圈中多次呼叫其中一種方法，您可以使用 [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) 屬性暫時關閉自動變更偵測，以獲得大幅的效能改進。</span><span class="sxs-lookup"><span data-stu-id="8f864-269">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) property.</span></span> <span data-ttu-id="8f864-270">如需詳細資訊，請參閱 [自動偵測變更](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8f864-270">For more information, see [Automatically Detecting Changes](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx).</span></span>

## <a name="disabling-validation-when-saving-changes"></a><span data-ttu-id="8f864-271">在儲存變更時停用驗證</span><span class="sxs-lookup"><span data-stu-id="8f864-271">Disabling Validation When Saving Changes</span></span>

<span data-ttu-id="8f864-272">當您呼叫 `SaveChanges` 方法時，根據預設，Entity Framework 會在更新資料庫之前，先驗證所有已變更之實體的所有屬性中的資料。</span><span class="sxs-lookup"><span data-stu-id="8f864-272">When you call the `SaveChanges` method, by default the Entity Framework validates the data in all properties of all changed entities before updating the database.</span></span> <span data-ttu-id="8f864-273">如果您已更新大量的實體，而且已經驗證資料，則這項工作是不必要的，而且您可以暫時關閉驗證，讓儲存變更的程式花較少的時間。</span><span class="sxs-lookup"><span data-stu-id="8f864-273">If you've updated a large number of entities and you've already validated the data, this work is unnecessary and you could make the process of saving the changes take less time by temporarily turning off validation.</span></span> <span data-ttu-id="8f864-274">您可以使用 [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) 屬性來這麼做。</span><span class="sxs-lookup"><span data-stu-id="8f864-274">You can do that using the [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) property.</span></span> <span data-ttu-id="8f864-275">如需詳細資訊，請參閱 [驗證](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8f864-275">For more information, see [Validation](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="8f864-276">摘要</span><span class="sxs-lookup"><span data-stu-id="8f864-276">Summary</span></span>

<span data-ttu-id="8f864-277">這一系列的教學課程會在 ASP.NET MVC 應用程式中使用 Entity Framework 完成。</span><span class="sxs-lookup"><span data-stu-id="8f864-277">This completes this series of tutorials on using the Entity Framework in an ASP.NET MVC application.</span></span> <span data-ttu-id="8f864-278">您可以在 [ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="8f864-278">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="8f864-279">如需如何在建立 web 應用程式之後進行部署的詳細資訊，請參閱 MSDN Library 中的 [ASP.NET 部署內容對應](https://msdn.microsoft.com/library/bb386521.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="8f864-279">For more information about how to deploy your web application after you've built it, see [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx) in the MSDN Library.</span></span>

<span data-ttu-id="8f864-280">如需與 MVC 相關之其他主題（例如驗證和授權）的詳細資訊，請參閱 [Mvc 建議的資源](../../getting-started/recommended-resources-for-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="8f864-280">For information about other topics related to MVC, such as authentication and authorization, see the [MVC Recommended Resources](../../getting-started/recommended-resources-for-mvc.md).</span></span>

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a><span data-ttu-id="8f864-281">通知</span><span class="sxs-lookup"><span data-stu-id="8f864-281">Acknowledgments</span></span>

- <span data-ttu-id="8f864-282">Tom Dykstra 撰寫了本教學課程的原始版本，也是 Microsoft Web Platform 和 Tools 內容小組的資深程式設計作者。</span><span class="sxs-lookup"><span data-stu-id="8f864-282">Tom Dykstra wrote the original version of this tutorial and is a senior programming writer on the Microsoft Web Platform and Tools Content Team.</span></span>
- <span data-ttu-id="8f864-283">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) 共同撰寫本教學課程，並已針對 EF 5 和 MVC 4 更新大部分的工作。</span><span class="sxs-lookup"><span data-stu-id="8f864-283">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) co-authored this tutorial and did most of the work updating it for EF 5 and MVC 4.</span></span> <span data-ttu-id="8f864-284">Rick 是 Microsoft 的資深程式設計作者，著重于 Azure 和 MVC。</span><span class="sxs-lookup"><span data-stu-id="8f864-284">Rick is a senior programming writer for Microsoft focusing on Azure and MVC.</span></span>
- <span data-ttu-id="8f864-285">[Rowan 莎莎](http://www.romiller.com) 和 Entity Framework 團隊的其他成員協助進行程式碼審核，並協助您在更新 EF 5 的教學課程時，在發生遷移的許多問題時進行調試。</span><span class="sxs-lookup"><span data-stu-id="8f864-285">[Rowan Miller](http://www.romiller.com) and other members of the Entity Framework team assisted with code reviews and helped debug many issues with migrations that arose while we were updating the tutorial for EF 5.</span></span>

## <a name="vb"></a><span data-ttu-id="8f864-286">VB</span><span class="sxs-lookup"><span data-stu-id="8f864-286">VB</span></span>

<span data-ttu-id="8f864-287">在最初產生教學課程時，我們提供了已完成下載專案的 c # 和 VB 版本。</span><span class="sxs-lookup"><span data-stu-id="8f864-287">When the tutorial was originally produced, we provided both C# and VB versions of the completed download project.</span></span> <span data-ttu-id="8f864-288">在這項更新中，我們會為每個章節提供一個可供下載的 c # 專案，讓您更輕鬆地從系列中的任何地方開始著手，但由於時間限制和其他優先順序，我們並不會針對 VB 進行。</span><span class="sxs-lookup"><span data-stu-id="8f864-288">With this update we are providing a C# downloadable project for each chapter to make it easier to get started anywhere in the series, but due to time limitations and other priorities we did not do that for VB.</span></span> <span data-ttu-id="8f864-289">如果您使用這些教學課程來建立 VB 專案，而且願意與他人共用，請讓我們知道。</span><span class="sxs-lookup"><span data-stu-id="8f864-289">If you build a VB project using these tutorials and would be willing to share that with others, please let us know.</span></span>

<a id="errors"></a>

## <a name="errors-and-workarounds"></a><span data-ttu-id="8f864-290">錯誤和解決方法</span><span class="sxs-lookup"><span data-stu-id="8f864-290">Errors and Workarounds</span></span>

### <a name="cannot-createshadow-copy"></a><span data-ttu-id="8f864-291">無法建立/陰影複製</span><span class="sxs-lookup"><span data-stu-id="8f864-291">Cannot create/shadow copy</span></span>

<span data-ttu-id="8f864-292">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="8f864-292">Error Message:</span></span>

<span data-ttu-id="8f864-293">*當該檔案已經存在時，無法建立/陰影複製 ' DotNetOpenAuth。*</span><span class="sxs-lookup"><span data-stu-id="8f864-293">*Cannot create/shadow copy 'DotNetOpenAuth.OpenId' when that file already exists.*</span></span>

<span data-ttu-id="8f864-294">解決方案：</span><span class="sxs-lookup"><span data-stu-id="8f864-294">Solution:</span></span>

<span data-ttu-id="8f864-295">等候幾秒鐘，然後重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="8f864-295">Wait a few seconds and refresh the page.</span></span>

### <a name="update-database-not-recognized"></a><span data-ttu-id="8f864-296">無法辨識 Update-Database</span><span class="sxs-lookup"><span data-stu-id="8f864-296">Update-Database not recognized</span></span>

<span data-ttu-id="8f864-297">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="8f864-297">Error Message:</span></span>

<span data-ttu-id="8f864-298">「*更新資料庫」一詞無法辨識為 Cmdlet、函式、指令檔或可操作程式的名稱。請檢查名稱的拼寫是否正確，如果包含路徑的話，請確認路徑是否正確，然後再試一次。* 從 *`Update-Database`* PMC 中的命令 (。 ) </span><span class="sxs-lookup"><span data-stu-id="8f864-298">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*(From the *`Update-Database`* command in the PMC.)</span></span>

<span data-ttu-id="8f864-299">解決方案：</span><span class="sxs-lookup"><span data-stu-id="8f864-299">Solution:</span></span>

<span data-ttu-id="8f864-300">結束 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="8f864-300">Exit Visual Studio.</span></span> <span data-ttu-id="8f864-301">重新開啟專案，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="8f864-301">Reopen project and try again.</span></span>

### <a name="validation-failed"></a><span data-ttu-id="8f864-302">驗證失敗</span><span class="sxs-lookup"><span data-stu-id="8f864-302">Validation failed</span></span>

<span data-ttu-id="8f864-303">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="8f864-303">Error Message:</span></span>

<span data-ttu-id="8f864-304">*一或多個實體的驗證失敗。如需詳細資訊，請參閱 ' EntityValidationErrors ' 屬性。*</span><span class="sxs-lookup"><span data-stu-id="8f864-304">*Validation failed for one or more entities. See 'EntityValidationErrors' property for more details.*</span></span> <span data-ttu-id="8f864-305">從 *`Update-Database`* PMC 中的命令 (。 ) </span><span class="sxs-lookup"><span data-stu-id="8f864-305">(From the *`Update-Database`* command in the PMC.)</span></span>

<span data-ttu-id="8f864-306">解決方案：</span><span class="sxs-lookup"><span data-stu-id="8f864-306">Solution:</span></span>

<span data-ttu-id="8f864-307">發生此問題的其中一個原因是方法執行時發生驗證錯誤 `Seed` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-307">One cause of this problem is validation errors when the `Seed` method runs.</span></span> <span data-ttu-id="8f864-308">請參閱 [植入和偵測 Entity Framework (EF) db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 以取得對方法進行偵錯工具的秘訣 `Seed` 。</span><span class="sxs-lookup"><span data-stu-id="8f864-308">See [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) for tips on debugging the `Seed` method.</span></span>

### <a name="http-50019-error"></a><span data-ttu-id="8f864-309">HTTP 500.19 錯誤</span><span class="sxs-lookup"><span data-stu-id="8f864-309">HTTP 500.19 error</span></span>

<span data-ttu-id="8f864-310">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="8f864-310">Error Message:</span></span>

<span data-ttu-id="8f864-311">*HTTP 錯誤 500.19-內部伺服器錯誤：無法存取要求的頁面，因為頁面的相關設定資料無效。*</span><span class="sxs-lookup"><span data-stu-id="8f864-311">*HTTP Error 500.19 - Internal Server Error The requested page cannot be accessed because the related configuration data for the page is invalid.*</span></span>

<span data-ttu-id="8f864-312">解決方案：</span><span class="sxs-lookup"><span data-stu-id="8f864-312">Solution:</span></span>

<span data-ttu-id="8f864-313">您可以取得此錯誤的其中一種方式，就是使用多個解決方案複本，每個複本都使用相同的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="8f864-313">One way you can get this error is from having multiple copies of the solution, each of them using the same port number.</span></span> <span data-ttu-id="8f864-314">您通常可以藉由結束 Visual Studio 的所有實例，然後重新開機您正在處理的專案，來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="8f864-314">You can usually solve this problem by exiting all instances of Visual Studio, then restarting the project your working on.</span></span> <span data-ttu-id="8f864-315">如果無法運作，請嘗試變更埠號碼。</span><span class="sxs-lookup"><span data-stu-id="8f864-315">If that doesn't work, try changing the port number.</span></span> <span data-ttu-id="8f864-316">以滑鼠右鍵按一下專案檔，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="8f864-316">Right click on the project file and then click properties.</span></span> <span data-ttu-id="8f864-317">選取 [ **Web** ] 索引標籤，然後變更 [ **專案 Url** ] 文字方塊中的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="8f864-317">Select the **Web** tab and then change the port number in the **Project Url** text box.</span></span>

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="8f864-318">搜尋 SQL Server 執行個體時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="8f864-318">Error locating SQL Server instance</span></span>

<span data-ttu-id="8f864-319">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="8f864-319">Error Message:</span></span>

<span data-ttu-id="8f864-320">*建立與 SQL Server 的連接時發生網路相關或實例特定的錯誤。找不到或無法存取伺服器。請驗證實例名稱是否正確，並將 SQL Server 設定為允許遠端連線。 (提供者： SQL 網路介面，錯誤： 26-尋找指定的伺服器/實例時發生錯誤)*</span><span class="sxs-lookup"><span data-stu-id="8f864-320">*A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)*</span></span>

<span data-ttu-id="8f864-321">解決方案：</span><span class="sxs-lookup"><span data-stu-id="8f864-321">Solution:</span></span>

<span data-ttu-id="8f864-322">請檢查連接字串。</span><span class="sxs-lookup"><span data-stu-id="8f864-322">Check connection string.</span></span> <span data-ttu-id="8f864-323">如果您已手動刪除資料庫，請在結構字串中變更資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="8f864-323">If you have manually deleted the database, change the name of the database in the construction string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8f864-324">[上一個](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md) 
> [下一步](building-the-ef5-mvc4-chapter-downloads.md)</span><span class="sxs-lookup"><span data-stu-id="8f864-324">[Previous](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
[Next](building-the-ef5-mvc4-chapter-downloads.md)</span></span>
