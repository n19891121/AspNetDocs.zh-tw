---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 頁型號 |微軟文件
author: rick-anderson
description: 在ASP.NET 1.x 中,開發人員可以選擇內聯代碼模型和代碼背後的代碼模型。 代碼後面可以使用 Src attr...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: 6c2435a06d04209db21fb8e075f68ff0b7a9ef7e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542855"
---
# <a name="the-aspnet-20-page-model"></a><span data-ttu-id="4c4ae-104">ASP.NET 2.0 頁型號</span><span class="sxs-lookup"><span data-stu-id="4c4ae-104">The ASP.NET 2.0 Page Model</span></span>

<span data-ttu-id="4c4ae-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4c4ae-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4c4ae-106">在ASP.NET 1.x 中,開發人員可以選擇內聯代碼模型和代碼背後的代碼模型。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-106">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="4c4ae-107">可以使用 Src@Page屬性或 指令的 Code 背後屬性實現代碼後面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-107">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="4c4ae-108">在ASP.NET 2.0中,開發人員在內聯代碼和代碼後面之間仍有選擇,但代碼背後的模型有顯著的增強功能。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-108">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

<span data-ttu-id="4c4ae-109">在ASP.NET 1.x 中,開發人員可以選擇內聯代碼模型和代碼背後的代碼模型。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-109">In ASP.NET 1.x, developers had a choice between an inline code model and a code-behind code model.</span></span> <span data-ttu-id="4c4ae-110">可以使用 Src@Page屬性或 指令的 Code 背後屬性實現代碼後面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-110">Code-behind could be implemented using either the Src attribute or the CodeBehind attribute of the @Page directive.</span></span> <span data-ttu-id="4c4ae-111">在ASP.NET 2.0中,開發人員在內聯代碼和代碼後面之間仍有選擇,但代碼背後的模型有顯著的增強功能。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-111">In ASP.NET 2.0, developers still have a choice between inline code and code-behind, but there have been significant enhancements to the code-behind model.</span></span>

## <a name="improvements-in-the-code-behind-model"></a><span data-ttu-id="4c4ae-112">程式碼後模型的改進</span><span class="sxs-lookup"><span data-stu-id="4c4ae-112">Improvements in the Code-Behind Model</span></span>

<span data-ttu-id="4c4ae-113">為了充分理解ASP.NET 2.0 中代碼背後的更改,最好快速查看模型,因為它存在於ASP.NET 1.x 中。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-113">In order to fully understand the changes in the code-behind model in ASP.NET 2.0, its best to quickly review the model as it existed in ASP.NET 1.x.</span></span>

## <a name="the-code-behind-model-in-aspnet-1x"></a><span data-ttu-id="4c4ae-114">ASP.NET 1.x 中的代碼後模型</span><span class="sxs-lookup"><span data-stu-id="4c4ae-114">The Code-Behind Model in ASP.NET 1.x</span></span>

<span data-ttu-id="4c4ae-115">在ASP.NET 1.x 中,代碼後面模型由 ASPX 檔(Webform)和包含程式設計代碼的代碼後檔組成。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-115">In ASP.NET 1.x, the code-behind model consisted of an ASPX file (the Webform) and a code-behind file containing programming code.</span></span> <span data-ttu-id="4c4ae-116">兩個檔使用 ASPX@Page檔中的指令連接。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-116">The two files were connected using the @Page directive in the ASPX file.</span></span> <span data-ttu-id="4c4ae-117">ASPX 頁面上的每個控制器在代碼後面的檔中都有相應的聲明作為實例變數。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-117">Each control on the ASPX page had a corresponding declaration in the code-behind file as an instance variable.</span></span> <span data-ttu-id="4c4ae-118">代碼背後的檔還包含事件綁定的代碼和 Visual Studio 設計器所需的生成代碼。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-118">The code-behind file also contained code for event binding and generated code necessary for the Visual Studio designer.</span></span> <span data-ttu-id="4c4ae-119">此模型工作相當良好,但由於 ASPX 頁中的每個 ASP.NET 元素都需要代碼背後的檔中的相應代碼,因此代碼和內容沒有真正的分離。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-119">This model worked fairly well, but because every ASP.NET element in the ASPX page required corresponding code in the code-behind file, there was no true separation of code and content.</span></span> <span data-ttu-id="4c4ae-120">例如,如果設計器向 Visual Studio IDE 外部的 ASPX 檔添加了新的伺服器控制項,則應用程式將由於代碼背後的檔中缺少該控制項的聲明而中斷。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-120">For example, if a designer added a new server control to an ASPX file outside of the Visual Studio IDE, the application would break due to the absence of a declaration for that control in the code-behind file.</span></span>

## <a name="the-code-behind-model-in-aspnet-20"></a><span data-ttu-id="4c4ae-121">ASP.NET 2.0 中的代碼後模型</span><span class="sxs-lookup"><span data-stu-id="4c4ae-121">The Code-Behind Model in ASP.NET 2.0</span></span>

<span data-ttu-id="4c4ae-122">ASP.NET 2.0 大大改進了此模型。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-122">ASP.NET 2.0 greatly improves upon this model.</span></span> <span data-ttu-id="4c4ae-123">在 ASP.NET 2.0 中,使用 ASP.NET 2.0 中提供的新*部分類*實現代碼後面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-123">In ASP.NET 2.0, code-behind is implemented using the new *partial classes* provided in ASP.NET 2.0.</span></span> <span data-ttu-id="4c4ae-124">ASP.NET 2.0 中的代碼後面類定義為部分類,這意味著它只包含類定義的一部分。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-124">The code-behind class in ASP.NET 2.0 is defined as a partial class meaning that it contains only part of the class definition.</span></span> <span data-ttu-id="4c4ae-125">類定義的其餘部分由 ASP.NET 2.0 在運行時或使用 ASPX 頁或預編譯網站時動態生成。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-125">The remaining part of the class definition is dynamically generated by ASP.NET 2.0 using the ASPX page at runtime or when the Web site is precompiled.</span></span> <span data-ttu-id="4c4ae-126">代碼背後的檔案和 ASPX 頁之間的連結仍使用 @ Page 指令建立。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-126">The link between the code-behind file and the ASPX page is still established using the @ Page directive.</span></span> <span data-ttu-id="4c4ae-127">但是,ASP.NET 2.0 現在使用 CodeFile 屬性,而不是代碼背後或 Src 屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-127">However, instead of a CodeBehind or Src attribute, ASP.NET 2.0 now uses the CodeFile attribute.</span></span> <span data-ttu-id="4c4ae-128">繼承屬性還用於指定頁面的類名稱。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-128">The Inherits attribute is also used to specify the class name for the page.</span></span>

<span data-ttu-id="4c4ae-129">典型的 @ 頁面指令可能如下所示:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-129">A typical @ Page directive might look like this:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

<span data-ttu-id="4c4ae-130">ASP.NET 2.0 代碼背後的檔中的典型類定義可能如下所示:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-130">A typical class definition in an ASP.NET 2.0 code-behind file might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="4c4ae-131">C# 和 Visual Basic 是當前支援部分類的唯一託管語言。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-131">C# and Visual Basic are the only managed languages that currently support partial classes.</span></span> <span data-ttu-id="4c4ae-132">因此,使用 J# 的開發人員將無法在 ASP.NET 2.0 中使用代碼後面模型。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-132">Therefore, developers using J# will not be able to use the code-behind model in ASP.NET 2.0.</span></span>

<span data-ttu-id="4c4ae-133">新模型增強了代碼背後的模型,因為開發人員現在將具有僅包含他們創建的代碼的代碼檔。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-133">The new model enhances the code-behind model because developers will now have code files that contain only the code that they have created.</span></span> <span data-ttu-id="4c4ae-134">它還提供了代碼和內容的真正分離,因為代碼後面的檔中沒有實例變數聲明。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-134">It also provides for a true separation of code and content because there are no instance variable declarations in the code-behind file.</span></span>

> [!NOTE]
> <span data-ttu-id="4c4ae-135">由於 ASPX 頁的部分類是事件綁定發生的位置,因此 Visual Basic 開發人員可以通過在代碼後面中使用 Handles 關鍵字綁定事件來實現輕微的性能提升。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-135">Because the partial class for the ASPX page is where event binding takes place, Visual Basic developers can realize a slight performance increase by using the Handles keyword in code-behind to bind events.</span></span> <span data-ttu-id="4c4ae-136">C# 沒有等效關鍵字。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-136">C# has no equivalent keyword.</span></span>

## <a name="new--page-directive-attributes"></a><span data-ttu-id="4c4ae-137">新增 = 頁面指令屬性</span><span class="sxs-lookup"><span data-stu-id="4c4ae-137">New @ Page Directive Attributes</span></span>

<span data-ttu-id="4c4ae-138">ASP.NET 2.0 向 @ Page 指令添加了許多新屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-138">ASP.NET 2.0 adds many new attributes to the @ Page directive.</span></span> <span data-ttu-id="4c4ae-139">以下屬性在ASP.NET 2.0 中是新的。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-139">The following attributes are new in ASP.NET 2.0.</span></span>

## <a name="async"></a><span data-ttu-id="4c4ae-140">非同步處理</span><span class="sxs-lookup"><span data-stu-id="4c4ae-140">Async</span></span>

<span data-ttu-id="4c4ae-141">Async 屬性允許您配置要非同步執行的頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-141">The Async attribute allows you to configure page to be executed asynchronously.</span></span> <span data-ttu-id="4c4ae-142">本模組稍後將介紹異步頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-142">Well cover asynchronous pages later in this module.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="4c4ae-143">同步逾時</span><span class="sxs-lookup"><span data-stu-id="4c4ae-143">AsyncTimeout</span></span>

<span data-ttu-id="4c4ae-144">指定非同步頁面的超時。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-144">Specified the timeout for asynchronous pages.</span></span> <span data-ttu-id="4c4ae-145">默認值為 45 秒。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-145">The default is 45 seconds.</span></span>

## <a name="codefile"></a><span data-ttu-id="4c4ae-146">代碼檔案</span><span class="sxs-lookup"><span data-stu-id="4c4ae-146">CodeFile</span></span>

<span data-ttu-id="4c4ae-147">CodeFile 屬性是 Visual Studio 2002/2003 中 CodeForin 屬性的替換。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-147">The CodeFile attribute is the replacement for the CodeBehind attribute in Visual Studio 2002/2003.</span></span>

### <a name="codefilebaseclass"></a><span data-ttu-id="4c4ae-148">程式碼檔案基礎類別</span><span class="sxs-lookup"><span data-stu-id="4c4ae-148">CodeFileBaseClass</span></span>

<span data-ttu-id="4c4ae-149">在希望多個頁面從單個基類派生的情況下,使用 CodeFileBaseClass 屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-149">The CodeFileBaseClass attribute is used in cases where you want multiple pages to derive from a single base class.</span></span> <span data-ttu-id="4c4ae-150">由於在ASP.NET中實現部分類,如果沒有此屬性,使用共用公共欄位引用在 ASPX 頁中聲明的控制項的基類將無法正常工作,因為 ASP.NETs 編譯引擎將根據頁面中的控件自動創建新成員。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-150">Because of the implementation of partial classes in ASP.NET, without this attribute, a base class that uses shared common fields to reference controls declared in an ASPX page would not work properly because ASP.NETs compilation engine will automatically create new members based on controls in the page.</span></span> <span data-ttu-id="4c4ae-151">因此,如果要在ASP.NET中為兩個或多個頁面定義一個公共基類,則需要在CodeFileBaseClass 屬性中定義指定基類,然後從該基類派生每個頁面類。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-151">Therefore, if you want a common base class for two or more pages in ASP.NET, you will need to define specify your base class in the CodeFileBaseClass attribute and then derive each pages class from that base class.</span></span> <span data-ttu-id="4c4ae-152">使用此屬性時,也需要 CodeFile 屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-152">The CodeFile attribute is also required when this attribute is used.</span></span>

