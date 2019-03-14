---
ms.openlocfilehash: 68a77fffb9e2ed0eba05cceb2bff041f159501c6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046585"
---
# <a name="aspnet-core-model-providers-sample"></a><span data-ttu-id="d2116-101">ASP.NET Core 模型提供者範例</span><span class="sxs-lookup"><span data-stu-id="d2116-101">ASP.NET Core Model Providers Sample</span></span>

<span data-ttu-id="d2116-102">此範例說明如何使用 Razor 頁面自訂路由和頁面模型提供者。</span><span class="sxs-lookup"><span data-stu-id="d2116-102">This sample illustrates use of Razor Pages custom route and page model providers.</span></span> <span data-ttu-id="d2116-103">這個範例會示範 [Razor 頁面路由和應用程式慣例](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-convention-features)主題中所述的功能。</span><span class="sxs-lookup"><span data-stu-id="d2116-103">This sample demonstrates the features described in the [Razor Pages route and app conventions](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-convention-features) topic.</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="d2116-104">這個範例中的範例</span><span class="sxs-lookup"><span data-stu-id="d2116-104">Examples in this sample</span></span>

| <span data-ttu-id="d2116-105">情節</span><span class="sxs-lookup"><span data-stu-id="d2116-105">Scenario</span></span> | <span data-ttu-id="d2116-106">範例示範</span><span class="sxs-lookup"><span data-stu-id="d2116-106">Sample demo</span></span> |
| -------- | ----------- |
| [<span data-ttu-id="d2116-107">模型慣例</span><span class="sxs-lookup"><span data-stu-id="d2116-107">Model conventions</span></span>](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-conventions#model-conventions) | <span data-ttu-id="d2116-108">將路由屬性和標頭新增至應用程式的頁面。</span><span class="sxs-lookup"><span data-stu-id="d2116-108">Add a route attribute and header to the app's pages.</span></span> |
| [<span data-ttu-id="d2116-109">使用 AddPageRoute 來新增頁面路由</span><span class="sxs-lookup"><span data-stu-id="d2116-109">Use AddPageRoute to add a page route</span></span>](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-conventions#configure-a-page-route) | <span data-ttu-id="d2116-110">將指定的路由新增至指定頁面上的頁面。</span><span class="sxs-lookup"><span data-stu-id="d2116-110">Adds the specified route to the page at the specified page.</span></span> |
| [<span data-ttu-id="d2116-111">頁面模型動作慣例</span><span class="sxs-lookup"><span data-stu-id="d2116-111">Page model action conventions</span></span>](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-conventions#page-model-action-conventions) | <span data-ttu-id="d2116-112">將標頭新增至資料夾中的頁面、將標頭新增至單一頁面，以及設定篩選條件 Factory 將標頭新增至應用程式的頁面。</span><span class="sxs-lookup"><span data-stu-id="d2116-112">Add a header to pages in a folder, add a header to a single page, and configure a filter factory to add a header to the app's pages.</span></span> |
| [<span data-ttu-id="d2116-113">取代預設頁面應用程式模型提供者</span><span class="sxs-lookup"><span data-stu-id="d2116-113">Replace the default page app model provider</span></span>](https://docs.microsoft.com/aspnet/core/razor-pages/razor-pages-conventions#replace-the-default-page-app-model-provider) | <span data-ttu-id="d2116-114">變更處理常式命名的慣例。</span><span class="sxs-lookup"><span data-stu-id="d2116-114">Change the conventions for handler naming.</span></span> |
