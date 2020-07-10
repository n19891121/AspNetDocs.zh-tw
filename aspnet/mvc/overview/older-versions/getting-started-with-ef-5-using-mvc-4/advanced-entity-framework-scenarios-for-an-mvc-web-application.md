---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: MVC Web 應用程式的 Advanced Entity Framework 案例， (10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio ... 來建立 ASP.NET MVC 4 應用程式。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: f8f079f6d8ea663c6888456be422a2bae93a4b87
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "86163437"
---
# <a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a><span data-ttu-id="717ce-103">MVC Web 應用程式的 Advanced Entity Framework 案例， (10) </span><span class="sxs-lookup"><span data-stu-id="717ce-103">Advanced Entity Framework Scenarios for an MVC Web Application (10 of 10)</span></span>

<span data-ttu-id="717ce-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="717ce-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="717ce-105">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="717ce-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="717ce-106">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="717ce-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="717ce-107">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="717ce-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="717ce-108">您可以從一開始就開始本教學課程系列，或[下載本章節的入門專案](building-the-ef5-mvc4-chapter-downloads.md)，並從這裡開始。</span><span class="sxs-lookup"><span data-stu-id="717ce-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="717ce-109">如果您遇到無法解決的問題，請[下載完整的章節](building-the-ef5-mvc4-chapter-downloads.md)並嘗試重現您的問題。</span><span class="sxs-lookup"><span data-stu-id="717ce-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="717ce-110">您通常可以藉由比較您的程式碼與已完成的程式碼，來找出問題的解決方法。</span><span class="sxs-lookup"><span data-stu-id="717ce-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="717ce-111">如需瞭解一些常見錯誤以及如何解決問題，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。</span><span class="sxs-lookup"><span data-stu-id="717ce-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="717ce-112">在上一個教學課程中，您已執行了儲存機制和工作單位模式。</span><span class="sxs-lookup"><span data-stu-id="717ce-112">In the previous tutorial you implemented the repository and unit of work patterns.</span></span> <span data-ttu-id="717ce-113">本教學課程涵蓋下列主題：</span><span class="sxs-lookup"><span data-stu-id="717ce-113">This tutorial covers the following topics:</span></span>

- <span data-ttu-id="717ce-114">執行原始 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="717ce-114">Performing raw SQL queries.</span></span>
- <span data-ttu-id="717ce-115">執行沒有追蹤的查詢。</span><span class="sxs-lookup"><span data-stu-id="717ce-115">Performing no-tracking queries.</span></span>
- <span data-ttu-id="717ce-116">檢查傳送至資料庫的查詢。</span><span class="sxs-lookup"><span data-stu-id="717ce-116">Examining queries sent to the database.</span></span>
- <span data-ttu-id="717ce-117">使用 proxy 類別。</span><span class="sxs-lookup"><span data-stu-id="717ce-117">Working with proxy classes.</span></span>
- <span data-ttu-id="717ce-118">停用變更的自動偵測。</span><span class="sxs-lookup"><span data-stu-id="717ce-118">Disabling automatic detection of changes.</span></span>
- <span data-ttu-id="717ce-119">儲存變更時停用驗證。</span><span class="sxs-lookup"><span data-stu-id="717ce-119">Disabling validation when saving changes.</span></span>
- [<span data-ttu-id="717ce-120">錯誤和解決辦法</span><span class="sxs-lookup"><span data-stu-id="717ce-120">Errors and Work Arounds</span></span>](#errors)

<span data-ttu-id="717ce-121">在這些主題中，您將會使用您已建立的頁面。</span><span class="sxs-lookup"><span data-stu-id="717ce-121">For most of these topics, you'll work with pages that you already created.</span></span> <span data-ttu-id="717ce-122">若要使用原始 SQL 進行大量更新，您將會建立新的頁面，以更新資料庫中所有課程的信用額度數：</span><span class="sxs-lookup"><span data-stu-id="717ce-122">To use raw SQL to do bulk updates you'll create a new page that updates the number of credits of all courses in the database:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="717ce-124">若要使用沒有追蹤的查詢，您必須將新的驗證邏輯新增至部門的 [編輯] 頁面：</span><span class="sxs-lookup"><span data-stu-id="717ce-124">And to use a no-tracking query you'll add new validation logic to the Department Edit page:</span></span>

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a><span data-ttu-id="717ce-126">執行原始 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="717ce-126">Performing Raw SQL Queries</span></span>

<span data-ttu-id="717ce-127">Entity Framework Code First API 包括可讓您直接將 SQL 命令傳遞至資料庫的方法。</span><span class="sxs-lookup"><span data-stu-id="717ce-127">The Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="717ce-128">您有下列選項：</span><span class="sxs-lookup"><span data-stu-id="717ce-128">You have the following options:</span></span>

- <span data-ttu-id="717ce-129">針對傳回實體類型的查詢使用 `DbSet.SqlQuery` 方法。</span><span class="sxs-lookup"><span data-stu-id="717ce-129">Use the `DbSet.SqlQuery` method for queries that return entity types.</span></span> <span data-ttu-id="717ce-130">傳回的物件必須是物件所預期的類型 `DbSet` ，而且資料庫內容會自動追蹤它們，除非您關閉追蹤。</span><span class="sxs-lookup"><span data-stu-id="717ce-130">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you turn tracking off.</span></span> <span data-ttu-id="717ce-131"> (請參閱下列有關方法的章節 `AsNoTracking` 。 ) </span><span class="sxs-lookup"><span data-stu-id="717ce-131">(See the following section about the `AsNoTracking` method.)</span></span>
- <span data-ttu-id="717ce-132">針對傳回 `Database.SqlQuery` 不是實體之類型的查詢，請使用方法。</span><span class="sxs-lookup"><span data-stu-id="717ce-132">Use the `Database.SqlQuery` method for queries that return types that aren't entities.</span></span> <span data-ttu-id="717ce-133">即使您使用這個方法來擷取實體類型，資料庫內容也不會追蹤傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="717ce-133">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>
- <span data-ttu-id="717ce-134">針對非查詢命令使用[Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) 。</span><span class="sxs-lookup"><span data-stu-id="717ce-134">Use the [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) for non-query commands.</span></span>

<span data-ttu-id="717ce-135">使用 Entity Framework 的優點之一，是它可避免將程式碼繫結至太接近儲存資料之特定方法的位置。</span><span class="sxs-lookup"><span data-stu-id="717ce-135">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="717ce-136">它可透過產生 SQL 查詢和命令來達成此目的，同時這也可讓您不必自行撰寫。</span><span class="sxs-lookup"><span data-stu-id="717ce-136">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="717ce-137">但在某些情況下，您需要執行手動建立的特定 SQL 查詢，而且這些方法可以讓您處理這類例外狀況。</span><span class="sxs-lookup"><span data-stu-id="717ce-137">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created, and these methods make it possible for you to handle such exceptions.</span></span>

<span data-ttu-id="717ce-138">如同在 Web 應用程式中執行 SQL 命令一樣，您必須採取一些預防措施，以保護您的網站免於遭受 SQL 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="717ce-138">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="717ce-139">執行這項操作的方法之一是使用參數化查詢，以確定網頁所提交的字串無法解譯為 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="717ce-139">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="717ce-140">在本教學課程中，您會在將使用者輸入整合到查詢時，使用參數化查詢。</span><span class="sxs-lookup"><span data-stu-id="717ce-140">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

### <a name="calling-a-query-that-returns-entities"></a><span data-ttu-id="717ce-141">呼叫傳回實體的查詢</span><span class="sxs-lookup"><span data-stu-id="717ce-141">Calling a Query that Returns Entities</span></span>

<span data-ttu-id="717ce-142">假設您想要讓 `GenericRepository` 類別提供額外的篩選和排序彈性，而不需要您使用其他方法建立衍生類別。</span><span class="sxs-lookup"><span data-stu-id="717ce-142">Suppose you want the `GenericRepository` class to provide additional filtering and sorting flexibility without requiring that you create a derived class with additional methods.</span></span> <span data-ttu-id="717ce-143">達成此目標的其中一種方法是新增可接受 SQL 查詢的方法。</span><span class="sxs-lookup"><span data-stu-id="717ce-143">One way to achieve that would be to add a method that accepts a SQL query.</span></span> <span data-ttu-id="717ce-144">接著，您可以在控制器中指定您想要的任何一種篩選或排序，例如 `Where` 相依于聯結或子查詢的子句。</span><span class="sxs-lookup"><span data-stu-id="717ce-144">You could then specify any kind of filtering or sorting you want in the controller, such as a `Where` clause that depends on a joins or a subquery.</span></span> <span data-ttu-id="717ce-145">在本節中，您將瞭解如何執行這種方法。</span><span class="sxs-lookup"><span data-stu-id="717ce-145">In this section you'll see how to implement such a method.</span></span>

<span data-ttu-id="717ce-146">`GetWithRawSql`將下列程式碼新增至*GenericRepository.cs*，以建立方法：</span><span class="sxs-lookup"><span data-stu-id="717ce-146">Create the `GetWithRawSql` method by adding the following code to *GenericRepository.cs*:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

<span data-ttu-id="717ce-147">在*CourseController.cs*中，從方法呼叫新的方法 `Details` ，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="717ce-147">In *CourseController.cs*, call the new method from the `Details` method, as shown in the following example:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

<span data-ttu-id="717ce-148">在此情況下，您可以使用 `GetByID` 方法，但是您會使用 `GetWithRawSql` 方法來驗證 `GetWithRawSQL` 方法是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="717ce-148">In this case you could have used the `GetByID` method, but you're using the `GetWithRawSql` method to verify that the `GetWithRawSQL` method works.</span></span>

<span data-ttu-id="717ce-149">執行 [詳細資料] 頁面，確認 select 查詢是否正常運作 (選取 [**課程**] 索引標籤，然後) 的 [**詳細資料**]。</span><span class="sxs-lookup"><span data-stu-id="717ce-149">Run the Details page to verify that the select query works (select the **Course** tab and then **Details** for one course).</span></span>

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a><span data-ttu-id="717ce-151">呼叫傳回其他類型之物件的查詢</span><span class="sxs-lookup"><span data-stu-id="717ce-151">Calling a Query that Returns Other Types of Objects</span></span>

<span data-ttu-id="717ce-152">先前您已針對顯示每個註冊日期之學生數目的 About 頁面，建立學生統計資料方格。</span><span class="sxs-lookup"><span data-stu-id="717ce-152">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="717ce-153">在*HomeController.cs*中執行此動作的程式碼會使用 LINQ：</span><span class="sxs-lookup"><span data-stu-id="717ce-153">The code that does this in *HomeController.cs* uses LINQ:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

<span data-ttu-id="717ce-154">假設您想要撰寫程式碼，直接在 SQL 中抓取這項資料，而不是使用 LINQ。</span><span class="sxs-lookup"><span data-stu-id="717ce-154">Suppose you want to write the code that retrieves this data directly in SQL rather than using LINQ.</span></span> <span data-ttu-id="717ce-155">若要這麼做，您必須執行查詢來傳回實體物件以外的專案，這表示您需要使用 `Database.SqlQuery` 方法。</span><span class="sxs-lookup"><span data-stu-id="717ce-155">To do that you need to run a query that returns something other than entity objects, which means you need to use the `Database.SqlQuery` method.</span></span>

<span data-ttu-id="717ce-156">在*HomeController.cs*中，將方法中的 LINQ 語句取代 `About` 為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="717ce-156">In *HomeController.cs*, replace the LINQ statement in the `About` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

<span data-ttu-id="717ce-157">執行 [關於] 頁面。</span><span class="sxs-lookup"><span data-stu-id="717ce-157">Run the About page.</span></span> <span data-ttu-id="717ce-158">它會顯示與之前相同的資料。</span><span class="sxs-lookup"><span data-stu-id="717ce-158">It displays the same data it did before.</span></span>

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a><span data-ttu-id="717ce-160">呼叫更新查詢</span><span class="sxs-lookup"><span data-stu-id="717ce-160">Calling an Update Query</span></span>

<span data-ttu-id="717ce-161">假設 Contoso 大學系統管理員想要能夠在資料庫中執行大量變更，例如變更每個課程的信用額度數。</span><span class="sxs-lookup"><span data-stu-id="717ce-161">Suppose Contoso University administrators want to be able to perform bulk changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="717ce-162">如果該大學有大量的課程，擷取全部課程作為實體並個別進行變更的效率不佳。</span><span class="sxs-lookup"><span data-stu-id="717ce-162">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="717ce-163">在本節中，您將會執行一個網頁，讓使用者指定一個因素來變更所有課程的信用額度數目，而您會藉由執行 SQL 語句來進行變更 `UPDATE` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-163">In this section you'll implement a web page that allows the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL `UPDATE` statement.</span></span> <span data-ttu-id="717ce-164">網頁看起來將如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="717ce-164">The web page will look like the following illustration:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

<span data-ttu-id="717ce-166">在上一個教學課程中，您使用了一般存放庫來讀取和更新 `Course` 控制器中的實體 `Course` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-166">In the previous tutorial you used the generic repository to read and update `Course` entities in the `Course` controller.</span></span> <span data-ttu-id="717ce-167">針對此大量更新作業，您需要建立不在一般存放庫中的新存放庫方法。</span><span class="sxs-lookup"><span data-stu-id="717ce-167">For this bulk update operation, you need to create a new repository method that isn't in the generic repository.</span></span> <span data-ttu-id="717ce-168">若要這麼做，您將建立 `CourseRepository` 衍生自類別的專用類別 `GenericRepository` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-168">To do that, you'll create a dedicated `CourseRepository` class that derives from the `GenericRepository` class.</span></span>

<span data-ttu-id="717ce-169">在*DAL*資料夾中，建立*CourseRepository.cs* ，並將現有的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="717ce-169">In the *DAL* folder, create *CourseRepository.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

<span data-ttu-id="717ce-170">在*UnitOfWork.cs*中，將存放 `Course` 庫類型從變更 `GenericRepository<Course>` 為`CourseRepository:`</span><span class="sxs-lookup"><span data-stu-id="717ce-170">In *UnitOfWork.cs*, change the `Course` repository type from `GenericRepository<Course>` to `CourseRepository:`</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

<span data-ttu-id="717ce-171">在*CourseController.cs*中，新增 `UpdateCourseCredits` 方法：</span><span class="sxs-lookup"><span data-stu-id="717ce-171">In *CourseController.cs*, add an `UpdateCourseCredits` method:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

<span data-ttu-id="717ce-172">這個方法將同時用於 `HttpGet` 和 `HttpPost` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-172">This method will be used for both `HttpGet` and `HttpPost`.</span></span> <span data-ttu-id="717ce-173">當 `HttpGet` `UpdateCourseCredits` 方法執行時， `multiplier` 變數會是 null，而且此視圖會顯示空白的文字方塊和 [提交] 按鈕，如上圖所示。</span><span class="sxs-lookup"><span data-stu-id="717ce-173">When the `HttpGet` `UpdateCourseCredits` method runs, the `multiplier` variable will be null and the view will display an empty text box and a submit button, as shown in the preceding illustration.</span></span>

<span data-ttu-id="717ce-174">按一下 [**更新**] 按鈕並 `HttpPost` 執行方法時， `multiplier` 將會在文字方塊中輸入值。</span><span class="sxs-lookup"><span data-stu-id="717ce-174">When the **Update** button is clicked and the `HttpPost` method runs, `multiplier` will have the value entered in the text box.</span></span> <span data-ttu-id="717ce-175">然後，程式碼會呼叫儲存機制 `UpdateCourseCredits` 方法，這會傳回受影響的資料列數目，而該值會儲存在 `ViewBag` 物件中。</span><span class="sxs-lookup"><span data-stu-id="717ce-175">The code then calls the repository `UpdateCourseCredits` method, which returns the number of affected rows, and that value is stored in the `ViewBag` object.</span></span> <span data-ttu-id="717ce-176">當此視圖收到物件中受影響的資料列數目時 `ViewBag` ，它會顯示該數位，而不是文字方塊和提交按鈕，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="717ce-176">When the view receives the number of affected rows in the `ViewBag` object, it displays that number instead of the text box and submit button, as shown in the following illustration:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

<span data-ttu-id="717ce-178">在 [更新課程信用額度] 頁面的 [ *Views\Course* ] 資料夾中建立一個視圖：</span><span class="sxs-lookup"><span data-stu-id="717ce-178">Create a view in the *Views\Course* folder for the Update Course Credits page:</span></span>

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

<span data-ttu-id="717ce-180">在*Views\Course\UpdateCourseCredits.cshtml*中，將範本程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="717ce-180">In *Views\Course\UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

<span data-ttu-id="717ce-181">藉由選取 [課程] \*\*\*\* 索引標籤，然後將 "/UpdateCourseCredits" 新增至瀏覽器位址列中的 URL 結尾 (例如：`http://localhost:50205/Course/UpdateCourseCredits`)，以執行 `UpdateCourseCredits` 方法。</span><span class="sxs-lookup"><span data-stu-id="717ce-181">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:50205/Course/UpdateCourseCredits`).</span></span> <span data-ttu-id="717ce-182">在文字方塊中輸入數目：</span><span class="sxs-lookup"><span data-stu-id="717ce-182">Enter a number in the text box:</span></span>

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

<span data-ttu-id="717ce-184">按一下 [更新]  。</span><span class="sxs-lookup"><span data-stu-id="717ce-184">Click **Update**.</span></span> <span data-ttu-id="717ce-185">您會看到受影響的資料列數目：</span><span class="sxs-lookup"><span data-stu-id="717ce-185">You see the number of rows affected:</span></span>

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

<span data-ttu-id="717ce-187">按一下 [回到清單]\*\*\*\*，以查看課程與已修訂學分數的清單。</span><span class="sxs-lookup"><span data-stu-id="717ce-187">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

<span data-ttu-id="717ce-189">如需原始 SQL 查詢的詳細資訊，請參閱 Entity Framework 小組 blog 上的[原始 Sql 查詢](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx)。</span><span class="sxs-lookup"><span data-stu-id="717ce-189">For more information about raw SQL queries, see [Raw SQL Queries](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) on the Entity Framework team blog.</span></span>

## <a name="no-tracking-queries"></a><span data-ttu-id="717ce-190">不追蹤的查詢</span><span class="sxs-lookup"><span data-stu-id="717ce-190">No-Tracking Queries</span></span>

<span data-ttu-id="717ce-191">當資料庫內容抓取資料庫資料列並建立代表它們的實體物件時，根據預設，它會追蹤記憶體中的實體是否與資料庫中的專案同步。</span><span class="sxs-lookup"><span data-stu-id="717ce-191">When a database context retrieves database rows and creates entity objects that represent them, by default it keeps track of whether the entities in memory are in sync with what's in the database.</span></span> <span data-ttu-id="717ce-192">記憶體中的資料所扮演的角色是一個快取，並會在您更新實體時使用。</span><span class="sxs-lookup"><span data-stu-id="717ce-192">The data in memory acts as a cache and is used when you update an entity.</span></span> <span data-ttu-id="717ce-193">這個快取通常在 Web 應用程式當中是不需要的，因為內容執行個體通常壽命都很短 (每次要求都會建立一個新的並進行處置)，並且通常讀取實體的內容都會在實體重新獲得利用前遭到處置。</span><span class="sxs-lookup"><span data-stu-id="717ce-193">This caching is often unnecessary in a web application because context instances are typically short-lived (a new one is created and disposed for each request) and the context that reads an entity is typically disposed before that entity is used again.</span></span>

<span data-ttu-id="717ce-194">您可以使用方法，指定內容是否追蹤查詢的實體物件 `AsNoTracking` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-194">You can specify whether the context tracks entity objects for a query by using the `AsNoTracking` method.</span></span> <span data-ttu-id="717ce-195">您會想要進行這項操作的常見案例包括下列情況：</span><span class="sxs-lookup"><span data-stu-id="717ce-195">Typical scenarios in which you might want to do that include the following:</span></span>

- <span data-ttu-id="717ce-196">此查詢會抓取關閉追蹤的大量資料，可能會明顯地提升效能。</span><span class="sxs-lookup"><span data-stu-id="717ce-196">The query retrieves such a large volume of data that turning off tracking might noticeably enhance performance.</span></span>
- <span data-ttu-id="717ce-197">您想要附加實體以進行更新，但您先前已針對不同目的抓取相同的實體。</span><span class="sxs-lookup"><span data-stu-id="717ce-197">You want to attach an entity in order to update it, but you earlier retrieved the same entity for a different purpose.</span></span> <span data-ttu-id="717ce-198">由於實體已由資料庫內容進行追蹤，您無法連結到您想要變更的實體。</span><span class="sxs-lookup"><span data-stu-id="717ce-198">Because the entity is already being tracked by the database context, you can't attach the entity that you want to change.</span></span> <span data-ttu-id="717ce-199">避免發生這種情況的其中一種方式，就是使用 `AsNoTracking` 選項搭配先前的查詢。</span><span class="sxs-lookup"><span data-stu-id="717ce-199">One way to prevent this from happening is to use the `AsNoTracking` option with the earlier query.</span></span>

<span data-ttu-id="717ce-200">在本節中，您將會執行商務邏輯，以說明其中的第二個案例。</span><span class="sxs-lookup"><span data-stu-id="717ce-200">In this section you'll implement business logic that illustrates the second of these scenarios.</span></span> <span data-ttu-id="717ce-201">具體來說，您將會強制執行商務規則，指出講師不能是一個以上部門的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="717ce-201">Specifically, you'll enforce a business rule that says that an instructor can't be the administrator of more than one department.</span></span>

<span data-ttu-id="717ce-202">在*DepartmentController.cs*中，新增可從和方法呼叫的新方法 `Edit` ， `Create` 以確定沒有任何兩個部門具有相同的系統管理員：</span><span class="sxs-lookup"><span data-stu-id="717ce-202">In *DepartmentController.cs*, add a new method that you can call from the `Edit` and `Create` methods to make sure that no two departments have the same administrator:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

<span data-ttu-id="717ce-203">如果沒有驗證錯誤，請在方法的區塊中加入程式碼 `try` `HttpPost` `Edit` ，以呼叫這個新的方法。</span><span class="sxs-lookup"><span data-stu-id="717ce-203">Add code in the `try` block of the `HttpPost` `Edit` method to call this new method if there are no validation errors.</span></span> <span data-ttu-id="717ce-204">此 `try` 區塊現在看起來如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="717ce-204">The `try` block now looks like the following example:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

<span data-ttu-id="717ce-205">執行部門 [編輯] 頁面，然後嘗試將部門的系統管理員變更為已經是不同部門之系統管理員的講師。</span><span class="sxs-lookup"><span data-stu-id="717ce-205">Run the Department Edit page and try to change a department's administrator to an instructor who is already the administrator of a different department.</span></span> <span data-ttu-id="717ce-206">您會收到預期的錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="717ce-206">You get the expected error message:</span></span>

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

<span data-ttu-id="717ce-208">現在，再次執行 [部門編輯] 頁面，這次變更**預算**金額。</span><span class="sxs-lookup"><span data-stu-id="717ce-208">Now run the Department Edit page again and this time change the **Budget** amount.</span></span> <span data-ttu-id="717ce-209">當您按一下 [**儲存**] 時，您會看到錯誤頁面：</span><span class="sxs-lookup"><span data-stu-id="717ce-209">When you click **Save**, you see an error page:</span></span>

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

<span data-ttu-id="717ce-211">例外狀況錯誤訊息為「」， `An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.` 這是因為下列事件順序所導致：</span><span class="sxs-lookup"><span data-stu-id="717ce-211">The exception error message is "`An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.`" This happened because of the following sequence of events:</span></span>

- <span data-ttu-id="717ce-212">`Edit`方法 `ValidateOneAdministratorAssignmentPerInstructor` 會呼叫方法，它會抓取所有以 Kim Abercrombie 為其系統管理員的部門。</span><span class="sxs-lookup"><span data-stu-id="717ce-212">The `Edit` method calls the `ValidateOneAdministratorAssignmentPerInstructor` method, which retrieves all departments that have Kim Abercrombie as their administrator.</span></span> <span data-ttu-id="717ce-213">這會導致讀取英文部門。</span><span class="sxs-lookup"><span data-stu-id="717ce-213">That causes the English department to be read.</span></span> <span data-ttu-id="717ce-214">因為這是正在編輯的部門，所以不會回報任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="717ce-214">Because that's the department being edited, no error is reported.</span></span> <span data-ttu-id="717ce-215">不過，此讀取作業的結果是，從資料庫讀取的英文部門實體現在正由資料庫內容追蹤。</span><span class="sxs-lookup"><span data-stu-id="717ce-215">As a result of this read operation, however, the English department entity that was read from the database is now being tracked by the database context.</span></span>
- <span data-ttu-id="717ce-216">`Edit`方法 `Modified` 會嘗試在 MVC 模型系結器所建立的英文部門實體上設定旗標，但因為內容已經追蹤英文部門的實體，所以失敗。</span><span class="sxs-lookup"><span data-stu-id="717ce-216">The `Edit` method tries to set the `Modified` flag on the English department entity created by the MVC model binder, but that fails because the context is already tracking an entity for the English department.</span></span>

<span data-ttu-id="717ce-217">這個問題的解決方法之一，是要讓內容免于追蹤驗證查詢所抓取的記憶體中部門實體。</span><span class="sxs-lookup"><span data-stu-id="717ce-217">One solution to this problem is to keep the context from tracking in-memory department entities retrieved by the validation query.</span></span> <span data-ttu-id="717ce-218">這麼做並沒有任何缺點，因為您將不會更新此實體，或以可從記憶體快取中獲益的方式再次讀取它。</span><span class="sxs-lookup"><span data-stu-id="717ce-218">There's no disadvantage to doing this, because you won't be updating this entity or reading it again in a way that would benefit from it being cached in memory.</span></span>

<span data-ttu-id="717ce-219">在*DepartmentController.cs*的方法中， `ValidateOneAdministratorAssignmentPerInstructor` 指定 [無追蹤]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="717ce-219">In *DepartmentController.cs*, in the `ValidateOneAdministratorAssignmentPerInstructor` method, specify no tracking, as shown in the following:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

<span data-ttu-id="717ce-220">重複嘗試編輯部門的**預算**金額。</span><span class="sxs-lookup"><span data-stu-id="717ce-220">Repeat your attempt to edit the **Budget** amount of a department.</span></span> <span data-ttu-id="717ce-221">這次作業會成功，而且網站會如預期般返回 [部門索引] 頁面，其中顯示修訂的預算值。</span><span class="sxs-lookup"><span data-stu-id="717ce-221">This time the operation is successful, and the site returns as expected to the Departments Index page, showing the revised budget value.</span></span>

## <a name="examining-queries-sent-to-the-database"></a><span data-ttu-id="717ce-222">檢查傳送至資料庫的查詢</span><span class="sxs-lookup"><span data-stu-id="717ce-222">Examining Queries Sent to the Database</span></span>

<span data-ttu-id="717ce-223">有時能夠看到傳送至資料庫的實際 SQL 查詢很有幫助。</span><span class="sxs-lookup"><span data-stu-id="717ce-223">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="717ce-224">若要這樣做，您可以在偵錯工具中檢查查詢變數，或呼叫查詢的 `ToString` 方法。</span><span class="sxs-lookup"><span data-stu-id="717ce-224">To do this, you can examine a query variable in the debugger or call the query's `ToString` method.</span></span> <span data-ttu-id="717ce-225">若要試試看，您將會看到一個簡單的查詢，然後查看當您加入積極式載入、篩選和排序等選項時，會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="717ce-225">To try this out, you'll look at a simple query and then look at what happens to it as you add options such eager loading, filtering, and sorting.</span></span>

<span data-ttu-id="717ce-226">在*控制器/CourseController*中，將 `Index` 方法取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="717ce-226">In *Controllers/CourseController*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

<span data-ttu-id="717ce-227">現在，在和方法的語句上設定*GenericRepository.cs*中的中斷點 `return query.ToList();` `return orderBy(query).ToList();` `Get` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-227">Now set a breakpoint in *GenericRepository.cs* on the `return query.ToList();` and the `return orderBy(query).ToList();` statements of the `Get` method.</span></span> <span data-ttu-id="717ce-228">在 [偵錯模式] 中執行專案，然後選取 [課程索引] 頁面。</span><span class="sxs-lookup"><span data-stu-id="717ce-228">Run the project in debug mode and select the Course Index page.</span></span> <span data-ttu-id="717ce-229">當程式碼到達中斷點時，請檢查 `query` 變數。</span><span class="sxs-lookup"><span data-stu-id="717ce-229">When the code reaches the breakpoint, examine the `query` variable.</span></span> <span data-ttu-id="717ce-230">您會看到傳送至 SQL Server 的查詢。</span><span class="sxs-lookup"><span data-stu-id="717ce-230">You see the query that's sent to SQL Server.</span></span> <span data-ttu-id="717ce-231">這是一個簡單的 `Select` 語句：</span><span class="sxs-lookup"><span data-stu-id="717ce-231">It's a simple `Select` statement:</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.json)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

<span data-ttu-id="717ce-232">查詢可能太長，無法在 Visual Studio 的調試視窗中顯示。</span><span class="sxs-lookup"><span data-stu-id="717ce-232">Queries can be too long to display in the debugging windows in Visual Studio.</span></span> <span data-ttu-id="717ce-233">若要查看整個查詢，您可以複製變數值，並將它貼到文字編輯器中：</span><span class="sxs-lookup"><span data-stu-id="717ce-233">To see the entire query, you can copy the variable value and paste it into a text editor:</span></span>

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

<span data-ttu-id="717ce-235">現在您會將下拉式清單新增至 [課程索引] 頁面，讓使用者可以篩選特定部門。</span><span class="sxs-lookup"><span data-stu-id="717ce-235">Now you'll add a drop-down list to the Course Index page so that users can filter for a particular department.</span></span> <span data-ttu-id="717ce-236">您將依標題排序課程，並針對導覽屬性指定積極式載入 `Department` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-236">You'll sort the courses by title, and you'll specify eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="717ce-237">在*CourseController.cs*中，將 `Index` 方法取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="717ce-237">In *CourseController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

<span data-ttu-id="717ce-238">方法會在參數中接收所選下拉式清單的值 `SelectedDepartment` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-238">The method receives the selected value of the drop-down list in the `SelectedDepartment` parameter.</span></span> <span data-ttu-id="717ce-239">如果未選取任何內容，此參數將會是 null。</span><span class="sxs-lookup"><span data-stu-id="717ce-239">If nothing is selected, this parameter will be null.</span></span>

<span data-ttu-id="717ce-240">`SelectList`包含所有部門的集合會傳遞至下拉式清單的視圖。</span><span class="sxs-lookup"><span data-stu-id="717ce-240">A `SelectList` collection containing all departments is passed to the view for the drop-down list.</span></span> <span data-ttu-id="717ce-241">傳遞至此函式的參數會 `SelectList` 指定值功能變數名稱、文字功能變數名稱和選取的專案。</span><span class="sxs-lookup"><span data-stu-id="717ce-241">The parameters passed to the `SelectList` constructor specify the value field name, the text field name, and the selected item.</span></span>

<span data-ttu-id="717ce-242">針對存放 `Get` 庫的方法 `Course` ，程式碼會針對導覽屬性指定篩選條件運算式、排序次序和積極式載入 `Department` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-242">For the `Get` method of the `Course` repository, the code specifies a filter expression, a sort order, and eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="717ce-243">`true`如果下拉式清單中未選取任何內容，則篩選運算式一律會傳回 (也就是 `SelectedDepartment` null) 。</span><span class="sxs-lookup"><span data-stu-id="717ce-243">The filter expression always returns `true` if nothing is selected in the drop-down list (that is, `SelectedDepartment` is null).</span></span>

<span data-ttu-id="717ce-244">在*Views\Course\Index.cshtml*中，于開頭標記的正後方 `table` 新增下列程式碼，以建立下拉式清單和提交按鈕：</span><span class="sxs-lookup"><span data-stu-id="717ce-244">In *Views\Course\Index.cshtml*, immediately before the opening `table` tag, add the following code to create the drop-down list and a submit button:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

<span data-ttu-id="717ce-245">在類別中仍設定中斷點後 `GenericRepository` ，請執行 [課程索引] 頁面。</span><span class="sxs-lookup"><span data-stu-id="717ce-245">With the breakpoints still set in the `GenericRepository` class, run the Course Index page.</span></span> <span data-ttu-id="717ce-246">繼續執行程式碼叫用中斷點的前兩次，以便在瀏覽器中顯示該頁面。</span><span class="sxs-lookup"><span data-stu-id="717ce-246">Continue through the first two times that the code hits a breakpoint, so that the page is displayed in the browser.</span></span> <span data-ttu-id="717ce-247">從下拉式清單中選取部門，然後按一下 [**篩選**]：</span><span class="sxs-lookup"><span data-stu-id="717ce-247">Select a department from the drop-down list and click **Filter**:</span></span>

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

<span data-ttu-id="717ce-249">這次，第一個中斷點將會是 [部門] 查詢的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="717ce-249">This time the first breakpoint will be for the departments query for the drop-down list.</span></span> <span data-ttu-id="717ce-250">在 `query` 下一次程式碼到達中斷點時略過，並查看變數，以查看查詢的 `Course` 樣子。</span><span class="sxs-lookup"><span data-stu-id="717ce-250">Skip that and view the `query` variable the next time the code reaches the breakpoint in order to see what the `Course` query now looks like.</span></span> <span data-ttu-id="717ce-251">您會看到如下所示的內容：</span><span class="sxs-lookup"><span data-stu-id="717ce-251">You'll see something like the following:</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.json)]

<span data-ttu-id="717ce-252">您可以看到查詢現在是一種會 `JOIN` 載入資料以及 `Department` `Course` 資料的查詢，而且它包含 `WHERE` 子句。</span><span class="sxs-lookup"><span data-stu-id="717ce-252">You can see that the query is now a `JOIN` query that loads `Department` data along with the `Course` data, and that it includes a `WHERE` clause.</span></span>

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a><span data-ttu-id="717ce-253">使用 Proxy 類別</span><span class="sxs-lookup"><span data-stu-id="717ce-253">Working with Proxy Classes</span></span>

<span data-ttu-id="717ce-254">當 Entity Framework 建立實體實例時 (例如，當您執行查詢) 時，通常會將其建立為動態產生之衍生型別的實例，作為實體的 proxy。</span><span class="sxs-lookup"><span data-stu-id="717ce-254">When the Entity Framework creates entity instances (for example, when you execute a query), it often creates them as instances of a dynamically generated derived type that acts as a proxy for the entity.</span></span> <span data-ttu-id="717ce-255">此 proxy 會覆寫實體的某些虛擬屬性，以插入在存取屬性時自動執行動作的勾點。</span><span class="sxs-lookup"><span data-stu-id="717ce-255">This proxy overrides some virtual properties of the entity to insert hooks for performing actions automatically when the property is accessed.</span></span> <span data-ttu-id="717ce-256">例如，這項機制是用來支援延遲載入關聯性。</span><span class="sxs-lookup"><span data-stu-id="717ce-256">For example, this mechanism is used to support lazy loading of relationships.</span></span>

<span data-ttu-id="717ce-257">在大部分的情況下，您不需要知道此 proxy 的使用方式，但有一些例外狀況：</span><span class="sxs-lookup"><span data-stu-id="717ce-257">Most of the time you don't need to be aware of this use of proxies, but there are exceptions:</span></span>

- <span data-ttu-id="717ce-258">在某些情況下，您可能會想要防止 Entity Framework 建立 proxy 實例。</span><span class="sxs-lookup"><span data-stu-id="717ce-258">In some scenarios you might want to prevent the Entity Framework from creating proxy instances.</span></span> <span data-ttu-id="717ce-259">例如，序列化非 proxy 實例可能會比序列化 proxy 實例更有效率。</span><span class="sxs-lookup"><span data-stu-id="717ce-259">For example, serializing non-proxy instances might be more efficient than serializing proxy instances.</span></span>
- <span data-ttu-id="717ce-260">當您使用運算子來具現化實體類別時 `new` ，您不會取得 proxy 實例。</span><span class="sxs-lookup"><span data-stu-id="717ce-260">When you instantiate an entity class using the `new` operator, you don't get a proxy instance.</span></span> <span data-ttu-id="717ce-261">這表示您不會取得延遲載入和自動變更追蹤之類的功能。</span><span class="sxs-lookup"><span data-stu-id="717ce-261">This means you don't get functionality such as lazy loading and automatic change tracking.</span></span> <span data-ttu-id="717ce-262">這通常沒什麼問題;您通常不需要消極式載入，因為您正在建立不在資料庫中的新實體，而且如果您將實體明確標示為，則通常不需要變更追蹤 `Added` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-262">This is typically okay; you generally don't need lazy loading, because you're creating a new entity that isn't in the database, and you generally don't need change tracking if you're explicitly marking the entity as `Added`.</span></span> <span data-ttu-id="717ce-263">不過，如果您需要消極式載入，而且需要變更追蹤，您可以使用類別的方法來建立具有 proxy 的新實體實例 `Create` `DbSet` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-263">However, if you do need lazy loading and you need change tracking, you can create new entity instances with proxies using the `Create` method of the `DbSet` class.</span></span>
- <span data-ttu-id="717ce-264">您可能想要從 proxy 類型取得實際的實體類型。</span><span class="sxs-lookup"><span data-stu-id="717ce-264">You might want to get an actual entity type from a proxy type.</span></span> <span data-ttu-id="717ce-265">您可以使用 `GetObjectType` 類別的方法 `ObjectContext` 來取得 proxy 類型實例的實際實體類型。</span><span class="sxs-lookup"><span data-stu-id="717ce-265">You can use the `GetObjectType` method of the `ObjectContext` class to get the actual entity type of a proxy type instance.</span></span>

<span data-ttu-id="717ce-266">如需詳細資訊，[請參閱在](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx)Entity Framework 小組的 blog 上使用 proxy。</span><span class="sxs-lookup"><span data-stu-id="717ce-266">For more information, see [Working with Proxies](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) on the Entity Framework team blog.</span></span>

## <a name="disabling-automatic-detection-of-changes"></a><span data-ttu-id="717ce-267">停用變更的自動偵測</span><span class="sxs-lookup"><span data-stu-id="717ce-267">Disabling Automatic Detection of Changes</span></span>

<span data-ttu-id="717ce-268">Entity Framework 藉由比較實體的目前值與原始值，判斷實體如何變更 (以及因此需要將哪些更新傳送至資料庫)。</span><span class="sxs-lookup"><span data-stu-id="717ce-268">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="717ce-269">查詢或附加實體時，會儲存原始值。</span><span class="sxs-lookup"><span data-stu-id="717ce-269">The original values are stored when the entity was queried or attached.</span></span> <span data-ttu-id="717ce-270">會導致自動變更偵測的一些方法如下：</span><span class="sxs-lookup"><span data-stu-id="717ce-270">Some of the methods that cause automatic change detection are the following:</span></span>

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

<span data-ttu-id="717ce-271">如果您要追蹤大量實體，並在迴圈中多次呼叫其中一種方法，您可以使用[AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx)屬性暫時關閉自動變更偵測，以獲得顯著的效能改進。</span><span class="sxs-lookup"><span data-stu-id="717ce-271">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) property.</span></span> <span data-ttu-id="717ce-272">如需詳細資訊，請參閱[自動偵測變更](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx)。</span><span class="sxs-lookup"><span data-stu-id="717ce-272">For more information, see [Automatically Detecting Changes](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx).</span></span>

## <a name="disabling-validation-when-saving-changes"></a><span data-ttu-id="717ce-273">儲存變更時停用驗證</span><span class="sxs-lookup"><span data-stu-id="717ce-273">Disabling Validation When Saving Changes</span></span>

<span data-ttu-id="717ce-274">當您呼叫 `SaveChanges` 方法時，根據預設，Entity Framework 會在更新資料庫之前，先驗證所有已變更實體的所有屬性中的資料。</span><span class="sxs-lookup"><span data-stu-id="717ce-274">When you call the `SaveChanges` method, by default the Entity Framework validates the data in all properties of all changed entities before updating the database.</span></span> <span data-ttu-id="717ce-275">如果您已更新大量實體，而且您已經驗證過資料，這是不必要的工作，而且您可以暫時關閉驗證，讓儲存變更的程式更少時間。</span><span class="sxs-lookup"><span data-stu-id="717ce-275">If you've updated a large number of entities and you've already validated the data, this work is unnecessary and you could make the process of saving the changes take less time by temporarily turning off validation.</span></span> <span data-ttu-id="717ce-276">您可以使用[ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx)屬性來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="717ce-276">You can do that using the [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) property.</span></span> <span data-ttu-id="717ce-277">如需詳細資訊，請參閱[驗證](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx)。</span><span class="sxs-lookup"><span data-stu-id="717ce-277">For more information, see [Validation](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="717ce-278">摘要</span><span class="sxs-lookup"><span data-stu-id="717ce-278">Summary</span></span>

<span data-ttu-id="717ce-279">這會完成這一系列的教學課程，以在 ASP.NET MVC 應用程式中使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="717ce-279">This completes this series of tutorials on using the Entity Framework in an ASP.NET MVC application.</span></span> <span data-ttu-id="717ce-280">您可以在[ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="717ce-280">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="717ce-281">如需有關如何在建立 web 應用程式之後進行部署的詳細資訊，請參閱 MSDN Library 中的[ASP.NET 部署內容對應](https://msdn.microsoft.com/library/bb386521.aspx)。</span><span class="sxs-lookup"><span data-stu-id="717ce-281">For more information about how to deploy your web application after you've built it, see [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx) in the MSDN Library.</span></span>

<span data-ttu-id="717ce-282">如需與 MVC 相關之其他主題（例如驗證和授權）的詳細資訊，請參閱[Mvc 建議資源](../../getting-started/recommended-resources-for-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="717ce-282">For information about other topics related to MVC, such as authentication and authorization, see the [MVC Recommended Resources](../../getting-started/recommended-resources-for-mvc.md).</span></span>

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a><span data-ttu-id="717ce-283">通知</span><span class="sxs-lookup"><span data-stu-id="717ce-283">Acknowledgments</span></span>

- <span data-ttu-id="717ce-284">Tom 作者: dykstra 已撰寫本教學課程的原始版本，而且是 Microsoft Web Platform 和 Tools 內容小組的資深程式設計作者。</span><span class="sxs-lookup"><span data-stu-id="717ce-284">Tom Dykstra wrote the original version of this tutorial and is a senior programming writer on the Microsoft Web Platform and Tools Content Team.</span></span>
- <span data-ttu-id="717ce-285">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) 共同撰寫本教學課程，而且大部分的工作都是針對 EF 5 和 MVC 4 進行更新。</span><span class="sxs-lookup"><span data-stu-id="717ce-285">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) co-authored this tutorial and did most of the work updating it for EF 5 and MVC 4.</span></span> <span data-ttu-id="717ce-286">Rick 是 Microsoft 的資深程式設計作者，著重于 Azure 和 MVC。</span><span class="sxs-lookup"><span data-stu-id="717ce-286">Rick is a senior programming writer for Microsoft focusing on Azure and MVC.</span></span>
- <span data-ttu-id="717ce-287">[Rowan 莎莎](http://www.romiller.com)和 Entity Framework 小組的其他成員會協助程式碼審核，並協助您在更新 EF 5 的教學課程時所出現的許多遷移問題。</span><span class="sxs-lookup"><span data-stu-id="717ce-287">[Rowan Miller](http://www.romiller.com) and other members of the Entity Framework team assisted with code reviews and helped debug many issues with migrations that arose while we were updating the tutorial for EF 5.</span></span>

## <a name="vb"></a><span data-ttu-id="717ce-288">VB</span><span class="sxs-lookup"><span data-stu-id="717ce-288">VB</span></span>

<span data-ttu-id="717ce-289">最初產生教學課程時，我們提供了 c # 和 VB 版本的已完成下載專案。</span><span class="sxs-lookup"><span data-stu-id="717ce-289">When the tutorial was originally produced, we provided both C# and VB versions of the completed download project.</span></span> <span data-ttu-id="717ce-290">在此更新中，我們將為每個章節提供 c # 可下載的專案，讓您更輕鬆地開始使用系列中的任何位置，但由於時間限制和其他優先順序，我們並未針對 VB 進行這項作業。</span><span class="sxs-lookup"><span data-stu-id="717ce-290">With this update we are providing a C# downloadable project for each chapter to make it easier to get started anywhere in the series, but due to time limitations and other priorities we did not do that for VB.</span></span> <span data-ttu-id="717ce-291">如果您使用這些教學課程建立 VB 專案，而且願意與他人共用，請讓我們知道。</span><span class="sxs-lookup"><span data-stu-id="717ce-291">If you build a VB project using these tutorials and would be willing to share that with others, please let us know.</span></span>

<a id="errors"></a>

## <a name="errors-and-workarounds"></a><span data-ttu-id="717ce-292">錯誤和因應措施</span><span class="sxs-lookup"><span data-stu-id="717ce-292">Errors and Workarounds</span></span>

### <a name="cannot-createshadow-copy"></a><span data-ttu-id="717ce-293">無法建立/陰影複製</span><span class="sxs-lookup"><span data-stu-id="717ce-293">Cannot create/shadow copy</span></span>

<span data-ttu-id="717ce-294">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="717ce-294">Error Message:</span></span>

<span data-ttu-id="717ce-295">*當該檔案已存在時，無法建立/陰影複製 ' DotNetOpenAuth '。*</span><span class="sxs-lookup"><span data-stu-id="717ce-295">*Cannot create/shadow copy 'DotNetOpenAuth.OpenId' when that file already exists.*</span></span>

<span data-ttu-id="717ce-296">解決方案：</span><span class="sxs-lookup"><span data-stu-id="717ce-296">Solution:</span></span>

<span data-ttu-id="717ce-297">等候幾秒鐘，然後重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="717ce-297">Wait a few seconds and refresh the page.</span></span>

### <a name="update-database-not-recognized"></a><span data-ttu-id="717ce-298">更新-無法辨識資料庫</span><span class="sxs-lookup"><span data-stu-id="717ce-298">Update-Database not recognized</span></span>

<span data-ttu-id="717ce-299">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="717ce-299">Error Message:</span></span>

<span data-ttu-id="717ce-300">「*更新-資料庫」一詞無法辨識為 Cmdlet、函式、指令檔或可運作程式的名稱。請檢查名稱的拼寫，或如果已包含路徑，請確認路徑正確，然後再試一次。* 從 *`Update-Database`* PMC 中的命令 (。 ) </span><span class="sxs-lookup"><span data-stu-id="717ce-300">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*(From the *`Update-Database`* command in the PMC.)</span></span>

<span data-ttu-id="717ce-301">解決方案：</span><span class="sxs-lookup"><span data-stu-id="717ce-301">Solution:</span></span>

<span data-ttu-id="717ce-302">結束 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="717ce-302">Exit Visual Studio.</span></span> <span data-ttu-id="717ce-303">重新開啟專案，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="717ce-303">Reopen project and try again.</span></span>

### <a name="validation-failed"></a><span data-ttu-id="717ce-304">驗證失敗</span><span class="sxs-lookup"><span data-stu-id="717ce-304">Validation failed</span></span>

<span data-ttu-id="717ce-305">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="717ce-305">Error Message:</span></span>

<span data-ttu-id="717ce-306">*一或多個實體的驗證失敗。如需詳細資訊，請參閱 ' EntityValidationErrors ' 屬性。*</span><span class="sxs-lookup"><span data-stu-id="717ce-306">*Validation failed for one or more entities. See 'EntityValidationErrors' property for more details.*</span></span> <span data-ttu-id="717ce-307">從 *`Update-Database`* PMC 中的命令 (。 ) </span><span class="sxs-lookup"><span data-stu-id="717ce-307">(From the *`Update-Database`* command in the PMC.)</span></span>

<span data-ttu-id="717ce-308">解決方案：</span><span class="sxs-lookup"><span data-stu-id="717ce-308">Solution:</span></span>

<span data-ttu-id="717ce-309">此問題的其中一個原因是方法執行時的驗證錯誤 `Seed` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-309">One cause of this problem is validation errors when the `Seed` method runs.</span></span> <span data-ttu-id="717ce-310">如需有關偵測方法的秘訣，請參閱[植入和偵錯工具 Entity Framework (EF) db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) `Seed` 。</span><span class="sxs-lookup"><span data-stu-id="717ce-310">See [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) for tips on debugging the `Seed` method.</span></span>

### <a name="http-50019-error"></a><span data-ttu-id="717ce-311">HTTP 500.19 錯誤</span><span class="sxs-lookup"><span data-stu-id="717ce-311">HTTP 500.19 error</span></span>

<span data-ttu-id="717ce-312">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="717ce-312">Error Message:</span></span>

<span data-ttu-id="717ce-313">*HTTP 錯誤 500.19-內部伺服器錯誤：無法存取要求的網頁，因為該頁面的相關設定資料無效。*</span><span class="sxs-lookup"><span data-stu-id="717ce-313">*HTTP Error 500.19 - Internal Server Error The requested page cannot be accessed because the related configuration data for the page is invalid.*</span></span>

<span data-ttu-id="717ce-314">解決方案：</span><span class="sxs-lookup"><span data-stu-id="717ce-314">Solution:</span></span>

<span data-ttu-id="717ce-315">您可以取得此錯誤的其中一種方式是，使用相同的埠號碼，讓解決方案有多個複本。</span><span class="sxs-lookup"><span data-stu-id="717ce-315">One way you can get this error is from having multiple copies of the solution, each of them using the same port number.</span></span> <span data-ttu-id="717ce-316">您通常可以藉由結束 Visual Studio 的所有實例，然後重新開機您正在處理的專案，來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="717ce-316">You can usually solve this problem by exiting all instances of Visual Studio, then restarting the project your working on.</span></span> <span data-ttu-id="717ce-317">如果無法解決問題，請嘗試變更埠號碼。</span><span class="sxs-lookup"><span data-stu-id="717ce-317">If that doesn't work, try changing the port number.</span></span> <span data-ttu-id="717ce-318">以滑鼠右鍵按一下專案檔，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="717ce-318">Right click on the project file and then click properties.</span></span> <span data-ttu-id="717ce-319">選取 [ **Web** ] 索引標籤，然後在 [**專案 Url** ] 文字方塊中變更埠號碼。</span><span class="sxs-lookup"><span data-stu-id="717ce-319">Select the **Web** tab and then change the port number in the **Project Url** text box.</span></span>

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="717ce-320">搜尋 SQL Server 執行個體時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="717ce-320">Error locating SQL Server instance</span></span>

<span data-ttu-id="717ce-321">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="717ce-321">Error Message:</span></span>

<span data-ttu-id="717ce-322">\*建立與 SQL Server 的連接時發生網路相關或實例特定的錯誤。找不到或無法存取伺服器。請確認實例名稱是否正確，以及 SQL Server 是否設定為允許遠端連線。 (提供者： SQL 網路介面，錯誤： 26-尋找指定的伺服器/實例時發生錯誤) \*</span><span class="sxs-lookup"><span data-stu-id="717ce-322">*A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)*</span></span>

<span data-ttu-id="717ce-323">解決方案：</span><span class="sxs-lookup"><span data-stu-id="717ce-323">Solution:</span></span>

<span data-ttu-id="717ce-324">檢查連接字串。</span><span class="sxs-lookup"><span data-stu-id="717ce-324">Check connection string.</span></span> <span data-ttu-id="717ce-325">如果您已手動刪除資料庫，請在結構字串中變更資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="717ce-325">If you have manually deleted the database, change the name of the database in the construction string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="717ce-326">[上一個](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md) 
> [下一步](building-the-ef5-mvc4-chapter-downloads.md)</span><span class="sxs-lookup"><span data-stu-id="717ce-326">[Previous](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
[Next](building-the-ef5-mvc4-chapter-downloads.md)</span></span>
