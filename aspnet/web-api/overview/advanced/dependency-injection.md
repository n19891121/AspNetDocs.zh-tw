---
uid: web-api/overview/advanced/dependency-injection
title: 相依性插入在 ASP.NET Web API 2-ASP.NET 4.x
author: MikeWasson
description: 本教學課程示範如何插入您的 ASP.NET Web API 控制器中的相依性，適用於 ASP.NET 4.x。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 0ad0b3c63741803e05274df4da3fcbe5481d32a4
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59391922"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a><span data-ttu-id="14987-103">ASP.NET Web API 2 中的相依性插入</span><span class="sxs-lookup"><span data-stu-id="14987-103">Dependency Injection in ASP.NET Web API 2</span></span>

<span data-ttu-id="14987-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="14987-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="14987-105">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="14987-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> <span data-ttu-id="14987-106">本教學課程會示範如何插入您的 ASP.NET Web API 控制器中的相依性。</span><span class="sxs-lookup"><span data-stu-id="14987-106">This tutorial shows how to inject dependencies into your ASP.NET Web API controller.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="14987-107">在本教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="14987-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="14987-108">Web API 2</span><span class="sxs-lookup"><span data-stu-id="14987-108">Web API 2</span></span>
> - [<span data-ttu-id="14987-109">Unity Application Block</span><span class="sxs-lookup"><span data-stu-id="14987-109">Unity Application Block</span></span>](https://www.nuget.org/packages/Unity/)
> - <span data-ttu-id="14987-110">Entity Framework 6 （也可使用這個第 5 版）</span><span class="sxs-lookup"><span data-stu-id="14987-110">Entity Framework 6 (version 5 also works)</span></span>


## <a name="what-is-dependency-injection"></a><span data-ttu-id="14987-111">相依性插入是什麼？</span><span class="sxs-lookup"><span data-stu-id="14987-111">What is Dependency Injection?</span></span>

<span data-ttu-id="14987-112">「相依性」是另一個物件所需的任何物件。</span><span class="sxs-lookup"><span data-stu-id="14987-112">A *dependency* is any object that another object requires.</span></span> <span data-ttu-id="14987-113">比方說，是很常見來定義[存放庫](http://martinfowler.com/eaaCatalog/repository.html)可處理的資料存取。</span><span class="sxs-lookup"><span data-stu-id="14987-113">For example, it's common to define a [repository](http://martinfowler.com/eaaCatalog/repository.html) that handles data access.</span></span> <span data-ttu-id="14987-114">讓我們舉例說明。</span><span class="sxs-lookup"><span data-stu-id="14987-114">Let's illustrate with an example.</span></span> <span data-ttu-id="14987-115">首先，我們會定義領域模型：</span><span class="sxs-lookup"><span data-stu-id="14987-115">First, we'll define a domain model:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="14987-116">以下是將項目儲存在資料庫中，使用 Entity Framework 的簡單的儲存機制類別。</span><span class="sxs-lookup"><span data-stu-id="14987-116">Here is a simple repository class that stores items in a database, using Entity Framework.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="14987-117">現在讓我們定義支援 GET 要求的 Web API 控制器`Product`實體。</span><span class="sxs-lookup"><span data-stu-id="14987-117">Now let's define a Web API controller that supports GET requests for `Product` entities.</span></span> <span data-ttu-id="14987-118">（我所出文章和其他方法，為求簡化離開）。以下是第一次嘗試：</span><span class="sxs-lookup"><span data-stu-id="14987-118">(I'm leaving out POST and other methods for simplicity.) Here is a first attempt:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="14987-119">請注意，控制器類別取決於`ProductRepository`，我們會讓建立控制器和`ProductRepository`執行個體。</span><span class="sxs-lookup"><span data-stu-id="14987-119">Notice that the controller class depends on `ProductRepository`, and we are letting the controller create the `ProductRepository` instance.</span></span> <span data-ttu-id="14987-120">不過，它是個好主意，硬式相依性，如此一來，有幾個原因。</span><span class="sxs-lookup"><span data-stu-id="14987-120">However, it's a bad idea to hard code the dependency in this way, for several reasons.</span></span>

- <span data-ttu-id="14987-121">如果您想要取代`ProductRepository`與不同的實作中，您還需要修改控制器類別。</span><span class="sxs-lookup"><span data-stu-id="14987-121">If you want to replace `ProductRepository` with a different implementation, you also need to modify the controller class.</span></span>
- <span data-ttu-id="14987-122">如果`ProductRepository`具有相依性，您必須設定這些控制器內。</span><span class="sxs-lookup"><span data-stu-id="14987-122">If the `ProductRepository` has dependencies, you must configure these inside the controller.</span></span> <span data-ttu-id="14987-123">針對大型專案中使用多個控制站，將組態程式碼變得散布在您的專案。</span><span class="sxs-lookup"><span data-stu-id="14987-123">For a large project with multiple controllers, your configuration code becomes scattered across your project.</span></span>
- <span data-ttu-id="14987-124">因為控制器是硬式編碼為查詢資料庫，它很難使用單元測試。</span><span class="sxs-lookup"><span data-stu-id="14987-124">It is hard to unit test, because the controller is hard-coded to query the database.</span></span> <span data-ttu-id="14987-125">單元測試，您應該使用模擬或虛設常式儲存機制，也就是不可能與目前的設計。</span><span class="sxs-lookup"><span data-stu-id="14987-125">For a unit test, you should use a mock or stub repository, which is not possible with the current design.</span></span>

<span data-ttu-id="14987-126">我們可以解決這些問題，由*插入*到控制器的存放庫。</span><span class="sxs-lookup"><span data-stu-id="14987-126">We can address these problems by *injecting* the repository into the controller.</span></span> <span data-ttu-id="14987-127">首先，重構`ProductRepository`介面的類別：</span><span class="sxs-lookup"><span data-stu-id="14987-127">First, refactor the `ProductRepository` class into an interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="14987-128">然後提供`IProductRepository`做為建構函式參數：</span><span class="sxs-lookup"><span data-stu-id="14987-128">Then provide the `IProductRepository` as a constructor parameter:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="14987-129">這個範例會使用[建構函式插入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)。</span><span class="sxs-lookup"><span data-stu-id="14987-129">This example uses [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="14987-130">您也可以使用*setter 插入*，您將設定透過 setter 方法或屬性的相依性。</span><span class="sxs-lookup"><span data-stu-id="14987-130">You can also use *setter injection*, where you set the dependency through a setter method or property.</span></span>

<span data-ttu-id="14987-131">但是，現在還有一個問題，因為您的應用程式不會直接建立控制器。</span><span class="sxs-lookup"><span data-stu-id="14987-131">But now there is a problem, because your application doesn't create the controller directly.</span></span> <span data-ttu-id="14987-132">當它路由傳送要求，且 Web API 並不知道的任何項目時，web API 建立控制器`IProductRepository`。</span><span class="sxs-lookup"><span data-stu-id="14987-132">Web API creates the controller when it routes the request, and Web API doesn't know anything about `IProductRepository`.</span></span> <span data-ttu-id="14987-133">這是 Web API 的相依性解析程式之處。</span><span class="sxs-lookup"><span data-stu-id="14987-133">This is where the Web API dependency resolver comes in.</span></span>

## <a name="the-web-api-dependency-resolver"></a><span data-ttu-id="14987-134">Web API 的相依性解析程式</span><span class="sxs-lookup"><span data-stu-id="14987-134">The Web API Dependency Resolver</span></span>

<span data-ttu-id="14987-135">Web API 定義**IDependencyResolver**介面解析相依性。</span><span class="sxs-lookup"><span data-stu-id="14987-135">Web API defines the **IDependencyResolver** interface for resolving dependencies.</span></span> <span data-ttu-id="14987-136">以下是介面的定義：</span><span class="sxs-lookup"><span data-stu-id="14987-136">Here is the definition of the interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="14987-137">**IDependencyScope**介面有兩種方法：</span><span class="sxs-lookup"><span data-stu-id="14987-137">The **IDependencyScope** interface has two methods:</span></span>

- <span data-ttu-id="14987-138">**GetService**建立類型的執行個體。</span><span class="sxs-lookup"><span data-stu-id="14987-138">**GetService** creates one instance of a type.</span></span>
- <span data-ttu-id="14987-139">**GetServices**建立指定類型之物件的集合。</span><span class="sxs-lookup"><span data-stu-id="14987-139">**GetServices** creates a collection of objects of a specified type.</span></span>

<span data-ttu-id="14987-140">**IDependencyResolver**方法繼承**IDependencyScope** ，並將**BeginScope**方法。</span><span class="sxs-lookup"><span data-stu-id="14987-140">The **IDependencyResolver** method inherits **IDependencyScope** and adds the **BeginScope** method.</span></span> <span data-ttu-id="14987-141">本教學課程稍後，我將討論範圍。</span><span class="sxs-lookup"><span data-stu-id="14987-141">I'll talk about scopes later in this tutorial.</span></span>

<span data-ttu-id="14987-142">當 Web API 建立控制器執行個體時，它會先呼叫**IDependencyResolver.GetService**，傳遞控制站類型。</span><span class="sxs-lookup"><span data-stu-id="14987-142">When Web API creates a controller instance, it first calls **IDependencyResolver.GetService**, passing in the controller type.</span></span> <span data-ttu-id="14987-143">您可以使用此擴充性攔截程序來建立控制器，解析任何相依性。</span><span class="sxs-lookup"><span data-stu-id="14987-143">You can use this extensibility hook to create the controller, resolving any dependencies.</span></span> <span data-ttu-id="14987-144">如果**GetService**傳回 null，Web API 控制器類別上的無參數建構函式的外觀。</span><span class="sxs-lookup"><span data-stu-id="14987-144">If **GetService** returns null, Web API looks for a parameterless constructor on the controller class.</span></span>

## <a name="dependency-resolution-with-the-unity-container"></a><span data-ttu-id="14987-145">使用 Unity 容器相依性解析</span><span class="sxs-lookup"><span data-stu-id="14987-145">Dependency Resolution with the Unity Container</span></span>

<span data-ttu-id="14987-146">雖然您可以撰寫完整**IDependencyResolver**介面從頭實作真的被設計來做為 Web API 與現有的 IoC 容器之間的橋樑。</span><span class="sxs-lookup"><span data-stu-id="14987-146">Although you could write a complete **IDependencyResolver** implementation from scratch, the interface is really designed to act as bridge between Web API and existing IoC containers.</span></span>

<span data-ttu-id="14987-147">IoC 容器是負責管理相依性的軟體元件。</span><span class="sxs-lookup"><span data-stu-id="14987-147">An IoC container is a software component that is responsible for managing dependencies.</span></span> <span data-ttu-id="14987-148">您向容器註冊類型，然後再使用 建立物件的 容器。</span><span class="sxs-lookup"><span data-stu-id="14987-148">You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="14987-149">容器會自動找出相依性關聯性。</span><span class="sxs-lookup"><span data-stu-id="14987-149">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="14987-150">許多 IoC 容器也可讓您控制物件存留期和範圍等項目。</span><span class="sxs-lookup"><span data-stu-id="14987-150">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="14987-151">「 IoC 」 代表 「 的控制項反轉 」，這是一種架構會呼叫應用程式程式碼的一般模式。</span><span class="sxs-lookup"><span data-stu-id="14987-151">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="14987-152">IoC 容器建構您的物件，其中 「 反轉 」 一般控制流程。</span><span class="sxs-lookup"><span data-stu-id="14987-152">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>


<span data-ttu-id="14987-153">本教學課程中，我們將使用[Unity](https://msdn.microsoft.com/library/ff647202.aspx)從 Microsoft Patterns&amp;作法。</span><span class="sxs-lookup"><span data-stu-id="14987-153">For this tutorial, we'll use [Unity](https://msdn.microsoft.com/library/ff647202.aspx) from Microsoft Patterns &amp; Practices.</span></span> <span data-ttu-id="14987-154">(其他熱門的程式庫包含[Castle Windsor](http://www.castleproject.org/)， [Spring.Net](http://www.springframework.net/)， [Autofac](https://code.google.com/p/autofac/)， [Ninject](http://www.ninject.org/)，和[StructureMap](http://structuremap.github.io/documentation/).)您可以使用 NuGet 套件管理員安裝 Unity。</span><span class="sxs-lookup"><span data-stu-id="14987-154">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/), and [StructureMap](http://structuremap.github.io/documentation/).) You can use NuGet Package Manager to install Unity.</span></span> <span data-ttu-id="14987-155">從**工具**功能表，在 Visual Studio 中，選取**NuGet 套件管理員**，然後選取**Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="14987-155">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="14987-156">在 [套件管理員主控台] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="14987-156">In the Package Manager Console window, type the following command:</span></span>

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

<span data-ttu-id="14987-157">以下是實作**IDependencyResolver**包裝 Unity 容器。</span><span class="sxs-lookup"><span data-stu-id="14987-157">Here is an implementation of **IDependencyResolver** that wraps a Unity container.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="14987-158">如果**GetService**的型別時，無法解析方法，它應該會傳回**null**。</span><span class="sxs-lookup"><span data-stu-id="14987-158">If the **GetService** method cannot resolve a type, it should return **null**.</span></span> <span data-ttu-id="14987-159">如果**GetServices**方法無法解析型別，它應該會傳回空集合物件。</span><span class="sxs-lookup"><span data-stu-id="14987-159">If the **GetServices** method cannot resolve a type, it should return an empty collection object.</span></span> <span data-ttu-id="14987-160">不會擲回未知類型的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="14987-160">Don't throw exceptions for unknown types.</span></span>


## <a name="configuring-the-dependency-resolver"></a><span data-ttu-id="14987-161">設定相依性解析程式</span><span class="sxs-lookup"><span data-stu-id="14987-161">Configuring the Dependency Resolver</span></span>

<span data-ttu-id="14987-162">設定相依性解析程式**DependencyResolver**屬性的全域**HttpConfiguration**物件。</span><span class="sxs-lookup"><span data-stu-id="14987-162">Set the dependency resolver on the **DependencyResolver** property of the global **HttpConfiguration** object.</span></span>

<span data-ttu-id="14987-163">下列程式碼的暫存器`IProductRepository`使用 Unity 的介面，然後建立`UnityResolver`。</span><span class="sxs-lookup"><span data-stu-id="14987-163">The following code registers the `IProductRepository` interface with Unity and then creates a `UnityResolver`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a><span data-ttu-id="14987-164">相依性範圍和控制站的存留期</span><span class="sxs-lookup"><span data-stu-id="14987-164">Dependency Scope and Controller Lifetime</span></span>

<span data-ttu-id="14987-165">控制站會建立每個要求。</span><span class="sxs-lookup"><span data-stu-id="14987-165">Controllers are created per request.</span></span> <span data-ttu-id="14987-166">若要管理物件存留期， **IDependencyResolver**使用的概念*範圍*。</span><span class="sxs-lookup"><span data-stu-id="14987-166">To manage object lifetimes, **IDependencyResolver** uses the concept of a *scope*.</span></span>

<span data-ttu-id="14987-167">相依性解析程式附加至**HttpConfiguration**物件具有全域範圍。</span><span class="sxs-lookup"><span data-stu-id="14987-167">The dependency resolver attached to the **HttpConfiguration** object has global scope.</span></span> <span data-ttu-id="14987-168">當 Web API 建立的控制器時，它會呼叫**BeginScope**。</span><span class="sxs-lookup"><span data-stu-id="14987-168">When Web API creates a controller, it calls **BeginScope**.</span></span> <span data-ttu-id="14987-169">這個方法會傳回**IDependencyScope**表示子範圍。</span><span class="sxs-lookup"><span data-stu-id="14987-169">This method returns an **IDependencyScope** that represents a child scope.</span></span>

<span data-ttu-id="14987-170">然後呼叫 web API **GetService**子領域建立控制站上。</span><span class="sxs-lookup"><span data-stu-id="14987-170">Web API then calls **GetService** on the child scope to create the controller.</span></span> <span data-ttu-id="14987-171">要求完成時，會呼叫 Web API**處置**子範圍。</span><span class="sxs-lookup"><span data-stu-id="14987-171">When request is complete, Web API calls **Dispose** on the child scope.</span></span> <span data-ttu-id="14987-172">使用**處置**處置控制器的相依性的方法。</span><span class="sxs-lookup"><span data-stu-id="14987-172">Use the **Dispose** method to dispose of the controller's dependencies.</span></span>

<span data-ttu-id="14987-173">如何實作**BeginScope** IoC 容器而定。</span><span class="sxs-lookup"><span data-stu-id="14987-173">How you implement **BeginScope** depends on the IoC container.</span></span> <span data-ttu-id="14987-174">For Unity，範圍會對應至子容器中：</span><span class="sxs-lookup"><span data-stu-id="14987-174">For Unity, scope corresponds to a child container:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

<span data-ttu-id="14987-175">大部分的 IoC 容器具有類似的對等項目。</span><span class="sxs-lookup"><span data-stu-id="14987-175">Most IoC containers have similar equivalents.</span></span>
