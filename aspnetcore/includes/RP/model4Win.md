---
ms.openlocfilehash: 85fa9f8b18dc7dfb3e9d37703549dc5c28dc7a4a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062595"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a>Scaffold 電影模型

* 從命令列執行下列命令 (在包含 *Program.cs*、*Startup.cs* 和 *.csproj* 檔案的專案目錄中)：

  ```console
  dotnet restore
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

如果您收到錯誤：
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

當您處於錯誤的目錄時，就會發生先前的錯誤。 開啟專案目錄 (包含 *Program.cs*、*Startup.cs* 和 *.csproj* 檔案的目錄) 的命令殼層，然後執行先前的命令。

如果您收到錯誤：
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

結束 Visual Studio 並再次執行命令。
