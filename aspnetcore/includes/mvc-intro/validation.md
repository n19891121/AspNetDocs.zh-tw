---
ms.openlocfilehash: 873e399dc7bf6bf97c0925c1bdcf21f699f0be2e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057585"
---
# <a name="add-validation-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="de529-101">將驗證新增至 ASP.NET Core MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="de529-101">Add validation to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="de529-102">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="de529-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="de529-103">在這一節中，您會將驗證邏輯新增至 `Movie` 模型，確保只要使用者建立或編輯電影，就會強制執行驗證規則。</span><span class="sxs-lookup"><span data-stu-id="de529-103">In this section you'll add validation logic to the `Movie` model, and you'll ensure that the validation rules are enforced any time a user creates or edits a movie.</span></span>

## <a name="keeping-things-dry"></a><span data-ttu-id="de529-104">項目保持 DRY</span><span class="sxs-lookup"><span data-stu-id="de529-104">Keeping things DRY</span></span>

<span data-ttu-id="de529-105">MVC 的設計原則之一是[DRY](https://wikipedia.org/wiki/Don%27t_repeat_yourself) (「不自行重複」)。</span><span class="sxs-lookup"><span data-stu-id="de529-105">One of the design tenets of MVC is [DRY](https://wikipedia.org/wiki/Don%27t_repeat_yourself) ("Don't Repeat Yourself").</span></span> <span data-ttu-id="de529-106">ASP.NET Core MVC 鼓勵您只指定一次功能或行為，然後讓它反映到應用程式的所有位置。</span><span class="sxs-lookup"><span data-stu-id="de529-106">ASP.NET Core MVC encourages you to specify functionality or behavior only once, and then have it be reflected everywhere in an app.</span></span> <span data-ttu-id="de529-107">這會減少您需要撰寫的程式碼數量，並讓您撰寫的程式碼錯誤較不容易出錯、更容易測試，以及更容易維護。</span><span class="sxs-lookup"><span data-stu-id="de529-107">This reduces the amount of code you need to write and makes the code you do write less error prone, easier to test, and easier to maintain.</span></span>

<span data-ttu-id="de529-108">MVC 和 Entity Framework Core Code First 所提供的驗證支援就是執行 DRY 準則的絶佳範例。</span><span class="sxs-lookup"><span data-stu-id="de529-108">The validation support provided by MVC and Entity Framework Core Code First is a good example of the DRY principle in action.</span></span> <span data-ttu-id="de529-109">您可以宣告方式在單一位置指定驗證規則 (在模型類別中) ，而規則可在應用程式的任何位置強制執行。</span><span class="sxs-lookup"><span data-stu-id="de529-109">You can declaratively specify validation rules in one place (in the model class) and the rules are enforced everywhere in the app.</span></span>

## <a name="adding-validation-rules-to-the-movie-model"></a><span data-ttu-id="de529-110">將驗證規則新增至電影模型</span><span class="sxs-lookup"><span data-stu-id="de529-110">Adding validation rules to the movie model</span></span>

<span data-ttu-id="de529-111">開啟 *Movie.cs* 檔案。</span><span class="sxs-lookup"><span data-stu-id="de529-111">Open the *Movie.cs* file.</span></span> <span data-ttu-id="de529-112">DataAnnotations 提供一組內建的驗證屬性 (attribute)，您可以宣告方式將其套用至類別或屬性 (property)。</span><span class="sxs-lookup"><span data-stu-id="de529-112">DataAnnotations provides a built-in set of validation attributes that you apply declaratively to any class or property.</span></span> <span data-ttu-id="de529-113">(它也包含如 `DataType` 的格式化屬性，可協助進行格式化，但不提供驗證。)</span><span class="sxs-lookup"><span data-stu-id="de529-113">(It also contains formatting attributes like `DataType` that help with formatting and don't provide any validation.)</span></span>

<span data-ttu-id="de529-114">更新 `Movie` 類別，以充分利用內建的 `Required`、`StringLength`、`RegularExpression` 和 `Range` 驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="de529-114">Update the `Movie` class to take advantage of the built-in `Required`, `StringLength`, `RegularExpression`, and `Range` validation attributes.</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie21/Models/MovieDateRatingDA.cs?name=snippet1)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Models/MovieDateRatingDA.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="de529-115">驗證屬性會指定您想要對套用目標之模型屬性，強制執行之行為。</span><span class="sxs-lookup"><span data-stu-id="de529-115">The validation attributes specify behavior that you want to enforce on the model properties they're applied to.</span></span> <span data-ttu-id="de529-116">`Required` 和 `MinimumLength` 屬性 (attribute) 指出屬性 (property) 必須是值；但無法防止使用者輸入空格以滿足此驗證。</span><span class="sxs-lookup"><span data-stu-id="de529-116">The `Required` and `MinimumLength` attributes indicates that a property must have a value; but nothing prevents a user from entering white space to satisfy this validation.</span></span> <span data-ttu-id="de529-117">`RegularExpression` 屬性則用來限制可輸入的字元。</span><span class="sxs-lookup"><span data-stu-id="de529-117">The `RegularExpression` attribute is used to limit what characters can be input.</span></span> <span data-ttu-id="de529-118">上述程式碼中的 `Genre` 和 `Rating` 必須只使用字母 (第一個字母大寫，不允許使用空格、數字和特殊字元)。</span><span class="sxs-lookup"><span data-stu-id="de529-118">In the code above, `Genre` and `Rating` must use only letters (First letter uppercase, white space, numbers and special characters are not allowed).</span></span> <span data-ttu-id="de529-119">`Range` 屬性會將值限制在指定的範圍內。</span><span class="sxs-lookup"><span data-stu-id="de529-119">The `Range` attribute constrains a value to within a specified range.</span></span> <span data-ttu-id="de529-120">`StringLength` 屬性可讓您設定字串屬性的最大長度，並選擇性設定其最小長度。</span><span class="sxs-lookup"><span data-stu-id="de529-120">The `StringLength` attribute lets you set the maximum length of a string property, and optionally its minimum length.</span></span> <span data-ttu-id="de529-121">實值型別 (如`decimal`、`int`、`float`、`DateTime`) 原本就是必要項目，而且不需要 `[Required]` 屬性。</span><span class="sxs-lookup"><span data-stu-id="de529-121">Value types (such as `decimal`, `int`, `float`, `DateTime`) are inherently required and don't need the `[Required]` attribute.</span></span>

<span data-ttu-id="de529-122">擁有 ASP.NET Core 自動強制執行的驗證規則有助於讓您的應用程式更穩固。</span><span class="sxs-lookup"><span data-stu-id="de529-122">Having validation rules automatically enforced by ASP.NET Core helps make your app more robust.</span></span> <span data-ttu-id="de529-123">它也確保您不會忘記要驗證某些項目，不小心讓不正確的資料進入資料庫。</span><span class="sxs-lookup"><span data-stu-id="de529-123">It also ensures that you can't forget to validate something and inadvertently let bad data into the database.</span></span>

## <a name="validation-error-ui-in-mvc"></a><span data-ttu-id="de529-124">MVC 中的驗證錯誤 UI</span><span class="sxs-lookup"><span data-stu-id="de529-124">Validation Error UI in MVC</span></span>

<span data-ttu-id="de529-125">執行應用程式並巡覽至電影控制器。</span><span class="sxs-lookup"><span data-stu-id="de529-125">Run the app and navigate to the Movies controller.</span></span>

<span data-ttu-id="de529-126">點選 [新建] 連結以新增新電影。</span><span class="sxs-lookup"><span data-stu-id="de529-126">Tap the **Create New** link to add a new movie.</span></span> <span data-ttu-id="de529-127">使用無效值填寫表單。</span><span class="sxs-lookup"><span data-stu-id="de529-127">Fill out the form with some invalid values.</span></span> <span data-ttu-id="de529-128">jQuery 用戶端驗證一偵測到錯誤，就會顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="de529-128">As soon as jQuery client side validation detects the error, it displays an error message.</span></span>

![有多個 jQuery 用戶端驗證錯誤的電影檢視表單](~/tutorials/first-mvc-app/validation/_static/val.png)

[!INCLUDE[](~/includes/currency.md)]

<span data-ttu-id="de529-130">請注意表單如何在包含無效值的每個欄位中自動呈現適當的驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="de529-130">Notice how the form has automatically rendered an appropriate validation error message in each field containing an invalid value.</span></span> <span data-ttu-id="de529-131">用戶端 (使用 JavaScript 和 jQuery) 與伺服器端 (若使用者已停用 JavaScript 時) 都會強制執行這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="de529-131">The errors are enforced both client-side (using JavaScript and jQuery) and server-side (in case a user has JavaScript disabled).</span></span>

<span data-ttu-id="de529-132">最明顯的好處是，您不需要為了啟用這項驗證 UI 而變更 `MoviesController` 類別或 *Create.cshtml* 檢視的程式碼，一行都不用。</span><span class="sxs-lookup"><span data-stu-id="de529-132">A significant benefit is that you didn't need to change a single line of code in the `MoviesController` class or in the *Create.cshtml* view in order to enable this validation UI.</span></span> <span data-ttu-id="de529-133">您稍早在本教學課程中建立的控制器和檢視會自動拾取您指定的驗證規則 (在 `Movie` 模型類別的屬性 (property) 上使用驗證屬性 (attribute))。</span><span class="sxs-lookup"><span data-stu-id="de529-133">The controller and views you created earlier in this tutorial automatically picked up the validation rules that you specified by using validation attributes on the properties of the `Movie` model class.</span></span> <span data-ttu-id="de529-134">使用 `Edit` 動作方法測試驗證，即會套用相同的驗證。</span><span class="sxs-lookup"><span data-stu-id="de529-134">Test validation using the `Edit` action method, and the same validation is applied.</span></span>

<span data-ttu-id="de529-135">要一直到沒有任何用戶端驗證錯誤之後，才會將表單資料傳送到伺服器。</span><span class="sxs-lookup"><span data-stu-id="de529-135">The form data isn't sent to the server until there are no client side validation errors.</span></span> <span data-ttu-id="de529-136">藉由使用 [Fiddler 工具](http://www.telerik.com/fiddler)，或 [F12 開發人員工具](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)，您可以將中斷點放入 `HTTP Post` 方法來驗證。</span><span class="sxs-lookup"><span data-stu-id="de529-136">You can verify this by putting a break point in the `HTTP Post` method, by using the [Fiddler tool](http://www.telerik.com/fiddler) , or the [F12 Developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>

## <a name="how-validation-works"></a><span data-ttu-id="de529-137">驗證的運作方式</span><span class="sxs-lookup"><span data-stu-id="de529-137">How validation works</span></span>

<span data-ttu-id="de529-138">您可能奇怪如何在不更新控制器或檢視程式碼的狀況下產生驗證 UI。</span><span class="sxs-lookup"><span data-stu-id="de529-138">You might wonder how the validation UI was generated without any updates to the code in the controller or views.</span></span> <span data-ttu-id="de529-139">下列程式碼示範兩種 `Create` 方法。</span><span class="sxs-lookup"><span data-stu-id="de529-139">The following code shows the two `Create` methods.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Controllers/MoviesController.cs?name=snippetCreate)]

