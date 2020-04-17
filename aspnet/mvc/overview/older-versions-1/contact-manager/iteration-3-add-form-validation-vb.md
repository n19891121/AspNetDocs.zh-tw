---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: 反覆運算#3 = 新增表單驗證 (VB) |微軟文件
author: rick-anderson
description: 在第三個反覆運算中,我們添加基本表單驗證。 我們防止人們在未填寫所需表單欄位的情況下提交表單。 我們還驗證了 emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 3ee2f40996873a7af2eaa255edd5f157c3fefb29
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542387"
---
# <a name="iteration-3--add-form-validation-vb"></a><span data-ttu-id="1c6f2-105">反覆項目 #3 – 新增表單驗證 (VB)</span><span class="sxs-lookup"><span data-stu-id="1c6f2-105">Iteration #3 – Add form validation (VB)</span></span>

<span data-ttu-id="1c6f2-106">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1c6f2-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="1c6f2-107">下載代碼</span><span class="sxs-lookup"><span data-stu-id="1c6f2-107">Download Code</span></span>](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> <span data-ttu-id="1c6f2-108">在第三個反覆運算中,我們添加基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="1c6f2-109">我們防止人們在未填寫所需表單欄位的情況下提交表單。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="1c6f2-110">我們還驗證電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-110">We also validate email addresses and phone numbers.</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="1c6f2-111">建構 MVC 應用程式 (VB) ASP.NET連絡人管理</span><span class="sxs-lookup"><span data-stu-id="1c6f2-111">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="1c6f2-112">在本系列教程中,我們從頭到尾構建整個聯繫人管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="1c6f2-113">透過聯絡人管理員應用程式,您可以儲存連絡人資訊 (姓名、電話號碼和電子郵件位址) 人員清單。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="1c6f2-114">我們通過多次反覆運算構建應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="1c6f2-115">每次反覆運算時,我們都會逐步改進應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="1c6f2-116">此多反覆運算方法的目標是使您能夠瞭解每次更改的原因。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="1c6f2-117">反覆運算#1 - 創建應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="1c6f2-118">在第一次反覆運算中,我們以最簡單的方式創建聯繫人管理器。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="1c6f2-119">我們添加對基本資料庫操作的支援:創建、讀取、更新和刪除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="1c6f2-120">反覆運算#2 - 使應用程式看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="1c6f2-121">在此反覆運算中,我們通過修改預設ASP.NET MVC 檢視母版頁和級聯樣式表來改進應用程式的外觀。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="1c6f2-122">反覆運算#3 - 添加表單驗證。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="1c6f2-123">在第三個反覆運算中,我們添加基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="1c6f2-124">我們防止人們在未填寫所需表單欄位的情況下提交表單。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="1c6f2-125">我們還驗證電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="1c6f2-126">反覆運算#4 - 使應用程式鬆散耦合。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="1c6f2-127">在第四次反覆運算中,我們利用多種軟體設計模式,使維護和修改聯繫人管理器應用程式變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="1c6f2-128">例如,我們重構應用程式以使用存儲庫模式和依賴項注入模式。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="1c6f2-129">反覆運算#5 - 創建單元測試。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="1c6f2-130">在第五次反覆運算中,我們通過添加單元測試使應用程式更易於維護和修改。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="1c6f2-131">我們類比數據模型類,並為控制器和驗證邏輯構建單元測試。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="1c6f2-132">反覆運算#6 - 使用測試驅動開發。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="1c6f2-133">在第六次反覆運算中,我們首先編寫單元測試並針對單元測試編寫代碼,從而向應用程式添加新功能。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="1c6f2-134">在此反覆運算中,我們添加聯繫人組。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="1c6f2-135">反覆運算#7 - 添加Ajax功能。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="1c6f2-136">在第七次反覆運算中,我們通過增加對Ajax的支援來提高應用程式的回應性和性能。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="1c6f2-137">此反覆運算</span><span class="sxs-lookup"><span data-stu-id="1c6f2-137">This Iteration</span></span>

<span data-ttu-id="1c6f2-138">在聯繫人管理器應用程式的第二次反覆運算中,我們添加基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="1c6f2-139">我們防止人員提交聯繫人而不輸入所需表單欄位的值。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="1c6f2-140">我們還驗證電話號碼和電子郵寄地址(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>

<span data-ttu-id="1c6f2-141">[![[New Project] \(新增專案\) 對話方塊](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1c6f2-141">[![The New Project dialog box](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span></span>

<span data-ttu-id="1c6f2-142">**圖 01**: 具有認證的表單([按下以檢視全尺寸影像](iteration-3-add-form-validation-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="1c6f2-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-vb/_static/image2.png))</span></span>

<span data-ttu-id="1c6f2-143">在此反覆運算中,我們將驗證邏輯直接添加到控制器操作中。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="1c6f2-144">通常,這不是向ASP.NET MVC 應用程式添加驗證的建議方法。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="1c6f2-145">更好的方法是將應用程序的驗證邏輯放在單獨的[服務層](http://martinfowler.com/eaaCatalog/serviceLayer.html)中。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="1c6f2-146">在下一次反覆運算中,我們將重構聯繫人管理器應用程式,以使應用程式更具可維護性。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="1c6f2-147">在此反覆運算中,為了簡單化,我們手動編寫所有驗證代碼。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="1c6f2-148">我們可以利用驗證框架,而不是自己編寫驗證代碼。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="1c6f2-149">例如,可以使用 Microsoft 企業庫驗證應用程式區 (VAB) 來實現 ASP.NET MVC 應用程式的驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="1c6f2-150">要瞭解有關驗證應用程式塊的更多,請參閱:</span><span class="sxs-lookup"><span data-stu-id="1c6f2-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="1c6f2-151">將驗證新增到建立檢視</span><span class="sxs-lookup"><span data-stu-id="1c6f2-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="1c6f2-152">讓我們首先向"創建"視圖添加驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="1c6f2-153">幸運的是,由於我們使用 Visual Studio 生成了"創建"視圖,因此"創建"視圖已包含顯示驗證消息所需的所有使用者介面邏輯。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="1c6f2-154">"創建"檢視包含在清單 1 中。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="1c6f2-155">**清單 1 - [檢視]連絡人\創建.aspx**</span><span class="sxs-lookup"><span data-stu-id="1c6f2-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

<span data-ttu-id="1c6f2-156">欄位驗證錯誤類用於設定 Html.驗證 Message() 説明程式呈現的輸出的樣式。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-156">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="1c6f2-157">輸入驗證錯誤類用於設定 Html.TextBox() 説明程式呈現的文字框(輸入)的樣式。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-157">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="1c6f2-158">驗證摘要錯誤類用於設置 Html.驗證摘要() 説明程式呈現的無序列表的樣式。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-158">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="1c6f2-159">您可以修改本節中描述的樣式表類,以自定義驗證錯誤消息的外觀。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-159">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>

## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="1c6f2-160">將驗證邏輯加入到建立作業</span><span class="sxs-lookup"><span data-stu-id="1c6f2-160">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="1c6f2-161">現在,"創建"視圖從不顯示驗證錯誤消息,因為我們尚未編寫邏輯來生成任何消息。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-161">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="1c6f2-162">為了顯示驗證錯誤消息,您需要將錯誤消息添加到 ModelState。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-162">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="1c6f2-163">當將表單欄位的值分配給屬性時,UpdateModel() 方法會自動將錯誤消息添加到 ModelState。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-163">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="1c6f2-164">例如,如果您嘗試將字串「apple」分配給接受 DateTime 值的 DateDate 屬性,則 UpdateModel() 方法將錯誤添加到 ModelState。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-164">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>

<span data-ttu-id="1c6f2-165">清單 2 中修改的 Create() 方法包含一個新部分,用於在新聯繫人插入資料庫之前驗證 Contact 類的屬性。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-165">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="1c6f2-166">**清單2 - 控制器\聯絡控制器.vb(透過認證建立)**</span><span class="sxs-lookup"><span data-stu-id="1c6f2-166">**Listing 2 - Controllers\ContactController.vb (Create with validation)**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

<span data-ttu-id="1c6f2-167">驗證部分強制執行四個不同的驗證規則:</span><span class="sxs-lookup"><span data-stu-id="1c6f2-167">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="1c6f2-168">FirstName 屬性的長度必須大於零(它不能僅由空格組成)</span><span class="sxs-lookup"><span data-stu-id="1c6f2-168">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="1c6f2-169">LastName 屬性的長度必須大於零(它不能僅由空格組成)</span><span class="sxs-lookup"><span data-stu-id="1c6f2-169">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="1c6f2-170">如果 Phone 屬性具有值(長度大於 0),則 Phone 屬性必須匹配正則運算式。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-170">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="1c6f2-171">如果 Email 屬性的值(長度大於 0),則 Email 屬性必須與正則運算式匹配。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-171">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="1c6f2-172">當存在驗證規則衝突時,在 AddModelError() 方法的説明下,將一條錯誤消息添加到 ModelState。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-172">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="1c6f2-173">將消息添加到 ModelState 時,會提供屬性的名稱和驗證錯誤消息的文本。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-173">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="1c6f2-174">此錯誤訊息由 Html.驗證摘要() 和 Html.驗證消息() 説明器方法顯示在檢視中。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-174">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="1c6f2-175">執行驗證規則後,將檢查 ModelState 的「IsValid」屬性。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-175">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="1c6f2-176">將任何驗證錯誤消息添加到 ModelState 時,「IsValid」屬性將返回 false。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-176">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="1c6f2-177">如果驗證失敗,則使用錯誤消息重新顯示"創建"表單。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-177">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="1c6f2-178">我收到用於驗證從正則表達式存儲庫的電話號碼和電子郵寄地址的正則運算式,[*http://regexlib.com*](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="1c6f2-178">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>

## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="1c6f2-179">將驗證邏輯加入編輯操作</span><span class="sxs-lookup"><span data-stu-id="1c6f2-179">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="1c6f2-180">編輯() 操作更新連絡人。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-180">The Edit() action updates a Contact.</span></span> <span data-ttu-id="1c6f2-181">Edit() 操作需要執行與 Create() 操作完全相同的驗證。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-181">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="1c6f2-182">我們不應複製相同的驗證代碼,而應重構聯繫人控制器,以便 Create() 和 Edit() 操作調用相同的驗證方法。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-182">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="1c6f2-183">修改後的聯繫人控制器類包含在清單 3 中。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-183">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="1c6f2-184">此類具有在 Create() 和 Edit() 操作中調用的新驗證連絡人() 方法。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-184">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="1c6f2-185">**清單3 - 控制器\聯絡控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="1c6f2-185">**Listing 3 - Controllers\ContactController.vb**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a><span data-ttu-id="1c6f2-186">總結</span><span class="sxs-lookup"><span data-stu-id="1c6f2-186">Summary</span></span>

<span data-ttu-id="1c6f2-187">在此反覆運算中,我們將基本表單驗證添加到我們的聯繫人管理器應用程式中。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-187">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="1c6f2-188">我們的驗證邏輯可防止使用者提交新連絡人或編輯現有連絡人,而不提供 Name 和 LASTName 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-188">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="1c6f2-189">此外,用戶必須提供有效的電話號碼和電子郵寄地址。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-189">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="1c6f2-190">在此反覆運算中,我們以最簡單的方式將驗證邏輯添加到我們的聯繫人管理器應用程式中。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-190">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="1c6f2-191">但是,從長期來看,將驗證邏輯混合到控制器邏輯中將給我們帶來問題。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-191">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="1c6f2-192">隨著時間的推移,我們的應用程式將更難維護和修改。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-192">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="1c6f2-193">在下一次反覆運算中,我們將重構我們的驗證邏輯和資料庫存取邏輯的控制器。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-193">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="1c6f2-194">我們將利用多種軟體設計原則,使我們能夠創建一個更鬆散耦合、更可維護的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c6f2-194">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1c6f2-195">[前一個](iteration-2-make-the-application-look-nice-vb.md)
> [下一個](iteration-4-make-the-application-loosely-coupled-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1c6f2-195">[Previous](iteration-2-make-the-application-look-nice-vb.md)
[Next](iteration-4-make-the-application-loosely-coupled-vb.md)</span></span>
