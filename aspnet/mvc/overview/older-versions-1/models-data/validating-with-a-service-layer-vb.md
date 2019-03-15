---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
title: 驗證與服務層 (VB) |Microsoft Docs
author: StephenWalther
description: 了解如何移動您的驗證邏輯出您對控制器動作並進入個別的服務層。 在本教學課程中，Stephen walther 將說明如何您...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 344bb38e-4965-4c47-bda1-f6d29ae5b83a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: ecce8e4f0a901ce8c185d2b085f4d706bd57fa1f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029135"
---
<a name="validating-with-a-service-layer-vb"></a><span data-ttu-id="eed56-104">驗證與服務層 (VB)</span><span class="sxs-lookup"><span data-stu-id="eed56-104">Validating with a Service Layer (VB)</span></span>
====================
<span data-ttu-id="eed56-105">藉由[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="eed56-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="eed56-106">了解如何移動您的驗證邏輯出您對控制器動作並進入個別的服務層。</span><span class="sxs-lookup"><span data-stu-id="eed56-106">Learn how to move your validation logic out of your controller actions and into a separate service layer.</span></span> <span data-ttu-id="eed56-107">在本教學課程中，Stephen Walther 會說明如何藉由隔離您的服務層，從您的控制器層級維護 sharp 關注點分離。</span><span class="sxs-lookup"><span data-stu-id="eed56-107">In this tutorial, Stephen Walther explains how you can maintain a sharp separation of concerns by isolating your service layer from your controller layer.</span></span>


<span data-ttu-id="eed56-108">本教學課程的目標是說明 ASP.NET MVC 應用程式中執行驗證的一種方法。</span><span class="sxs-lookup"><span data-stu-id="eed56-108">The goal of this tutorial is to describe one method of performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="eed56-109">在本教學課程中，您將了解如何移動您的驗證邏輯出您的控制器並進入個別的服務層。</span><span class="sxs-lookup"><span data-stu-id="eed56-109">In this tutorial, you learn how to move your validation logic out of your controllers and into a separate service layer.</span></span>

## <a name="separating-concerns"></a><span data-ttu-id="eed56-110">區隔的考量</span><span class="sxs-lookup"><span data-stu-id="eed56-110">Separating Concerns</span></span>

<span data-ttu-id="eed56-111">當您建置 ASP.NET MVC 應用程式時，不應該將您的資料庫邏輯放在您對控制器動作。</span><span class="sxs-lookup"><span data-stu-id="eed56-111">When you build an ASP.NET MVC application, you should not place your database logic inside your controller actions.</span></span> <span data-ttu-id="eed56-112">混用您的資料庫和控制器邏輯，可讓您的應用程式更難維護一段時間。</span><span class="sxs-lookup"><span data-stu-id="eed56-112">Mixing your database and controller logic makes your application more difficult to maintain over time.</span></span> <span data-ttu-id="eed56-113">建議您將所有資料庫邏輯放在個別的存放庫圖層。</span><span class="sxs-lookup"><span data-stu-id="eed56-113">The recommendation is that you place all of your database logic in a separate repository layer.</span></span>

<span data-ttu-id="eed56-114">例如，列表 1 包含名為 ProductRepository 簡單存放庫。</span><span class="sxs-lookup"><span data-stu-id="eed56-114">For example, Listing 1 contains a simple repository named the ProductRepository.</span></span> <span data-ttu-id="eed56-115">產品存放庫包含所有應用程式的資料存取程式碼。</span><span class="sxs-lookup"><span data-stu-id="eed56-115">The product repository contains all of the data access code for the application.</span></span> <span data-ttu-id="eed56-116">清單也包含產品存放庫會實作 IProductRepository 介面。</span><span class="sxs-lookup"><span data-stu-id="eed56-116">The listing also includes the IProductRepository interface that the product repository implements.</span></span>

<span data-ttu-id="eed56-117">**Listing 1 - Models\ProductRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="eed56-117">**Listing 1 - Models\ProductRepository.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample1.vb)]