<span data-ttu-id="de529-140">第一個 (HTTP GET)`Create` 動作方法會顯示初始建立表單。</span><span class="sxs-lookup"><span data-stu-id="de529-140">The first (HTTP GET) `Create` action method displays the initial Create form.</span></span> <span data-ttu-id="de529-141">第二個 (`[HttpPost]`) 版本處理表單張貼。</span><span class="sxs-lookup"><span data-stu-id="de529-141">The second (`[HttpPost]`) version handles the form post.</span></span> <span data-ttu-id="de529-142">第二個 `Create` 方法 (`[HttpPost]` 版本) 會呼叫`ModelState.IsValid` 檢查電影是否有任何驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="de529-142">The second `Create` method (The `[HttpPost]` version) calls `ModelState.IsValid` to check whether the movie has any validation errors.</span></span> <span data-ttu-id="de529-143">呼叫此方法會評估已套用至物件的所有驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="de529-143">Calling this method evaluates any validation attributes that have been applied to the object.</span></span> <span data-ttu-id="de529-144">如果物件有驗證錯誤，則 `Create` 方法會重新顯示表單。</span><span class="sxs-lookup"><span data-stu-id="de529-144">If the object has validation errors, the `Create` method re-displays the form.</span></span> <span data-ttu-id="de529-145">如果沒有任何錯誤，方法即會將新的電影儲存到資料庫。</span><span class="sxs-lookup"><span data-stu-id="de529-145">If there are no errors, the method saves the new movie in the database.</span></span> <span data-ttu-id="de529-146">在影片範例中，在用戶端上偵測到驗證錯誤時，表單不會發佈至伺服器；出現用戶端驗證錯誤時，一定不會呼叫第二個 `Create` 方法。</span><span class="sxs-lookup"><span data-stu-id="de529-146">In our movie example, the form isn't posted to the server when there are validation errors detected on the client side; the second `Create` method is never called when there are client side validation errors.</span></span> <span data-ttu-id="de529-147">如果您停用瀏覽器的 JavaScript，用戶端驗證也會停用，而且您可以測試 HTTP POST `Create` 方法 `ModelState.IsValid` 偵測任何驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="de529-147">If you disable JavaScript in your browser, client validation is disabled and you can test the HTTP POST `Create` method `ModelState.IsValid` detecting any validation errors.</span></span>

