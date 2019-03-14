---
title: 將驗證新增至 ASP.NET Core Razor 頁面
author: rick-anderson
description: 了解如何將驗證新增至 ASP.NET Core 中的 Razor 頁面。
ms.author: riande
ms.custom: mvc
ms.date: 12/5/2018
uid: tutorials/razor-pages/validation
ms.openlocfilehash: 93303b76561a8a800432ee707997f240f15e29c7
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57024375"
---
# <a name="add-validation-to-an-aspnet-core-razor-page"></a><span data-ttu-id="7d3ce-103">將驗證新增至 ASP.NET Core Razor 頁面</span><span class="sxs-lookup"><span data-stu-id="7d3ce-103">Add validation to an ASP.NET Core Razor Page</span></span>

<span data-ttu-id="7d3ce-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="7d3ce-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="7d3ce-105">在本節中將驗證邏輯新增至 `Movie` 模型。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-105">In this section, validation logic is added to the `Movie` model.</span></span> <span data-ttu-id="7d3ce-106">使用者建立或編輯電影時，就會強制執行驗證規則。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-106">The validation rules are enforced any time a user creates or edits a movie.</span></span>

## <a name="validation"></a><span data-ttu-id="7d3ce-107">驗證</span><span class="sxs-lookup"><span data-stu-id="7d3ce-107">Validation</span></span>

<span data-ttu-id="7d3ce-108">軟體開發的核心原則稱為 [DRY](https://wikipedia.org/wiki/Don%27t_repeat_yourself)("**D**on't **R**epeat **Y**ourself", 不重複原則)。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-108">A key tenet of software development is called [DRY](https://wikipedia.org/wiki/Don%27t_repeat_yourself) ("**D**on't **R**epeat **Y**ourself").</span></span> <span data-ttu-id="7d3ce-109">Razor Pages可促進開發，只要指定功能一次，就能在整個應用程式中運用。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-109">Razor Pages encourages development where functionality is specified once, and it's reflected throughout the app.</span></span> <span data-ttu-id="7d3ce-110">DRY 有助於：</span><span class="sxs-lookup"><span data-stu-id="7d3ce-110">DRY can help:</span></span>

* <span data-ttu-id="7d3ce-111">降低應用程式中的程式碼數量。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-111">Reduce the amount of code in an app.</span></span>
* <span data-ttu-id="7d3ce-112">使程式碼較少出現錯誤，而且更容易進行測試和維護。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-112">Make the code less error prone, and easier to test and maintain.</span></span>

<span data-ttu-id="7d3ce-113">Razor Pages 和 Entity Framework 所提供的驗證支援就是 DRY 準則的絶佳範例。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-113">The validation support provided by Razor Pages and Entity Framework is a good example of the DRY principle.</span></span> <span data-ttu-id="7d3ce-114">驗證規則是在單一位置 (在模型類別中) 以宣告方式指定，而規則可在應用程式的任何位置強制執行。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-114">Validation rules are declaratively specified in one place (in the model class), and the rules are enforced everywhere in the app.</span></span>

### <a name="adding-validation-rules-to-the-movie-model"></a><span data-ttu-id="7d3ce-115">將驗證規則新增至電影模型</span><span class="sxs-lookup"><span data-stu-id="7d3ce-115">Adding validation rules to the movie model</span></span>

<span data-ttu-id="7d3ce-116">開啟 *Models/Movie.cs* 檔案。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-116">Open the *Models/Movie.cs* file.</span></span> <span data-ttu-id="7d3ce-117">[DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) 提供一組內建的驗證屬性 (attribute)，其以宣告方式套用至類別或屬性 (property)。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-117">[DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) provides a built-in set of validation attributes that are applied declaratively to a class or property.</span></span> <span data-ttu-id="7d3ce-118">DataAnnotations 也包含格式化屬性 (例如 `DataType`)，可協助進行格式化，但不提供驗證。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-118">DataAnnotations also contain formatting attributes like `DataType` that help with formatting and don't provide validation.</span></span>

<span data-ttu-id="7d3ce-119">更新 `Movie` 類別，以充分利用 `Required`、`StringLength`、`RegularExpression` 和 `Range` 驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-119">Update the `Movie` class to take advantage of the `Required`, `StringLength`, `RegularExpression`, and `Range` validation attributes.</span></span>

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/MovieDateRatingDA.cs?name=snippet1)]

