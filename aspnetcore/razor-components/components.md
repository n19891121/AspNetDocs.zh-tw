---
title: 建立及使用 Razor 元件
author: guardrex
description: 了解如何建立和使用 Razor 元件，包括如何繫結至資料、 處理事件，以及管理元件的生命週期。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/13/2019
uid: razor-components/components
ms.openlocfilehash: 1533587f9f11e99f24d860c02f0efb6713119308
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031095"
---
# <a name="create-and-use-razor-components"></a><span data-ttu-id="3a7c3-103">建立及使用 Razor 元件</span><span class="sxs-lookup"><span data-stu-id="3a7c3-103">Create and use Razor Components</span></span>

<span data-ttu-id="3a7c3-104">藉由[Luke Latham](https://github.com/guardrex)， [Daniel Roth](https://github.com/danroth27)，和[Morné Zaayman](https://github.com/MorneZaayman)</span><span class="sxs-lookup"><span data-stu-id="3a7c3-104">By [Luke Latham](https://github.com/guardrex), [Daniel Roth](https://github.com/danroth27), and [Morné Zaayman](https://github.com/MorneZaayman)</span></span>

<span data-ttu-id="3a7c3-105">[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([如何下載](xref:index#how-to-download-a-sample))。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="3a7c3-106">請參閱[入門](xref:razor-components/get-started)主題，以取得必要條件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-106">See the [Get started](xref:razor-components/get-started) topic for prerequisites.</span></span>

<span data-ttu-id="3a7c3-107">Razor 元件應用程式使用來建置*元件*。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-107">Razor Components apps are built using *components*.</span></span> <span data-ttu-id="3a7c3-108">元件是自封式的區塊的使用者介面 (UI)，例如頁面、 對話方塊中或表單。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-108">A component is a self-contained chunk of user interface (UI), such as a page, dialog, or form.</span></span> <span data-ttu-id="3a7c3-109">元件包含 HTML 標記和處理所需的邏輯插入資料，或是在 UI 事件回應。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-109">A component includes HTML markup and the processing logic required to inject data or respond to UI events.</span></span> <span data-ttu-id="3a7c3-110">元件是富彈性且輕量級。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-110">Components are flexible and lightweight.</span></span> <span data-ttu-id="3a7c3-111">可以巢狀結構、 重複使用，並在專案之間共用。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-111">They can be nested, reused, and shared among projects.</span></span>

## <a name="component-classes"></a><span data-ttu-id="3a7c3-112">元件類別</span><span class="sxs-lookup"><span data-stu-id="3a7c3-112">Component classes</span></span>

<span data-ttu-id="3a7c3-113">元件的實作方式通常 *.cshtml*檔案搭配使用C#和 HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-113">Components are typically implemented in *.cshtml* files using a combination of C# and HTML markup.</span></span> <span data-ttu-id="3a7c3-114">元件 UI 是使用 HTML 來定義。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-114">The UI for a component is defined using HTML.</span></span> <span data-ttu-id="3a7c3-115">動態轉譯邏輯 (例如迴圈、條件、運算式) 是使用內嵌的 C# 語法 (稱為 [Razor](xref:mvc/views/razor)) 來新增的。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-115">Dynamic rendering logic (for example, loops, conditionals, expressions) is added using an embedded C# syntax called [Razor](xref:mvc/views/razor).</span></span> <span data-ttu-id="3a7c3-116">編譯 Razor 元件應用程式時，HTML 標記和C#轉譯邏輯會轉換成元件類別。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-116">When a Razor Components app is compiled, the HTML markup and C# rendering logic are converted into a component class.</span></span> <span data-ttu-id="3a7c3-117">產生之類別的名稱比對的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-117">The name of the generated class matches the name of the file.</span></span>

<span data-ttu-id="3a7c3-118">元件類別的成員中定義`@functions`區塊 (多部`@functions`區塊是允許)。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-118">Members of the component class are defined in a `@functions` block (more than one `@functions` block is permissible).</span></span> <span data-ttu-id="3a7c3-119">在 `@functions`方法來處理事件或定義其他元件邏輯，以及指定區塊，元件狀態 （屬性、 欄位）。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-119">In the `@functions` block, component state (properties, fields) is specified along with methods for event handling or for defining other component logic.</span></span>

<span data-ttu-id="3a7c3-120">元件成員再使用，因為部分元件的呈現邏輯使用C#開始使用的運算式`@`。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-120">Component members can then be used as part of the component's rendering logic using C# expressions that start with `@`.</span></span> <span data-ttu-id="3a7c3-121">例如，C#前面加上呈現欄位`@`的欄位名稱。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-121">For example, a C# field is rendered by prefixing `@` to the field name.</span></span> <span data-ttu-id="3a7c3-122">下列範例會評估，並呈現：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-122">The following example evaluates and renders:</span></span>

* <span data-ttu-id="3a7c3-123">`_headingFontStyle` CSS 屬性值，如`font-style`。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-123">`_headingFontStyle` to the CSS property value for `font-style`.</span></span>
* <span data-ttu-id="3a7c3-124">`_headingText` 內容`<h1>`項目。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-124">`_headingText` to the content of the `<h1>` element.</span></span>

```cshtml
<h1 style="font-style:@_headingFontStyle">@_headingText</h1>

@functions {
    private string _headingFontStyle = "italic";
    private string _headingText = "Put on your new Blazor!";
}
```

<span data-ttu-id="3a7c3-125">一開始呈現元件之後，元件會重新產生其呈現樹狀結構，以回應事件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-125">After the component is initially rendered, the component regenerates its render tree in response to events.</span></span> <span data-ttu-id="3a7c3-126">Razor 元件再比較新的轉譯樹狀目錄中，針對上一個，並套用至瀏覽器的文件物件模型 (DOM) 的任何修改。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-126">Razor Components then compares the new render tree against the previous one and applies any modifications to the browser's Document Object Model (DOM).</span></span>

## <a name="using-components"></a><span data-ttu-id="3a7c3-127">使用元件</span><span class="sxs-lookup"><span data-stu-id="3a7c3-127">Using components</span></span>

<span data-ttu-id="3a7c3-128">元件可以包含宣告的其他元件使用 HTML 項目語法。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-128">Components can include other components by declaring them using HTML element syntax.</span></span> <span data-ttu-id="3a7c3-129">使用元件的標記看起來像是 HTML 標籤，其中標籤名稱是元件類型。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-129">The markup for using a component looks like an HTML tag where the name of the tag is the component type.</span></span>

<span data-ttu-id="3a7c3-130">下列標記呈現`HeadingComponent`(*HeadingComponent.cshtml*) 執行個體：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-130">The following markup renders a `HeadingComponent` (*HeadingComponent.cshtml*) instance:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/Index.cshtml?name=snippet_HeadingComponent)]

## <a name="component-parameters"></a><span data-ttu-id="3a7c3-131">元件參數</span><span class="sxs-lookup"><span data-stu-id="3a7c3-131">Component parameters</span></span>

<span data-ttu-id="3a7c3-132">元件可以有*元件的參數*，這使用來定義*非公用*元件類別的屬性裝飾`[Parameter]`。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-132">Components can have *component parameters*, which are defined using *non-public* properties on the component class decorated with `[Parameter]`.</span></span> <span data-ttu-id="3a7c3-133">使用這些屬性來指定標記中元件的引數。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-133">Use attributes to specify arguments for a component in markup.</span></span>

<span data-ttu-id="3a7c3-134">在下列範例中，`ParentComponent`設定的值`Title`屬性`ChildComponent`:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-134">In the following example, the `ParentComponent` sets the value of the `Title` property of the `ChildComponent`:</span></span>

<span data-ttu-id="3a7c3-135">*ParentComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-135">*ParentComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ParentComponent.cshtml?name=snippet_ParentComponent&highlight=5)]

<span data-ttu-id="3a7c3-136">*ChildComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-136">*ChildComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ChildComponent.cshtml?highlight=7-8)]

## <a name="child-content"></a><span data-ttu-id="3a7c3-137">子內容</span><span class="sxs-lookup"><span data-stu-id="3a7c3-137">Child content</span></span>

<span data-ttu-id="3a7c3-138">另一個元件的內容時，可以設定元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-138">Components can set the content of another component.</span></span> <span data-ttu-id="3a7c3-139">指派的元件提供標記，用於指定接收元件之間的內容。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-139">The assigning component provides the content between the tags that specify the receiving component.</span></span> <span data-ttu-id="3a7c3-140">例如，`ParentComponent`可以提供內容的轉譯子元件放在內容`<ChildComponent>`標記。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-140">For example, a `ParentComponent` can provide content for rendering by a Child component by placing the content inside `<ChildComponent>` tags.</span></span>

<span data-ttu-id="3a7c3-141">*ParentComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-141">*ParentComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ParentComponent.cshtml?name=snippet_ParentComponent&highlight=6-7)]

<span data-ttu-id="3a7c3-142">子元件`ChildContent`屬性表示`RenderFragment`。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-142">The Child component has a `ChildContent` property that represents a `RenderFragment`.</span></span> <span data-ttu-id="3a7c3-143">值`ChildContent`位於子元件的標記應該用來呈現內容的位置。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-143">The value of `ChildContent` is positioned in the child component's markup where the content should be rendered.</span></span> <span data-ttu-id="3a7c3-144">在下列範例中，值`ChildContent`會收到來自父元件，並在啟動程序的面板內呈現`panel-body`。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-144">In the following example, the value of `ChildContent` is received from the parent component and rendered inside the Bootstrap panel's `panel-body`.</span></span>

<span data-ttu-id="3a7c3-145">*ChildComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-145">*ChildComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ChildComponent.cshtml?highlight=3,10-11)]

> [!NOTE]
> <span data-ttu-id="3a7c3-146">屬性接收`RenderFragment`內容必須命名為`ChildContent`依照慣例。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-146">The property receiving the `RenderFragment` content must be named `ChildContent` by convention.</span></span>

## <a name="data-binding"></a><span data-ttu-id="3a7c3-147">資料繫結</span><span class="sxs-lookup"><span data-stu-id="3a7c3-147">Data binding</span></span>

<span data-ttu-id="3a7c3-148">資料繫結元件和 DOM 項目以完成`bind`屬性。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-148">Data binding to both components and DOM elements is accomplished with the `bind` attribute.</span></span> <span data-ttu-id="3a7c3-149">下列範例會繫結`ItalicsCheck`屬性為核取方塊的核取狀態：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-149">The following example binds the `ItalicsCheck` property to the check box's checked state:</span></span>

```cshtml
<input type="checkbox" class="form-check-input" id="italicsCheck" 
    bind="@_italicsCheck" />
```

<span data-ttu-id="3a7c3-150">當核取方塊已選取，並清除時，要將屬性的值更新為`true`和`false`分別。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-150">When the check box is selected and cleared, the property's value is updated to `true` and `false`, respectively.</span></span>

<span data-ttu-id="3a7c3-151">轉譯元件時，不是為了回應，若要變更屬性的值時，才會更新 UI 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-151">The check box is updated in the UI only when the component is rendered, not in response to changing the property's value.</span></span> <span data-ttu-id="3a7c3-152">事件處理常式程式碼執行之後，元件會轉譯本身，因為屬性更新是通常在 UI 中立即反映。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-152">Since components render themselves after event handler code executes, property updates are usually reflected in the UI immediately.</span></span>

<span data-ttu-id="3a7c3-153">使用`bind`具有`CurrentValue`屬性 (`<input bind="@CurrentValue" />`) 基本上等同於下列：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-153">Using `bind` with a `CurrentValue` property (`<input bind="@CurrentValue" />`) is essentially equivalent to the following:</span></span>

```cshtml
<input value="@CurrentValue" 
    onchange="@((UIChangeEventArgs __e) => CurrentValue = __e.Value)" />
```

<span data-ttu-id="3a7c3-154">轉譯元件時，`value`的輸入項目來自`CurrentValue`屬性。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-154">When the component is rendered, the `value` of the input element comes from the `CurrentValue` property.</span></span> <span data-ttu-id="3a7c3-155">當使用者在文字方塊中，輸入`onchange`引發事件和`CurrentValue`屬性設定為已變更的值。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-155">When the user types in the text box, the `onchange` event is fired and the `CurrentValue` property is set to the changed value.</span></span> <span data-ttu-id="3a7c3-156">事實上，程式碼產生是稍微複雜因為`bind`處理少數的情況下會執行類型轉換。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-156">In reality, the code generation is a little more complex because `bind` handles a few cases where type conversions are performed.</span></span> <span data-ttu-id="3a7c3-157">基本上，`bind`產生關聯的運算式的目前值`value`使用已註冊的處理常式的屬性和處理變更。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-157">In principle, `bind` associates the current value of an expression with a `value` attribute and handles changes using the registered handler.</span></span>

<span data-ttu-id="3a7c3-158">**格式字串**</span><span class="sxs-lookup"><span data-stu-id="3a7c3-158">**Format strings**</span></span>

<span data-ttu-id="3a7c3-159">資料繫結搭配<xref:System.DateTime>格式字串。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-159">Data binding works with <xref:System.DateTime> format strings.</span></span> <span data-ttu-id="3a7c3-160">此時，無法使用其他格式的運算式，例如貨幣或數字的格式。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-160">Other format expressions, such as currency or number formats, aren't available at this time.</span></span>

```cshtml
<input bind="@StartDate" format-value="yyyy-MM-dd" />

@functions {
    [Parameter]
    private DateTime StartDate { get; set; } = new DateTime(2020, 1, 1);
}
```

<span data-ttu-id="3a7c3-161">`format-value`屬性會指定要套用至日期格式`value`的`input`項目。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-161">The `format-value` attribute specifies the date format to apply to the `value` of the `input` element.</span></span> <span data-ttu-id="3a7c3-162">的格式也用來剖析的值時`onchange`就會發生事件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-162">The format is also used to parse the value when an `onchange` event occurs.</span></span>

<span data-ttu-id="3a7c3-163">**元件的參數**</span><span class="sxs-lookup"><span data-stu-id="3a7c3-163">**Component parameters**</span></span>

<span data-ttu-id="3a7c3-164">繫結也會辨識元件參數，其中`bind-{property}`跨元件可以繫結的屬性值。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-164">Binding also recognizes component parameters, where `bind-{property}` can bind a property value across components.</span></span>

<span data-ttu-id="3a7c3-165">下列元件會使用`ChildComponent`並繫結`ParentYear`參數的父代`Year`子元件上的參數：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-165">The following component uses `ChildComponent` and binds the `ParentYear` parameter from the parent to the `Year` parameter on the child component:</span></span>

<span data-ttu-id="3a7c3-166">父元件：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-166">Parent component:</span></span>

```cshtml
@page "/ParentComponent"

<h1>Parent Component</h1>

<p>ParentYear: @ParentYear</p>

<ChildComponent bind-Year="@ParentYear" />

<button class="btn btn-primary" onclick="@ChangeTheYear">
    Change Year to 1986
</button>

@functions {
    [Parameter]
    private int ParentYear { get; set; } = 1978;

    void ChangeTheYear()
    {
        ParentYear = 1986;
    }
}
```

<span data-ttu-id="3a7c3-167">子元件：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-167">Child component:</span></span>

```cshtml
<h2>Child Component</h2>

<p>Year: @Year</p>

@functions {
    [Parameter]
    private int Year { get; set; }

    [Parameter]
    private Action<int> YearChanged { get; set; }
}
```

<span data-ttu-id="3a7c3-168">`Year`參數是可繫結，因為它有隨附`YearChanged`的型別對應的事件`Year`參數。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-168">The `Year` parameter is bindable because it has a companion `YearChanged` event that matches the type of the `Year` parameter.</span></span>

<span data-ttu-id="3a7c3-169">正在載入`ParentComponent`會產生下列標記：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-169">Loading the `ParentComponent` produces the following markup:</span></span>

```html
<h1>Parent Component</h1>

<p>ParentYear: 1978</p>

<h2>Child Component</h2>

<p>Year: 1978</p>
```

<span data-ttu-id="3a7c3-170">如果的值`ParentYear`屬性會變更選取的按鈕，即可`ParentComponent`，則`Year`屬性`ChildComponent`會更新。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-170">If the value of the `ParentYear` property is changed by selecting the button in the `ParentComponent`, the `Year` property of the `ChildComponent` is updated.</span></span> <span data-ttu-id="3a7c3-171">新值`Year`UI 中轉譯時`ParentComponent`會重新顯示：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-171">The new value of `Year` is rendered in the UI when the `ParentComponent` is rerendered:</span></span>

```html
<h1>Parent Component</h1>

<p>ParentYear: 1986</p>

<h2>Child Component</h2>

<p>Year: 1986</p>
```

## <a name="event-handling"></a><span data-ttu-id="3a7c3-172">事件處理</span><span class="sxs-lookup"><span data-stu-id="3a7c3-172">Event handling</span></span>

<span data-ttu-id="3a7c3-173">Razor 元件提供事件處理功能。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-173">Razor Components provide event handling features.</span></span> <span data-ttu-id="3a7c3-174">HTML 元素屬性的具名`on<event>`(例如`onclick`， `onsubmit`) 以委派型別值、 Razor 元件，請將視為事件處理常式的屬性的值。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-174">For an HTML element attribute named `on<event>` (for example, `onclick`, `onsubmit`) with a delegate-typed value, Razor Components treats the attribute's value as an event handler.</span></span> <span data-ttu-id="3a7c3-175">屬性的名稱一律以開頭`on`。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-175">The attribute's name always starts with `on`.</span></span>

<span data-ttu-id="3a7c3-176">下列程式碼會呼叫`UpdateHeading`在 UI 中選取按鈕時的方法：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-176">The following code calls the `UpdateHeading` method when the button is selected in the UI:</span></span>

```cshtml
<button class="btn btn-primary" onclick="@UpdateHeading">
    Update heading
</button>

@functions {
    void UpdateHeading(UIMouseEventArgs e)
    {
        ...
    }
}
```

<span data-ttu-id="3a7c3-177">下列程式碼會呼叫`CheckboxChanged`方法在 UI 中變更該核取方塊時：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-177">The following code calls the `CheckboxChanged` method when the check box is changed in the UI:</span></span>

```cshtml
<input type="checkbox" class="form-check-input" onchange="@CheckboxChanged" />

@functions {
    void CheckboxChanged()
    {
        ...
    }
}
```

<span data-ttu-id="3a7c3-178">事件處理常式也可以非同步處理和傳回<xref:System.Threading.Tasks.Task>。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-178">Event handlers can also be asynchronous and return a <xref:System.Threading.Tasks.Task>.</span></span> <span data-ttu-id="3a7c3-179">不需要手動呼叫`StateHasChanged()`。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-179">There's no need to manually call `StateHasChanged()`.</span></span> <span data-ttu-id="3a7c3-180">發生時，會記錄例外狀況。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-180">Exceptions are logged when they occur.</span></span>

```cshtml
<button class="btn btn-primary" onclick="@UpdateHeading">
    Update heading
</button>

@functions {
    async Task UpdateHeading(UIMouseEventArgs e)
    {
        ...
    }
}
```

<span data-ttu-id="3a7c3-181">對於某些事件，允許特定事件的事件引數型別。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-181">For some events, event-specific event argument types are permitted.</span></span> <span data-ttu-id="3a7c3-182">如果存取其中一個事件類型不是必要的它不需要在方法呼叫中。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-182">If access to one of these event types isn't necessary, it isn't required in the method call.</span></span>

<span data-ttu-id="3a7c3-183">支援的事件引數清單是：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-183">The list of supported event arguments is:</span></span>

* <span data-ttu-id="3a7c3-184">UIEventArgs</span><span class="sxs-lookup"><span data-stu-id="3a7c3-184">UIEventArgs</span></span>
* <span data-ttu-id="3a7c3-185">UIChangeEventArgs</span><span class="sxs-lookup"><span data-stu-id="3a7c3-185">UIChangeEventArgs</span></span>
* <span data-ttu-id="3a7c3-186">UIKeyboardEventArgs</span><span class="sxs-lookup"><span data-stu-id="3a7c3-186">UIKeyboardEventArgs</span></span>
* <span data-ttu-id="3a7c3-187">UIMouseEventArgs</span><span class="sxs-lookup"><span data-stu-id="3a7c3-187">UIMouseEventArgs</span></span>

<span data-ttu-id="3a7c3-188">也可以使用 lambda 運算式：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-188">Lambda expressions can also be used:</span></span>

```cshtml
<button onclick="@(e => Console.WriteLine("Hello, world!"))">Say hello</button>
```

<span data-ttu-id="3a7c3-189">通常很方便透過額外的值，例如關閉時逐一查看一組項目。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-189">It's often convenient to close over additional values, such as when iterating over a set of elements.</span></span> <span data-ttu-id="3a7c3-190">下列範例會建立三個按鈕，每一個`UpdateHeading`傳遞的事件引數 (`UIMouseEventArgs`) 和按鈕的編號 (`buttonNumber`) 時在 UI 中選取：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-190">The following example creates three buttons, each of which calls `UpdateHeading` passing an event argument (`UIMouseEventArgs`) and its button number (`buttonNumber`) when selected in the UI:</span></span>

```cshtml
<h2>@message</h2>

@for (var i = 1; i < 4; i++)
{
    var buttonNumber = i;

    <button class="btn btn-primary" 
            onclick="@(e => UpdateHeading(e, buttonNumber))">
        Button #@i
    </button>
}

@functions {
    string message = "Select a button to learn its position.";

    void UpdateHeading(UIMouseEventArgs e, int buttonNumber)
    {
        message = $"You selected Button #{buttonNumber} at " +
            "mouse position: {e.ClientX} X {e.ClientY}.";
    }
}
```

## <a name="capture-references-to-components"></a><span data-ttu-id="3a7c3-191">擷取元件的參考</span><span class="sxs-lookup"><span data-stu-id="3a7c3-191">Capture references to components</span></span>

<span data-ttu-id="3a7c3-192">元件參考提供方式 get 元件執行個體的參考，讓您發出命令至該執行個體，例如`Show`或`Reset`。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-192">Component references provide a way get a reference to a component instance so that you can issue commands to that instance, such as `Show` or `Reset`.</span></span> <span data-ttu-id="3a7c3-193">若要擷取元件的參考，請新增`ref`屬性的子元件，然後定義具有相同名稱和相同類型的欄位，做為子元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-193">To capture a component reference, add a `ref` attribute to the child component and then define a field with the same name and the same type as the child component.</span></span>

```cshtml
<MyLoginDialog ref="loginDialog" ... />

@functions {
    MyLoginDialog loginDialog;

    void OnSomething()
    {
        loginDialog.Show();
    }
}
```

<span data-ttu-id="3a7c3-194">轉譯元件時，`loginDialog`欄位會填入`MyLoginDialog`子元件執行個體。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-194">When the component is rendered, the `loginDialog` field is populated with the `MyLoginDialog` child component instance.</span></span> <span data-ttu-id="3a7c3-195">然後，您可以叫用的元件執行個體上的.NET 方法。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-195">You can then invoke .NET methods on the component instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a7c3-196">`loginDialog`元件會轉譯並包含其輸出之後，才會填入變數`MyLoginDialog`項目。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-196">The `loginDialog` variable is only populated after the component is rendered and its output includes the `MyLoginDialog` element.</span></span> <span data-ttu-id="3a7c3-197">直到那時，沒有任何參考。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-197">Until that point, there's nothing to reference.</span></span> <span data-ttu-id="3a7c3-198">若要操作元件的參考，該元件已經完成轉譯之後，使用`OnAfterRenderAsync`或`OnAfterRender`方法。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-198">To manipulate components references after the component has finished rendering, use the `OnAfterRenderAsync` or `OnAfterRender` methods.</span></span>

<span data-ttu-id="3a7c3-199">雖然擷取元件的參考會使用類似的語法，來[擷取項目參考](xref:razor-components/javascript-interop#capture-references-to-elements)，它不[JavaScript interop](xref:razor-components/javascript-interop)功能。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-199">While capturing component references uses a similar syntax to [capturing element references](xref:razor-components/javascript-interop#capture-references-to-elements), it isn't a [JavaScript interop](xref:razor-components/javascript-interop) feature.</span></span> <span data-ttu-id="3a7c3-200">元件參考都不會傳遞至 JavaScript 程式碼;只有.NET 程式碼中使用。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-200">Component references aren't passed to JavaScript code; they're only used in .NET code.</span></span>

> [!NOTE]
> <span data-ttu-id="3a7c3-201">請勿**不**使用元件參考来變動子元件的狀態。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-201">Do **not** use component references to mutate the state of child components.</span></span> <span data-ttu-id="3a7c3-202">請改用標準的宣告式參數將資料傳遞至子元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-202">Instead, use normal declarative parameters to pass data to child components.</span></span> <span data-ttu-id="3a7c3-203">這會導致子元件，以自動 rerender 在正確時間。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-203">This causes child components to rerender at the correct times automatically.</span></span>

## <a name="lifecycle-methods"></a><span data-ttu-id="3a7c3-204">生命週期方法</span><span class="sxs-lookup"><span data-stu-id="3a7c3-204">Lifecycle methods</span></span>

<span data-ttu-id="3a7c3-205">`OnInitAsync` 和`OnInit`執行程式碼以初始化元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-205">`OnInitAsync` and `OnInit` execute code to initialize the component.</span></span> <span data-ttu-id="3a7c3-206">若要執行非同步作業，請使用`OnInitAsync`而`await`作業上的關鍵字：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-206">To perform an asynchronous operation, use `OnInitAsync` and the `await` keyword on the operation:</span></span>

```csharp
protected override async Task OnInitAsync()
{
    await ...
}
```

<span data-ttu-id="3a7c3-207">同步作業中，使用`OnInit`:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-207">For a synchronous operation, use `OnInit`:</span></span>

```csharp
protected override void OnInit()
{
    ...
}
```

<span data-ttu-id="3a7c3-208">`OnParametersSetAsync` 和`OnParametersSet`元件已收到來自其父代的參數和值會指派給屬性時，會呼叫。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-208">`OnParametersSetAsync` and `OnParametersSet` are called when a component has received parameters from its parent and the values are assigned to properties.</span></span> <span data-ttu-id="3a7c3-209">在元件初始化之後，會執行這些方法，然後每當元件呈現：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-209">These methods are executed after component initialization and then each time the component is rendered:</span></span>

```csharp
protected override async Task OnParametersSetAsync()
{
    await ...
}
```

```csharp
protected override void OnParametersSet()
{
    ...
}
```

<span data-ttu-id="3a7c3-210">`OnAfterRenderAsync` 和`OnAfterRender`元件完成轉譯之後呼叫。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-210">`OnAfterRenderAsync` and `OnAfterRender` are called after a component has finished rendering.</span></span> <span data-ttu-id="3a7c3-211">會在此時填入項目和元件的參考。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-211">Element and component references are populated at this point.</span></span> <span data-ttu-id="3a7c3-212">您可以使用這個階段，執行額外的初始化步驟中使用的呈現的內容，例如啟用轉譯的 DOM 項目運作的第三方 JavaScript 程式庫。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-212">Use this stage to perform additional initialization steps using the rendered content, such as activating third-party JavaScript libraries that operate on the rendered DOM elements.</span></span>

```csharp
protected override async Task OnAfterRenderAsync()
{
    await ...
}
```

```csharp
protected override void OnAfterRender()
{
    ...
}
```

<span data-ttu-id="3a7c3-213">`SetParameters` 您可以覆寫參數設定之前執行程式碼：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-213">`SetParameters` can be overridden to execute code before parameters are set:</span></span>

```csharp
public override void SetParameters(ParameterCollection parameters)
{
    ...

    base.SetParameters(parameters);
}
```

<span data-ttu-id="3a7c3-214">如果`base.SetParameters`不叫用的自訂程式碼可以解譯方式所需的任何輸入的參數值。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-214">If `base.SetParameters` isn't invoked, the custom code can interpret the incoming parameters value in any way required.</span></span> <span data-ttu-id="3a7c3-215">例如，傳入的參數不一定要指派給類別上的屬性。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-215">For example, the incoming parameters aren't required to be assigned to the properties on the class.</span></span>

<span data-ttu-id="3a7c3-216">`ShouldRender` 若要隱藏 ui 的 重新整理，可以被覆寫。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-216">`ShouldRender` can be overridden to suppress refreshing of the UI.</span></span> <span data-ttu-id="3a7c3-217">如果實作會傳回`true`，UI 會重新整理。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-217">If the implementation returns `true`, the UI is refreshed.</span></span> <span data-ttu-id="3a7c3-218">即使`ShouldRender`會覆寫時，該元件一開始一律呈現。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-218">Even if `ShouldRender` is overridden, the component is always initially rendered.</span></span>

```csharp
protected override bool ShouldRender()
{
    var renderUI = true;

    return renderUI;
}
```

## <a name="component-disposal-with-idisposable"></a><span data-ttu-id="3a7c3-219">使用 IDisposable 的元件可供使用</span><span class="sxs-lookup"><span data-stu-id="3a7c3-219">Component disposal with IDisposable</span></span>

<span data-ttu-id="3a7c3-220">如果元件會實作<xref:System.IDisposable>，則[Dispose 方法](/dotnet/standard/garbage-collection/implementing-dispose)從 UI 移除元件時呼叫。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-220">If a component implements <xref:System.IDisposable>, the [Dispose method](/dotnet/standard/garbage-collection/implementing-dispose) is called when the component is removed from the UI.</span></span> <span data-ttu-id="3a7c3-221">下列元件會使用`@implements IDisposable`而`Dispose`方法：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-221">The following component uses `@implements IDisposable` and the `Dispose` method:</span></span>

```csharp
@using System
@implements IDisposable

...

@functions {
    public void Dispose()
    {
        ...
    }
}
```

## <a name="routing"></a><span data-ttu-id="3a7c3-222">路由</span><span class="sxs-lookup"><span data-stu-id="3a7c3-222">Routing</span></span>

<span data-ttu-id="3a7c3-223">Razor 元件中的路由之後，即可提供應用程式中每個可存取元件的路由範本。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-223">Routing in Razor Components is achieved by providing a route template to each accessible component in the app.</span></span>

<span data-ttu-id="3a7c3-224">當 *.cshtml*檔案並`@page`編譯指示詞，指定產生的類別<xref:Microsoft.AspNetCore.Mvc.RouteAttribute>指定路由範本。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-224">When a *.cshtml* file with an `@page` directive is compiled, the generated class is given a <xref:Microsoft.AspNetCore.Mvc.RouteAttribute> specifying the route template.</span></span> <span data-ttu-id="3a7c3-225">在執行階段，路由器會尋找使用的元件類別`RouteAttribute`並呈現任何元件有符合所要求的 URL 的路由範本。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-225">At runtime, the router looks for component classes with a `RouteAttribute` and renders whichever component has a route template that matches the requested URL.</span></span>

<span data-ttu-id="3a7c3-226">多個路由範本可以套用至元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-226">Multiple route templates can be applied to a component.</span></span> <span data-ttu-id="3a7c3-227">下列元件會回應要求`/BlazorRoute`和`/DifferentBlazorRoute`:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-227">The following component responds to requests for `/BlazorRoute` and `/DifferentBlazorRoute`:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?name=snippet_BlazorRoute)]

## <a name="route-parameters"></a><span data-ttu-id="3a7c3-228">路由參數</span><span class="sxs-lookup"><span data-stu-id="3a7c3-228">Route parameters</span></span>

<span data-ttu-id="3a7c3-229">元件可以接收路由範本中提供的路由參數`@page`指示詞。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-229">Components can receive route parameters from the route template provided in the `@page` directive.</span></span> <span data-ttu-id="3a7c3-230">路由器會使用路由參數，來填入對應的元件參數。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-230">The router uses route parameters to populate the corresponding component parameters.</span></span>

<span data-ttu-id="3a7c3-231">*RouteParameter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-231">*RouteParameter.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?name=snippet_RouteParameter)]

<span data-ttu-id="3a7c3-232">不支援選擇性參數，因此兩個`@page`指示詞會套用在上述範例中。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-232">Optional parameters aren't supported, so two `@page` directives are applied in the example above.</span></span> <span data-ttu-id="3a7c3-233">第一個允許瀏覽至不含參數的元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-233">The first permits navigation to the component without a parameter.</span></span> <span data-ttu-id="3a7c3-234">第二個`@page`指示詞會採用`{text}`路由參數，並將值指派給`Text`屬性。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-234">The second `@page` directive takes the `{text}` route parameter and assigns the value to the `Text` property.</span></span>

## <a name="base-class-inheritance-for-a-code-behind-experience"></a><span data-ttu-id="3a7c3-235">「 程式碼後置 」 體驗的基底類別繼承</span><span class="sxs-lookup"><span data-stu-id="3a7c3-235">Base class inheritance for a "code-behind" experience</span></span>

<span data-ttu-id="3a7c3-236">元件檔 (*.cshtml*) 混合 HTML 標記和C#處理相同檔案中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-236">Component files (*.cshtml*) mix HTML markup and C# processing code in the same file.</span></span> <span data-ttu-id="3a7c3-237">`@inherits`指示詞可用來提供元件標記分開處理程式碼的 「 程式碼後置 」 體驗中的 Razor 元件應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-237">The `@inherits` directive can be used to provide Razor Components apps with a "code-behind" experience that separates component markup from processing code.</span></span>

<span data-ttu-id="3a7c3-238">[範例應用程式](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/)示範如何元件可以繼承的基底類別， `BlazorRocksBase`，以提供元件的屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-238">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) shows how a component can inherit a base class, `BlazorRocksBase`, to provide the component's properties and methods.</span></span>

<span data-ttu-id="3a7c3-239">*BlazorRocks.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-239">*BlazorRocks.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRocks.cshtml?name=snippet_BlazorRocks)]

<span data-ttu-id="3a7c3-240">*BlazorRocksBase.cs*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-240">*BlazorRocksBase.cs*:</span></span>

[!code-csharp[](common/samples/3.x/BlazorSample/Pages/BlazorRocksBase.cs)]

<span data-ttu-id="3a7c3-241">基底類別應該衍生自`BlazorComponent`。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-241">The base class should derive from `BlazorComponent`.</span></span>

## <a name="razor-support"></a><span data-ttu-id="3a7c3-242">Razor 支援</span><span class="sxs-lookup"><span data-stu-id="3a7c3-242">Razor support</span></span>

<span data-ttu-id="3a7c3-243">**Razor 指示詞**</span><span class="sxs-lookup"><span data-stu-id="3a7c3-243">**Razor directives**</span></span>

<span data-ttu-id="3a7c3-244">下表顯示 razor 指示詞。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-244">Razor directives are shown in the following table.</span></span>

| <span data-ttu-id="3a7c3-245">指示詞</span><span class="sxs-lookup"><span data-stu-id="3a7c3-245">Directive</span></span> | <span data-ttu-id="3a7c3-246">描述</span><span class="sxs-lookup"><span data-stu-id="3a7c3-246">Description</span></span> |
| --------- | ----------- |
| [<span data-ttu-id="3a7c3-247">\@函式</span><span class="sxs-lookup"><span data-stu-id="3a7c3-247">\@functions</span></span>](xref:mvc/views/razor#section-5) | <span data-ttu-id="3a7c3-248">將C#元件的程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-248">Adds a C# code block to a component.</span></span> |
| `@implements` | <span data-ttu-id="3a7c3-249">實作的介面，產生的元件類別。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-249">Implements an interface for the generated component class.</span></span> |
| [<span data-ttu-id="3a7c3-250">\@inherits</span><span class="sxs-lookup"><span data-stu-id="3a7c3-250">\@inherits</span></span>](xref:mvc/views/razor#section-3) | <span data-ttu-id="3a7c3-251">提供完整的控制權，該元件繼承的類別。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-251">Provides full control of the class that the component inherits.</span></span> |
| [<span data-ttu-id="3a7c3-252">\@inject</span><span class="sxs-lookup"><span data-stu-id="3a7c3-252">\@inject</span></span>](xref:mvc/views/razor#section-4) | <span data-ttu-id="3a7c3-253">可讓服務從注入[服務容器](xref:fundamentals/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-253">Enables service injection from the [service container](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="3a7c3-254">如需詳細資訊，請參閱[在檢視中插入相依性](xref:mvc/views/dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-254">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span> |
| `@layout` | <span data-ttu-id="3a7c3-255">指定的配置元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-255">Specifies a layout component.</span></span> <span data-ttu-id="3a7c3-256">配置元件用來避免程式碼重複和不一致。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-256">Layout components are used to avoid code duplication and inconsistency.</span></span> |
| [<span data-ttu-id="3a7c3-257">\@page</span><span class="sxs-lookup"><span data-stu-id="3a7c3-257">\@page</span></span>](xref:razor-pages/index#razor-pages) | <span data-ttu-id="3a7c3-258">指定此元件應該直接處理要求。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-258">Specifies that the component should handle requests directly.</span></span> <span data-ttu-id="3a7c3-259">`@page`指示詞可以使用路由和選擇性的參數來指定。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-259">The `@page` directive can be specified with a route and optional parameters.</span></span> <span data-ttu-id="3a7c3-260">Razor 頁面與`@page`指示詞不需要在檔案頂端的第一個指示詞。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-260">Unlike Razor Pages, the `@page` directive doesn't need to be the first directive at the top of the file.</span></span> <span data-ttu-id="3a7c3-261">如需詳細資訊，請參閱[路由](xref:razor-components/routing)。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-261">For more information, see [Routing](xref:razor-components/routing).</span></span> |
| [<span data-ttu-id="3a7c3-262">\@使用</span><span class="sxs-lookup"><span data-stu-id="3a7c3-262">\@using</span></span>](xref:mvc/views/razor#using) | <span data-ttu-id="3a7c3-263">將C#`using`指示詞加入產生的元件類別。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-263">Adds the C# `using` directive to the generated component class.</span></span> |
| [<span data-ttu-id="3a7c3-264">\@addTagHelper</span><span class="sxs-lookup"><span data-stu-id="3a7c3-264">\@addTagHelper</span></span>](xref:mvc/views/razor#tag-helpers) | <span data-ttu-id="3a7c3-265">使用`@addTagHelper`使用比應用程式的組件的不同組件中的元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-265">Use `@addTagHelper` to use a component in a different assembly than the app's assembly.</span></span> |

<span data-ttu-id="3a7c3-266">**條件式屬性**</span><span class="sxs-lookup"><span data-stu-id="3a7c3-266">**Conditional attributes**</span></span>

<span data-ttu-id="3a7c3-267">屬性會根據.NET 值，有條件地呈現。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-267">Attributes are conditionally rendered based on the .NET value.</span></span> <span data-ttu-id="3a7c3-268">如果值為`false`或`null`，不會呈現的屬性。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-268">If the value is `false` or `null`,  the attribute isn't rendered.</span></span> <span data-ttu-id="3a7c3-269">如果值為`true`，會呈現該屬性最小化。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-269">If the value is `true`, the attribute is rendered minimized.</span></span>

<span data-ttu-id="3a7c3-270">在下列範例中，`IsCompleted`判斷`checked`呈現控制項的標記中：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-270">In the following example, `IsCompleted` determines if `checked` is rendered in the control's markup:</span></span>

```cshtml
<input type="checkbox" checked="@IsCompleted" />

@functions {
    [Parameter]
    private bool IsCompleted { get; set; }
}
```

<span data-ttu-id="3a7c3-271">如果`IsCompleted`是`true`，核取方塊會呈現為：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-271">If `IsCompleted` is `true`, the check box is rendered as:</span></span>

```html
<input type="checkbox" checked />
```

<span data-ttu-id="3a7c3-272">如果`IsCompleted`是`false`，核取方塊會呈現為：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-272">If `IsCompleted` is `false`, the check box is rendered as:</span></span>

```html
<input type="checkbox" />
```

<span data-ttu-id="3a7c3-273">**在 Razor 的其他資訊**</span><span class="sxs-lookup"><span data-stu-id="3a7c3-273">**Additional information on Razor**</span></span>

<span data-ttu-id="3a7c3-274">如需有關 Razor 的詳細資訊，請參閱[Razor 語法參考](xref:mvc/views/razor)。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-274">For more information on Razor, see the [Razor syntax reference](xref:mvc/views/razor).</span></span>

## <a name="raw-html"></a><span data-ttu-id="3a7c3-275">原始 HTML</span><span class="sxs-lookup"><span data-stu-id="3a7c3-275">Raw HTML</span></span>

<span data-ttu-id="3a7c3-276">字串通常呈現使用 DOM 文字節點，這表示它們可能包含任何標記為忽略，並視為常值文字。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-276">Strings are normally rendered using DOM text nodes, which means that any markup they may contain is ignored and treated as literal text.</span></span> <span data-ttu-id="3a7c3-277">若要轉譯原始 HTML，換行中的 HTML 內容`MarkupString`值。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-277">To render raw HTML, wrap the HTML content in a `MarkupString` value.</span></span> <span data-ttu-id="3a7c3-278">此值會以 HTML 或 SVG 剖析並插入至 dom。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-278">The value is parsed as HTML or SVG and inserted into the DOM.</span></span>

> [!WARNING]
> <span data-ttu-id="3a7c3-279">從任何建構的原始 HTML 呈現未受信任的來源**安全性風險**，應該予以避免 ！</span><span class="sxs-lookup"><span data-stu-id="3a7c3-279">Rendering raw HTML constructed from any untrusted source is a **security risk** and should be avoided!</span></span>

<span data-ttu-id="3a7c3-280">下列範例顯示如何使用`MarkupString`要轉譯的輸出的元件加入靜態 HTML 內容的區塊類型：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-280">The following example shows using the `MarkupString` type to add a block of static HTML content to the rendered output of a component:</span></span>

```html
@((MarkupString)myMarkup)

@functions {
    string myMarkup = "<p class='markup'>This is a <em>markup string</em>.</p>";
}
```

## <a name="templated-components"></a><span data-ttu-id="3a7c3-281">樣板化的元件</span><span class="sxs-lookup"><span data-stu-id="3a7c3-281">Templated components</span></span>

<span data-ttu-id="3a7c3-282">樣板化的元件是接受一或多個 UI 範本做為參數，然後為元件的轉譯邏輯的一部分使用的元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-282">Templated components are components that accept one or more UI templates as parameters, which can then be used as part of the component's rendering logic.</span></span> <span data-ttu-id="3a7c3-283">樣板化元件可讓您撰寫更一般的元件可重複使用的較高層級元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-283">Templated components allow you to author higher-level components that are more reusable than regular components.</span></span> <span data-ttu-id="3a7c3-284">一些範例包括：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-284">A couple of examples include:</span></span>

* <span data-ttu-id="3a7c3-285">資料表元件，可讓使用者指定資料表的標頭、 資料列和頁尾範本。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-285">A table component that allows a user to specify templates for the table's header, rows, and footer.</span></span>
* <span data-ttu-id="3a7c3-286">可讓使用者從清單中指定用於轉譯項目範本清單元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-286">A list component that allows a user to specify a template for rendering items in a list.</span></span>

### <a name="template-parameters"></a><span data-ttu-id="3a7c3-287">範本參數</span><span class="sxs-lookup"><span data-stu-id="3a7c3-287">Template parameters</span></span>

<span data-ttu-id="3a7c3-288">藉由指定一或多個元件的參數型別定義的樣板化的元件`RenderFragment`或`RenderFragment<T>`。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-288">A templated component is defined by specifying one or more component parameters of type `RenderFragment` or `RenderFragment<T>`.</span></span> <span data-ttu-id="3a7c3-289">轉譯片段代表一段所呈現之元件的 UI。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-289">A render fragment represents a segment of UI that is rendered by the component.</span></span> <span data-ttu-id="3a7c3-290">轉譯片段 （選擇性） 使用參數來叫用轉譯片段時，可以指定。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-290">A render fragment optionally takes a parameter that can be specified when the render fragment is invoked.</span></span>

<span data-ttu-id="3a7c3-291">*Components/TableTemplate.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-291">*Components/TableTemplate.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/TableTemplate.cshtml)]

<span data-ttu-id="3a7c3-292">當使用樣板化的元件，可以使用參數的名稱相符的子項目來指定範本參數 (`TableHeader`和`RowTemplate`在下列範例中):</span><span class="sxs-lookup"><span data-stu-id="3a7c3-292">When using a templated component, the template parameters can be specified using child elements that match the names of the parameters (`TableHeader` and `RowTemplate` in the following example):</span></span>

```cshtml
<TableTemplate Items="@pets">
    <TableHeader>
        <th>ID</th>
        <th>Name</th>
    </TableHeader>
    <RowTemplate>
        <td>@context.PetId</td>
        <td>@context.Name</td>
    </RowTemplate>
</TableTemplate>
```

### <a name="template-context-parameters"></a><span data-ttu-id="3a7c3-293">範本內容參數</span><span class="sxs-lookup"><span data-stu-id="3a7c3-293">Template context parameters</span></span>

<span data-ttu-id="3a7c3-294">元件的引數的型別`RenderFragment<T>`傳遞項目具有名為的隱含參數`context`(例如從上述的程式碼範例中， `@context.PetId`)，但您可以變更參數名稱使用`Context`子上的屬性項目。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-294">Component arguments of type `RenderFragment<T>` passed as elements have an implicit parameter named `context` (for example from the preceding code sample, `@context.PetId`), but you can change the parameter name using the `Context` attribute on the child element.</span></span> <span data-ttu-id="3a7c3-295">在下列範例中，`RowTemplate`項目的`Context`屬性會指定`pet`參數：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-295">In the following example, the `RowTemplate` element's `Context` attribute specifies the `pet` parameter:</span></span>

```cshtml
<TableTemplate Items="@pets">
    <TableHeader>
        <th>ID</th>
        <th>Name</th>
    </TableHeader>
    <RowTemplate Context="pet">
        <td>@pet.PetId</td>
        <td>@pet.Name</td>
    </RowTemplate>
</TableTemplate>
```

<span data-ttu-id="3a7c3-296">或者，您可以指定`Context`元件項目上的屬性。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-296">Alternatively, you can specify the `Context` attribute on the component element.</span></span> <span data-ttu-id="3a7c3-297">指定`Context`屬性會套用至所有指定的範本參數。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-297">The specified `Context` attribute applies to all specified template parameters.</span></span> <span data-ttu-id="3a7c3-298">這適合用於當您想要指定隱含子內容的內容參數名稱 (而不需要任何包裝子項目)。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-298">This can be useful when you want to specify the content parameter name for implicit child content (without any wrapping child element).</span></span> <span data-ttu-id="3a7c3-299">在下列範例中，`Context`屬性會出現在`TableTemplate`項目，並套用至所有的範本參數：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-299">In the following example, the `Context` attribute appears on the `TableTemplate` element and applies to all template parameters:</span></span>

```cshtml
<TableTemplate Items="@pets" Context="pet">
    <TableHeader>
        <th>ID</th>
        <th>Name</th>
    </TableHeader>
    <RowTemplate>
        <td>@pet.PetId</td>
        <td>@pet.Name</td>
    </RowTemplate>
</TableTemplate>
```

### <a name="generic-typed-components"></a><span data-ttu-id="3a7c3-300">泛型類型的元件</span><span class="sxs-lookup"><span data-stu-id="3a7c3-300">Generic-typed components</span></span>

<span data-ttu-id="3a7c3-301">樣板化的元件通常以一般方式是型別。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-301">Templated components are often generically typed.</span></span> <span data-ttu-id="3a7c3-302">例如，一般的清單檢視範本元件可以用來呈現`IEnumerable<T>`值。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-302">For example, a generic List View Template component can be used to render `IEnumerable<T>` values.</span></span> <span data-ttu-id="3a7c3-303">若要定義一般元件，請使用`@typeparam`指示詞來指定型別參數。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-303">To define a generic component, use the `@typeparam` directive to specify type parameters.</span></span>

<span data-ttu-id="3a7c3-304">*Components/ListViewTemplate.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-304">*Components/ListViewTemplate.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/ListViewTemplate.cshtml?highlight=1)]

<span data-ttu-id="3a7c3-305">當使用泛型型別元件，盡可能推斷型別參數：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-305">When using generic-typed components, the type parameter is inferred if possible:</span></span>

```cshtml
<ListViewTemplate Items="@pets">
    <ItemTemplate Context="pet">
        <li>@pet.Name</li>
    </ItemTemplate>
</ListViewTemplate>
```

<span data-ttu-id="3a7c3-306">否則，型別參數必須明確指定使用的屬性，以符合類型參數的名稱。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-306">Otherwise, the type parameter must be explicitly specified using an attribute that matches the name of the type parameter.</span></span> <span data-ttu-id="3a7c3-307">在下列範例中，`TItem="Pet"`指定的型別：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-307">In the following example, `TItem="Pet"` specifies the type:</span></span>

```cshtml
<ListViewTemplate Items="@pets" TItem="Pet">
    <ItemTemplate Context="pet">
        <li>@pet.Name</li>
    </ItemTemplate>
</ListViewTemplate>
```

## <a name="cascading-values-and-parameters"></a><span data-ttu-id="3a7c3-308">階層式值和參數</span><span class="sxs-lookup"><span data-stu-id="3a7c3-308">Cascading values and parameters</span></span>

<span data-ttu-id="3a7c3-309">在某些情況下，不方便流程資料從子系的元件使用的上階元件[元件參數](#component-parameters)，特別是在有數個元件層級。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-309">In some scenarios, it's inconvenient to flow data from an ancestor component to a descendent component using [component parameters](#component-parameters), especially when there are several component layers.</span></span> <span data-ttu-id="3a7c3-310">階層式值和參數解決這個問題，並提供便利的方式提供的值及其下階的元件的所有上階元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-310">Cascading values and parameters solve this problem by providing a convenient way for an ancestor component to provide a value to all of its descendent components.</span></span> <span data-ttu-id="3a7c3-311">階層式值和參數也會提供元件，以協調的方式。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-311">Cascading values and parameters also provide an approach for components to coordinate.</span></span>

### <a name="theme-example"></a><span data-ttu-id="3a7c3-312">佈景主題的範例</span><span class="sxs-lookup"><span data-stu-id="3a7c3-312">Theme example</span></span>

<span data-ttu-id="3a7c3-313">在下列*佈景主題*範例應用程式，從範例`ThemeInfo`類別會指定元件階層往下流動，以便所有指定的組件的應用程式內的按鈕都共用相同的樣式的佈景主題資訊。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-313">In the following *Theme* example from the sample app, the `ThemeInfo` class specifies the theme information to flow down the component hierarchy so that all of the buttons within a given part of the app share the same style.</span></span>

<span data-ttu-id="3a7c3-314">*UIThemeClasses/ThemeInfo.cs*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-314">*UIThemeClasses/ThemeInfo.cs*:</span></span>

```csharp
public class ThemeInfo
{
    public string ButtonClass { get; set; }
}
```

<span data-ttu-id="3a7c3-315">上階元件可以提供階層式值，使用串聯值元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-315">An ancestor component can provide a cascading value using the Cascading Value component.</span></span> <span data-ttu-id="3a7c3-316">階層式值元件包裝子樹狀結構的元件階層，並提供該樹狀子目錄內的所有元件的單一值。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-316">The Cascading Value component wraps a subtree of the component hierarchy and supplies a single value to all components within that subtree.</span></span>

<span data-ttu-id="3a7c3-317">例如，範例應用程式指定佈景主題的資訊 (`ThemeInfo`) 中的應用程式的版面配置組成的版面配置主體的所有元件的串聯式參數為其中一個`@Body`屬性。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-317">For example, the sample app specifies theme information (`ThemeInfo`) in one of the app's layouts as a cascading parameter for all components that make up the layout body of the `@Body` property.</span></span> <span data-ttu-id="3a7c3-318">`ButtonClass` 被指派的值`btn-success`配置元件中。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-318">`ButtonClass` is assigned a value of `btn-success` in the layout component.</span></span> <span data-ttu-id="3a7c3-319">任何子系的元件可以使用這個屬性，透過`ThemeInfo`階層式物件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-319">Any descendent component can consume this property through the `ThemeInfo` cascading object.</span></span>

<span data-ttu-id="3a7c3-320">*Shared/CascadingValuesParametersLayout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-320">*Shared/CascadingValuesParametersLayout.cshtml*:</span></span>

```cshtml
@inherits BlazorLayoutComponent
@using BlazorSample.UIThemeClasses

<div class="container-fluid">
    <div class="row">
        <div class="col-sm-3">
            <NavMenu />
        </div>
        <div class="col-sm-9">
            <CascadingValue Value="@theme">
                <div class="content px-4">
                    @Body
                </div>
            </CascadingValue>
        </div>
    </div>
</div>

@functions {
    ThemeInfo theme = new ThemeInfo { ButtonClass = "btn-success" };
}
```

<span data-ttu-id="3a7c3-321">若要讓使用串聯值，元件會宣告使用串聯參數`[CascadingParameter]`屬性，或者根據字串名稱值：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-321">To make use of cascading values, components declare cascading parameters using the `[CascadingParameter]` attribute or based on a string name value:</span></span>

```cshtml
<CascadingValue Value=@PermInfo Name="UserPermissions">...</CascadingValue>

[CascadingParameter(Name = "UserPermissions")] PermInfo Permissions { get; set; }
```

<span data-ttu-id="3a7c3-322">如果您有多個相同類型的階層式值，而且需要在相同的樹狀子目錄中加以區隔，以字串名稱值的繫結是相關。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-322">Binding with a string name value is relevant if you have multiple cascading values of the same type and need to differentiate them within the same subtree.</span></span>

<span data-ttu-id="3a7c3-323">串聯值繫結至串聯參數的型別。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-323">Cascading values are bound to cascading parameters by type.</span></span>

<span data-ttu-id="3a7c3-324">範例應用程式中的階層式值參數佈景主題元件繫結至`ThemeInfo`串聯值的串聯式參數。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-324">In the sample app, the Cascading Values Parameters Theme component binds to the `ThemeInfo` cascading value to a cascading parameter.</span></span> <span data-ttu-id="3a7c3-325">參數用來設定其中一個元件所顯示的按鈕之 CSS 類別。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-325">The parameter is used to set the CSS class for one of the buttons displayed by the component.</span></span>

<span data-ttu-id="3a7c3-326">*Pages/CascadingValuesParametersTheme.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-326">*Pages/CascadingValuesParametersTheme.cshtml*:</span></span>

```cshtml
@page "/cascadingvaluesparameterstheme"
@layout CascadingValuesParametersLayout
@using BlazorSample.UIThemeClasses

<h1>Cascading Values & Parameters</h1>

<p>Current count: @currentCount</p>

<p>
    <button class="btn" onclick="@IncrementCount">
        Increment Counter (Unthemed)
    </button>
</p>

<p>
    <button class="btn @ThemeInfo.ButtonClass" onclick="@IncrementCount">
        Increment Counter (Themed)
    </button>
</p>

@functions {
    int currentCount = 0;

    [CascadingParameter] protected ThemeInfo ThemeInfo { get; set; }

    void IncrementCount()
    {
        currentCount++;
    }
}
```

### <a name="tabset-example"></a><span data-ttu-id="3a7c3-327">TabSet 範例</span><span class="sxs-lookup"><span data-stu-id="3a7c3-327">TabSet example</span></span>

<span data-ttu-id="3a7c3-328">串聯參數也可讓元件階層中共同作業的元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-328">Cascading parameters also enable components to collaborate across the component hierarchy.</span></span> <span data-ttu-id="3a7c3-329">例如，請考慮下列*TabSet*範例應用程式中的範例。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-329">For example, consider the following *TabSet* example in the sample app.</span></span>

<span data-ttu-id="3a7c3-330">範例應用程式有`ITab`索引標籤實作的介面：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-330">The sample app has an `ITab` interface that tabs implement:</span></span>

[!code-cs[](common/samples/3.x/BlazorSample/UIInterfaces/ITab.cs)]

<span data-ttu-id="3a7c3-331">階層式值參數 TabSet 元件使用的索引標籤上設定的元件，其中包含數個索引標籤上的元件：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-331">The Cascading Values Parameters TabSet component uses the Tab Set component, which contains several Tab components:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/CascadingValuesParametersTabSet.cshtml?name=snippet_TabSet)]

<span data-ttu-id="3a7c3-332">子索引標籤上的元件不明確當做參數傳遞至索引標籤設定。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-332">The child Tab components aren't explicitly passed as parameters to the Tab Set.</span></span> <span data-ttu-id="3a7c3-333">相反地，子索引標籤上的元件是索引標籤上設定的子內容的一部分。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-333">Instead, the child Tab components are part of the child content of the Tab Set.</span></span> <span data-ttu-id="3a7c3-334">不過，索引標籤設定仍然需要知道每個索引標籤上的元件，以便它可以轉譯標頭和作用中的索引標籤。若要啟用這項協調，而不需要額外的程式碼，此索引標籤上設定的元件*做為階層式值可以提供本身*，然後挑選的子系的索引標籤元件。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-334">However, the Tab Set still needs to know about each Tab component so that it can render the headers and the active tab. To enable this coordination without requiring additional code, the Tab Set component *can provide itself as a cascading value* that is then picked up by the descendent Tab components.</span></span>

<span data-ttu-id="3a7c3-335">*Components/TabSet.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-335">*Components/TabSet.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/TabSet.cshtml)]

<span data-ttu-id="3a7c3-336">子系的索引標籤上的元件擷取包含索引標籤組作為階層式的參數，因此 索引標籤上的元件將本身新增至索引標籤上設定，而座標上哪一個索引標籤為作用中。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-336">The descendent Tab components capture the containing Tab Set as a cascading parameter, so the Tab components add themselves to the Tab Set and coordinate on which tab is active.</span></span>

<span data-ttu-id="3a7c3-337">*Components/Tab.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-337">*Components/Tab.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/Tab.cshtml)]

## <a name="razor-templates"></a><span data-ttu-id="3a7c3-338">Razor 範本</span><span class="sxs-lookup"><span data-stu-id="3a7c3-338">Razor templates</span></span>

<span data-ttu-id="3a7c3-339">呈現使用 Razor 範本語法就可以定義片段。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-339">Render fragments can be defined using Razor template syntax.</span></span> <span data-ttu-id="3a7c3-340">Razor 範本是用來定義 UI 程式碼片段，並假設以下列格式：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-340">Razor templates are a way to define a UI snippet and assume the following format:</span></span>

```cshtml
@<tag>...</tag>
```

<span data-ttu-id="3a7c3-341">下列範例說明如何指定`RenderFragment`和`RenderFragment<T>`值。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-341">The following example illustrates how to specify `RenderFragment` and `RenderFragment<T>` values.</span></span>

<span data-ttu-id="3a7c3-342">*RazorTemplates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3a7c3-342">*RazorTemplates.cshtml*:</span></span>

```cshtml
@{
    RenderFragment template = @<p>The time is @DateTime.Now.</p>;
    RenderFragment<Pet> petTemplate = (pet) => @<p>Your pet's name is @pet.Name.</p>;
}
```

<span data-ttu-id="3a7c3-343">呈現使用的 Razor 範本可以做為引數傳遞到樣板化的元件，或直接呈現所定義的片段。</span><span class="sxs-lookup"><span data-stu-id="3a7c3-343">Render fragments defined using Razor templates can be passed as arguments to templated components or rendered directly.</span></span> <span data-ttu-id="3a7c3-344">比方說前, 一個範本會直接轉譯下列 Razor 標記：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-344">For example, the previous templates are directly rendered with the following Razor markup:</span></span>

```cshtml
@template

@petTemplate(new Pet { Name = "Rex" })
```

<span data-ttu-id="3a7c3-345">轉譯輸出：</span><span class="sxs-lookup"><span data-stu-id="3a7c3-345">Rendered output:</span></span>

```
The time is 10/04/2018 01:26:52.

Your pet's name is Rex.
```