## <a name="compilationmode"></a><span data-ttu-id="4c4ae-153">編譯模式</span><span class="sxs-lookup"><span data-stu-id="4c4ae-153">CompilationMode</span></span>

<span data-ttu-id="4c4ae-154">此屬性允許您設置 ASPX 頁的編譯模式屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-154">This attribute allows you to set the CompilationMode property of the ASPX page.</span></span> <span data-ttu-id="4c4ae-155">"編譯模式"屬性是包含值 **"始終**、**自動**"和 **"從不"** 的枚舉。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-155">The CompilationMode property is an enumeration containing the values **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="4c4ae-156">默認值為 **「始終**」。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-156">The default is **Always**.</span></span> <span data-ttu-id="4c4ae-157">如果可能,**自動**設置將阻止ASP.NET動態編譯頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-157">The **Auto** setting will prevent ASP.NET from dynamically compiling the page if possible.</span></span> <span data-ttu-id="4c4ae-158">從動態編譯中排除頁面可提高性能。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-158">Excluding pages from dynamic compilation increases performance.</span></span> <span data-ttu-id="4c4ae-159">但是,如果排除的頁面包含必須編譯的代碼,則在流覽頁面時將引發錯誤。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-159">However, if a page that is excluded contains that code that must be compiled, an error will be thrown when the page is browsed.</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="4c4ae-160">開啟事件驗證</span><span class="sxs-lookup"><span data-stu-id="4c4ae-160">EnableEventValidation</span></span>

<span data-ttu-id="4c4ae-161">此屬性指定是否驗證回退和回調事件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-161">This attribute specifies whether or not postback and callback events are validated.</span></span> <span data-ttu-id="4c4ae-162">啟用此功能後,將檢查用於回退或回調事件的參數,以確保它們源自最初呈現這些事件的伺服器控制項。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-162">When this is enabled, arguments to postback or callback events are checked to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="4c4ae-163">啟用"啟用"</span><span class="sxs-lookup"><span data-stu-id="4c4ae-163">EnableTheming</span></span>

<span data-ttu-id="4c4ae-164">此屬性指定ASP.NET主題是否在頁面上使用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-164">This attribute specifies whether or not ASP.NET themes are used on a page.</span></span> <span data-ttu-id="4c4ae-165">預設值為**false**。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-165">The default is **false**.</span></span> <span data-ttu-id="4c4ae-166">ASP.NET主題在第[10單元](profiles-themes-and-web-parts.md)中介紹。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-166">ASP.NET themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="linepragmas"></a><span data-ttu-id="4c4ae-167">線普拉格瑪斯</span><span class="sxs-lookup"><span data-stu-id="4c4ae-167">LinePragmas</span></span>

<span data-ttu-id="4c4ae-168">此屬性指定是否應在編譯期間添加行雜注。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-168">This attribute specifies whether line pragmas should be added during compilation.</span></span> <span data-ttu-id="4c4ae-169">行雜注是調試器用於標記代碼特定部分的選項。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-169">Line pragmas are options used by debuggers to mark specific sections of code.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="4c4ae-170">保持捲動位置後回</span><span class="sxs-lookup"><span data-stu-id="4c4ae-170">MaintainScrollPositionOnPostback</span></span>

<span data-ttu-id="4c4ae-171">此屬性指定是否將 JAVAScript 注入頁面以保持回退之間的滾動位置。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-171">This attribute specifies whether or not JavaScript is injected into the page in order to maintain scroll position between postbacks.</span></span> <span data-ttu-id="4c4ae-172">默認情況下,此屬性**為 false。**</span><span class="sxs-lookup"><span data-stu-id="4c4ae-172">This attribute is **false** by default.</span></span>

<span data-ttu-id="4c4ae-173">當此屬性為**true**時,ASP.NET&lt;將在&gt;回退後添加如下所示的腳本塊:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-173">When this attribute is **true**, ASP.NET will add a &lt;script&gt; block on postback that looks like this:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

<span data-ttu-id="4c4ae-174">請注意,此腳本塊的 src 是 WebResource.axd。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-174">Note that the src for this script block is WebResource.axd.</span></span> <span data-ttu-id="4c4ae-175">此資源不是物理路徑。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-175">This resource is not a physical path.</span></span> <span data-ttu-id="4c4ae-176">請求此文本時,ASP.NET動態生成腳本。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-176">When this script is requested, ASP.NET dynamically builds the script.</span></span>

### <a name="masterpagefile"></a><span data-ttu-id="4c4ae-177">母版頁面檔案</span><span class="sxs-lookup"><span data-stu-id="4c4ae-177">MasterPageFile</span></span>

<span data-ttu-id="4c4ae-178">此屬性指定目前的頁面的主頁檔。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-178">This attribute specifies the master page file for the current page.</span></span> <span data-ttu-id="4c4ae-179">路徑可為相對路徑或絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-179">The path can be relative or absolute.</span></span> <span data-ttu-id="4c4ae-180">母版頁在[單元 4](master-pages.md)中介紹。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-180">Master pages are covered in [Module 4](master-pages.md).</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="4c4ae-181">樣式表主題</span><span class="sxs-lookup"><span data-stu-id="4c4ae-181">StyleSheetTheme</span></span>

<span data-ttu-id="4c4ae-182">此屬性允許您覆蓋由ASP.NET 2.0 主題定義的使用者介面外觀屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-182">This attribute allows you to override user-interface appearance properties defined by an ASP.NET 2.0 theme.</span></span> <span data-ttu-id="4c4ae-183">主題在第[10 單元](profiles-themes-and-web-parts.md)中介紹。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-183">Themes are covered in [Module 10](profiles-themes-and-web-parts.md).</span></span>

## <a name="theme"></a><span data-ttu-id="4c4ae-184">佈景主題</span><span class="sxs-lookup"><span data-stu-id="4c4ae-184">Theme</span></span>

<span data-ttu-id="4c4ae-185">指定頁面的主題。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-185">Specifies the theme for the page.</span></span> <span data-ttu-id="4c4ae-186">如果未為 StyleSheetTheme 屬性指定值,則主題屬性將覆蓋應用於頁面上控制件的所有樣式。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-186">If a value is not specified for the StyleSheetTheme attribute, the Theme attribute overrides all styles applied to controls on the page.</span></span>

## <a name="title"></a><span data-ttu-id="4c4ae-187">Title</span><span class="sxs-lookup"><span data-stu-id="4c4ae-187">Title</span></span>

<span data-ttu-id="4c4ae-188">設置頁面的標題。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-188">Sets the title for the page.</span></span> <span data-ttu-id="4c4ae-189">這裡指定的值會顯示在呈現頁面&lt;的標題&gt;元素中。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-189">The value specified here will appear in the &lt;title&gt; element of the rendered page.</span></span>

### <a name="viewstateencryptionmode"></a><span data-ttu-id="4c4ae-190">檢視狀態加密模式</span><span class="sxs-lookup"><span data-stu-id="4c4ae-190">ViewStateEncryptionMode</span></span>

<span data-ttu-id="4c4ae-191">設置檢視狀態加密模式枚舉的值。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-191">Sets the value for the ViewStateEncryptionMode enumeration.</span></span> <span data-ttu-id="4c4ae-192">可用值為 **「始終**、**自動**」和 **「從不**」。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-192">The available values are **Always**, **Auto**, and **Never**.</span></span> <span data-ttu-id="4c4ae-193">默認值為 **"自動**"。當此屬性設置為 **「自動」** 的值時,檢視狀態被加密是控制項透過調用**註冊需求視點狀態加密**方法請求它。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-193">The default value is **Auto**. When this attribute is set to a value of **Auto**, viewstate is encrypted is a control requests it by calling the **RegisterRequiresViewStateEncryption** method.</span></span>

## <a name="setting-public-property-values-via-the--page-directive"></a><span data-ttu-id="4c4ae-194">透過 @ 頁面指令設定公共財產值</span><span class="sxs-lookup"><span data-stu-id="4c4ae-194">Setting Public Property Values via the @ Page Directive</span></span>

<span data-ttu-id="4c4ae-195">ASP.NET 2.0 中 @ Page 指令的另一個新功能是設置基類公共屬性的初始值的能力。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-195">Another new capability of the @ Page directive in ASP.NET 2.0 is the ability to set the initial value of public properties of a base class.</span></span> <span data-ttu-id="4c4ae-196">例如,假設您的基類中具有名為 **「SomeText」** 的公共屬性,並且您希望在載入頁面時將其初始化為**Hello。**</span><span class="sxs-lookup"><span data-stu-id="4c4ae-196">Suppose, for example, that you have a public property called **SomeText** in your base class and you d like it to be initialized to **Hello** when a page is loaded.</span></span> <span data-ttu-id="4c4ae-197">只設定值值在 @ Page 指令中設定值即可實現此目的:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-197">You can accomplish this by simply setting the value in the @ Page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

<span data-ttu-id="4c4ae-198">@Page 指令的 **「一些文字」** 屬性將基類別中的「SomeText」屬性的初始值設定為*Hello!*。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-198">The **SomeText** attribute of the @ Page directive sets the initial value of the SomeText property in the base class to *Hello!*.</span></span> <span data-ttu-id="4c4ae-199">以下視訊是使用 @ Page 指令設定基類別中公共屬性的初始值的演練。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-199">The video below is a walkthrough of setting the initial value of a public property in a base class using the @ Page directive.</span></span>

![](the-asp-net-2-0-page-model/_static/image1.png)