<span data-ttu-id="7d3ce-120">驗證屬性 (attribute) 會指定對模型屬性 (property) 強制執行的行為：</span><span class="sxs-lookup"><span data-stu-id="7d3ce-120">Validation attributes specify behavior that's enforced on model properties:</span></span>

* <span data-ttu-id="7d3ce-121">`Required` 和 `MinimumLength` 屬性 (attribute) 指出屬性 (property) 必須具有值。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-121">The `Required` and `MinimumLength` attributes indicate that a property must have a value.</span></span> <span data-ttu-id="7d3ce-122">不過，使用者可以輸入空白字元以滿足可為 Null 之類型的驗證條件約束。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-122">However, nothing prevents a user from entering whitespace to satisfy the validation constraint for a nullable type.</span></span> <span data-ttu-id="7d3ce-123">不可為 Null 的[實值類型](/dotnet/csharp/language-reference/keywords/value-types) (如 `decimal`、`int`、`float` 和 `DateTime`) 原本就是必要項目，而且不需要 `Required` 屬性。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-123">Non-nullable [value types](/dotnet/csharp/language-reference/keywords/value-types) (such as `decimal`, `int`, `float`, and `DateTime`) are inherently required and don't need the `Required` attribute.</span></span>
* <span data-ttu-id="7d3ce-124">`RegularExpression` 屬性會限制使用者可以輸入的字元數目。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-124">The `RegularExpression` attribute limits the characters that the user can enter.</span></span> <span data-ttu-id="7d3ce-125">在上述程式碼中，`Genre` 必須以一個以上的大寫字母開頭，並在後面加上零個以上的字母、單引號或雙引號、空格字元或連字號。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-125">In the preceding code, `Genre` must start with one or more capital letters and follow with zero or more letters, single or double quotes, whitespace characters, or dashes.</span></span> <span data-ttu-id="7d3ce-126">`Rating` 必須以一個以上的大寫字母開頭，並在後面加上零個以上的字母、數字、單引號或雙引號、空格字元或連字號。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-126">`Rating` must start with one or more capital letters and follow with zero or more letters, numbers, single or double quotes, whitespace characters, or dashes.</span></span>
* <span data-ttu-id="7d3ce-127">`Range` 屬性會將值限制在指定的範圍內。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-127">The `Range` attribute constrains a value to a specified range.</span></span>
* <span data-ttu-id="7d3ce-128">`StringLength` 屬性可設定字串的最大長度，並選擇性地設定最小長度。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-128">The `StringLength` attribute sets the maximum length of a string, and optionally the minimum length.</span></span> 

<span data-ttu-id="7d3ce-129">擁有 ASP.NET Core 自動強制執行的驗證規則有助於讓應用程式更穩固。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-129">Having validation rules automatically enforced by ASP.NET Core helps make an app more robust.</span></span> <span data-ttu-id="7d3ce-130">對模型的自動驗證可協助保護應用程式，因為您不需要在新增新程式碼時記得加以套用。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-130">Automatic validation on models helps protect the app because you don't have to remember to apply them when new code is added.</span></span>

### <a name="validation-error-ui-in-razor-pages"></a><span data-ttu-id="7d3ce-131">Razor 頁面中的驗證錯誤 UI</span><span class="sxs-lookup"><span data-stu-id="7d3ce-131">Validation Error UI in Razor Pages</span></span>

<span data-ttu-id="7d3ce-132">執行應用程式，並巡覽至 Pages/Movies。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-132">Run the app and navigate to Pages/Movies.</span></span>

<span data-ttu-id="7d3ce-133">選取 **Create New** 連結。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-133">Select the **Create New** link.</span></span> <span data-ttu-id="7d3ce-134">使用某些無效值完成表單。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-134">Complete the form with some invalid values.</span></span> <span data-ttu-id="7d3ce-135">當 jQuery 用戶端驗證偵測到錯誤時，它會顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-135">When jQuery client-side validation detects the error, it displays an error message.</span></span>

![有多個 jQuery 用戶端驗證錯誤的電影檢視表單](validation/_static/val.png)

[!INCLUDE[](~/includes/currency.md)]

<span data-ttu-id="7d3ce-137">請注意表單在包含無效值的每個欄位中自動呈現驗證錯誤訊息的方式。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-137">Notice how the form has automatically rendered a validation error message in each field containing an invalid value.</span></span> <span data-ttu-id="7d3ce-138">用戶端 (使用 JavaScript 和 jQuery) 與伺服器端 (當使用者已停用 JavaScript 時) 都會強制執行這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-138">The errors are enforced both client-side (using JavaScript and jQuery) and server-side (when a user has JavaScript disabled).</span></span>

