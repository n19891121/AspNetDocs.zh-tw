---
title: 建置您的第一個 Razor 元件應用程式
author: guardrex
description: 逐步建置 Razor 元件應用程式，並了解基本 Razor 元件概念。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/11/2019
uid: tutorials/first-razor-components-app
ms.openlocfilehash: 0c3dd2366581d73bad44e2911602e13c6c0daf9a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040775"
---
# <a name="build-your-first-razor-components-app"></a>建置您的第一個 Razor 元件應用程式

作者：[Daniel Roth](https://github.com/danroth27) 和 [Luke Latham](https://github.com/guardrex)

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

本教學課程說明如何使用 Razor 元件來建置應用程式，並示範基本 Razor 元件概念。 您可以使用 Razor 元件型專案 (.NET Core 3.0 或更新版本中可支援) 或使用 Blazor 型專案 (.NET Core 未來的版本中可支援) 來進行此教學課程。

針對使用 ASP.NET Core Razor 元件 (建議使用) 的體驗：

* 依照 <xref:razor-components/get-started> 中的指引來建立 Razor 元件型專案。
* 將專案命名為 `RazorComponents`。
* 這會從 Razor 元件範本建立一個多專案解決方案。 Razor 元件會以 *RazorComponents.App* 的形式產生。

針對使用 Blazor 的體驗：

* 依照 <xref:spa/blazor/get-started> 中的指引來建立 Blazor 型專案。
* 將專案命名為 `Blazor`。
* 這會從 Blazor 範本建立一個單一專案解決方案。

[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/build-your-first-razor-components-app/samples/) ([如何下載](xref:index#how-to-download-a-sample))。 如需了解先決條件，請參閱下列主題：

## <a name="build-components"></a>組建元件

1. 瀏覽至每個應用程式的三個頁面：首頁、計數器和擷取資料。 這些頁面會由 *Pages* 資料夾中的 Razor 檔案實作：*Index.cshtml*、*Counter.cshtml* 和 *FetchData.cshtml*。

1. 在 [計數器] 頁面上，選取 [按我] 按鈕以在不重新整理頁面的情況下讓計數器遞增。 讓網頁中的計數器遞增通常需要撰寫 JavaScript，但 Razor 元件提供一個使用 C# 的更好方法。

1. 檢查 *Counter.cshtml* 檔案中「計數器」元件的實作。

   *Pages/Counter.cshtml*：

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Counter1.cshtml)]

   「計數器」元件的 UI 是使用 HTML 來定義的。 動態轉譯邏輯 (例如迴圈、條件、運算式) 是使用內嵌的 C# 語法 (稱為 [Razor](xref:mvc/views/razor)) 來新增的。 HTML 標記和 C# 轉譯邏輯會在組建時轉換為元件類別。 所產生 .NET 類別的名稱會與檔案名稱相符。

   元件類別的成員定義在 `@functions` 區塊中。 在 `@functions` 區塊中，會指定元件狀態 (屬性、欄位) 來處理事件或定義其他元件邏輯。 然後會使用這些成員作為元件轉譯邏輯的一部分，並用於處理事件。

   選取 [Click me] \(按我\) 按鈕時：

   * 會呼叫「計數器」元件的已註冊 `onclick` 處理常式 (`IncrementCount` 方法)。
   * 「計數器」元件會重新產生其轉譯樹狀結構。
   * 新的轉譯樹狀結構會與先前的樹狀結構做比較。
   * 只會套用對「文件物件模型」(DOM) 所做的修改。 顯示的計數即會更新。

1. 修改「計數器」元件的 C# 邏輯，讓計數以 2 遞增而不是 1。

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Counter2.cshtml?highlight=14)]

1. 重建並執行應用程式以查看變更。 選取 [Click me] \(按我\) 按鈕，計數器就會以 2 遞增。

## <a name="use-components"></a>使用元件

使用類似 HTML 的語法將一個元件包含在另一個元件中。

1. 藉由將 `<Counter />` 元素新增至「索引」元件，將「計數器」元件新增至應用程式的「索引」(首頁) 元件。

   如果您使用 Blazor 來進行此體驗，則「索引」元件中會有「問卷提示」元件 (`<SurveyPrompt>` 元素)。 請以 `<Counter>` 元素取代 `<SurveyPrompt>` 元素。

   *Pages/Index.cshtml*：

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/Index.cshtml?highlight=7)]

1. 重建並執行應用程式。 首頁有自己的計數器。

## <a name="component-parameters"></a>元件參數

元件也可以有參數。 定義元件參數時，是在元件類別上使用以 `[Parameter]` 裝飾的非公開屬性來定義。 使用這些屬性來指定標記中元件的引數。

1. 更新元件的 `@functions` C# 程式碼：

   * 新增以 `[Parameter]` 屬性裝飾的 `IncrementAmount` 屬性。
   * 將 `IncrementCount` 方法變更為在增加 `currentCount`的值時使用 `IncrementAmount`。

   *Pages/Counter.cshtml*：

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Counter.cshtml?highlight=12,16)]

<!-- Add back when supported.
   > [!NOTE]
   > From Visual Studio, you can quickly add a component parameter by using the `para` snippet. Type `para` and press the `Tab` key twice.
-->

1. 使用屬性在「首頁」元件的 `<Counter>` 元素中指定 `IncrementAmount` 參數。 設定值來讓計數器以 10 遞增。

   *Pages/Index.cshtml*：

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Index.cshtml?highlight=7)]

1. 重新載入頁面。 每次選取 [Click me] \(按我\) 按鈕時，首頁計數器都會以 10 遞增。 [計數器] 頁面上的計數器會以 1 遞增。

## <a name="route-to-components"></a>路由到元件

