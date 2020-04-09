---
uid: webhooks/diagnostics/debugging
title: ASP.NET WebHooks 調試 |微軟文件
author: rick-anderson
description: 如何調試ASP.NET WebHooks。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 2f1f8196478e7025a0467acb945d9ed36c8fd0ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675373"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="65e51-103">ASP.NET WebHooks 除錯</span><span class="sxs-lookup"><span data-stu-id="65e51-103">ASP.NET WebHooks debugging</span></span>

## <a name="debugging-in-azure"></a><span data-ttu-id="65e51-104">在 Azure 中除錯</span><span class="sxs-lookup"><span data-stu-id="65e51-104">Debugging in Azure</span></span>

<span data-ttu-id="65e51-105">在 Azure 中執行時除錯 Web 應用程式,請參閱[使用 Visual Studio 在 Azure 應用服務中對 Web 應用進行故障排除教學](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)。</span><span class="sxs-lookup"><span data-stu-id="65e51-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="65e51-106">使用來源與符號進行除錯</span><span class="sxs-lookup"><span data-stu-id="65e51-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="65e51-107">除了調試自己的代碼外,還可以直接調試到 Microsoft ASP.NET WebHooks,實際上還可以調試到所有 .NET。</span><span class="sxs-lookup"><span data-stu-id="65e51-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="65e51-108">無論您在本地調試還是遠端調試,這都有效。</span><span class="sxs-lookup"><span data-stu-id="65e51-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="65e51-109">首先,通過去**調試**,然後選擇**和設置**,配置 Visual Studio 以查找源和符號。</span><span class="sxs-lookup"><span data-stu-id="65e51-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="65e51-110">設定以下的選項:</span><span class="sxs-lookup"><span data-stu-id="65e51-110">Set the options like this:</span></span>

![選項與設定](_static/SourceSymbols.png)

<span data-ttu-id="65e51-112">然後添加指向[symbolsource.org](http://symbolsource.org)的鏈接以下載源和符號。</span><span class="sxs-lookup"><span data-stu-id="65e51-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="65e51-113">跳到上面選單的 **「符號」** 選項卡,並將以下內容新增為符號位置:</span><span class="sxs-lookup"><span data-stu-id="65e51-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="65e51-114">此外,請確保緩存目錄具有短名稱;否則,檔名可能會太長,這將導致符號無法載入。</span><span class="sxs-lookup"><span data-stu-id="65e51-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="65e51-115">範例路徑是:</span><span class="sxs-lookup"><span data-stu-id="65e51-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="65e51-116">設定應如下所示:</span><span class="sxs-lookup"><span data-stu-id="65e51-116">The settings should look similar to this:</span></span>

![選項符號檔案位置範例](_static/SymSource.png)