<span data-ttu-id="7d3ce-139">明顯的好處是：**不**需要在 Create 或 Edit 頁面中進行程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-139">A significant benefit is that **no** code changes were necessary in the Create  or Edit pages.</span></span> <span data-ttu-id="7d3ce-140">一旦 DataAnnotations 套用至模型，就會啟用驗證 UI。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-140">Once DataAnnotations were applied to the model, the validation UI was enabled.</span></span> <span data-ttu-id="7d3ce-141">本教學課程中建立的 Razor 頁面會自動拾取驗證規則 (在 `Movie` 模型類別的屬性 (property) 上使用驗證屬性 (attribute))。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-141">The Razor Pages created in this tutorial automatically picked up the validation rules (using validation attributes on the properties of the `Movie` model class).</span></span> <span data-ttu-id="7d3ce-142">使用 Edit 頁面測試驗證，會套用相同的驗證。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-142">Test validation using the Edit page, the same validation is applied.</span></span>

<span data-ttu-id="7d3ce-143">要一直到沒有任何用戶端驗證錯誤之後，才會將表單資料發佈到伺服器。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-143">The form data isn't posted to the server until there are no client-side validation errors.</span></span> <span data-ttu-id="7d3ce-144">請確認表單資料不會經由下列一或多種方式發佈：</span><span class="sxs-lookup"><span data-stu-id="7d3ce-144">Verify form data isn't posted by one or more of the following approaches:</span></span>

* <span data-ttu-id="7d3ce-145">將中斷點放置在 `OnPostAsync` 方法中。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-145">Put a break point in the `OnPostAsync` method.</span></span> <span data-ttu-id="7d3ce-146">提交表單 (選取 [建立] 或 [儲存])。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-146">Submit the form (select **Create** or **Save**).</span></span> <span data-ttu-id="7d3ce-147">永遠不會叫用中斷點。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-147">The break point is never hit.</span></span>
* <span data-ttu-id="7d3ce-148">使用 [Fiddler 工具](http://www.telerik.com/fiddler)。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-148">Use the [Fiddler tool](http://www.telerik.com/fiddler).</span></span>
* <span data-ttu-id="7d3ce-149">使用瀏覽器開發人員工具來監視網路流量。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-149">Use the browser developer tools to monitor network traffic.</span></span>

### <a name="server-side-validation"></a><span data-ttu-id="7d3ce-150">伺服器端驗證</span><span class="sxs-lookup"><span data-stu-id="7d3ce-150">Server-side validation</span></span>

<span data-ttu-id="7d3ce-151">在瀏覽器中停用 JavaScript 時，提交含有錯誤的表單將發佈到伺服器。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-151">When JavaScript is disabled in the browser, submitting the form with errors will post to the server.</span></span>

<span data-ttu-id="7d3ce-152">選擇性地測試伺服器端驗證：</span><span class="sxs-lookup"><span data-stu-id="7d3ce-152">Optional, test server-side validation:</span></span>

* <span data-ttu-id="7d3ce-153">在瀏覽器中停用 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-153">Disable JavaScript in the browser.</span></span> <span data-ttu-id="7d3ce-154">您可以使用瀏覽器的開發人員工具來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-154">You can do this using your browser's developer tools.</span></span> <span data-ttu-id="7d3ce-155">如果您無法在該瀏覽器中停用 JavaScript，請嘗試另一個瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-155">If you can't disable JavaScript in the browser, try another browser.</span></span>
* <span data-ttu-id="7d3ce-156">在 Create 或 Edit 頁面的 `OnPostAsync` 方法中設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-156">Set a break point in the `OnPostAsync` method of the Create or Edit page.</span></span>
* <span data-ttu-id="7d3ce-157">提交含有驗證錯誤的表單。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-157">Submit a form with validation errors.</span></span>
* <span data-ttu-id="7d3ce-158">確認模型狀態無效：</span><span class="sxs-lookup"><span data-stu-id="7d3ce-158">Verify the model state is invalid:</span></span>

  ```csharp
   if (!ModelState.IsValid)
   {
      return Page();
   }
  ```

<span data-ttu-id="7d3ce-159">下列程式碼顯示您稍早在本教學課程中包含 Scaffold 的部分 *Create.cshtml* 頁面。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-159">The following code shows a portion of the *Create.cshtml* page that you scaffolded earlier in the tutorial.</span></span> <span data-ttu-id="7d3ce-160">Create 和 Edit 頁面會使用它來顯示初始表單，以及在發生錯誤時重新顯示格式。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-160">It's used by the Create and Edit pages to display the initial form and to redisplay the form in the event of an error.</span></span>

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Create.cshtml?range=14-20)]

