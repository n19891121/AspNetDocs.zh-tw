---
title: Razor 元件 JavaScript interop
author: guardrex
description: 了解如何叫用 JavaScript 函式，從.NET 和.NET 從 JavaScript Blazor 和 Razor 元件的應用程式中的方法。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/javascript-interop
ms.openlocfilehash: 9f822fee8990b03ff15ffa9857a2ddd95328a6ce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050365"
---
# <a name="razor-components-javascript-interop"></a>Razor 元件 JavaScript interop

藉由[Javier Calvarro Nelson](https://github.com/javiercn)， [Daniel Roth](https://github.com/danroth27)，和[Luke Latham](https://github.com/guardrex)

Razor 元件應用程式可以叫用 JavaScript 函式，從.NET 和.NET 中的 JavaScript 程式碼的方法。

## <a name="invoke-javascript-functions-from-net-methods"></a>叫用.NET 方法的 JavaScript 函式

有些.NET 程式碼時要呼叫的 JavaScript 函式需要的時候。 例如，瀏覽器功能或從 JavaScript 程式庫應用程式的功能，可以公開 JavaScript 呼叫。

若要從.NET 呼叫 JavaScript，使用`IJSRuntime`抽象概念。 `InvokeAsync<T>`方法`IJSRuntime`會為您想要搭配任意數目的 JSON 可序列化的引數叫用的 JavaScript 函式的識別項。 函式識別項是相對於全域範圍 (`window`)。 如果您想要呼叫`window.someScope.someFunction`，此識別項是`someScope.someFunction`。 就不需要註冊函式，會在呼叫之前。 傳回的型別`T`也必須是 JSON 可序列化。

針對伺服器端 ASP.NET Core Razor 元件應用程式：

* 伺服器端應用程式會處理多個使用者要求。 請不要呼叫`JSRuntime.Current`元件叫用 JavaScript 函式中。
* 插入`IJSRuntime`抽象並用來發出 interop 的 JavaScript 呼叫插入的物件。

下列範例根據[TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder)，實驗性的 JavaScript 基礎解碼器。 此範例示範如何叫用的 JavaScript 函式，從C#方法。 JavaScript 函式會接受位元組陣列，從C#方法，將陣列，並傳回元件用於顯示的文字。

內部`<head>`項目*wwwroot/index.html*，提供使用的函式`TextDecoder`解碼傳入的陣列：

```html
<script>
  window.ConvertArray = (win1251Array) => {
    var win1251decoder = new TextDecoder('windows-1251');
    var bytes = new Uint8Array(win1251Array);
    var decodedArray = win1251decoder.decode(bytes);
    console.log(decodedArray);
    return decodedArray;
  };
</script>
```

JavaScript 程式碼，例如上述範例中，所示的程式碼也可以載入 JavaScript 檔案中的指令碼檔案的參考所*wwwroot/index.html*檔案。

下列元件：

* 叫用`ConvertArray`JavaScript 函式使用`JsRuntime`當元件 按鈕 (**轉換陣列**) 已選取。
* JavaScript 函式呼叫之後，會傳遞的陣列轉換成字串。 若要顯示的元件，會傳回字串。

```cshtml
@page "/"
@using Microsoft.JSInterop;
@inject IJSRuntime JsRuntime;

<h1>Call JavaScript Function Example</h1>

<button type="button" class="btn btn-primary" onclick="@ConvertArray">
    Convert Array
</button>

<p class="mt-2" style="font-size:1.6em">
    <span class="badge badge-success">
        @ConvertedText
    </span>
</p>

@functions {
    // Quote (c)2005 Universal Pictures: Serenity
    // https://www.uphe.com/movies/serenity
    // David Krumholtz on IMDB: https://www.imdb.com/name/nm0472710/

    private MarkupString ConvertedText =
        new MarkupString("Select the <b>Convert Array</b> button.");

    private uint[] QuoteArray = new uint[]
        {
            60, 101, 109, 62, 67, 97, 110, 39, 116, 32, 115, 116, 111, 112, 32,
            116, 104, 101, 32, 115, 105, 103, 110, 97, 108, 44, 32, 77, 97,
            108, 46, 60, 47, 101, 109, 62, 32, 45, 32, 77, 114, 46, 32, 85, 110,
            105, 118, 101, 114, 115, 101, 10, 10,
        };

    async void ConvertArray()
    {
        var text =
            await JsRuntime.InvokeAsync<string>("ConvertArray", QuoteArray);

        ConvertedText = new MarkupString(text);

        StateHasChanged();
    }
}
```

用戶端 Blazor 應用程式，如`IJSRuntime`抽象層是從可存取`JSRuntime.Current`，這指的是目前使用者的要求。 因為只有一位使用者的用戶端 Blazor 應用程式，使用`JSRuntime.Current`叫用 JavaScript 函式可正常運作。 只使用`JSRuntime.Current`用戶端 Blazor 應用程式中。

本主題相關的用戶端範例應用程式，在兩個 JavaScript 函式可與接收使用者輸入並顯示歡迎訊息 DOM 互動的用戶端應用程式：

* `showPrompt` &ndash; 會產生接受使用者輸入 （使用者名稱） 的提示，並傳回給呼叫者的名稱。
* `displayWelcome` &ndash; 會從呼叫端的歡迎訊息指派至 DOM 物件，但`id`的`welcome`。

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=2-7)]

