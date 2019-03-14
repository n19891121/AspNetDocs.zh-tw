---
title: 開始使用 ASP.NET Core SignalR
author: bradygaster
description: 在本教學課程中，您會建立使用 ASP.NET Core SignalR 的聊天應用程式。
ms.author: bradyg
ms.custom: mvc
ms.date: 11/30/2018
uid: tutorials/signalr
ms.openlocfilehash: 53ec924c2d7b4fac227be0c0bf24d93476528167
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029025"
---
# <a name="tutorial-get-started-with-aspnet-core-signalr"></a>教學課程：開始使用 ASP.NET Core SignalR

本教學課程將教授使用 SignalR 建置即時應用程式的基本概念。 您將學習如何：

> [!div class="checklist"]
> * 建立 Web 專案。
> * 新增 SignalR 用戶端程式庫。
> * 建立 SignalR 中樞。
> * 設定專案以使用 SignalR。
> * 新增程式碼，以將訊息從任何用戶端傳送至所有連線的用戶端。

最後，您會有一個運作正常的聊天應用程式：

![SignalR 範例應用程式](signalr/_static/signalr-get-started-finished.png)

[檢視或下載範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([如何下載](xref:index#how-to-download-a-sample))。

[!INCLUDE [|Prerequisites](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-web-project"></a>建立 Web 專案

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

* 從功能表中選取 [檔案] > [新增專案] 。

* 在 [新增專案] 對話方塊中，選取 [已安裝] > [Visual C++] > [Web] > [ASP.NET Core Web 應用程式]。 將專案命名為 *SignalRChat*。

  ![Visual Studio 的 [新增專案] 對話方塊](signalr/_static/signalr-new-project-dialog.png)

* 選取 [Web 應用程式] 建立使用 Razor Pages 的專案。

* 選取 **.NET Core** 作為目標 Framework、選取 [ASP.NET Core 2.2]，然後按一下 [確定]。

  ![Visual Studio 的 [新增專案] 對話方塊](signalr/_static/signalr-new-project-choose-type.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

* 對要建立新專案資料夾所在的資料夾，開啟[整合式終端機](https://code.visualstudio.com/docs/editor/integrated-terminal)。

* 執行下列命令：

   ```console
   dotnet new webapp -o SignalRChat
   code -r SignalRChat
   ```

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* 從功能表中選取 [檔案] > [新增方案] 。

* 選取 [.NET Core] > [應用程式] > [ASP.NET Core Web 應用程式] (不要選取 [ASP.NET Core Web 應用程式 (MVC)])。

* 選取 [下一步]。

* 將專案命名為 *SignalRChat*，然後選取 [建立]。

---

## <a name="add-the-signalr-client-library"></a>新增 SignalR 用戶端程式庫

SignalR 伺服器程式庫包含在 `Microsoft.AspNetCore.App` 中繼套件內。 JavaScript 用戶端程式庫不會自動包括在專案中。 針對此教學課程，您會使用程式庫管理員 (LibMan) 從 *unpkg* 取得用戶端程式庫。 unpkg 是一個內容傳遞網路 (CDN)，可以傳遞在 Node.js 套件管理員 (npm) 中找到的任何項目。

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio/)

* 在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取 [新增] > [用戶端程式庫]。

* 在 [新增用戶端程式庫] 對話方塊中，針對 [提供者] 選取 [unpkg]。 

* 針對 [程式庫]，輸入 `@aspnet/signalr@1`，然後選取非預覽版的最新版本。

  ![[新增用戶端程式庫] 對話方塊 - 選取程式庫](signalr/_static/libman1.png)

* 選取 [選擇特定檔案]、展開 [散發者/瀏覽器] 資料夾，然後選取 *signalr.js* 與 *signalr.min.js*。

* 將 [目標位置] 設定為 *wwwroot/lib/signalr/*，然後選取 [安裝]。

  ![[新增用戶端程式庫] 對話方塊 - 選取檔案與目的地](signalr/_static/libman2.png)

  LibMan 會建立 *wwwroot/lib/signalr* 資料夾，並將選取的檔案複製到其中。

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code/)

* 在整合式終端機中，執行下列命令以安裝 LibMan。

  ```console
  dotnet tool install -g Microsoft.Web.LibraryManager.Cli
  ```

* 執行下列命令以透過使用 LibMan 來取得 SignalR 用戶端程式庫。 您可能必須等幾秒鐘，才會看到輸出。

  ```console
  libman install @aspnet/signalr -p unpkg -d wwwroot/lib/signalr --files dist/browser/signalr.js --files dist/browser/signalr.min.js
  ```

  參數指定下列選項：
  * 使用 unpkg 提供者。
  * 將檔案複製到 *wwwroot/lib/signalr* 目的地。
  * 只複製指定的檔案。

  輸出看起來會像下列範例這樣：

  ```console
  wwwroot/lib/signalr/dist/browser/signalr.js written to disk
  wwwroot/lib/signalr/dist/browser/signalr.min.js written to disk
  Installed library "@aspnet/signalr@1.0.3" to "wwwroot/lib/signalr"
  ```

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* 在 [終端機] 中執行下列命令以安裝 LibMan。

  ```console
  dotnet tool install -g Microsoft.Web.LibraryManager.Cli
  ```

* 瀏覽到專案資料夾 (包含 *SignalRChat.csproj* 檔案的資料夾)。

* 執行下列命令以透過使用 LibMan 來取得 SignalR 用戶端程式庫。

  ```console
  libman install @aspnet/signalr -p unpkg -d wwwroot/lib/signalr --files dist/browser/signalr.js --files dist/browser/signalr.min.js
  ```

  參數指定下列選項：
  * 使用 unpkg 提供者。
  * 將檔案複製到 *wwwroot/lib/signalr* 目的地。
  * 只複製指定的檔案。

  輸出看起來會像下列範例這樣：

  ```console
  wwwroot/lib/signalr/dist/browser/signalr.js written to disk
  wwwroot/lib/signalr/dist/browser/signalr.min.js written to disk
  Installed library "@aspnet/signalr@1.0.3" to "wwwroot/lib/signalr"
  ```

---

## <a name="create-a-signalr-hub"></a>建立 SignalR 中樞

*中樞*類別可提供作為高階管線，用來處理用戶端/伺服器通訊。

* 在 SignalRChat 專案資料夾中，建立 *Hubs* 資料夾。

* 在 *Hubs* 資料夾中，建立含有下列程式碼的 *ChatHub.cs* 檔案：

  [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

  `ChatHub` 類別繼承自 SignalR `Hub` 類別。 `Hub` 類別管理連線、群組和傳訊。

  連線的用戶端可以呼叫 `SendMessage` 方法將訊息傳送至所有用戶端。 本教學課程稍後將示範呼叫該方法的 JavaScript 用戶端程式碼。 SignalR 程式碼是以非同步方式來提供最大的延展性。

## <a name="configure-signalr"></a>設定 SignalR

SignalR 伺服器必須設定為將 SignalR 要求傳遞給 SignalR。

* 將下列醒目提示的程式碼新增至 *Startup.cs* 檔案。

  [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=7,33,52-55)]

  這些變更會將 SignalR 新增至 ASP.NET Core 相依性插入系統和中介軟體管線。

## <a name="add-signalr-client-code"></a>新增 SignalR 用戶端程式碼

* 以下列程式碼取代 *Pages\Index.cshtml* 中的程式碼：

  [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

  上述程式碼：

  * 建立名稱和訊息文字的文字方塊，以及提交按鈕。
  * 使用 `id="messagesList"` 建立清單，用於顯示接收自 SignalR 中樞的訊息。
  * 包含 SignalR 的指令碼參考和您在下一個步驟中建立的 *chat.js* 應用程式程式碼。

* 在 *wwwroot/js* 資料夾中，建立含有下列程式碼的 *chat.js* 檔案：

  [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

  上述程式碼：

  * 建立並啟動連線。
  * 新增處理常式至提交按鈕，以將訊息傳送至中樞。
  * 新增處理常式至連線物件，以從中樞接收訊息，並將它們新增至清單。

## <a name="run-the-app"></a>執行應用程式

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* 按 **CTRL+F5** 即可執行應用程式而不偵錯。

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

* 在整合式終端機中，執行下列命令：

  ```console
  dotnet run -p SignalRChat.csproj
  ```
  
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* 從功能表中選取 [執行] > [啟動但不偵錯]。

---

* 從網址列複製 URL，開啟另一個瀏覽器執行個體或索引標籤，然後將 URL 貼入網址列。

* 選擇任一個瀏覽器，輸入名稱和訊息，然後選取 [傳送訊息] 按鈕。

  名稱和訊息會立即顯示在兩個頁面上。

  ![SignalR 範例應用程式](signalr/_static/signalr-get-started-finished.png)

> [!TIP]
> 如果應用程式無法運作，請開啟您的瀏覽器開發人員工具 (F12)，然後移至主控台。 您可能會看到與 HTML 和 JavaScript 程式碼相關的錯誤。 例如，假設您將 *signalr.js* 放置在與指示不同的資料夾中。 在此情況下，該檔案的參考無法運作，您會在主控台中看到 404 錯誤。
> ![signalr.js 找不到錯誤](signalr/_static/f12-console.png)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 建立 Web 應用程式專案。
> * 新增 SignalR 用戶端程式庫。
> * 建立 SignalR 中樞。
> * 設定專案以使用 SignalR。
> * 新增使用中樞的程式碼，以將訊息從任何用戶端傳送至所有連線的用戶端。

若要深入了解 SignalR，請參閱簡介：

> [!div class="nextstepaction"]
> [ASP.NET Core SignalR 簡介](xref:signalr/introduction)
