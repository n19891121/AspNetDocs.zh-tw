---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: 使用 ASP.NET Web API 2 中的屬性路由建立 REST API |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: f6ff5fa18a44b3e6717ec0141ebe101bcdc0bee4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045178"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="2a000-102">使用 ASP.NET Web API 2 中的屬性路由建立 REST API</span><span class="sxs-lookup"><span data-stu-id="2a000-102">Create a REST API with Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="2a000-103">由 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2a000-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2a000-104">Web API 2 支援新的路由類型，稱為 *屬性路由*。</span><span class="sxs-lookup"><span data-stu-id="2a000-104">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="2a000-105">如需屬性路由的一般總覽，請參閱 [WEB API 2 中的屬性路由](attribute-routing-in-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="2a000-105">For a general overview of attribute routing, see [Attribute Routing in Web API 2](attribute-routing-in-web-api-2.md).</span></span> <span data-ttu-id="2a000-106">在本教學課程中，您將使用屬性路由來建立書籍集合的 REST API。</span><span class="sxs-lookup"><span data-stu-id="2a000-106">In this tutorial, you will use attribute routing to create a REST API for a collection of books.</span></span> <span data-ttu-id="2a000-107">API 將支援下列動作：</span><span class="sxs-lookup"><span data-stu-id="2a000-107">The API will support the following actions:</span></span>

| <span data-ttu-id="2a000-108">動作</span><span class="sxs-lookup"><span data-stu-id="2a000-108">Action</span></span> | <span data-ttu-id="2a000-109">範例 URI</span><span class="sxs-lookup"><span data-stu-id="2a000-109">Example URI</span></span> |
| --- | --- |
| <span data-ttu-id="2a000-110">取得所有書籍的清單。</span><span class="sxs-lookup"><span data-stu-id="2a000-110">Get a list of all books.</span></span> | <span data-ttu-id="2a000-111">/api/books</span><span class="sxs-lookup"><span data-stu-id="2a000-111">/api/books</span></span> |
| <span data-ttu-id="2a000-112">依識別碼取得書籍。</span><span class="sxs-lookup"><span data-stu-id="2a000-112">Get a book by ID.</span></span> | <span data-ttu-id="2a000-113">/api/books/1</span><span class="sxs-lookup"><span data-stu-id="2a000-113">/api/books/1</span></span> |
| <span data-ttu-id="2a000-114">取得書籍的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2a000-114">Get the details of a book.</span></span> | <span data-ttu-id="2a000-115">/api/books/1/details</span><span class="sxs-lookup"><span data-stu-id="2a000-115">/api/books/1/details</span></span> |
| <span data-ttu-id="2a000-116">依內容類型取得書籍清單。</span><span class="sxs-lookup"><span data-stu-id="2a000-116">Get a list of books by genre.</span></span> | <span data-ttu-id="2a000-117">/api/books/fantasy</span><span class="sxs-lookup"><span data-stu-id="2a000-117">/api/books/fantasy</span></span> |
| <span data-ttu-id="2a000-118">依發行日期取得書籍清單。</span><span class="sxs-lookup"><span data-stu-id="2a000-118">Get a list of books by publication date.</span></span> | <span data-ttu-id="2a000-119">/api/books/date/2013-02-16/api/books/date/2013/02/16 (替代表單) </span><span class="sxs-lookup"><span data-stu-id="2a000-119">/api/books/date/2013-02-16 /api/books/date/2013/02/16 (alternate form)</span></span> |
| <span data-ttu-id="2a000-120">取得特定作者的書籍清單。</span><span class="sxs-lookup"><span data-stu-id="2a000-120">Get a list of books by a particular author.</span></span> | <span data-ttu-id="2a000-121">/api/authors/1/books</span><span class="sxs-lookup"><span data-stu-id="2a000-121">/api/authors/1/books</span></span> |

<span data-ttu-id="2a000-122">所有方法都是唯讀 (HTTP GET 要求) 。</span><span class="sxs-lookup"><span data-stu-id="2a000-122">All methods are read-only (HTTP GET requests).</span></span>

<span data-ttu-id="2a000-123">針對資料層，我們會使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="2a000-123">For the data layer, we'll use Entity Framework.</span></span> <span data-ttu-id="2a000-124">書籍記錄會有下欄欄位：</span><span class="sxs-lookup"><span data-stu-id="2a000-124">Book records will have the following fields:</span></span>

- <span data-ttu-id="2a000-125">識別碼</span><span class="sxs-lookup"><span data-stu-id="2a000-125">ID</span></span>
- <span data-ttu-id="2a000-126">標題</span><span class="sxs-lookup"><span data-stu-id="2a000-126">Title</span></span>
- <span data-ttu-id="2a000-127">Genre</span><span class="sxs-lookup"><span data-stu-id="2a000-127">Genre</span></span>
- <span data-ttu-id="2a000-128">發行日期</span><span class="sxs-lookup"><span data-stu-id="2a000-128">Publication date</span></span>
- <span data-ttu-id="2a000-129">價格</span><span class="sxs-lookup"><span data-stu-id="2a000-129">Price</span></span>
- <span data-ttu-id="2a000-130">描述</span><span class="sxs-lookup"><span data-stu-id="2a000-130">Description</span></span>
- <span data-ttu-id="2a000-131">作者 (外鍵給作者資料表) </span><span class="sxs-lookup"><span data-stu-id="2a000-131">AuthorID (foreign key to an Authors table)</span></span>

<span data-ttu-id="2a000-132">但是針對大部分的要求，API 會傳回此資料的子集 (標題、作者和內容類型) 。</span><span class="sxs-lookup"><span data-stu-id="2a000-132">For most requests, however, the API will return a subset of this data (title, author, and genre).</span></span> <span data-ttu-id="2a000-133">若要取得完整記錄，用戶端要求 `/api/books/{id}/details` 。</span><span class="sxs-lookup"><span data-stu-id="2a000-133">To get the complete record, the client requests `/api/books/{id}/details`.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a000-134">先決條件</span><span class="sxs-lookup"><span data-stu-id="2a000-134">Prerequisites</span></span>

<span data-ttu-id="2a000-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) 社區、Professional 或 Enterprise edition。</span><span class="sxs-lookup"><span data-stu-id="2a000-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="2a000-136">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="2a000-136">Create the Visual Studio Project</span></span>

<span data-ttu-id="2a000-137">從執行 Visual Studio 開始。</span><span class="sxs-lookup"><span data-stu-id="2a000-137">Start by running Visual Studio.</span></span> <span data-ttu-id="2a000-138">從 [檔案]\*\*\*\* 功能表選取 [新增]\*\*\*\*，再選取 [專案]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="2a000-138">From the **File** menu, select **New** and then select **Project**.</span></span>

<span data-ttu-id="2a000-139">展開 [**已安裝**的  >  **Visual c #** ] 類別。</span><span class="sxs-lookup"><span data-stu-id="2a000-139">Expand the **Installed** > **Visual C#** category.</span></span> <span data-ttu-id="2a000-140">選取 [ **Visual c #**] 底下的 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="2a000-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="2a000-141">在專案範本清單中，選取 [ \*\*ASP.NET Web 應用程式 (] .NET Framework) \*\*。</span><span class="sxs-lookup"><span data-stu-id="2a000-141">In the list of project templates, select **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="2a000-142">將專案命名為 &quot; >booksapi &quot; 。</span><span class="sxs-lookup"><span data-stu-id="2a000-142">Name the project &quot;BooksAPI&quot;.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

<span data-ttu-id="2a000-143">在 [ **新增 ASP.NET Web 應用程式** ] 對話方塊中，選取 **空白** 範本。</span><span class="sxs-lookup"><span data-stu-id="2a000-143">In the **New ASP.NET Web Application** dialog, select the **Empty** template.</span></span> <span data-ttu-id="2a000-144">在 [新增資料夾和核心參考] 底下，選取 [ **WEB API** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="2a000-144">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="2a000-145">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2a000-145">Click **OK**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

<span data-ttu-id="2a000-146">這會建立針對 Web API 功能設定的基本架構專案。</span><span class="sxs-lookup"><span data-stu-id="2a000-146">This creates a skeleton project that is configured for Web API functionality.</span></span>

### <a name="domain-models"></a><span data-ttu-id="2a000-147">領域模型</span><span class="sxs-lookup"><span data-stu-id="2a000-147">Domain Models</span></span>

<span data-ttu-id="2a000-148">接下來，加入網域模型的類別。</span><span class="sxs-lookup"><span data-stu-id="2a000-148">Next, add classes for domain models.</span></span> <span data-ttu-id="2a000-149">在 [方案總管] 中，於 Models 資料夾上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="2a000-149">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="2a000-150">選取 [ **新增**]，然後選取 [ **類別**]。</span><span class="sxs-lookup"><span data-stu-id="2a000-150">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="2a000-151">將類別命名為 `Author`。</span><span class="sxs-lookup"><span data-stu-id="2a000-151">Name the class `Author`.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

<span data-ttu-id="2a000-152">以下列程式碼取代 Author.cs 中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="2a000-152">Replace the code in Author.cs with the following:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

<span data-ttu-id="2a000-153">現在新增另一個名為 `Book` 的類別。</span><span class="sxs-lookup"><span data-stu-id="2a000-153">Now add another class named `Book`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a><span data-ttu-id="2a000-154">新增 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="2a000-154">Add a Web API Controller</span></span>

<span data-ttu-id="2a000-155">在此步驟中，我們將新增使用 Entity Framework 作為資料層的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="2a000-155">In this step, we'll add a Web API controller that uses Entity Framework as the data layer.</span></span>

<span data-ttu-id="2a000-156">按 CTRL+SHIFT+B 以建置專案。</span><span class="sxs-lookup"><span data-stu-id="2a000-156">Press CTRL+SHIFT+B to build the project.</span></span> <span data-ttu-id="2a000-157">Entity Framework 使用反映來探索模型的屬性，因此需要已編譯的元件才能建立資料庫架構。</span><span class="sxs-lookup"><span data-stu-id="2a000-157">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

<span data-ttu-id="2a000-158">在 [方案總管] 中，於 Controllers 資料夾上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="2a000-158">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="2a000-159">選取 [ **新增**]，然後選取 [ **控制器**]。</span><span class="sxs-lookup"><span data-stu-id="2a000-159">Select **Add**, then select **Controller**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

<span data-ttu-id="2a000-160">在 [ **新增 Scaffold** ] 對話方塊中， **使用 Entity Framework 選取 [具有動作的 Web API 2 控制器**]。</span><span class="sxs-lookup"><span data-stu-id="2a000-160">In the **Add Scaffold** dialog, select **Web API 2 Controller with actions, using Entity Framework**.</span></span>

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

<span data-ttu-id="2a000-161">在 [ **新增控制器** ] 對話方塊中，針對 [ **控制器名稱**] 輸入 &quot; BooksController &quot; 。</span><span class="sxs-lookup"><span data-stu-id="2a000-161">In the **Add Controller** dialog, for **Controller name**, enter &quot;BooksController&quot;.</span></span> <span data-ttu-id="2a000-162">選取 [ &quot; 使用非同步控制器動作 &quot; ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="2a000-162">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="2a000-163">針對 [ **模型類別**]，選取 [ &quot; 書籍] &quot; 。</span><span class="sxs-lookup"><span data-stu-id="2a000-163">For **Model class**, select &quot;Book&quot;.</span></span> <span data-ttu-id="2a000-164"> (如果您沒有看到 `Book` 下拉式清單中列出的類別，請確定您已建立專案。 ) 然後按一下 [+] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2a000-164">(If you don't see the `Book` class listed in the dropdown, make sure that you built the project.) Then click the "+" button.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

<span data-ttu-id="2a000-165">按一下 [**新增資料內容**] 對話方塊中的 [**加入**]。</span><span class="sxs-lookup"><span data-stu-id="2a000-165">Click **Add** in the **New Data Context** dialog.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

<span data-ttu-id="2a000-166">按一下 [**新增控制器**] 對話方塊中的 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="2a000-166">Click **Add** in the **Add Controller** dialog.</span></span> <span data-ttu-id="2a000-167">此樣板會新增名為 `BooksController` 的類別，該類別會定義 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="2a000-167">The scaffolding adds a class named `BooksController` that defines the API controller.</span></span> <span data-ttu-id="2a000-168">它也會在 [模型] 資料夾中加入名為的類別 `BooksAPIContext` ，該類別會定義 Entity Framework 的資料內容。</span><span class="sxs-lookup"><span data-stu-id="2a000-168">It also adds a class named `BooksAPIContext` in the Models folder, which defines the data context for Entity Framework.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a><span data-ttu-id="2a000-169">植入資料庫</span><span class="sxs-lookup"><span data-stu-id="2a000-169">Seed the Database</span></span>

<span data-ttu-id="2a000-170">從 [工具] 功能表選取 [ **NuGet 封裝管理員**]，然後選取 **封裝管理員主控台**。</span><span class="sxs-lookup"><span data-stu-id="2a000-170">From the Tools menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

<span data-ttu-id="2a000-171">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="2a000-171">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

<span data-ttu-id="2a000-172">此命令會建立一個 [遷移] 資料夾，並新增名為 Configuration.cs 的新程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="2a000-172">This command creates a Migrations folder and adds a new code file named Configuration.cs.</span></span> <span data-ttu-id="2a000-173">開啟此檔案，並將下列程式碼加入至 `Configuration.Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="2a000-173">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

<span data-ttu-id="2a000-174">在封裝管理員主控台] 視窗中，輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="2a000-174">In the Package Manager Console window, type the following commands.</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

<span data-ttu-id="2a000-175">這些命令會建立本機資料庫，並叫用種子方法來填入資料庫。</span><span class="sxs-lookup"><span data-stu-id="2a000-175">These commands create a local database and invoke the Seed method to populate the database.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a><span data-ttu-id="2a000-176">新增 DTO 類別</span><span class="sxs-lookup"><span data-stu-id="2a000-176">Add DTO Classes</span></span>

<span data-ttu-id="2a000-177">如果您現在執行應用程式，並將 GET 要求傳送至/api/books/1，回應看起來會像下面這樣。</span><span class="sxs-lookup"><span data-stu-id="2a000-177">If you run the application now and send a GET request to /api/books/1, the response looks similar to the following.</span></span> <span data-ttu-id="2a000-178"> (我新增了縮排，以提供可讀性。 ) </span><span class="sxs-lookup"><span data-stu-id="2a000-178">(I added indentation for readability.)</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

<span data-ttu-id="2a000-179">相反地，我希望此要求傳回欄位的子集。</span><span class="sxs-lookup"><span data-stu-id="2a000-179">Instead, I want this request to return a subset of the fields.</span></span> <span data-ttu-id="2a000-180">此外，我希望它傳回作者的姓名，而不是作者識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a000-180">Also, I want it to return the author's name, rather than the author ID.</span></span> <span data-ttu-id="2a000-181">為了達成此目的，我們將修改控制器方法，以 *傳回資料傳輸物件* (DTO) 而非 EF 模型。</span><span class="sxs-lookup"><span data-stu-id="2a000-181">To accomplish this, we'll modify the controller methods to return a *data transfer object* (DTO) instead of the EF model.</span></span> <span data-ttu-id="2a000-182">DTO 是專為攜帶資料而設計的物件。</span><span class="sxs-lookup"><span data-stu-id="2a000-182">A DTO is an object that is designed only to carry data.</span></span>

<span data-ttu-id="2a000-183">在方案總管中，以滑鼠右鍵按一下專案，**然後選取 [**  |  **新增資料夾**]。</span><span class="sxs-lookup"><span data-stu-id="2a000-183">In Solution Explorer, right-click the project and select **Add** | **New Folder**.</span></span> <span data-ttu-id="2a000-184">將資料夾命名為 &quot; dto &quot; 。</span><span class="sxs-lookup"><span data-stu-id="2a000-184">Name the folder &quot;DTOs&quot;.</span></span> <span data-ttu-id="2a000-185">`BookDto`使用下列定義，將名為的類別新增至 dto 資料夾：</span><span class="sxs-lookup"><span data-stu-id="2a000-185">Add a class named `BookDto` to the DTOs folder, with the following definition:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

<span data-ttu-id="2a000-186">新增另一個名為 `BookDetailDto`的類別。</span><span class="sxs-lookup"><span data-stu-id="2a000-186">Add another class named `BookDetailDto`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

<span data-ttu-id="2a000-187">接下來，更新 `BooksController` 類別以傳回 `BookDto` 實例。</span><span class="sxs-lookup"><span data-stu-id="2a000-187">Next, update the `BooksController` class to return `BookDto` instances.</span></span> <span data-ttu-id="2a000-188">我們將使用可 [查詢的. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) 方法將 `Book` 實例投影至 `BookDto` 實例。</span><span class="sxs-lookup"><span data-stu-id="2a000-188">We'll use the [Queryable.Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) method to project `Book` instances to `BookDto` instances.</span></span> <span data-ttu-id="2a000-189">以下是控制器類別的更新程式碼。</span><span class="sxs-lookup"><span data-stu-id="2a000-189">Here is the updated code for the controller class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> <span data-ttu-id="2a000-190">我刪除了 `PutBook` 、 `PostBook` 和 `DeleteBook` 方法，因為本教學課程不需要它們。</span><span class="sxs-lookup"><span data-stu-id="2a000-190">I deleted the `PutBook`, `PostBook`, and `DeleteBook` methods, because they aren't needed for this tutorial.</span></span>

<span data-ttu-id="2a000-191">現在，如果您執行應用程式並要求/api/books/1，回應主體看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="2a000-191">Now if you run the application and request /api/books/1, the response body should look like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a><span data-ttu-id="2a000-192">新增路由屬性</span><span class="sxs-lookup"><span data-stu-id="2a000-192">Add Route Attributes</span></span>

<span data-ttu-id="2a000-193">接下來，我們會將控制器轉換成使用屬性路由。</span><span class="sxs-lookup"><span data-stu-id="2a000-193">Next, we'll convert the controller to use attribute routing.</span></span> <span data-ttu-id="2a000-194">首先，將 **RoutePrefix** 屬性新增至控制器。</span><span class="sxs-lookup"><span data-stu-id="2a000-194">First, add a **RoutePrefix** attribute to the controller.</span></span> <span data-ttu-id="2a000-195">這個屬性會定義此控制器上所有方法的初始 URI 區段。</span><span class="sxs-lookup"><span data-stu-id="2a000-195">This attribute defines the initial URI segments for all methods on this controller.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

<span data-ttu-id="2a000-196">然後，將 **[Route]** 屬性新增至控制器動作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2a000-196">Then add **[Route]** attributes to the controller actions, as follows:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

<span data-ttu-id="2a000-197">每個控制器方法的路由範本都是前置詞加上 **route** 屬性中所指定的字串。</span><span class="sxs-lookup"><span data-stu-id="2a000-197">The route template for each controller method is the prefix plus the string specified in the **Route** attribute.</span></span> <span data-ttu-id="2a000-198">如果是 `GetBook` 方法，路由範本會包含參數化的字串 &quot; {id： int} &quot; ，如果 URI 區段包含整數值，則會相符。</span><span class="sxs-lookup"><span data-stu-id="2a000-198">For the `GetBook` method, the route template includes the parameterized string &quot;{id:int}&quot;, which matches if the URI segment contains an integer value.</span></span>

| <span data-ttu-id="2a000-199">方法</span><span class="sxs-lookup"><span data-stu-id="2a000-199">Method</span></span> | <span data-ttu-id="2a000-200">路由範本</span><span class="sxs-lookup"><span data-stu-id="2a000-200">Route Template</span></span> | <span data-ttu-id="2a000-201">範例 URI</span><span class="sxs-lookup"><span data-stu-id="2a000-201">Example URI</span></span> |
| --- | --- | --- |
| `GetBooks` | <span data-ttu-id="2a000-202">「api/書籍」</span><span class="sxs-lookup"><span data-stu-id="2a000-202">"api/books"</span></span> | `http://localhost/api/books` |
| `GetBook` | <span data-ttu-id="2a000-203">"api/書籍/{id： int}"</span><span class="sxs-lookup"><span data-stu-id="2a000-203">"api/books/{id:int}"</span></span> | `http://localhost/api/books/5` |

## <a name="get-book-details"></a><span data-ttu-id="2a000-204">取得書籍詳細資料</span><span class="sxs-lookup"><span data-stu-id="2a000-204">Get Book Details</span></span>

<span data-ttu-id="2a000-205">為了取得書籍詳細資料，用戶端會將 GET 要求傳送至 `/api/books/{id}/details` ，其中 *{id}* 是書籍的識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a000-205">To get book details, the client will send a GET request to `/api/books/{id}/details`, where *{id}* is the ID of the book.</span></span>

<span data-ttu-id="2a000-206">將下列方法新增至 `BooksController` 類別。</span><span class="sxs-lookup"><span data-stu-id="2a000-206">Add the following method to the `BooksController` class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

<span data-ttu-id="2a000-207">如果您要求 `/api/books/1/details` ，回應看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="2a000-207">If you request `/api/books/1/details`, the response looks like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a><span data-ttu-id="2a000-208">依內容類型取得書籍</span><span class="sxs-lookup"><span data-stu-id="2a000-208">Get Books By Genre</span></span>

<span data-ttu-id="2a000-209">若要取得特定類型的書籍清單，用戶端會將 GET 要求傳送至，其中內容類型是內容類型的 `/api/books/genre` 名稱。 *genre*</span><span class="sxs-lookup"><span data-stu-id="2a000-209">To get a list of books in a specific genre, the client will send a GET request to `/api/books/genre`, where *genre* is the name of the genre.</span></span> <span data-ttu-id="2a000-210">(例如，`/api/books/fantasy`)。</span><span class="sxs-lookup"><span data-stu-id="2a000-210">(For example, `/api/books/fantasy`.)</span></span>

<span data-ttu-id="2a000-211">將下列方法新增至 `BooksController` 。</span><span class="sxs-lookup"><span data-stu-id="2a000-211">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

<span data-ttu-id="2a000-212">在這裡，我們會在 URI 範本中定義包含 {類型} 參數的路由。</span><span class="sxs-lookup"><span data-stu-id="2a000-212">Here we are defining a route that contains a {genre} parameter in the URI template.</span></span> <span data-ttu-id="2a000-213">請注意，Web API 可以區分這兩個 Uri，並將其路由傳送至不同的方法：</span><span class="sxs-lookup"><span data-stu-id="2a000-213">Notice that Web API is able to distinguish these two URIs and route them to different methods:</span></span>

`/api/books/1`

`/api/books/fantasy`

<span data-ttu-id="2a000-214">這是因為 `GetBook` 方法包含「識別碼」區段必須是整數值的條件約束：</span><span class="sxs-lookup"><span data-stu-id="2a000-214">That's because the `GetBook` method includes a constraint that the "id" segment must be an integer value:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

<span data-ttu-id="2a000-215">如果您要求/api/books/fantasy，回應看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="2a000-215">If you request /api/books/fantasy, the response looks like this:</span></span>

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a><span data-ttu-id="2a000-216">依作者取得書籍</span><span class="sxs-lookup"><span data-stu-id="2a000-216">Get Books By Author</span></span>

<span data-ttu-id="2a000-217">為了取得特定作者的書籍清單，用戶端會將 GET 要求傳送至 `/api/authors/id/books` ，其中 *id* 是作者的識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a000-217">To get a list of a books for a particular author, the client will send a GET request to `/api/authors/id/books`, where *id* is the ID of the author.</span></span>

<span data-ttu-id="2a000-218">將下列方法新增至 `BooksController` 。</span><span class="sxs-lookup"><span data-stu-id="2a000-218">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

<span data-ttu-id="2a000-219">這個範例很有趣，因為 &quot; 書籍 &quot; 會被視為作者的子資源 &quot; &quot; 。</span><span class="sxs-lookup"><span data-stu-id="2a000-219">This example is interesting because &quot;books&quot; is treated a child resource of &quot;authors&quot;.</span></span> <span data-ttu-id="2a000-220">此模式在 RESTful Api 中相當常見。</span><span class="sxs-lookup"><span data-stu-id="2a000-220">This pattern is quite common in RESTful APIs.</span></span>

<span data-ttu-id="2a000-221">路由範本中的波浪線 (~) 會覆寫 **RoutePrefix** 屬性中的路由前置詞。</span><span class="sxs-lookup"><span data-stu-id="2a000-221">The tilde (~) in the route template overrides the route prefix in the **RoutePrefix** attribute.</span></span>

## <a name="get-books-by-publication-date"></a><span data-ttu-id="2a000-222">依發行日期取得書籍</span><span class="sxs-lookup"><span data-stu-id="2a000-222">Get Books By Publication Date</span></span>

<span data-ttu-id="2a000-223">若要依發行日期取得書籍清單，用戶端會將 GET 要求傳送至 `/api/books/date/yyyy-mm-dd` ，其中 *yyyy mm* 為日期。</span><span class="sxs-lookup"><span data-stu-id="2a000-223">To get a list of books by publication date, the client will send a GET request to `/api/books/date/yyyy-mm-dd`, where *yyyy-mm-dd* is the date.</span></span>

<span data-ttu-id="2a000-224">以下是執行這項作業的一種方式：</span><span class="sxs-lookup"><span data-stu-id="2a000-224">Here is one way to do this:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

<span data-ttu-id="2a000-225">`{pubdate:datetime}`參數限制為符合**日期時間**值。</span><span class="sxs-lookup"><span data-stu-id="2a000-225">The `{pubdate:datetime}` parameter is constrained to match a **DateTime** value.</span></span> <span data-ttu-id="2a000-226">這是可行的，但其實比我們想要的還寬鬆。</span><span class="sxs-lookup"><span data-stu-id="2a000-226">This works, but it's actually more permissive than we'd like.</span></span> <span data-ttu-id="2a000-227">例如，這些 Uri 也會與路由相符：</span><span class="sxs-lookup"><span data-stu-id="2a000-227">For example, these URIs will also match the route:</span></span>

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

<span data-ttu-id="2a000-228">允許這些 Uri 沒有任何問題。</span><span class="sxs-lookup"><span data-stu-id="2a000-228">There's nothing wrong with allowing these URIs.</span></span> <span data-ttu-id="2a000-229">不過，您可以將正則運算式條件約束新增至路由範本，以限制特定格式的路由：</span><span class="sxs-lookup"><span data-stu-id="2a000-229">However, you can restrict the route to a particular format by adding a regular-expression constraint to the route template:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

<span data-ttu-id="2a000-230">現在只有格式為 yyyy-mm-dd 的日期才 &quot; &quot; 會相符。</span><span class="sxs-lookup"><span data-stu-id="2a000-230">Now only dates in the form &quot;yyyy-mm-dd&quot; will match.</span></span> <span data-ttu-id="2a000-231">請注意，我們不會使用 RegEx 來驗證我們是否有實際的日期。</span><span class="sxs-lookup"><span data-stu-id="2a000-231">Notice that we don't use the regex to validate that we got a real date.</span></span> <span data-ttu-id="2a000-232">當 Web API 嘗試將 URI 區段轉換成 **DateTime** 實例時，便會進行處理。</span><span class="sxs-lookup"><span data-stu-id="2a000-232">That is handled when Web API tries to convert the URI segment into a **DateTime** instance.</span></span> <span data-ttu-id="2a000-233">不正確日期，例如 ' 2012-47-99 ' 將無法轉換，而且用戶端會收到404錯誤。</span><span class="sxs-lookup"><span data-stu-id="2a000-233">An invalid date such as '2012-47-99' will fail to be converted, and the client will get a 404 error.</span></span>

<span data-ttu-id="2a000-234">您也可以 `/api/books/date/yyyy/mm/dd` 使用不同的 RegEx 來新增另一個 **[Route]** 屬性，以支援 () 的斜線分隔符號。</span><span class="sxs-lookup"><span data-stu-id="2a000-234">You can also support a slash separator (`/api/books/date/yyyy/mm/dd`) by adding another **[Route]** attribute with a different regex.</span></span>

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

<span data-ttu-id="2a000-235">這裡有一個很微妙但很重要的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2a000-235">There is a subtle but important detail here.</span></span> <span data-ttu-id="2a000-236">第二個路由範本在 \* {pubdate} 參數的開頭有萬用字元字元 () ：</span><span class="sxs-lookup"><span data-stu-id="2a000-236">The second route template has a wildcard character (\*) at the start of the {pubdate} parameter:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.txt)]

<span data-ttu-id="2a000-237">這會告訴路由引擎 {pubdate} 應該符合 URI 的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="2a000-237">This tells the routing engine that {pubdate} should match the rest of the URI.</span></span> <span data-ttu-id="2a000-238">範本參數預設會符合單一 URI 區段。</span><span class="sxs-lookup"><span data-stu-id="2a000-238">By default, a template parameter matches a single URI segment.</span></span> <span data-ttu-id="2a000-239">在此情況下，我們希望 {pubdate} 跨越數個 URI 區段：</span><span class="sxs-lookup"><span data-stu-id="2a000-239">In this case, we want {pubdate} to span several URI segments:</span></span>

`/api/books/date/2013/06/17`

## <a name="controller-code"></a><span data-ttu-id="2a000-240">控制器程式碼</span><span class="sxs-lookup"><span data-stu-id="2a000-240">Controller Code</span></span>

<span data-ttu-id="2a000-241">以下是 BooksController 類別的完整程式碼。</span><span class="sxs-lookup"><span data-stu-id="2a000-241">Here is the complete code for the BooksController class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a><span data-ttu-id="2a000-242">總結</span><span class="sxs-lookup"><span data-stu-id="2a000-242">Summary</span></span>

<span data-ttu-id="2a000-243">當您設計 API 的 Uri 時，屬性路由可提供更多的控制權和更大的彈性。</span><span class="sxs-lookup"><span data-stu-id="2a000-243">Attribute routing gives you more control and greater flexibility when designing the URIs for your API.</span></span>