[<span data-ttu-id="4c4ae-200">開啟全螢幕視訊</span><span class="sxs-lookup"><span data-stu-id="4c4ae-200">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a><span data-ttu-id="4c4ae-201">頁面類別的新公共屬性</span><span class="sxs-lookup"><span data-stu-id="4c4ae-201">New Public Properties of the Page Class</span></span>

<span data-ttu-id="4c4ae-202">以下公共屬性是 ASP.NET 2.0 中的新屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-202">The following public properties are new in ASP.NET 2.0.</span></span>

## <a name="apprelativetemplatesourcedirectory"></a><span data-ttu-id="4c4ae-203">套用相關樣本來源目錄</span><span class="sxs-lookup"><span data-stu-id="4c4ae-203">AppRelativeTemplateSourceDirectory</span></span>

<span data-ttu-id="4c4ae-204">返回與應用程式相關的路徑到頁面或控制項。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-204">Returns the application-relative path to the page or control.</span></span> <span data-ttu-id="4c4ae-205">例如,對於位於的http://app/folder/page.aspx頁面,屬性返回 \*/資料夾/。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-205">For example, for a page located at http://app/folder/page.aspx, the property returns ~/folder/.</span></span>

## <a name="apprelativevirtualpath"></a><span data-ttu-id="4c4ae-206">套用相對虛擬路徑</span><span class="sxs-lookup"><span data-stu-id="4c4ae-206">AppRelativeVirtualPath</span></span>

<span data-ttu-id="4c4ae-207">將相對虛擬目錄路徑返回到頁面或控制項。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-207">Returns the relative virtual directory path to the page or control.</span></span> <span data-ttu-id="4c4ae-208">例如,對於位於的http://app/folder/page.aspx頁面,屬性返回 \*/資料夾/頁.aspx。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-208">For example for a page located at http://app/folder/page.aspx, the property returns ~/folder/page.aspx.</span></span>

## <a name="asynctimeout"></a><span data-ttu-id="4c4ae-209">同步逾時</span><span class="sxs-lookup"><span data-stu-id="4c4ae-209">AsyncTimeout</span></span>

<span data-ttu-id="4c4ae-210">獲取或設置用於異步頁面處理的超時。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-210">Gets or sets the timeout used for asynchronous page handling.</span></span> <span data-ttu-id="4c4ae-211">(此模組稍後將介紹異步頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-211">(Asynchronous pages will be covered later in this module.)</span></span>

## <a name="clientquerystring"></a><span data-ttu-id="4c4ae-212">客戶端查詢字串</span><span class="sxs-lookup"><span data-stu-id="4c4ae-212">ClientQueryString</span></span>

<span data-ttu-id="4c4ae-213">返回請求網址的查詢字串部分的唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-213">A read-only property that returns the query string portion of the requested URL.</span></span> <span data-ttu-id="4c4ae-214">此值是 URL 編碼的。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-214">This value is URL encoded.</span></span> <span data-ttu-id="4c4ae-215">您可以使用 Hthterver 實用程式類的網址解碼方法對其進行解碼。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-215">You can use the UrlDecode method of the HttpServerUtility class to decode it.</span></span>

## <a name="clientscript"></a><span data-ttu-id="4c4ae-216">用戶端文稿</span><span class="sxs-lookup"><span data-stu-id="4c4ae-216">ClientScript</span></span>

<span data-ttu-id="4c4ae-217">此屬性返回一個用戶端ScriptManager物件,該物件可用於管理用戶端腳本的ASP.NET發射。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-217">This property returns a ClientScriptManager object that can be used to manage ASP.NETs emission of client-side script.</span></span> <span data-ttu-id="4c4ae-218">(本模組稍後將介紹用戶端腳本管理器類。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-218">(The ClientScriptManager class is covered later in this module.)</span></span>

## <a name="enableeventvalidation"></a><span data-ttu-id="4c4ae-219">開啟事件驗證</span><span class="sxs-lookup"><span data-stu-id="4c4ae-219">EnableEventValidation</span></span>

<span data-ttu-id="4c4ae-220">此屬性控制是否為回退和回調事件啟用事件驗證。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-220">This property controls whether or not event validation is enabled for postback and callback events.</span></span> <span data-ttu-id="4c4ae-221">啟用後,將驗證用於回退或回調事件的參數,以確保它們源自最初呈現這些事件的伺服器控制件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-221">When enabled, arguments to postback or callback events are verified to ensure that they originated from the server control that originally rendered them.</span></span>

## <a name="enabletheming"></a><span data-ttu-id="4c4ae-222">啟用"啟用"</span><span class="sxs-lookup"><span data-stu-id="4c4ae-222">EnableTheming</span></span>

<span data-ttu-id="4c4ae-223">此屬性獲取或設置布林,用於指定ASP.NET 2.0 主題是否應用於頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-223">This property gets or sets a Boolean that specifies whether or not an ASP.NET 2.0 theme applies to the page.</span></span>

## <a name="form"></a><span data-ttu-id="4c4ae-224">表單</span><span class="sxs-lookup"><span data-stu-id="4c4ae-224">Form</span></span>

<span data-ttu-id="4c4ae-225">此屬性將 ASPX 頁上的 HTML 窗體作為 HtmlForm 物件返回。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-225">This property returns the HTML form on the ASPX page as an HtmlForm object.</span></span>

## <a name="header"></a><span data-ttu-id="4c4ae-226">頁首</span><span class="sxs-lookup"><span data-stu-id="4c4ae-226">Header</span></span>

<span data-ttu-id="4c4ae-227">此屬性返回對包含頁面標題的 HtmlHead 物件的引用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-227">This property returns a reference to an HtmlHead object that contains the page header.</span></span> <span data-ttu-id="4c4ae-228">您可以使用傳回的 HtmlHead 物件獲取/設定樣式表、符標記等。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-228">You can use the returned HtmlHead object to get/set style sheets, Meta tags, etc.</span></span>

## <a name="idseparator"></a><span data-ttu-id="4c4ae-229">IdSe 參數</span><span class="sxs-lookup"><span data-stu-id="4c4ae-229">IdSeparator</span></span>

<span data-ttu-id="4c4ae-230">當ASP.NET為頁面上的控制項建構唯一ID時,此唯讀屬性獲取用於分隔控制項識別碼的字元。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-230">This read-only property gets the character that is used to separate control identifiers when ASP.NET is building a unique ID for controls on a page.</span></span> <span data-ttu-id="4c4ae-231">但並不是針對直接從程式碼使用而設計。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-231">It is not intended to be used directly from your code.</span></span>

## <a name="isasync"></a><span data-ttu-id="4c4ae-232">IsAsync</span><span class="sxs-lookup"><span data-stu-id="4c4ae-232">IsAsync</span></span>

<span data-ttu-id="4c4ae-233">此屬性允許異步頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-233">This property allows for asynchronous pages.</span></span> <span data-ttu-id="4c4ae-234">本模組稍後將討論異步頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-234">Asynchronous pages are discussed later in this module.</span></span>

## <a name="iscallback"></a><span data-ttu-id="4c4ae-235">IsCallback</span><span class="sxs-lookup"><span data-stu-id="4c4ae-235">IsCallback</span></span>

<span data-ttu-id="4c4ae-236">如果頁面是回電的結果,則此唯讀屬性將**返回 true。**</span><span class="sxs-lookup"><span data-stu-id="4c4ae-236">This read-only property returns **true** if the page is the result of a call back.</span></span> <span data-ttu-id="4c4ae-237">本模組稍後將討論回電。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-237">Call backs are discussed later in this module.</span></span>

## <a name="iscrosspagepostback"></a><span data-ttu-id="4c4ae-238">是交叉頁面後傳回</span><span class="sxs-lookup"><span data-stu-id="4c4ae-238">IsCrossPagePostBack</span></span>

<span data-ttu-id="4c4ae-239">如果頁面是跨頁回郵的一部分,則此唯讀屬性將**返回 true。**</span><span class="sxs-lookup"><span data-stu-id="4c4ae-239">This read-only property returns **true** if the page is part of a cross-page postback.</span></span> <span data-ttu-id="4c4ae-240">本模組稍後將介紹跨頁回郵。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-240">Cross-page postbacks are covered later in this module.</span></span>

## <a name="items"></a><span data-ttu-id="4c4ae-241">項目</span><span class="sxs-lookup"><span data-stu-id="4c4ae-241">Items</span></span>

<span data-ttu-id="4c4ae-242">返回對 I字典實例的引用,該實例包含存儲在頁面上下文中的所有物件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-242">Returns a reference to an IDictionary instance that contains all objects stored in the pages context.</span></span> <span data-ttu-id="4c4ae-243">您可以將項添加到此 I字典物件,它們將在上下文的整個生存期內可供您使用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-243">You can add items to this IDictionary object and they will be available to you throughout the lifetime of the context.</span></span>

## <a name="maintainscrollpositiononpostback"></a><span data-ttu-id="4c4ae-244">保持捲動位置後回</span><span class="sxs-lookup"><span data-stu-id="4c4ae-244">MaintainScrollPositionOnPostBack</span></span>

<span data-ttu-id="4c4ae-245">此屬性控制ASP.NET是否發出 JavaScript,該 JavaScript 在回退後在瀏覽器中維護頁面滾動位置。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-245">This property controls whether or not ASP.NET emits JavaScript that maintains the pages scroll position in the browser after a postback occurs.</span></span> <span data-ttu-id="4c4ae-246">(本模組前面討論了此屬性的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-246">(Details of this property were discussed earlier in this module.)</span></span>

## <a name="master"></a><span data-ttu-id="4c4ae-247">Master</span><span class="sxs-lookup"><span data-stu-id="4c4ae-247">Master</span></span>

<span data-ttu-id="4c4ae-248">此唯讀屬性返回對已應用母版頁的頁面的 MasterPage 實例的引用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-248">This read-only property returns a reference to the MasterPage instance for a page to which a master page has been applied.</span></span>

## <a name="masterpagefile"></a><span data-ttu-id="4c4ae-249">母版頁面檔案</span><span class="sxs-lookup"><span data-stu-id="4c4ae-249">MasterPageFile</span></span>

<span data-ttu-id="4c4ae-250">獲取或設置頁面的主頁檔名。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-250">Gets or sets the master page filename for the page.</span></span> <span data-ttu-id="4c4ae-251">此屬性只能在 PreInit 方法中設置。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-251">This property can only be set in the PreInit method.</span></span>

## <a name="maxpagestatefieldlength"></a><span data-ttu-id="4c4ae-252">最大頁面狀態長度</span><span class="sxs-lookup"><span data-stu-id="4c4ae-252">MaxPageStateFieldLength</span></span>

<span data-ttu-id="4c4ae-253">此屬性獲取或設置以位元組為單位的頁面狀態的最大長度。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-253">This property gets or sets the maximum length for the pages state in bytes.</span></span> <span data-ttu-id="4c4ae-254">如果屬性設置為正數,則頁面視圖狀態將分解為多個隱藏欄位,以便不超過指定的位元組數。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-254">If the property is set to a positive number, the pages view state will be broken up into multiple hidden fields so that it doesnt exceed the number of bytes specified.</span></span> <span data-ttu-id="4c4ae-255">如果屬性為負數,則視圖狀態不會分解為塊。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-255">If the property is a negative number, the view state will not be broken into chunks.</span></span>

## <a name="pageadapter"></a><span data-ttu-id="4c4ae-256">頁面配接器</span><span class="sxs-lookup"><span data-stu-id="4c4ae-256">PageAdapter</span></span>

<span data-ttu-id="4c4ae-257">返回對 PageAdapter 物件的引用,該物件修改請求流覽器的頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-257">Returns a reference to the PageAdapter object that modifies the page for the requesting browser.</span></span>

## <a name="previouspage"></a><span data-ttu-id="4c4ae-258">上一頁</span><span class="sxs-lookup"><span data-stu-id="4c4ae-258">PreviousPage</span></span>

<span data-ttu-id="4c4ae-259">在伺服器.傳輸或跨頁回發的情況下返回對上一頁的引用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-259">Returns a reference to the previous page in cases of a Server.Transfer or a cross-page postback.</span></span>

## <a name="skinid"></a><span data-ttu-id="4c4ae-260">皮膚代碼</span><span class="sxs-lookup"><span data-stu-id="4c4ae-260">SkinID</span></span>

<span data-ttu-id="4c4ae-261">指定要應用於頁面的ASP.NET 2.0 外觀。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-261">Specifies the ASP.NET 2.0 skin to apply to the page.</span></span>

## <a name="stylesheettheme"></a><span data-ttu-id="4c4ae-262">樣式表主題</span><span class="sxs-lookup"><span data-stu-id="4c4ae-262">StyleSheetTheme</span></span>

<span data-ttu-id="4c4ae-263">此屬性獲取或設置應用於頁面的樣式表。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-263">This property gets or sets the style sheet that is applied to a page.</span></span>

## <a name="templatecontrol"></a><span data-ttu-id="4c4ae-264">樣本控制</span><span class="sxs-lookup"><span data-stu-id="4c4ae-264">TemplateControl</span></span>

<span data-ttu-id="4c4ae-265">返回對頁面的包含控制項的引用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-265">Returns a reference to the containing control for the page.</span></span>

## <a name="theme"></a><span data-ttu-id="4c4ae-266">佈景主題</span><span class="sxs-lookup"><span data-stu-id="4c4ae-266">Theme</span></span>

<span data-ttu-id="4c4ae-267">獲取或設置應用於頁面的ASP.NET 2.0 主題的名稱。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-267">Gets or sets the name of the ASP.NET 2.0 theme applied to the page.</span></span> <span data-ttu-id="4c4ae-268">此值必須在 PreInit 方法之前設置。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-268">This value must be set prior to the PreInit method.</span></span>

## <a name="title"></a><span data-ttu-id="4c4ae-269">Title</span><span class="sxs-lookup"><span data-stu-id="4c4ae-269">Title</span></span>

<span data-ttu-id="4c4ae-270">此屬性獲取或設置從頁眉獲取的頁面的標題。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-270">This property gets or sets the title for the page as obtained from the pages header.</span></span>

## <a name="viewstateencryptionmode"></a><span data-ttu-id="4c4ae-271">檢視狀態加密模式</span><span class="sxs-lookup"><span data-stu-id="4c4ae-271">ViewStateEncryptionMode</span></span>

<span data-ttu-id="4c4ae-272">獲取或設定頁面的 ViewState 加密模式。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-272">Gets or sets the ViewStateEncryptionMode of the page.</span></span> <span data-ttu-id="4c4ae-273">在本模組前面查看對此屬性的詳細討論。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-273">See a detailed discussion of this property earlier in this module.</span></span>

## <a name="new-protected-properties-of-the-page-class"></a><span data-ttu-id="4c4ae-274">頁面類別的新受保護屬性</span><span class="sxs-lookup"><span data-stu-id="4c4ae-274">New Protected Properties of the Page Class</span></span>

<span data-ttu-id="4c4ae-275">以下是 ASP.NET 2.0 中 Page 類的新受保護屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-275">The following are the new protected properties of the Page class in ASP.NET 2.0.</span></span>

## <a name="adapter"></a><span data-ttu-id="4c4ae-276">配接器</span><span class="sxs-lookup"><span data-stu-id="4c4ae-276">Adapter</span></span>

<span data-ttu-id="4c4ae-277">返回對在請求該頁面的設備上呈現該頁的 ControlAdapter 的引用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-277">Returns a reference to the ControlAdapter that renders the page on the device that requested it.</span></span>

## <a name="asyncmode"></a><span data-ttu-id="4c4ae-278">非同步模式</span><span class="sxs-lookup"><span data-stu-id="4c4ae-278">AsyncMode</span></span>

<span data-ttu-id="4c4ae-279">此屬性指示頁面是否非同步處理。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-279">This property indicates whether or not the page is processed asynchronously.</span></span> <span data-ttu-id="4c4ae-280">它供運行時使用,而不是直接在代碼中使用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-280">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="clientidseparator"></a><span data-ttu-id="4c4ae-281">用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="4c4ae-281">ClientIDSeparator</span></span>

<span data-ttu-id="4c4ae-282">此屬性返回在為控制項創建唯一客戶端 ID 時用作分隔符的字元。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-282">This property returns the character used as a separator when creating unique client IDs for controls.</span></span> <span data-ttu-id="4c4ae-283">它供運行時使用,而不是直接在代碼中使用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-283">It is intended for use by the runtime and not directly in code.</span></span>

## <a name="pagestatepersister"></a><span data-ttu-id="4c4ae-284">佩奇·邦斯特</span><span class="sxs-lookup"><span data-stu-id="4c4ae-284">PageStatePersister</span></span>

<span data-ttu-id="4c4ae-285">此屬性返回頁面的 Page StatePersister 物件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-285">This property returns the PageStatePersister object for the page.</span></span> <span data-ttu-id="4c4ae-286">此屬性主要由ASP.NET控件開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-286">This property is primarily used by ASP.NET control developers.</span></span>

## <a name="uniquefilepathsuffix"></a><span data-ttu-id="4c4ae-287">唯一的檔案路徑修復</span><span class="sxs-lookup"><span data-stu-id="4c4ae-287">UniqueFilePathSuffix</span></span>

<span data-ttu-id="4c4ae-288">此屬性返回一個唯一的後綴,該後綴追加到緩存瀏覽器的檔路徑上。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-288">This property returns a unique suffix that is appended to the file path for caching browsers.</span></span> <span data-ttu-id="4c4ae-289">預設值為\_\_ufps\* 和 6 位元數位。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-289">The default value is \_\_ufps= and a 6-digit number.</span></span>

## <a name="new-public-methods-for-the-page-class"></a><span data-ttu-id="4c4ae-290">頁面類別的新公共方法</span><span class="sxs-lookup"><span data-stu-id="4c4ae-290">New Public Methods for the Page Class</span></span>

<span data-ttu-id="4c4ae-291">以下公共方法是 ASP.NET 2.0 中的 Page 類的新增方法。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-291">The following public methods are new to the Page class in ASP.NET 2.0.</span></span>

## <a name="addonprerendercompleteasync"></a><span data-ttu-id="4c4ae-292">額外預先成同步</span><span class="sxs-lookup"><span data-stu-id="4c4ae-292">AddOnPreRenderCompleteAsync</span></span>

<span data-ttu-id="4c4ae-293">此方法註冊事件處理程式委託以進行非同步頁面執行。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-293">This method registers event handler delegates for asynchronous page execution.</span></span> <span data-ttu-id="4c4ae-294">本模組稍後將討論異步頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-294">Asynchronous pages are discussed later in this module.</span></span>

## <a name="applystylesheetskin"></a><span data-ttu-id="4c4ae-295">套用樣式表外觀</span><span class="sxs-lookup"><span data-stu-id="4c4ae-295">ApplyStyleSheetSkin</span></span>

<span data-ttu-id="4c4ae-296">將頁面樣式表中的屬性應用於頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-296">Applies the properties in a pages style sheet to the page.</span></span>

## <a name="executeregisteredasynctasks"></a><span data-ttu-id="4c4ae-297">執行已註冊的同步工作</span><span class="sxs-lookup"><span data-stu-id="4c4ae-297">ExecuteRegisteredAsyncTasks</span></span>

<span data-ttu-id="4c4ae-298">此方法是異步任務。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-298">This method beings an asynchronous task.</span></span>

### <a name="getvalidators"></a><span data-ttu-id="4c4ae-299">取得驗證器</span><span class="sxs-lookup"><span data-stu-id="4c4ae-299">GetValidators</span></span>

<span data-ttu-id="4c4ae-300">如果未指定任何驗證組或默認驗證組,則返回驗證器的集合。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-300">Returns a collection of validators for the specified validation group or the default validation group if none is specified.</span></span>

## <a name="registerasynctask"></a><span data-ttu-id="4c4ae-301">註冊同步工作</span><span class="sxs-lookup"><span data-stu-id="4c4ae-301">RegisterAsyncTask</span></span>

<span data-ttu-id="4c4ae-302">此方法註冊新的異步任務。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-302">This method registers a new async task.</span></span> <span data-ttu-id="4c4ae-303">本模組稍後將介紹異步頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-303">Asynchronous pages are covered later in this module.</span></span>

## <a name="registerrequirescontrolstate"></a><span data-ttu-id="4c4ae-304">註冊需要控制狀態</span><span class="sxs-lookup"><span data-stu-id="4c4ae-304">RegisterRequiresControlState</span></span>

<span data-ttu-id="4c4ae-305">此方法告訴ASP.NET必須保留頁面控件狀態。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-305">This method tells ASP.NET that the pages control state must be persisted.</span></span>

## <a name="registerrequiresviewstateencryption"></a><span data-ttu-id="4c4ae-306">註冊需要檢視狀態加密</span><span class="sxs-lookup"><span data-stu-id="4c4ae-306">RegisterRequiresViewStateEncryption</span></span>

<span data-ttu-id="4c4ae-307">此方法告訴ASP.NET頁面檢視狀態需要加密。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-307">This method tells ASP.NET that the pages viewstate requires encryption.</span></span>

## <a name="resolveclienturl"></a><span data-ttu-id="4c4ae-308">解析用戶端</span><span class="sxs-lookup"><span data-stu-id="4c4ae-308">ResolveClientUrl</span></span>

<span data-ttu-id="4c4ae-309">返回可用於圖像等用戶端請求的相對 URL。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-309">Returns a relative URL that can be used for client requests for images, etc.</span></span>

## <a name="setfocus"></a><span data-ttu-id="4c4ae-310">SetFocus</span><span class="sxs-lookup"><span data-stu-id="4c4ae-310">SetFocus</span></span>

<span data-ttu-id="4c4ae-311">此方法將焦點設置為最初載入頁面時指定的控制項。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-311">This method will set the focus to the control that is specified when the page is initially loaded.</span></span>

## <a name="unregisterrequirescontrolstate"></a><span data-ttu-id="4c4ae-312">取消註冊需要控制狀態</span><span class="sxs-lookup"><span data-stu-id="4c4ae-312">UnregisterRequiresControlState</span></span>

<span data-ttu-id="4c4ae-313">此方法將取消註冊傳遞給它的控制項,因為不再需要控制項狀態持久性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-313">This method will unregister the control that is passed to it as no longer requiring control state persistence.</span></span>

## <a name="changes-to-the-page-lifecycle"></a><span data-ttu-id="4c4ae-314">變更頁面生命循環</span><span class="sxs-lookup"><span data-stu-id="4c4ae-314">Changes to the Page Lifecycle</span></span>

<span data-ttu-id="4c4ae-315">ASP.NET 2.0 中的頁面生命週期沒有顯著變化,但您應該知道一些新方法。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-315">The page lifecycle in ASP.NET 2.0 hasn't changed dramatically, but there are some new methods that you should be aware of.</span></span> <span data-ttu-id="4c4ae-316">下面概述了ASP.NET 2.0 頁生命週期。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-316">The ASP.NET 2.0 page lifecycle is outlined below.</span></span>

## <a name="preinit-new-in-aspnet-20"></a><span data-ttu-id="4c4ae-317">PreInit(ASP.NET 2.0 中的新增功能)</span><span class="sxs-lookup"><span data-stu-id="4c4ae-317">PreInit (New in ASP.NET 2.0)</span></span>

<span data-ttu-id="4c4ae-318">PreInit 事件是開發人員可以訪問的生命週期中最早的階段。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-318">The PreInit event is the earliest stage in the lifecycle that a developer can access.</span></span> <span data-ttu-id="4c4ae-319">通過添加此事件,可以以程式設計方式更改ASP.NET 2.0 主題、母版頁、ASP.NET 2.0 配置檔的訪問屬性等。如果您處於後回狀態,則實現Viewstate尚未應用於生命週期的此時控件非常重要。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-319">The addition of this event makes it possible to programmatically change ASP.NET 2.0 themes, master pages, access properties for an ASP.NET 2.0 profile, etc. If you are in a postback state, its important to realize that Viewstate has not yet been applied to controls at this point in the lifecycle.</span></span> <span data-ttu-id="4c4ae-320">因此,如果開發人員在此階段更改控件的屬性,則在頁面生命週期的稍後版本中可能會覆蓋該控制項的屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-320">Therefore, if a developer changes a property of a control at this stage, it will likely be overwritten later in the pages lifecycle.</span></span>

## <a name="init"></a><span data-ttu-id="4c4ae-321">Init</span><span class="sxs-lookup"><span data-stu-id="4c4ae-321">Init</span></span>

<span data-ttu-id="4c4ae-322">Init 事件未從 ASP.NET 1.x 更改。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-322">The Init event has not changed from ASP.NET 1.x.</span></span> <span data-ttu-id="4c4ae-323">這是您希望讀取或初始化頁面上控制項屬性的位置。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-323">This is where you would want to read or initialize properties of controls on your page.</span></span> <span data-ttu-id="4c4ae-324">在此階段,母版頁、主題等已應用於該頁。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-324">At this stage, master pages, themes, etc. are already applied to the page.</span></span>

## <a name="initcomplete-new-in-20"></a><span data-ttu-id="4c4ae-325">InitComplete(2.0 新增)</span><span class="sxs-lookup"><span data-stu-id="4c4ae-325">InitComplete (New in 2.0)</span></span>

<span data-ttu-id="4c4ae-326">InitComplete 事件在頁面初始化階段結束時調用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-326">The InitComplete event is called at the end of the pages initialization stage.</span></span> <span data-ttu-id="4c4ae-327">在生命週期的此時,可以訪問頁面上的控件,但尚未填充其狀態。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-327">At this point in the lifecycle, you can access controls on the page, but their state has not yet been populated.</span></span>

## <a name="preload-new-in-20"></a><span data-ttu-id="4c4ae-328">預載入(2.0 中新增)</span><span class="sxs-lookup"><span data-stu-id="4c4ae-328">PreLoad (New in 2.0)</span></span>

<span data-ttu-id="4c4ae-329">此事件是在應用所有回郵數據后,並在頁面\_載入之前調用的。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-329">This event is called after all postback data has been applied and just prior to Page\_Load.</span></span>

## <a name="load"></a><span data-ttu-id="4c4ae-330">載入</span><span class="sxs-lookup"><span data-stu-id="4c4ae-330">Load</span></span>

<span data-ttu-id="4c4ae-331">載入事件未從 ASP.NET 1.x 更改。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-331">The Load event has not changed from ASP.NET 1.x.</span></span>

## <a name="loadcomplete-new-in-20"></a><span data-ttu-id="4c4ae-332">載入完成(2.0 中新增)</span><span class="sxs-lookup"><span data-stu-id="4c4ae-332">LoadComplete (New in 2.0)</span></span>

<span data-ttu-id="4c4ae-333">LoadComplete 事件是頁面載入階段的最後一個事件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-333">The LoadComplete event is the last event in the pages load stage.</span></span> <span data-ttu-id="4c4ae-334">在此階段,所有回退和視圖狀態數據已應用於頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-334">At this stage, all postback and viewstate data has been applied to the page.</span></span>

## <a name="prerender"></a><span data-ttu-id="4c4ae-335">預算</span><span class="sxs-lookup"><span data-stu-id="4c4ae-335">PreRender</span></span>

<span data-ttu-id="4c4ae-336">如果希望對動態添加到頁面的控制項正確維護檢視狀態,則 PreRender 事件是添加它們的最後機會。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-336">If you would like for viewstate to be properly maintained for controls that are added to the page dynamically, the PreRender event is the last opportunity to add them.</span></span>

## <a name="prerendercomplete-new-in-20"></a><span data-ttu-id="4c4ae-337">預成成成(2.0中新增)</span><span class="sxs-lookup"><span data-stu-id="4c4ae-337">PreRenderComplete (New in 2.0)</span></span>

<span data-ttu-id="4c4ae-338">在預渲染完成階段,所有控制項都已添加到頁面,並且頁面已準備好呈現。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-338">At the PreRenderComplete stage, all controls have been added to the page and the page is ready to be rendered.</span></span> <span data-ttu-id="4c4ae-339">預渲染完成事件是保存頁面檢視狀態之前引發的最後一個事件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-339">The PreRenderComplete event is the last event raised before the pages viewstate is saved.</span></span>

## <a name="savestatecomplete-new-in-20"></a><span data-ttu-id="4c4ae-340">儲存狀態完成(2.0 中的新增功能)</span><span class="sxs-lookup"><span data-stu-id="4c4ae-340">SaveStateComplete (New in 2.0)</span></span>

<span data-ttu-id="4c4ae-341">保存所有頁面檢視狀態和控制狀態后,將立即調用"保存狀態完成"事件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-341">The SaveStateComplete event is called immediately after all page viewstate and control state has been saved.</span></span> <span data-ttu-id="4c4ae-342">這是頁面實際呈現到瀏覽器之前的最後一個事件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-342">This is the last event before the page is actually rendered to the browser.</span></span>

## <a name="render"></a><span data-ttu-id="4c4ae-343">轉譯</span><span class="sxs-lookup"><span data-stu-id="4c4ae-343">Render</span></span>

<span data-ttu-id="4c4ae-344">自 1.x ASP.NET 以來,渲染方法未更改。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-344">The Render method has not changed since ASP.NET 1.x.</span></span> <span data-ttu-id="4c4ae-345">這是 HtmlTextWriter 初始化並將頁面呈現到瀏覽器的位置。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-345">This is where the HtmlTextWriter is initialized and the page is rendered to the browser.</span></span>

## <a name="cross-page-postback-in-aspnet-20"></a><span data-ttu-id="4c4ae-346">ASP.NET 2.0 中的跨頁回郵</span><span class="sxs-lookup"><span data-stu-id="4c4ae-346">Cross-Page Postback in ASP.NET 2.0</span></span>

<span data-ttu-id="4c4ae-347">在ASP.NET 1.x 中,需要回郵後貼到同一頁。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-347">In ASP.NET 1.x, postbacks were required to post to the same page.</span></span> <span data-ttu-id="4c4ae-348">不允許進行跨頁回郵。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-348">Cross-page postbacks were not allowed.</span></span> <span data-ttu-id="4c4ae-349">ASP.NET 2.0 添加了透過 IButtonControl 介面發回其他頁面的功能。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-349">ASP.NET 2.0 adds the ability to post back to a different page via the IButtonControl interface.</span></span> <span data-ttu-id="4c4ae-350">實現新的 IButtonControl 介面的任何控制項(除了第三方自定義控制件之外,還可以利用此新功能,使用 PostBackUrl 屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-350">Any control that implements the new IButtonControl interface (Button, LinkButton, and ImageButton in addition to third-party custom controls) can take advantage of this new functionality via the use of the PostBackUrl attribute.</span></span> <span data-ttu-id="4c4ae-351">以下代碼顯示將回發回第二頁的 Button 控制件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-351">The following code shows a Button control that posts back to a second page.</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

<span data-ttu-id="4c4ae-352">當頁面被發回時,啟動回郵的頁面可通過第二頁上的「上頁」屬性訪問。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-352">When the page is posted back, the Page that initiates the postback is accessible via the PreviousPage property on the second page.</span></span> <span data-ttu-id="4c4ae-353">此功能通過新的 WebForm\_DoPostBackOptions 用戶端功能實現,該功能 ASP.NET 2.0 在控制項回退回其他頁面時呈現到頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-353">This functionality is implemented via the new WebForm\_DoPostBackWithOptions client-side function that ASP.NET 2.0 renders to the page when a control posts back to a different page.</span></span> <span data-ttu-id="4c4ae-354">此 JAVAScript 函數由向用戶端發出腳本的新 WebResource.axd 處理程式提供。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-354">This JavaScript function is provided by the new WebResource.axd handler which emits script to the client.</span></span>

<span data-ttu-id="4c4ae-355">下面的視頻是跨頁回帖的演練。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-355">The video below is a walkthrough of a cross-page postback.</span></span>

![](the-asp-net-2-0-page-model/_static/image2.png)

[<span data-ttu-id="4c4ae-356">開啟全螢幕視訊</span><span class="sxs-lookup"><span data-stu-id="4c4ae-356">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a><span data-ttu-id="4c4ae-357">有關跨頁回郵的更多詳細資訊</span><span class="sxs-lookup"><span data-stu-id="4c4ae-357">More Details on Cross-Page Postbacks</span></span>

### <a name="viewstate"></a><span data-ttu-id="4c4ae-358">檢視狀態</span><span class="sxs-lookup"><span data-stu-id="4c4ae-358">Viewstate</span></span>

<span data-ttu-id="4c4ae-359">您可能已經問自己,在跨頁回退方案中,從第一頁中查看狀態會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-359">You may have asked yourself already about what happens to the viewstate from the first page in a cross-page postback scenario.</span></span> <span data-ttu-id="4c4ae-360">畢竟,任何不實現 IPostBackDataHandler 的控制項都將透過檢視狀態保持其狀態,因此,要造訪跨頁後回的第二頁上該控制項的屬性,您必須有權訪問該頁的視圖狀態。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-360">After all, any control that does not implement IPostBackDataHandler will persist its state via viewstate, so to have access to the properties of that control on the second page of a cross-page postback, you must have access to the viewstate for the page.</span></span> <span data-ttu-id="4c4ae-361">ASP.NET 2.0 使用第二頁\_\_中稱為 「上頁」的新隱藏欄位處理此方案。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-361">ASP.NET 2.0 takes care of this scenario using a new hidden field in the second page called \_\_PREVIOUSPAGE.</span></span> <span data-ttu-id="4c4ae-362">「\_\_上一頁」 的檢視狀態,以便您可以存取第二頁中所有控制項的屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-362">The \_\_PREVIOUSPAGE form field contains the viewstate for the first page so that you can have access to the properties of all controls in the second page.</span></span>

### <a name="circumventing-findcontrol"></a><span data-ttu-id="4c4ae-363">繞過尋找控制</span><span class="sxs-lookup"><span data-stu-id="4c4ae-363">Circumventing FindControl</span></span>

<span data-ttu-id="4c4ae-364">在跨頁回發的影片演練中,我使用 FindControl 方法獲取對第一頁上的 TextBox 控制件的引用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-364">In the video walkthrough of a cross-page postback, I used the FindControl method to get a reference to the TextBox control on the first page.</span></span> <span data-ttu-id="4c4ae-365">該方法適用於此目的,但 FindControl 成本高昂,需要編寫其他代碼。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-365">That method works well for that purpose, but FindControl is expensive and it requires writing additional code.</span></span> <span data-ttu-id="4c4ae-366">幸運的是,ASP.NET 2.0 為此提供了 FindControl 的替代方法,這在很多方案中都不起作用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-366">Fortunately, ASP.NET 2.0 provides an alternative to FindControl for this purpose that will work in many scenarios.</span></span> <span data-ttu-id="4c4ae-367">使用「上一頁類型」指令允許您使用 TypeName 或 VirtualPath 屬性對上一頁進行強類型引用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-367">The PreviousPageType directive allows you to have a strongly-typed reference to the previous page by using either the TypeName or the VirtualPath attribute.</span></span> <span data-ttu-id="4c4ae-368">TypeName 屬性允許您指定上一頁的類型,而 VirtualPath 屬性允許您使用虛擬路徑引用上一頁。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-368">The TypeName attribute allows you to specify the type of the previous page while the VirtualPath attribute allows you to refer to the previous page using a virtual path.</span></span> <span data-ttu-id="4c4ae-369">設置上一頁類型指令後,必須公開要允許使用公共屬性訪問的控制項等。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-369">After you've set the PreviousPageType directive, you must then expose the controls, etc. to which you want to allow access using public properties.</span></span>

## <a name="lab-1-cross-page-postback"></a><span data-ttu-id="4c4ae-370">實驗室 1 跨頁回郵</span><span class="sxs-lookup"><span data-stu-id="4c4ae-370">Lab 1 Cross-Page Postback</span></span>

<span data-ttu-id="4c4ae-371">在本實驗中,您將創建一個應用程式,該應用程式使用ASP.NET2.0的新跨頁回郵功能。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-371">In this lab, you will create an application that uses the new cross-page postback functionality of ASP.NET 2.0.</span></span>

1. <span data-ttu-id="4c4ae-372">打開 Visual Studio 2005 並創建新 ASP.NET 網站。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-372">Open Visual Studio 2005 and create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="4c4ae-373">添加新的 Web 表單,稱為頁 2.aspx。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-373">Add a new Webform called page2.aspx.</span></span>
3. <span data-ttu-id="4c4ae-374">在「設計」檢視中打開預設.aspx 並添加按鈕控制項和 TextBox 控制件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-374">Open the Default.aspx in Design view and add a Button control and a TextBox control.</span></span> 

    1. <span data-ttu-id="4c4ae-375">為按鈕控制項指定 **「提交按鈕**」的 ID,而文字框控制件為**使用者名**ID。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-375">Give the Button control an ID of **SubmitButton** and the TextBox control an ID of **UserName**.</span></span>
    2. <span data-ttu-id="4c4ae-376">將按鈕的 PostBackUrl 屬性設置為頁 2.aspx。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-376">Set the PostBackUrl property of the Button to page2.aspx.</span></span>
4. <span data-ttu-id="4c4ae-377">在源檢視中打開頁面 2.aspx。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-377">Open page2.aspx in Source view.</span></span>
5. <span data-ttu-id="4c4ae-378">新增 # 上一頁類型指令,如下所示:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-378">Add a @ PreviousPageType directive as shown below:</span></span>
6. <span data-ttu-id="4c4ae-379">將以下代碼加入頁面 2.aspx 的代碼後面的\_頁面 載入:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-379">Add the following code to the Page\_Load of page2.aspx's code-behind:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. <span data-ttu-id="4c4ae-380">單擊"生成"功能表上的"生成"功能表生成專案。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-380">Build the project by clicking on Build on the Build menu.</span></span>
8. <span data-ttu-id="4c4ae-381">將以下代碼加入 Default.aspx 的代碼後面:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-381">Add the following code to the code-behind for Default.aspx:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. <span data-ttu-id="4c4ae-382">將頁\_2.aspx 中的頁面載入變更為以下內容:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-382">Change the Page\_Load in page2.aspx to the following:</span></span> 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. <span data-ttu-id="4c4ae-383">建置專案。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-383">Build the project.</span></span>
11. <span data-ttu-id="4c4ae-384">執行專案。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-384">Run the project.</span></span>
12. <span data-ttu-id="4c4ae-385">在文字框中輸入您的姓名,然後按一下這個按鈕。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-385">Enter your name in the TextBox and click the button.</span></span>
13. <span data-ttu-id="4c4ae-386">結果如何?</span><span class="sxs-lookup"><span data-stu-id="4c4ae-386">What is the result?</span></span>

## <a name="asynchronous-pages-in-aspnet-20"></a><span data-ttu-id="4c4ae-387">ASP.NET 2.0 中的非同步頁面</span><span class="sxs-lookup"><span data-stu-id="4c4ae-387">Asynchronous Pages in ASP.NET 2.0</span></span>

<span data-ttu-id="4c4ae-388">ASP.NET中的許多爭用問題是由外部調用(如 Web 服務或資料庫調用)的延遲、檔 IO 延遲等引起的。當針對ASP.NET應用程式發出請求時,ASP.NET使用其工作線程之一來為該請求提供服務。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-388">Many contention problems in ASP.NET are caused by latency of external calls (such as Web service or database calls), file IO latency, etc. When a request is made against an ASP.NET application, ASP.NET uses one of its worker threads to service that request.</span></span> <span data-ttu-id="4c4ae-389">該請求擁有該線程,直到請求完成並發送回應。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-389">That request owns that thread until the request is complete and the response has been sent.</span></span> <span data-ttu-id="4c4ae-390">ASP.NET 2.0 尋求通過添加非同步執行頁面的功能來解決此類問題的延遲問題。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-390">ASP.NET 2.0 seeks to resolve latency issues with these types of issues by adding the capability to execute pages asynchronously.</span></span> <span data-ttu-id="4c4ae-391">這意味著工作線程可以啟動請求,然後將其他執行交給另一個線程,從而快速返回到可用的線程池。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-391">That means that a worker thread can start the request and then hand off additional execution to another thread, thereby returning to the available thread pool quickly.</span></span> <span data-ttu-id="4c4ae-392">當檔 IO、資料庫調用等完成時,將從線程池獲取一個新線程以完成請求。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-392">When the file IO, database call, etc. has completed, a new thread is obtained from the thread pool to finish the request.</span></span>

<span data-ttu-id="4c4ae-393">使頁面非同步執行的第一步是設定頁面指令的**Async**屬性,如下所示:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-393">The first step in making a page execute asynchronously is to set the **Async** attribute of the page directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

<span data-ttu-id="4c4ae-394">此屬性告訴ASP.NET實現頁面的IHttpAsyncHandler。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-394">This attribute tells ASP.NET to implement the IHttpAsyncHandler for the page.</span></span>

<span data-ttu-id="4c4ae-395">下一步是在預渲染之前在頁面生命週期的某一點調用 AddOnPreRenderCompleteAsync 方法。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-395">The next step is to call the AddOnPreRenderCompleteAsync method at a point in the lifecycle of the page prior to PreRender.</span></span> <span data-ttu-id="4c4ae-396">(此方法通常在頁面\_載入中呼叫。AddOnPreRenderCompleteasync方法採用兩個參數;a BeginEventHandler 和 endEventHandler。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-396">(This method is typically called in Page\_Load.) The AddOnPreRenderCompleteAsync method takes two parameters; a BeginEventHandler and an EndEventHandler.</span></span> <span data-ttu-id="4c4ae-397">BeginEventHandler 傳回 IAsyncResult,然後將該結果作為參數傳遞給 EndEventHandler。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-397">The BeginEventHandler returns an IAsyncResult which is then passed as a parameter to the EndEventHandler.</span></span>

<span data-ttu-id="4c4ae-398">下面的視頻是異步頁面請求的演練。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-398">The video below is a walkthrough of an asynchronous page request.</span></span>

![](the-asp-net-2-0-page-model/_static/image3.png)

[<span data-ttu-id="4c4ae-399">開啟全螢幕視訊</span><span class="sxs-lookup"><span data-stu-id="4c4ae-399">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> <span data-ttu-id="4c4ae-400">在結束事件處理程式完成之前,非同步頁面不會呈現給瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-400">An async page does not render to the browser until the EndEventHandler has completed.</span></span> <span data-ttu-id="4c4ae-401">毫無疑問,但一些開發人員會認為非同步請求類似於異步回調。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-401">No doubt but that some developers will think of async requests as being similar to async callbacks.</span></span> <span data-ttu-id="4c4ae-402">重要的是要意識到他們不是。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-402">It's important to realize that they are not.</span></span> <span data-ttu-id="4c4ae-403">非同步請求的好處是,可以將第一個輔助線程返回到線程池以服務新請求,從而減少由於受 IO 綁定等原因引起的爭用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-403">The benefit to asynchronous requests is that the first worker thread can be returned to the thread pool to service new requests, thereby reducing contention due to being IO bound, etc.</span></span>

## <a name="script-callbacks-in-aspnet-20"></a><span data-ttu-id="4c4ae-404">ASP.NET 2.0 中的文本回調</span><span class="sxs-lookup"><span data-stu-id="4c4ae-404">Script Callbacks in ASP.NET 2.0</span></span>

<span data-ttu-id="4c4ae-405">Web 開發人員一直在尋找防止與回調關聯的閃爍的方法。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-405">Web developers have always looked for ways to prevent the flickering associated with a callback.</span></span> <span data-ttu-id="4c4ae-406">在ASP.NET 1.x 中,智慧導航是避免閃爍的最常見方法,但智慧導航由於在用戶端上實現的複雜性而給一些開發人員帶來了問題。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-406">In ASP.NET 1.x, SmartNavigation was the most common method for avoiding flickering, but SmartNavigation caused problems for some developers because of the complexity of its implementation on the client.</span></span> <span data-ttu-id="4c4ae-407">ASP.NET 2.0 使用腳本回調解決此問題。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-407">ASP.NET 2.0 addresses this issue with script callbacks.</span></span> <span data-ttu-id="4c4ae-408">文本回調利用 XMLHTTP 通過 JavaScript 對 Web 伺服器發出請求。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-408">Script callbacks utilize XMLHttp to make requests against the Web server via JavaScript.</span></span> <span data-ttu-id="4c4ae-409">XMLHTTP 請求返回 XML 數據,然後可以通過瀏覽器的 DOM 進行操作。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-409">The XMLHttp request returns XML data that can then be manipulated via the browser's DOM.</span></span> <span data-ttu-id="4c4ae-410">XMLHttp 代碼由新的 WebResource.axd 處理程式對使用者隱藏。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-410">XMLHttp code is hidden from the user by the new WebResource.axd handler.</span></span>

<span data-ttu-id="4c4ae-411">為了在 2.0 ASP.NET 配置腳本回調,需要執行幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-411">There are several steps that are necessary in order to configure a script callback in ASP.NET 2.0.</span></span>

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a><span data-ttu-id="4c4ae-412">步驟 1 : 實現 IcallbackEventHandler 介面</span><span class="sxs-lookup"><span data-stu-id="4c4ae-412">Step 1 : Implement the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="4c4ae-413">為了ASP.NET識別您的頁面參與腳本回調,必須實現ICallbackEventHandler介面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-413">In order for ASP.NET to recognize your page as participating in a script callback, you must implement the ICallbackEventHandler interface.</span></span> <span data-ttu-id="4c4ae-414">您可以在代碼後面的檔案中執行此操作,如下所示:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-414">You can do this in your code-behind file like so:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

<span data-ttu-id="4c4ae-415">您還可以使用 # 執行指令執行此操作,如下所示:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-415">You can also do this using the @ Implements directive like so:</span></span>

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

<span data-ttu-id="4c4ae-416">在使用內聯ASP.NET代碼時,通常可以使用 @ 實現指令。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-416">You would typically use the @ Implements directive when using inline ASP.NET code.</span></span>

## <a name="step-2--call-getcallbackeventreference"></a><span data-ttu-id="4c4ae-417">第二步 : 呼叫傳回事件參考</span><span class="sxs-lookup"><span data-stu-id="4c4ae-417">Step 2 : Call GetCallbackEventReference</span></span>

<span data-ttu-id="4c4ae-418">如前所述,XMLHTTP調用封裝在 WebResource.axd 處理程式中。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-418">As mentioned previously, the XMLHttp call is encapsulated in the WebResource.axd handler.</span></span> <span data-ttu-id="4c4ae-419">呈現頁面時,ASP.NET將添加對 WebForm DoCallback\_的調用,WebForm DoCallback 是 WebResource.axd 提供的用戶端腳本。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-419">When your page is rendered, ASP.NET will add a call to WebForm\_DoCallback, a client script that is provided by WebResource.axd.</span></span> <span data-ttu-id="4c4ae-420">WebForm\_DoCallback 函數\_\_將替換 回調的 doPostBack 函數。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-420">The WebForm\_DoCallback function replaces the \_\_doPostBack function for a callback.</span></span> <span data-ttu-id="4c4ae-421">請記住,\_\_以程式設計方式提交頁面上的表單。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-421">Remember that \_\_doPostBack programmatically submits the form on the page.</span></span> <span data-ttu-id="4c4ae-422">在回調方案中,您希望防止回退,因此\_\_PostBack 是不夠的。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-422">In a callback scenario, you want to prevent a postback, so \_\_doPostBack will not suffice.</span></span>

> [!NOTE]
> <span data-ttu-id="4c4ae-423">\_\_doPostBack 仍呈現在用戶端文本回調方案中的頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-423">\_\_doPostBack is still rendered to the page in a client script callback scenario.</span></span> <span data-ttu-id="4c4ae-424">但是,它不用於回調。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-424">However, it's not used for the callback.</span></span>

<span data-ttu-id="4c4ae-425">WebForm\_DoCallback 用戶端函數的參數通過伺服器端函數 GetCallbackEventReference 提供,該函\_數通常在頁面載入中調用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-425">The arguments for the WebForm\_DoCallback client-side function are provided via the server-side function GetCallbackEventReference which would normally be called in Page\_Load.</span></span> <span data-ttu-id="4c4ae-426">對 GetbackEvent 參考的典型調用可能如下所示:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-426">A typical call to GetCallbackEventReference might look like this:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="4c4ae-427">在這種情況下,cm 是用戶端腳本管理器的實例。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-427">In this case, cm is an instance of ClientScriptManager.</span></span> <span data-ttu-id="4c4ae-428">本模組稍後將介紹用戶端腳本管理器類。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-428">The ClientScriptManager class will be covered later in this module.</span></span>

<span data-ttu-id="4c4ae-429">有幾個重載版本的 GetbackEvent 參考。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-429">There are several overloaded versions of GetCallbackEventReference.</span></span> <span data-ttu-id="4c4ae-430">在這種情況下,參數如下所示:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-430">In this case, the arguments are as follows:</span></span>

`this`

<span data-ttu-id="4c4ae-431">對調用 GetbackEvent參照的控制件的引用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-431">A reference to the control where GetCallbackEventReference is being called.</span></span> <span data-ttu-id="4c4ae-432">在這種情況下,它是頁面本身。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-432">In this case, it's the page itself.</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

<span data-ttu-id="4c4ae-433">將從用戶端代碼傳遞到伺服器端事件的字串參數。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-433">A string argument that will be passed from the client-side code to the server-side event.</span></span> <span data-ttu-id="4c4ae-434">在這種情況下,我傳遞名為 ddlCompany 的下拉的值。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-434">In this case, Im passing the value of a dropdown called ddlCompany.</span></span>

`ShowCompanyName`

<span data-ttu-id="4c4ae-435">用戶端函數的名稱,該函數將接受伺服器端回調事件的返回值(作為字串)。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-435">The name of the client-side function that will accept the return value (as string) from the server-side callback event.</span></span> <span data-ttu-id="4c4ae-436">僅當伺服器端回調成功時,才會調用此功能。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-436">This function will only be called when the server-side callback is successful.</span></span> <span data-ttu-id="4c4ae-437">因此,為了魯棒性,通常建議使用重載版本的 GetCallbackEventReference,該版本需要一個額外的字串參數,指定用戶端函數的名稱,在發生錯誤時執行。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-437">Therefore, for the sake of robustness, it is generally recommended to use the overloaded version of GetCallbackEventReference that takes an additional string argument specifying the name of a client-side function to execute in the event of an error.</span></span>

`null`

<span data-ttu-id="4c4ae-438">表示在回調到伺服器之前啟動的用戶端函數的字串。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-438">A string representing a client-side function that it initiated before the callback to the server.</span></span> <span data-ttu-id="4c4ae-439">在這種情況下,沒有這樣的腳本,因此參數為 null。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-439">In this case, there is no such script, so the argument is null.</span></span>

`true`

<span data-ttu-id="4c4ae-440">指定是否非同步執行回調的布林。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-440">A Boolean specifying whether or not to conduct the callback asynchronously.</span></span>

<span data-ttu-id="4c4ae-441">用戶端上對 WebForm\_DoCallback 的調用將傳遞這些參數。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-441">The call to WebForm\_DoCallback on the client will pass these arguments.</span></span> <span data-ttu-id="4c4ae-442">因此,在用戶端上呈現此頁面時,該代碼將如下所示:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-442">Therefore, when this page is rendered on the client, that code will look like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

<span data-ttu-id="4c4ae-443">請注意,用戶端上函數的簽名有點不同。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-443">Notice that the signature of the function on the client is a bit different.</span></span> <span data-ttu-id="4c4ae-444">用戶端函數傳遞 5 個字串和一個布爾。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-444">The client-side function passes 5 strings and a Boolean.</span></span> <span data-ttu-id="4c4ae-445">附加字串(在上例中為空)包含用戶端函數,該函數將處理來自伺服器端回調的任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-445">The additional string (which is null in the above example) contains the client-side function that will handle any errors from the server-side callback.</span></span>

## <a name="step-3--hook-the-client-side-control-event"></a><span data-ttu-id="4c4ae-446">步驟 3 : 鉤用戶端控制事件</span><span class="sxs-lookup"><span data-stu-id="4c4ae-446">Step 3 : Hook the Client-Side Control Event</span></span>

<span data-ttu-id="4c4ae-447">請注意,上面 GetCallbackEventReference 的返回值已分配給字串變數。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-447">Notice that the return value of GetCallbackEventReference above was assigned to a string variable.</span></span> <span data-ttu-id="4c4ae-448">該字串用於鉤接啟動回調的控制項的用戶端事件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-448">That string is used to hook a client-side event for the control that initiates the callback.</span></span> <span data-ttu-id="4c4ae-449">在此示例中,回調由頁面上的下拉展開,因此我想掛接*OnChange*事件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-449">In this example, the callback is initiated by a dropdown on the page, so I want to hook the *OnChange* event.</span></span>

<span data-ttu-id="4c4ae-450">要掛接用戶端事件,只需將處理程式添加到客戶端標記,如下所示:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-450">To hook the client-side event, simply add a handler to the client-side markup as follows:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

<span data-ttu-id="4c4ae-451">回想一下*cbRef*是從調用 GetbackEvent 參考的返回值。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-451">Recall that *cbRef* is the return value from the call to GetCallbackEventReference.</span></span> <span data-ttu-id="4c4ae-452">它包含上面顯示的對 WebForm\_DoCallback 的調用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-452">It contains the call to WebForm\_DoCallback that was shown above.</span></span>

## <a name="step-4--register-the-client-side-script"></a><span data-ttu-id="4c4ae-453">步驟 4 : 註冊用戶端文稿</span><span class="sxs-lookup"><span data-stu-id="4c4ae-453">Step 4 : Register the Client-Side Script</span></span>

<span data-ttu-id="4c4ae-454">回想一下,對 GetCallbackEventReference 的呼叫指定在伺服器端回檔成功時將執行名為**ShowCompanyName**的用戶端文稿。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-454">Recall that the call to GetCallbackEventReference specified that a client-side script called **ShowCompanyName** would be executed when the server-side callback succeeds.</span></span> <span data-ttu-id="4c4ae-455">需要使用 ClientScriptManager 實例將該文本添加到頁面。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-455">That script needs to be added to the page using a ClientScriptManager instance.</span></span> <span data-ttu-id="4c4ae-456">(本模組稍後將討論用戶端腳本管理器類。你這樣做,像這樣:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-456">(The ClientScriptManager class will be discussed later in this module.) You do that like so:</span></span>

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a><span data-ttu-id="4c4ae-457">步驟 5 : 呼叫 ICallbackEventHandler 介面的方法</span><span class="sxs-lookup"><span data-stu-id="4c4ae-457">Step 5 : Call the Methods of the ICallbackEventHandler Interface</span></span>

<span data-ttu-id="4c4ae-458">ICallbackEventHandler 包含需要在代碼中實現的兩種方法。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-458">The ICallbackEventHandler contains two methods that you need to implement in your code.</span></span> <span data-ttu-id="4c4ae-459">它們是 **「提高回調事件**」和 **「獲取回調事件**」。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-459">They are **RaiseCallbackEvent** and **GetCallbackEvent**.</span></span>

<span data-ttu-id="4c4ae-460">**RaiseCallbackEvent**將字串作為參數,不返回任何內容。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-460">**RaiseCallbackEvent** takes a string as an argument and returns nothing.</span></span> <span data-ttu-id="4c4ae-461">字串參數從用戶端呼叫傳遞到 WebForm\_DoCallback。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-461">The string argument is passed from the client-side call to WebForm\_DoCallback.</span></span> <span data-ttu-id="4c4ae-462">在這種情況下,該值是名為 ddlCompany 的下拉*的值*屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-462">In this case, that value is the *value* attribute of the dropdown called ddlCompany.</span></span> <span data-ttu-id="4c4ae-463">伺服器端代碼應放在「提高回調事件」方法中。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-463">Your server-side code should be placed in the RaiseCallbackEvent method.</span></span> <span data-ttu-id="4c4ae-464">例如,如果您的回調針對外部資源發出 Web 請求,則應將該代碼放在「提高回調事件」 中。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-464">For example, if your callback is making a WebRequest against an external resource, that code should be placed in RaiseCallbackEvent.</span></span>

<span data-ttu-id="4c4ae-465">**GetCallbackEvent**負責處理回調返回給客戶端的問題。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-465">**GetCallbackEvent** is responsible for processing the return of the callback to the client.</span></span> <span data-ttu-id="4c4ae-466">它不需要參數並返回字串。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-466">It takes no arguments and returns a string.</span></span> <span data-ttu-id="4c4ae-467">傳回的字串會傳回為參數傳回客戶端函數,在本例*中為 ShowCompanyName*。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-467">The string that it returns will be passed as an argument to the client-side function, in this case *ShowCompanyName*.</span></span>

<span data-ttu-id="4c4ae-468">完成上述步驟後,即可在 2.0 ASP.NET 執行腳本回調。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-468">Once you have completed the above steps, you are ready to perform a script callback in ASP.NET 2.0.</span></span>

![](the-asp-net-2-0-page-model/_static/image4.png)

[<span data-ttu-id="4c4ae-469">開啟全螢幕視訊</span><span class="sxs-lookup"><span data-stu-id="4c4ae-469">Open Full-Screen Video</span></span>](the-asp-net-2-0-page-model/_static/callback1.wmv)

<span data-ttu-id="4c4ae-470">ASP.NET文稿回調在支援進行 XMLHTTP 調用的任何瀏覽器中都受支援。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-470">Script callbacks in ASP.NET are supported in any browser that supports making XMLHttp calls.</span></span> <span data-ttu-id="4c4ae-471">這包括當今使用的所有現代瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-471">That includes all of the modern browsers in use today.</span></span> <span data-ttu-id="4c4ae-472">Internet Explorer 使用 XMLHttp ActiveX 物件,而其他現代瀏覽器(包括即將推出的 IE 7)使用內部 XMLHTTP 物件。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-472">Internet Explorer uses the XMLHttp ActiveX object while other modern browsers (including the upcoming IE 7) use an intrinsic XMLHttp object.</span></span> <span data-ttu-id="4c4ae-473">要以程式設計方式確定瀏覽器是否支援回調,可以使用 **「請求.Browser.支援回撥」** 屬性。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-473">To programmatically determine if a browser supports callbacks, you can use the **Request.Browser.SupportCallback** property.</span></span> <span data-ttu-id="4c4ae-474">如果請求的用戶端支援腳本回調,則此屬性將返回**true。**</span><span class="sxs-lookup"><span data-stu-id="4c4ae-474">This property will return **true** if the requesting client supports script callbacks.</span></span>

## <a name="working-with-client-script-in-aspnet-20"></a><span data-ttu-id="4c4ae-475">在 ASP.NET 2.0 中使用用戶端文稿</span><span class="sxs-lookup"><span data-stu-id="4c4ae-475">Working with Client Script in ASP.NET 2.0</span></span>

<span data-ttu-id="4c4ae-476">ASP.NET 2.0 中的用戶端腳本是使用用戶端腳本管理員類管理的。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-476">Client scripts in ASP.NET 2.0 are managed via the use of the ClientScriptManager class.</span></span> <span data-ttu-id="4c4ae-477">用戶端文稿管理器類使用類型和名稱跟蹤用戶端腳本。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-477">The ClientScriptManager class keeps track of client scripts using a type and a name.</span></span> <span data-ttu-id="4c4ae-478">這樣可以防止同一腳本多次以程式設計方式插入到頁面上。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-478">This prevents the same script from being programmatically inserted on a page more than once.</span></span>

> [!NOTE]
> <span data-ttu-id="4c4ae-479">在頁面上成功註冊腳本后,任何後續註冊同一腳本的嘗試都將導致腳本無法第二次註冊。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-479">After a script has been successfully registered on a page, any subsequent attempt to register the same script will simply result in the script not being registered a second time.</span></span> <span data-ttu-id="4c4ae-480">不添加重複的腳本,也不會發生異常。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-480">No duplicate scripts are added and no exception occurs.</span></span> <span data-ttu-id="4c4ae-481">為了避免不必要的計算,可以使用一些方法來確定腳本是否已註冊,以便不要嘗試多次註冊腳本。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-481">To avoid unnecessary computation, there are methods that you can use to determine if a script is already registered so that you do not attempt to register it more than once.</span></span>

<span data-ttu-id="4c4ae-482">用戶端文本管理員的方法應對所有當前ASP.NET開發人員都熟悉:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-482">The methods of the ClientScriptManager should be familiar to all current ASP.NET developers:</span></span>

## <a name="registerclientscriptblock"></a><span data-ttu-id="4c4ae-483">註冊用戶端文稿塊</span><span class="sxs-lookup"><span data-stu-id="4c4ae-483">RegisterClientScriptBlock</span></span>

<span data-ttu-id="4c4ae-484">此方法將腳本添加到呈現頁面的頂部。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-484">This method adds a script to the top of the rendered page.</span></span> <span data-ttu-id="4c4ae-485">這對於添加將在用戶端上顯式調用的函數非常有用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-485">This is useful for adding functions that will be explicitly called on the client.</span></span>

<span data-ttu-id="4c4ae-486">此方法有兩個重載版本。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-486">There are two overloaded versions of this method.</span></span> <span data-ttu-id="4c4ae-487">四個參數中有三個在它們中很常見。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-487">Three of four arguments are common among them.</span></span> <span data-ttu-id="4c4ae-488">其中包括：</span><span class="sxs-lookup"><span data-stu-id="4c4ae-488">They are:</span></span>

`type (string)`

<span data-ttu-id="4c4ae-489">***類型***參數標識腳本的類型。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-489">The ***type*** argument identifies a type for the script.</span></span> <span data-ttu-id="4c4ae-490">通常最好使用頁面的類型(這。獲取類型的類型。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-490">It is generally a good idea to use the page's type (this.GetType()) for the type.</span></span>

`key (string)`

<span data-ttu-id="4c4ae-491">***鍵***參數是腳本的使用者定義的密鑰。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-491">The ***key*** argument is a user-defined key for the script.</span></span> <span data-ttu-id="4c4ae-492">對於每個腳本來說,這應該是唯一的。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-492">This should be unique for each script.</span></span> <span data-ttu-id="4c4ae-493">如果嘗試添加具有相同鍵和已添加腳本類型的腳本,則不會添加該腳本。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-493">If you attempt to add a script with the same key and type of an already added script, it will not be added.</span></span>

`script (string)`

<span data-ttu-id="4c4ae-494">***文本***參數是包含要添加的實際文本的字串。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-494">The ***script*** argument is a string containing the actual script to add.</span></span> <span data-ttu-id="4c4ae-495">建議使用 StringBuilder 創建腳本,然後在 StringBuilder 上使用 ToString() 方法分配***腳本***參數。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-495">It's recommended that you use a StringBuilder to create the script and then use the ToString() method on the StringBuilder to assign the ***script*** argument.</span></span>

<span data-ttu-id="4c4ae-496">如果使用載入的註冊用戶端腳本塊,該參數僅包含三個參數,則必須在腳本中包含腳本元素&lt;&gt;(&lt;腳&gt;本 和 /腳本)。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-496">If you use the overloaded RegisterClientScriptBlock that only takes three arguments, you must include script elements (&lt;script&gt; and &lt;/script&gt;) in your script.</span></span>

<span data-ttu-id="4c4ae-497">您可以選擇使用採用第四個參數的註冊用戶端腳本塊的重載。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-497">You may choose to use the overload of RegisterClientScriptBlock that takes a fourth argument.</span></span> <span data-ttu-id="4c4ae-498">第四個參數是布爾,它指定ASP.NET是否應該為您添加腳本元素。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-498">The fourth argument is a Boolean that specifies whether or not ASP.NET should add script elements for you.</span></span> <span data-ttu-id="4c4ae-499">如果此參數**為 true,** 則文本不應顯式包含文稿元素。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-499">If this argument is **true**, your script should not include the script elements explicitly.</span></span>

<span data-ttu-id="4c4ae-500">使用 IsClientScriptBlock 註冊方法確定腳本是否已註冊。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-500">Use the IsClientScriptBlockRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="4c4ae-501">這允許您避免嘗試重新註冊已註冊的腳本。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-501">This allows you to avoid an attempt to re-register a script that has already been registered.</span></span>

### <a name="registerclientscriptinclude-new-in-20"></a><span data-ttu-id="4c4ae-502">註冊用戶端文稿包括(2.0 中的新增功能)</span><span class="sxs-lookup"><span data-stu-id="4c4ae-502">RegisterClientScriptInclude (New in 2.0)</span></span>

<span data-ttu-id="4c4ae-503">註冊用戶端文稿包含標記創建連結到外部文稿檔的腳本塊。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-503">The RegisterClientScriptInclude tag creates a script block that links to an external script file.</span></span> <span data-ttu-id="4c4ae-504">它有兩個過載。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-504">It has two overloads.</span></span> <span data-ttu-id="4c4ae-505">一個需要一個鍵和一個URL。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-505">One takes a key and a URL.</span></span> <span data-ttu-id="4c4ae-506">第二個參數添加第三個參數,指定類型。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-506">The second adds a third argument specifying the type.</span></span>

<span data-ttu-id="4c4ae-507">例如,以下代碼產生一個腳本塊,該文本塊連結到應用程式文本資料夾的根目錄中的 js 函數.js:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-507">For example, the following code generates a script block that links to jsfunctions.js in the root of the scripts folder of the application:</span></span>

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

<span data-ttu-id="4c4ae-508">此代碼在呈現的頁面中產生以下代碼:</span><span class="sxs-lookup"><span data-stu-id="4c4ae-508">This code produces the following code in the rendered page:</span></span>

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> <span data-ttu-id="4c4ae-509">腳本塊呈現在頁面底部。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-509">The script block is rendered at the bottom of the page.</span></span>

<span data-ttu-id="4c4ae-510">使用 IsClientScript 包括註冊方法確定文本是否已註冊。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-510">Use the IsClientScriptIncludeRegistered method to determine if a script has already been registered.</span></span> <span data-ttu-id="4c4ae-511">這允許您避免嘗試重新註冊腳本。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-511">This allows you to avoid an attempt to re-register a script.</span></span>

## <a name="registerstartupscript"></a><span data-ttu-id="4c4ae-512">註冊啟動文稿</span><span class="sxs-lookup"><span data-stu-id="4c4ae-512">RegisterStartupScript</span></span>

<span data-ttu-id="4c4ae-513">註冊啟動腳本方法採用與註冊用戶端腳本塊方法相同的參數。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-513">The RegisterStartupScript method takes the same arguments as the RegisterClientScriptBlock method.</span></span> <span data-ttu-id="4c4ae-514">註冊到註冊啟動腳本的腳本在頁面載入後在 OnLoad 用戶端事件之前執行。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-514">A script registered with RegisterStartupScript executes after the page loads but before the OnLoad client-side event.</span></span> <span data-ttu-id="4c4ae-515">在 1.X 中,註冊&lt;到的 腳本位於關閉&gt;/窗體 標記之前,而註冊到 RegisterClientScriptBlock&lt;的腳&gt;本則緊隨打開 表單 標記之後放置。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-515">In 1.X, scripts registered with RegisterStartupScript were placed just before the closing &lt;/form&gt; tag while scripts registered with RegisterClientScriptBlock were placed immediately after the opening &lt;form&gt; tag.</span></span> <span data-ttu-id="4c4ae-516">在 ASP.NET 2.0 中,兩&lt;者&gt;都放在 關閉 /窗體標記之前。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-516">In ASP.NET 2.0, both are placed immediately before the closing &lt;/form&gt; tag.</span></span>

> [!NOTE]
> <span data-ttu-id="4c4ae-517">如果向註冊啟動腳本註冊函數,則在客戶端代碼中顯式調用該函數之前,該函數不會執行。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-517">If you register a function with RegisterStartupScript, that function will not execute until you explicitly call it in client-side code.</span></span>

<span data-ttu-id="4c4ae-518">使用 IsStartupScript 註冊方法確定腳本是否已註冊,並避免嘗試重新註冊腳本。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-518">Use the IsStartupScriptRegistered method to determine if a script has already been registered and avoid an attempt to re-register a script.</span></span>

## <a name="other-clientscriptmanager-methods"></a><span data-ttu-id="4c4ae-519">其他用戶端文稿管理員方法</span><span class="sxs-lookup"><span data-stu-id="4c4ae-519">Other ClientScriptManager Methods</span></span>

<span data-ttu-id="4c4ae-520">下面是用戶端ScriptManager 類的其他一些有用方法。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-520">Here are some of the other useful methods of the ClientScriptManager class.</span></span>

|  <span data-ttu-id="4c4ae-521"><strong>取得回撥事件參考</strong></span><span class="sxs-lookup"><span data-stu-id="4c4ae-521"><strong>GetCallbackEventReference</strong></span></span>   |                                                 <span data-ttu-id="4c4ae-522">請參閱本模組前面的腳本回調。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-522">See script callbacks earlier in this module.</span></span>                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <span data-ttu-id="4c4ae-523"><strong>取得後回用戶端超連結</strong></span><span class="sxs-lookup"><span data-stu-id="4c4ae-523"><strong>GetPostBackClientHyperlink</strong></span></span>  |                <span data-ttu-id="4c4ae-524">獲取可用於從用戶端事件發回的 JavaScript 引用&lt;(javascript:&gt;呼叫 )。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-524">Gets a JavaScript reference (javascript:&lt;call&gt;) that can be used to post back from a client-side event.</span></span>                 |
|  <span data-ttu-id="4c4ae-525"><strong>取得後回活動參考</strong></span><span class="sxs-lookup"><span data-stu-id="4c4ae-525"><strong>GetPostBackEventReference</strong></span></span>   |                                   <span data-ttu-id="4c4ae-526">獲取可用於從用戶端發起回帖子的字串。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-526">Gets a string that can be used to initiate a post back from the client.</span></span>                                    |
|      <span data-ttu-id="4c4ae-527"><strong>取得 Web 資源網址</strong></span><span class="sxs-lookup"><span data-stu-id="4c4ae-527"><strong>GetWebResourceUrl</strong></span></span>       | <span data-ttu-id="4c4ae-528">返回嵌入在程式集中的資源的 URL。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-528">Returns a URL to a resource that is embedded in an assembly.</span></span> <span data-ttu-id="4c4ae-529">必須與<strong>註冊用戶端腳本資源</strong>結合使用。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-529">Must be used in conjunction with <strong>RegisterClientScriptResource</strong>.</span></span> |
| <span data-ttu-id="4c4ae-530"><strong>註冊用戶端文稿資源</strong></span><span class="sxs-lookup"><span data-stu-id="4c4ae-530"><strong>RegisterClientScriptResource</strong></span></span> |     <span data-ttu-id="4c4ae-531">將 Web 資源註冊到該頁。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-531">Registers a Web resource with the page.</span></span> <span data-ttu-id="4c4ae-532">這些資源嵌入到程式集中並由新的 WebResource.axd 處理程式處理。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-532">These are resources embedded in an assembly and handled by the new WebResource.axd handler.</span></span>      |
|     <span data-ttu-id="4c4ae-533"><strong>註冊隱藏欄位</strong></span><span class="sxs-lookup"><span data-stu-id="4c4ae-533"><strong>RegisterHiddenField</strong></span></span>      |                                                 <span data-ttu-id="4c4ae-534">將隱藏的表單欄段與頁面註冊。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-534">Registers a hidden form field with the page.</span></span>                                                 |
|  <span data-ttu-id="4c4ae-535"><strong>註冊提交聲明</strong></span><span class="sxs-lookup"><span data-stu-id="4c4ae-535"><strong>RegisterOnSubmitStatement</strong></span></span>   |                                  <span data-ttu-id="4c4ae-536">註冊提交 HTML 窗體時執行的用戶端代碼。</span><span class="sxs-lookup"><span data-stu-id="4c4ae-536">Registers client-side code that executes when the HTML form is submitted.</span></span>                                   |