<span data-ttu-id="de529-148">您可以在 `[HttpPost] Create` 方法中設定中斷點，並確認永遠不會呼叫該方法，用戶端驗證就不會在偵測到驗證錯誤時，提交表單資料。</span><span class="sxs-lookup"><span data-stu-id="de529-148">You can set a break point in the `[HttpPost] Create` method and verify the method is never called, client side validation won't submit the form data when validation errors are detected.</span></span> <span data-ttu-id="de529-149">如果您停用瀏覽器的 JavaScript，然後提交有錯誤的表單，就會叫用中斷點。</span><span class="sxs-lookup"><span data-stu-id="de529-149">If you disable JavaScript in your browser, then submit the form with errors, the break point will be hit.</span></span> <span data-ttu-id="de529-150">您仍可使用沒有 JavaScript 的完整驗證。</span><span class="sxs-lookup"><span data-stu-id="de529-150">You still get full validation without JavaScript.</span></span> 

<span data-ttu-id="de529-151">下圖顯示如何停用 FireFox 瀏覽器的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="de529-151">The following image shows how to disable JavaScript in the FireFox browser.</span></span>

![Firefox：在 [選項] 的 [內容] 索引標籤中，取消核取 [啟用 Javascript] 核取方塊。](~/tutorials/first-mvc-app/validation/_static/ff.png)

