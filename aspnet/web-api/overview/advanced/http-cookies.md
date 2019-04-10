---
uid: web-api/overview/advanced/http-cookies
title: HTTP Cookie 在 ASP.NET Web API-ASP.NET 4.x
author: MikeWasson
description: 描述如何傳送和接收 HTTP cookie 在 Web API 中，asp.net 4.x。
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: cd6391582f05ab80c4bd45a455a2ce488d1186c1
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418322"
---
# <a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="4cf24-103">ASP.NET Web API 中的 HTTP Cookie</span><span class="sxs-lookup"><span data-stu-id="4cf24-103">HTTP Cookies in ASP.NET Web API</span></span>

<span data-ttu-id="4cf24-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4cf24-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="4cf24-105">本主題描述如何傳送和接收 Web API 中的 HTTP cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-105">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="4cf24-106">HTTP Cookie 的背景</span><span class="sxs-lookup"><span data-stu-id="4cf24-106">Background on HTTP Cookies</span></span>

<span data-ttu-id="4cf24-107">本節提供 cookie 在 HTTP 層級的實作方式的簡短概觀。</span><span class="sxs-lookup"><span data-stu-id="4cf24-107">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="4cf24-108">如需詳細資訊，請參閱[RFC 6265](http://tools.ietf.org/html/rfc6265)。</span><span class="sxs-lookup"><span data-stu-id="4cf24-108">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="4cf24-109">Cookie 是一種伺服器會傳送 HTTP 回應中的資料。</span><span class="sxs-lookup"><span data-stu-id="4cf24-109">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="4cf24-110">用戶端 （選擇性） 儲存 cookie，並傳回它在後續的要求。</span><span class="sxs-lookup"><span data-stu-id="4cf24-110">The client (optionally) stores the cookie and returns it on subsequent requests.</span></span> <span data-ttu-id="4cf24-111">這可讓用戶端與伺服器共用狀態。</span><span class="sxs-lookup"><span data-stu-id="4cf24-111">This allows the client and server to share state.</span></span> <span data-ttu-id="4cf24-112">若要設定的 cookie，伺服器會納入回應 Set-cookie 標頭。</span><span class="sxs-lookup"><span data-stu-id="4cf24-112">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="4cf24-113">Cookie 的格式為名稱 / 值組，以選擇性屬性。</span><span class="sxs-lookup"><span data-stu-id="4cf24-113">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="4cf24-114">例如: </span><span class="sxs-lookup"><span data-stu-id="4cf24-114">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="4cf24-115">以下是具有屬性範例：</span><span class="sxs-lookup"><span data-stu-id="4cf24-115">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="4cf24-116">若要返回伺服器的 cookie，用戶端會包含 Cookie 標頭之後的要求中。</span><span class="sxs-lookup"><span data-stu-id="4cf24-116">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="4cf24-117">HTTP 回應可以包含多個 Set-cookie 標頭。</span><span class="sxs-lookup"><span data-stu-id="4cf24-117">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="4cf24-118">用戶端傳回使用單一的 Cookie 標頭的多個 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-118">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="4cf24-119">範圍和持續時間的 cookie 就會受 Set-cookie 標頭中的下列屬性：</span><span class="sxs-lookup"><span data-stu-id="4cf24-119">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="4cf24-120">**網域**:會告知用戶端網域應接收的 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-120">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="4cf24-121">例如，如果網域是"example.com 」，用戶端 cookie 傳回給為 example.com，則每一個子網域。</span><span class="sxs-lookup"><span data-stu-id="4cf24-121">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="4cf24-122">如果未指定，網域會是原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="4cf24-122">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="4cf24-123">**路徑**:將 cookie 限制網域內指定的路徑。</span><span class="sxs-lookup"><span data-stu-id="4cf24-123">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="4cf24-124">如果未指定，則會使用要求 URI 的路徑。</span><span class="sxs-lookup"><span data-stu-id="4cf24-124">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="4cf24-125">**到期**:設定 cookie 的到期日。</span><span class="sxs-lookup"><span data-stu-id="4cf24-125">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="4cf24-126">當計時器到期，用戶端就會刪除 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-126">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="4cf24-127">**最大壽命**:設定 cookie 的最長使用期限。</span><span class="sxs-lookup"><span data-stu-id="4cf24-127">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="4cf24-128">最長使用期限到達時，用戶端就會刪除 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-128">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="4cf24-129">如果兩個`Expires`並`Max-Age`設定，`Max-Age`會優先使用。</span><span class="sxs-lookup"><span data-stu-id="4cf24-129">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="4cf24-130">如果沒有設定，用戶端目前的工作階段結束時，就會刪除的 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-130">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="4cf24-131">（「 工作階段 」 的確切意義取決於使用者代理程式。）</span><span class="sxs-lookup"><span data-stu-id="4cf24-131">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="4cf24-132">不過，請注意，用戶端可能會忽略 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-132">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="4cf24-133">例如，使用者可能會停用 cookie，基於隱私原因。</span><span class="sxs-lookup"><span data-stu-id="4cf24-133">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="4cf24-134">用戶端可能會刪除 cookie 之前過期，或限制儲存的 cookie 數目。</span><span class="sxs-lookup"><span data-stu-id="4cf24-134">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="4cf24-135">基於隱私原因，用戶端通常會拒絕 「 協力廠商 」 cookie，該網域不符合原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="4cf24-135">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="4cf24-136">簡單地說，伺服器不應依賴取回它所設定的 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-136">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="4cf24-137">Web API 中的 cookie</span><span class="sxs-lookup"><span data-stu-id="4cf24-137">Cookies in Web API</span></span>

<span data-ttu-id="4cf24-138">若要將 cookie 加入至 HTTP 回應中，建立**CookieHeaderValue**執行個體，表示 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-138">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="4cf24-139">然後呼叫**AddCookies**擴充方法，其定義於**System.Net.Http。HttpResponseHeadersExtensions**類別，以新增 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-139">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="4cf24-140">例如，下列程式碼加入控制器動作中的 cookie:</span><span class="sxs-lookup"><span data-stu-id="4cf24-140">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="4cf24-141">請注意， **AddCookies**接受陣列**CookieHeaderValue**執行個體。</span><span class="sxs-lookup"><span data-stu-id="4cf24-141">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="4cf24-142">若要從用戶端要求中擷取的 cookie，呼叫**GetCookies**方法：</span><span class="sxs-lookup"><span data-stu-id="4cf24-142">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="4cf24-143">A **CookieHeaderValue**包含的集合**CookieState**執行個體。</span><span class="sxs-lookup"><span data-stu-id="4cf24-143">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="4cf24-144">每個**CookieState**代表一個 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-144">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="4cf24-145">使用索引子方法來取得**CookieState**依名稱所示。</span><span class="sxs-lookup"><span data-stu-id="4cf24-145">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="4cf24-146">結構化的 Cookie 資料</span><span class="sxs-lookup"><span data-stu-id="4cf24-146">Structured Cookie Data</span></span>

<span data-ttu-id="4cf24-147">許多瀏覽器限制多少的 cookie，它們會儲存&#8212;總數，以及每個網域的數目。</span><span class="sxs-lookup"><span data-stu-id="4cf24-147">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="4cf24-148">因此，它可用來將結構化的資料放入單一 cookie，而不是設定多個 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-148">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="4cf24-149">RFC 6265 未定義 cookie 資料的結構。</span><span class="sxs-lookup"><span data-stu-id="4cf24-149">RFC 6265 does not define the structure of cookie data.</span></span>


<span data-ttu-id="4cf24-150">使用**CookieHeaderValue**類別，您可以將傳遞的 cookie 資料的名稱 / 值組清單。</span><span class="sxs-lookup"><span data-stu-id="4cf24-150">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="4cf24-151">這些名稱 / 值組會編碼為 URL 編碼格式的 Set-cookie 標頭中的資料：</span><span class="sxs-lookup"><span data-stu-id="4cf24-151">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="4cf24-152">先前的程式碼會產生下列 Set-cookie 標頭：</span><span class="sxs-lookup"><span data-stu-id="4cf24-152">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="4cf24-153">**CookieState**類別會提供一個索引子方法，讓讀取要求訊息中的 cookie 中的子的值：</span><span class="sxs-lookup"><span data-stu-id="4cf24-153">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="4cf24-154">範例：設定和擷取的訊息處理常式中的 Cookie</span><span class="sxs-lookup"><span data-stu-id="4cf24-154">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="4cf24-155">先前的範例，示範了如何使用來自 Web API 控制器內的 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-155">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="4cf24-156">另一個選項是使用[訊息處理常式](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="4cf24-156">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="4cf24-157">訊息處理常式會叫用稍早於控制站的管線。</span><span class="sxs-lookup"><span data-stu-id="4cf24-157">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="4cf24-158">訊息處理常式可以從要求讀取 cookie，才能在要求到達控制器，或控制站產生回應之後，將 cookie 加入至回應。</span><span class="sxs-lookup"><span data-stu-id="4cf24-158">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="4cf24-159">下列程式碼顯示建立工作階段識別碼的訊息處理常式。</span><span class="sxs-lookup"><span data-stu-id="4cf24-159">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="4cf24-160">工作階段識別碼會儲存在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="4cf24-160">The session ID is stored in a cookie.</span></span> <span data-ttu-id="4cf24-161">處理常式會檢查工作階段 cookie 的要求。</span><span class="sxs-lookup"><span data-stu-id="4cf24-161">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="4cf24-162">如果要求不包含 cookie，處理常式就會產生新的工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="4cf24-162">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="4cf24-163">在任一情況下，處理常式會儲存在工作階段識別碼**HttpRequestMessage.Properties**屬性包。</span><span class="sxs-lookup"><span data-stu-id="4cf24-163">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="4cf24-164">它也會加入至 HTTP 回應的工作階段 cookie。</span><span class="sxs-lookup"><span data-stu-id="4cf24-164">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="4cf24-165">此實作不會驗證從用戶端的工作階段識別碼實際上所簽發的伺服器。</span><span class="sxs-lookup"><span data-stu-id="4cf24-165">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="4cf24-166">不使用它做為一種驗證 ！</span><span class="sxs-lookup"><span data-stu-id="4cf24-166">Don't use it as a form of authentication!</span></span> <span data-ttu-id="4cf24-167">此範例的重點是要顯示 HTTP cookie 管理。</span><span class="sxs-lookup"><span data-stu-id="4cf24-167">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="4cf24-168">控制器可以取得工作階段識別碼，從**HttpRequestMessage.Properties**屬性包。</span><span class="sxs-lookup"><span data-stu-id="4cf24-168">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
