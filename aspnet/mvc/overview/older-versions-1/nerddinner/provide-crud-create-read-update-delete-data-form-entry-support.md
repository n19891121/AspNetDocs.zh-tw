---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: 提供 CRUD(建立、讀取、更新、刪除)資料表單輸入支援 |微軟文件
author: rick-anderson
description: 步驟 5 演示如何透過支援編輯、創建和刪除晚餐來進一步增加我們的 DinnersController 課程。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: 2b75a7eda8bce4baa25d92626639f4d904eb363a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542621"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a><span data-ttu-id="dc8c8-103">提供 CRUD (建立、讀取、更新、刪除) 資料表單項目支援</span><span class="sxs-lookup"><span data-stu-id="dc8c8-103">Provide CRUD (Create, Read, Update, Delete) Data Form Entry Support</span></span>

<span data-ttu-id="dc8c8-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="dc8c8-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="dc8c8-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="dc8c8-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="dc8c8-106">這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第5步,它介紹了如何使用 ASP.NETmVC1構建小型但完整的Web應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-106">This is step 5 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="dc8c8-107">步驟 5 演示如何透過支援編輯、創建和刪除晚餐來進一步增加我們的 DinnersController 課程。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-107">Step 5 shows how to take our DinnersController class further by enable support for editing, creating and deleting Dinners with it as well.</span></span>
> 
> <span data-ttu-id="dc8c8-108">如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a><span data-ttu-id="dc8c8-109">神經晚餐步驟 5:創建、更新、刪除表單方案</span><span class="sxs-lookup"><span data-stu-id="dc8c8-109">NerdDinner Step 5: Create, Update, Delete Form Scenarios</span></span>

<span data-ttu-id="dc8c8-110">我們介紹了控制器和視圖,並介紹了如何使用它們在現場為 Dinner 實現清單/詳細信息體驗。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-110">We've introduced controllers and views, and covered how to use them to implement a listing/details experience for Dinners on site.</span></span> <span data-ttu-id="dc8c8-111">我們的下一步是進一步提高我們的 DinnersController 課程,並支援編輯、創建和刪除晚餐。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-111">Our next step will be to take our DinnersController class further and enable support for editing, creating and deleting Dinners with it as well.</span></span>

### <a name="urls-handled-by-dinnerscontroller"></a><span data-ttu-id="dc8c8-112">由晚餐控制器處理的網址</span><span class="sxs-lookup"><span data-stu-id="dc8c8-112">URLs handled by DinnersController</span></span>

<span data-ttu-id="dc8c8-113">我們之前向 DinnersController 添加了操作方法,這些方法對兩個 URL 進行了支援 *:/晚餐*和 */晚餐/詳細資訊/[id]。*</span><span class="sxs-lookup"><span data-stu-id="dc8c8-113">We previously added action methods to DinnersController that implemented support for two URLs: */Dinners* and */Dinners/Details/[id]*.</span></span>

| <span data-ttu-id="dc8c8-114">**URL**</span><span class="sxs-lookup"><span data-stu-id="dc8c8-114">**URL**</span></span> | <span data-ttu-id="dc8c8-115">**動詞**</span><span class="sxs-lookup"><span data-stu-id="dc8c8-115">**VERB**</span></span> | <span data-ttu-id="dc8c8-116">**目的**</span><span class="sxs-lookup"><span data-stu-id="dc8c8-116">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc8c8-117">*/晚餐/*</span><span class="sxs-lookup"><span data-stu-id="dc8c8-117">*/Dinners/*</span></span> | <span data-ttu-id="dc8c8-118">GET</span><span class="sxs-lookup"><span data-stu-id="dc8c8-118">GET</span></span> | <span data-ttu-id="dc8c8-119">顯示即將來臨的晚宴的 HTML 清單。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-119">Display an HTML list of upcoming dinners.</span></span> |
| <span data-ttu-id="dc8c8-120">*/晚餐/詳情/[id]*</span><span class="sxs-lookup"><span data-stu-id="dc8c8-120">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="dc8c8-121">GET</span><span class="sxs-lookup"><span data-stu-id="dc8c8-121">GET</span></span> | <span data-ttu-id="dc8c8-122">顯示有關特定晚餐的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-122">Display details about a specific dinner.</span></span> |

<span data-ttu-id="dc8c8-123">現在,我們將添加操作方法來實現三個附加*URL:/晚餐/編輯/[id]、/\*\*晚餐/創建*和 */晚餐/刪除/[id]。*</span><span class="sxs-lookup"><span data-stu-id="dc8c8-123">We will now add action methods to implement three additional URLs: */Dinners/Edit/[id]*, */Dinners/Create*, and */Dinners/Delete/[id]*.</span></span> <span data-ttu-id="dc8c8-124">這些 URL 將支援編輯現有晚餐、創建新晚餐和刪除晚餐。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-124">These URLs will enable support for editing existing Dinners, creating new Dinners, and deleting Dinners.</span></span>

<span data-ttu-id="dc8c8-125">我們將支援 HTTP GET 和 HTTP POST 謂詞與這些新 URL 的互動。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-125">We will support both HTTP GET and HTTP POST verb interactions with these new URLs.</span></span> <span data-ttu-id="dc8c8-126">對這些 URL 的 HTTP GET 請求將顯示資料的初始 HTML 檢視(在"編輯"的情況下填充了 Dinner 資料的窗體,在"創建"的情況下填充了空白表單,在"刪除"的情況下顯示刪除確認螢幕)。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-126">HTTP GET requests to these URLs will display the initial HTML view of the data (a form populated with the Dinner data in the case of "edit", a blank form in the case of "create", and a delete confirmation screen in the case of "delete").</span></span> <span data-ttu-id="dc8c8-127">對這些 URL 的 HTTP POST 請求將儲存/更新/刪除我們的晚餐儲存庫中的晚餐數據(並從那裡保存到資料庫)。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-127">HTTP POST requests to these URLs will save/update/delete the Dinner data in our DinnerRepository (and from there to the database).</span></span>

| <span data-ttu-id="dc8c8-128">**URL**</span><span class="sxs-lookup"><span data-stu-id="dc8c8-128">**URL**</span></span> | <span data-ttu-id="dc8c8-129">**動詞**</span><span class="sxs-lookup"><span data-stu-id="dc8c8-129">**VERB**</span></span> | <span data-ttu-id="dc8c8-130">**目的**</span><span class="sxs-lookup"><span data-stu-id="dc8c8-130">**Purpose**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc8c8-131">*/晚餐/編輯/[id]*</span><span class="sxs-lookup"><span data-stu-id="dc8c8-131">*/Dinners/Edit/[id]*</span></span> | <span data-ttu-id="dc8c8-132">GET</span><span class="sxs-lookup"><span data-stu-id="dc8c8-132">GET</span></span> | <span data-ttu-id="dc8c8-133">顯示填充晚餐資料的可編輯 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-133">Display an editable HTML form populated with Dinner data.</span></span> |
| <span data-ttu-id="dc8c8-134">POST</span><span class="sxs-lookup"><span data-stu-id="dc8c8-134">POST</span></span> | <span data-ttu-id="dc8c8-135">將特定 Dinner 的表單更改保存到資料庫。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-135">Save the form changes for a particular Dinner to the database.</span></span> |
| <span data-ttu-id="dc8c8-136">*/晚餐/創建*</span><span class="sxs-lookup"><span data-stu-id="dc8c8-136">*/Dinners/Create*</span></span> | <span data-ttu-id="dc8c8-137">GET</span><span class="sxs-lookup"><span data-stu-id="dc8c8-137">GET</span></span> | <span data-ttu-id="dc8c8-138">顯示一個空的 HTML 表單,允許使用者定義新的晚餐。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-138">Display an empty HTML form that allows users to define new Dinners.</span></span> |
| <span data-ttu-id="dc8c8-139">POST</span><span class="sxs-lookup"><span data-stu-id="dc8c8-139">POST</span></span> | <span data-ttu-id="dc8c8-140">創建新的晚餐並將其保存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-140">Create a new Dinner and save it in the database.</span></span> |
| <span data-ttu-id="dc8c8-141">*/晚餐/刪除/[id]*</span><span class="sxs-lookup"><span data-stu-id="dc8c8-141">*/Dinners/Delete/[id]*</span></span> | <span data-ttu-id="dc8c8-142">GET</span><span class="sxs-lookup"><span data-stu-id="dc8c8-142">GET</span></span> | <span data-ttu-id="dc8c8-143">顯示刪除確認螢幕。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-143">Display delete confirmation screen.</span></span> |
| <span data-ttu-id="dc8c8-144">POST</span><span class="sxs-lookup"><span data-stu-id="dc8c8-144">POST</span></span> | <span data-ttu-id="dc8c8-145">從資料庫中刪除指定的晚餐。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-145">Deletes the specified dinner from the database.</span></span> |

### <a name="edit-support"></a><span data-ttu-id="dc8c8-146">編輯支援</span><span class="sxs-lookup"><span data-stu-id="dc8c8-146">Edit Support</span></span>