*Counter.cshtml* 檔案頂端的 `@page` 指示詞會指定此元件是路由端點。 「計數器」元件會處理傳送給 `/Counter` 的要求。 若沒有 `@page` 指示詞，此元件就不會處理路由傳送的要求，但其他元件仍可使用此元件。

## <a name="dependency-injection"></a>相依性插入

在應用程式服務容器中註冊的服務可透過[相依性插入 (DI)](xref:fundamentals/dependency-injection) 供元件使用。 請使用 `@inject` 指示詞將服務插入至元件。

檢查 FetchData 元件 (*Pages/FetchData.cshtml*) 的指示詞。 `@inject` 指示詞會用來將 `WeatherForecastService` 服務執行個體插入至元件：

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData1.cshtml?highlight=3)]

`WeatherForecastService` 服務會註冊為[單一項目](xref:fundamentals/dependency-injection#service-lifetimes)，讓一個服務執行個體可供整個應用程式使用。

FetchData 元件會使用插入的服務作為 `ForecastService`，以擷取 `WeatherForecast` 物件的陣列：

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData2.cshtml?highlight=6)]

[@foreach](/dotnet/csharp/language-reference/keywords/foreach-in) 迴圈會用來將每個預測執行個體轉譯為天氣資料表中的資料列：

[!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData3.cshtml?highlight=11-19)]

## <a name="build-a-todo-list"></a>組建待辦事項清單

在實作簡單待辦事項清單的應用程式中新增頁面。

1. 將名為 *Todo.cshtml* 的空白檔案新增至 *Pages* 資料夾。

1. 提供頁面的初始標記：

   ```cshtml
   @page "/todo"

   <h1>Todo</h1>
   ```

1. 將 [待辦事項] 頁面新增至導覽列。

   NavMenu 元件 (*Shared/NavMenu.csthml*) 會用於應用程式的版面配置。 版面配置是可讓您避免應用程式中內容重複的元件。 如需詳細資訊，請參閱<xref:razor-components/layouts>。

   透過在 *Shared/NavMenu.csthml* 檔案中現有清單項目下方新增下列清單項目標記，為 [待辦事項] 頁面新增 `<NavLink>`：

   ```cshtml
   <li class="nav-item px-3">
       <NavLink class="nav-link" href="todo">
           <span class="oi oi-list-rich" aria-hidden="true"></span> Todo
       </NavLink>
   </li>
   ```

1. 重建並執行應用程式。 瀏覽新的 [待辦事項] 頁面，以確認 [待辦事項] 頁面的連結可以運作。

1. 將 *TodoItem.cs* 檔案新增至專案的根目錄，以保存代表待辦事項的類別。 請使用下列 `TodoItem` 類別的 C# 程式碼：

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/TodoItem.cs)]

1. 返回「待辦事項」元件 (*Todo.cshtml*)：

   * 在 `@functions` 區塊中新增待辦事項的欄位。 「待辦事項」元件會使用此欄位來維護待辦事項清單的狀態。
   * 新增未排序的清單標記和 `foreach` 迴圈，將每個待辦事項轉譯為清單項目。

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData4.cshtml?highlight=5-10,12-14)]

1. 應用程式需要 UI 項目，才能將待辦事項新增至清單。 在清單下方新增文字輸入和按鈕：

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData5.cshtml?highlight=12-13)]

1. 重建並執行應用程式。 選取 [Add todo] \(新增待辦事項\) 按鈕時，不會發生任何情況，因為事件處理常式並未連接至這個按鈕。

1. 將 `AddTodo` 方法新增至「待辦事項」元件，然後使用 `onclick` 屬性將它註冊用於按鈕點選：

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData6.cshtml?highlight=2,7-10)]

   當選取按鈕時，就會呼叫 `AddTodo` C# 方法。

1. 若要取得新待辦事項的標題，請新增 `newTodo` 字串欄位，然後使用 `bind` 屬性將它繫結至文字輸入的值：

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData7.cshtml?highlight=2)]

   ```cshtml
   <input placeholder="Something todo" bind="@newTodo" />
   ```

1. 更新 `AddTodo` 方法，將 `TodoItem` 與指定的標題新增至清單。 請將 `newTodo` 設定為空字串，以清除文字輸入的值：

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData8.cshtml?highlight=19-26)]

1. 重建並執行應用程式。 請將一些待辦事項新增至待辦事項清單，以測試新程式碼。

1. 每個待辦事項的標題文字都可設定為可編輯，而核取方塊則可協助使用者記錄已完成的項目。 請為每個待辦事項新增核取方塊輸入，然後將其值繫結至 `IsDone` 屬性。 將 `@todo.Title` 變更為繫結至 `@todo.Title` 的 `<input>` 元素：

   [!code-cshtml[](build-your-first-razor-components-app/samples_snapshot/3.x/FetchData9.cshtml?highlight=5-6)]

1. 若要確認是否已繫結這些值，請更新 `<h1>` 標頭，以顯示未完成之待辦事項 (`IsDone` 為 `false`) 的數目計數。

   ```cshtml
   <h1>Todo (@todos.Count(todo => !todo.IsDone))</h1>
   ```

1. 已完成的「待辦事項」元件 (*Todo.cshtml*)：

   [!code-cshtml[](build-your-first-razor-components-app/samples/3.x/RazorComponents/RazorComponents.App/Pages/Todo.cshtml)]

1. 重建並執行應用程式。 請新增待辦事項，以測試新程式碼。

## <a name="publish-and-deploy-the-app"></a>發佈及部署應用程式

若要發佈應用程式，請參閱 <xref:host-and-deploy/razor-components/index#publish-the-app>。
