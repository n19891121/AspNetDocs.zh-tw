---
ms.openlocfilehash: 545448e3673b02abc7e685bd987f2cf5f71375b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57051955"
---
> [!WARNING]
> <span data-ttu-id="2d0f1-101">基於安全性考量，您必須選擇將 `GET` 要求資料繫結到頁面模型屬性。</span><span class="sxs-lookup"><span data-stu-id="2d0f1-101">For security reasons, you must opt in to binding `GET` request data to page model properties.</span></span> <span data-ttu-id="2d0f1-102">請先驗證使用者輸入再將其對應至屬性。</span><span class="sxs-lookup"><span data-stu-id="2d0f1-102">Verify user input before mapping it to properties.</span></span> <span data-ttu-id="2d0f1-103">在解決仰賴查詢字串或路由值的案例時，選擇使用 `GET` 繫結會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="2d0f1-103">Opting in to `GET` binding is useful when addressing scenarios which rely on query string or route values.</span></span>
>
> <span data-ttu-id="2d0f1-104">若要在 `GET` 要求上繫結屬性，請將 [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute)屬性的 `SupportsGet` 屬性設定為 `true`：`[BindProperty(SupportsGet = true)]`</span><span class="sxs-lookup"><span data-stu-id="2d0f1-104">To bind a property on `GET` requests, set the [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) attribute's `SupportsGet` property to `true`: `[BindProperty(SupportsGet = true)]`</span></span>