<span data-ttu-id="dc8c8-147">讓我們從實現"編輯"方案開始。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-147">Let's begin by implementing the "edit" scenario.</span></span>

#### <a name="the-http-get-edit-action-method"></a><span data-ttu-id="dc8c8-148">HTTP-GET 編輯操作方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-148">The HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="dc8c8-149">我們將首先實現編輯操作方法的 HTTP"GET"行為。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-149">We'll start by implementing the HTTP "GET" behavior of our edit action method.</span></span> <span data-ttu-id="dc8c8-150">當請求 */Dinners/Edit/[id]* URL 時,將調用此方法。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-150">This method will be invoked when the */Dinners/Edit/[id]* URL is requested.</span></span> <span data-ttu-id="dc8c8-151">我們的實現將如下所示:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-151">Our implementation will look like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

<span data-ttu-id="dc8c8-152">上述代碼使用 Dinner 儲存庫檢索 Dinner 物件。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-152">The code above uses the DinnerRepository to retrieve a Dinner object.</span></span> <span data-ttu-id="dc8c8-153">然後,它使用「晚餐」對象呈現視圖範本。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-153">It then renders a View template using the Dinner object.</span></span> <span data-ttu-id="dc8c8-154">由於我們尚未將範本名稱顯式傳遞給*View()* 幫助器方法,它將使用基於約定的預設路徑來解決視圖範本:/視圖/Dinners/Edit.aspx。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-154">Because we haven't explicitly passed a template name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Edit.aspx.</span></span>

<span data-ttu-id="dc8c8-155">現在,讓我們創建此視圖範本。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-155">Let's now create this view template.</span></span> <span data-ttu-id="dc8c8-156">我們將在「編輯」方法中右鍵按一下並選擇「新增檢視」上下文選單命令來執行此操作:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-156">We will do this by right-clicking within the Edit method and selecting the "Add View" context menu command:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

<span data-ttu-id="dc8c8-157">在「添加檢視」對話框中,我們將指示我們將將 Dinner 物件傳遞給檢視範本作為其模型,並選擇自動基腳模式「編輯」範本:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-157">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to auto-scaffold an "Edit" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

<span data-ttu-id="dc8c8-158">當我們按下「添加」按鈕時,Visual Studio 將在「@Views_Dinners」目錄中為我們添加新的「Edit.aspx」檢視範本檔。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-158">When we click the "Add" button, Visual Studio will add a new "Edit.aspx" view template file for us within the "\Views\Dinners" directory.</span></span> <span data-ttu-id="dc8c8-159">它還將在代碼編輯器中打開新的「Edit.aspx」檢視範本, 填充了初始的「編輯」基架實現,如下所示:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-159">It will also open up the new "Edit.aspx" view template within the code-editor – populated with an initial "Edit" scaffold implementation like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

<span data-ttu-id="dc8c8-160">讓我們對產生的預設「編輯」基架進行一些更改,並更新編輯檢視範本以包含以下內容(這將刪除一些我們不想公開的屬性):</span><span class="sxs-lookup"><span data-stu-id="dc8c8-160">Let's make a few changes to the default "edit" scaffold generated, and update the edit view template to have the content below (which removes a few of the properties we don't want to expose):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

<span data-ttu-id="dc8c8-161">當我們運行應用程式並請求 *「/晚餐/編輯/1」URL*時,我們將看到以下頁面:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-161">When we run the application and request the *"/Dinners/Edit/1"* URL we will see the following page:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

<span data-ttu-id="dc8c8-162">我們的檢視生成的 HTML 標記如下所示。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-162">The HTML markup generated by our view looks like below.</span></span> <span data-ttu-id="dc8c8-163">它是標準 HTML&lt;&gt;– 噹 按&lt;下"儲存" 輸入類型&gt;="提交" 按鈕時,具有對 */Dinners/Edit/1* URL 執行 HTTP POST 的表單元素。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-163">It is standard HTML – with a &lt;form&gt; element that performs an HTTP POST to the */Dinners/Edit/1* URL when the "Save" &lt;input type="submit"/&gt; button is pushed.</span></span> <span data-ttu-id="dc8c8-164">已為每個&lt;可編輯屬性輸出&gt;HTML 輸入類型=「文字」/元素:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-164">A HTML &lt;input type="text"/&gt; element has been output for each editable property:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a><span data-ttu-id="dc8c8-165">Html.BeginForm() 與 html.TextBox() html 說明器方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-165">Html.BeginForm() and Html.TextBox() Html Helper Methods</span></span>

<span data-ttu-id="dc8c8-166">我們的"Edit.aspx"檢視範本使用多個"Html 幫助程式"方法:Html.驗證摘要()、Html.BeginForm()、Html.TextBox()和 Html.驗證消息()。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-166">Our "Edit.aspx" view template is using several "Html Helper" methods: Html.ValidationSummary(), Html.BeginForm(), Html.TextBox(), and Html.ValidationMessage().</span></span> <span data-ttu-id="dc8c8-167">除了為我們生成 HTML 標記外,這些幫助程式方法還提供內建的錯誤處理和驗證支援。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-167">In addition to generating HTML markup for us, these helper methods provide built-in error handling and validation support.</span></span>

##### <a name="htmlbeginform-helper-method"></a><span data-ttu-id="dc8c8-168">Html.BeginForm() 說明器方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-168">Html.BeginForm() helper method</span></span>

<span data-ttu-id="dc8c8-169">Html.BeginForm() 幫助器方法是在我們的標記中&lt;輸出&gt;HTML 表單元素的內容。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-169">The Html.BeginForm() helper method is what output the HTML &lt;form&gt; element in our markup.</span></span> <span data-ttu-id="dc8c8-170">在我們的 Edit.aspx 檢視範本中,您會注意到,在使用此方法時,我們正在應用 C#"使用"語句。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-170">In our Edit.aspx view template you'll notice that we are applying a C# "using" statement when using this method.</span></span> <span data-ttu-id="dc8c8-171">開啟的大&lt;括弧表示表&gt;單 內容的開始,而關閉的大括&lt;弧表示&gt;/form 元素的結束:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-171">The open curly brace indicates the beginning of the &lt;form&gt; content, and the closing curly brace is what indicates the end of the &lt;/form&gt; element:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

<span data-ttu-id="dc8c8-172">或者,如果您發現"使用"語句方法對於這樣的方案不自然,則可以使用 Html.BeginForm() 和 Html.EndForm() 組合 (執行相同的功能):</span><span class="sxs-lookup"><span data-stu-id="dc8c8-172">Alternatively, if you find the "using" statement approach unnatural for a scenario like this, you can use a Html.BeginForm() and Html.EndForm() combination (which does the same thing):</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

<span data-ttu-id="dc8c8-173">呼叫 Html.BeginForm() 沒有任何參數將導致它輸出對目前請求的 URL 執行 HTTP-POST 的表單元素。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-173">Calling Html.BeginForm() without any parameters will cause it to output a form element that does an HTTP-POST to the current request's URL.</span></span> <span data-ttu-id="dc8c8-174">這就是為什麼我們的"編輯"視圖生成*&lt;表單操作\"/晚餐/編輯/1"方法="後&gt;"* 元素。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-174">That is why our Edit view generates a *&lt;form action="/Dinners/Edit/1" method="post"&gt;* element.</span></span> <span data-ttu-id="dc8c8-175">如果我們想要發佈到其他 URL,我們也可以將顯式參數傳遞給 Html.BeginForm()。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-175">We could have alternatively passed explicit parameters to Html.BeginForm() if we wanted to post to a different URL.</span></span>

##### <a name="htmltextbox-helper-method"></a><span data-ttu-id="dc8c8-176">Html.TextBox() 說明器方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-176">Html.TextBox() helper method</span></span>

<span data-ttu-id="dc8c8-177">我們的 Edit.aspx 檢視使用 Html.TextBox() 協助器&lt;方法輸出&gt;輸入類型=「文字」/元素:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-177">Our Edit.aspx view uses the Html.TextBox() helper method to output &lt;input type="text"/&gt; elements:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

<span data-ttu-id="dc8c8-178">上面的 Html.TextBox() 方法採用單個參數&lt;, 用於指定 要輸出的輸入類型的 id/name&gt;屬性= "text"/ 元素,以及用於填充文字框值的模型屬性。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-178">The Html.TextBox() method above takes a single parameter – which is being used to specify both the id/name attributes of the &lt;input type="text"/&gt; element to output, as well as the model property to populate the textbox value from.</span></span> <span data-ttu-id="dc8c8-179">例如,我們傳遞給"編輯"視圖的 Dinner 物件具有".NET 期貨"的"標題"屬性值,因此我們的 Html.TextBox("標題")方法調用輸出:*&lt;輸入 id="標題"名稱="標題"類型="文本&gt;"值=".NET 期貨"/。*</span><span class="sxs-lookup"><span data-stu-id="dc8c8-179">For example, the Dinner object we passed to the Edit view had a "Title" property value of ".NET Futures", and so our Html.TextBox("Title") method call output: *&lt;input id="Title" name="Title" type="text" value=".NET Futures" /&gt;*.</span></span>

