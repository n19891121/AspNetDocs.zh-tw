---
ms.openlocfilehash: 6b2bc386ec179e786de205af0ca6dbd610e000d9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056485"
---
# <a name="aspnet-core-background-tasks-sample-generic-host"></a><span data-ttu-id="142f5-101">ASP.NET Core 背景工作範例 (泛型主機)</span><span class="sxs-lookup"><span data-stu-id="142f5-101">ASP.NET Core Background Tasks Sample (Generic Host)</span></span>

<span data-ttu-id="142f5-102">此範例說明如何使用 [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice)。</span><span class="sxs-lookup"><span data-stu-id="142f5-102">This sample illustrates the use of [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice).</span></span> <span data-ttu-id="142f5-103">這個範例會示範[在 ASP.NET Core 中使用託管服務的背景工作](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services)主題中所述的功能。</span><span class="sxs-lookup"><span data-stu-id="142f5-103">This sample demonstrates the features described in the [Background tasks with hosted services in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) topic.</span></span>

<span data-ttu-id="142f5-104">在 [Visual Studio Code](https://code.visualstudio.com/) 中執行範例時，請將 *.vscode/launch.json* 中主控台設定的 **console** 值設定成 `externalTerminal` 或 `integratedTerminal`。</span><span class="sxs-lookup"><span data-stu-id="142f5-104">When running the sample in [Visual Studio Code](https://code.visualstudio.com/), set the **console** value of the console configuration in *.vscode/launch.json* to either `externalTerminal` or `integratedTerminal`.</span></span> <span data-ttu-id="142f5-105">使用 `internalConsole` 會不相容於應用程式用於將背景工作項目加入佇列的按鍵輸入。</span><span class="sxs-lookup"><span data-stu-id="142f5-105">Use of the `internalConsole` is incompatible with console keystroke input that the app uses to enqueue background work items.</span></span>
