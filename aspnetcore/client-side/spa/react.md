---
title: React 專案範本與 ASP.NET Core 搭配使用
author: SteveSandersonMS
description: 了解如何開始使用 React 和 create-react-app 適用的 ASP.NET Core 單頁應用程式 (SPA) 專案範本。
monikerRange: '>= aspnetcore-2.1'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/13/2019
uid: spa/react
ms.openlocfilehash: 3b2b2e67b5d577872bafefef5624a13ca1a22449
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026845"
---
# <a name="use-the-react-project-template-with-aspnet-core"></a><span data-ttu-id="d6412-103">React 專案範本與 ASP.NET Core 搭配使用</span><span class="sxs-lookup"><span data-stu-id="d6412-103">Use the React project template with ASP.NET Core</span></span>

<span data-ttu-id="d6412-104">更新的 React 專案範本可利用 React 和 [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) 慣例來實作功能多樣的用戶端使用者介面 (UI)，適合作為 ASP.NET Core 應用程式入門。</span><span class="sxs-lookup"><span data-stu-id="d6412-104">The updated React project template provides a convenient starting point for ASP.NET Core apps using React and [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) conventions to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="d6412-105">這個範本相當於建立一個 ASP.NET Core 專案作為 API 後端，以及建立一個標準 CRA React 專案作為 UI，但是可以將這兩個專案裝載至單一應用程式專案中，這樣便可視為一個整體進行建置與發行。</span><span class="sxs-lookup"><span data-stu-id="d6412-105">The template is equivalent to creating both an ASP.NET Core project to act as an API backend, and a standard CRA React project to act as a UI, but with the convenience of hosting both in a single app project that can be built and published as a single unit.</span></span>

## <a name="create-a-new-app"></a><span data-ttu-id="d6412-106">建立新的應用程式</span><span class="sxs-lookup"><span data-stu-id="d6412-106">Create a new app</span></span>

<span data-ttu-id="d6412-107">如已安裝 ASP.NET Core 2.1，就沒有必要安裝 React 專案範本。</span><span class="sxs-lookup"><span data-stu-id="d6412-107">If you have ASP.NET Core 2.1 installed, there's no need to install the React project template.</span></span>

<span data-ttu-id="d6412-108">進入命令提示字元，然後在空目錄中使用 `dotnet new react` 命令以建立新的專案。</span><span class="sxs-lookup"><span data-stu-id="d6412-108">Create a new project from a command prompt using the command `dotnet new react` in an empty directory.</span></span> <span data-ttu-id="d6412-109">例如，下列命令會在 *my-new-app* 目錄中建立應用程式並切換到該目錄：</span><span class="sxs-lookup"><span data-stu-id="d6412-109">For example, the following commands create the app in a *my-new-app* directory and switch to that directory:</span></span>

```console
dotnet new react -o my-new-app
cd my-new-app
```

<span data-ttu-id="d6412-110">從 Visual Studio 或 .NET Core CLI 執行該應用程式：</span><span class="sxs-lookup"><span data-stu-id="d6412-110">Run the app from either Visual Studio or the .NET Core CLI:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="d6412-111">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d6412-111">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="d6412-112">開啟產生的 *.csproj* 檔案，然後在該處以一般方式來執行該應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6412-112">Open the generated *.csproj* file, and run the app as normal from there.</span></span>

<span data-ttu-id="d6412-113">建置程序會在首次執行時還原 npm 相依性，這可能需要幾分鐘時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="d6412-113">The build process restores npm dependencies on the first run, which can take several minutes.</span></span> <span data-ttu-id="d6412-114">後續建置所需的時間將會縮短。</span><span class="sxs-lookup"><span data-stu-id="d6412-114">Subsequent builds are much faster.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="d6412-115">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="d6412-115">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="d6412-116">請確定您有一個名稱為 `ASPNETCORE_Environment` 環境變數而且它的值為 `Development`。</span><span class="sxs-lookup"><span data-stu-id="d6412-116">Ensure you have an environment variable called `ASPNETCORE_Environment` with value of `Development`.</span></span> <span data-ttu-id="d6412-117">在 Windows 上 (於非 PowerShell 提示字元中)，執行 `SET ASPNETCORE_Environment=Development`。</span><span class="sxs-lookup"><span data-stu-id="d6412-117">On Windows (in non-PowerShell prompts), run `SET ASPNETCORE_Environment=Development`.</span></span> <span data-ttu-id="d6412-118">在 Linux 或 macOS 上，執行 `export ASPNETCORE_Environment=Development`。</span><span class="sxs-lookup"><span data-stu-id="d6412-118">On Linux or macOS, run `export ASPNETCORE_Environment=Development`.</span></span>