<span data-ttu-id="dc8c8-180">或者,我們可以使用第一個 Html.TextBox() 參數來指定元素的 ID/名稱,然後顯式傳遞值以用作第二個參數:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-180">Alternatively, we can use the first Html.TextBox() parameter to specify the id/name of the element, and then explicitly pass in the value to use as a second parameter:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

<span data-ttu-id="dc8c8-181">通常,我們希望對輸出的值執行自定義格式設置。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-181">Often we'll want to perform custom formatting on the value that is output.</span></span> <span data-ttu-id="dc8c8-182">內置於 .NET 的 String.Format() 靜態方法對於這些方案很有用。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-182">The String.Format() static method built-into .NET is useful for these scenarios.</span></span> <span data-ttu-id="dc8c8-183">我們的 Edit.aspx 檢視樣本正在使用此設定事件日期值(類型為 DateTime)的格式,以便它不顯示時間上的秒數:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-183">Our Edit.aspx view template is using this to format the EventDate value (which is of type DateTime) so that it doesn't show seconds for the time:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

<span data-ttu-id="dc8c8-184">可以選擇使用 Html.TextBox() 的第三個參數來輸出其他 HTML 屬性。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-184">A third parameter to Html.TextBox() can optionally be used to output additional HTML attributes.</span></span> <span data-ttu-id="dc8c8-185">下面的程式碼段演示如何&lt;在輸入類型="text"/&gt;元素上呈現額外的大小="30"屬性和類="mycssclass"屬性。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-185">The code-snippet below demonstrates how to render an additional size="30" attribute and a class="mycssclass" attribute on the &lt;input type="text"/&gt; element.</span></span> <span data-ttu-id="dc8c8-186">請注意,如何使用「類」@" character because "從類屬性的名稱中轉義是 C# 中的保留關鍵字:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-186">Note how we are escaping the name of the class attribute using a "@" character because "class" is a reserved keyword in C#:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a><span data-ttu-id="dc8c8-187">完整編取 HTTP-POST 編輯操作方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-187">Implementing the HTTP-POST Edit Action Method</span></span>

<span data-ttu-id="dc8c8-188">現在,我們實現了"編輯"操作方法的 HTTP-GET 版本。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-188">We now have the HTTP-GET version of our Edit action method implemented.</span></span> <span data-ttu-id="dc8c8-189">當使用者請求 */Dinners/Edit/1* URL 時,他們收到一個 HTML 頁面,如下所示:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-189">When a user requests the */Dinners/Edit/1* URL they receive an HTML page like the following:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

<span data-ttu-id="dc8c8-190">按下「保存」按鈕會導致表單發布到 */Dinners/Edit/1* URL,並使用 HTTP&lt;&gt;POST 謂 詞 提交 HTML 輸入表單值。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-190">Pressing the "Save" button causes a form post to the */Dinners/Edit/1* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span> <span data-ttu-id="dc8c8-191">現在,讓我們實現編輯操作方法的 HTTP POST 行為 , 這將處理保存晚餐。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-191">Let's now implement the HTTP POST behavior of our edit action method – which will handle saving the Dinner.</span></span>

<span data-ttu-id="dc8c8-192">我們將首先向 DinnersController 添加一個重載的「編輯」操作方法,該控制器上具有「AcceptVerbs」屬性,指示它處理 HTTP POST 方案:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-192">We'll begin by adding an overloaded "Edit" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

<span data-ttu-id="dc8c8-193">當 [AcceptVerbs] 屬性應用於重載操作方法時,ASP.NET MVC 根據傳入的 HTTP 謂詞自動處理向相應操作方法發送請求。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-193">When the [AcceptVerbs] attribute is applied to overloaded action methods, ASP.NET MVC automatically handles dispatching requests to the appropriate action method depending on the incoming HTTP verb.</span></span> <span data-ttu-id="dc8c8-194">HTTP POST 對 */Dinners/Edit/[id]* URL 的請求將轉到上述編輯方法,而所有其他 HTTP 謂詞請求 */Dinners/Edit/[id]* URL 將`[AcceptVerbs]`轉到我們實現的第一個編輯方法( 該方法沒有屬性)。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-194">HTTP POST requests to */Dinners/Edit/[id]* URLs will go to the above Edit method, while all other HTTP verb requests to */Dinners/Edit/[id]* URLs will go to the first Edit method we implemented (which did not have an `[AcceptVerbs]` attribute).</span></span>

| <span data-ttu-id="dc8c8-195">**側主題:為什麼通過 HTTP 謂詞進行區分?**</span><span class="sxs-lookup"><span data-stu-id="dc8c8-195">**Side Topic: Why differentiate via HTTP verbs?**</span></span> |
| --- |
| <span data-ttu-id="dc8c8-196">您可能會問 – 為什麼我們使用單個 URL 並通過 HTTP 謂詞區分其行為?</span><span class="sxs-lookup"><span data-stu-id="dc8c8-196">You might ask – why are we using a single URL and differentiating its behavior via the HTTP verb?</span></span> <span data-ttu-id="dc8c8-197">為什麼不只有兩個單獨的 URL 來處理載入和儲存編輯更改?</span><span class="sxs-lookup"><span data-stu-id="dc8c8-197">Why not just have two separate URLs to handle loading and saving edit changes?</span></span> <span data-ttu-id="dc8c8-198">例如:/Dinners/Edit/[id]以顯示初始窗體和/Dinners/保存/[id]來處理表單帖子以保存它?</span><span class="sxs-lookup"><span data-stu-id="dc8c8-198">For example: /Dinners/Edit/[id] to display the initial form and /Dinners/Save/[id] to handle the form post to save it?</span></span> <span data-ttu-id="dc8c8-199">發佈兩個單獨的 URL 的缺點是,如果我們發布到 /Dinners/Save/2,然後由於輸入錯誤而需要重新顯示 HTML 表單,最終使用者最終將在其瀏覽器的位址列中具有 /Dinners/Save/2 URL(因為這是表單發布到的 URL)。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-199">The downside with publishing two separate URLs is that in cases where we post to /Dinners/Save/2, and then need to redisplay the HTML form because of an input error, the end-user will end up having the /Dinners/Save/2 URL in their browser's address bar (since that was the URL the form posted to).</span></span> <span data-ttu-id="dc8c8-200">如果最終使用者將此重新顯示的頁面標記為其瀏覽器收藏夾清單,或將 URL 複製/貼上並透過電子郵件發送給朋友,則他們最終將保存將來無法工作的 URL(因為該 URL 取決於帖子值)。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-200">If the end-user bookmarks this redisplayed page to their browser favorites list, or copy/pastes the URL and emails it to a friend, they will end up saving a URL that won't work in the future (since that URL depends on post values).</span></span> <span data-ttu-id="dc8c8-201">通過公開單個 URL(如:/Dinners/Edit/[id])並通過 HTTP 謂詞區分其處理,最終使用者可以安全地為編輯頁面添加書籤和/或將 URL 發送給其他人。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-201">By exposing a single URL (like: /Dinners/Edit/[id]) and differentiating the processing of it by HTTP verb, it is safe for end-users to bookmark the edit page and/or send the URL to others.</span></span> |

#### <a name="retrieving-form-post-values"></a><span data-ttu-id="dc8c8-202">檢索表單過帳值</span><span class="sxs-lookup"><span data-stu-id="dc8c8-202">Retrieving Form Post Values</span></span>

<span data-ttu-id="dc8c8-203">我們可以通過多種方式訪問 HTTP POST"編輯" 方法中的已發布的表單參數。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-203">There are a variety of ways we can access posted form parameters within our HTTP POST "Edit" method.</span></span> <span data-ttu-id="dc8c8-204">一個簡單的方法是只使用 Controller 基數上的 Request 屬性來存取表單的值:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-204">One simple approach is to just use the Request property on the Controller base class to access the form collection and retrieve the posted values directly:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

<span data-ttu-id="dc8c8-205">不過,上述方法有點冗長,尤其是在添加錯誤處理邏輯後。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-205">The above approach is a little verbose, though, especially once we add error handling logic.</span></span>

<span data-ttu-id="dc8c8-206">此方案的更好方法是在控制器基類上利用內置*的 UpdateModel()* 説明器方法。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-206">A better approach for this scenario is to leverage the built-in *UpdateModel()* helper method on the Controller base class.</span></span> <span data-ttu-id="dc8c8-207">它支援更新使用傳入表單參數傳遞的物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-207">It supports updating the properties of an object we pass it using the incoming form parameters.</span></span> <span data-ttu-id="dc8c8-208">它使用反射來確定物件上的屬性名稱,然後根據用戶端提交的輸入值自動轉換和分配值。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-208">It uses reflection to determine the property names on the object, and then automatically converts and assigns values to them based on the input values submitted by the client.</span></span>

<span data-ttu-id="dc8c8-209">我們可以使用 UpdateModel() 方法使用此代碼簡化我們的 HTTP-POST 編輯操作:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-209">We could use the UpdateModel() method to simplify our HTTP-POST Edit Action using this code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

<span data-ttu-id="dc8c8-210">我們現在可以訪問 */Dinners/Edit/1* URL,並更改我們的晚餐標題:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-210">We can now visit the */Dinners/Edit/1* URL, and change the title of our Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

