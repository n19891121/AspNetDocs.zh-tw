---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 使用母版頁和部分重用 UI |微軟文件
author: rick-anderson
description: 步驟 7 探討了在檢視範本中應用" DRY 原則" 的方法,以便使用部分檢視範範本和母版頁來消除代碼重複。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: f381c4424a9fa0718cd234beeb01ce41bc4ca61e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542595"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a><span data-ttu-id="c9cb4-103">重複使用使用主版頁面和部分頁面的 UI</span><span class="sxs-lookup"><span data-stu-id="c9cb4-103">Re-use UI Using Master Pages and Partials</span></span>

<span data-ttu-id="c9cb4-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c9cb4-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="c9cb4-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="c9cb4-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="c9cb4-106">這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第7步,該教程示範如何使用ASP.NET MVC 1 構建小型但完整的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-106">This is step 7 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="c9cb4-107">步驟 7 探討了在檢視範本中應用" DRY 原則" 的方法,以便使用部分檢視範範本和母版頁來消除代碼重複。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-107">Step 7 looks at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication, using partial view templates and master pages.</span></span>
> 
> <span data-ttu-id="c9cb4-108">如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-7-partials-and-master-pages"></a><span data-ttu-id="c9cb4-109">神經晚餐步驟 7:部分和母版頁</span><span class="sxs-lookup"><span data-stu-id="c9cb4-109">NerdDinner Step 7: Partials and Master Pages</span></span>

<span data-ttu-id="c9cb4-110">MVC 擁抱ASP.NET的設計理念之一是"不要重複自己"原則(通常稱為"DRY")。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-110">One of the design philosophies ASP.NET MVC embraces is the "Do Not Repeat Yourself" principle (commonly referred to as "DRY").</span></span> <span data-ttu-id="c9cb4-111">DRY 設計有助於消除代碼和邏輯的重複,最終使應用程式構建速度更快,更易於維護。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-111">A DRY design helps eliminate the duplication of code and logic, which ultimately makes applications faster to build and easier to maintain.</span></span>

<span data-ttu-id="c9cb4-112">我們已經看到 DRY 原則應用於我們的一些 NerdDinner 方案。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-112">We've already seen the DRY principle applied in several of our NerdDinner scenarios.</span></span> <span data-ttu-id="c9cb4-113">舉幾個例子:我們的驗證邏輯在我們的模型層中實現,這使得它可以在控制器中編輯和創建方案之間強制執行;我們正在跨「編輯」、「詳細資訊」和「刪除」操作方法重用「未找到」檢視範範範範範範範範範範範範範範範範範範範範;我們使用具有檢視範本的約定命名模式,這樣無需在調用 View() 説明器方法時顯式指定名稱;我們正在重新使用 DinnerFormViewModel 類進行編輯和創建操作方案。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-113">A few examples: our validation logic is implemented within our model layer, which enables it to be enforced across both edit and create scenarios in our controller; we are re-using the "NotFound" view template across the Edit, Details and Delete action methods; we are using a convention- naming pattern with our view templates, which eliminates the need to explicitly specify the name when we call the View() helper method; and we are re-using the DinnerFormViewModel class for both Edit and Create action scenarios.</span></span>

<span data-ttu-id="c9cb4-114">現在,讓我們來看看如何在我們的視圖範本中應用"DRY 原則",以消除代碼重複。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-114">Let's now look at ways we can apply the "DRY Principle" within our view templates to eliminate code duplication there as well.</span></span>

### <a name="re-visiting-our-edit-and-create-view-templates"></a><span data-ttu-id="c9cb4-115">重新存取的編輯及建立檢視範本</span><span class="sxs-lookup"><span data-stu-id="c9cb4-115">Re-visiting our Edit and Create View Templates</span></span>