<span data-ttu-id="de529-153">下圖顯示如何停用 Chrome 瀏覽器的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="de529-153">The following image shows how to disable JavaScript in the Chrome browser.</span></span>

![Google Chrome：在 [內容] 設定的 [Javascript] 區段中，選取 [不允許任何站台執行 JavaScript]。](~/tutorials/first-mvc-app/validation/_static/chrome.png)

<span data-ttu-id="de529-155">停用 JavaScript 之後，張貼無效的資料並逐步執行偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="de529-155">After you disable JavaScript, post invalid data and step through the debugger.</span></span>

![偵錯張貼的無效資料時，ModelState.IsValid 上的 IntelliSense 會顯示值為 false。](~/tutorials/first-mvc-app/validation/_static/ms.png)

<span data-ttu-id="de529-157">以下是您稍早在本教學課程中包含 Scaffold 的部分 *Create.cshtml* 檢視範本。</span><span class="sxs-lookup"><span data-stu-id="de529-157">Below is portion of the *Create.cshtml* view template that you scaffolded earlier in the tutorial.</span></span> <span data-ttu-id="de529-158">上述動作方法會使用它來顯示初始表單，以及在發生錯誤時重新顯示它。</span><span class="sxs-lookup"><span data-stu-id="de529-158">It's used by the action methods shown above both to display the initial form and to redisplay it in the event of an error.</span></span>

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Views/Movies/CreateRatingBrevity.cshtml)]