<span data-ttu-id="dc8c8-211">按下"保存"按鈕時,我們將執行"編輯"操作的表單帖子,更新的值將保留在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-211">When we click the "Save" button, we'll perform a form post to our Edit action, and the updated values will be persisted in the database.</span></span> <span data-ttu-id="dc8c8-212">然後,我們將重定向到晚餐的詳細資訊 URL(將顯示新保存的值):</span><span class="sxs-lookup"><span data-stu-id="dc8c8-212">We will then be redirected to the Details URL for the Dinner (which will display the newly saved values):</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a><span data-ttu-id="dc8c8-213">處理編輯錯誤</span><span class="sxs-lookup"><span data-stu-id="dc8c8-213">Handling Edit Errors</span></span>

<span data-ttu-id="dc8c8-214">我們當前的 HTTP-POST 實現工作正常,除非出現錯誤。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-214">Our current HTTP-POST implementation works fine – except when there are errors.</span></span>

<span data-ttu-id="dc8c8-215">當使用者在編輯表單時出錯時,我們需要確保表單重新顯示一條資訊性錯誤消息,以指導他們修復表單。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-215">When a user makes a mistake editing a form, we need to make sure that the form is redisplayed with an informative error message that guides them to fix it.</span></span> <span data-ttu-id="dc8c8-216">這包括最終使用者發佈不正確的輸入(例如:格式不正確的日期字串)的情況,以及輸入格式有效但存在業務規則衝突的情況。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-216">This includes cases where an end-user posts incorrect input (for example: a malformed date string), as well as cases where the input format is valid but there is a business rule violation.</span></span> <span data-ttu-id="dc8c8-217">發生錯誤時,窗體應保留使用者最初輸入的輸入數據,以便不必手動重新填充其更改。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-217">When errors occur the form should preserve the input data the user originally entered so that they don't have to refill their changes manually.</span></span> <span data-ttu-id="dc8c8-218">此過程應根據需要重複多次,直到表單成功完成。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-218">This process should repeat as many times as necessary until the form successfully completes.</span></span>

<span data-ttu-id="dc8c8-219">ASP.NET MVC 包含一些不錯的內置功能,使錯誤處理和表單重新顯示變得簡單。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-219">ASP.NET MVC includes some nice built-in features that make error handling and form redisplay easy.</span></span> <span data-ttu-id="dc8c8-220">要查看這些功能,讓我們使用以下代碼更新我們的 Edit 操作方法:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-220">To see these features in action let's update our Edit action method with the following code:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

<span data-ttu-id="dc8c8-221">上述代碼與之前的實現類似,只是我們現在正在將 try/catch 錯誤處理塊包裝在工作周圍。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-221">The above code is similar to our previous implementation – except that we are now wrapping a try/catch error handling block around our work.</span></span> <span data-ttu-id="dc8c8-222">如果在調用 UpdateModel() 時或嘗試保存 DinnerRepository 時出現異常(如果我們試圖保存的 Dinner 物件由於模型中的規則衝突而無效,則將引發異常),則將執行 catch 錯誤處理塊。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-222">If an exception occurs either when calling UpdateModel(), or when we try and save the DinnerRepository (which will raise an exception if the Dinner object we are trying to save is invalid because of a rule violation within our model), our catch error handling block will execute.</span></span> <span data-ttu-id="dc8c8-223">在其中,我們迴圈對「晚餐」物件中存在的任何規則衝突,並將其添加到 ModelState 對象(我們稍後將討論)。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-223">Within it we loop over any rule violations that exist in the Dinner object and add them to a ModelState object (which we'll discuss shortly).</span></span> <span data-ttu-id="dc8c8-224">然後,我們重新顯示視圖。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-224">We then redisplay the view.</span></span>

<span data-ttu-id="dc8c8-225">要看到這個工作,讓我們重新運行應用程式,編輯晚餐,並更改它有一個空的標題,事件日期的"BOGUS",並使用一個英國電話號碼與國家國家值的美國。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-225">To see this working let's re-run the application, edit a Dinner, and change it to have an empty Title, an EventDate of "BOGUS", and use a UK phone number with a country value of USA.</span></span> <span data-ttu-id="dc8c8-226">當我們按下「保存」按鈕時,我們的 HTTP POST 編輯方法將無法保存晚餐(因為存在錯誤),並將重新顯示該窗體:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-226">When we press the "Save" button our HTTP POST Edit method will not be able to save the Dinner (because there are errors) and will redisplay the form:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

<span data-ttu-id="dc8c8-227">我們的應用程式有一個體面的錯誤經驗。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-227">Our application has a decent error experience.</span></span> <span data-ttu-id="dc8c8-228">具有無效輸入的文本元素以紅色突出顯示,驗證錯誤消息向最終用戶顯示。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-228">The text elements with the invalid input are highlighted in red, and validation error messages are displayed to the end user about them.</span></span> <span data-ttu-id="dc8c8-229">該表單還保留使用者最初輸入的輸入數據,以便他們不必重新填充任何內容。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-229">The form is also preserving the input data the user originally entered – so that they don't have to refill anything.</span></span>

<span data-ttu-id="dc8c8-230">你可能會問,這是怎麼發生的?</span><span class="sxs-lookup"><span data-stu-id="dc8c8-230">How, you might ask, did this occur?</span></span> <span data-ttu-id="dc8c8-231">標題、事件日期和 ContactPhone 文字框如何以紅色突出顯示自己,並知道要輸出最初輸入的用戶值?</span><span class="sxs-lookup"><span data-stu-id="dc8c8-231">How did the Title, EventDate, and ContactPhone textboxes highlight themselves in red and know to output the originally entered user values?</span></span> <span data-ttu-id="dc8c8-232">錯誤訊息是如何顯示在頂部清單中的?</span><span class="sxs-lookup"><span data-stu-id="dc8c8-232">And how did error messages get displayed in the list at the top?</span></span> <span data-ttu-id="dc8c8-233">好消息是,這不是魔術造成的,而是因為我們使用了一些內置ASP.NET MVC 功能,使輸入驗證和錯誤處理方案變得容易。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-233">The good news is that this didn't occur by magic - rather it was because we used some of the built-in ASP.NET MVC features that make input validation and error handling scenarios easy.</span></span>

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a><span data-ttu-id="dc8c8-234">瞭解模型狀態與驗證 HTML 說明器方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-234">Understanding ModelState and the Validation HTML Helper Methods</span></span>

<span data-ttu-id="dc8c8-235">控制器類具有"ModelState"屬性集合,它提供了一種指示模型物件傳遞給 View 存在錯誤的方法。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-235">Controller classes have a "ModelState" property collection which provides a way to indicate that errors exist with a model object being passed to a View.</span></span> <span data-ttu-id="dc8c8-236">ModelState 集合中的錯誤條目標識具有問題的模型屬性的名稱(例如:"標題"、"事件日期"或"ContactPhone"),並允許指定人性化的錯誤消息(例如:"需要標題")。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-236">Error entries within the ModelState collection identify the name of the model property with the issue (for example: "Title", "EventDate", or "ContactPhone"), and allow a human-friendly error message to be specified (for example: "Title is required").</span></span>

<span data-ttu-id="dc8c8-237">*UpdateModel()* 幫助器方法在嘗試將窗體值分配給模型對象的屬性時遇到錯誤時自動填充模型狀態集合。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-237">The *UpdateModel()* helper method automatically populates the ModelState collection when it encounters errors while trying to assign form values to properties on the model object.</span></span> <span data-ttu-id="dc8c8-238">例如,我們的 Dinner 物件的 EventDate 屬性為「日期時間」類型。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-238">For example, our Dinner object's EventDate property is of type DateTime.</span></span> <span data-ttu-id="dc8c8-239">當 UpdateModel() 方法無法在上述方案中為其分配字串值「BOGUS」時,UpdateModel() 方法向 ModelState 集合添加了一個條目,指示該屬性發生了賦值錯誤。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-239">When the UpdateModel() method was unable to assign the string value "BOGUS" to it in the scenario above, the UpdateModel() method added an entry to the ModelState collection indicating an assignment error had occurred with that property.</span></span>

<span data-ttu-id="dc8c8-240">開發人員還可以編寫代碼,將錯誤條目顯式添加到 ModelState 集合中,就像我們在下面的"catch"錯誤處理塊中所做的一樣,該塊基於"晚餐"物件中的活動規則衝突填充了 ModelState 集合:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-240">Developers can also write code to explicitly add error entries into the ModelState collection like we are doing below within our "catch" error handling block, which is populating the ModelState collection with entries based on the active Rule Violations in the Dinner object:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a><span data-ttu-id="dc8c8-241">HTML 說明器與模型狀態</span><span class="sxs-lookup"><span data-stu-id="dc8c8-241">Html Helper Integration with ModelState</span></span>

<span data-ttu-id="dc8c8-242">HTML 說明器方法(如 Html.TextBox() ) - 在呈現輸出時選中 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-242">HTML helper methods - like Html.TextBox() - check the ModelState collection when rendering output.</span></span> <span data-ttu-id="dc8c8-243">如果項存在錯誤,則呈現使用者輸入的值和 CSS 錯誤類。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-243">If an error for the item exists, they render the user-entered value and a CSS error class.</span></span>