<span data-ttu-id="c9cb4-116">目前,我們使用兩個不同的檢視範本 - "Edit.aspx"和"Create.aspx" - 以顯示我們的晚餐表單 UI。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-116">Currently we are using two different view templates – "Edit.aspx" and "Create.aspx" – to display our Dinner form UI.</span></span> <span data-ttu-id="c9cb4-117">快速直觀地比較它們,突出顯示它們有多相似。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-117">A quick visual comparison of them highlights how similar they are.</span></span> <span data-ttu-id="c9cb4-118">下面是建立表單的外觀:</span><span class="sxs-lookup"><span data-stu-id="c9cb4-118">Below is what the create form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

<span data-ttu-id="c9cb4-119">下面是我們的「編輯」表單外觀:</span><span class="sxs-lookup"><span data-stu-id="c9cb4-119">And here is what our "Edit" form looks like:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

<span data-ttu-id="c9cb4-120">沒有什麼區別嗎?</span><span class="sxs-lookup"><span data-stu-id="c9cb4-120">Not much of a difference is there?</span></span> <span data-ttu-id="c9cb4-121">除了標題和標題文本之外,窗體佈局和輸入控制項是相同的。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-121">Other than the title and header text, the form layout and input controls are identical.</span></span>

<span data-ttu-id="c9cb4-122">如果我們打開"Edit.aspx"和"Create.aspx"視圖範本,我們會發現它們包含相同的表單佈局和輸入控制代碼。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-122">If we open up the "Edit.aspx" and "Create.aspx" view templates we'll find that they contain identical form layout and input control code.</span></span> <span data-ttu-id="c9cb4-123">這種重複意味著我們最終必須作出兩次更改,每當我們介紹或改變一個新的晚餐屬性 - 這是不好的。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-123">This duplication means we end up having to make changes twice anytime we introduce or change a new Dinner property - which is not good.</span></span>

### <a name="using-partial-view-templates"></a><span data-ttu-id="c9cb4-124">使用部分檢視範本</span><span class="sxs-lookup"><span data-stu-id="c9cb4-124">Using Partial View Templates</span></span>

<span data-ttu-id="c9cb4-125">mVC ASP.NET支援定義可用於封裝頁面子部分的檢視呈現邏輯的「部分檢視」樣本的能力。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-125">ASP.NET MVC supports the ability to define "partial view" templates that can be used to encapsulate view rendering logic for a sub-portion of a page.</span></span> <span data-ttu-id="c9cb4-126">"部分"提供了一種有用的方法來定義一次視圖呈現邏輯,然後在應用程式之間的多個位置重用它。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-126">"Partials" provide a useful way to define view rendering logic once, and then re-use it in multiple places across an application.</span></span>

<span data-ttu-id="c9cb4-127">為了説明"DRYup"我們的 Edit.aspx 和 Create.aspx 視圖範本複製,我們可以創建名為"DinnerForm.ascx"的部分視圖範本,該範本封裝了兩者共有的窗體佈局和輸入元素。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-127">To help "DRY-up" our Edit.aspx and Create.aspx view template duplication, we can create a partial view template named "DinnerForm.ascx" that encapsulates the form layout and input elements common to both.</span></span> <span data-ttu-id="c9cb4-128">我們將透過右鍵按下 /Views/Dinners 目錄並選擇「&gt;新增- 檢視」選單命令來執行此操作:</span><span class="sxs-lookup"><span data-stu-id="c9cb4-128">We'll do this by right-clicking on our /Views/Dinners directory and choosing the "Add-&gt;View" menu command:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

<span data-ttu-id="c9cb4-129">這將顯示「添加檢視」對話框。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-129">This will display the "Add View" dialog.</span></span> <span data-ttu-id="c9cb4-130">我們將命名要創建「DinnerForm」的新檢視,在對話框中選擇「創建部分視圖」複選框,並指示我們將傳遞一個 DinnerFormViewModel 類:</span><span class="sxs-lookup"><span data-stu-id="c9cb4-130">We'll name the new view we want to create "DinnerForm", select the "Create a partial view" checkbox within the dialog, and indicate that we will pass it a DinnerFormViewModel class:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

