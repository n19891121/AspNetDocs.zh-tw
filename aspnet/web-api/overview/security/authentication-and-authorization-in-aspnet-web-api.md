---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET Web API 中的身份驗證和授權 |微軟文件
author: MikeWasson
description: 提供了ASP.NET Web API 中的身份驗證和授權的概述。
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676255"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a><span data-ttu-id="f6de2-103">ASP.NET Web API 中的驗證和授權</span><span class="sxs-lookup"><span data-stu-id="f6de2-103">Authentication and Authorization in ASP.NET Web API</span></span>

<span data-ttu-id="f6de2-104">由[邁克·瓦森](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f6de2-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="f6de2-105">您已經創建了 Web API,但現在要控制對它的訪問。</span><span class="sxs-lookup"><span data-stu-id="f6de2-105">You've created a web API, but now you want to control access to it.</span></span> <span data-ttu-id="f6de2-106">在本系列文章中,我們將介紹一些保護 Web API 免受未經授權的使用者訪問的選項。</span><span class="sxs-lookup"><span data-stu-id="f6de2-106">In this series of articles, we'll look at some options for securing a web API from unauthorized users.</span></span> <span data-ttu-id="f6de2-107">本系列將涵蓋身份驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="f6de2-107">This series will cover both authentication and authorization.</span></span>

- <span data-ttu-id="f6de2-108">*身份驗證*是知道使用者的身份。</span><span class="sxs-lookup"><span data-stu-id="f6de2-108">*Authentication* is knowing the identity of the user.</span></span> <span data-ttu-id="f6de2-109">例如,Alice 使用使用者名稱和密碼登錄,伺服器使用密碼對 Alice 進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="f6de2-109">For example, Alice logs in with her username and password, and the server uses the password to authenticate Alice.</span></span>
- <span data-ttu-id="f6de2-110">*授權*是決定是否允許使用者執行操作。</span><span class="sxs-lookup"><span data-stu-id="f6de2-110">*Authorization* is deciding whether a user is allowed to perform an action.</span></span> <span data-ttu-id="f6de2-111">例如,Alice 有權獲取資源,但不能創建資源。</span><span class="sxs-lookup"><span data-stu-id="f6de2-111">For example, Alice has permission to get a resource but not create a resource.</span></span>

<span data-ttu-id="f6de2-112">本系列的第一篇文章概述了ASP.NET Web API 中的身份驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="f6de2-112">The first article in the series gives a general overview of authentication and authorization in ASP.NET Web API.</span></span> <span data-ttu-id="f6de2-113">其他主題描述 Web API 的常見身份驗證方案。</span><span class="sxs-lookup"><span data-stu-id="f6de2-113">Other topics describe common authentication scenarios for Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="f6de2-114">感謝那些回顧這個系列並提供寶貴反饋的人:里克·安德森、利維·布羅德里克、巴里·多蘭斯、湯姆·戴克斯特拉、葛紅梅、大衛·馬特森、丹尼爾·羅斯、蒂姆·蒂肯。</span><span class="sxs-lookup"><span data-stu-id="f6de2-114">Thanks to the people who reviewed this series and provided valuable feedback: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.</span></span>

## <a name="authentication"></a><span data-ttu-id="f6de2-115">驗證</span><span class="sxs-lookup"><span data-stu-id="f6de2-115">Authentication</span></span>

<span data-ttu-id="f6de2-116">Web API 假定身份驗證發生在主機中。</span><span class="sxs-lookup"><span data-stu-id="f6de2-116">Web API assumes that authentication happens in the host.</span></span> <span data-ttu-id="f6de2-117">對於 Web 託管,主機是 IIS,它使用 HTTP 模組進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="f6de2-117">For web-hosting, the host is IIS, which uses HTTP modules for authentication.</span></span> <span data-ttu-id="f6de2-118">您可以將專案配置為使用 IIS 或 ASP.NET 內置的任何身份驗證模組,或者編寫自己的 HTTP 模組以執行自定義身份驗證。</span><span class="sxs-lookup"><span data-stu-id="f6de2-118">You can configure your project to use any of the authentication modules built in to IIS or ASP.NET, or write your own HTTP module to perform custom authentication.</span></span>

<span data-ttu-id="f6de2-119">當主機對使用者進行身份驗證時,它會創建一個*主體*,它是一個[IThe 物件](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx),表示代碼運行的安全上下文。</span><span class="sxs-lookup"><span data-stu-id="f6de2-119">When the host authenticates the user, it creates a *principal*, which is an [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) object that represents the security context under which code is running.</span></span> <span data-ttu-id="f6de2-120">主機通過設置**Thread.Currentthe 將**主體附加到當前線程。</span><span class="sxs-lookup"><span data-stu-id="f6de2-120">The host attaches the principal to the current thread by setting **Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="f6de2-121">主體包含一個關聯的**標識**物件,該物件包含有關使用者的資訊。</span><span class="sxs-lookup"><span data-stu-id="f6de2-121">The principal contains an associated **Identity** object that contains information about the user.</span></span> <span data-ttu-id="f6de2-122">如果使用者已使用身份認證,**識別.Is 認證**屬性會傳回**true**。</span><span class="sxs-lookup"><span data-stu-id="f6de2-122">If the user is authenticated, the **Identity.IsAuthenticated** property returns **true**.</span></span> <span data-ttu-id="f6de2-123">對匿名要求 **,已身份驗證\*\*\*\*傳回 false**。</span><span class="sxs-lookup"><span data-stu-id="f6de2-123">For anonymous requests, **IsAuthenticated** returns **false**.</span></span> <span data-ttu-id="f6de2-124">有關主體的詳細資訊,請參閱[基於角色的安全性](https://msdn.microsoft.com/library/shz8h065.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6de2-124">For more information about principals, see [Role-Based Security](https://msdn.microsoft.com/library/shz8h065.aspx).</span></span>

### <a name="http-message-handlers-for-authentication"></a><span data-ttu-id="f6de2-125">驗證的 HTTP 訊息處理程式</span><span class="sxs-lookup"><span data-stu-id="f6de2-125">HTTP Message Handlers for Authentication</span></span>

<span data-ttu-id="f6de2-126">您可以將身份驗證邏輯放入[HTTP 消息處理程式](../advanced/http-message-handlers.md)中,而不是使用主機進行身份驗證。</span><span class="sxs-lookup"><span data-stu-id="f6de2-126">Instead of using the host for authentication, you can put authentication logic into an [HTTP message handler](../advanced/http-message-handlers.md).</span></span> <span data-ttu-id="f6de2-127">在這種情況下,消息處理程序檢查 HTTP 請求並設置主體。</span><span class="sxs-lookup"><span data-stu-id="f6de2-127">In that case, the message handler examines the HTTP request and sets the principal.</span></span>

<span data-ttu-id="f6de2-128">何時應該使用消息處理程序進行身份驗證?</span><span class="sxs-lookup"><span data-stu-id="f6de2-128">When should you use message handlers for authentication?</span></span> <span data-ttu-id="f6de2-129">以下是一些權衡:</span><span class="sxs-lookup"><span data-stu-id="f6de2-129">Here are some tradeoffs:</span></span>

- <span data-ttu-id="f6de2-130">HTTP 模組看到通過ASP.NET管道的所有請求。</span><span class="sxs-lookup"><span data-stu-id="f6de2-130">An HTTP module sees all requests that go through the ASP.NET pipeline.</span></span> <span data-ttu-id="f6de2-131">消息處理程式只看到路由到 Web API 的請求。</span><span class="sxs-lookup"><span data-stu-id="f6de2-131">A message handler only sees requests that are routed to Web API.</span></span>
- <span data-ttu-id="f6de2-132">您可以設置每個路由的消息處理程式,這允許您將身份驗證方案應用於特定路由。</span><span class="sxs-lookup"><span data-stu-id="f6de2-132">You can set per-route message handlers, which lets you apply an authentication scheme to a specific route.</span></span>
- <span data-ttu-id="f6de2-133">HTTP 模組特定於 IIS。</span><span class="sxs-lookup"><span data-stu-id="f6de2-133">HTTP modules are specific to IIS.</span></span> <span data-ttu-id="f6de2-134">消息處理程式與主機無關,因此可以同時用於 Web 託管和自託管。</span><span class="sxs-lookup"><span data-stu-id="f6de2-134">Message handlers are host-agnostic, so they can be used with both web-hosting and self-hosting.</span></span>
- <span data-ttu-id="f6de2-135">HTTP 模組參與 IIS 日誌記錄、審核等。</span><span class="sxs-lookup"><span data-stu-id="f6de2-135">HTTP modules participate in IIS logging, auditing, and so on.</span></span>
- <span data-ttu-id="f6de2-136">HTTP 模組在管道中運行較早。</span><span class="sxs-lookup"><span data-stu-id="f6de2-136">HTTP modules run earlier in the pipeline.</span></span> <span data-ttu-id="f6de2-137">如果在消息處理程序中處理身份驗證,則在處理程式運行之前不會設置主體。</span><span class="sxs-lookup"><span data-stu-id="f6de2-137">If you handle authentication in a message handler, the principal does not get set until the handler runs.</span></span> <span data-ttu-id="f6de2-138">此外,當回應離開消息處理程式時,主體將還原到上一個主體。</span><span class="sxs-lookup"><span data-stu-id="f6de2-138">Moreover, the principal reverts back to the previous principal when the response leaves the message handler.</span></span>

<span data-ttu-id="f6de2-139">通常,如果您不需要支援自託管,HTTP 模組是一個更好的選擇。</span><span class="sxs-lookup"><span data-stu-id="f6de2-139">Generally, if you don't need to support self-hosting, an HTTP module is a better option.</span></span> <span data-ttu-id="f6de2-140">如果需要支援自託管,請考慮消息處理程式。</span><span class="sxs-lookup"><span data-stu-id="f6de2-140">If you need to support self-hosting, consider a message handler.</span></span>

### <a name="setting-the-principal"></a><span data-ttu-id="f6de2-141">設置主體</span><span class="sxs-lookup"><span data-stu-id="f6de2-141">Setting the Principal</span></span>

<span data-ttu-id="f6de2-142">如果應用程式執行任何自定義身份驗證邏輯,則必須在以下兩個位置設置主體:</span><span class="sxs-lookup"><span data-stu-id="f6de2-142">If your application performs any custom authentication logic, you must set the principal on two places:</span></span>

- <span data-ttu-id="f6de2-143">**執行緒.電流主體**。</span><span class="sxs-lookup"><span data-stu-id="f6de2-143">**Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="f6de2-144">此屬性是在 .NET 中設置線程主體的標準方法。</span><span class="sxs-lookup"><span data-stu-id="f6de2-144">This property is the standard way to set the thread's principal in .NET.</span></span>
- <span data-ttu-id="f6de2-145">**HTTPContext.當前.使用者**。</span><span class="sxs-lookup"><span data-stu-id="f6de2-145">**HttpContext.Current.User**.</span></span> <span data-ttu-id="f6de2-146">此屬性特定於ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="f6de2-146">This property is specific to ASP.NET.</span></span>

<span data-ttu-id="f6de2-147">以下代碼展示如何設定主體:</span><span class="sxs-lookup"><span data-stu-id="f6de2-147">The following code shows how to set the principal:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="f6de2-148">對於 Web 託管,必須在兩個位置設置主體;否則,安全上下文可能會變得不一致。</span><span class="sxs-lookup"><span data-stu-id="f6de2-148">For web-hosting, you must set the principal in both places; otherwise the security context may become inconsistent.</span></span> <span data-ttu-id="f6de2-149">但是,對於自託管 **,HTTPContext.current**為 null。</span><span class="sxs-lookup"><span data-stu-id="f6de2-149">For self-hosting, however, **HttpContext.Current** is null.</span></span> <span data-ttu-id="f6de2-150">因此,為了確保代碼與主機無關,請在分配給**HTTPContext.Current**之前檢查空。</span><span class="sxs-lookup"><span data-stu-id="f6de2-150">To ensure your code is host-agnostic, therefore, check for null before assigning to **HttpContext.Current**, as shown.</span></span>

## <a name="authorization"></a><span data-ttu-id="f6de2-151">授權</span><span class="sxs-lookup"><span data-stu-id="f6de2-151">Authorization</span></span>

<span data-ttu-id="f6de2-152">授權在管道中稍後發生,更接近控制器。</span><span class="sxs-lookup"><span data-stu-id="f6de2-152">Authorization happens later in the pipeline, closer to the controller.</span></span> <span data-ttu-id="f6de2-153">這樣,在授予對資源的許可權時,可以做出更精細的選擇。</span><span class="sxs-lookup"><span data-stu-id="f6de2-153">That lets you make more granular choices when you grant access to resources.</span></span>

- <span data-ttu-id="f6de2-154">*授權篩選器在*控制器操作之前運行。</span><span class="sxs-lookup"><span data-stu-id="f6de2-154">*Authorization filters* run before the controller action.</span></span> <span data-ttu-id="f6de2-155">如果請求未獲授權,篩選器將返回錯誤回應,並且不會調用該操作。</span><span class="sxs-lookup"><span data-stu-id="f6de2-155">If the request is not authorized, the filter returns an error response, and the action is not invoked.</span></span>
- <span data-ttu-id="f6de2-156">在控制器操作中,可以從**ApiController.User**屬性獲取當前主體。</span><span class="sxs-lookup"><span data-stu-id="f6de2-156">Within a controller action, you can get the current principal from the **ApiController.User** property.</span></span> <span data-ttu-id="f6de2-157">例如,您可以根據使用者名篩選資源清單,僅返回屬於該使用者的資源。</span><span class="sxs-lookup"><span data-stu-id="f6de2-157">For example, you might filter a list of resources based on the user name, returning only those resources that belong to that user.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a><span data-ttu-id="f6de2-158">使用授權設定屬性</span><span class="sxs-lookup"><span data-stu-id="f6de2-158">Using the [Authorize] Attribute</span></span>

<span data-ttu-id="f6de2-159">Web API 提供一個內建的授權篩選器,[授權屬性](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6de2-159">Web API provides a built-in authorization filter, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx).</span></span> <span data-ttu-id="f6de2-160">此篩選器檢查使用者是否經過身份驗證。</span><span class="sxs-lookup"><span data-stu-id="f6de2-160">This filter checks whether the user is authenticated.</span></span> <span data-ttu-id="f6de2-161">如果沒有,它將返回 HTTP 狀態代碼 401(未授權),而不調用該操作。</span><span class="sxs-lookup"><span data-stu-id="f6de2-161">If not, it returns HTTP status code 401 (Unauthorized), without invoking the action.</span></span>

<span data-ttu-id="f6de2-162">您可以全域、控制器等級或單一次操作等級應用篩選器。</span><span class="sxs-lookup"><span data-stu-id="f6de2-162">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>

<span data-ttu-id="f6de2-163">**全域**:要限制每個 Web API 控制器的存取,將**授權屬性**篩選器加入到全域篩選器清單中:</span><span class="sxs-lookup"><span data-stu-id="f6de2-163">**Globally**: To restrict access for every Web API controller, add the **AuthorizeAttribute** filter to the global filter list:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="f6de2-164">**控制器**:要限制特定控制器的存取,將篩選器作為屬性新增到控制器:</span><span class="sxs-lookup"><span data-stu-id="f6de2-164">**Controller**: To restrict access for a specific controller, add the filter as an attribute to the controller:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="f6de2-165">**操作**:要限制特定操作的存取,將屬性加入操作方法:</span><span class="sxs-lookup"><span data-stu-id="f6de2-165">**Action**: To restrict access for specific actions, add the attribute to the action method:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="f6de2-166">或者,您可以限制控制器,然後允許使用`[AllowAnonymous]`屬性 匿名訪問特定操作。</span><span class="sxs-lookup"><span data-stu-id="f6de2-166">Alternatively, you can restrict the controller and then allow anonymous access to specific actions, by using the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="f6de2-167">在下面的範例中,`Post`該方法受到限制`Get`, 但該方法允許匿名訪問。</span><span class="sxs-lookup"><span data-stu-id="f6de2-167">In the following example, the `Post` method is restricted, but the `Get` method allows anonymous access.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="f6de2-168">在前面的示例中,篩選器允許任何經過身份驗證的使用者訪問受限制的方法;只有匿名使用者被擋在外。您還可以限制對特定使用者或特定角色的使用者的訪問:</span><span class="sxs-lookup"><span data-stu-id="f6de2-168">In the previous examples, the filter allows any authenticated user to access the restricted methods; only anonymous users are kept out. You can also limit access to specific users or to users in specific roles:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="f6de2-169">Web API 控制器的授權**屬性**篩選器位於**System.Web.http**命名空間中。</span><span class="sxs-lookup"><span data-stu-id="f6de2-169">The **AuthorizeAttribute** filter for Web API controllers is located in the **System.Web.Http** namespace.</span></span> <span data-ttu-id="f6de2-170">**系統.Web.Mvc**命名空間中有 MVC 控制器的類似篩選器,該篩選器與 Web API 控制器不相容。</span><span class="sxs-lookup"><span data-stu-id="f6de2-170">There is a similar filter for MVC controllers in the **System.Web.Mvc** namespace, which is not compatible with Web API controllers.</span></span>

### <a name="custom-authorization-filters"></a><span data-ttu-id="f6de2-171">自訂授權篩選器</span><span class="sxs-lookup"><span data-stu-id="f6de2-171">Custom Authorization Filters</span></span>

<span data-ttu-id="f6de2-172">要編寫自訂授權篩選器,請派生自以下類型之一:</span><span class="sxs-lookup"><span data-stu-id="f6de2-172">To write a custom authorization filter, derive from one of these types:</span></span>

- <span data-ttu-id="f6de2-173">**授權屬性**.</span><span class="sxs-lookup"><span data-stu-id="f6de2-173">**AuthorizeAttribute**.</span></span> <span data-ttu-id="f6de2-174">擴展此類以基於當前使用者和使用者的角色執行授權邏輯。</span><span class="sxs-lookup"><span data-stu-id="f6de2-174">Extend this class to perform authorization logic based on the current user and the user's roles.</span></span>
- <span data-ttu-id="f6de2-175">**授權篩選器屬性**.</span><span class="sxs-lookup"><span data-stu-id="f6de2-175">**AuthorizationFilterAttribute**.</span></span> <span data-ttu-id="f6de2-176">擴展此類以執行不一定基於當前使用者或角色的同步授權邏輯。</span><span class="sxs-lookup"><span data-stu-id="f6de2-176">Extend this class to perform synchronous authorization logic that is not necessarily based on the current user or role.</span></span>
- <span data-ttu-id="f6de2-177">**I 授權篩選器**。</span><span class="sxs-lookup"><span data-stu-id="f6de2-177">**IAuthorizationFilter**.</span></span> <span data-ttu-id="f6de2-178">實現此介面以執行非同步授權邏輯;例如,如果授權邏輯進行非同步 I/O 或網路調用。</span><span class="sxs-lookup"><span data-stu-id="f6de2-178">Implement this interface to perform asynchronous authorization logic; for example, if your authorization logic makes asynchronous I/O or network calls.</span></span> <span data-ttu-id="f6de2-179">(如果授權邏輯是 CPU 綁定的,則從**授權篩選器屬性**派生會更簡單,因為則不需要編寫非同步方法。</span><span class="sxs-lookup"><span data-stu-id="f6de2-179">(If your authorization logic is CPU-bound, it is simpler to derive from **AuthorizationFilterAttribute**, because then you don't need to write an asynchronous method.)</span></span>

<span data-ttu-id="f6de2-180">下圖顯示了**授權屬性**類的類層次結構。</span><span class="sxs-lookup"><span data-stu-id="f6de2-180">The following diagram shows the class hierarchy for the **AuthorizeAttribute** class.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a><span data-ttu-id="f6de2-181">控制器操作的授權</span><span class="sxs-lookup"><span data-stu-id="f6de2-181">Authorization Inside a Controller Action</span></span>

<span data-ttu-id="f6de2-182">在某些情況下,您可以允許請求繼續,但基於主體更改行為。</span><span class="sxs-lookup"><span data-stu-id="f6de2-182">In some cases, you might allow a request to proceed, but change the behavior based on the principal.</span></span> <span data-ttu-id="f6de2-183">例如,返回的資訊可能會根據使用者的角色而變化。</span><span class="sxs-lookup"><span data-stu-id="f6de2-183">For example, the information that you return might change depending on the user's role.</span></span> <span data-ttu-id="f6de2-184">在控制器方法中,可以從**ApiController.User**屬性獲取當前主體。</span><span class="sxs-lookup"><span data-stu-id="f6de2-184">Within a controller method, you can get the current principal from the **ApiController.User** property.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
