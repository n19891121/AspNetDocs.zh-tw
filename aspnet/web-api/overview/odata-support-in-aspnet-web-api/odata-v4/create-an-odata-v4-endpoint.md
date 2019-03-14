---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: 建立 OData v4 端點使用 ASP.NET Web API 2.2 |Microsoft Docs
author: MikeWasson
description: 開放式資料通訊協定 (OData) 是網站的資料存取通訊協定。 OData 提供統一的方式來查詢及管理透過 CRUD 作業的資料集...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: c6a4aa4eb563fd77d5afd9248175d5f5b7984d19
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042595"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a><span data-ttu-id="ee0b4-104">建立使用 ASP.NET Web API OData v4 端點</span><span class="sxs-lookup"><span data-stu-id="ee0b4-104">Create an OData v4 Endpoint Using ASP.NET Web API</span></span> 

> <span data-ttu-id="ee0b4-105">開放式資料通訊協定 (OData) 是網站的資料存取通訊協定。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-105">The Open Data Protocol (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="ee0b4-106">OData 提供統一的方式來查詢及操作資料集，透過 CRUD 作業 （建立、 讀取、 更新和刪除）。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-106">OData provides a uniform way to query and manipulate data sets through CRUD operations (create, read, update, and delete).</span></span>
>
> <span data-ttu-id="ee0b4-107">ASP.NET Web API 支援 v3 和 v4 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-107">ASP.NET Web API supports both v3 and v4 of the protocol.</span></span> <span data-ttu-id="ee0b4-108">您甚至可以執行並排顯示的 v4 端點與 v3 端點。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-108">You can even have a v4 endpoint that runs side-by-side with a v3 endpoint.</span></span>
>
> <span data-ttu-id="ee0b4-109">本教學課程會示範如何建立支援 CRUD 作業的 OData v4 端點。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-109">This tutorial shows how to create an OData v4 endpoint that supports CRUD operations.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ee0b4-110">在本教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="ee0b4-110">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="ee0b4-111">Web API 5.2</span><span class="sxs-lookup"><span data-stu-id="ee0b4-111">Web API 5.2</span></span>
> - <span data-ttu-id="ee0b4-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="ee0b4-112">OData v4</span></span>
> - <span data-ttu-id="ee0b4-113">Visual Studio 2017 (下載 Visual Studio 2017[此處](https://visualstudio.microsoft.com/downloads/))</span><span class="sxs-lookup"><span data-stu-id="ee0b4-113">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/))</span></span>
> - <span data-ttu-id="ee0b4-114">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="ee0b4-114">Entity Framework 6</span></span>
> - <span data-ttu-id="ee0b4-115">.NET 4.7.2</span><span class="sxs-lookup"><span data-stu-id="ee0b4-115">.NET 4.7.2</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="ee0b4-116">教學課程的版本</span><span class="sxs-lookup"><span data-stu-id="ee0b4-116">Tutorial versions</span></span>
>
> <span data-ttu-id="ee0b4-117">OData 第 3 版，請參閱 <<c0> [ 建立 OData v3 端點](../odata-v3/creating-an-odata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-117">For the OData Version 3, see [Creating an OData v3 Endpoint](../odata-v3/creating-an-odata-endpoint.md).</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="ee0b4-118">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="ee0b4-118">Create the Visual Studio Project</span></span>

<span data-ttu-id="ee0b4-119">在 Visual Studio 中，從**檔案**功能表上，選取**新增** &gt; **專案**。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-119">In Visual Studio, from the **File** menu, select **New** &gt; **Project**.</span></span>

<span data-ttu-id="ee0b4-120">依序展開**已安裝** &gt; **視覺C#**  &gt; **Web**，然後選取**ASP.NET Web 應用程式 (.NET Framework)** 範本。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-120">Expand **Installed** &gt; **Visual C#** &gt; **Web**, and select the **ASP.NET Web Application (.NET Framework)** template.</span></span> <span data-ttu-id="ee0b4-121">將專案命名為&quot;ProductService&quot;。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-121">Name the project &quot;ProductService&quot;.</span></span>

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

<span data-ttu-id="ee0b4-122">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-122">Select **OK**.</span></span>



[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

<span data-ttu-id="ee0b4-123">選取 **空**範本。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-123">Select the **Empty** template.</span></span> <span data-ttu-id="ee0b4-124">底下**新增的資料夾和核心參考：**，選取**Web API**。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-124">Under **Add folders and core references for:**, select **Web API**.</span></span> <span data-ttu-id="ee0b4-125">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-125">Select **OK**.</span></span>

## <a name="install-the-odata-packages"></a><span data-ttu-id="ee0b4-126">安裝 OData 的套件</span><span class="sxs-lookup"><span data-stu-id="ee0b4-126">Install the OData packages</span></span>

<span data-ttu-id="ee0b4-127">從 [工具] 功能表中，選取 [NuGet 套件管理員] &gt; [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-127">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="ee0b4-128">在 [套件管理員主控台] 視窗中，輸入：</span><span class="sxs-lookup"><span data-stu-id="ee0b4-128">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

<span data-ttu-id="ee0b4-129">此命令會安裝最新的 OData NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-129">This command installs the latest OData NuGet packages.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="ee0b4-130">新增模型類別</span><span class="sxs-lookup"><span data-stu-id="ee0b4-130">Add a model class</span></span>

<span data-ttu-id="ee0b4-131">A*模型*是物件，表示您的應用程式中的資料實體。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-131">A *model* is an object that represents a data entity in your application.</span></span>

<span data-ttu-id="ee0b4-132">在 [方案總管] 中，以滑鼠右鍵按一下 [模型] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-132">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="ee0b4-133">從操作功能表中，選取**新增** &gt; **類別**。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-133">From the context menu, select **Add** &gt; **Class**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="ee0b4-134">依照慣例，模型類別會放在 Models 資料夾中，但您不需要遵循此慣例，在您自己的專案中。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-134">By convention, model classes are placed in the Models folder, but you don't have to follow this convention in your own projects.</span></span>


<span data-ttu-id="ee0b4-135">將類別命名為 `Product` 。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-135">Name the class `Product`.</span></span> <span data-ttu-id="ee0b4-136">在 Product.cs 檔案中，請以下列取代未定案程式碼：</span><span class="sxs-lookup"><span data-stu-id="ee0b4-136">In the Product.cs file, replace the boilerplate code with the following:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

<span data-ttu-id="ee0b4-137">`Id`屬性是實體索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-137">The `Id` property is the entity key.</span></span> <span data-ttu-id="ee0b4-138">用戶端可以查詢的實體索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-138">Clients can query entities by key.</span></span> <span data-ttu-id="ee0b4-139">例如，若要取得識別碼 5 的產品，URI 是`/Products(5)`。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-139">For example, to get the product with ID of 5, the URI is `/Products(5)`.</span></span> <span data-ttu-id="ee0b4-140">`Id`屬性也會在後端資料庫中的主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-140">The `Id` property will also be the primary key in the back-end database.</span></span>

## <a name="enable-entity-framework"></a><span data-ttu-id="ee0b4-141">讓 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="ee0b4-141">Enable Entity Framework</span></span>

<span data-ttu-id="ee0b4-142">本教學課程中，我們將使用 Entity Framework (EF) Code First 建立的後端資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-142">For this tutorial, we'll use Entity Framework (EF) Code First to create the back-end database.</span></span>

> [!NOTE]
> <span data-ttu-id="ee0b4-143">Web API OData 中不需要 EF。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-143">Web API OData does not require EF.</span></span> <span data-ttu-id="ee0b4-144">使用任何可以將資料庫實體轉譯為模型的資料存取層。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-144">Use any data-access layer that can translate database entities into models.</span></span>


<span data-ttu-id="ee0b4-145">首先，安裝 ef 的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-145">First, install the NuGet package for EF.</span></span> <span data-ttu-id="ee0b4-146">從 [工具] 功能表中，選取 [NuGet 套件管理員] &gt; [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-146">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="ee0b4-147">在 [套件管理員主控台] 視窗中，輸入：</span><span class="sxs-lookup"><span data-stu-id="ee0b4-147">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

<span data-ttu-id="ee0b4-148">開啟 Web.config 檔案中，並將下列區段內新增**組態**項目，之後**configSections**項目。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-148">Open the Web.config file, and add the following section inside the **configuration** element, after the **configSections** element.</span></span>

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

<span data-ttu-id="ee0b4-149">這項設定將加入 LocalDB 資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-149">This setting adds a connection string for a LocalDB database.</span></span> <span data-ttu-id="ee0b4-150">當您在本機執行應用程式，則會使用此資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-150">This database will be used when you run the app locally.</span></span>

<span data-ttu-id="ee0b4-151">接下來，新增名為類別`ProductsContext`到 Models 資料夾：</span><span class="sxs-lookup"><span data-stu-id="ee0b4-151">Next, add a class named `ProductsContext` to the Models folder:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

<span data-ttu-id="ee0b4-152">在建構函式，`"name=ProductsContext"`提供的連接字串名稱。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-152">In the constructor, `"name=ProductsContext"` gives the name of the connection string.</span></span>

## <a name="configure-the-odata-endpoint"></a><span data-ttu-id="ee0b4-153">設定 OData 端點</span><span class="sxs-lookup"><span data-stu-id="ee0b4-153">Configure the OData endpoint</span></span>

<span data-ttu-id="ee0b4-154">開啟檔案的應用程式\_Start/WebApiConfig.cs。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-154">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="ee0b4-155">新增下列**使用**陳述式：</span><span class="sxs-lookup"><span data-stu-id="ee0b4-155">Add the following **using** statements:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

<span data-ttu-id="ee0b4-156">然後新增下列程式碼**註冊**方法：</span><span class="sxs-lookup"><span data-stu-id="ee0b4-156">Then add the following code to the **Register** method:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

<span data-ttu-id="ee0b4-157">此程式碼會執行兩件事：</span><span class="sxs-lookup"><span data-stu-id="ee0b4-157">This code does two things:</span></span>

- <span data-ttu-id="ee0b4-158">建立實體資料模型 (EDM)。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-158">Creates an Entity Data Model (EDM).</span></span>
- <span data-ttu-id="ee0b4-159">新增一個路由。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-159">Adds a route.</span></span>

<span data-ttu-id="ee0b4-160">EDM 是資料的抽象模型。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-160">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="ee0b4-161">EDM 用來建立服務的中繼資料文件。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-161">The EDM is used to create the service metadata document.</span></span> <span data-ttu-id="ee0b4-162">**ODataConventionModelBuilder**類別會使用預設命名慣例來建立 EDM。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-162">The **ODataConventionModelBuilder** class creates an EDM by using default naming conventions.</span></span> <span data-ttu-id="ee0b4-163">這個方法需要最少的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-163">This approach requires the least code.</span></span> <span data-ttu-id="ee0b4-164">如果您想要更充分掌控 EDM 中，您可以使用**ODataModelBuilder**藉由新增屬性、 金鑰和導覽屬性明確地建立 EDM 的類別。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-164">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="ee0b4-165">A*路由*告知如何將 HTTP 要求傳送至端點的 Web API。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-165">A *route* tells Web API how to route HTTP requests to the endpoint.</span></span> <span data-ttu-id="ee0b4-166">若要建立 OData v4 路由，請呼叫**MapODataServiceRoute**擴充方法。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-166">To create an OData v4 route, call the **MapODataServiceRoute** extension method.</span></span>

<span data-ttu-id="ee0b4-167">如果您的應用程式有多個 OData 端點，請在每個建立個別的路由。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-167">If your application has multiple OData endpoints, create a separate route for each.</span></span> <span data-ttu-id="ee0b4-168">提供每個路由，唯一的路由名稱和前置詞。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-168">Give each route a unique route name and prefix.</span></span>

## <a name="add-the-odata-controller"></a><span data-ttu-id="ee0b4-169">加入 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="ee0b4-169">Add the OData controller</span></span>

<span data-ttu-id="ee0b4-170">A*控制器*是處理 HTTP 要求的類別。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-170">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="ee0b4-171">您建立個別的控制器，在您的 OData 服務中設定每個實體。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-171">You create a separate controller for each entity set in your OData service.</span></span> <span data-ttu-id="ee0b4-172">在本教學課程中，您會建立一個控制站，`Product`實體。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-172">In this tutorial, you will create one controller, for the `Product` entity.</span></span>

<span data-ttu-id="ee0b4-173">在 [方案總管] 中，以滑鼠右鍵按一下 [控制器] 資料夾，然後選取**新增** &gt; **類別**。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-173">In Solution Explorer, right-click the Controllers folder and select **Add** &gt; **Class**.</span></span> <span data-ttu-id="ee0b4-174">將類別命名為 `ProductsController` 。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-174">Name the class `ProductsController`.</span></span>

> [!NOTE]
> <span data-ttu-id="ee0b4-175">本教學課程中的 OData v3 使用新版**新增控制器**scaffolding。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-175">The version of this tutorial for OData v3 uses the **Add Controller** scaffolding.</span></span> <span data-ttu-id="ee0b4-176">目前沒有任何樣板 OData v4。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-176">Currently, there is no scaffolding for OData v4.</span></span>


<span data-ttu-id="ee0b4-177">以下列取代 ProductsController.cs 的未定案程式碼。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-177">Replace the boilerplate code in ProductsController.cs with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

<span data-ttu-id="ee0b4-178">控制器會使用`ProductsContext`類別來存取使用 EF 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-178">The controller uses the `ProductsContext` class to access the database using EF.</span></span> <span data-ttu-id="ee0b4-179">請注意，控制器會覆寫**處置**方法來處置**ProductsContext**。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-179">Notice that the controller overrides the **Dispose** method to dispose of the **ProductsContext**.</span></span>

<span data-ttu-id="ee0b4-180">這是控制器的起點。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-180">This is the starting point for the controller.</span></span> <span data-ttu-id="ee0b4-181">接下來，我們將新增的所有 CRUD 作業的方法。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-181">Next, we'll add methods for all of the CRUD operations.</span></span>

## <a name="query-the-entity-set"></a><span data-ttu-id="ee0b4-182">查詢的實體集</span><span class="sxs-lookup"><span data-stu-id="ee0b4-182">Query the entity set</span></span>

<span data-ttu-id="ee0b4-183">新增下列方法來`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-183">Add the following methods to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

<span data-ttu-id="ee0b4-184">無參數的版本`Get`方法會傳回整個產品集合。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-184">The parameterless version of the `Get` method returns the entire Products collection.</span></span> <span data-ttu-id="ee0b4-185">`Get`方法*金鑰*參數依其索引鍵查閱的產品 (在此情況下，`Id`屬性)。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-185">The `Get` method with a *key* parameter looks up a product by its key (in this case, the `Id` property).</span></span>

<span data-ttu-id="ee0b4-186">**[EnableQuery]** 屬性可讓用戶端使用查詢選項，例如 $filter、 $sort 和 $page 修改查詢。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-186">The **[EnableQuery]** attribute enables clients to modify the query, by using query options such as $filter, $sort, and $page.</span></span> <span data-ttu-id="ee0b4-187">如需詳細資訊，請參閱 <<c0> [ 支援的 OData 查詢選項](../supporting-odata-query-options.md)。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-187">For more information, see [Supporting OData Query Options](../supporting-odata-query-options.md).</span></span>

## <a name="add-an-entity-to-the-entity-set"></a><span data-ttu-id="ee0b4-188">將實體新增至實體集</span><span class="sxs-lookup"><span data-stu-id="ee0b4-188">Add an entity to the entity set</span></span>

<span data-ttu-id="ee0b4-189">若要讓用戶端將新的產品加入至資料庫，將新增下列方法加入`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-189">To enable clients to add a new product to the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a><span data-ttu-id="ee0b4-190">更新實體</span><span class="sxs-lookup"><span data-stu-id="ee0b4-190">Update an entity</span></span>

<span data-ttu-id="ee0b4-191">OData 支援兩個不同的語意，來更新實體、 PATCH 和 PUT。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-191">OData supports two different semantics for updating an entity, PATCH and PUT.</span></span>

- <span data-ttu-id="ee0b4-192">修補程式會執行部分更新。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-192">PATCH performs a partial update.</span></span> <span data-ttu-id="ee0b4-193">用戶端指定要更新屬性。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-193">The client specifies just the properties to update.</span></span>
- <span data-ttu-id="ee0b4-194">PUT 將會取代整個實體。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-194">PUT replaces the entire entity.</span></span>

<span data-ttu-id="ee0b4-195">PUT 的缺點是用戶端必須在實體中，包括未變更的值傳送的所有屬性的值。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-195">The disadvantage of PUT is that the client must send values for all of the properties in the entity, including values that are not changing.</span></span> <span data-ttu-id="ee0b4-196">[OData 規格](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719)修補程式是慣用的狀態。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-196">The [OData spec](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) states that PATCH is preferred.</span></span>

<span data-ttu-id="ee0b4-197">在任何情況下，以下是 PATCH 和 PUT 方法的程式碼：</span><span class="sxs-lookup"><span data-stu-id="ee0b4-197">In any case, here is the code for both PATCH and PUT methods:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

<span data-ttu-id="ee0b4-198">修補程式，在控制器會使用**差異&lt;T&gt;** 來追蹤變更的類型。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-198">In the case of PATCH, the controller uses the **Delta&lt;T&gt;** type to track the changes.</span></span>

## <a name="delete-an-entity"></a><span data-ttu-id="ee0b4-199">刪除實體</span><span class="sxs-lookup"><span data-stu-id="ee0b4-199">Delete an entity</span></span>

<span data-ttu-id="ee0b4-200">若要啟用從資料庫刪除一項產品的用戶端，新增下列方法加入`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="ee0b4-200">To enable clients to delete a product from the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