<span data-ttu-id="c9cb4-131">當我們按下「添加」按鈕時,Visual Studio 將在「@Views_Dinners」目錄中為我們創建新的「DinnerForm.ascx」視圖範本。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-131">When we click the "Add" button, Visual Studio will create a new "DinnerForm.ascx" view template for us within the "\Views\Dinners" directory.</span></span>

<span data-ttu-id="c9cb4-132">然後,我們可以將重複的表單佈局/輸入控制代碼從我們的 Edit.aspx/ Create.aspx 視圖範本複製/粘貼到新的「DinnerForm.ascx」部分檢視範本中:</span><span class="sxs-lookup"><span data-stu-id="c9cb4-132">We can then copy/paste the duplicate form layout / input control code from our Edit.aspx/ Create.aspx view templates into our new "DinnerForm.ascx" partial view template:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

<span data-ttu-id="c9cb4-133">然後,我們可以更新我們的"編輯"和"創建"視圖範本,以調用 DinnerForm 部分範本並消除表單複製。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-133">We can then update our Edit and Create view templates to call the DinnerForm partial template and eliminate the form duplication.</span></span> <span data-ttu-id="c9cb4-134">我們可以在檢視範本中呼叫 Html.Render 部分(「DinnerForm」)來執行此操作:</span><span class="sxs-lookup"><span data-stu-id="c9cb4-134">We can do this by calling Html.RenderPartial("DinnerForm") within our view templates:</span></span>

##### <a name="createaspx"></a><span data-ttu-id="c9cb4-135">建立.aspx</span><span class="sxs-lookup"><span data-stu-id="c9cb4-135">Create.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a><span data-ttu-id="c9cb4-136">編輯.aspx</span><span class="sxs-lookup"><span data-stu-id="c9cb4-136">Edit.aspx</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

<span data-ttu-id="c9cb4-137">在調用 Html.Render 部分(例如:\*視圖/Dinners/DinnerForm.ascx)時,您可以顯式限定所需的部分範本的路徑。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-137">You can explicitly qualify the path of the partial template you want when calling Html.RenderPartial (for example: ~Views/Dinners/DinnerForm.ascx").</span></span> <span data-ttu-id="c9cb4-138">但是,在上面的代碼中,我們利用了 mVC ASP.NET中基於約定的命名模式,並將"DinnerForm"指定為要呈現的部分名稱。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-138">In our code above, though, we are taking advantage of the convention-based naming pattern within ASP.NET MVC, and just specifying "DinnerForm" as the name of the partial to render.</span></span> <span data-ttu-id="c9cb4-139">當我們這樣做時ASP.NET MVC 將首先查看基於約定的視圖目錄(對於 DinnerSController,這將是 /視圖/晚餐)。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-139">When we do this ASP.NET MVC will look first in the convention-based views directory (for DinnersController this would be /Views/Dinners).</span></span> <span data-ttu-id="c9cb4-140">如果找不到部分範本,它將在 /Views/共享目錄中查找它。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-140">If it doesn't find the partial template there it will then look for it in the /Views/Shared directory.</span></span>

<span data-ttu-id="c9cb4-141">當僅使用部分檢視的名稱調用 Html.Render 部分()時,ASP.NET MVC 將傳遞給調用視圖範本使用的相同模型和 ViewData 字典物件。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-141">When Html.RenderPartial() is called with just the name of the partial view, ASP.NET MVC will pass to the partial view the same Model and ViewData dictionary objects used by the calling view template.</span></span> <span data-ttu-id="c9cb4-142">或者,有重載版本的 Html.Render 偏()使您能夠傳遞備用模型物件和/或 ViewData 字典供部分視圖使用。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-142">Alternatively, there are overloaded versions of Html.RenderPartial() that enable you to pass an alternate Model object and/or ViewData dictionary for the partial view to use.</span></span> <span data-ttu-id="c9cb4-143">這對於只想傳遞完整模型/視圖模型子集的方案非常有用。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-143">This is useful for scenarios where you only want to pass a subset of the full Model/ViewModel.</span></span>

