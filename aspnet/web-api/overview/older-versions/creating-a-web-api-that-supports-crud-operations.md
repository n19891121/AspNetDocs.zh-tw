---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: 提供 CRUD 作業，在 ASP.NET Web API 1-ASP.NET 4.x
author: MikeWasson
description: 教學課程會示範如何使用適用於 ASP.NET 的 ASP.NET Web API HTTP 服務中支援的 CRUD 作業 4.x。
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: 3c2a41482b7f9b60a8864b853df23ab5991b6da7
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65108736"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a><span data-ttu-id="1ec6f-103">啟用 ASP.NET Web API 1 中的 CRUD 作業</span><span class="sxs-lookup"><span data-stu-id="1ec6f-103">Enabling CRUD Operations in ASP.NET Web API 1</span></span>

<span data-ttu-id="1ec6f-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1ec6f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="1ec6f-105">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="1ec6f-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> <span data-ttu-id="1ec6f-106">本教學課程示範如何使用適用於 ASP.NET 的 ASP.NET Web API HTTP 服務中支援的 CRUD 作業 4.x。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-106">This tutorial shows how to support CRUD operations in an HTTP service using ASP.NET Web API for ASP.NET 4.x.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1ec6f-107">在本教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="1ec6f-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="1ec6f-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="1ec6f-108">Visual Studio 2012</span></span>
> - <span data-ttu-id="1ec6f-109">Web API 1 （也適用於使用 Web API 2）</span><span class="sxs-lookup"><span data-stu-id="1ec6f-109">Web API 1 (also works with Web API 2)</span></span>

<span data-ttu-id="1ec6f-110">代表 CRUD&quot;建立、 讀取、 更新和刪除，&quot;是四個基本資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-110">CRUD stands for &quot;Create, Read, Update, and Delete,&quot; which are the four basic database operations.</span></span> <span data-ttu-id="1ec6f-111">許多 HTTP 服務也模型透過 REST 或 REST 型 Api 的 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-111">Many HTTP services also model CRUD operations through REST or REST-like APIs.</span></span>

<span data-ttu-id="1ec6f-112">在本教學課程中，您將建置非常簡單的 web API 以管理的產品清單。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-112">In this tutorial, you will build a very simple web API to manage a list of products.</span></span> <span data-ttu-id="1ec6f-113">每項產品會包含名稱、 價格和類別目錄 (例如&quot;toys&quot;或是&quot;硬體&quot;)，再加上產品識別碼。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-113">Each product will contain a name, price, and category (such as &quot;toys&quot; or &quot;hardware&quot;), plus a product ID.</span></span>

<span data-ttu-id="1ec6f-114">產品的 API 會公開下列方法。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-114">The products API will expose following methods.</span></span>

