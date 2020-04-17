---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 使用檢視數據並實現檢視模型類 |微軟文件
author: rick-anderson
description: 步驟 6 顯示了如何支援更豐富的表單編輯方案,並討論了兩種方法,可用於將數據從控制器傳遞到視圖:...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 7fa2af2a55d12bbe11b29dff594823a1e5ea0152
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541100"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a><span data-ttu-id="e5b4f-103">使用 ViewData 和實作 ViewModel 類別</span><span class="sxs-lookup"><span data-stu-id="e5b4f-103">Use ViewData and Implement ViewModel Classes</span></span>

<span data-ttu-id="e5b4f-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e5b4f-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e5b4f-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="e5b4f-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="e5b4f-106">這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第6步,該教學示範如何使用ASP.NET MVC 1 構建小型但完整的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-106">This is step 6 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="e5b4f-107">步驟 6 顯示了如何支援更豐富的表單編輯方案,並討論了可用於將數據從控制器傳遞到視圖的兩種方法:ViewData 和 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-107">Step 6 shows how enable support for richer form editing scenarios, and also discusses two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>
> 
> <span data-ttu-id="e5b4f-108">如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a><span data-ttu-id="e5b4f-109">神經晚餐步驟 6:查看數據和視圖模型</span><span class="sxs-lookup"><span data-stu-id="e5b4f-109">NerdDinner Step 6: ViewData and ViewModel</span></span>

<span data-ttu-id="e5b4f-110">我們介紹了一些表單發佈方案,並討論了如何實現創建、更新和刪除 (CRUD) 支援。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-110">We've covered a number of form post scenarios, and discussed how to implement create, update and delete (CRUD) support.</span></span> <span data-ttu-id="e5b4f-111">現在,我們將進一步實施 DinnersController,並支援更豐富的表單編輯方案。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-111">We'll now take our DinnersController implementation further and enable support for richer form editing scenarios.</span></span> <span data-ttu-id="e5b4f-112">在此過程中,我們將討論兩種可用於將數據從控制器傳遞到視圖的方法:ViewData 和 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-112">While doing this we'll discuss two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>

### <a name="passing-data-from-controllers-to-view-templates"></a><span data-ttu-id="e5b4f-113">將資料從控制器傳遞到檢視範本</span><span class="sxs-lookup"><span data-stu-id="e5b4f-113">Passing Data from Controllers to View-Templates</span></span>

<span data-ttu-id="e5b4f-114">MVC 模式的一個定義特徵是嚴格"關注點分離",它有助於在應用程式的不同元件之間強制執行。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-114">One of the defining characteristics of the MVC pattern is the strict "separation of concerns" it helps enforce between the different components of an application.</span></span> <span data-ttu-id="e5b4f-115">模型、控制器和視圖都有定義明確的角色和職責,它們之間以定義明確的方式相互通信。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-115">Models, Controllers and Views each have well defined roles and responsibilities, and they communicate amongst each other in well defined ways.</span></span> <span data-ttu-id="e5b4f-116">這有助於提高可測試性和代碼重用性。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-116">This helps promote testability and code reuse.</span></span>

<span data-ttu-id="e5b4f-117">當 Controller 類別決定將 HTML 回應呈現回用戶端時,它負責顯式將呈現回應所需的所有資料傳遞給檢視範本。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-117">When a Controller class decides to render an HTML response back to a client, it is responsible for explicitly passing to the view template all of the data needed to render the response.</span></span> <span data-ttu-id="e5b4f-118">檢視範本絕不應執行任何資料檢索或應用程式邏輯,而應限制自己僅具有由控制器從模型/數據中驅動的呈現代碼。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-118">View templates should never perform any data retrieval or application logic – and should instead limit themselves to only have rendering code that is driven off of the model/data passed to it by the controller.</span></span>