<span data-ttu-id="eed56-118">列表 2 中的控制站會使用其 index （）] 和 [create （） 動作中的儲存機制層。</span><span class="sxs-lookup"><span data-stu-id="eed56-118">The controller in Listing 2 uses the repository layer in both its Index() and Create() actions.</span></span> <span data-ttu-id="eed56-119">請注意，此控制器不包含任何資料庫的邏輯。</span><span class="sxs-lookup"><span data-stu-id="eed56-119">Notice that this controller does not contain any database logic.</span></span> <span data-ttu-id="eed56-120">建立儲存機制層，可讓您維持清楚分離關注點。</span><span class="sxs-lookup"><span data-stu-id="eed56-120">Creating a repository layer enables you to maintain a clean separation of concerns.</span></span> <span data-ttu-id="eed56-121">控制器負責應用程式的流程控制邏輯，並將存放庫會負責資料存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="eed56-121">Controllers are responsible for application flow control logic and the repository is responsible for data access logic.</span></span>

<span data-ttu-id="eed56-122">**Listing 2 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="eed56-122">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample2.vb)]

## <a name="creating-a-service-layer"></a><span data-ttu-id="eed56-123">建立服務層</span><span class="sxs-lookup"><span data-stu-id="eed56-123">Creating a Service Layer</span></span>

<span data-ttu-id="eed56-124">因此，應用程式流程控制邏輯位於控制器，而所屬的存放庫中的資料存取邏輯。</span><span class="sxs-lookup"><span data-stu-id="eed56-124">So, application flow control logic belongs in a controller and data access logic belongs in a repository.</span></span> <span data-ttu-id="eed56-125">在此情況下，您在其中放置您的驗證邏輯？</span><span class="sxs-lookup"><span data-stu-id="eed56-125">In that case, where do you put your validation logic?</span></span> <span data-ttu-id="eed56-126">其中一個選項是將您的驗證邏輯，在*服務層*。</span><span class="sxs-lookup"><span data-stu-id="eed56-126">One option is to place your validation logic in a *service layer*.</span></span>

<span data-ttu-id="eed56-127">服務層是在 ASP.NET MVC 應用程式，以促成控制站和儲存機制層之間的通訊額外層級。</span><span class="sxs-lookup"><span data-stu-id="eed56-127">A service layer is an additional layer in an ASP.NET MVC application that mediates communication between a controller and repository layer.</span></span> <span data-ttu-id="eed56-128">服務層包含商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="eed56-128">The service layer contains business logic.</span></span> <span data-ttu-id="eed56-129">特別是，它會包含驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="eed56-129">In particular, it contains validation logic.</span></span>

<span data-ttu-id="eed56-130">例如，產品的服務層，在 列表 3 中有 CreateProduct() 方法。</span><span class="sxs-lookup"><span data-stu-id="eed56-130">For example, the product service layer in Listing 3 has a CreateProduct() method.</span></span> <span data-ttu-id="eed56-131">CreateProduct() 方法會呼叫 ValidateProduct() 来驗證的方法將新產品，然後將產品傳遞至產品存放庫。</span><span class="sxs-lookup"><span data-stu-id="eed56-131">The CreateProduct() method calls the ValidateProduct() method to validate a new product before passing the product to the product repository.</span></span>

<span data-ttu-id="eed56-132">**Listing 3 - Models\ProductService.vb**</span><span class="sxs-lookup"><span data-stu-id="eed56-132">**Listing 3 - Models\ProductService.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample3.vb)]

<span data-ttu-id="eed56-133">若要使用的服務層，而不是儲存機制層的列表 4 中已更新 Product 控制器。</span><span class="sxs-lookup"><span data-stu-id="eed56-133">The Product controller has been updated in Listing 4 to use the service layer instead of the repository layer.</span></span> <span data-ttu-id="eed56-134">在控制器層與服務層。</span><span class="sxs-lookup"><span data-stu-id="eed56-134">The controller layer talks to the service layer.</span></span> <span data-ttu-id="eed56-135">服務層與儲存機制層。</span><span class="sxs-lookup"><span data-stu-id="eed56-135">The service layer talks to the repository layer.</span></span> <span data-ttu-id="eed56-136">每一層都有不同的責任。</span><span class="sxs-lookup"><span data-stu-id="eed56-136">Each layer has a separate responsibility.</span></span>