| <span data-ttu-id="1ec6f-115">動作</span><span class="sxs-lookup"><span data-stu-id="1ec6f-115">Action</span></span> | <span data-ttu-id="1ec6f-116">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1ec6f-116">HTTP method</span></span> | <span data-ttu-id="1ec6f-117">相對 URI</span><span class="sxs-lookup"><span data-stu-id="1ec6f-117">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1ec6f-118">取得所有產品的清單</span><span class="sxs-lookup"><span data-stu-id="1ec6f-118">Get a list of all products</span></span> | <span data-ttu-id="1ec6f-119">GET</span><span class="sxs-lookup"><span data-stu-id="1ec6f-119">GET</span></span> | <span data-ttu-id="1ec6f-120">/api/products</span><span class="sxs-lookup"><span data-stu-id="1ec6f-120">/api/products</span></span> |
| <span data-ttu-id="1ec6f-121">取得產品識別碼</span><span class="sxs-lookup"><span data-stu-id="1ec6f-121">Get a product by ID</span></span> | <span data-ttu-id="1ec6f-122">GET</span><span class="sxs-lookup"><span data-stu-id="1ec6f-122">GET</span></span> | <span data-ttu-id="1ec6f-123">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="1ec6f-123">/api/products/*id*</span></span> |
| <span data-ttu-id="1ec6f-124">依類別取得的產品</span><span class="sxs-lookup"><span data-stu-id="1ec6f-124">Get a product by category</span></span> | <span data-ttu-id="1ec6f-125">GET</span><span class="sxs-lookup"><span data-stu-id="1ec6f-125">GET</span></span> | <span data-ttu-id="1ec6f-126">/api/products?category=*category*</span><span class="sxs-lookup"><span data-stu-id="1ec6f-126">/api/products?category=*category*</span></span> |
| <span data-ttu-id="1ec6f-127">建立新的產品</span><span class="sxs-lookup"><span data-stu-id="1ec6f-127">Create a new product</span></span> | <span data-ttu-id="1ec6f-128">POST</span><span class="sxs-lookup"><span data-stu-id="1ec6f-128">POST</span></span> | <span data-ttu-id="1ec6f-129">/api/products</span><span class="sxs-lookup"><span data-stu-id="1ec6f-129">/api/products</span></span> |
| <span data-ttu-id="1ec6f-130">將產品更新</span><span class="sxs-lookup"><span data-stu-id="1ec6f-130">Update a product</span></span> | <span data-ttu-id="1ec6f-131">PUT</span><span class="sxs-lookup"><span data-stu-id="1ec6f-131">PUT</span></span> | <span data-ttu-id="1ec6f-132">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="1ec6f-132">/api/products/*id*</span></span> |
| <span data-ttu-id="1ec6f-133">刪除產品</span><span class="sxs-lookup"><span data-stu-id="1ec6f-133">Delete a product</span></span> | <span data-ttu-id="1ec6f-134">DELETE</span><span class="sxs-lookup"><span data-stu-id="1ec6f-134">DELETE</span></span> | <span data-ttu-id="1ec6f-135">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="1ec6f-135">/api/products/*id*</span></span> |

<span data-ttu-id="1ec6f-136">請注意一些 Uri 路徑中包含產品識別碼。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-136">Notice that some of the URIs include the product ID in path.</span></span> <span data-ttu-id="1ec6f-137">例如，若要取得其識別碼為 28 的產品，用戶端傳送 GET 要求`http://hostname/api/products/28`。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-137">For example, to get the product whose ID is 28, the client sends a GET request for `http://hostname/api/products/28`.</span></span>

### <a name="resources"></a><span data-ttu-id="1ec6f-138">資源</span><span class="sxs-lookup"><span data-stu-id="1ec6f-138">Resources</span></span>

<span data-ttu-id="1ec6f-139">產品的 API 會定義兩種資源類型的 Uri:</span><span class="sxs-lookup"><span data-stu-id="1ec6f-139">The products API defines URIs for two resource types:</span></span>

| <span data-ttu-id="1ec6f-140">資源</span><span class="sxs-lookup"><span data-stu-id="1ec6f-140">Resource</span></span> | <span data-ttu-id="1ec6f-141">URI</span><span class="sxs-lookup"><span data-stu-id="1ec6f-141">URI</span></span> |
| --- | --- |
| <span data-ttu-id="1ec6f-142">所有產品的清單。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-142">The list of all the products.</span></span> | <span data-ttu-id="1ec6f-143">/api/products</span><span class="sxs-lookup"><span data-stu-id="1ec6f-143">/api/products</span></span> |
| <span data-ttu-id="1ec6f-144">個別的產品。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-144">An individual product.</span></span> | <span data-ttu-id="1ec6f-145">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="1ec6f-145">/api/products/*id*</span></span> |

### <a name="methods"></a><span data-ttu-id="1ec6f-146">方法</span><span class="sxs-lookup"><span data-stu-id="1ec6f-146">Methods</span></span>

<span data-ttu-id="1ec6f-147">四個主要 HTTP 方法 （GET、 PUT、 POST 和 DELETE） 可以對應至 CRUD 作業，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-147">The four main HTTP methods (GET, PUT, POST, and DELETE) can be mapped to CRUD operations as follows:</span></span>

- <span data-ttu-id="1ec6f-148">取得作業會擷取指定之 URI 的資源的表示法。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-148">GET retrieves the representation of the resource at a specified URI.</span></span> <span data-ttu-id="1ec6f-149">取得應該在伺服器上沒有任何副作用。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-149">GET should have no side effects on the server.</span></span>
- <span data-ttu-id="1ec6f-150">PUT 更新資源，以在指定的 URI。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-150">PUT updates a resource at a specified URI.</span></span> <span data-ttu-id="1ec6f-151">PUT 也可用來建立新的資源： 指定的 URI，如果伺服器允許用戶端指定新的 Uri。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-151">PUT can also be used to create a new resource at a specified URI, if the server allows clients to specify new URIs.</span></span> <span data-ttu-id="1ec6f-152">本教學課程中，此 API 不支援透過 PUT 建立。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-152">For this tutorial, the API will not support creation through PUT.</span></span>
- <span data-ttu-id="1ec6f-153">POST 建立新的資源。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-153">POST creates a new resource.</span></span> <span data-ttu-id="1ec6f-154">伺服器會指派新的物件的 URI，並傳回此 URI 做為回應訊息的一部分。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-154">The server assigns the URI for the new object and returns this URI as part of the response message.</span></span>
- <span data-ttu-id="1ec6f-155">[刪除] 刪除的資源時指定的 URI。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-155">DELETE deletes a resource at a specified URI.</span></span>

<span data-ttu-id="1ec6f-156">注意:PUT 方法會取代整個產品實體。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-156">Note: The PUT method replaces the entire product entity.</span></span> <span data-ttu-id="1ec6f-157">也就是用戶端應該傳送更新的產品的完整表示法。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-157">That is, the client is expected to send a complete representation of the updated product.</span></span> <span data-ttu-id="1ec6f-158">如果您想要支援部分更新，PATCH 方法是慣用的。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-158">If you want to support partial updates, the PATCH method is preferred.</span></span> <span data-ttu-id="1ec6f-159">本教學課程不會實作修補程式。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-159">This tutorial does not implement PATCH.</span></span>

## <a name="create-a-new-web-api-project"></a><span data-ttu-id="1ec6f-160">建立新的 Web API 專案</span><span class="sxs-lookup"><span data-stu-id="1ec6f-160">Create a New Web API Project</span></span>

<span data-ttu-id="1ec6f-161">啟動執行 Visual Studio，並選取**新的專案**從**開始**頁面。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-161">Start by running Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="1ec6f-162">或從**檔案**功能表上，選取**新增**，然後**專案**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-162">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="1ec6f-163">在 **範本**窗格中，選取**已安裝的範本**展開**Visual C#** 節點。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-163">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="1ec6f-164">底下**Visual C#**，選取**Web**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-164">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="1ec6f-165">在專案範本清單中，選取**ASP.NET MVC 4 Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-165">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="1ec6f-166">將專案命名為&quot;ProductStore&quot;然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-166">Name the project &quot;ProductStore&quot; and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

<span data-ttu-id="1ec6f-167">在 **新的 ASP.NET MVC 4 專案**對話方塊中，選取**Web API** ，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-167">In the **New ASP.NET MVC 4 Project** dialog, select **Web API** and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a><span data-ttu-id="1ec6f-168">新增模型</span><span class="sxs-lookup"><span data-stu-id="1ec6f-168">Adding a Model</span></span>

<span data-ttu-id="1ec6f-169">「模型」是代表應用程式中資料的物件。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-169">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="1ec6f-170">在 ASP.NET Web API 中，您可以使用強型別的 CLR 物件模型，和他們將會自動序列化為 XML 或 JSON 的用戶端。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-170">In ASP.NET Web API, you can use strongly typed CLR objects as models, and they will automatically be serialized to XML or JSON for the client.</span></span>

<span data-ttu-id="1ec6f-171">針對 ProductStore API，我們的資料包含產品，因此我們將建立新的類別，名為`Product`。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-171">For the ProductStore API, our data consists of products, so we'll create a new class named `Product`.</span></span>

<span data-ttu-id="1ec6f-172">如果沒有顯示 [方案總管] 中，按一下**檢視**功能表，然後選取**方案總管 中**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-172">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="1ec6f-173">在 [方案總管] 中，以滑鼠右鍵按一下**模型**資料夾。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-173">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="1ec6f-174">從操作功能表中，選取**新增**，然後選取**類別**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-174">From the context menu, select **Add**, then select **Class**.</span></span> <span data-ttu-id="1ec6f-175">將類別命名為&quot;產品&quot;。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-175">Name the class &quot;Product&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

<span data-ttu-id="1ec6f-176">新增下列屬性以`Product`類別。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-176">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a><span data-ttu-id="1ec6f-177">加入儲存機制</span><span class="sxs-lookup"><span data-stu-id="1ec6f-177">Adding a Repository</span></span>

<span data-ttu-id="1ec6f-178">我們需要儲存 products 的集合。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-178">We need to store a collection of products.</span></span> <span data-ttu-id="1ec6f-179">它是個不錯的主意，來區隔我們的服務實作的集合。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-179">It's a good idea to separate the collection from our service implementation.</span></span> <span data-ttu-id="1ec6f-180">如此一來，我們可以變更備份存放區，不需要重新撰寫的服務類別。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-180">That way, we can change the backing store without rewriting the service class.</span></span> <span data-ttu-id="1ec6f-181">這種類型的設計會呼叫*存放庫*模式。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-181">This type of design is called the *repository* pattern.</span></span> <span data-ttu-id="1ec6f-182">定義泛型介面，存放庫開始。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-182">Start by defining a generic interface for the repository.</span></span>

<span data-ttu-id="1ec6f-183">在 [方案總管] 中，以滑鼠右鍵按一下**模型**資料夾。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-183">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="1ec6f-184">選取 **新增**，然後選取**新項目**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-184">Select **Add**, then select **New Item**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

<span data-ttu-id="1ec6f-185">在 [**範本**窗格中，選取**已安裝的範本**展開 C#] 節點。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-185">In the **Templates** pane, select **Installed Templates** and expand the C# node.</span></span> <span data-ttu-id="1ec6f-186">在 C# 中，選取**程式碼**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-186">Under C#, select **Code**.</span></span> <span data-ttu-id="1ec6f-187">在程式碼範本清單中，選取**介面**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-187">In the list of code templates, select **Interface**.</span></span> <span data-ttu-id="1ec6f-188">介面命名&quot;IProductRepository&quot;。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-188">Name the interface &quot;IProductRepository&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

<span data-ttu-id="1ec6f-189">新增下列實作：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-189">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

<span data-ttu-id="1ec6f-190">現在將另一個類別新增至 [模型] 資料夾，名為&quot;ProductRepository。&quot;此類別會實作 `IProductRepository` 介面。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-190">Now add another class to the Models folder, named &quot;ProductRepository.&quot; This class will implement the `IProductRepository` interface.</span></span> <span data-ttu-id="1ec6f-191">新增下列實作：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-191">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

<span data-ttu-id="1ec6f-192">存放庫會保留在本機記憶體中的清單。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-192">The repository keeps the list in local memory.</span></span> <span data-ttu-id="1ec6f-193">這是 [確定]，教學課程中，但實際的應用程式中，您會將資料儲存於外部的資料庫或在雲端儲存體中。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-193">This is OK for a tutorial, but in a real application, you would store the data externally, either a database or in cloud storage.</span></span> <span data-ttu-id="1ec6f-194">儲存機制模式將會進行變更之後的實作變得更容易。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-194">The repository pattern will make it easier to change the implementation later.</span></span>

## <a name="adding-a-web-api-controller"></a><span data-ttu-id="1ec6f-195">新增 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="1ec6f-195">Adding a Web API Controller</span></span>

<span data-ttu-id="1ec6f-196">如果您已使用 ASP.NET MVC，然後您就已經熟悉控制站。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-196">If you have worked with ASP.NET MVC, then you are already familiar with controllers.</span></span> <span data-ttu-id="1ec6f-197">在 ASP.NET Web API 中，*控制器*是處理來自用戶端的 HTTP 要求的類別。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-197">In ASP.NET Web API, a *controller* is a class that handles HTTP requests from the client.</span></span> <span data-ttu-id="1ec6f-198">新增專案 精靈建立專案時，為您建立兩個控制站。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-198">The New Project wizard created two controllers for you when it created the project.</span></span> <span data-ttu-id="1ec6f-199">若要查看它們，請展開方案總管 中的 控制器 資料夾。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-199">To see them, expand the Controllers folder in Solution Explorer.</span></span>

- <span data-ttu-id="1ec6f-200">HomeController 是傳統的 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-200">HomeController is a traditional ASP.NET MVC controller.</span></span> <span data-ttu-id="1ec6f-201">它會負責提供 HTML 頁面的網站，並與我們的 web API 不直接相關。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-201">It is responsible for serving HTML pages for the site, and is not directly related to our web API.</span></span>
- <span data-ttu-id="1ec6f-202">ValuesController 是範例 WebAPI 控制器。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-202">ValuesController is an example WebAPI controller.</span></span>

<span data-ttu-id="1ec6f-203">請繼續並以滑鼠右鍵按一下方案總管 中的檔案，然後選取刪除 ValuesController，**刪除。**</span><span class="sxs-lookup"><span data-stu-id="1ec6f-203">Go ahead and delete ValuesController, by right-clicking the file in Solution Explorer and selecting **Delete.**</span></span> <span data-ttu-id="1ec6f-204">現在加入的新控制器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-204">Now add a new controller, as follows:</span></span>

<span data-ttu-id="1ec6f-205">在**方案總管 中**，以滑鼠右鍵按一下 [控制器] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-205">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="1ec6f-206">選取 **新增**，然後選取**控制站**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-206">Select **Add** and then select **Controller**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

<span data-ttu-id="1ec6f-207">在 **新增控制器**精靈，將控制器命名&quot;ProductsController&quot;。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-207">In the **Add Controller** wizard, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="1ec6f-208">在 **樣板**下拉式清單中，選取**空白 API 控制器**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-208">In the **Template** drop-down list, select **Empty API Controller**.</span></span> <span data-ttu-id="1ec6f-209">然後按一下 [加入] 。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-209">Then click **Add**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="1ec6f-210">您不需要將您的控制站放入名為控制器的資料夾。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-210">It is not necessary to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="1ec6f-211">資料夾名稱並不重要;它只是方便方法來組織您的原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-211">The folder name is not important; it is simply a convenient way to organize your source files.</span></span>

<span data-ttu-id="1ec6f-212">**新增控制器**精靈會建立名為 ProductsController.cs 在 Controllers 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-212">The **Add Controller** wizard will create a file named ProductsController.cs in the Controllers folder.</span></span> <span data-ttu-id="1ec6f-213">如果此檔案尚未開啟，按兩下檔案以開啟它。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-213">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="1ec6f-214">新增下列**使用**陳述式：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-214">Add the following **using** statement:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

<span data-ttu-id="1ec6f-215">新增欄位來保存**IProductRepository**執行個體。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-215">Add a field that holds an **IProductRepository** instance.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> <span data-ttu-id="1ec6f-216">呼叫`new ProductRepository()`控制器中不是最好的設計，因為它所繫結的特定實作控制器`IProductRepository`。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-216">Calling `new ProductRepository()` in the controller is not the best design, because it ties the controller to a particular implementation of `IProductRepository`.</span></span> <span data-ttu-id="1ec6f-217">好的方法，請參閱 <<c0> [ 使用 Web API 的相依性解析程式](../advanced/dependency-injection.md)。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-217">For a better approach, see [Using the Web API Dependency Resolver](../advanced/dependency-injection.md).</span></span>

## <a name="getting-a-resource"></a><span data-ttu-id="1ec6f-218">取得資源</span><span class="sxs-lookup"><span data-stu-id="1ec6f-218">Getting a Resource</span></span>

<span data-ttu-id="1ec6f-219">ProductStore API 會公開數個&quot;讀取&quot;HTTP GET 方法的動作。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-219">The ProductStore API will expose several &quot;read&quot; actions as HTTP GET methods.</span></span> <span data-ttu-id="1ec6f-220">每個動作將會對應到方法，以在`ProductsController`類別。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-220">Each action will correspond to a method in the `ProductsController` class.</span></span>

| <span data-ttu-id="1ec6f-221">動作</span><span class="sxs-lookup"><span data-stu-id="1ec6f-221">Action</span></span> | <span data-ttu-id="1ec6f-222">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1ec6f-222">HTTP method</span></span> | <span data-ttu-id="1ec6f-223">相對 URI</span><span class="sxs-lookup"><span data-stu-id="1ec6f-223">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1ec6f-224">取得所有產品的清單</span><span class="sxs-lookup"><span data-stu-id="1ec6f-224">Get a list of all products</span></span> | <span data-ttu-id="1ec6f-225">GET</span><span class="sxs-lookup"><span data-stu-id="1ec6f-225">GET</span></span> | <span data-ttu-id="1ec6f-226">/api/products</span><span class="sxs-lookup"><span data-stu-id="1ec6f-226">/api/products</span></span> |
| <span data-ttu-id="1ec6f-227">取得產品識別碼</span><span class="sxs-lookup"><span data-stu-id="1ec6f-227">Get a product by ID</span></span> | <span data-ttu-id="1ec6f-228">GET</span><span class="sxs-lookup"><span data-stu-id="1ec6f-228">GET</span></span> | <span data-ttu-id="1ec6f-229">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="1ec6f-229">/api/products/*id*</span></span> |
| <span data-ttu-id="1ec6f-230">依類別取得的產品</span><span class="sxs-lookup"><span data-stu-id="1ec6f-230">Get a product by category</span></span> | <span data-ttu-id="1ec6f-231">GET</span><span class="sxs-lookup"><span data-stu-id="1ec6f-231">GET</span></span> | <span data-ttu-id="1ec6f-232">/api/products?category=*category*</span><span class="sxs-lookup"><span data-stu-id="1ec6f-232">/api/products?category=*category*</span></span> |

<span data-ttu-id="1ec6f-233">若要取得所有產品的清單，將下列方法來新增`ProductsController`類別：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-233">To get the list of all products, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

<span data-ttu-id="1ec6f-234">方法名稱開頭&quot;取得&quot;，因此依照慣例則會對應至 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-234">The method name starts with &quot;Get&quot;, so by convention it maps to GET requests.</span></span> <span data-ttu-id="1ec6f-235">此外，因為方法沒有任何參數，則會對應至不包含在 URI *&quot;識別碼&quot;* 路徑中的區段。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-235">Also, because the method has no parameters, it maps to a URI that does not contain an *&quot;id&quot;* segment in the path.</span></span>

<span data-ttu-id="1ec6f-236">若要取得的產品識別碼，將下列方法來新增`ProductsController`類別：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-236">To get a product by ID, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

<span data-ttu-id="1ec6f-237">此方法名稱也會以開頭&quot;取得&quot;，但方法具有一個名為參數*識別碼*。此參數對應到&quot;識別碼&quot;URI 路徑區段。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-237">This method name also starts with &quot;Get&quot;, but the method has a parameter named *id*. This parameter is mapped to the &quot;id&quot; segment of the URI path.</span></span> <span data-ttu-id="1ec6f-238">ASP.NET Web API 架構會自動將識別碼轉換為正確的資料類型 (**int**) 參數。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-238">The ASP.NET Web API framework automatically converts the ID to the correct data type (**int**) for the parameter.</span></span>

<span data-ttu-id="1ec6f-239">GetProduct 方法會擲回的例外狀況型別的**HttpResponseException**如果*識別碼*無效。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-239">The GetProduct method throws an exception of type **HttpResponseException** if *id* is not valid.</span></span> <span data-ttu-id="1ec6f-240">這個例外狀況會由架構轉譯為 404 （找不到） 錯誤。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-240">This exception will be translated by the framework into a 404 (Not Found) error.</span></span>

<span data-ttu-id="1ec6f-241">最後，新增方法以依類別目錄來尋找產品：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-241">Finally, add a method to find products by category:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

<span data-ttu-id="1ec6f-242">如果在要求 URI 查詢字串，Web API 就會嘗試比對上的控制器方法的參數的查詢參數。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-242">If the request URI has a query string, Web API tries to match the query parameters to parameters on the controller method.</span></span> <span data-ttu-id="1ec6f-243">因此，在表單的 URI"api/產品？ 類別 =*分類*"會對應至這個方法。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-243">Therefore, a URI of the form "api/products?category=*category*" will map to this method.</span></span>

## <a name="creating-a-resource"></a><span data-ttu-id="1ec6f-244">建立資源</span><span class="sxs-lookup"><span data-stu-id="1ec6f-244">Creating a Resource</span></span>

<span data-ttu-id="1ec6f-245">接下來，我們將新增方法以`ProductsController`類別來建立新的產品。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-245">Next, we'll add a method to the `ProductsController` class to create a new product.</span></span> <span data-ttu-id="1ec6f-246">以下是簡單的方法實作：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-246">Here is a simple implementation of the method:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

<span data-ttu-id="1ec6f-247">請注意此方法的相關的兩件事：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-247">Note two things about this method:</span></span>

- <span data-ttu-id="1ec6f-248">方法名稱開頭為&quot;文章...&quot;.</span><span class="sxs-lookup"><span data-stu-id="1ec6f-248">The method name starts with &quot;Post...&quot;.</span></span> <span data-ttu-id="1ec6f-249">若要建立新的產品，用戶端會傳送 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-249">To create a new product, the client sends an HTTP POST request.</span></span>
- <span data-ttu-id="1ec6f-250">此方法會採用類型參數的產品。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-250">The method takes a parameter of type Product.</span></span> <span data-ttu-id="1ec6f-251">在 Web API 中，使用複雜類型的參數會從要求主體還原序列化。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-251">In Web API, parameters with complex types are deserialized from the request body.</span></span> <span data-ttu-id="1ec6f-252">因此，我們會預期用戶端傳送以 XML 或 JSON 格式的產品物件的序列化表示法。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-252">Therefore, we expect the client to send a serialized representation of a product object, in either XML or JSON format.</span></span>

<span data-ttu-id="1ec6f-253">此實作會使用，但還不算完整。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-253">This implementation will work, but it is not quite complete.</span></span> <span data-ttu-id="1ec6f-254">在理想情況下，我們想要包括下列的 HTTP 回應：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-254">Ideally, we would like the HTTP response to include the following:</span></span>

- <span data-ttu-id="1ec6f-255">**回應碼：** 根據預設，Web API 架構會設定回應狀態碼為 200 （確定）。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-255">**Response code:** By default, the Web API framework sets the response status code to 200 (OK).</span></span> <span data-ttu-id="1ec6f-256">但是，根據 HTTP/1.1 通訊協定，POST 要求所產生的資源，建立伺服器應該會回覆狀態 201 （已建立）。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-256">But according to the HTTP/1.1 protocol, when a POST request results in the creation of a resource, the server should reply with status 201 (Created).</span></span>
- <span data-ttu-id="1ec6f-257">**位置：** 當伺服器建立資源時，它應該包含回應的 Location 標頭中的新資源的 URI。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-257">**Location:** When the server creates a resource, it should include the URI of the new resource in the Location header of the response.</span></span>

<span data-ttu-id="1ec6f-258">ASP.NET Web API 可讓您更容易操作的 HTTP 回應訊息。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-258">ASP.NET Web API makes it easy to manipulate the HTTP response message.</span></span> <span data-ttu-id="1ec6f-259">以下是改進的實作：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-259">Here is the improved implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

<span data-ttu-id="1ec6f-260">請注意，方法的傳回型別現在**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-260">Notice that the method return type is now **HttpResponseMessage**.</span></span> <span data-ttu-id="1ec6f-261">藉由傳回**HttpResponseMessage**而不是一項產品，我們可以控制的 HTTP 回應訊息，包括狀態碼和 Location 標頭詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-261">By returning an **HttpResponseMessage** instead of a Product, we can control the details of the HTTP response message, including the status code and the Location header.</span></span>

<span data-ttu-id="1ec6f-262">**CreateResponse**方法會建立**HttpResponseMessage**並自動將 Product 物件的序列化的表示寫入本文提出的回應訊息。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-262">The **CreateResponse** method creates an **HttpResponseMessage** and automatically writes a serialized representation of the Product object into the body fo the response message.</span></span>

> [!NOTE]
> <span data-ttu-id="1ec6f-263">此範例不會驗證`Product`。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-263">This example does not validate the `Product`.</span></span> <span data-ttu-id="1ec6f-264">如需模型驗證資訊，請參閱[ASP.NET Web API 中的模型驗證](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-264">For information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

## <a name="updating-a-resource"></a><span data-ttu-id="1ec6f-265">更新資源</span><span class="sxs-lookup"><span data-stu-id="1ec6f-265">Updating a Resource</span></span>

<span data-ttu-id="1ec6f-266">使用 PUT 更新產品很簡單：</span><span class="sxs-lookup"><span data-stu-id="1ec6f-266">Updating a product with PUT is straightforward:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

<span data-ttu-id="1ec6f-267">方法名稱開頭為&quot;放...&quot;，使 Web API 的 PUT 要求來比對。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-267">The method name starts with &quot;Put...&quot;, so Web API matches it to PUT requests.</span></span> <span data-ttu-id="1ec6f-268">此方法會採用兩個參數、 產品識別碼和更新的產品。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-268">The method takes two parameters, the product ID and the updated product.</span></span> <span data-ttu-id="1ec6f-269">*識別碼*參數取自 URI 路徑，而*產品*參數從要求主體還原序列化。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-269">The *id* parameter is taken from the URI path, and the *product* parameter is deserialized from the request body.</span></span> <span data-ttu-id="1ec6f-270">根據預設，ASP.NET Web API 架構會從路由的簡單參數類型和要求本文中的複雜類型。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-270">By default, the ASP.NET Web API framework takes simple parameter types from the route and complex types from the request body.</span></span>

## <a name="deleting-a-resource"></a><span data-ttu-id="1ec6f-271">刪除資源</span><span class="sxs-lookup"><span data-stu-id="1ec6f-271">Deleting a Resource</span></span>

<span data-ttu-id="1ec6f-272">若要刪除資源，定義 「 刪除中...」方法。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-272">To delete a resource, define a "Delete..." method.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

<span data-ttu-id="1ec6f-273">如果 DELETE 要求成功，它會傳回狀態 200 （確定） 與實體本文描述狀態;狀態 202 （已接受） 如果仍在刪除暫止;或狀態 204 （沒有內容） 沒有實體主體。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-273">If a DELETE request succeeds, it can return status 200 (OK) with an entity-body that describes the status; status 202 (Accepted) if the deletion is still pending; or status 204 (No Content) with no entity body.</span></span> <span data-ttu-id="1ec6f-274">在此情況下，`DeleteProduct`方法具有`void`傳回型別，因此 ASP.NET Web API 會自動轉譯為此狀態碼 204 （沒有內容）。</span><span class="sxs-lookup"><span data-stu-id="1ec6f-274">In this case, the `DeleteProduct` method has a `void` return type, so ASP.NET Web API automatically translates this into status code 204 (No Content).</span></span>