<span data-ttu-id="e5b4f-119">現在,我們的 DinnersController 類傳遞給檢視範本的模型數據簡單而直接 — 在 Index()的情況下,是晚餐物件的清單,如果是詳細資訊(、Edit()、Create() 和刪除()的情況下,只有一個晚餐物件。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-119">Right now the model data being passed by our DinnersController class to our view templates is simple and straight-forward – a list of Dinner objects in the case of Index(), and a single Dinner object in the case of Details(), Edit(), Create() and Delete().</span></span> <span data-ttu-id="e5b4f-120">當我們向應用程式添加更多 UI 功能時,我們通常需要傳遞的不僅僅是這些數據,才能在檢視範本中呈現 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-120">As we add more UI capabilities to our application, we are often going to need to pass more than just this data to render HTML responses within our view templates.</span></span> <span data-ttu-id="e5b4f-121">例如,我們可能希望將"編輯"和"創建檢視"中的"國家/地區"欄位從 HTML 文本框更改為下拉清單。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-121">For example, we might want to change the "Country" field within our Edit and Create views from being an HTML textbox to a dropdownlist.</span></span> <span data-ttu-id="e5b4f-122">我們不是在檢視範本中硬編碼國家名稱的下拉清單,而是希望從我們動態填充的支援國家/地區列表中生成它。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-122">Rather than hard-code the dropdown list of country names in the view template, we might want to generate it from a list of supported countries that we populate dynamically.</span></span> <span data-ttu-id="e5b4f-123">我們需要一種方法,將 Dinner 物件*和支援*的國家/ 地區清單從控制器傳遞到視圖範本。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-123">We will need a way to pass both the Dinner object *and* the list of supported countries from our controller to our view templates.</span></span>

<span data-ttu-id="e5b4f-124">讓我們來看看兩種實現此目的的方法。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-124">Let's look at two ways we can accomplish this.</span></span>

### <a name="using-the-viewdata-dictionary"></a><span data-ttu-id="e5b4f-125">使用檢視資料字典</span><span class="sxs-lookup"><span data-stu-id="e5b4f-125">Using the ViewData Dictionary</span></span>

<span data-ttu-id="e5b4f-126">控制器基類公開一個"ViewData"字典屬性,該屬性可用於將其他數據項從控制器傳遞到視圖。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-126">The Controller base class exposes a "ViewData" dictionary property that can be used to pass additional data items from Controllers to Views.</span></span>

<span data-ttu-id="e5b4f-127">例如,為了支援我們希望將「編輯」視圖中的「國家/地區」文本框從 HTML 文本框更改為下拉清單的方案,我們可以更新我們的 Edit() 操作方法,以傳遞(除了晚餐物件之外)可用作國家/地區下拉清單的模型的 SelectList 物件。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-127">For example, to support the scenario where we want to change the "Country" textbox within our Edit view from being an HTML textbox to a dropdownlist, we can update our Edit() action method to pass (in addition to a Dinner object) a SelectList object that can be used as the model of a countries dropdownlist.</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

<span data-ttu-id="e5b4f-128">上面 SelectList 的建構函數正在接受要使用下拉清單以及當前選擇的值填充下拉清單的縣清單。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-128">The constructor of the SelectList above is accepting a list of counties to populate the drop-downlist with, as well as the currently selected value.</span></span>

<span data-ttu-id="e5b4f-129">然後,我們可以更新我們的 Edit.aspx 檢視範本,以使用 Html.DropDownList() 説明程式方法,而不是我們以前使用的 Html.TextBox() 幫助器方法:</span><span class="sxs-lookup"><span data-stu-id="e5b4f-129">We can then update our Edit.aspx view template to use the Html.DropDownList() helper method instead of the Html.TextBox() helper method we used previously:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

<span data-ttu-id="e5b4f-130">上面的 Html.DropDownList() 説明器方法採用兩個參數。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-130">The Html.DropDownList() helper method above takes two parameters.</span></span> <span data-ttu-id="e5b4f-131">第一個是要輸出的 HTML 窗體元素的名稱。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-131">The first is the name of the HTML form element to output.</span></span> <span data-ttu-id="e5b4f-132">第二個是我們通過 ViewData 字典傳遞的"選擇清單"</span><span class="sxs-lookup"><span data-stu-id="e5b4f-132">The second is the "SelectList" model we passed via the ViewData dictionary.</span></span> <span data-ttu-id="e5b4f-133">我們使用 C#"as"關鍵字將字典中的類型轉換為 SelectList。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-133">We are using the C# "as" keyword to cast the type within the dictionary as a SelectList.</span></span>

<span data-ttu-id="e5b4f-134">現在,當我們運行應用程式並訪問瀏覽器中的 */Dinners/Edit/1* URL 時,我們將看到我們的編輯 UI 已更新以顯示國家/地區清單而不是文本框:</span><span class="sxs-lookup"><span data-stu-id="e5b4f-134">And now when we run our application and access the */Dinners/Edit/1* URL within our browser we'll see that our edit UI has been updated to display a dropdownlist of countries instead of a textbox:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

<span data-ttu-id="e5b4f-135">由於我們還從 HTTP-POST Edit 方法呈現 Edit 檢視範本(在發生錯誤時),我們希望確保在錯誤方案中呈現檢視範本時,還要更新此方法以將 SelectList 添加到 ViewData:</span><span class="sxs-lookup"><span data-stu-id="e5b4f-135">Because we also render the Edit view template from the HTTP-POST Edit method (in scenarios when errors occur), we'll want to make sure that we also update this method to add the SelectList to ViewData when the view template is rendered in error scenarios:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

<span data-ttu-id="e5b4f-136">現在,我們的晚餐控制器編輯方案支援下拉清單。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-136">And now our DinnersController edit scenario supports a DropDownList.</span></span>

### <a name="using-a-viewmodel-pattern"></a><span data-ttu-id="e5b4f-137">使用檢視模型模式</span><span class="sxs-lookup"><span data-stu-id="e5b4f-137">Using a ViewModel Pattern</span></span>

<span data-ttu-id="e5b4f-138">ViewData 字典方法具有相當快速且易於實現的好處。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-138">The ViewData dictionary approach has the benefit of being fairly fast and easy to implement.</span></span> <span data-ttu-id="e5b4f-139">但是,有些開發人員不喜歡使用基於字串的字典,因為拼寫錯誤可能導致在編譯時不會捕獲的錯誤。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-139">Some developers don't like using string-based dictionaries, though, since typos can lead to errors that will not be caught at compile-time.</span></span> <span data-ttu-id="e5b4f-140">未鍵入的 ViewData 字典還要求在檢視範本中使用強類型語言(如 C#)時使用「as」運算符或強制轉換。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-140">The un-typed ViewData dictionary also requires using the "as" operator or casting when using a strongly-typed language like C# in a view template.</span></span>

<span data-ttu-id="e5b4f-141">我們可以使用的另一種方法是通常稱為「視圖模型」 模式的方法。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-141">An alternative approach that we could use is one often referred to as the "ViewModel" pattern.</span></span> <span data-ttu-id="e5b4f-142">使用此模式時,我們創建針對特定檢視方案優化的強類型類,並公開視圖範本所需的動態值/內容的屬性。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-142">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="e5b4f-143">然後,我們的控制器類可以填充這些視圖優化的類並將其傳遞給我們的視圖範本使用。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-143">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="e5b4f-144">這支援檢視範本中的類型安全、編譯時間檢查和編輯器對講。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-144">This enables type-safety, compile-time checking, and editor intellisense within view templates.</span></span>

<span data-ttu-id="e5b4f-145">例如,為了啟用晚餐表單編輯方案,我們可以創建一個「DinnerFormViewModel」類,如下所示,該類公開了兩個強類型屬性:一個「晚餐」物件,以及填充國家/地區下拉清單所需的 SelectList 模型:</span><span class="sxs-lookup"><span data-stu-id="e5b4f-145">For example, to enable dinner form editing scenarios we can create a "DinnerFormViewModel" class like below that exposes two strongly-typed properties: a Dinner object, and the SelectList model needed to populate the countries dropdownlist:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

<span data-ttu-id="e5b4f-146">然後,我們可以更新我們的 Edit() 操作方法,使用從存儲庫檢索的 Dinner 物件創建 DinnerFormViewModel,然後將其傳遞到檢視範本:</span><span class="sxs-lookup"><span data-stu-id="e5b4f-146">We can then update our Edit() action method to create the DinnerFormViewModel using the Dinner object we retrieve from our repository, and then pass it to our view template:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

<span data-ttu-id="e5b4f-147">然後,我們將更新視圖範本,以便它期望有一個「DinnerFormViewModel」而不是「Dinner」物件,例如,更改 edit.aspx 頁面頂部的「繼承」屬性:</span><span class="sxs-lookup"><span data-stu-id="e5b4f-147">We'll then update our view template so that it expects a "DinnerFormViewModel" instead of a "Dinner" object by changing the "inherits" attribute at the top of the edit.aspx page like so:</span></span>

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

<span data-ttu-id="e5b4f-148">一旦我們這樣做,視圖範本中「模型」屬性的對講義將更新,以反映我們傳遞的 DinnerFormViewModel 類型的物件模型:</span><span class="sxs-lookup"><span data-stu-id="e5b4f-148">Once we do this, the intellisense of the "Model" property within our view template will be updated to reflect the object model of the DinnerFormViewModel type we are passing it:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

<span data-ttu-id="e5b4f-149">然後,我們可以更新視圖代碼以擺脫它。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-149">We can then update our view code to work off of it.</span></span> <span data-ttu-id="e5b4f-150">請注意,下面我們如何不更改要創建的輸入元素的名稱(表單元素仍將命名為"標題"、"國家/地區"),但我們正在更新 HTML 幫助器方法,以便使用 DinnerFormViewModel 類檢索值:</span><span class="sxs-lookup"><span data-stu-id="e5b4f-150">Notice below how we are not changing the names of the input elements we are creating (the form elements will still be named "Title", "Country") – but we are updating the HTML Helper methods to retrieve the values using the DinnerFormViewModel class:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

<span data-ttu-id="e5b4f-151">在呈現錯誤時,我們還將更新編輯帖子方法以使用 DinnerFormViewModel 類:</span><span class="sxs-lookup"><span data-stu-id="e5b4f-151">We'll also update our Edit post method to use the DinnerFormViewModel class when rendering errors:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

<span data-ttu-id="e5b4f-152">我們還可以更新我們的 Create() 操作方法,以重複使用完全相同的*DinnerFormViewModel*類,使這些國家 / 地區也能夠刪除清單。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-152">We can also update our Create() action methods to re-use the exact same *DinnerFormViewModel* class to enable the countries DropDownList within those as well.</span></span> <span data-ttu-id="e5b4f-153">下面是 HTTP-GET 實現:</span><span class="sxs-lookup"><span data-stu-id="e5b4f-153">Below is the HTTP-GET implementation:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

<span data-ttu-id="e5b4f-154">下面是 HTTP-POST 建立方法的實現:</span><span class="sxs-lookup"><span data-stu-id="e5b4f-154">Below is the implementation of the HTTP-POST Create method:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

<span data-ttu-id="e5b4f-155">現在,我們的"編輯"和"創建"螢幕都支持選擇國家/地區的下拉清單。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-155">And now both our Edit and Create screens support drop-downlists for picking the country.</span></span>

### <a name="custom-shaped-viewmodel-classes"></a><span data-ttu-id="e5b4f-156">自訂元件的檢視模型類別</span><span class="sxs-lookup"><span data-stu-id="e5b4f-156">Custom-shaped ViewModel classes</span></span>

<span data-ttu-id="e5b4f-157">在上面的場景中,我們的 DinnerFormViewModel 類直接將 Dinner 模型物件公開為屬性,以及支援 SelectList 模型屬性。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-157">In the scenario above, our DinnerFormViewModel class directly exposes the Dinner model object as a property, along with a supporting SelectList model property.</span></span> <span data-ttu-id="e5b4f-158">此方法適用於要在檢視範本中創建的 HTML UI 與網域模型物件相對接近的情況。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-158">This approach works fine for scenarios where the HTML UI we want to create within our view template corresponds relatively closely to our domain model objects.</span></span>

<span data-ttu-id="e5b4f-159">對於情況並非如此的情況,可以使用的一個選項是創建一個自定義形狀的 ViewModel 類,其物件模型更優化以供視圖使用,並且可能與基礎域模型物件的外觀完全不同。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-159">For scenarios where this isn't the case, one option that you can use is to create a custom-shaped ViewModel class whose object model is more optimized for consumption by the view – and which might look completely different from the underlying domain model object.</span></span> <span data-ttu-id="e5b4f-160">例如,它可能會公開從多個模型物件收集的不同屬性名稱和/或聚合屬性。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-160">For example, it could potentially expose different property names and/or aggregate properties collected from multiple model objects.</span></span>

<span data-ttu-id="e5b4f-161">自定義形狀的 ViewModel 類既可用於將數據從控制器傳遞到要渲染的檢視,也可用於幫助處理發回控制器操作方法的表單數據。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-161">Custom-shaped ViewModel classes can be used both to pass data from controllers to views to render, as well as to help handle form data posted back to a controller's action method.</span></span> <span data-ttu-id="e5b4f-162">對於此後續方案,您可能讓操作方法使用發佈表單的數據更新 ViewModel 物件,然後使用 ViewModel 實例映射或檢索實際域模型物件。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-162">For this later scenario, you might have the action method update a ViewModel object with the form-posted data, and then use the ViewModel instance to map or retrieve an actual domain model object.</span></span>

<span data-ttu-id="e5b4f-163">自定義形狀的 ViewModel 類可以提供很大的靈活性,並且每當在檢視範本中查找呈現代碼或操作方法中的表單發佈代碼開始變得過於複雜時,都是要調查的內容。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-163">Custom-shaped ViewModel classes can provide a great deal of flexibility, and are something to investigate any time you find the rendering code within your view templates or the form-posting code inside your action methods starting to get too complicated.</span></span> <span data-ttu-id="e5b4f-164">這通常表明網域模型與您生成的 UI 不乾淨對應,並且中間自定義形狀的 ViewModel 類可以提供説明。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-164">This is often a sign that your domain models don't cleanly correspond to the UI you are generating, and that an intermediate custom-shaped ViewModel class can help.</span></span>

### <a name="next-step"></a><span data-ttu-id="e5b4f-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e5b4f-165">Next Step</span></span>

<span data-ttu-id="e5b4f-166">現在,讓我們來瞭解一下如何使用部分頁和母版頁來重用和共用整個應用程式中的 UI。</span><span class="sxs-lookup"><span data-stu-id="e5b4f-166">Let's now look at how we can use partials and master-pages to re-use and share UI across our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e5b4f-167">[前一個](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [下一個](re-use-ui-using-master-pages-and-partials.md)</span><span class="sxs-lookup"><span data-stu-id="e5b4f-167">[Previous](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Next](re-use-ui-using-master-pages-and-partials.md)</span></span>