<span data-ttu-id="eed56-137">**Listing 4 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="eed56-137">**Listing 4 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample4.vb)]

<span data-ttu-id="eed56-138">請注意，產品中會建立服務產品控制器建構函式。</span><span class="sxs-lookup"><span data-stu-id="eed56-138">Notice that the product service is created in the product controller constructor.</span></span> <span data-ttu-id="eed56-139">建立產品服務時，位於模型狀態字典會傳遞至服務。</span><span class="sxs-lookup"><span data-stu-id="eed56-139">When the product service is created, the model state dictionary is passed to the service.</span></span> <span data-ttu-id="eed56-140">產品服務會用來通過驗證的設定，錯誤訊息傳回至控制器的模型狀態。</span><span class="sxs-lookup"><span data-stu-id="eed56-140">The product service uses model state to pass validation error messages back to the controller.</span></span>

## <a name="decoupling-the-service-layer"></a><span data-ttu-id="eed56-141">減少服務層</span><span class="sxs-lookup"><span data-stu-id="eed56-141">Decoupling the Service Layer</span></span>

<span data-ttu-id="eed56-142">我們無法隔離控制站和服務層，在一個方面。</span><span class="sxs-lookup"><span data-stu-id="eed56-142">We have failed to isolate the controller and service layers in one respect.</span></span> <span data-ttu-id="eed56-143">在控制站和服務層透過模型狀態進行通訊。</span><span class="sxs-lookup"><span data-stu-id="eed56-143">The controller and service layers communicate through model state.</span></span> <span data-ttu-id="eed56-144">換句話說，服務層會將相依性對 ASP.NET MVC 架構的特定功能。</span><span class="sxs-lookup"><span data-stu-id="eed56-144">In other words, the service layer has a dependency on a particular feature of the ASP.NET MVC framework.</span></span>

<span data-ttu-id="eed56-145">我們想要隔離服務層，從我們盡量的控制器層級。</span><span class="sxs-lookup"><span data-stu-id="eed56-145">We want to isolate the service layer from our controller layer as much as possible.</span></span> <span data-ttu-id="eed56-146">理論上，我們應該能夠使用任何類型的應用程式和不只在 ASP.NET MVC 應用程式的服務層。</span><span class="sxs-lookup"><span data-stu-id="eed56-146">In theory, we should be able to use the service layer with any type of application and not only an ASP.NET MVC application.</span></span> <span data-ttu-id="eed56-147">比方說，在未來，我們可能會想要建置 WPF 應用程式的前端。</span><span class="sxs-lookup"><span data-stu-id="eed56-147">For example, in the future, we might want to build a WPF front-end for our application.</span></span> <span data-ttu-id="eed56-148">我們應該找出方法來移除對 ASP.NET MVC 的相依性模型狀態，從我們的服務層。</span><span class="sxs-lookup"><span data-stu-id="eed56-148">We should find a way to remove the dependency on ASP.NET MVC model state from our service layer.</span></span>

<span data-ttu-id="eed56-149">表 5 中，使其不再使用的模型狀態已更新的服務層。</span><span class="sxs-lookup"><span data-stu-id="eed56-149">In Listing 5, the service layer has been updated so that it no longer uses model state.</span></span> <span data-ttu-id="eed56-150">相反地，它會使用任何可實作 IValidationDictionary 介面的類別。</span><span class="sxs-lookup"><span data-stu-id="eed56-150">Instead, it uses any class that implements the IValidationDictionary interface.</span></span>

<span data-ttu-id="eed56-151">**Listing 5 - Models\ProductService.vb (decoupled)**</span><span class="sxs-lookup"><span data-stu-id="eed56-151">**Listing 5 - Models\ProductService.vb (decoupled)**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample5.vb)]

<span data-ttu-id="eed56-152">IValidationDictionary 介面被定義在列表 6。</span><span class="sxs-lookup"><span data-stu-id="eed56-152">The IValidationDictionary interface is defined in Listing 6.</span></span> <span data-ttu-id="eed56-153">這個簡單的介面具有單一方法和單一屬性。</span><span class="sxs-lookup"><span data-stu-id="eed56-153">This simple interface has a single method and a single property.</span></span>

