---
uid: webhooks/diagnostics/debugging
title: ASP.NET Webhook 偵錯 |Microsoft Docs
author: rick-anderson
description: 如何偵錯 ASP.NET Webhook。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062495"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="86a89-103">偵錯 ASP.NET Webhook</span><span class="sxs-lookup"><span data-stu-id="86a89-103">ASP.NET WebHooks debugging</span></span>  

## <a name="debugging-in-azure"></a><span data-ttu-id="86a89-104">在 Azure 中偵錯</span><span class="sxs-lookup"><span data-stu-id="86a89-104">Debugging in Azure</span></span>

<span data-ttu-id="86a89-105">若要偵錯 Web 應用程式在 Azure 中執行時，請參閱本教學課程[疑難排解 Azure App Service 使用 Visual Studio 中的 web 應用程式](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)。</span><span class="sxs-lookup"><span data-stu-id="86a89-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="86a89-106">使用來源和符號偵錯</span><span class="sxs-lookup"><span data-stu-id="86a89-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="86a89-107">除了您自己的程式碼偵錯，就可以直接在 Microsoft ASP.NET Webhook，事實上，偵錯所有.NET。</span><span class="sxs-lookup"><span data-stu-id="86a89-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="86a89-108">這適用於無論是否您在本機或遠端的偵錯。</span><span class="sxs-lookup"><span data-stu-id="86a89-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="86a89-109">首先，設定 Visual Studio 用來尋找來源和符號移至**偵錯**，然後**選項和設定**。</span><span class="sxs-lookup"><span data-stu-id="86a89-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="86a89-110">設定選項如下：</span><span class="sxs-lookup"><span data-stu-id="86a89-110">Set the options like this:</span></span>

![選項和設定](_static/SourceSymbols.png)

<span data-ttu-id="86a89-112">然後新增連結[symbolsource.org](http://symbolsource.org)下載的來源和符號。</span><span class="sxs-lookup"><span data-stu-id="86a89-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="86a89-113">移至**符號**上方選單 索引標籤，並新增下列做為符號的位置：</span><span class="sxs-lookup"><span data-stu-id="86a89-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="86a89-114">此外，請確定快取目錄有簡短的名稱;否則的檔案名稱可以變得太長導致不載入符號。</span><span class="sxs-lookup"><span data-stu-id="86a89-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="86a89-115">範例路徑為：</span><span class="sxs-lookup"><span data-stu-id="86a89-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="86a89-116">設定看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="86a89-116">The settings should look similar to this:</span></span>

![選項符號檔位置範例](_static/SymSource.png)