<span data-ttu-id="de529-159">[輸入標記協助程式](xref:mvc/views/working-with-forms) 會使用 [DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) 屬性，並產生在用戶端上進行 jQuery 驗證所需的 HTML 屬性。</span><span class="sxs-lookup"><span data-stu-id="de529-159">The [Input Tag Helper](xref:mvc/views/working-with-forms) uses the [DataAnnotations](/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) attributes and produces HTML attributes needed for jQuery Validation on the client side.</span></span> <span data-ttu-id="de529-160">[驗證標記協助程式](xref:mvc/views/working-with-forms#the-validation-tag-helpers)會顯示驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="de529-160">The [Validation Tag Helper](xref:mvc/views/working-with-forms#the-validation-tag-helpers) displays validation errors.</span></span> <span data-ttu-id="de529-161">如需詳細資訊，請參閱[驗證](xref:mvc/models/validation)。</span><span class="sxs-lookup"><span data-stu-id="de529-161">See [Validation](xref:mvc/models/validation) for more information.</span></span>

<span data-ttu-id="de529-162">此方法最好的一點在於，控制器和 `Create` 檢視範本對要強制執行的實際驗證規則，或顯示的特定錯誤訊息，全都一無所知。</span><span class="sxs-lookup"><span data-stu-id="de529-162">What's really nice about this approach is that neither the controller nor the `Create` view template knows anything about the actual validation rules being enforced or about the specific error messages displayed.</span></span> <span data-ttu-id="de529-163">驗證規則和錯誤字串只在 `Movie` 類別中指定。</span><span class="sxs-lookup"><span data-stu-id="de529-163">The validation rules and the error strings are specified only in the `Movie` class.</span></span> <span data-ttu-id="de529-164">這些相同的驗證規則會自動套用到 `Edit` 檢視，以及任何其他您可能建立以編輯模型的檢視範本。</span><span class="sxs-lookup"><span data-stu-id="de529-164">These same validation rules are automatically applied to the `Edit` view and any other views templates you might create that edit your model.</span></span>

<span data-ttu-id="de529-165">當您需要變更驗證邏輯時，您可以在模型中新增驗證屬性 (本例中為 `Movie` 類別)，只在一個位置完成作業。</span><span class="sxs-lookup"><span data-stu-id="de529-165">When you need to change validation logic, you can do so in exactly one place by adding validation attributes to the model (in this example, the `Movie` class).</span></span> <span data-ttu-id="de529-166">您不必擔心應用程式的不同部分會與規則強制執行的方式不一致，所有的驗證邏輯都是在同一個地方定義，用於所有位置。</span><span class="sxs-lookup"><span data-stu-id="de529-166">You won't have to worry about different parts of the application being inconsistent with how the rules are enforced — all validation logic will be defined in one place and used everywhere.</span></span> <span data-ttu-id="de529-167">這會讓程式碼非常整齊乾淨，容易維護及發展。</span><span class="sxs-lookup"><span data-stu-id="de529-167">This keeps the code very clean, and makes it easy to maintain and evolve.</span></span> <span data-ttu-id="de529-168">這表示您會完全接受 DRY 原則。</span><span class="sxs-lookup"><span data-stu-id="de529-168">And it means that you'll be fully honoring the DRY principle.</span></span>

## <a name="using-datatype-attributes"></a><span data-ttu-id="de529-169">使用 DataType 屬性</span><span class="sxs-lookup"><span data-stu-id="de529-169">Using DataType Attributes</span></span>

<span data-ttu-id="de529-170">開啟 *Movie.cs* 檔案並檢查 `Movie` 類別。</span><span class="sxs-lookup"><span data-stu-id="de529-170">Open the *Movie.cs* file and examine the `Movie` class.</span></span> <span data-ttu-id="de529-171">除了一組內建的驗證屬性之外，`System.ComponentModel.DataAnnotations` 命名空間還提供了格式屬性。</span><span class="sxs-lookup"><span data-stu-id="de529-171">The `System.ComponentModel.DataAnnotations` namespace provides formatting attributes in addition to the built-in set of validation attributes.</span></span> <span data-ttu-id="de529-172">發行日期和價格欄位已經套用 `DataType` 列舉值。</span><span class="sxs-lookup"><span data-stu-id="de529-172">We've already applied a `DataType` enumeration value to the release date and to the price fields.</span></span> <span data-ttu-id="de529-173">下列程式碼會示範具有適當 `DataType` 屬性 (attribute) 的 `ReleaseDate` 和 `Price` 屬性 (property)。</span><span class="sxs-lookup"><span data-stu-id="de529-173">The following code shows the `ReleaseDate` and `Price` properties with the appropriate `DataType` attribute.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Models/MovieDateRatingDA.cs?highlight=2,6&name=snippet2)]

<span data-ttu-id="de529-174">`DataType` 屬性只會提供檢視引擎格式化資料的提示 (同時會提供一些項目/屬性，例如 URL 的 `<a>` 以及用於電子郵件的 `<a href="mailto:EmailAddress.com">`)。</span><span class="sxs-lookup"><span data-stu-id="de529-174">The `DataType` attributes only provide hints for the view engine to format the data (and supplies elements/attributes such as `<a>` for URL's and `<a href="mailto:EmailAddress.com">` for email.</span></span> <span data-ttu-id="de529-175">您可使用 `RegularExpression` 屬性来驗證資料的格式。</span><span class="sxs-lookup"><span data-stu-id="de529-175">You can use the `RegularExpression` attribute to validate the format of the data.</span></span> <span data-ttu-id="de529-176">`DataType`屬性用於指定比資料庫內建類型更特定的資料類型，這些並非驗證屬性。</span><span class="sxs-lookup"><span data-stu-id="de529-176">The `DataType` attribute is used to specify a data type that's more specific than the database intrinsic type, they're not validation attributes.</span></span> <span data-ttu-id="de529-177">本例中，我們只想要追蹤日期，不追蹤時間。</span><span class="sxs-lookup"><span data-stu-id="de529-177">In this case we only want to keep track of the date, not the time.</span></span> <span data-ttu-id="de529-178">`DataType` 列舉提供許多資料類型，例如 Date、Time、PhoneNumber、Currency、EmailAddress 等等。</span><span class="sxs-lookup"><span data-stu-id="de529-178">The `DataType` Enumeration provides for many data types, such as Date, Time, PhoneNumber, Currency, EmailAddress and more.</span></span> <span data-ttu-id="de529-179">`DataType` 屬性也可讓應用程式自動提供類型的特定功能。</span><span class="sxs-lookup"><span data-stu-id="de529-179">The `DataType` attribute can also enable the application to automatically provide type-specific features.</span></span> <span data-ttu-id="de529-180">例如，可建立 `DataType.EmailAddress` 的 `mailto:` 連結，而且可以在支援 HTML5 的瀏覽器中提供 `DataType.Date` 的日期選擇器。</span><span class="sxs-lookup"><span data-stu-id="de529-180">For example, a `mailto:` link can be created for `DataType.EmailAddress`, and a date selector can be provided for `DataType.Date` in browsers that support HTML5.</span></span> <span data-ttu-id="de529-181">`DataType` 屬性會發出 HTML 5 瀏覽器了解的 HTML 5 `data-` (讀音 data dash) 屬性。</span><span class="sxs-lookup"><span data-stu-id="de529-181">The `DataType` attributes emit HTML 5 `data-` (pronounced data dash) attributes that HTML 5 browsers can understand.</span></span> <span data-ttu-id="de529-182">`DataType` 屬性**不**會提供任何驗證。</span><span class="sxs-lookup"><span data-stu-id="de529-182">The `DataType` attributes do **not** provide any validation.</span></span>

<span data-ttu-id="de529-183">`DataType.Date` 未指定顯示日期的格式。</span><span class="sxs-lookup"><span data-stu-id="de529-183">`DataType.Date` doesn't specify the format of the date that's displayed.</span></span> <span data-ttu-id="de529-184">根據預設，將依據以伺服器 `CultureInfo` 為基礎的預設格式顯示資料欄位。</span><span class="sxs-lookup"><span data-stu-id="de529-184">By default, the data field is displayed according to the default formats based on the server's `CultureInfo`.</span></span>

<span data-ttu-id="de529-185">`DisplayFormat` 屬性用來明確指定日期格式：</span><span class="sxs-lookup"><span data-stu-id="de529-185">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>

```csharp
[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
public DateTime ReleaseDate { get; set; }
```

<span data-ttu-id="de529-186">`ApplyFormatInEditMode` 設定可指定在文字方塊中顯示值以供編輯時，也應該套用的格式。</span><span class="sxs-lookup"><span data-stu-id="de529-186">The `ApplyFormatInEditMode` setting specifies that the formatting should also be applied when the value is displayed in a text box for editing.</span></span> <span data-ttu-id="de529-187">(您也許不想讓它出現在某些欄位中，例如貨幣值，可能會不希望在文字方塊中出現貨幣符號可進行編輯。)</span><span class="sxs-lookup"><span data-stu-id="de529-187">(You might not want that for some fields — for example, for currency values, you probably don't want the currency symbol in the text box for editing.)</span></span>

<span data-ttu-id="de529-188">您可單獨使用 `DisplayFormat` 屬性，但通常最好是使用 `DataType` 屬性。</span><span class="sxs-lookup"><span data-stu-id="de529-188">You can use the `DisplayFormat` attribute by itself, but it's generally a good idea to use the `DataType` attribute.</span></span> <span data-ttu-id="de529-189">`DataType` 屬性會傳逹資料的語意，而不是在螢幕上呈現資料的方式，並提供下列使用 DisplayFormat 無法取得的優點：</span><span class="sxs-lookup"><span data-stu-id="de529-189">The `DataType` attribute conveys the semantics of the data as opposed to how to render it on a screen, and provides the following benefits that you don't get with DisplayFormat:</span></span>

* <span data-ttu-id="de529-190">瀏覽器可以啟用 HTML5 功能 (例如顯示日曆控制項、適合地區設定的貨幣符號、電子郵件連結等等)。</span><span class="sxs-lookup"><span data-stu-id="de529-190">The browser can enable HTML5 features (for example to show a calendar control, the locale-appropriate currency symbol, email links, etc.)</span></span>

* <span data-ttu-id="de529-191">根據預設，瀏覽器將根據您的地區設定，使用正確的格式呈現資料。</span><span class="sxs-lookup"><span data-stu-id="de529-191">By default, the browser will render data using the correct format based on your locale.</span></span>

* <span data-ttu-id="de529-192">`DataType` 屬性可以讓 MVC 選擇正確的欄位範本來轉譯資料 (如果單獨使用，`DisplayFormat` 會使用字串範本)。</span><span class="sxs-lookup"><span data-stu-id="de529-192">The `DataType` attribute can enable MVC to choose the right field template to render the data (the `DisplayFormat` if used by itself uses the string template).</span></span>

> [!NOTE]
> <span data-ttu-id="de529-193">jQuery 驗證無法用於 `Range` 屬性與 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="de529-193">jQuery validation doesn't work with the `Range` attribute and `DateTime`.</span></span> <span data-ttu-id="de529-194">例如，下列程式碼一律會顯示用戶端驗證錯誤，即使當日期位在指定範圍中也一樣：</span><span class="sxs-lookup"><span data-stu-id="de529-194">For example, the following code will always display a client side validation error, even when the date is in the specified range:</span></span>

```csharp
[Range(typeof(DateTime), "1/1/1966", "1/1/2020")]
   ```

<span data-ttu-id="de529-195">您需要停用 jQuery 日期驗證以使用附帶 `DateTime` 的 `Range` 屬性。</span><span class="sxs-lookup"><span data-stu-id="de529-195">You will need to disable jQuery date validation to use the `Range` attribute with `DateTime`.</span></span> <span data-ttu-id="de529-196">編譯模型中的硬性日期通常不是良好的做法，因此不建議使用 `Range` 屬性和 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="de529-196">It's generally not a good practice to compile hard dates in your models, so using the `Range` attribute and `DateTime` is discouraged.</span></span>

<span data-ttu-id="de529-197">下列程式碼會顯示一行上的結合屬性：</span><span class="sxs-lookup"><span data-stu-id="de529-197">The following code shows combining attributes on one line:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie21/Models/MovieDateRatingDAmult.cs?name=snippet1)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc//sample/MvcMovie/Models/MovieDateRatingDAmult.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="de529-198">在數列的下一個部分中，我們會檢閱應用程式，並對自動產生的 `Details` 和 `Delete` 方法進行一些改良。</span><span class="sxs-lookup"><span data-stu-id="de529-198">In the next part of the series, we'll review the application and make some improvements to the automatically generated `Details` and `Delete` methods.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de529-199">其他資源</span><span class="sxs-lookup"><span data-stu-id="de529-199">Additional resources</span></span>

* [<span data-ttu-id="de529-200">使用表單</span><span class="sxs-lookup"><span data-stu-id="de529-200">Working with Forms</span></span>](xref:mvc/views/working-with-forms)
* [<span data-ttu-id="de529-201">全球化和當地語系化</span><span class="sxs-lookup"><span data-stu-id="de529-201">Globalization and localization</span></span>](xref:fundamentals/localization)
* [<span data-ttu-id="de529-202">標記協助程式簡介</span><span class="sxs-lookup"><span data-stu-id="de529-202">Introduction to Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
* [<span data-ttu-id="de529-203">撰寫標記協助程式</span><span class="sxs-lookup"><span data-stu-id="de529-203">Author Tag Helpers</span></span>](xref:mvc/views/tag-helpers/authoring)