<span data-ttu-id="d6412-119">執行 [dotnet build](/dotnet/core/tools/dotnet-build)，確認應用程式正確地建置。</span><span class="sxs-lookup"><span data-stu-id="d6412-119">Run [dotnet build](/dotnet/core/tools/dotnet-build) to verify your app builds correctly.</span></span> <span data-ttu-id="d6412-120">建置程序會在首次執行時還原 npm 相依性，這可能需要幾分鐘時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="d6412-120">On the first run, the build process restores npm dependencies, which can take several minutes.</span></span> <span data-ttu-id="d6412-121">後續建置所需的時間將會縮短。</span><span class="sxs-lookup"><span data-stu-id="d6412-121">Subsequent builds are much faster.</span></span>

<span data-ttu-id="d6412-122">執行 [dotnet run](/dotnet/core/tools/dotnet-run) 來啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6412-122">Run [dotnet run](/dotnet/core/tools/dotnet-run) to start the app.</span></span>

---

<span data-ttu-id="d6412-123">這個專案範本會建立一個 ASP.NET Core 應用程式以及一個 React 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6412-123">The project template creates an ASP.NET Core app and a React app.</span></span> <span data-ttu-id="d6412-124">ASP.NET Core 應用程式主要用於存取資料、授權以及其他伺服器端事項。</span><span class="sxs-lookup"><span data-stu-id="d6412-124">The ASP.NET Core app is intended to be used for data access, authorization, and other server-side concerns.</span></span> <span data-ttu-id="d6412-125">位在 *ClientApp* 子目錄中的 React 應用程式，是用於所有 UI 方面的作業。</span><span class="sxs-lookup"><span data-stu-id="d6412-125">The React app, residing in the *ClientApp* subdirectory, is intended to be used for all UI concerns.</span></span>

## <a name="add-pages-images-styles-modules-etc"></a><span data-ttu-id="d6412-126">新增頁面、影像、樣式、模組等等。</span><span class="sxs-lookup"><span data-stu-id="d6412-126">Add pages, images, styles, modules, etc.</span></span>

<span data-ttu-id="d6412-127">*ClientApp* 目錄是標準 CRA React 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6412-127">The *ClientApp* directory is a standard CRA React app.</span></span> <span data-ttu-id="d6412-128">如需詳細資訊，請參閱官方 [CRA 文件](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="d6412-128">See the official [CRA documentation](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) for more information.</span></span>

<span data-ttu-id="d6412-129">這個範本建立的 React 應用程式以及 CRA 本身建立的應用程式，二者之間存在些微的不同，不過應用程式的功能是一樣的。</span><span class="sxs-lookup"><span data-stu-id="d6412-129">There are slight differences between the React app created by this template and the one created by CRA itself; however, the app's capabilities are unchanged.</span></span> <span data-ttu-id="d6412-130">由範本所建立的應用程式包含以 [Bootstrap](https://getbootstrap.com/) \(英文\) 為基礎的配置，以及基本的路由範例。</span><span class="sxs-lookup"><span data-stu-id="d6412-130">The app created by the template contains a [Bootstrap](https://getbootstrap.com/)-based layout and a basic routing example.</span></span>

## <a name="install-npm-packages"></a><span data-ttu-id="d6412-131">安裝 npm 套件</span><span class="sxs-lookup"><span data-stu-id="d6412-131">Install npm packages</span></span>

