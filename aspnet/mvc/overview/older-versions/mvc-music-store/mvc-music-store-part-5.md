---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 第 5 部分：編輯表單和範本化 |Microsoft Docs
author: jongalloway
description: 本教學課程系列會詳細說明所有建置 ASP.NET MVC Music 市集範例應用程式所採取的步驟。 第 5 部分涵蓋編輯表單和範本。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: e02e15a8955fa42692fac486dadfa426540295f7
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59387467"
---
# <a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="40ba2-104">第 5 部分：編輯表單和範本</span><span class="sxs-lookup"><span data-stu-id="40ba2-104">Part 5: Edit Forms and Templating</span></span>

<span data-ttu-id="40ba2-105">藉由[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="40ba2-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="40ba2-106">MVC Music 市集是介紹，並逐步說明如何使用 ASP.NET MVC 和 Visual Studio 進行 web 開發的教學課程應用程式。</span><span class="sxs-lookup"><span data-stu-id="40ba2-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="40ba2-107">MVC Music 市集是銷售線上音樂 album 和實作基本的網站管理、 使用者登入時，和 「 購物車 」 功能的輕量級的範例存放區實作。</span><span class="sxs-lookup"><span data-stu-id="40ba2-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="40ba2-108">本教學課程系列會詳細說明所有建置 ASP.NET MVC Music 市集範例應用程式所採取的步驟。</span><span class="sxs-lookup"><span data-stu-id="40ba2-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="40ba2-109">第 5 部分涵蓋編輯表單和範本。</span><span class="sxs-lookup"><span data-stu-id="40ba2-109">Part 5 covers Edit Forms and Templating.</span></span>


<span data-ttu-id="40ba2-110">在過去的章節中，我們已從資料庫載入資料，並顯示它。</span><span class="sxs-lookup"><span data-stu-id="40ba2-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="40ba2-111">在本章中，我們也會啟用編輯的資料。</span><span class="sxs-lookup"><span data-stu-id="40ba2-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="40ba2-112">建立 StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="40ba2-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="40ba2-113">我們一開始先建立新的控制器，稱為**StoreManagerController**。</span><span class="sxs-lookup"><span data-stu-id="40ba2-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="40ba2-114">此控制器中，我們將可利用 ASP.NET MVC 3 Tools Update 中提供的 Scaffolding 功能。</span><span class="sxs-lookup"><span data-stu-id="40ba2-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="40ba2-115">設定 [新增控制器] 對話方塊的選項，如下所示。</span><span class="sxs-lookup"><span data-stu-id="40ba2-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="40ba2-116">當您按一下 [新增] 按鈕時，您會看到的 ASP.NET MVC 3 scaffolding 機制，會為您的工作：</span><span class="sxs-lookup"><span data-stu-id="40ba2-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="40ba2-117">它會建立新的 StoreManagerController，其區域變數的 Entity Framework</span><span class="sxs-lookup"><span data-stu-id="40ba2-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="40ba2-118">它將 StoreManager 資料夾加入至專案的 [Views] 資料夾</span><span class="sxs-lookup"><span data-stu-id="40ba2-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="40ba2-119">它會新增 Create.cshtml 」、 「 Delete.cshtml 」、 「 Details.cshtml 」、 「 Edit.cshtml 和 「 Index.cshtml 檢視中，強型別為專輯類別</span><span class="sxs-lookup"><span data-stu-id="40ba2-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="40ba2-120">新的 StoreManager 控制器類別包含 CRUD （建立、 讀取、 更新、 刪除） 模型類別知道如何與專輯的控制器動作，並使用我們的 Entity Framework 內容進行資料庫存取。</span><span class="sxs-lookup"><span data-stu-id="40ba2-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="40ba2-121">修改包含 Scaffold 的檢視</span><span class="sxs-lookup"><span data-stu-id="40ba2-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="40ba2-122">請務必記住，雖然為我們產生這個程式碼，它是標準 ASP.NET MVC 的程式碼，就像我們最近撰寫本教學課程。</span><span class="sxs-lookup"><span data-stu-id="40ba2-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="40ba2-123">其目的是要儲存於撰寫未定案控制器程式碼和手動的方式，建立強型別的檢視的省下花的時間，但這不是產生的程式碼可能看過開頭不得變更的相關註解中的可怕的類型程式碼。</span><span class="sxs-lookup"><span data-stu-id="40ba2-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="40ba2-124">這是您的程式碼，您應該要加以變更。</span><span class="sxs-lookup"><span data-stu-id="40ba2-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="40ba2-125">因此，讓我們開始快速編輯 以 StoreManager 索引 檢視 (/ Views/StoreManager/Index.cshtml)。</span><span class="sxs-lookup"><span data-stu-id="40ba2-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="40ba2-126">此檢視會顯示資料表會列出在我們的存放區中的 Album，以編輯 / 詳細資料 / 刪除的連結，並包含專輯的公用屬性。</span><span class="sxs-lookup"><span data-stu-id="40ba2-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="40ba2-127">我們將先移除 AlbumArtUrl 欄位中，因為它不在此顯示中非常有用。</span><span class="sxs-lookup"><span data-stu-id="40ba2-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="40ba2-128">中&lt;資料表&gt;區段的 檢視程式碼中，移除&lt;th&gt;並&lt;td&gt;周圍 AlbumArtUrl 參考，如下列醒目提示的程式行所示的項目：</span><span class="sxs-lookup"><span data-stu-id="40ba2-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="40ba2-129">修改過的檢視程式碼會如下所示：</span><span class="sxs-lookup"><span data-stu-id="40ba2-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="40ba2-130">率先一睹存放區管理員</span><span class="sxs-lookup"><span data-stu-id="40ba2-130">A first look at the Store Manager</span></span>

<span data-ttu-id="40ba2-131">現在執行應用程式，並瀏覽至 StoreManager /。</span><span class="sxs-lookup"><span data-stu-id="40ba2-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="40ba2-132">這會顯示我們剛才修改，顯示一份專輯連結編輯的詳細資訊，以及刪除存放區中儲存管理員索引。</span><span class="sxs-lookup"><span data-stu-id="40ba2-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="40ba2-133">按一下 [編輯] 連結顯示欄位是編輯的表單的專輯、 音樂類型與演出者包括下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="40ba2-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="40ba2-134">按一下底部的 「 回至清單 」 連結，然後按一下 Album 的詳細資料 連結。</span><span class="sxs-lookup"><span data-stu-id="40ba2-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="40ba2-135">這會顯示個別的專輯的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="40ba2-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="40ba2-136">同樣地，按一下 [回到清單] 連結，，然後按一下 [刪除] 連結。</span><span class="sxs-lookup"><span data-stu-id="40ba2-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="40ba2-137">這會顯示確認對話方塊中，顯示專輯詳細資料，並詢問我們是否確定要刪除它。</span><span class="sxs-lookup"><span data-stu-id="40ba2-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="40ba2-138">按一下底部的 [刪除] 按鈕將會刪除 album，並返回 [索引] 頁面，其中顯示刪除的專輯。</span><span class="sxs-lookup"><span data-stu-id="40ba2-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="40ba2-139">我們無法完成存放區管理員 中，但我們具有運作中的控制器和檢視的 CRUD 作業，從啟動的程式碼。</span><span class="sxs-lookup"><span data-stu-id="40ba2-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="40ba2-140">查看市集管理員控制器程式碼</span><span class="sxs-lookup"><span data-stu-id="40ba2-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="40ba2-141">存放區管理員控制器包含的程式碼。</span><span class="sxs-lookup"><span data-stu-id="40ba2-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="40ba2-142">讓我們進行此程序從上到下。</span><span class="sxs-lookup"><span data-stu-id="40ba2-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="40ba2-143">控制器包含一些標準的命名空間，MVC 控制器，以及我們的模型命名空間的參考。</span><span class="sxs-lookup"><span data-stu-id="40ba2-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="40ba2-144">控制器有 MusicStoreEntities，供用於資料存取的每個控制器動作的私用執行個體。</span><span class="sxs-lookup"><span data-stu-id="40ba2-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="40ba2-145">存放管理員 Index 和 Details 動作</span><span class="sxs-lookup"><span data-stu-id="40ba2-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="40ba2-146">[索引] 檢視會擷取一份專輯，包括每一個 album 的參考內容類型與演出者資訊，如我們先前所見的存放區瀏覽的方法上工作時。</span><span class="sxs-lookup"><span data-stu-id="40ba2-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="40ba2-147">[索引] 檢視會遵循連結物件的參考，讓它讓控制器正在有效率且查詢的原始要求中的這項資訊可以顯示每個相簿的內容類型名稱和演出者名稱。</span><span class="sxs-lookup"><span data-stu-id="40ba2-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="40ba2-148">StoreManager 控制器的詳細資料控制器動作的運作方式完全相同的存放區控制站的詳細資料動作，我們撰寫了先前-它會查詢該專輯使用 Find() 方法的識別碼，然後將它傳回至檢視。</span><span class="sxs-lookup"><span data-stu-id="40ba2-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="40ba2-149">建立動作方法</span><span class="sxs-lookup"><span data-stu-id="40ba2-149">The Create Action Methods</span></span>

<span data-ttu-id="40ba2-150">建立動作方法會稍有不同之處我們到目前為止，已了解，因為它們會處理表單的輸入。</span><span class="sxs-lookup"><span data-stu-id="40ba2-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="40ba2-151">當使用者第一次瀏覽時 /StoreManager/建立/它們將會顯示空白的表單。</span><span class="sxs-lookup"><span data-stu-id="40ba2-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="40ba2-152">這個 HTML 網頁會包含&lt;表單&gt;元素，其中包含下拉式清單中，文字方塊中輸入項目可以在其中輸入專輯的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="40ba2-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="40ba2-153">使用者會專輯表單值中的填滿之後，可按下 [儲存] 按鈕送出這些變更回到我們的應用程式，以儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="40ba2-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="40ba2-154">當使用者按下 [儲存] 按鈕&lt;表單&gt;就會執行 HTTP POST 回到 /StoreManager/建立/URL，並提交&lt;表單&gt;值做為 HTTP post 要求的一部分。</span><span class="sxs-lookup"><span data-stu-id="40ba2-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="40ba2-155">ASP.NET MVC 可讓我們輕鬆地將分割邏輯的這兩種 URL 引動過程案例讓我們實作我們 StoreManagerController 類別 – 處理初始的 HTTP GET 瀏覽至 /StoreManager/Create 內兩個個別 [建立] 動作方法/ URL，以及其他處理提交的變更 HTTP POST。</span><span class="sxs-lookup"><span data-stu-id="40ba2-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="40ba2-156">將資訊傳遞至檢視，使用 ViewBag</span><span class="sxs-lookup"><span data-stu-id="40ba2-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="40ba2-157">我們已在稍早在本教學課程中使用 ViewBag，但還沒有特別談一下。</span><span class="sxs-lookup"><span data-stu-id="40ba2-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="40ba2-158">ViewBag 可讓我們將資訊傳遞至檢視，而不需使用強型別的模型物件。</span><span class="sxs-lookup"><span data-stu-id="40ba2-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="40ba2-159">在此情況下，不需要將這兩個內容類型和演出者名稱的清單傳遞至表單，以填入下拉式清單中，我們的編輯 HTTP-GET 控制器動作，而若要這樣做，最簡單的方法是傳回它們，當做 ViewBag 項目。</span><span class="sxs-lookup"><span data-stu-id="40ba2-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="40ba2-160">ViewBag 是動態物件，這表示，您可以輸入 ViewBag.Foo 或 ViewBag.YourNameHere 而不需要撰寫程式碼以定義這些屬性。</span><span class="sxs-lookup"><span data-stu-id="40ba2-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="40ba2-161">在此情況下，控制器程式碼會使用 ViewBag.GenreId 和 ViewBag.ArtistId 以便 GenreId 和 ArtistId，會專輯屬性會設定它們，將會提交表單的下拉式清單值。</span><span class="sxs-lookup"><span data-stu-id="40ba2-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="40ba2-162">這些下拉式清單中的值會傳回使用 SelectList 物件，只針對該目的內建表單。</span><span class="sxs-lookup"><span data-stu-id="40ba2-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="40ba2-163">這是使用如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="40ba2-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="40ba2-164">您可以看到從動作方法的程式碼，以便建立這個物件正在使用三個參數：</span><span class="sxs-lookup"><span data-stu-id="40ba2-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="40ba2-165">將會顯示下拉式清單中的項目清單。</span><span class="sxs-lookup"><span data-stu-id="40ba2-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="40ba2-166">請注意，這不只是字串-我們要將傳遞的內容類型清單。</span><span class="sxs-lookup"><span data-stu-id="40ba2-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="40ba2-167">下一個參數傳遞至 SelectList 是選取的值。</span><span class="sxs-lookup"><span data-stu-id="40ba2-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="40ba2-168">此 SelectList 如何知道如何預先選取清單中的項目。</span><span class="sxs-lookup"><span data-stu-id="40ba2-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="40ba2-169">這會是更容易了解當我們查看的編輯表單，這是十分類似。</span><span class="sxs-lookup"><span data-stu-id="40ba2-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="40ba2-170">最後一個參數是要顯示的屬性。</span><span class="sxs-lookup"><span data-stu-id="40ba2-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="40ba2-171">在此情況下，這表示 Genre.Name 屬性會顯示給使用者。</span><span class="sxs-lookup"><span data-stu-id="40ba2-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="40ba2-172">這一點之後，接著，建立 HTTP GET 的動作是很簡單-ViewBag，加入兩個 SelectLists，並沒有模型物件傳遞至表單 （因為它尚未尚未建立）。</span><span class="sxs-lookup"><span data-stu-id="40ba2-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="40ba2-173">卸除的清單檢視中顯示建立的 HTML 協助程式</span><span class="sxs-lookup"><span data-stu-id="40ba2-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="40ba2-174">因為我們一直在討論如何將下拉式清單值傳遞至檢視，讓我們快速瀏覽檢視來查看這些值的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="40ba2-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="40ba2-175">在 檢視程式碼 (/ Views/StoreManager/Create.cshtml)，您會看到下列呼叫來顯示內容類型下拉式清單下。</span><span class="sxs-lookup"><span data-stu-id="40ba2-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="40ba2-176">這稱為 HTML 協助程式-執行常見的檢視工作的公用程式方法。</span><span class="sxs-lookup"><span data-stu-id="40ba2-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="40ba2-177">HTML 協助程式會很有用的精簡、 可讀性，讓我們檢視程式碼。</span><span class="sxs-lookup"><span data-stu-id="40ba2-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="40ba2-178">Html.DropDownList 協助程式由 ASP.NET MVC 提供，但如我們稍後所見，就可以建立自己的協助程式，我們將在我們的應用程式中重複使用的檢視程式碼。</span><span class="sxs-lookup"><span data-stu-id="40ba2-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="40ba2-179">Html.DropDownList 呼叫只需要告知兩件事-其中取得清單中，若要顯示，以及哪些值 （如果有的話） 應會預先選取。</span><span class="sxs-lookup"><span data-stu-id="40ba2-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="40ba2-180">第一個參數，也就是 GenreId 會告訴 DropDownList 以尋找名稱為 GenreId 模型或 ViewBag 中的值。</span><span class="sxs-lookup"><span data-stu-id="40ba2-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="40ba2-181">第二個參數用來指出要顯示的值為一開始選取的下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="40ba2-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="40ba2-182">這種形式是建立表單，因為沒有要預先選取的值，並傳遞 String.Empty。</span><span class="sxs-lookup"><span data-stu-id="40ba2-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="40ba2-183">處理張貼的表單值</span><span class="sxs-lookup"><span data-stu-id="40ba2-183">Handling the Posted Form values</span></span>

<span data-ttu-id="40ba2-184">如同我們討論之前，有兩個與每個表單相關聯的動作方法。</span><span class="sxs-lookup"><span data-stu-id="40ba2-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="40ba2-185">第一個會處理 HTTP GET 要求，並顯示表單。</span><span class="sxs-lookup"><span data-stu-id="40ba2-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="40ba2-186">第二個會處理 HTTP POST 要求，其中包含送出的表單值。</span><span class="sxs-lookup"><span data-stu-id="40ba2-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="40ba2-187">請注意，控制器動作有 [HttpPost] 屬性，它會告訴 ASP.NET MVC 只應該回應 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="40ba2-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="40ba2-188">此動作會有四個責任：</span><span class="sxs-lookup"><span data-stu-id="40ba2-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="40ba2-189">讀取表單值</span><span class="sxs-lookup"><span data-stu-id="40ba2-189">Read the form values</span></span>
- 2. <span data-ttu-id="40ba2-190">檢查表單值是否傳遞的任何驗證規則</span><span class="sxs-lookup"><span data-stu-id="40ba2-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="40ba2-191">如果表單提交有效，將資料儲存，並顯示更新的清單</span><span class="sxs-lookup"><span data-stu-id="40ba2-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="40ba2-192">如果表單提交不是有效的重新顯示有驗證錯誤表單</span><span class="sxs-lookup"><span data-stu-id="40ba2-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="40ba2-193">讀取與模型繫結的表單值</span><span class="sxs-lookup"><span data-stu-id="40ba2-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="40ba2-194">控制器動作正在處理的標題、 價格和 AlbumArtUrl 包含 GenreId 和 ArtistId （從下拉式清單） 的值和文字方塊值的表單提交。</span><span class="sxs-lookup"><span data-stu-id="40ba2-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="40ba2-195">雖然您可以直接存取表單值、 更好的方法是使用內建於 ASP.NET MVC 模型繫結功能。</span><span class="sxs-lookup"><span data-stu-id="40ba2-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="40ba2-196">當控制器動作將做為參數的模型型別時，ASP.NET MVC 會嘗試填入表單的輸入 （以及路由和查詢字串值） 在該類型的物件。</span><span class="sxs-lookup"><span data-stu-id="40ba2-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="40ba2-197">其做法是要尋找的名稱符合屬性的模型物件，例如設定新的專輯物件 GenreId 值時，它會尋找名稱 GenreId 的輸入。</span><span class="sxs-lookup"><span data-stu-id="40ba2-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="40ba2-198">當您建立檢視，在 ASP.NET MVC 中使用標準的方法時，將一律使用屬性名稱做為輸入的欄位名稱，因此這的欄位名稱會只比對會呈現表單。</span><span class="sxs-lookup"><span data-stu-id="40ba2-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="40ba2-199">驗證模型</span><span class="sxs-lookup"><span data-stu-id="40ba2-199">Validating the Model</span></span>

<span data-ttu-id="40ba2-200">使用簡單的呼叫來 ModelState.IsValid 驗證模型。</span><span class="sxs-lookup"><span data-stu-id="40ba2-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="40ba2-201">我們還沒有任何驗證規則加入我們的專輯類別-但我們會這麼做有點-現在這項檢查不會有許多執行。</span><span class="sxs-lookup"><span data-stu-id="40ba2-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="40ba2-202">重要的是這 ModelStat.IsValid 項檢查會適應我們放在我們的模型，以便未來的變更，驗證規則不需要任何更新至控制器動作程式碼的驗證規則。</span><span class="sxs-lookup"><span data-stu-id="40ba2-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="40ba2-203">正在儲存提交的值</span><span class="sxs-lookup"><span data-stu-id="40ba2-203">Saving the submitted values</span></span>

<span data-ttu-id="40ba2-204">如果表單提交會通過驗證，就可以將值儲存到資料庫。</span><span class="sxs-lookup"><span data-stu-id="40ba2-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="40ba2-205">使用 Entity Framework，只需要將模型新增至相簿集合，並呼叫 SaveChanges。</span><span class="sxs-lookup"><span data-stu-id="40ba2-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="40ba2-206">Entity Framework 會產生適當的 SQL 命令，以保存的值。</span><span class="sxs-lookup"><span data-stu-id="40ba2-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="40ba2-207">儲存資料之後, 我們重新導向回專輯的清單，我們會看到我們的更新。</span><span class="sxs-lookup"><span data-stu-id="40ba2-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="40ba2-208">這是藉由傳回 RedirectToAction 控制器動作，我們想要顯示的名稱。</span><span class="sxs-lookup"><span data-stu-id="40ba2-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="40ba2-209">在此情況下，這是 Index 方法。</span><span class="sxs-lookup"><span data-stu-id="40ba2-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="40ba2-210">顯示無效的表單提交作業，發生驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="40ba2-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="40ba2-211">在無效的格式輸入的情況下的下拉式清單中的值加入 ViewBag （如 HTTP GET 案例中），並繫結的模型值如顯示時，會傳回給檢視。</span><span class="sxs-lookup"><span data-stu-id="40ba2-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="40ba2-212">驗證錯誤會自動顯示使用@Html.ValidationMessageForHTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="40ba2-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="40ba2-213">測試建立表單</span><span class="sxs-lookup"><span data-stu-id="40ba2-213">Testing the Create Form</span></span>

<span data-ttu-id="40ba2-214">若要測試此時執行的應用程式和瀏覽至 /StoreManager/建立 /-這會顯示您 StoreController 建立 HTTP GET 方法所傳回的空白表單。</span><span class="sxs-lookup"><span data-stu-id="40ba2-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="40ba2-215">填入一些值，然後按一下 [建立] 按鈕來送出表單。</span><span class="sxs-lookup"><span data-stu-id="40ba2-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="40ba2-216">處理編輯</span><span class="sxs-lookup"><span data-stu-id="40ba2-216">Handling Edits</span></span>

<span data-ttu-id="40ba2-217">編輯動作配對 （HTTP-GET 和 HTTP-POST） 是非常類似於我們剛才看到的建立動作方法。</span><span class="sxs-lookup"><span data-stu-id="40ba2-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="40ba2-218">因為編輯案例牽涉到使用現有的相簿，編輯 HTTP GET 方法會載入專輯根據 「 識別碼 」 的參數，傳遞透過路由。</span><span class="sxs-lookup"><span data-stu-id="40ba2-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="40ba2-219">因為我們已經先前討論過，在 詳細資料控制器動作來擷取由 AlbumId album 的這段程式碼都是相同的。</span><span class="sxs-lookup"><span data-stu-id="40ba2-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="40ba2-220">使用 建立 / HTTP GET 方法，透過 ViewBag 傳回下拉式值清單。</span><span class="sxs-lookup"><span data-stu-id="40ba2-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="40ba2-221">這可讓我們回到 Album 為我們的模型物件的檢視 （也就強型別專輯類別） 並透過 ViewBag 傳遞其他資料 （例如內容類型清單）。</span><span class="sxs-lookup"><span data-stu-id="40ba2-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="40ba2-222">編輯 HTTP POST 動作是非常類似於建立的 HTTP POST 動作。</span><span class="sxs-lookup"><span data-stu-id="40ba2-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="40ba2-223">唯一的差別，而非資料庫中新增新的相簿。專輯集合中，我們覺得專輯的目前執行個體使用 db。Entry(album) 並將其狀態設定為已修改。</span><span class="sxs-lookup"><span data-stu-id="40ba2-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="40ba2-224">這會告訴 Entity Framework，我們會修改現有的相簿，而不是建立一個新。</span><span class="sxs-lookup"><span data-stu-id="40ba2-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="40ba2-225">我們可以執行應用程式，並瀏覽至/StoreManger/，然後按一下 album 的編輯連結此進行測試。</span><span class="sxs-lookup"><span data-stu-id="40ba2-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="40ba2-226">這會顯示編輯的 HTTP GET 方法所顯示的編輯表單。</span><span class="sxs-lookup"><span data-stu-id="40ba2-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="40ba2-227">填入一些值，然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="40ba2-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="40ba2-228">這會張貼表單時，儲存值，並傳回我們 [專輯] 清單中，顯示已更新的值。</span><span class="sxs-lookup"><span data-stu-id="40ba2-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="40ba2-229">處理刪除</span><span class="sxs-lookup"><span data-stu-id="40ba2-229">Handling Deletion</span></span>

<span data-ttu-id="40ba2-230">刪除會遵循與編輯和建立，使用一個控制器動作，以顯示 [確認] 表單中和另一個控制器動作，以處理表單提交相同的模式。</span><span class="sxs-lookup"><span data-stu-id="40ba2-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="40ba2-231">HTTP GET 刪除控制器動作正是我們先前的存放區管理員詳細資料控制器動作相同。</span><span class="sxs-lookup"><span data-stu-id="40ba2-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="40ba2-232">專輯類型，使用 刪除檢視的內容樣板，我們就會顯示一個表單，強型別。</span><span class="sxs-lookup"><span data-stu-id="40ba2-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="40ba2-233">刪除範本會顯示在模型中的所有欄位，但我們可以稍微簡化該清單。</span><span class="sxs-lookup"><span data-stu-id="40ba2-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="40ba2-234">變更檢視中的程式碼 /Views/StoreManager/Delete.cshtml 所示。</span><span class="sxs-lookup"><span data-stu-id="40ba2-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="40ba2-235">這會顯示簡化的刪除確認。</span><span class="sxs-lookup"><span data-stu-id="40ba2-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="40ba2-236">按一下 [刪除] 按鈕會使表單回傳至伺服器，它會執行 DeleteConfirmed 動作。</span><span class="sxs-lookup"><span data-stu-id="40ba2-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="40ba2-237">我們 HTTP-POST 刪除控制器動作會採取下列動作：</span><span class="sxs-lookup"><span data-stu-id="40ba2-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="40ba2-238">依識別碼專輯的負載</span><span class="sxs-lookup"><span data-stu-id="40ba2-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="40ba2-239">會專輯刪除它並儲存變更</span><span class="sxs-lookup"><span data-stu-id="40ba2-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="40ba2-240">重新導向至索引中，顯示已從清單中移除相簿</span><span class="sxs-lookup"><span data-stu-id="40ba2-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="40ba2-241">若要測試這種情況，執行應用程式，並瀏覽至 /StoreManager。</span><span class="sxs-lookup"><span data-stu-id="40ba2-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="40ba2-242">從清單中選取 專輯，然後按一下 刪除 連結。</span><span class="sxs-lookup"><span data-stu-id="40ba2-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="40ba2-243">這會顯示我們刪除確認 畫面。</span><span class="sxs-lookup"><span data-stu-id="40ba2-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="40ba2-244">按一下 刪除 按鈕會專輯中移除，並傳回我們至存放區管理員索引 頁面，其中顯示已刪除 album。</span><span class="sxs-lookup"><span data-stu-id="40ba2-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="40ba2-245">使用自訂的 HTML Helper 來截斷文字</span><span class="sxs-lookup"><span data-stu-id="40ba2-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="40ba2-246">我們有一項潛在的問題與我們的存放區管理員索引頁面。</span><span class="sxs-lookup"><span data-stu-id="40ba2-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="40ba2-247">我們專輯標題和演出者名稱的屬性都可以是時間夠長，則可能會擲回，關閉我們的表格格式。</span><span class="sxs-lookup"><span data-stu-id="40ba2-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="40ba2-248">我們將建立自訂的 HTML Helper，讓我們輕鬆地截斷這些及其他屬性，在我們的檢視。</span><span class="sxs-lookup"><span data-stu-id="40ba2-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="40ba2-249">Razor 的@helper語法使得它很容易就能建立您自己的 helper 函式，使用您的檢視中。</span><span class="sxs-lookup"><span data-stu-id="40ba2-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="40ba2-250">開啟 /Views/StoreManager/Index.cshtml 檢視，然後加入下列程式碼直接之後@model列。</span><span class="sxs-lookup"><span data-stu-id="40ba2-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="40ba2-251">這個 helper 方法會採用字串和允許的最大長度。</span><span class="sxs-lookup"><span data-stu-id="40ba2-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="40ba2-252">如果提供的文字會小於指定的長度，協助專家將其輸出做為是。</span><span class="sxs-lookup"><span data-stu-id="40ba2-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="40ba2-253">如果很長，它會截斷文字，並呈現"..."的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="40ba2-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="40ba2-254">現在我們可以使用我們截斷的協助程式，以確保的專輯標題和演出者名稱的屬性都少於 25 個字元。</span><span class="sxs-lookup"><span data-stu-id="40ba2-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="40ba2-255">使用新的截斷協助程式的完整檢視程式碼下方會出現。</span><span class="sxs-lookup"><span data-stu-id="40ba2-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="40ba2-256">現在當我們瀏覽 /StoreManager/ URL，則專輯和標題會保留下面我們最大長度。</span><span class="sxs-lookup"><span data-stu-id="40ba2-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="40ba2-257">注意:這會顯示簡單的情況下，建立和使用協助程式在一個檢視中。</span><span class="sxs-lookup"><span data-stu-id="40ba2-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="40ba2-258">若要深入了解建立可供您在整個網站的協助程式，請參閱我部落格文章： [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span><span class="sxs-lookup"><span data-stu-id="40ba2-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="40ba2-259">[上一頁](mvc-music-store-part-4.md)
> [下一頁](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="40ba2-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>