<span data-ttu-id="7d3ce-161">[輸入標記協助程式](xref:mvc/views/working-with-forms)會使用 [DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) 屬性，並產生在用戶端上進行 jQuery 驗證所需的 HTML 屬性。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-161">The [Input Tag Helper](xref:mvc/views/working-with-forms) uses the [DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) attributes and produces HTML attributes needed for jQuery Validation on the client-side.</span></span> <span data-ttu-id="7d3ce-162">[驗證標記協助程式](xref:mvc/views/working-with-forms#the-validation-tag-helpers)會顯示驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-162">The [Validation Tag Helper](xref:mvc/views/working-with-forms#the-validation-tag-helpers) displays validation errors.</span></span> <span data-ttu-id="7d3ce-163">如需詳細資訊，請參閱[驗證](xref:mvc/models/validation)。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-163">See [Validation](xref:mvc/models/validation) for more information.</span></span>

<span data-ttu-id="7d3ce-164">Create 和 Edit 頁面中沒有任何驗證規則。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-164">The Create and Edit pages have no validation rules in them.</span></span> <span data-ttu-id="7d3ce-165">只有在 `Movie` 類別中才能指定驗證規則和錯誤字串。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-165">The validation rules and the error strings are specified only in the `Movie` class.</span></span> <span data-ttu-id="7d3ce-166">這些驗證規則會自動套用至編輯 `Movie` 模型的 Razor 頁面。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-166">These validation rules are automatically applied to Razor Pages that edit the `Movie` model.</span></span>

<span data-ttu-id="7d3ce-167">當驗證邏輯需要變更時，它只會在模型中進行。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-167">When validation logic needs to change, it's done only in the model.</span></span> <span data-ttu-id="7d3ce-168">驗證會一致地套用在整個應用程式中(驗證邏輯定義於一個位置)。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-168">Validation is applied consistently throughout the application (validation logic is defined in one place).</span></span> <span data-ttu-id="7d3ce-169">位於一個位置的驗證有助於讓程式碼保持整潔，並可讓您更容易進行維護和更新。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-169">Validation in one place helps keep the code clean, and makes it easier to maintain and update.</span></span>

## <a name="using-datatype-attributes"></a><span data-ttu-id="7d3ce-170">使用 DataType 屬性</span><span class="sxs-lookup"><span data-stu-id="7d3ce-170">Using DataType Attributes</span></span>

<span data-ttu-id="7d3ce-171">檢查 `Movie` 類別。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-171">Examine the `Movie` class.</span></span> <span data-ttu-id="7d3ce-172">除了一組內建的驗證屬性之外，`System.ComponentModel.DataAnnotations` 命名空間還提供了格式屬性。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-172">The `System.ComponentModel.DataAnnotations` namespace provides formatting attributes in addition to the built-in set of validation attributes.</span></span> <span data-ttu-id="7d3ce-173">`DataType` 屬性 (attribute) 會套用至 `ReleaseDate` 和 `Price` 屬性 (property)。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-173">The `DataType` attribute is applied to the `ReleaseDate` and `Price` properties.</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie/Models/MovieDateRatingDA.cs?highlight=2,6&name=snippet2)]

<span data-ttu-id="7d3ce-174">`DataType` 屬性只提供檢視引擎將資料格式化的提示 (以及提供一些屬性，例如用於 URL 的 `<a>` 和用於電子郵件的 `<a href="mailto:EmailAddress.com">`)。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-174">The `DataType` attributes only provide hints for the view engine to format the data (and supplies attributes such as `<a>` for URL's and `<a href="mailto:EmailAddress.com">` for email).</span></span> <span data-ttu-id="7d3ce-175">使用 `RegularExpression` 屬性來驗證資料的格式。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-175">Use the `RegularExpression` attribute to validate the format of the data.</span></span> <span data-ttu-id="7d3ce-176">`DataType` 屬性可用於指定比資料庫內建類型更特定的資料類型。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-176">The `DataType` attribute is used to specify a data type that's more specific than the database intrinsic type.</span></span> <span data-ttu-id="7d3ce-177">`DataType` 屬性不是驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-177">`DataType` attributes are not validation attributes.</span></span> <span data-ttu-id="7d3ce-178">在範例應用程式中，只會顯示日期，而不含時間。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-178">In the sample application, only the date is displayed, without time.</span></span>

<span data-ttu-id="7d3ce-179">`DataType` 列舉可提供給許多資料類型，例如 Date、Time、PhoneNumber、Currency、EmailAddress 等等。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-179">The `DataType` Enumeration provides for many data types, such as Date, Time, PhoneNumber, Currency, EmailAddress, and more.</span></span> <span data-ttu-id="7d3ce-180">`DataType` 屬性也可讓應用程式自動提供類型的特定功能。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-180">The `DataType` attribute can also enable the application to automatically provide type-specific features.</span></span> <span data-ttu-id="7d3ce-181">例如，可針對 `DataType.EmailAddress` 建立 `mailto:` 連結。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-181">For example, a `mailto:` link can be created for `DataType.EmailAddress`.</span></span> <span data-ttu-id="7d3ce-182">在支援 HTML5 的瀏覽器中，可以為 `DataType.Date` 提供日期選取器。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-182">A date selector can be provided for `DataType.Date` in browsers that support HTML5.</span></span> <span data-ttu-id="7d3ce-183">`DataType` 屬性會發出 HTML 5 瀏覽器使用的 HTML 5 `data-` (唸成的 data dash) 屬性。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-183">The `DataType` attributes emits HTML 5 `data-` (pronounced data dash) attributes that HTML 5 browsers consume.</span></span> <span data-ttu-id="7d3ce-184">`DataType` 屬性**不**會提供任何驗證。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-184">The `DataType` attributes do **not** provide any validation.</span></span>

<span data-ttu-id="7d3ce-185">`DataType.Date` 未指定顯示日期的格式。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-185">`DataType.Date` doesn't specify the format of the date that's displayed.</span></span> <span data-ttu-id="7d3ce-186">根據預設，將依據以伺服器 `CultureInfo` 為基礎的預設格式顯示資料欄位。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-186">By default, the data field is displayed according to the default formats based on the server's `CultureInfo`.</span></span>


<span data-ttu-id="7d3ce-187">`[Column(TypeName = "decimal(18, 2)")]` 資料註解為必要項，因此 Entity Framework Core 可將 `Price` 正確對應到資料庫中的貨幣。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-187">The `[Column(TypeName = "decimal(18, 2)")]` data annotation is required so Entity Framework Core can correctly map `Price` to currency in the database.</span></span> <span data-ttu-id="7d3ce-188">如需詳細資訊，請參閱[資料類型](/ef/core/modeling/relational/data-types)。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-188">For more information, see [Data Types](/ef/core/modeling/relational/data-types).</span></span>

<span data-ttu-id="7d3ce-189">`DisplayFormat` 屬性用來明確指定日期格式：</span><span class="sxs-lookup"><span data-stu-id="7d3ce-189">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>

```csharp
[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
public DateTime ReleaseDate { get; set; }
```

<span data-ttu-id="7d3ce-190">`ApplyFormatInEditMode` 設定可指定當顯示值以供編輯時，應該套用的格式。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-190">The `ApplyFormatInEditMode` setting specifies that the formatting should be applied when the value is displayed for editing.</span></span> <span data-ttu-id="7d3ce-191">但在某些欄位中，您可能不想要套用該行為。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-191">You might not want that behavior for some fields.</span></span> <span data-ttu-id="7d3ce-192">例如，在貨幣值中，應該不會希望編輯 UI 中出現貨幣符號。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-192">For example, in currency values, you probably don't want the currency symbol in the edit UI.</span></span>

<span data-ttu-id="7d3ce-193">`DisplayFormat` 屬性可以單獨使用，但通常最好是使用 `DataType` 屬性。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-193">The `DisplayFormat` attribute can be used by itself, but it's generally a good idea to use the `DataType` attribute.</span></span> <span data-ttu-id="7d3ce-194">`DataType` 屬性會傳逹資料的語意，而不是在螢幕上呈現資料的方式，並提供下列使用 DisplayFormat 無法取得的優點：</span><span class="sxs-lookup"><span data-stu-id="7d3ce-194">The `DataType` attribute conveys the semantics of the data as opposed to how to render it on a screen, and provides the following benefits that you don't get with DisplayFormat:</span></span>

* <span data-ttu-id="7d3ce-195">瀏覽器可以啟用 HTML5 功能 (例如顯示日曆控制項、適合地區設定的貨幣符號、電子郵件連結等等)。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-195">The browser can enable HTML5 features (for example to show a calendar control, the locale-appropriate currency symbol, email links, etc.)</span></span>
* <span data-ttu-id="7d3ce-196">根據預設，瀏覽器將根據您的地區設定，使用正確的格式呈現資料。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-196">By default, the browser will render data using the correct format based on your locale.</span></span>
* <span data-ttu-id="7d3ce-197">`DataType` 屬性可以啟用 ASP.NET Core 架構，來選擇用於呈現資料的正確欄位範本。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-197">The `DataType` attribute can enable the ASP.NET Core framework to choose the right field template to render the data.</span></span> <span data-ttu-id="7d3ce-198">`DisplayFormat` 若是單獨使用，則會使用字串範本。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-198">The `DisplayFormat` if used by itself uses the string template.</span></span>

<span data-ttu-id="7d3ce-199">請注意：jQuery 驗證不適用於 `Range` 屬性與 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-199">Note: jQuery validation doesn't work with the `Range` attribute and `DateTime`.</span></span> <span data-ttu-id="7d3ce-200">例如，下列程式碼一律會顯示用戶端驗證錯誤，即使當日期位在指定範圍中也一樣：</span><span class="sxs-lookup"><span data-stu-id="7d3ce-200">For example, the following code will always display a client-side validation error, even when the date is in the specified range:</span></span>

```csharp
[Range(typeof(DateTime), "1/1/1966", "1/1/2020")]
   ```

<span data-ttu-id="7d3ce-201">編譯模型中的硬性日期通常不是良好的做法，因此不建議使用 `Range` 屬性和 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-201">It's generally not a good practice to compile hard dates in your models, so using the `Range` attribute and `DateTime` is discouraged.</span></span>

<span data-ttu-id="7d3ce-202">下列程式碼會顯示一行上的結合屬性：</span><span class="sxs-lookup"><span data-stu-id="7d3ce-202">The following code shows combining attributes on one line:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Models/MovieDateRatingDAmult.cs?name=snippet1)]