<span data-ttu-id="d6412-132">若要安裝協力廠商 npm 套件，請在 *ClientApp* 子目錄中使用命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="d6412-132">To install third-party npm packages, use a command prompt in the *ClientApp* subdirectory.</span></span> <span data-ttu-id="d6412-133">例如: </span><span class="sxs-lookup"><span data-stu-id="d6412-133">For example:</span></span>

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a><span data-ttu-id="d6412-134">發行與部署</span><span class="sxs-lookup"><span data-stu-id="d6412-134">Publish and deploy</span></span>

<span data-ttu-id="d6412-135">在開發時，應用程式會以方便開發人員操作的模式執行。</span><span class="sxs-lookup"><span data-stu-id="d6412-135">In development, the app runs in a mode optimized for developer convenience.</span></span> <span data-ttu-id="d6412-136">例如，JavaScript 組合會包含來源對應 (以便在偵錯時，您可以看到原始程式碼)。</span><span class="sxs-lookup"><span data-stu-id="d6412-136">For example, JavaScript bundles include source maps (so that when debugging, you can see your original source code).</span></span> <span data-ttu-id="d6412-137">應用程式會監控磁碟上的 JavaScript、HTML 和 CSS 檔案變更，當發現檔案變更時，便自動重新編譯和重新載入。</span><span class="sxs-lookup"><span data-stu-id="d6412-137">The app watches JavaScript, HTML, and CSS file changes on disk and automatically recompiles and reloads when it sees those files change.</span></span>

<span data-ttu-id="d6412-138">在實際執行環境中，請提供具有最佳效能的應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="d6412-138">In production, serve a version of your app that's optimized for performance.</span></span> <span data-ttu-id="d6412-139">這是設定為自動進行的。</span><span class="sxs-lookup"><span data-stu-id="d6412-139">This is configured to happen automatically.</span></span> <span data-ttu-id="d6412-140">當您發行時，組建組態會釋出一個經過精簡、轉譯的用戶端程式碼組建。</span><span class="sxs-lookup"><span data-stu-id="d6412-140">When you publish, the build configuration emits a minified, transpiled build of your client-side code.</span></span> <span data-ttu-id="d6412-141">不同於開發組建，正式組建不需要在伺服器上安裝 Node.js。</span><span class="sxs-lookup"><span data-stu-id="d6412-141">Unlike the development build, the production build doesn't require Node.js to be installed on the server.</span></span>

<span data-ttu-id="d6412-142">您可以使用標準 [ASP.NET Core 裝載和部署方法](xref:host-and-deploy/index)。</span><span class="sxs-lookup"><span data-stu-id="d6412-142">You can use standard [ASP.NET Core hosting and deployment methods](xref:host-and-deploy/index).</span></span>

## <a name="run-the-cra-server-independently"></a><span data-ttu-id="d6412-143">獨立執行 CRA 伺服器</span><span class="sxs-lookup"><span data-stu-id="d6412-143">Run the CRA server independently</span></span>

<span data-ttu-id="d6412-144">專案已設定為：當 ASP.NET Core 應用程式在開發模式中啟動時，便在背景啟動它自己的 CRA 程式開發伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="d6412-144">The project is configured to start its own instance of the CRA development server in the background when the ASP.NET Core app starts in development mode.</span></span> <span data-ttu-id="d6412-145">因為這表示您不需要手動執行不同的伺服器，所以省了不少麻煩。</span><span class="sxs-lookup"><span data-stu-id="d6412-145">This is convenient because it means you don't have to run a separate server manually.</span></span>

