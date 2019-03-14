---
ms.openlocfilehash: e5c80c80380dadfce9cff5ec268535076258d980
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041115"
---
<span data-ttu-id="ef9ef-101">執行身分識別框架：</span><span class="sxs-lookup"><span data-stu-id="ef9ef-101">Run the Identity scaffolder:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="ef9ef-102">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ef9ef-102">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="ef9ef-103">從**方案總管**，以滑鼠右鍵按一下專案 >**新增** > **新增 Scaffold 項目**。</span><span class="sxs-lookup"><span data-stu-id="ef9ef-103">From **Solution Explorer**, right-click on the project > **Add** > **New Scaffolded Item**.</span></span>
* <span data-ttu-id="ef9ef-104">從左窗格**新增 Scaffold**對話方塊中，選取**識別** > **新增**。</span><span class="sxs-lookup"><span data-stu-id="ef9ef-104">From the left pane of the **Add Scaffold** dialog, select **Identity** > **ADD**.</span></span>
* <span data-ttu-id="ef9ef-105">在 [ **ADD 身分識別**] 對話方塊中，選取您想要的選項。</span><span class="sxs-lookup"><span data-stu-id="ef9ef-105">In the **ADD Identity** dialog, select the options you want.</span></span>
  * <span data-ttu-id="ef9ef-106">選取現有的版面配置頁面，或您的版面配置檔將會覆寫以不正確的標記。</span><span class="sxs-lookup"><span data-stu-id="ef9ef-106">Select your existing layout page, or your layout file will be overwritten with incorrect markup.</span></span> <span data-ttu-id="ef9ef-107">比方說`~/Pages/Shared/_Layout.cshtml`Razor 頁面`~/Views/Shared/_Layout.cshtml`MVC 專案</span><span class="sxs-lookup"><span data-stu-id="ef9ef-107">For example `~/Pages/Shared/_Layout.cshtml` for Razor Pages `~/Views/Shared/_Layout.cshtml` for MVC projects</span></span>
  * <span data-ttu-id="ef9ef-108">選取  **+** 來建立新的按鈕**資料內容類別**。</span><span class="sxs-lookup"><span data-stu-id="ef9ef-108">Select the **+** button to create a new **Data context class**.</span></span>
* <span data-ttu-id="ef9ef-109">選取 **新增**。</span><span class="sxs-lookup"><span data-stu-id="ef9ef-109">Select **ADD**.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="ef9ef-110">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="ef9ef-110">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="ef9ef-111">如果之前尚未安裝 ASP.NET Core scaffolder，請立即安裝：</span><span class="sxs-lookup"><span data-stu-id="ef9ef-111">If you have not previously installed the ASP.NET Core scaffolder, install it now:</span></span>

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

<span data-ttu-id="ef9ef-112">新增的套件參考[Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/)至專案 (\*.csproj) 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef9ef-112">Add a package reference to [Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/) to the project (\*.csproj) file.</span></span> <span data-ttu-id="ef9ef-113">在專案目錄中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="ef9ef-113">Run the following command in the project directory:</span></span>

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

<span data-ttu-id="ef9ef-114">執行下列命令來列出識別 scaffolder 選項：</span><span class="sxs-lookup"><span data-stu-id="ef9ef-114">Run the following command to list the Identity scaffolder options:</span></span>

```cli
dotnet aspnet-codegenerator identity -h
```

<span data-ttu-id="ef9ef-115">在 [專案] 資料夾中，執行身分識別 scaffolder 使用您想要的選項。</span><span class="sxs-lookup"><span data-stu-id="ef9ef-115">In the project folder, run the Identity scaffolder with the options you want.</span></span> <span data-ttu-id="ef9ef-116">例如，若要設定的預設 UI 身分識別和檔案的最小數目，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="ef9ef-116">For example, to setup identity with the default UI and the minimum number of files, run the following command:</span></span>

```cli
dotnet aspnet-codegenerator identity --useDefaultUI
```

-------------