<span data-ttu-id="eed56-154">**列表 6-Models\IValidationDictionary.cs**</span><span class="sxs-lookup"><span data-stu-id="eed56-154">**Listing 6 - Models\IValidationDictionary.cs**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample6.vb)]

<span data-ttu-id="eed56-155">列表 7，名為 ModelStateWrapper 類別中的類別會實作 IValidationDictionary 介面。</span><span class="sxs-lookup"><span data-stu-id="eed56-155">The class in Listing 7, named the ModelStateWrapper class, implements the IValidationDictionary interface.</span></span> <span data-ttu-id="eed56-156">您可以將模型狀態字典傳遞至建構函式具現化 ModelStateWrapper 類別。</span><span class="sxs-lookup"><span data-stu-id="eed56-156">You can instantiate the ModelStateWrapper class by passing a model state dictionary to the constructor.</span></span>

<span data-ttu-id="eed56-157">**Listing 7 - Models\ModelStateWrapper.vb**</span><span class="sxs-lookup"><span data-stu-id="eed56-157">**Listing 7 - Models\ModelStateWrapper.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample7.vb)]

<span data-ttu-id="eed56-158">最後，在 列表 8 更新的控制器會使用 ModelStateWrapper 其建構函式中建立的服務層時。</span><span class="sxs-lookup"><span data-stu-id="eed56-158">Finally, the updated controller in Listing 8 uses the ModelStateWrapper when creating the service layer in its constructor.</span></span>

<span data-ttu-id="eed56-159">**Listing 8 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="eed56-159">**Listing 8 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample8.vb)]

<span data-ttu-id="eed56-160">使用 IValidationDictionary 介面和 ModelStateWrapper 類別可讓我們完全區隔我們的服務層，從我們的控制器層級。</span><span class="sxs-lookup"><span data-stu-id="eed56-160">Using the IValidationDictionary interface and the ModelStateWrapper class enables us to completely isolate our service layer from our controller layer.</span></span> <span data-ttu-id="eed56-161">服務層不再相依於模型狀態。</span><span class="sxs-lookup"><span data-stu-id="eed56-161">The service layer is no longer dependent on model state.</span></span> <span data-ttu-id="eed56-162">您可以傳遞任何實作服務層的 IValidationDictionary 介面的類別。</span><span class="sxs-lookup"><span data-stu-id="eed56-162">You can pass any class that implements the IValidationDictionary interface to the service layer.</span></span> <span data-ttu-id="eed56-163">比方說，WPF 應用程式可能會實作簡單的集合類別的 IValidationDictionary 介面。</span><span class="sxs-lookup"><span data-stu-id="eed56-163">For example, a WPF application might implement the IValidationDictionary interface with a simple collection class.</span></span>

## <a name="summary"></a><span data-ttu-id="eed56-164">總結</span><span class="sxs-lookup"><span data-stu-id="eed56-164">Summary</span></span>

<span data-ttu-id="eed56-165">本教學課程的目標是要討論的 ASP.NET MVC 應用程式中執行驗證的其中一種方法。</span><span class="sxs-lookup"><span data-stu-id="eed56-165">The goal of this tutorial was to discuss one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="eed56-166">在本教學課程中，您已了解如何移動所有的驗證邏輯出您的控制器並進入個別的服務層。</span><span class="sxs-lookup"><span data-stu-id="eed56-166">In this tutorial, you learned how to move all of your validation logic out of your controllers and into a separate service layer.</span></span> <span data-ttu-id="eed56-167">您也學到如何建立 ModelStateWrapper 類別，以隔離您的服務層，從您的控制器層級。</span><span class="sxs-lookup"><span data-stu-id="eed56-167">You also learned how to isolate your service layer from your controller layer by creating a ModelStateWrapper class.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="eed56-168">[上一頁](validating-with-the-idataerrorinfo-interface-vb.md)
> [下一頁](validation-with-the-data-annotation-validators-vb.md)</span><span class="sxs-lookup"><span data-stu-id="eed56-168">[Previous](validating-with-the-idataerrorinfo-interface-vb.md)
[Next](validation-with-the-data-annotation-validators-vb.md)</span></span>