<span data-ttu-id="d6412-146">此預設設定有一個缺點。</span><span class="sxs-lookup"><span data-stu-id="d6412-146">There's a drawback to this default setup.</span></span> <span data-ttu-id="d6412-147">每當您修改 C# 程式碼後，需要重新啟動 ASP.NET Core 應用程式，CRA 伺服器才會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="d6412-147">Each time you modify your C# code and your ASP.NET Core app needs to restart, the CRA server restarts.</span></span> <span data-ttu-id="d6412-148">大約幾秒鐘時間，才會開始備份。</span><span class="sxs-lookup"><span data-stu-id="d6412-148">A few seconds are required to start back up.</span></span> <span data-ttu-id="d6412-149">如果您經常編輯 C# 程式碼，且不想要等候 CRA 伺服器重新啟動，可以在外部執行 CRA 伺服器，與 ASP.NET Core 程序獨立開來。</span><span class="sxs-lookup"><span data-stu-id="d6412-149">If you're making frequent C# code edits and don't want to wait for the CRA server to restart, run the CRA server externally, independently of the ASP.NET Core process.</span></span> <span data-ttu-id="d6412-150">方法如下：</span><span class="sxs-lookup"><span data-stu-id="d6412-150">To do so:</span></span>

1. <span data-ttu-id="d6412-151">新增 *.env*的檔案*ClientApp*子目錄，使用下列設定：</span><span class="sxs-lookup"><span data-stu-id="d6412-151">Add a *.env* file to the *ClientApp* subdirectory with the following setting:</span></span>

    ```
    BROWSER=none
    ```
    
    <span data-ttu-id="d6412-152">啟動 CRA 伺服器外部時，這會導致無法開啟網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d6412-152">This will prevent your web browser from opening when starting the CRA server externally.</span></span>

2. <span data-ttu-id="d6412-153">在命令提示字元中，切換至 *ClientApp* 子目錄，然後啟動 CRA 程式開發伺服器：</span><span class="sxs-lookup"><span data-stu-id="d6412-153">In a command prompt, switch to the *ClientApp* subdirectory, and launch the CRA development server:</span></span>

    ```console
    cd ClientApp
    npm start
    ```

3. <span data-ttu-id="d6412-154">修改您的 ASP.NET Core 應用程式來使用外部的 CRA 伺服器執行個體，而不是啟動它自己的一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="d6412-154">Modify your ASP.NET Core app to use the external CRA server instance instead of launching one of its own.</span></span> <span data-ttu-id="d6412-155">在 *Startup* 類別中，將 `spa.UseReactDevelopmentServer` 引動過程取代為：</span><span class="sxs-lookup"><span data-stu-id="d6412-155">In your *Startup* class, replace the `spa.UseReactDevelopmentServer` invocation with the following:</span></span>

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:3000");
    ```

<span data-ttu-id="d6412-156">當您啟動 ASP.NET Core 應用程式，它並不會啟動 CRA 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d6412-156">When you start your ASP.NET Core app, it won't launch a CRA server.</span></span> <span data-ttu-id="d6412-157">而是改為使用您手動啟動的執行個體。</span><span class="sxs-lookup"><span data-stu-id="d6412-157">The instance you started manually is used instead.</span></span> <span data-ttu-id="d6412-158">這樣可以加快它的啟動和重新啟動速度。</span><span class="sxs-lookup"><span data-stu-id="d6412-158">This enables it to start and restart faster.</span></span> <span data-ttu-id="d6412-159">不用每一次都要等候 React 應用程式來重新建置。</span><span class="sxs-lookup"><span data-stu-id="d6412-159">It's no longer waiting for your React app to rebuild each time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6412-160">「 伺服器端轉譯 」 不支援的功能，此範本。</span><span class="sxs-lookup"><span data-stu-id="d6412-160">"Server-side rendering" is not a supported feature of this template.</span></span> <span data-ttu-id="d6412-161">我們使用此範本的目標是符合 「 建立 react-應用程式 」 使用的同位檢查。</span><span class="sxs-lookup"><span data-stu-id="d6412-161">Our goal with this template is to meet parity with "create-react-app".</span></span> <span data-ttu-id="d6412-162">因此，案例和功能不包含在 「 建立 react-應用程式 」 專案 （例如 SSR) 中不支援，而且會留給您作為練習使用者。</span><span class="sxs-lookup"><span data-stu-id="d6412-162">As such, scenarios and features not included in a "create-react-app" project (such as SSR) are not supported and are left as an exercise for the user.</span></span>