| <span data-ttu-id="c9cb4-144">**側主題:為什麼&lt;&gt;%&lt;而不是&gt;%= % ?**</span><span class="sxs-lookup"><span data-stu-id="c9cb4-144">**Side Topic: Why &lt;% %&gt; instead of &lt;%= %&gt;?**</span></span> |
| --- |
| <span data-ttu-id="c9cb4-145">使用此代碼您可能注意到的一個微妙事情是,在呼&lt;叫 Html.Render.Render 部分()&lt;時,&gt;我們&gt;使用的是 % 塊 而不是 %% 塊。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-145">One of the subtle things you might have noticed with the code above is that we are using a &lt;% %&gt; block instead of a &lt;%= %&gt; block when calling Html.RenderPartial().</span></span> <span data-ttu-id="c9cb4-146">&lt;%=&gt; %ASP.NET 塊表示開發人員想要呈現指定值(例如:%= &lt;"你好"&gt;百分比 將呈現"你好")。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-146">&lt;%= %&gt; blocks in ASP.NET indicate that a developer wants to render a specified value (for example: &lt;%= "Hello" %&gt; would render "Hello").</span></span> <span data-ttu-id="c9cb4-147">&lt;%&gt;區塊表示開發人員想要執行代碼,並且其中的任何呈現輸出都必須顯式完成(例如:&lt;百分比回應.Write("你好")%&gt;。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-147">&lt;% %&gt; blocks instead indicate that the developer wants to execute code, and that any rendered output within them must be done explicitly (for example: &lt;% Response.Write("Hello") %&gt;.</span></span> <span data-ttu-id="c9cb4-148">我們使用&lt;上述 Html.Render&gt;部分程式碼的% 區塊的原因是 Html.Render 部份() 方法不傳回字串,而是將內容直接輸出到呼叫檢視範本的輸出流。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-148">The reason we are using a &lt;% %&gt; block with our Html.RenderPartial code above is because the Html.RenderPartial() method doesn't return a string, and instead outputs the content directly to the calling view template's output stream.</span></span> <span data-ttu-id="c9cb4-149">這樣做是出於性能效率的原因,並且這樣做可以避免創建(可能非常大的)臨時字串物件。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-149">It does this for performance efficiency reasons, and by doing so it avoids the need to create a (potentially very large) temporary string object.</span></span> <span data-ttu-id="c9cb4-150">這減少了記憶體使用量,並提高了應用程式的總體輸送量。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-150">This reduces memory usage and improves overall application throughput.</span></span> <span data-ttu-id="c9cb4-151">使用 Html.Render 部份()時,一個常見的錯誤是忘記在呼叫結束時添加分號,而該分&lt;號在&gt;% 塊內。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-151">One common mistake when using Html.RenderPartial() is to forget to add a semi-colon at the end of the call when it is within a &lt;% %&gt; block.</span></span> <span data-ttu-id="c9cb4-152">例如,此代碼將導致編譯器錯誤:% &lt;Html.Render 部分("DinnerForm")您&gt;需要編&lt;寫: % html.render部分("DinnerForm");%&gt;這是&lt;因為&gt;% % 塊是自包含的程式碼語句,並且使用 C# 程式碼語句時需要用分號終止。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-152">For example, this code will cause a compiler error: &lt;% Html.RenderPartial("DinnerForm") %&gt; You instead need to write: &lt;% Html.RenderPartial("DinnerForm"); %&gt; This is because &lt;% %&gt; blocks are self-contained code statements, and when using C# code statements need to be terminated with a semi-colon.</span></span> |

### <a name="using-partial-view-templates-to-clarify-code"></a><span data-ttu-id="c9cb4-153">使用部分檢視樣本來澄清代碼</span><span class="sxs-lookup"><span data-stu-id="c9cb4-153">Using Partial View Templates to Clarify Code</span></span>

<span data-ttu-id="c9cb4-154">我們創建了"DinnerForm"部分視圖範本,以避免在多個位置複製視圖呈現邏輯。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-154">We created the "DinnerForm" partial view template to avoid duplicating view rendering logic in multiple places.</span></span> <span data-ttu-id="c9cb4-155">這是創建部分檢視範本的最常見原因。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-155">This is the most common reason to create partial view templates.</span></span>

<span data-ttu-id="c9cb4-156">有時,即使只在單個位置調用部分視圖,創建部分視圖仍然有意義。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-156">Sometimes it still makes sense to create partial views even when they are only being called in a single place.</span></span> <span data-ttu-id="c9cb4-157">非常複雜的檢視範本在提取檢視呈現邏輯並將其分區為一個或多個命名良好的部分範本時,通常更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-157">Very complicated view templates can often become much easier to read when their view rendering logic is extracted and partitioned into one or more well named partial templates.</span></span>

<span data-ttu-id="c9cb4-158">例如,在我們的項目中考慮 Site.master 檔中的以下代碼段(我們稍後將查看)。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-158">For example, consider the below code-snippet from the Site.master file in our project (which we will be looking at shortly).</span></span> <span data-ttu-id="c9cb4-159">代碼相對直接讀取 - 部分是因為在螢幕右上角顯示登入/登出連結的邏輯封裝在「LogOnUserControl」部分:</span><span class="sxs-lookup"><span data-stu-id="c9cb4-159">The code is relatively straight-forward to read – partly because the logic to display a login/logout link at the top right of the screen is encapsulated within the "LogOnUserControl" partial:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

<span data-ttu-id="c9cb4-160">每當您發現自己試圖瞭解檢視範本中的 html/代碼標記時感到困惑,請考慮如果提取某些標記並將其重構為命名良好的部分檢視,是否不清楚。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-160">Whenever you find yourself getting confused trying to understand the html/code markup within a view-template, consider whether it wouldn't be clearer if some of it was extracted and refactored into well-named partial views.</span></span>

### <a name="master-pages"></a><span data-ttu-id="c9cb4-161">主版頁面</span><span class="sxs-lookup"><span data-stu-id="c9cb4-161">Master Pages</span></span>

<span data-ttu-id="c9cb4-162">除了支援部分檢視外,ASP.NET MVC 還支援創建可用於定義網站通用佈局和頂級 html 的「母版頁」範本的功能。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-162">In addition to supporting partial views, ASP.NET MVC also supports the ability to create "master page" templates that can be used to define the common layout and top-level html of a site.</span></span> <span data-ttu-id="c9cb4-163">然後,可以將內容占位符控件添加到母版頁,以標識視圖可以覆蓋或"填充"的可替換區域。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-163">Content placeholder controls can then be added to the master page to identify replaceable regions that can be overridden or "filled in" by views.</span></span> <span data-ttu-id="c9cb4-164">這提供了一種非常有效(和 DRY)的方法,用於跨應用程式應用通用佈局。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-164">This provides a very effective (and DRY) way to apply a common layout across an application.</span></span>

<span data-ttu-id="c9cb4-165">默認情況下,新的ASP.NET MVC 專案會自動向其添加母版頁範本。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-165">By default, new ASP.NET MVC projects have a master page template automatically added to them.</span></span> <span data-ttu-id="c9cb4-166">此母版頁名為「Site.master」,位於 [視圖] 共用] 資料夾中:</span><span class="sxs-lookup"><span data-stu-id="c9cb4-166">This master page is named "Site.master" and lives within the \Views\Shared\ folder:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

<span data-ttu-id="c9cb4-167">預設的 Site.master 檔如下所示。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-167">The default Site.master file looks like below.</span></span> <span data-ttu-id="c9cb4-168">它定義網站的外層 html,以及頂部導航功能表。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-168">It defines the outer html of the site, along with a menu for navigation at the top.</span></span> <span data-ttu-id="c9cb4-169">它包含兩個可取代的內容佔位元控制檔 - 一個用於標題,另一個用於要取代頁面的主要內容的位置:</span><span class="sxs-lookup"><span data-stu-id="c9cb4-169">It contains two replaceable content placeholder controls – one for the title, and the other for where the primary content of a page should be replaced:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

<span data-ttu-id="c9cb4-170">我們為NerdDinner應用程式創建的所有檢視範本("清單"、"詳細資訊"、"編輯"、"創建"、"未找到"等)都基於此 Site.master 範本。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-170">All of the view templates we've created for our NerdDinner application ("List", "Details", "Edit", "Create", "NotFound", etc) have been based on this Site.master template.</span></span> <span data-ttu-id="c9cb4-171">當我們使用「新增檢視」對話框建立檢視時,預設情況下新增到頂部&lt;% = 頁面&gt;% 指令的「MasterPageFile」屬性指示此指示:</span><span class="sxs-lookup"><span data-stu-id="c9cb4-171">This is indicated via the "MasterPageFile" attribute that was added by default to the top &lt;% @ Page %&gt; directive when we created our views using the "Add View" dialog:</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

<span data-ttu-id="c9cb4-172">這意味著我們可以更改 Site.master 內容,並在呈現任何檢視範本時自動應用和使用更改。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-172">What this means is that we can change the Site.master content, and have the changes automatically be applied and used when we render any of our view templates.</span></span>

<span data-ttu-id="c9cb4-173">讓我們更新我們的網站.master 的標頭部分,以便我們的應用程式的標頭是"NerdDinner"而不是"我的 MVC 應用程式"。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-173">Let's update our Site.master's header section so that the header of our application is "NerdDinner" instead of "My MVC Application".</span></span> <span data-ttu-id="c9cb4-174">讓我們還更新我們的導航功能表,以便第一個選項卡是「查找晚餐」(由 HomeController 的 Index() 操作方法處理),並且讓我們添加一個名為"主持晚餐「的新選項卡(由 DinnersController 的 Create() 操作方法處理):</span><span class="sxs-lookup"><span data-stu-id="c9cb4-174">Let's also update our navigation menu so that the first tab is "Find a Dinner" (handled by the HomeController's Index() action method), and let's add a new tab called "Host a Dinner" (handled by the DinnersController's Create() action method):</span></span>

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