地方`<script>`參考中的 JavaScript 檔案的標記*wwwroot/index.html*檔案：

[!code-html[](./common/samples/3.x/BlazorSample/wwwroot/index.html?highlight=16)]

不將指令碼標記放在元件檔，因為無法以動態方式更新指令碼標記。

使用 JavaScript 函式，藉由呼叫.NET 方法 interop`InvokeAsync<T>`方法`IJSRuntime`。

範例應用程式會使用一組C#方法，`Prompt`並`Display`，以叫用`showPrompt`並`displayWelcome`JavaScript 函式：

*JsInteropClasses/ExampleJsInterop.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=6-8,14-16)]

`IJSRuntime`抽象層是以非同步方式來提供伺服器端案例。 如果應用程式執行用戶端，而且您想要以同步方式叫用的 JavaScript 函式來向下轉型`IJSInProcessRuntime`並呼叫`Invoke<T>`改。 建議的大部分 JavaScript interop 程式庫使用非同步 Api，以確保程式庫適用於所有案例中，用戶端或伺服器端。

範例應用程式包含元件，可示範 JS interop。 元件：

* 接收透過 JS 提示使用者輸入。
* 要處理的元件傳回的文字。
* 呼叫第二個的 JS 函式與顯示歡迎訊息 DOM 互動。

*Pages/JSInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=1&end=21&highlight=2-3,9-11,13,16-20)]

1. 當`TriggerJsPrompt`執行選取的元件**觸發程序 JavaScript 提示** 按鈕，`ExampleJsInterop.Prompt`方法中的C#呼叫程式碼。
1. `Prompt`方法會執行 JavaScript`showPrompt`中所提供的函式*wwwroot/exampleJsInterop.js*檔案。
1. `showPrompt`函式會接受使用者輸入 （使用者的名稱），也就是 HTML 編碼，並傳回至`Prompt`方法最後回到元件。 該元件會將使用者的名稱儲存在本機變數中， `name`。
1. 將字串儲存在`name`會納入歡迎訊息，傳遞至第二個C#方法中， `ExampleJsInterop.Display`。
1. `Display` 呼叫的 JavaScript 函式， `displayWelcome`，會呈現標題標記的歡迎訊息。

## <a name="capture-references-to-elements"></a>擷取的項目參考

有些[JavaScript interop](xref:razor-components/javascript-interop)案例需要 HTML 項目的參考。 比方說，UI 程式庫可能需要的項目參考進行初始化，或者您可能需要類似命令的 Api 呼叫項目，例如`focus`或`play`。

您可以擷取在元件中的 HTML 項目的參考，加上`ref`屬性的 HTML 項目，然後定義類型的欄位`ElementRef`名稱的值相符`ref`屬性。

下列範例會示範擷取使用者名稱輸入項目的參考：

```csharp
<input ref="username" ... />

@functions {
    ElementRef username;
}
```

> [!NOTE]
> 請勿**不**這種方式填入 DOM 中使用擷取的項目參考 如此一來，可能會干擾宣告式轉譯模型。

.NET 程式碼是而言，`ElementRef`是不透明的控制代碼。 *只*您可以使用它做一件事是將其傳遞至 JavaScript 程式碼，透過 JavaScript interop。 當您這樣做時，JavaScript 後端程式碼會接收`HTMLElement`執行個體，它可以使用一般的 DOM Api。

比方說，下列程式碼會定義.NET 延伸模組方法，以允許將焦點設定在項目：

*mylib.js*:

```javascript
window.myLib = {
  focusElement : function (element) {
    element.focus();
  }
}
```

*ElementRefExtensions.cs*:

```csharp
using Microsoft.AspNetCore.Blazor;
using Microsoft.JSInterop;
using System.Threading.Tasks;

namespace MyLib
{
    public static class MyLibElementRefExtensions
    {
        public static Task Focus(this ElementRef elementRef)
        {
            return JSRuntime.Current.InvokeAsync<object>("myLib.focusElement", elementRef);
        }
    }
}
```

接下來是輸入在您的元件之一：