<span data-ttu-id="dc8c8-244">例如,在我們的「編輯」檢視中,我們使用 Html.TextBox() 説明器方法來呈現晚餐物件的事件日期:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-244">For example, in our "Edit" view we are using the Html.TextBox() helper method to render the EventDate of our Dinner object:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

<span data-ttu-id="dc8c8-245">在錯誤方案中呈現檢視時,Html.TextBox() 方法檢查了 ModelState 集合,以查看是否存在與 Dinner 物件的「EventDate」屬性關聯的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-245">When the view was rendered in the error scenario, the Html.TextBox() method checked the ModelState collection to see if there were any errors associated with the "EventDate" property of our Dinner object.</span></span> <span data-ttu-id="dc8c8-246">當它確定存在錯誤時,它呈現提交的使用者輸入(「BOGUS」)作為值,並將 css 錯誤類別&lt;新增到 它產生的輸入類型="textbox"/&gt;標記:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-246">When it determined that there was an error it rendered the submitted user input ("BOGUS") as the value, and added a css error class to the &lt;input type="textbox"/&gt; markup it generated:</span></span>

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

<span data-ttu-id="dc8c8-247">您可以自定義 css 錯誤類的外觀,以按所需時間查看。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-247">You can customize the appearance of the css error class to look however you want.</span></span> <span data-ttu-id="dc8c8-248">預設 CSS 錯誤類別 ( "輸入認證-錯誤' ) 在 *_content_site.css*樣式表中定義,如下所示:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-248">The default CSS error class – "input-validation-error" – is defined in the *\content\site.css* stylesheet and looks like below:</span></span>

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

<span data-ttu-id="dc8c8-249">此 CSS 規則導致無效輸入元素突出顯示的原因如下:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-249">This CSS rule is what caused our invalid input elements to be highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a><span data-ttu-id="dc8c8-250">HTML.驗證訊息() 說明器方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-250">Html.ValidationMessage() Helper Method</span></span>

<span data-ttu-id="dc8c8-251">HTML.驗證訊息() 說明器方法可用於輸出與特定模型屬性關聯的 ModelState 錯誤訊息:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-251">The Html.ValidationMessage() helper method can be used to output the ModelState error message associated with a particular model property:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

<span data-ttu-id="dc8c8-252">上述代碼輸出:*&lt;跨類別=「欄位驗證錯誤&gt;」 值「BOGUS」無效&lt;/跨&gt;*</span><span class="sxs-lookup"><span data-stu-id="dc8c8-252">The above code outputs: *&lt;span class="field-validation-error"&gt; The value ‘BOGUS' is invalid&lt;/span&gt;*</span></span>

<span data-ttu-id="dc8c8-253">HTML.驗證訊息() 說明器方法支援第二個參數,該參數允許開發人員重寫顯示的錯誤文本訊息:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-253">The Html.ValidationMessage() helper method also supports a second parameter that allows developers to override the error text message that is displayed:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

<span data-ttu-id="dc8c8-254">上述代碼輸出:*&lt;跨類="欄位驗證-錯誤"/span,&gt;\*&lt;&gt;* 而不是當 EventDate 屬性存在錯誤時,而不是默認錯誤文本。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-254">The above code outputs: *&lt;span class="field-validation-error"&gt;\*&lt;/span&gt;* instead of the default error text when an error is present for the EventDate property.</span></span>

##### <a name="htmlvalidationsummary-helper-method"></a><span data-ttu-id="dc8c8-255">HTML.驗證摘要() 說明器方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-255">Html.ValidationSummary() Helper Method</span></span>

<span data-ttu-id="dc8c8-256">HTML.驗證摘要() 說明程式方法可用於呈現摘要錯誤訊息,並附帶 ModelState&lt;&gt;&lt;集合中&gt;&lt;所有&gt;詳細錯誤訊息 的 ul li//ul 清單:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-256">The Html.ValidationSummary() helper method can be used to render a summary error message, accompanied by a &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; list of all detailed error messages in the ModelState collection:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

<span data-ttu-id="dc8c8-257">HTML.驗證摘要() 說明程式方法採用可選字串參數 , 它定義摘要錯誤訊息,以顯示在詳細錯誤清單的上方:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-257">The Html.ValidationSummary() helper method takes an optional string parameter – which defines a summary error message to display above the list of detailed errors:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

<span data-ttu-id="dc8c8-258">您可以選擇使用 CSS 來覆蓋錯誤列表的外觀。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-258">You can optionally use CSS to override what the error list looks like.</span></span>

#### <a name="using-a-addruleviolations-helper-method"></a><span data-ttu-id="dc8c8-259">使用新增規則衝突說明程式方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-259">Using a AddRuleViolations Helper Method</span></span>

<span data-ttu-id="dc8c8-260">我們的初始 HTTP-POST 編輯實現使用 catch 塊中的 foreach 語句來迴圈訪問 Dinner 物件的「規則衝突」,並將它們添加到控制器的 ModelState 集合中:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-260">Our initial HTTP-POST Edit implementation used a foreach statement within its catch block to loop over the Dinner object's Rule Violations and add them to the controller's ModelState collection:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

<span data-ttu-id="dc8c8-261">通過將「控制器幫助器」類添加到NerdDinner專案中,並在其中實現「AddRuleRule衝突」擴充方法,將説明器方法添加到ASP.NET MVC ModelState字典類,我們可以使此代碼更簡潔一些。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-261">We can make this code a little cleaner by adding a "ControllerHelpers" class to the NerdDinner project, and implement an "AddRuleViolations" extension method within it that adds a helper method to the ASP.NET MVC ModelStateDictionary class.</span></span> <span data-ttu-id="dc8c8-262">此擴充方法可以使用規則衝突錯誤清單封裝填充 ModelState字典所需的邏輯:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-262">This extension method can encapsulate the logic necessary to populate the ModelStateDictionary with a list of RuleViolation errors:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

<span data-ttu-id="dc8c8-263">然後,我們可以更新我們的 HTTP-POST 編輯操作方法,以使用此擴展方法使用我們的晚餐規則衝突填充 ModelState 集合。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-263">We can then update our HTTP-POST Edit action method to use this extension method to populate the ModelState collection with our Dinner Rule Violations.</span></span>

#### <a name="complete-edit-action-method-implementations"></a><span data-ttu-id="dc8c8-264">完整的編輯操作方法實現</span><span class="sxs-lookup"><span data-stu-id="dc8c8-264">Complete Edit Action Method Implementations</span></span>

<span data-ttu-id="dc8c8-265">以下代碼實現了編輯方案所需的控制器邏輯:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-265">The code below implements all of the controller logic necessary for our Edit scenario:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

<span data-ttu-id="dc8c8-266">我們的 Edit 實現好處是,我們的 Controller 類和 View 範本都不需要瞭解我們的 Dinner 模型正在強制執行的特定驗證或業務規則。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-266">The nice thing about our Edit implementation is that neither our Controller class nor our View template has to know anything about the specific validation or business rules being enforced by our Dinner model.</span></span> <span data-ttu-id="dc8c8-267">將來,我們可以向模型添加其他規則,並且不必對我們的控制器或視圖進行任何代碼更改,以便支援這些規則。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-267">We can add additional rules to our model in the future and do not have to make any code changes to our controller or view in order for them to be supported.</span></span> <span data-ttu-id="dc8c8-268">這為我們提供了靈活性,以便在未來以最少的代碼更改輕鬆發展我們的應用程式需求。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-268">This provides us with the flexibility to easily evolve our application requirements in the future with a minimum of code changes.</span></span>

### <a name="create-support"></a><span data-ttu-id="dc8c8-269">建立支援</span><span class="sxs-lookup"><span data-stu-id="dc8c8-269">Create Support</span></span>

<span data-ttu-id="dc8c8-270">我們已經完成了晚餐控制器類的"編輯"行為。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-270">We've finished implementing the "Edit" behavior of our DinnersController class.</span></span> <span data-ttu-id="dc8c8-271">現在,讓我們繼續實現其上的"創建"支援-這將使用戶能夠添加新的晚餐。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-271">Let's now move on to implement the "Create" support on it – which will enable users to add new Dinners.</span></span>

#### <a name="the-http-get-create-action-method"></a><span data-ttu-id="dc8c8-272">HTTP-GET 建立操作方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-272">The HTTP-GET Create Action Method</span></span>

<span data-ttu-id="dc8c8-273">我們將首先實現創建操作方法的 HTTP"GET"行為。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-273">We'll begin by implementing the HTTP "GET" behavior of our create action method.</span></span> <span data-ttu-id="dc8c8-274">當有人訪問 */Dinners/創建*URL 時,將調用此方法。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-274">This method will be called when someone visits the */Dinners/Create* URL.</span></span> <span data-ttu-id="dc8c8-275">我們的實現如下所示:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-275">Our implementation looks like:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

