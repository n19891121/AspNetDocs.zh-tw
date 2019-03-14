---
ms.openlocfilehash: 24726fba7f431f701b264a988a8de1b67d41d8a2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048715"
---
# <a name="add-search-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="39c5d-101">將搜尋新增至 ASP.NET Core MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="39c5d-101">Add search to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="39c5d-102">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="39c5d-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="39c5d-103">在本節中，您將搜尋功能新增至 `Index` 動作方法，可讓您依據「內容類型」或「名稱」搜尋電影。</span><span class="sxs-lookup"><span data-stu-id="39c5d-103">In this section you add search capability to the `Index` action method that lets you search movies by *genre* or *name*.</span></span>

<span data-ttu-id="39c5d-104">以下列程式碼取代 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="39c5d-104">Update the `Index` method with the following code:</span></span>
<!--
[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Shared/_Layout.cshtml?highlight=7,31)]
-->

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_1stSearch)]

<span data-ttu-id="39c5d-105">`Index` 動作方法的第一行會建立 [LINQ](/dotnet/standard/using-linq) 查詢，以選取電影：</span><span class="sxs-lookup"><span data-stu-id="39c5d-105">The first line of the `Index` action method creates a [LINQ](/dotnet/standard/using-linq) query to select the movies:</span></span>

```csharp
var movies = from m in _context.Movie
             select m;
```

<span data-ttu-id="39c5d-106">查詢｢只｣會在此時定義，它尚**未**對資料庫執行。</span><span class="sxs-lookup"><span data-stu-id="39c5d-106">The query is *only* defined at this point, it has **not** been run against the database.</span></span>

<span data-ttu-id="39c5d-107">如果 `searchString` 參數包含字串，則會修改電影查詢來篩選搜尋字串的值：</span><span class="sxs-lookup"><span data-stu-id="39c5d-107">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_SearchNull2)]

<span data-ttu-id="39c5d-108">上述 `s => s.Title.Contains()` 程式碼是 [Lambda 運算式](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)。</span><span class="sxs-lookup"><span data-stu-id="39c5d-108">The `s => s.Title.Contains()` code above is a [Lambda Expression](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions).</span></span> <span data-ttu-id="39c5d-109">在以方法為基礎的 [LINQ](/dotnet/standard/using-linq) 查詢中，Lambda 會用來作為標準查詢運算子方法的引數，例如 [Where](/dotnet/api/system.linq.enumerable.where) 方法或 `Contains` (用於上述程式碼)。</span><span class="sxs-lookup"><span data-stu-id="39c5d-109">Lambdas are used in method-based [LINQ](/dotnet/standard/using-linq) queries as arguments to standard query operator methods such as the [Where](/dotnet/api/system.linq.enumerable.where) method or `Contains` (used in the code above).</span></span> <span data-ttu-id="39c5d-110">定義 LINQ 查詢或藉由呼叫像是 `Where`、`Contains` 或 `OrderBy` 等方法進行修改時，並不會加以執行。</span><span class="sxs-lookup"><span data-stu-id="39c5d-110">LINQ queries are not executed when they're defined or when they're modified by calling a method such as `Where`, `Contains`  or `OrderBy`.</span></span> <span data-ttu-id="39c5d-111">而會延後執行查詢。</span><span class="sxs-lookup"><span data-stu-id="39c5d-111">Rather, query execution is deferred.</span></span>  <span data-ttu-id="39c5d-112">這是指延遲評估運算式，直到實際反覆運算其實現值或呼叫 `ToListAsync` 方法為止。</span><span class="sxs-lookup"><span data-stu-id="39c5d-112">That means that the evaluation of an expression is delayed until its realized value is actually iterated over or the `ToListAsync` method is called.</span></span> <span data-ttu-id="39c5d-113">如需延後查詢執行的詳細資訊，請參閱[查詢執行](/dotnet/framework/data/adonet/ef/language-reference/query-execution)。</span><span class="sxs-lookup"><span data-stu-id="39c5d-113">For more information about deferred query execution, see [Query Execution](/dotnet/framework/data/adonet/ef/language-reference/query-execution).</span></span>

<span data-ttu-id="39c5d-114">注意:[Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) 方法是在資料庫上執行，而不是在上方顯示的 C# 程式碼中執行。</span><span class="sxs-lookup"><span data-stu-id="39c5d-114">Note: The [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) method is run on the database, not in the c# code shown above.</span></span> <span data-ttu-id="39c5d-115">查詢是否區分大小寫取決於資料庫和定序。</span><span class="sxs-lookup"><span data-stu-id="39c5d-115">The case sensitivity on the query depends on the database and the collation.</span></span> <span data-ttu-id="39c5d-116">在 SQL Server 上，[Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) 對應至 [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql)，因此不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="39c5d-116">On SQL Server, [Contains](/dotnet/api/system.data.objects.dataclasses.entitycollection-1.contains) maps to [SQL LIKE](/sql/t-sql/language-elements/like-transact-sql), which is case insensitive.</span></span> <span data-ttu-id="39c5d-117">在 SQLlite 中，由於使用預設定序，它會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="39c5d-117">In SQLlite, with the default collation, it's case sensitive.</span></span>

<span data-ttu-id="39c5d-118">巡覽至 `/Movies/Index`。</span><span class="sxs-lookup"><span data-stu-id="39c5d-118">Navigate to `/Movies/Index`.</span></span> <span data-ttu-id="39c5d-119">將查詢字串 (例如 `?searchString=Ghost`) 附加至 URL。</span><span class="sxs-lookup"><span data-stu-id="39c5d-119">Append a query string such as `?searchString=Ghost` to the URL.</span></span> <span data-ttu-id="39c5d-120">隨即顯示篩選過的電影。</span><span class="sxs-lookup"><span data-stu-id="39c5d-120">The filtered movies are displayed.</span></span>

![索引檢視](~/tutorials/first-mvc-app/search/_static/ghost.png)

<span data-ttu-id="39c5d-122">如果您將 `Index` 方法的簽章變更為包含名為 `id` 的參數，則 `id` 參數會比對 *Startup.cs* 中所設定之預設路由的選擇性 `{id}` 預留位置。</span><span class="sxs-lookup"><span data-stu-id="39c5d-122">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the optional `{id}` placeholder for the default routes set in *Startup.cs*.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]