```cshtml
@using MyLib

<input ref="username" />
<button onclick="@SetFocus">Set focus</button>

@functions {
    ElementRef username;

    void SetFocus()
    {
        username.Focus();
    }
}
```

> [!IMPORTANT]
> `username`元件呈現，並包含其輸出之後，才會填入變數`<input>`項目。 如果您嘗試將傳遞擴展`ElementRef`JavaScript 程式碼中，JavaScript 程式碼會接收`null`。 若要操作項目參考，該元件已經完成呈現 （若要設定初始焦點的項目上） 的使用之後`OnAfterRenderAsync`或是`OnAfterRender`[元件的生命週期方法](xref:razor-components/components#lifecycle-methods)。

## <a name="invoke-net-methods-from-javascript-functions"></a>叫用.NET 方法，從 JavaScript 函式

### <a name="static-net-method-call"></a>靜態的.NET 方法呼叫

若要叫用靜態的.NET 方法，從 JavaScript，請使用`DotNet.invokeMethod`或`DotNet.invokeMethodAsync`函式。 在您想要呼叫時，包含函式，以及任何引數的組件名稱的靜態方法的識別碼中傳遞。 同樣地，非同步版本是以支援伺服器端案例的慣用物件。 若要可叫用 javascript，.NET 方法必須是公用、 靜態的以及與裝飾`[JSInvokable]`。 根據預設，方法識別項是方法名稱，但您可以指定不同的識別項使用`JSInvokableAttribute`建構函式。 呼叫開放式泛型方法目前不支援。

範例應用程式包含C#方法傳回的陣列`int`s。 方法以裝飾`JSInvokable`屬性。

*Pages/JsInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=47&end=58&highlight=7-11)]

提供給用戶端 JavaScript 叫用C#.NET 方法。

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=8-12)]

當**觸發程序.NET 靜態方法 ReturnArrayAsync**選取按鈕時，檢查在瀏覽器的 web 開發人員工具主控台輸出：

```console
Array(4) [ 1, 2, 3, 4 ]
```

第四個陣列值推入至的陣列 (`data.push(4);`) 所傳回`ReturnArrayAsync`。

### <a name="instance-method-call"></a>執行個體方法呼叫

您也可以從 JavaScript 呼叫.NET 執行個體方法。 要叫用的.NET 執行個體方法，從 JavaScript，第一次.NET 執行個體傳遞給 JavaScript 藉由包裝在`DotNetObjectRef`執行個體。 .NET 執行個體由參考傳遞至 JavaScript，以及您可以叫用執行個體使用的.NET 執行個體方法`invokeMethod`或`invokeMethodAsync`函式。 您也可以將.NET 執行個體傳遞做為引數，當叫用 JavaScript 從其他.NET 方法。

> [!NOTE]
> 範例應用程式會將訊息記錄到用戶端主控台。 下列範例中所示範的範例應用程式，請檢查瀏覽器的開發人員工具中的瀏覽器的主控台輸出。

當**觸發程序的.NET 執行個體方法 HelloHelper.SayHello**選取按鈕時，`ExampleJsInterop.CallHelloHelperSayHello`呼叫，並將名稱中，傳遞`Blazor`，方法。

*Pages/JsInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=60&end=69&highlight=8)]

`CallHelloHelperSayHello` JavaScript 函式會叫用`sayHello`的新執行個體與`HelloHelper`。

*JsInteropClasses/ExampleJsInterop.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=19-25)]

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=15-17)]

將名稱傳遞給`HelloHelper`的建構函式，它會設定`HelloHelper.Name`屬性。 當 JavaScript 函式`sayHello`執行時，`HelloHelper.SayHello`傳回`Hello, {Name}!`訊息，由 JavaScript 函式寫入至主控台。

*JsInteropClasses/HelloHelper.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/HelloHelper.cs?name=snippet1&highlight=5,10-11)]

在瀏覽器的 web 開發人員工具中輸出的主控台：

```console
Hello, Blazor!
```

## <a name="share-interop-code-in-a-razor-component-class-library"></a>共用元件 Razor 類別庫中的 interop 程式碼

JavaScript interop 程式碼可以包含在 Razor 元件類別庫 (`dotnet new blazorlib`)，這可讓您共用的 NuGet 套件中的程式碼。

Razor 元件類別程式庫會處理已建置的組件中內嵌的 JavaScript 資源。 JavaScript 檔案會放置於*wwwroot*資料夾，然後工具會負責建置程式庫時，內嵌資源。

應用程式的專案檔中參考的內建的 NuGet 套件，就像任何標準的 NuGet 套件參考。 還原應用程式之後，應用程式程式碼可以呼叫 JavaScript，就好像C#。