<span data-ttu-id="dc8c8-276">上面的代碼將創建一個新的 Dinner 物件,並將其事件日期屬性分配為將來一周。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-276">The code above creates a new Dinner object, and assigns its EventDate property to be one week in the future.</span></span> <span data-ttu-id="dc8c8-277">然後,它呈現基於新"晚餐"對象的視圖。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-277">It then renders a View that is based on the new Dinner object.</span></span> <span data-ttu-id="dc8c8-278">由於我們尚未顯式將名稱傳遞給*View()* 幫助器方法,它將使用基於約定的預設路徑來解決視圖範本:/視圖/Dinners/Create.aspx。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-278">Because we haven't explicitly passed a name to the *View()* helper method, it will use the convention based default path to resolve the view template: /Views/Dinners/Create.aspx.</span></span>

<span data-ttu-id="dc8c8-279">現在,讓我們創建此視圖範本。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-279">Let's now create this view template.</span></span> <span data-ttu-id="dc8c8-280">我們可以在"創建操作"方法中右鍵按一下並選擇"添加檢視"上下文選單命令來執行此操作。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-280">We can do this by right-clicking within the Create action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="dc8c8-281">在「添加檢視」對話框中,我們將指示我們將將 Dinner 物件傳遞到檢視範本,並選擇自動基腳手架「創建」範本:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-281">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to the view template, and choose to auto-scaffold a "Create" template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

<span data-ttu-id="dc8c8-282">按下「添加」按鈕時,Visual Studio 會將基於腳手架的新「Create.aspx」視圖保存到「_Views_Dinners」目錄,並在 IDE 中將其打開:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-282">When we click the "Add" button, Visual Studio will save a new scaffold-based "Create.aspx" view to the "\Views\Dinners" directory, and open it up within the IDE:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

<span data-ttu-id="dc8c8-283">讓我們對為我們生成的預設「創建」基架檔進行一些更改,並將其修改為如下所示:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-283">Let's make a few changes to the default "create" scaffold file that was generated for us, and modify it up to look like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

<span data-ttu-id="dc8c8-284">現在,當我們運行應用程式並訪問瀏覽器中的 *「/Dinner/Create」URL*時,它將從我們的「創建操作」實現中呈現如下 UI:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-284">And now when we run our application and access the *"/Dinners/Create"* URL within the browser it will render UI like below from our Create action implementation:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a><span data-ttu-id="dc8c8-285">完整式 HTTP-POST 建立操作方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-285">Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="dc8c8-286">我們實現了"創建操作方法"的 HTTP-GET 版本。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-286">We have the HTTP-GET version of our Create action method implemented.</span></span> <span data-ttu-id="dc8c8-287">當使用者按下「儲存」按鈕時,它會執行表單發布到 */Dinners/Create* URL,並使用 HTTP&lt;POST 謂詞 提交&gt;HTML 輸入表單值。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-287">When a user clicks the "Save" button it performs a form post to the */Dinners/Create* URL, and submits the HTML &lt;input&gt; form values using the HTTP POST verb.</span></span>

<span data-ttu-id="dc8c8-288">現在,讓我們實現創建操作方法的 HTTP POST 行為。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-288">Let's now implement the HTTP POST behavior of our create action method.</span></span> <span data-ttu-id="dc8c8-289">我們將首先向 DinnersController 添加一個重載的「創建」操作方法,該控制器上具有「AcceptVerbs」屬性,指示它處理 HTTP POST 方案:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-289">We'll begin by adding an overloaded "Create" action method to our DinnersController that has an "AcceptVerbs" attribute on it that indicates it handles HTTP POST scenarios:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

<span data-ttu-id="dc8c8-290">我們可以通過多種方式訪問啟用 HTTP-POST 的"創建"方法中的已過帳表單參數。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-290">There are a variety of ways we can access the posted form parameters within our HTTP-POST enabled "Create" method.</span></span>

<span data-ttu-id="dc8c8-291">一種方法是創建新的 Dinner 物件,然後使用*UpdateModel()* 説明器方法(就像我們使用"編輯"操作所做的那樣)使用張貼的表單值填充它。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-291">One approach is to create a new Dinner object and then use the *UpdateModel()* helper method (like we did with the Edit action) to populate it with the posted form values.</span></span> <span data-ttu-id="dc8c8-292">然後,我們可以將其添加到 DinnerRepository 中,將其儲存到資料庫中,並將使用者重定向到「詳細資訊」操作,以便使用以下代碼顯示新創建的 Dinner:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-292">We can then add it to our DinnerRepository, persist it to the database, and redirect the user to our Details action to show the newly created Dinner using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

<span data-ttu-id="dc8c8-293">或者,我們可以使用一種方法,其中我們的 Create() 操作方法將 Dinner 物件作為方法參數。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-293">Alternatively, we can use an approach where we have our Create() action method take a Dinner object as a method parameter.</span></span> <span data-ttu-id="dc8c8-294">然後ASP.NET MVC 將自動為我們實例化新的 Dinner 物件,使用表單輸入填充其屬性,並將其傳遞給我們的操作方法:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-294">ASP.NET MVC will then automatically instantiate a new Dinner object for us, populate its properties using the form inputs, and pass it to our action method:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

<span data-ttu-id="dc8c8-295">上述操作方法通過檢查 ModelState.IsValid 屬性,驗證 Dinner 物件已成功填充表單後值。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-295">Our action method above verifies that the Dinner object has been successfully populated with the form post values by checking the ModelState.IsValid property.</span></span> <span data-ttu-id="dc8c8-296">如果存在輸入轉換問題(例如:EventDate 屬性的"BOGUS"字串),並且有任何問題,我們的操作方法將重新顯示窗體,則返回 false。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-296">This will return false if there are input conversion issues (for example: a string of "BOGUS" for the EventDate property), and if there are any issues our action method redisplays the form.</span></span>

<span data-ttu-id="dc8c8-297">如果輸入值有效,則操作方法將嘗試將新 Dinner 添加到 DinnerRepository 中。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-297">If the input values are valid, then the action method attempts to add and save the new Dinner to the DinnerRepository.</span></span> <span data-ttu-id="dc8c8-298">它將這項工作包裝在 try/catch 塊中,如果有任何違反業務規則的行為(這將導致晚餐存儲庫.Save() 方法引發異常,則重新顯示表單。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-298">It wraps this work within a try/catch block and redisplays the form if there are any business rule violations (which would cause the dinnerRepository.Save() method to raise an exception).</span></span>

<span data-ttu-id="dc8c8-299">要查看此錯誤處理行為是否在起作用,我們可以請求 */Dinners/Create* URL 並填寫有關新晚餐的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-299">To see this error handling behavior in action, we can request the */Dinners/Create* URL and fill out details about a new Dinner.</span></span> <span data-ttu-id="dc8c8-300">輸入或值不正確將導致重新顯示建立窗體,並突出顯示錯誤如下:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-300">Incorrect input or values will cause the create form to be redisplayed with the errors highlighted like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

<span data-ttu-id="dc8c8-301">請注意,我們的"創建"表單如何遵守與"編輯"表單完全相同的驗證和業務規則。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-301">Notice how our Create form is honoring the exact same validation and business rules as our Edit form.</span></span> <span data-ttu-id="dc8c8-302">這是因為我們的驗證和業務規則是在模型中定義的,並且未嵌入到應用程式的 UI 或控制器中。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-302">This is because our validation and business rules were defined in the model, and were not embedded within the UI or controller of the application.</span></span> <span data-ttu-id="dc8c8-303">這意味著我們以後可以在一個位置更改/發展我們的驗證或業務規則,並在整個應用程式中應用這些規則。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-303">This means we can later change/evolve our validation or business rules in a single place and have them apply throughout our application.</span></span> <span data-ttu-id="dc8c8-304">我們不必更改"編輯"或"創建操作方法"中的任何代碼,即可自動遵守任何新規則或對現有規則的修改。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-304">We will not have to change any code within either our Edit or Create action methods to automatically honor any new rules or modifications to existing ones.</span></span>

<span data-ttu-id="dc8c8-305">當我們修復輸入值並再次按下"保存"按鈕時,我們添加到 DinnerRepository 將成功,並且將添加新的 Dinner 添加到資料庫中。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-305">When we fix the input values and click the "Save" button again, our addition to the DinnerRepository will succeed, and a new Dinner will be added to the database.</span></span> <span data-ttu-id="dc8c8-306">然後,我們將重定向到 */Dinners/詳細資訊/[id]* URL - 我們將向這裡介紹有關新創建的晚餐的詳細資訊:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-306">We will then be redirected to the */Dinners/Details/[id]* URL – where we will be presented with details about the newly created Dinner:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a><span data-ttu-id="dc8c8-307">移除支援</span><span class="sxs-lookup"><span data-stu-id="dc8c8-307">Delete Support</span></span>

<span data-ttu-id="dc8c8-308">現在,讓我們向"刪除"支援添加到我們的晚餐控制器。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-308">Let's now add "Delete" support to our DinnersController.</span></span>