<span data-ttu-id="c9cb4-175">當我們保存 Site.master 檔並刷新瀏覽器時,我們將看到我們的標頭更改顯示在應用程式中的所有檢視中。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-175">When we save the Site.master file and refresh our browser we'll see our header changes show up across all views within our application.</span></span> <span data-ttu-id="c9cb4-176">例如：</span><span class="sxs-lookup"><span data-stu-id="c9cb4-176">For example:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

<span data-ttu-id="c9cb4-177">使用 */Dinners/編輯/[id]* URL:</span><span class="sxs-lookup"><span data-stu-id="c9cb4-177">And with the */Dinners/Edit/[id]* URL:</span></span>

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a><span data-ttu-id="c9cb4-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9cb4-178">Next Step</span></span>

<span data-ttu-id="c9cb4-179">部分頁和母版頁提供了非常靈活的選項,使您能夠乾淨地組織視圖。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-179">Partials and master pages provide very flexible options that enable you to cleanly organize views.</span></span> <span data-ttu-id="c9cb4-180">您會發現,它們可説明您避免複製檢視內容/代碼,並使檢視範本更易於閱讀和維護。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-180">You'll find that they help you avoid duplicating view content/ code, and make your view templates easier to read and maintain.</span></span>

<span data-ttu-id="c9cb4-181">現在,讓我們重新訪問我們之前構建的清單方案,並啟用可擴展的分頁支援。</span><span class="sxs-lookup"><span data-stu-id="c9cb4-181">Let's now revisit the listing scenario we built earlier and enable scalable paging support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c9cb4-182">[前一個](use-viewdata-and-implement-viewmodel-classes.md)
> [下一個](implement-efficient-data-paging.md)</span><span class="sxs-lookup"><span data-stu-id="c9cb4-182">[Previous](use-viewdata-and-implement-viewmodel-classes.md)
[Next](implement-efficient-data-paging.md)</span></span>