<span data-ttu-id="7d3ce-203">[Razor Pages 和 EF Core 使用者入門](xref:data/ef-rp/intro)說明使用 Razor Pages 執行進階 EF Core 作業。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-203">[Get started with Razor Pages and EF Core](xref:data/ef-rp/intro) shows advanced EF Core operations with Razor Pages.</span></span>

### <a name="publish-to-azure"></a><span data-ttu-id="7d3ce-204">發佈至 Azure</span><span class="sxs-lookup"><span data-stu-id="7d3ce-204">Publish to Azure</span></span>

<span data-ttu-id="7d3ce-205">如需部署至 Azure 的資訊，請參閱[教學課程：使用 SQL Database 在 Azure 中建置 ASP.NET 應用程式](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase)。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-205">For information on deploying to Azure, see [Tutorial: Build an ASP.NET app in Azure with SQL Database](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase).</span></span> <span data-ttu-id="7d3ce-206">這些指示適用於 ASP.NET 應用程式，而不是 ASP.NET Core 應用程式，但是步驟都相同。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-206">These instructions are for an ASP.NET app, not an ASP.NET Core app, but the steps are the same.</span></span>

<span data-ttu-id="7d3ce-207">感謝您看完這份 Razor Pages 簡介。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-207">Thanks for completing this introduction to Razor Pages.</span></span> <span data-ttu-id="7d3ce-208">完成本教學課程之後，非常建議您繼續參閱 [Razor 頁面與 EF Core 使用者入門](xref:data/ef-rp/intro)。</span><span class="sxs-lookup"><span data-stu-id="7d3ce-208">[Get started with Razor Pages and EF Core](xref:data/ef-rp/intro) is an excellent follow up to this tutorial.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d3ce-209">其他資源</span><span class="sxs-lookup"><span data-stu-id="7d3ce-209">Additional resources</span></span>

* <xref:mvc/views/working-with-forms>
* <xref:fundamentals/localization>
* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/authoring>

> [!div class="step-by-step"]
> [<span data-ttu-id="7d3ce-210">上一步：新增欄位</span><span class="sxs-lookup"><span data-stu-id="7d3ce-210">Previous: Adding a new field</span></span>](xref:tutorials/razor-pages/new-field)