#### <a name="the-http-get-delete-action-method"></a><span data-ttu-id="dc8c8-309">HTTP-GET 移除操作方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-309">The HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="dc8c8-310">我們將首先實現刪除操作方法的 HTTP GET 行為。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-310">We'll begin by implementing the HTTP GET behavior of our delete action method.</span></span> <span data-ttu-id="dc8c8-311">當有人訪問 */Dinners/Delete/[id]* URL 時,將調用此方法。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-311">This method will get called when someone visits the */Dinners/Delete/[id]* URL.</span></span> <span data-ttu-id="dc8c8-312">以下是實現:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-312">Below is the implementation:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

<span data-ttu-id="dc8c8-313">操作方法嘗試檢索要刪除的"晚餐"。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-313">The action method attempts to retrieve the Dinner to be deleted.</span></span> <span data-ttu-id="dc8c8-314">如果「晚餐」存在,則根據「晚餐」對象呈現視圖。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-314">If the Dinner exists it renders a View based on the Dinner object.</span></span> <span data-ttu-id="dc8c8-315">如果物件不存在(或已被刪除),它將返回一個視圖,該視圖呈現了我們之前為"詳細資訊"操作方法創建的"NotFound"視圖範本。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-315">If the object doesn't exist (or has already been deleted) it returns a View that renders the "NotFound" view template we created earlier for our "Details" action method.</span></span>

<span data-ttu-id="dc8c8-316">我們可以在「刪除操作」方法中右鍵按一下並選擇「添加檢視」 上下文選單命令來創建「刪除」檢視範本。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-316">We can create the "Delete" view template by right-clicking within the Delete action method and selecting the "Add View" context menu command.</span></span> <span data-ttu-id="dc8c8-317">在「添加檢視」對話框中,我們將指示我們將將 Dinner 物件作為模型傳遞給視圖範本,並選擇創建空範本:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-317">Within the "Add View" dialog we'll indicate that we are passing a Dinner object to our view template as its model, and choose to create an empty template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

<span data-ttu-id="dc8c8-318">當我們按下「添加」按鈕時,Visual Studio 將在「@Views_Dinners」目錄中為我們添加新的」Delete.aspx「視圖範本檔。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-318">When we click the "Add" button, Visual Studio will add a new "Delete.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="dc8c8-319">我們將向樣本新增一些 HTML 和代碼,以實現如下刪除確認螢幕:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-319">We'll add some HTML and code to the template to implement a delete confirmation screen like below:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

<span data-ttu-id="dc8c8-320">上面的代碼顯示要刪除的 Dinner 的標題,並在最終使用者按下其中的&lt;「&gt;刪除」 按鈕時輸出對 /Dinners/Delete/[id] URL 執行 POST 的表單元素。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-320">The code above displays the title of the Dinner to be deleted, and outputs a &lt;form&gt; element that does a POST to the /Dinners/Delete/[id] URL if the end-user clicks the "Delete" button within it.</span></span>

<span data-ttu-id="dc8c8-321">當我們運行應用程式並造訪有效 Dinner 物件的 *"/晚餐/刪除/[id]"URL*時,它將呈現如下 UI:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-321">When we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it renders UI like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| <span data-ttu-id="dc8c8-322">**側主題:我們為什麼要進行 POST?**</span><span class="sxs-lookup"><span data-stu-id="dc8c8-322">**Side Topic: Why are we doing a POST?**</span></span> |
| --- |
| <span data-ttu-id="dc8c8-323">您可能會問 – 我們為什麼要在"刪除"確認&lt;螢幕&gt;中 創建 表單?</span><span class="sxs-lookup"><span data-stu-id="dc8c8-323">You might ask – why did we go through the effort of creating a &lt;form&gt; within our Delete confirmation screen?</span></span> <span data-ttu-id="dc8c8-324">為什麼不只使用標準超連結連結到執行實際刪除操作的操作方法?</span><span class="sxs-lookup"><span data-stu-id="dc8c8-324">Why not just use a standard hyperlink to link to an action method that does the actual delete operation?</span></span> <span data-ttu-id="dc8c8-325">原因是,我們希望小心防範 Web 爬網者和搜尋引擎發現我們的 URL,並在跟蹤連結時無意中導致數據被刪除。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-325">The reason is because we want to be careful to guard against web-crawlers and search engines discovering our URLs and inadvertently causing data to be deleted when they follow the links.</span></span> <span data-ttu-id="dc8c8-326">基於 HTTP-GET 的 URL 被視為「安全」的 URL,它們可以訪問/爬網,並且它們不應遵循 HTTP-POST URL。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-326">HTTP-GET based URLs are considered "safe" for them to access/crawl, and they are supposed to not follow HTTP-POST ones.</span></span> <span data-ttu-id="dc8c8-327">一個好的規則是確保您始終將破壞性或數據修改操作放在 HTTP-POST 請求後面。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-327">A good rule is to make sure you always put destructive or data modifying operations behind HTTP-POST requests.</span></span> |

#### <a name="implementing-the-http-post-delete-action-method"></a><span data-ttu-id="dc8c8-328">完整或 HTTP-POST 移除操作方法</span><span class="sxs-lookup"><span data-stu-id="dc8c8-328">Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="dc8c8-329">現在,我們實現了 HTTP-GET 版本的刪除操作方法,顯示刪除確認螢幕。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-329">We now have the HTTP-GET version of our Delete action method implemented which displays a delete confirmation screen.</span></span> <span data-ttu-id="dc8c8-330">當最終使用者按下「刪除」按鈕時,它將執行表單發布到 */Dinners/Dinner/[id]* URL。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-330">When an end user clicks the "Delete" button it will perform a form post to the */Dinners/Dinner/[id]* URL.</span></span>

<span data-ttu-id="dc8c8-331">現在,讓我們使用以下代碼實現刪除操作方法的 HTTP「POST」行為:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-331">Let's now implement the HTTP "POST" behavior of the delete action method using the code below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

<span data-ttu-id="dc8c8-332">HTTP-POST 版本的"刪除"操作方法嘗試檢索要刪除的晚餐物件。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-332">The HTTP-POST version of our Delete action method attempts to retrieve the dinner object to delete.</span></span> <span data-ttu-id="dc8c8-333">如果找不到它(因為它已被刪除),它將呈現我們的"未找到"範本。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-333">If it can't find it (because it has already been deleted) it renders our "NotFound" template.</span></span> <span data-ttu-id="dc8c8-334">如果它找到晚餐,它會從晚餐存儲庫中刪除它。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-334">If it finds the Dinner, it deletes it from the DinnerRepository.</span></span> <span data-ttu-id="dc8c8-335">然後,它呈現一個"已刪除"範本。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-335">It then renders a "Deleted" template.</span></span>

<span data-ttu-id="dc8c8-336">要實現"已刪除"範本,我們將在操作方法中右鍵單擊並選擇"添加視圖"上下文菜單。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-336">To implement the "Deleted" template we'll right-click in the action method and choose the "Add View" context menu.</span></span> <span data-ttu-id="dc8c8-337">我們將檢視命名為"已刪除",並將其命名為空範本(而不是採用強類型模型物件)。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-337">We'll name our view "Deleted" and have it be an empty template (and not take a strongly-typed model object).</span></span> <span data-ttu-id="dc8c8-338">然後,我們將向其中添加一些 HTML 內容:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-338">We'll then add some HTML content to it:</span></span>

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

<span data-ttu-id="dc8c8-339">現在,當我們運行我們的應用程式,並訪問有效的晚餐物件的 *"/晚餐/刪除/[id]"URL*時,它將呈現我們的晚餐刪除確認螢幕,如下所示:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-339">And now when we run our application and access the *"/Dinners/Delete/[id]"* URL for a valid Dinner object it will render our Dinner delete confirmation screen like below:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

<span data-ttu-id="dc8c8-340">當我們按下「刪除」按鈕時,它將對 */Dinners/Delete/[id]* URL 執行 HTTP-POST,這將從我們的資料庫中刪除晚餐,並顯示我們的「已刪除」視圖範本:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-340">When we click the "Delete" button it will perform an HTTP-POST to the */Dinners/Delete/[id]* URL, which will delete the Dinner from our database, and display our "Deleted" view template:</span></span>

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a><span data-ttu-id="dc8c8-341">模型繫結安全性</span><span class="sxs-lookup"><span data-stu-id="dc8c8-341">Model Binding Security</span></span>

<span data-ttu-id="dc8c8-342">我們討論了使用ASP.NET MVC 的內建模型綁定功能的兩種不同的方法。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-342">We've discussed two different ways to use the built-in model-binding features of ASP.NET MVC.</span></span> <span data-ttu-id="dc8c8-343">第一個使用 UpdateModel() 方法更新現有模型物件的屬性,第二個使用 ASP.NET mVC 支援將模型物件作為操作方法參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-343">The first using the UpdateModel() method to update properties on an existing model object, and the second using ASP.NET MVC's support for passing model objects in as action method parameters.</span></span> <span data-ttu-id="dc8c8-344">這兩種技術都非常強大,非常有用。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-344">Both of these techniques are very powerful and extremely useful.</span></span>

