---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用 ASP.NET MVC 應用程式中的 Entity Framework 進行排序、篩選和分頁 (3/10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 48938b378a741a0f1c351c2cb1d33b5140c6cf93
ms.sourcegitcommit: 8d34fb54e790cfba2d64097afc8276da5b22283e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85484398"
---
# <a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a><span data-ttu-id="f3b1e-103">使用 ASP.NET MVC 應用程式中的 Entity Framework 進行排序、篩選和分頁 (3/10) </span><span class="sxs-lookup"><span data-stu-id="f3b1e-103">Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application (3 of 10)</span></span>

<span data-ttu-id="f3b1e-104">由 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f3b1e-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="f3b1e-105">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="f3b1e-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="f3b1e-106">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="f3b1e-107">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="f3b1e-108">您可以從開頭開始進行教學課程系列，或 [下載此章節的入門專案](building-the-ef5-mvc4-chapter-downloads.md) ，從這裡開始。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="f3b1e-109">如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="f3b1e-110">您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="f3b1e-111">針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="f3b1e-112">在上一個教學課程中，您已針對實體的基本 CRUD 作業，執行一組網頁 `Student` 。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-112">In the previous tutorial you implemented a set of web pages for basic CRUD operations for `Student` entities.</span></span> <span data-ttu-id="f3b1e-113">在本教學課程中，您會將排序、篩選和分頁功能新增至 **學生** 的 [索引] 頁面。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-113">In this tutorial you'll add sorting, filtering, and paging functionality to the **Students** Index page.</span></span> <span data-ttu-id="f3b1e-114">此外，還要建立將執行簡易群組的頁面。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-114">You'll also create a page that does simple grouping.</span></span>

<span data-ttu-id="f3b1e-115">下圖顯示當您完成時的頁面外觀。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-115">The following illustration shows what the page will look like when you're done.</span></span> <span data-ttu-id="f3b1e-116">資料行標題是使用者可以按一下以依據該資料行排序的連結。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-116">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="f3b1e-117">重覆按一下資料行標題，可切換遞增和遞減排序次序。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-117">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a><span data-ttu-id="f3b1e-119">將資料行排序連結新增至 Students 的 [索引] 頁面</span><span class="sxs-lookup"><span data-stu-id="f3b1e-119">Add Column Sort Links to the Students Index Page</span></span>

<span data-ttu-id="f3b1e-120">若要將排序新增至學生的 [索引] 頁面，您將變更 `Index` 控制器的方法， `Student` 並將程式碼加入至 `Student` 索引視圖。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-120">To add sorting to the Student Index page, you'll change the `Index` method of the `Student` controller and add code to the `Student` Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="f3b1e-121">將排序功能加入至 Index 方法</span><span class="sxs-lookup"><span data-stu-id="f3b1e-121">Add Sorting Functionality to the Index Method</span></span>

<span data-ttu-id="f3b1e-122">在 *Controllers\StudentController.cs*中，以 `Index` 下列程式碼取代方法：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-122">In *Controllers\StudentController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="f3b1e-123">此程式碼會從 URL 中的查詢字串接收 `sortOrder` 參數。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-123">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="f3b1e-124">ASP.NET MVC 會提供查詢字串值，做為動作方法的參數。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-124">The query string value is provided by ASP.NET MVC as a parameter to the action method.</span></span> <span data-ttu-id="f3b1e-125">該參數是 "Name" 或 "Date" 的字串，後面可選擇性地接著底線和字串 "desc" 來指定遞減順序。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-125">The parameter will be a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="f3b1e-126">預設排序順序為遞增。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-126">The default sort order is ascending.</span></span>

<span data-ttu-id="f3b1e-127">第一次要求 [索引] 頁面時，沒有任何查詢字串。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-127">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="f3b1e-128">學生會以遞增的順序顯示 `LastName` ，也就是由語句中的逐步執行案例所建立的預設值 `switch` 。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-128">The students are displayed in ascending order by `LastName`, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="f3b1e-129">使用者按一下資料行標題超連結時，適當的 `sortOrder` 值將會在查詢字串值中提供。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-129">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="f3b1e-130">`ViewBag`系統會使用這兩個變數，讓 view 可以使用適當的查詢字串值來設定資料行標題超連結：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-130">The two `ViewBag` variables are used so that the view can configure the column heading hyperlinks with the appropriate query string values:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="f3b1e-131">這些是三元陳述式。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-131">These are ternary statements.</span></span> <span data-ttu-id="f3b1e-132">第一個是指定如果 `sortOrder` 參數是 null 或空白，則 `ViewBag.NameSortParm` 應該設定為 "name \_ desc"; 否則，它應該設定為空字串。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-132">The first one specifies that if the `sortOrder` parameter is null or empty, `ViewBag.NameSortParm` should be set to "name\_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="f3b1e-133">這兩個陳述式讓檢視能夠設定資料行標題超連結，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-133">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

| <span data-ttu-id="f3b1e-134">目前排序次序</span><span class="sxs-lookup"><span data-stu-id="f3b1e-134">Current sort order</span></span> | <span data-ttu-id="f3b1e-135">姓氏超連結</span><span class="sxs-lookup"><span data-stu-id="f3b1e-135">Last Name Hyperlink</span></span> | <span data-ttu-id="f3b1e-136">日期超連結</span><span class="sxs-lookup"><span data-stu-id="f3b1e-136">Date Hyperlink</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f3b1e-137">姓氏遞增</span><span class="sxs-lookup"><span data-stu-id="f3b1e-137">Last Name ascending</span></span> | <span data-ttu-id="f3b1e-138">descending</span><span class="sxs-lookup"><span data-stu-id="f3b1e-138">descending</span></span> | <span data-ttu-id="f3b1e-139">ascending</span><span class="sxs-lookup"><span data-stu-id="f3b1e-139">ascending</span></span> |
| <span data-ttu-id="f3b1e-140">姓氏遞減</span><span class="sxs-lookup"><span data-stu-id="f3b1e-140">Last Name descending</span></span> | <span data-ttu-id="f3b1e-141">ascending</span><span class="sxs-lookup"><span data-stu-id="f3b1e-141">ascending</span></span> | <span data-ttu-id="f3b1e-142">ascending</span><span class="sxs-lookup"><span data-stu-id="f3b1e-142">ascending</span></span> |
| <span data-ttu-id="f3b1e-143">日期遞增</span><span class="sxs-lookup"><span data-stu-id="f3b1e-143">Date ascending</span></span> | <span data-ttu-id="f3b1e-144">ascending</span><span class="sxs-lookup"><span data-stu-id="f3b1e-144">ascending</span></span> | <span data-ttu-id="f3b1e-145">descending</span><span class="sxs-lookup"><span data-stu-id="f3b1e-145">descending</span></span> |
| <span data-ttu-id="f3b1e-146">日期遞減</span><span class="sxs-lookup"><span data-stu-id="f3b1e-146">Date descending</span></span> | <span data-ttu-id="f3b1e-147">ascending</span><span class="sxs-lookup"><span data-stu-id="f3b1e-147">ascending</span></span> | <span data-ttu-id="f3b1e-148">ascending</span><span class="sxs-lookup"><span data-stu-id="f3b1e-148">ascending</span></span> |

<span data-ttu-id="f3b1e-149">方法會使用 [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) 來指定要排序的資料行。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-149">The method uses [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) to specify the column to sort by.</span></span> <span data-ttu-id="f3b1e-150">程式碼會在語句之前建立 [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) 變數 `switch` 、在語句中修改它， `switch` 並在 `ToList` 語句之後呼叫方法 `switch` 。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-150">The code creates an [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) variable before the `switch` statement, modifies it in the `switch` statement, and calls the `ToList` method after the `switch` statement.</span></span> <span data-ttu-id="f3b1e-151">當您建立和修改 `IQueryable` 變數時，沒有查詢會傳送至資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-151">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="f3b1e-152">在您 `IQueryable` 呼叫方法（例如）將物件轉換成集合之前，不會執行查詢 `ToList` 。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-152">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToList`.</span></span> <span data-ttu-id="f3b1e-153">因此，此程式碼會產生一個查詢，而此查詢在語句之前都不會執行 `return View` 。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-153">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="f3b1e-154">將資料行標題超連結新增至學生索引視圖</span><span class="sxs-lookup"><span data-stu-id="f3b1e-154">Add Column Heading Hyperlinks to the Student Index View</span></span>

<span data-ttu-id="f3b1e-155">在 *Views\Student\Index.cshtml*中，以 `<tr>` 反 `<th>` 白顯示的程式碼取代標題資料列的和元素：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-155">In *Views\Student\Index.cshtml*, replace the `<tr>` and `<th>` elements for the heading row with the highlighted code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

<span data-ttu-id="f3b1e-156">此程式碼會使用屬性中的資訊 `ViewBag` ，以適當的查詢字串值設定超連結。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-156">This code uses the information in the `ViewBag` properties to set up hyperlinks with the appropriate query string values.</span></span>

<span data-ttu-id="f3b1e-157">執行頁面，然後按一下 [ **姓氏** ] 和 [ **註冊日期] 資料** 行標題，以確認排序可正常運作。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-157">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="f3b1e-159">當您按一下 [ **姓氏** ] 標題之後，學生會以姓氏順序顯示。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-159">After you click the **Last Name** heading, students are displayed in descending last name order.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a><span data-ttu-id="f3b1e-160">將搜尋方塊新增至學生的 [索引] 頁面</span><span class="sxs-lookup"><span data-stu-id="f3b1e-160">Add a Search Box to the Students Index Page</span></span>

<span data-ttu-id="f3b1e-161">若要將篩選新增至 Students 的 [索引] 頁面，您要將文字方塊和提交按鈕新增至檢視，並在 `Index` 方法中進行對應的變更。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-161">To add filtering to the Students Index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="f3b1e-162">文字方塊可讓您輸入要在名字和姓氏欄位中搜尋的字串。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-162">The text box will let you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="f3b1e-163">將篩選功能新增至 Index 方法</span><span class="sxs-lookup"><span data-stu-id="f3b1e-163">Add Filtering Functionality to the Index Method</span></span>

<span data-ttu-id="f3b1e-164">在 *Controllers\StudentController.cs*中，以 `Index` 下列程式碼取代方法 () 會反白顯示變更：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-164">In *Controllers\StudentController.cs*, replace the `Index` method with the following code (the changes are highlighted):</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

<span data-ttu-id="f3b1e-165">您已將 `searchString` 參數新增至 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-165">You've added a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="f3b1e-166">您也已將子句新增至 LINQ 語句 `where` ，這個子句只會選取其名字或姓氏包含搜尋字串的學生。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-166">You've also added to the LINQ statement a `where` clause that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="f3b1e-167">搜尋字串值是從您將加入至索引視圖的文字方塊中收到。只有在有要搜尋的值時，才會執行加入 [where](https://msdn.microsoft.com/library/bb535040.aspx) 子句的語句。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-167">The search string value is received from a text box that you'll add to the Index view.The statement that adds the [where](https://msdn.microsoft.com/library/bb535040.aspx) clause is executed only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="f3b1e-168">在許多情況下，您可以在 Entity Framework 實體集上呼叫相同的方法，或是在記憶體中的集合上呼叫擴充方法。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-168">In many cases you can call the same method either on an Entity Framework entity set or as an extension method on an in-memory collection.</span></span> <span data-ttu-id="f3b1e-169">結果通常是相同的，但在某些情況下可能會有所不同。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-169">The results are normally the same but in some cases may be different.</span></span> <span data-ttu-id="f3b1e-170">例如， `Contains` 當您將空字串傳遞給它時，方法的 .NET Framework 執行會傳回所有資料列，但是 SQL Server Compact 4.0 的 Entity Framework 提供者會針對空字串傳回零個數據列。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-170">For example, the .NET Framework implementation of the `Contains` method returns all rows when you pass an empty string to it, but the Entity Framework provider for SQL Server Compact 4.0 returns zero rows for empty strings.</span></span> <span data-ttu-id="f3b1e-171">因此，範例中的程式碼 (將 `Where` 語句放在 `if` 語句內) 可確保您取得所有 SQL Server 版本的相同結果。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-171">Therefore the code in the example (putting the `Where` statement inside an `if` statement) makes sure that you get the same results for all versions of SQL Server.</span></span> <span data-ttu-id="f3b1e-172">此外，此方法的 .NET Framework 實 `Contains` 依預設會執行區分大小寫的比較，但是 Entity Framework SQL Server 提供者預設會執行不區分大小寫的比較。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-172">Also, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but Entity Framework SQL Server providers perform case-insensitive comparisons by default.</span></span> <span data-ttu-id="f3b1e-173">因此，呼叫 `ToUpper` 方法以明確區分大小寫，可確保當您稍後變更程式碼以使用存放庫時，不會變更結果，而不會傳回 `IEnumerable` 集合而不是 `IQueryable` 物件。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-173">Therefore, calling the `ToUpper` method to make the test explicitly case-insensitive ensures that results do not change when you change the code later to use a repository, which will return an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="f3b1e-174">(當您在 `IEnumerable` 集合上呼叫 `Contains` 方法時，將取得 .NET Framework 實作；當您在 `IQueryable` 物件上呼叫它時，則會取得資料庫提供者實作。)</span><span class="sxs-lookup"><span data-stu-id="f3b1e-174">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.)</span></span>

### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="f3b1e-175">將搜尋方塊新增至學生的 [索引] 檢視</span><span class="sxs-lookup"><span data-stu-id="f3b1e-175">Add a Search Box to the Student Index View</span></span>

<span data-ttu-id="f3b1e-176">在 *Views\Student\Index.cshtml*中，于開頭標記之前加入醒目提示的程式碼，以便 `table` 建立標題、文字方塊和 **搜尋** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-176">In *Views\Student\Index.cshtml*, add the highlighted code immediately before the opening `table` tag in order to create a caption, a text box, and a **Search** button.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

<span data-ttu-id="f3b1e-177">執行頁面，輸入搜尋字串，然後按一下 [ **搜尋** ] 以確認篩選是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-177">Run the page, enter a search string, and click **Search** to verify that filtering is working.</span></span>

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="f3b1e-179">請注意，URL 未包含「a」搜尋字串，這表示如果您將此頁面加入書簽，當您使用書簽時，將不會取得篩選過的清單。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-179">Notice the URL doesn't contain the "an" search string, which means that if you bookmark this page, you won't get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="f3b1e-180">您將在稍後的教學課程中，變更 [ **搜尋** ] 按鈕，以使用篩選準則的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-180">You'll change the **Search** button to use query strings for filter criteria later in the tutorial.</span></span>

## <a name="add-paging-to-the-students-index-page"></a><span data-ttu-id="f3b1e-181">將分頁新增至學生索引頁面</span><span class="sxs-lookup"><span data-stu-id="f3b1e-181">Add Paging to the Students Index Page</span></span>

<span data-ttu-id="f3b1e-182">若要將分頁新增至學生的 [索引] 頁面，您必須先安裝 **PagedList Mvc** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-182">To add paging to the Students Index page, you'll start by installing the **PagedList.Mvc** NuGet package.</span></span> <span data-ttu-id="f3b1e-183">然後，您會在方法中進行其他變更 `Index` ，並將分頁連結新增至 `Index` 視圖。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-183">Then you'll make additional changes in the `Index` method and add paging links to the `Index` view.</span></span> <span data-ttu-id="f3b1e-184">**PagedList** 是 ASP.NET Mvc 的許多良好分頁和排序封裝的其中一種，其用途僅限於範例，而不是其他選項的建議。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-184">**PagedList.Mvc** is one of many good paging and sorting packages for ASP.NET MVC, and its use here is intended only as an example, not as a recommendation for it over other options.</span></span> <span data-ttu-id="f3b1e-185">下圖顯示頁面連結。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-185">The following illustration shows the paging links.</span></span>

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a><span data-ttu-id="f3b1e-187">安裝 PagedList MVC NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="f3b1e-187">Install the PagedList.MVC NuGet Package</span></span>

<span data-ttu-id="f3b1e-188">NuGet **PagedList** 套件會自動安裝 **PagedList** 套件作為相依性。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-188">The NuGet **PagedList.Mvc** package automatically installs the **PagedList** package as a dependency.</span></span> <span data-ttu-id="f3b1e-189">**PagedList**封裝會安裝 `PagedList` 和集合的集合型別和擴充方法 `IQueryable` `IEnumerable` 。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-189">The **PagedList** package installs a `PagedList` collection type and extension methods for `IQueryable` and `IEnumerable` collections.</span></span> <span data-ttu-id="f3b1e-190">擴充方法會在或以外的集合中建立單一資料頁面 `PagedList` `IQueryable` `IEnumerable` ，而 `PagedList` 集合會提供數個可協助分頁的屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-190">The extension methods create a single page of data in a `PagedList` collection out of your `IQueryable` or `IEnumerable`, and the `PagedList` collection provides several properties and methods that facilitate paging.</span></span> <span data-ttu-id="f3b1e-191">**PagedList**會安裝分頁協助程式，以顯示分頁按鈕。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-191">The **PagedList.Mvc** package installs a paging helper that displays the paging buttons.</span></span>

<span data-ttu-id="f3b1e-192">從 [ **工具** ] 功能表選取 [ **nuget 封裝管理員** ]，然後 **管理方案的 nuget 套件**。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-192">From the **Tools** menu, select **NuGet Package Manager** and then **Manage NuGet Packages for Solution**.</span></span>

<span data-ttu-id="f3b1e-193">在 [ **管理 NuGet 封裝** ] 對話方塊中，按一下左側的 [ **線上** ] 索引標籤，然後在搜尋方塊中輸入「分頁」。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-193">In the **Manage NuGet Packages** dialog box, click the **Online** tab on the left and then enter "paged" in the search box.</span></span> <span data-ttu-id="f3b1e-194">當您看到 **PagedList** 的封裝時，請按一下 [ **安裝**]。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-194">When you see the **PagedList.Mvc** package, click **Install**.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="f3b1e-195">在 [ **選取專案** ] 方塊中，按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-195">In the **Select Projects** box, click **OK**.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="f3b1e-196">將分頁功能新增至 Index 方法</span><span class="sxs-lookup"><span data-stu-id="f3b1e-196">Add Paging Functionality to the Index Method</span></span>

<span data-ttu-id="f3b1e-197">在 *Controllers\StudentController.cs*中，加入 `using` `PagedList` 命名空間的語句：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-197">In *Controllers\StudentController.cs*, add a `using` statement for the `PagedList` namespace:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="f3b1e-198">以下列程式碼取代 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-198">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="f3b1e-199">這段程式碼會將 `page` 參數、目前的排序次序參數和目前的篩選參數新增至方法簽章，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-199">This code adds a `page` parameter, a current sort order parameter, and a current filter parameter to the method signature, as shown here:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="f3b1e-200">第一次顯示頁面，或是使用者尚未按一下分頁或排序連結時，所有參數都會是 null。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-200">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters will be null.</span></span> <span data-ttu-id="f3b1e-201">如果按一下分頁連結， `page` 變數會包含要顯示的頁碼。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-201">If a paging link is clicked, the `page` variable will contain the page number to display.</span></span>

<span data-ttu-id="f3b1e-202">`A ViewBag` 屬性提供目前排序次序的視圖，因為這必須包含在分頁連結中，才能讓排序次序在分頁時保持相同：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-202">`A ViewBag` property provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="f3b1e-203">另一個屬性，則會 `ViewBag.CurrentFilter` 提供具有目前篩選字串的視圖。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-203">Another property, `ViewBag.CurrentFilter`, provides the view with the current filter string.</span></span> <span data-ttu-id="f3b1e-204">此值必須包含在分頁連結中，才能維護分頁期間的篩選設定，而且它必須在頁面重新顯示時還原為文字方塊。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-204">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span> <span data-ttu-id="f3b1e-205">如果搜尋字串在分頁期間變更，頁面必須重設為 1，因為新的篩選可能會導致顯示不同的資料。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-205">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="f3b1e-206">在文字方塊中輸入值並按下 [提交] 按鈕時，會變更搜尋字串。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-206">The search string is changed when a value is entered in the text box and the submit button is pressed.</span></span> <span data-ttu-id="f3b1e-207">在該情況下， `searchString` 參數不是 null。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-207">In that case, the `searchString` parameter is not null.</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

<span data-ttu-id="f3b1e-208">在方法的結尾， `ToPagedList` 學生物件的擴充方法 `IQueryable` 會將學生查詢轉換成支援分頁的集合類型中的單一學生頁面。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-208">At the end of the method, the `ToPagedList` extension method on the students `IQueryable` object converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="f3b1e-209">然後將該單一頁面傳給視圖：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-209">That single page of students is then passed to the view:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="f3b1e-210">`ToPagedList` 方法會採用頁面數。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-210">The `ToPagedList` method takes a page number.</span></span> <span data-ttu-id="f3b1e-211">這兩個問號代表 [null 聯合運算子](https://msdn.microsoft.com/library/ms173224.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-211">The two question marks represent the [null-coalescing operator](https://msdn.microsoft.com/library/ms173224.aspx).</span></span> <span data-ttu-id="f3b1e-212">Null 聯合運算子將針對可為 Null 的型別定義預設值；`(page ?? 1)` 運算式表示在它含有值時會傳回值 `page`，或在 `page` 為 null 時傳回 1。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-212">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

### <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="f3b1e-213">將分頁連結新增至學生索引視圖</span><span class="sxs-lookup"><span data-stu-id="f3b1e-213">Add Paging Links to the Student Index View</span></span>

<span data-ttu-id="f3b1e-214">在 *Views\Student\Index.cshtml*中，以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-214">In *Views\Student\Index.cshtml*, replace the existing code with the following code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

<span data-ttu-id="f3b1e-215">頁面頂端的 `@model` 陳述式指定檢視現在會取得 `PagedList` 物件，而不是 `List` 物件。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-215">The `@model` statement at the top of the page specifies that the view now gets a `PagedList` object instead of a `List` object.</span></span>

<span data-ttu-id="f3b1e-216">的 `using` 語句 `PagedList.Mvc` 可為分頁按鈕的 MVC helper 提供存取權。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-216">The `using` statement for `PagedList.Mvc` gives access to the MVC helper for the paging buttons.</span></span>

<span data-ttu-id="f3b1e-217">程式碼會使用 [html.beginform](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) 的多載，以允許它指定 [FormMethod. Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-217">The code uses an overload of [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) that allows it to specify [FormMethod.Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css).</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

<span data-ttu-id="f3b1e-218">預設 [html.beginform](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) 會使用 POST 提交表單資料，這表示參數會在 HTTP 訊息內文中傳遞，而不是以 URL 形式傳遞至查詢字串。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-218">The default [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="f3b1e-219">當您指定 HTTP GET 時，表單資料會以 URL 中作為查詢字串傳遞，這可讓使用者為該 URL 加上書籤。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-219">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="f3b1e-220">[使用 HTTP GET 的 W3C 指導方針](http://www.w3.org/2001/tag/doc/whenToUseGet.html)指定當動作不會產生更新時，您應該使用 GET。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-220">The [W3C guidelines for the use of HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) specify that you should use GET when the action does not result in an update.</span></span>

<span data-ttu-id="f3b1e-221">文字方塊會使用目前的搜尋字串來初始化，因此當您按一下新的頁面時，可以看到目前的搜尋字串。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-221">The text box is initialized with the current search string so when you click a new page you can see the current search string.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

<span data-ttu-id="f3b1e-222">資料行標頭連結會使用查詢字串，將目前的搜尋字串傳遞至控制器，讓使用者可以在篩選結果內排序：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-222">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

<span data-ttu-id="f3b1e-223">目前的頁面和總頁數隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-223">The current page and total number of pages are displayed.</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

<span data-ttu-id="f3b1e-224">如果沒有可顯示的頁面，則會顯示「0的頁面0」。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-224">If there are no pages to display, "Page 0 of 0" is shown.</span></span> <span data-ttu-id="f3b1e-225"> (在這種情況下，頁碼大於頁面計數 `Model.PageNumber` ，因為是1，且 `Model.PageCount` 是0。 ) </span><span class="sxs-lookup"><span data-stu-id="f3b1e-225">(In that case the page number is greater than the page count because `Model.PageNumber` is 1, and `Model.PageCount` is 0.)</span></span>

<span data-ttu-id="f3b1e-226">協助程式會顯示分頁按鈕 `PagedListPager` ：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-226">The paging buttons are displayed by the `PagedListPager` helper:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

<span data-ttu-id="f3b1e-227">`PagedListPager`Helper 提供許多您可以自訂的選項，包括 url 和樣式。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-227">The `PagedListPager` helper provides a number of options that you can customize, including URLs and styling.</span></span> <span data-ttu-id="f3b1e-228">如需詳細資訊，請參閱 GitHub 網站上的 [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-228">For more information, see [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) on the GitHub site.</span></span>

<span data-ttu-id="f3b1e-229">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-229">Run the page.</span></span>

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="f3b1e-231">以不同排序次序按一下分頁連結，以確定分頁運作正常。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-231">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="f3b1e-232">然後輸入搜尋字串並再次嘗試分頁，以確認分頁的排序和篩選能正確運作。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-232">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a><span data-ttu-id="f3b1e-233">建立顯示學生統計資料的 [About （關於）] 頁面</span><span class="sxs-lookup"><span data-stu-id="f3b1e-233">Create an About Page That Shows Student Statistics</span></span>

<span data-ttu-id="f3b1e-234">對於 Contoso 大學網站的 About 頁面，您將顯示每個註冊日期已有多少學生註冊。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-234">For the Contoso University website's About page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="f3b1e-235">這需要對群組進行分組和簡單計算。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-235">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="f3b1e-236">若要完成此工作，您需要執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-236">To accomplish this, you'll do the following:</span></span>

- <span data-ttu-id="f3b1e-237">針對您需要傳遞至檢視的資料，建立檢視模型類別。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-237">Create a view model class for the data that you need to pass to the view.</span></span>
- <span data-ttu-id="f3b1e-238">修改 `About` 控制器中的方法 `Home` 。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-238">Modify the `About` method in the `Home` controller.</span></span>
- <span data-ttu-id="f3b1e-239">修改 `About` 視圖。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-239">Modify the `About` view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="f3b1e-240">建立視圖模型</span><span class="sxs-lookup"><span data-stu-id="f3b1e-240">Create the View Model</span></span>

<span data-ttu-id="f3b1e-241">建立 *viewmodel* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-241">Create a *ViewModels* folder.</span></span> <span data-ttu-id="f3b1e-242">在該資料夾中，新增類別檔案 *EnrollmentDateGroup.cs* ，並以下列程式碼取代現有的程式碼：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-242">In that folder, add a class file *EnrollmentDateGroup.cs* and replace the existing code with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="f3b1e-243">修改 Home 控制器</span><span class="sxs-lookup"><span data-stu-id="f3b1e-243">Modify the Home Controller</span></span>

<span data-ttu-id="f3b1e-244">在 *HomeController.cs*中，將下列 `using` 語句新增至檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-244">In *HomeController.cs*, add the following `using` statements at the top of the file:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="f3b1e-245">在類別的左大括弧後面緊接著，加入資料庫內容的類別變數：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-245">Add a class variable for the database context immediately after the opening curly brace for the class:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

<span data-ttu-id="f3b1e-246">以下列程式碼取代 `About` 方法：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-246">Replace the `About` method with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="f3b1e-247">LINQ 陳述式會依註冊日期將學生實體組成群組、計算每個群組中的實體數目、將結果儲存在 `EnrollmentDateGroup` 檢視模型物件的集合中。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-247">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>

<span data-ttu-id="f3b1e-248">新增 `Dispose` 方法：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-248">Add a `Dispose` method:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a><span data-ttu-id="f3b1e-249">修改 About 檢視</span><span class="sxs-lookup"><span data-stu-id="f3b1e-249">Modify the About View</span></span>

<span data-ttu-id="f3b1e-250">將 *Views\Home\About.cshtml* 檔案中的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-250">Replace the code in the *Views\Home\About.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

<span data-ttu-id="f3b1e-251">執行應用程式，然後按一下 [ **關於** ] 連結。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-251">Run the app and click the **About** link.</span></span> <span data-ttu-id="f3b1e-252">每個註冊日期的學生人數將會顯示在資料表中。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-252">The count of students for each enrollment date is displayed in a table.</span></span>

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a><span data-ttu-id="f3b1e-254">選擇性：將應用程式部署到 Windows Azure</span><span class="sxs-lookup"><span data-stu-id="f3b1e-254">Optional: Deploy the app to Windows Azure</span></span>

<span data-ttu-id="f3b1e-255">到目前為止，您的應用程式在您的開發電腦上 IIS Express 于本機執行。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-255">So far your application has been running locally in IIS Express on your development computer.</span></span> <span data-ttu-id="f3b1e-256">若要讓其他人可透過網際網路使用它，您必須將它部署至 web 主機服務提供者。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-256">To make it available for other people to use over the Internet, you have to deploy it to a web hosting provider.</span></span> <span data-ttu-id="f3b1e-257">在本教學課程的這個選擇性區段中，您會將其部署至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-257">In this optional section of the tutorial you'll deploy it to a Windows Azure Web Site.</span></span>

### <a name="using-code-first-migrations-to-deploy-the-database"></a><span data-ttu-id="f3b1e-258">使用 Code First 移轉部署資料庫</span><span class="sxs-lookup"><span data-stu-id="f3b1e-258">Using Code First Migrations to Deploy the Database</span></span>

<span data-ttu-id="f3b1e-259">若要部署資料庫，您將會使用 Code First 移轉。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-259">To deploy the database you'll use Code First Migrations.</span></span> <span data-ttu-id="f3b1e-260">當您建立用來設定從 Visual Studio 部署之設定的發行設定檔時，您會選取標示為 [執行] 的核取方塊， \*\* (在應用程式啟動) 上執行 Code First 移轉 \*\*。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-260">When you create the publish profile that you use to configure settings for deploying from Visual Studio, you'll select a check box that is labeled **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="f3b1e-261">這項設定會導致部署程式在目的地伺服器上自動設定應用程式 *Web.config* 檔，讓 Code First 使用 `MigrateDatabaseToLatestVersion` 初始化運算式類別。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-261">This setting causes the deployment process to automatically configure the application *Web.config* file on the destination server so that Code First uses the `MigrateDatabaseToLatestVersion` initializer class.</span></span>

<span data-ttu-id="f3b1e-262">Visual Studio 在部署程式期間，不會對資料庫執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-262">Visual Studio does not do anything with the database during the deployment process.</span></span> <span data-ttu-id="f3b1e-263">當部署的應用程式在部署之後第一次存取資料庫時，Code First 會自動建立資料庫，或將資料庫架構更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-263">When the deployed application accesses the database for the first time after deployment, Code First automatically creates the database or updates the database schema to the latest version.</span></span> <span data-ttu-id="f3b1e-264">如果應用程式是執行遷移 `Seed` 方法，則在建立資料庫或更新架構之後，便會執行此方法。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-264">If the application implements a Migrations `Seed` method, the method runs after the database is created or the schema is updated.</span></span>

<span data-ttu-id="f3b1e-265">您的遷移 `Seed` 方法會插入測試資料。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-265">Your Migrations `Seed` method inserts test data.</span></span> <span data-ttu-id="f3b1e-266">如果您要部署到生產環境，則必須變更 `Seed` 方法，使其只會插入您想要插入至生產資料庫的資料。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-266">If you were deploying to a production environment, you would have to change the `Seed` method so that it only inserts data that you want to be inserted into your production database.</span></span> <span data-ttu-id="f3b1e-267">例如，在您目前的資料模型中，您可能想要在開發資料庫中擁有真實的課程，但虛構的學生。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-267">For example, in your current data model you might want to have real courses but fictional students in the development database.</span></span> <span data-ttu-id="f3b1e-268">您可以撰寫 `Seed` 方法以在開發期間載入，然後在部署至生產環境之前，先將虛構的學生加上批註。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-268">You can write a `Seed` method to load both in development, and then comment out the fictional students before you deploy to production.</span></span> <span data-ttu-id="f3b1e-269">或者，您可以撰寫一個 `Seed` 方法來僅載入課程，並使用應用程式的 UI，以手動方式在測試資料庫中輸入虛構的學生。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-269">Or you can write a `Seed` method to load only courses, and enter the fictional students in the test database manually by using the application's UI.</span></span>

### <a name="get-a-windows-azure-account"></a><span data-ttu-id="f3b1e-270">取得 Windows Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="f3b1e-270">Get a Windows Azure account</span></span>

<span data-ttu-id="f3b1e-271">您將需要 Windows Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-271">You'll need a Windows Azure account.</span></span> <span data-ttu-id="f3b1e-272">如果您還沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-272">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f3b1e-273">如需詳細資訊，請參閱 [Windows Azure 免費試用](https://azure.microsoft.com/free/dotnet/)。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-273">For details, see [Windows Azure Free Trial](https://azure.microsoft.com/free/dotnet/).</span></span>

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a><span data-ttu-id="f3b1e-274">在 Windows Azure 中建立網站和 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="f3b1e-274">Create a web site and a SQL database in Windows Azure</span></span>

<span data-ttu-id="f3b1e-275">您的 Windows Azure 網站將在共用主控環境中執行，這表示它會在與其他 Windows Azure 用戶端共用的虛擬機器 (Vm) 上執行。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-275">Your Windows Azure Web Site will run in a shared hosting environment, which means it runs on virtual machines (VMs) that are shared with other Windows Azure clients.</span></span> <span data-ttu-id="f3b1e-276">共用主控環境是一種在雲端中開始營運的低成本方法。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-276">A shared hosting environment is a low-cost way to get started in the cloud.</span></span> <span data-ttu-id="f3b1e-277">因為應用程式是在專用 VM 上執行，所以如果日後您的 Web 流量增加，可依需求對應用程式進行延展。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-277">Later, if your web traffic increases, the application can scale to meet the need by running on dedicated VMs.</span></span> <span data-ttu-id="f3b1e-278">如果您需要更複雜的架構，您可以遷移至 Windows Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-278">If you need a more complex architecture, you can migrate to a Windows Azure Cloud Service.</span></span> <span data-ttu-id="f3b1e-279">雲端服務是執行於您可視本身需求來設定的專用 VM 上。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-279">Cloud services run on dedicated VMs that you can configure according to your needs.</span></span>

<span data-ttu-id="f3b1e-280">Windows Azure SQL Database 是以 SQL Server 技術為基礎的雲端式關係資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-280">Windows Azure SQL Database is a cloud-based relational database service that is built on SQL Server technologies.</span></span> <span data-ttu-id="f3b1e-281">使用 SQL Server 的工具和應用程式也可以使用 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-281">Tools and applications that work with SQL Server also work with SQL Database.</span></span>

1. <span data-ttu-id="f3b1e-282">在 [ [Windows Azure 管理入口網站](https://manage.windowsazure.com/)中，按一下左邊索引標籤中的 [ **網站** ]，然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-282">In the [Windows Azure Management Portal](https://manage.windowsazure.com/), click **Web Sites** in the left tab, and then click **New**.</span></span>

    ![管理入口網站中的 [新增] 按鈕](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. <span data-ttu-id="f3b1e-284">按一下 [ **自訂建立**]。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-284">Click **CUSTOM CREATE**.</span></span>

    ![在管理入口網站中使用資料庫連結建立](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

   <span data-ttu-id="f3b1e-286">**新網站-[自訂建立**嚮導] 隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-286">The **New Web Site - Custom Create** wizard opens.</span></span>
3. <span data-ttu-id="f3b1e-287">在嚮導的 [ **新增網站** ] 步驟中，于 [ **URL** ] 方塊中輸入字串，以作為應用程式的唯一 URL。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-287">In the **New Web Site** step of the wizard, enter a string in the **URL** box to use as the unique URL for your application.</span></span> <span data-ttu-id="f3b1e-288">完整的 URL 將包含您在此處輸入的字串，加上您在文字方塊旁看到的尾碼。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-288">The complete URL will consist of what you enter here plus the suffix that you see next to the text box.</span></span> <span data-ttu-id="f3b1e-289">圖例顯示「ConU」，但該 URL 可能會被採用，因此您必須選擇不同的 URL。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-289">The illustration shows "ConU", but that URL is probably taken so you will have to choose a different one.</span></span>

    ![在管理入口網站中使用資料庫連結建立](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. <span data-ttu-id="f3b1e-291">在 [ **區域** ] 下拉式清單中，選擇接近您的區域。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-291">In the **Region** drop-down list, choose a region close to you.</span></span> <span data-ttu-id="f3b1e-292">這項設定會指定您的網站將在哪一個資料中心執行。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-292">This setting specifies which data center your web site will run in.</span></span>
5. <span data-ttu-id="f3b1e-293">在 [ **資料庫** ] 下拉式清單中，選擇 [ **建立免費的 20 MB SQL Database**]。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-293">In the **Database** drop-down list, choose **Create a free 20 MB SQL database**.</span></span>

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. <span data-ttu-id="f3b1e-294">在 [ **DB 連接字串名稱**] 中，輸入 *SchoolCoNtext*。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-294">In the **DB CONNECTION STRING NAME**, enter *SchoolContext*.</span></span>

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. <span data-ttu-id="f3b1e-295">按一下指向方塊底部右邊的箭號。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-295">Click the arrow that points to the right at the bottom of the box.</span></span> <span data-ttu-id="f3b1e-296">Wizard 會前進到 [ **資料庫設定** ] 步驟。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-296">The wizard advances to the **Database Settings** step.</span></span>
8. <span data-ttu-id="f3b1e-297">在 [ **名稱** ] 方塊中，輸入 *ContosoUniversityDB*。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-297">In the **Name** box, enter *ContosoUniversityDB*.</span></span>
9. <span data-ttu-id="f3b1e-298">在 [ **伺服器** ] 方塊中，選取 [ **新增 SQL Database 伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-298">In the **Server** box, select **New SQL Database server**.</span></span> <span data-ttu-id="f3b1e-299">或者，如果您先前已建立伺服器，就可以從下拉式清單中選取該伺服器。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-299">Alternatively, if you previously created a server, you can select that server from the drop-down list.</span></span>
10. <span data-ttu-id="f3b1e-300">輸入系統管理員 **登入名稱** 和 **密碼**。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-300">Enter an administrator **LOGIN NAME** and **PASSWORD**.</span></span> <span data-ttu-id="f3b1e-301">如果選取 [新增 SQL Database 伺服器]\*\*\*\*，則不要在此處輸入現有的名稱和密碼，而是輸入新的名稱和密碼；您現在定義的名稱和密碼將供未來存取資料庫時使用。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-301">If you selected **New SQL Database server** you aren't entering an existing name and password here, you're entering a new name and password that you're defining now to use later when you access the database.</span></span> <span data-ttu-id="f3b1e-302">如果您選取先前建立的伺服器，則會輸入該伺服器的認證。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-302">If you selected a server that you created previously, you'll enter credentials for that server.</span></span> <span data-ttu-id="f3b1e-303">在本教學課程中，您不會選取 [ ***Advanced*** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-303">For this tutorial, you won't select the ***Advanced*** check box.</span></span> <span data-ttu-id="f3b1e-304">***Advanced***選項可讓您設定資料庫定[序](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-304">The ***Advanced*** options enable you to set the database [collation](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx).</span></span>
11. <span data-ttu-id="f3b1e-305">選擇您為網站選擇的相同 **區域** 。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-305">Choose the same **Region** that you chose for the web site.</span></span>
12. <span data-ttu-id="f3b1e-306">按一下方塊右下角的核取記號，表示您已完成。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-306">Click the check mark at the bottom right of the box to indicate that you're finished.</span></span>   
  
    ![新網站的資料庫設定步驟-使用資料庫建立嚮導建立](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

    <span data-ttu-id="f3b1e-308">下圖顯示使用現有的 SQL Server 和登入。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-308">The following image shows using an existing SQL Server and Login.</span></span>   
  
    ![新網站的資料庫設定步驟-使用資料庫建立嚮導建立](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
    <span data-ttu-id="f3b1e-310">管理入口網站回到 [網站] 頁面，[ **狀態** ] 欄會顯示正在建立網站。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-310">The Management Portal returns to the Web Sites page, and the **Status** column shows that the site is being created.</span></span> <span data-ttu-id="f3b1e-311">在一段時間之後 (通常不到一分鐘的) ，[ **狀態** ] 資料行會顯示已成功建立網站。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-311">After a while (typically less than a minute), the **Status** column shows that the site was successfully created.</span></span> <span data-ttu-id="f3b1e-312">在左側的導覽列中，您帳戶中的網站數目會出現在 [ **網站** ] 圖示旁，而資料庫數目會出現在 [ **SQL 資料庫** ] 圖示旁。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-312">In the navigation bar at the left, the number of sites you have in your account appears next to the **Web Sites** icon, and the number of databases appears next to the **SQL Databases** icon.</span></span>

## <a name="deploy-the-application-to-windows-azure"></a><span data-ttu-id="f3b1e-313">將應用程式部署到 Windows Azure</span><span class="sxs-lookup"><span data-stu-id="f3b1e-313">Deploy the application to Windows Azure</span></span>

1. <span data-ttu-id="f3b1e-314">在 Visual Studio 的 [方案總管]\*\*\*\* 中以滑鼠右鍵按一下專案，再選取內容功能表中的 [發佈]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-314">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>  
  
    ![專案內容功能表中的 [發行]](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. <span data-ttu-id="f3b1e-316">在**發佈 Web** wizard 的 [**設定檔**] 索引標籤中，按一下 [匯**入**]。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-316">In the **Profile** tab of the **Publish Web** wizard, click **Import**.</span></span>  
  
    ![匯入發行設定](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. <span data-ttu-id="f3b1e-318">如果您先前未在 Visual Studio 中新增 Windows Azure 訂用帳戶，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-318">If you have not previously added your Windows Azure subscription in Visual Studio, perform the following steps.</span></span> <span data-ttu-id="f3b1e-319">在這些步驟中，您會新增訂用帳戶，以便 **從 Windows Azure** 網站匯入下的下拉式清單會包含您的網站。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-319">In these steps you add your subscription so that the drop-down list under **Import from a Windows Azure web site** will include your web site.</span></span>

    <span data-ttu-id="f3b1e-320">a.</span><span class="sxs-lookup"><span data-stu-id="f3b1e-320">a.</span></span> <span data-ttu-id="f3b1e-321">在 [匯 **入發行設定檔** ] 對話方塊中，按一下 [ **從 windows Azure**網站匯入]，然後按一下 [ **新增 windows azure 訂閱**]。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-321">In the **Import Publish Profile** dialog box, click **Import from a Windows Azure web site**, and then click **Add Windows Azure subscription**.</span></span>

    ![新增 Windows Azure 訂用帳戶](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    <span data-ttu-id="f3b1e-323">b.</span><span class="sxs-lookup"><span data-stu-id="f3b1e-323">b.</span></span> <span data-ttu-id="f3b1e-324">在 [匯 **入 Windows Azure 訂閱** ] 對話方塊中，按一下 [ **下載訂閱**檔案]。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-324">In the **Import Windows Azure Subscriptions** dialog box, click **Download subscription file**.</span></span>

    ![下載訂用帳戶檔案](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    <span data-ttu-id="f3b1e-326">c.</span><span class="sxs-lookup"><span data-stu-id="f3b1e-326">c.</span></span> <span data-ttu-id="f3b1e-327">在瀏覽器視窗中，儲存 *.publishsettings* 檔案。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-327">In your browser window, save the *.publishsettings* file.</span></span>

    ![下載 .publishsettings 檔案](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > <span data-ttu-id="f3b1e-329">安全性- *.publishsettings* 檔案包含您的認證 (未編碼的) ，用來管理您的 Windows Azure 訂閱和服務。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-329">Security - The *publishsettings* file contains your credentials (unencoded) that are used to administer your Windows Azure subscriptions and services.</span></span> <span data-ttu-id="f3b1e-330">這個檔案的安全性最佳作法是暫時儲存在來原始目錄外部 (例如，在 *Libraries\Documents* 資料夾) 中，然後在匯入完成後將它刪除。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-330">The security best practice for this file is to store it temporarily outside your source directories (for example in the *Libraries\Documents* folder), and then delete it once the import has completed.</span></span> <span data-ttu-id="f3b1e-331">取得檔案存取權的惡意使用者 `.publishsettings` 可以編輯、建立及刪除您的 Windows Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-331">A malicious user who gains access to the `.publishsettings` file can edit, create, and delete your Windows Azure services.</span></span>

    <span data-ttu-id="f3b1e-332">d.</span><span class="sxs-lookup"><span data-stu-id="f3b1e-332">d.</span></span> <span data-ttu-id="f3b1e-333">在 [匯 **入 Windows Azure 訂閱** ] 對話方塊中，按一下 **[流覽]** 並流覽至 *.publishsettings* 檔案。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-333">In the **Import Windows Azure Subscriptions** dialog box, click **Browse** and navigate to the *.publishsettings* file.</span></span>

    ![下載 sub](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    <span data-ttu-id="f3b1e-335">e.</span><span class="sxs-lookup"><span data-stu-id="f3b1e-335">e.</span></span> <span data-ttu-id="f3b1e-336">按一下 [匯入]  。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-336">Click **Import**.</span></span>

    ![import](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. <span data-ttu-id="f3b1e-338">在 [匯 **入發行設定檔** ] 對話方塊中，選取 [ **從 Windows Azure 網站匯入**]，從下拉式清單中選取您的網站，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-338">In the **Import Publish Profile** dialog box, select **Import from a Windows Azure web site**, select your web site from the drop-down list, and then click **OK**.</span></span>  
  
    ![匯入發行設定檔](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. <span data-ttu-id="f3b1e-340">在 [ **連接** ] 索引標籤中，按一下 [ **驗證連接** ]，確認設定正確無誤。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-340">In the **Connection** tab, click **Validate Connection** to make sure that the settings are correct.</span></span>  
  
    ![驗證連接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. <span data-ttu-id="f3b1e-342">驗證連接之後，[ **驗證** 連線] 按鈕旁邊會顯示綠色核取記號。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-342">When the connection has been validated, a green check mark is shown next to the **Validate Connection** button.</span></span> <span data-ttu-id="f3b1e-343">按一下 [下一步]  。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-343">Click **Next**.</span></span>  
  
    ![已成功驗證連接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. <span data-ttu-id="f3b1e-345">開啟 [ **SchoolCoNtext** ] 底下的 [**遠端連線字串**] 下拉式清單，然後選取您所建立之資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-345">Open the **Remote connection string** drop-down list under **SchoolContext** and select the connection string for the database you created.</span></span>
8. <span data-ttu-id="f3b1e-346">選取 [ \*\*執行] Code First 移轉 (在應用程式啟動) 上執行 \*\*。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-346">Select **Execute Code First Migrations (runs on application start)**.</span></span>
9. <span data-ttu-id="f3b1e-347">取消核取 [ **在執行時間使用此連接字串** \*\*UserCoNtext (DefaultConnection) \*\*，因為此應用程式不會使用成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-347">Uncheck **Use this connection string at runtime** for the **UserContext (DefaultConnection)**, since this application is not using the membership database.</span></span>   
  
    ![[設定] 索引標籤](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. <span data-ttu-id="f3b1e-349">按一下 [下一步]  。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-349">Click **Next**.</span></span>
11. <span data-ttu-id="f3b1e-350">在 [ **預覽** ] 索引標籤中，按一下 [ **開始預覽**]。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-350">In the **Preview** tab, click **Start Preview**.</span></span>  
  
    ![[預覽] 索引標籤中的 [StartPreview] 按鈕](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
    <span data-ttu-id="f3b1e-352">索引標籤會顯示要複製到伺服器的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-352">The tab displays a list of the files that will be copied to the server.</span></span> <span data-ttu-id="f3b1e-353">發佈應用程式時不需要顯示預覽，但這是很有用的功能。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-353">Displaying the preview isn't required to publish the application but is a useful function to be aware of.</span></span> <span data-ttu-id="f3b1e-354">在此情況下，您不需要對所顯示的檔案清單進行任何動作。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-354">In this case, you don't need to do anything with the list of files that is displayed.</span></span> <span data-ttu-id="f3b1e-355">下一次部署此應用程式時，只有已變更的檔案才會出現在此清單中。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-355">The next time you deploy this application, only the files that have changed will be in this list.</span></span>  
  
    ![StartPreview 檔輸出](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. <span data-ttu-id="f3b1e-357">按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-357">Click **Publish**.</span></span>  
    <span data-ttu-id="f3b1e-358">Visual Studio 開始將檔案複製到 Windows Azure 伺服器的程式。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-358">Visual Studio begins the process of copying the files to the Windows Azure server.</span></span>
13. <span data-ttu-id="f3b1e-359">[輸出] \*\*\*\* 視窗會顯示已採取的部署動作，並報告部署作業已順利完成。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-359">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>  
  
    ![報告部署成功的輸出視窗](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. <span data-ttu-id="f3b1e-361">部署成功後，預設瀏覽器會自動開啟至已部署網站的 URL。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-361">Upon successful deployment, the default browser automatically opens to the URL of the deployed web site.</span></span>  
    <span data-ttu-id="f3b1e-362">您建立的應用程式現在正在雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-362">The application you created is now running in the cloud.</span></span> <span data-ttu-id="f3b1e-363">按一下 [學生] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-363">Click the Students tab.</span></span>  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

<span data-ttu-id="f3b1e-365">此時您的 *SchoolCoNtext* 資料庫已在 Windows Azure SQL Database 中建立，因為您選取了 [ \*\*執行] Code First 移轉 (會在應用程式啟動) 上 \*\*執行。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-365">At this point your *SchoolContext* database has been created in the Windows Azure SQL Database because you selected **Execute Code First Migrations (runs on app start)**.</span></span> <span data-ttu-id="f3b1e-366">已部署網站中的 *Web.config* 檔已變更，因此 [>migratedatabasetolatestversion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 初始化運算式會在您第一次程式碼讀取或寫入資料庫中的資料時執行， (當您選取 [ **學生** ] 索引標籤時，會發生這種情況) ：</span><span class="sxs-lookup"><span data-stu-id="f3b1e-366">The *Web.config* file in the deployed web site has been changed so that the [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) initializer would run the first time your code reads or writes data in the database (which happened when you selected the **Students** tab):</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

<span data-ttu-id="f3b1e-367">部署程式也會建立新的連接字串， \* (SchoolCoNtext \_ DatabasePublish\*) ，以便 Code First 移轉用來更新資料庫架構和植入資料庫。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-367">The deployment process also created a new connection string *(SchoolContext\_DatabasePublish*) for Code First Migrations to use for updating the database schema and seeding the database.</span></span>

![Database_Publish 連接字串](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

<span data-ttu-id="f3b1e-369">*DefaultConnection*連接字串適用于在本教學課程中未使用的成員資格資料庫 () 。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-369">The *DefaultConnection* connection string is for the membership database (which we are not using in this tutorial).</span></span> <span data-ttu-id="f3b1e-370">ContosoUniversity 資料庫的 *SchoolCoNtext* 連接字串。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-370">The *SchoolContext* connection string is for the ContosoUniversity database.</span></span>

<span data-ttu-id="f3b1e-371">您可以在 *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*的電腦上找到 Web.config 檔案的已部署版本。您可以使用 FTP 來存取已部署的 *Web.config* 檔案本身。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-371">You can find the deployed version of the Web.config file on your own computer in *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*. You can access the deployed *Web.config* file itself by using FTP.</span></span> <span data-ttu-id="f3b1e-372">如需相關指示，請參閱 [使用 Visual Studio：部署程式碼更新 ASP.NET Web 部署](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-372">For instructions, see [ASP.NET Web Deployment using Visual Studio: Deploying a Code Update](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md).</span></span> <span data-ttu-id="f3b1e-373">遵循開頭為「若要使用 FTP 工具的指示，您需要三個專案： FTP URL、使用者名稱和密碼。」</span><span class="sxs-lookup"><span data-stu-id="f3b1e-373">Follow the instructions that start with "To use an FTP tool, you need three things: the FTP URL, the user name, and the password."</span></span>

> [!NOTE]
> <span data-ttu-id="f3b1e-374">Web 應用程式不會執行安全性，因此尋找 URL 的任何人都可以變更資料。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-374">The web app doesn't implement security, so anyone who finds the URL can change the data.</span></span> <span data-ttu-id="f3b1e-375">如需如何保護網站的相關指示，請參閱 [使用成員資格、OAuth 和 SQL Database 將安全的 ASP.NET MVC 應用程式部署到 Windows Azure 網站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-375">For instructions on how to secure the web site, see [Deploy a Secure ASP.NET MVC app with Membership, OAuth, and SQL Database to a Windows Azure Web Site](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span> <span data-ttu-id="f3b1e-376">您可以使用 Windows Azure 管理入口網站或 Visual Studio 中的 **伺服器總管** ，防止其他人使用該網站來停止網站。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-376">You can prevent other people from using the site by using the Windows Azure Management Portal or **Server Explorer** in Visual Studio to stop the site.</span></span>

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a><span data-ttu-id="f3b1e-377">Code First 初始化運算式</span><span class="sxs-lookup"><span data-stu-id="f3b1e-377">Code First Initializers</span></span>

<span data-ttu-id="f3b1e-378">在 [部署] 區段中，您會看到使用的是 [>migratedatabasetolatestversion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 初始化運算式。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-378">In the deployment section you saw the [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) initializer being used.</span></span> <span data-ttu-id="f3b1e-379">Code First 也提供可供您使用的其他初始化運算式，包括 [>createdatabaseifnotexists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (預設) 、 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) 和 [DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-379">Code First also provides other initializers that you can use, including [CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (the default), [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) and [DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx).</span></span> <span data-ttu-id="f3b1e-380">`DropCreateAlways`初始化運算式有助於設定單元測試的條件。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-380">The `DropCreateAlways` initializer can be useful for setting up conditions for unit tests.</span></span> <span data-ttu-id="f3b1e-381">您也可以撰寫自己的初始化運算式，如果您不想等到應用程式讀取或寫入資料庫，也可以明確地呼叫初始化運算式。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-381">You can also write your own initializers, and you can call an initializer explicitly if you don't want to wait until the application reads from or writes to the database.</span></span> <span data-ttu-id="f3b1e-382">如需初始化運算式的完整說明，請參閱本書程式設計 Entity Framework 的第6章 [： Code First](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman 和 Rowan 莎莎。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-382">For a comprehensive explanation of initializers, see chapter 6 of the book [Programming Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) by Julie Lerman and Rowan Miller.</span></span>

## <a name="summary"></a><span data-ttu-id="f3b1e-383">摘要</span><span class="sxs-lookup"><span data-stu-id="f3b1e-383">Summary</span></span>

<span data-ttu-id="f3b1e-384">在本教學課程中，您已瞭解如何建立資料模型，以及如何執行基本的 CRUD、排序、篩選、分頁和群組功能。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-384">In this tutorial you've seen how to create a data model and implement basic CRUD, sorting, filtering, paging, and grouping functionality.</span></span> <span data-ttu-id="f3b1e-385">在下一個教學課程中，您將會藉由展開資料模型來開始查看更多的主題。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-385">In the next tutorial you'll begin looking at more advanced topics by expanding the data model.</span></span>

<span data-ttu-id="f3b1e-386">您可以在 [ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="f3b1e-386">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f3b1e-387">[上一個](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md) 
> [下一步](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="f3b1e-387">[Previous](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
[Next](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)</span></span>