<span data-ttu-id="dc8c8-345">這種力量也帶來了責任。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-345">This power also brings with it responsibility.</span></span> <span data-ttu-id="dc8c8-346">在接受任何用戶輸入時,始終對安全性持偏執狀態很重要,在綁定物件以形成輸入時也是如此。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-346">It is important to always be paranoid about security when accepting any user input, and this is also true when binding objects to form input.</span></span> <span data-ttu-id="dc8c8-347">您應該始終小心 HTML 編碼任何使用者輸入的值,以避免 HTML 和 JavaScript 注入攻擊,並小心 SQL 注入攻擊(請注意:我們使用 LINQ 到 SQL 作為應用程式,它會自動對參數進行編碼,以防止這些類型的攻擊)。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-347">You should be careful to always HTML encode any user-entered values to avoid HTML and JavaScript injection attacks, and be careful of SQL injection attacks (note: we are using LINQ to SQL for our application, which automatically encodes parameters to prevent these types of attacks).</span></span> <span data-ttu-id="dc8c8-348">您絕不應僅依賴客戶端驗證,並且始終使用伺服器端驗證來防止駭客試圖向您發送虛假值。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-348">You should never rely on client-side validation alone, and always employ server-side validation to guard against hackers attempting to send you bogus values.</span></span>

<span data-ttu-id="dc8c8-349">使用 ASP.NET MVC 的綁定功能時,要確保考慮的另一個安全項是綁定物件的範圍。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-349">One additional security item to make sure you think about when using the binding features of ASP.NET MVC is the scope of the objects you are binding.</span></span> <span data-ttu-id="dc8c8-350">具體來說,您希望確保您瞭解允許綁定的屬性的安全含義,並確保僅允許最終使用者更新真正應該更新的屬性。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-350">Specifically, you want to make sure you understand the security implications of the properties you are allowing to be bound, and make sure you only allow those properties that really should be updatable by an end-user to be updated.</span></span>

<span data-ttu-id="dc8c8-351">默認情況下,UpdateModel() 方法將嘗試更新模型物件上與傳入窗體參數值匹配的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-351">By default, the UpdateModel() method will attempt to update all properties on the model object that match incoming form parameter values.</span></span> <span data-ttu-id="dc8c8-352">同樣,默認情況下作為操作方法參數傳遞的物件可以通過窗體參數設置其所有屬性。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-352">Likewise, objects passed as action method parameters also by default can have all of their properties set via form parameters.</span></span>

#### <a name="locking-down-binding-on-a-per-usage-basis"></a><span data-ttu-id="dc8c8-353">依使用方式鎖定繫結</span><span class="sxs-lookup"><span data-stu-id="dc8c8-353">Locking down binding on a per-usage basis</span></span>

<span data-ttu-id="dc8c8-354">通過提供可更新的屬性的顯式"包含清單",可以按使用方式鎖定綁定策略。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-354">You can lock down the binding policy on a per-usage basis by providing an explicit "include list" of properties that can be updated.</span></span> <span data-ttu-id="dc8c8-355">這可以通過將額外的字串陣列參數傳遞給 UpdateModel() 方法來實現,如下所示:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-355">This can be done by passing an extra string array parameter to the UpdateModel() method like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

<span data-ttu-id="dc8c8-356">作為操作方法參數傳遞的物件還支援 [Bind] 屬性,該屬性允許如下指定允許屬性的「包含清單」:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-356">Objects passed as action method parameters also support a [Bind] attribute that enables an "include list" of allowed properties to be specified like below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a><span data-ttu-id="dc8c8-357">在類型上鎖定繫結</span><span class="sxs-lookup"><span data-stu-id="dc8c8-357">Locking down binding on a type basis</span></span>

<span data-ttu-id="dc8c8-358">您還可以按類型鎖定綁定規則。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-358">You can also lock down the binding rules on a per-type basis.</span></span> <span data-ttu-id="dc8c8-359">這允許您指定綁定規則一次,然後將它們應用於所有控制器和操作方法的所有方案(包括 UpdateModel 和操作方法參數方案)。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-359">This allows you to specify the binding rules once, and then have them apply in all scenarios (including both UpdateModel and action method parameter scenarios) across all controllers and action methods.</span></span>

<span data-ttu-id="dc8c8-360">您可以通過將 [Bind] 屬性添加到類型上,或透過在應用程式的 Global.asax 檔中註冊來自定義每種類型的綁定規則(對於您不擁有該類型的方案非常有用)。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-360">You can customize the per-type binding rules by adding a [Bind] attribute onto a type, or by registering it within the Global.asax file of the application (useful for scenarios where you don't own the type).</span></span> <span data-ttu-id="dc8c8-361">然後,可以使用 Bind 屬性的「包含」和「排除」屬性來控制特定類或介面可綁定哪些屬性。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-361">You can then use the Bind attribute's Include and Exclude properties to control which properties are bindable for the particular class or interface.</span></span>

<span data-ttu-id="dc8c8-362">我們將在NerdDinner應用程式中對Dinner類使用此技術,並為其添加 [Bind] 屬性,將可綁定屬性清單限制為以下內容:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-362">We'll use this technique for the Dinner class in our NerdDinner application, and add a [Bind] attribute to it that restricts the list of bindable properties to the following:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

<span data-ttu-id="dc8c8-363">請注意,我們不允許通過綁定操作 RSSP 集合,也不允許通過綁定設置 DinnerID 或託管比屬性。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-363">Notice we are not allowing the RSVPs collection to be manipulated via binding, nor are we allowing the DinnerID or HostedBy properties to be set via binding.</span></span> <span data-ttu-id="dc8c8-364">出於安全原因,我們將只使用操作方法中的顯式代碼來操作這些特定屬性。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-364">For security reasons we'll instead only manipulate these particular properties using explicit code within our action methods.</span></span>

### <a name="crud-wrap-up"></a><span data-ttu-id="dc8c8-365">CRUD 總結</span><span class="sxs-lookup"><span data-stu-id="dc8c8-365">CRUD Wrap-Up</span></span>

<span data-ttu-id="dc8c8-366">ASP.NET MVC 包含許多內置功能,可幫助實現表單發布方案。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-366">ASP.NET MVC includes a number of built-in features that help with implementing form posting scenarios.</span></span> <span data-ttu-id="dc8c8-367">我們使用多種功能在晚餐存儲庫上提供 CRUD UI 支援。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-367">We used a variety of these features to provide CRUD UI support on top of our DinnerRepository.</span></span>

<span data-ttu-id="dc8c8-368">我們使用以模型為中心的方法來實現我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-368">We are using a model-focused approach to implement our application.</span></span> <span data-ttu-id="dc8c8-369">這意味著我們所有的驗證和業務規則邏輯都在我們的模型層中定義,而不是在我們的控制器或視圖中定義。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-369">This means that all our validation and business rule logic is defined within our model layer – and not within our controllers or views.</span></span> <span data-ttu-id="dc8c8-370">我們的 Controller 類和 View 範本都不知道我們的 Dinner 模型類正在強制執行的特定業務規則。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-370">Neither our Controller class nor our View templates know anything about the specific business rules being enforced by our Dinner model class.</span></span>

<span data-ttu-id="dc8c8-371">這將保持我們的應用程序體系結構清潔,並使其更易於測試。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-371">This will keep our application architecture clean and make it easier to test.</span></span> <span data-ttu-id="dc8c8-372">將來,我們可以向模型層添加其他業務規則,而不必對我們的控制器或視圖*進行任何代碼更改*,以便支援這些規則。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-372">We can add additional business rules to our model layer in the future and *not have to make any code changes* to our Controller or View in order for them to be supported.</span></span> <span data-ttu-id="dc8c8-373">這將為我們提供極大的敏捷性,以便我們在未來發展和改變我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-373">This is going to provide us with a great deal of agility to evolve and change our application in the future.</span></span>

<span data-ttu-id="dc8c8-374">我們的晚餐控制器現在啟用晚餐列表/詳細資訊,以及創建、編輯和刪除支援。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-374">Our DinnersController now enables Dinner listings/details, as well as create, edit and delete support.</span></span> <span data-ttu-id="dc8c8-375">類別的完整代碼如下所示:</span><span class="sxs-lookup"><span data-stu-id="dc8c8-375">The complete code for the class can be found below:</span></span>

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a><span data-ttu-id="dc8c8-376">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc8c8-376">Next Step</span></span>

<span data-ttu-id="dc8c8-377">現在,我們的 DinnersController 類中實現了基本的 CRUD(創建、讀取、更新和刪除)支援。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-377">We now have basic CRUD (Create, Read, Update and Delete) support implement within our DinnersController class.</span></span>

<span data-ttu-id="dc8c8-378">現在,讓我們來看看如何使用 ViewData 和 ViewModel 類在我們的窗體上啟用更豐富的 UI。</span><span class="sxs-lookup"><span data-stu-id="dc8c8-378">Let's now look at how we can use ViewData and ViewModel classes to enable even richer UI on our forms.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dc8c8-379">[前一個](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [下一個](use-viewdata-and-implement-viewmodel-classes.md)</span><span class="sxs-lookup"><span data-stu-id="dc8c8-379">[Previous](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
[Next](use-viewdata-and-implement-viewmodel-classes.md)</span></span>
