---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET Web API 中的驗證和授權 |Microsoft Docs
author: MikeWasson
description: 提供 ASP.NET Web API 中驗證和授權的一般總覽。
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345624"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>ASP.NET Web API 中的驗證和授權

由 [Mike Wasson](https://github.com/MikeWasson)

您已建立 web API，但現在想要控制其存取權。 在這一系列的文章中，我們將探討用來保護 web API 免于未經授權使用者安全的一些選項。 此系列將涵蓋驗證和授權。

- *驗證* 正在得知使用者的身分識別。 例如，Alice 以其使用者名稱和密碼登入，而伺服器使用密碼來驗證 Alice。
- *授權* 正在決定是否允許使用者執行動作。 例如，Alice 有權取得資源，但無法建立資源。

本系列的第一篇文章提供 ASP.NET Web API 中驗證和授權的一般總覽。 其他主題則說明 Web API 的常見驗證案例。

> [!NOTE]
> 感謝審查本系列的人員，並提供寶貴的意見反應： Rick Anderson、于 levi Broderick、Barry Dorrans、Tom Dykstra、Hongmei Ge、David Matson、Daniel Roth、Tim Teebken。

## <a name="authentication"></a>驗證

Web API 會假設在主機中進行驗證。 針對 web 裝載，主機是 IIS，使用 HTTP 模組進行驗證。 您可以將專案設定為使用內建在 IIS 或 ASP.NET 中的任何驗證模組，或撰寫您自己的 HTTP 模組來執行自訂驗證。

當主機驗證使用者時，它會建立一個 *主體*，這是一個 [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) 物件，代表用來執行程式碼的安全性內容。 主機會藉由設定 **thread.currentprincipal**，將主體附加至目前的執行緒。 主體包含相關聯的身分 **識別** 物件，其中包含使用者的相關資訊。 如果使用者經過驗證， **IsAuthenticated** 屬性就會傳回 **true**。 若為匿名要求， **IsAuthenticated** 會傳回 **false**。 如需主體的詳細資訊，請參閱以 [角色為基礎的安全性](https://msdn.microsoft.com/library/shz8h065.aspx)。

### <a name="http-message-handlers-for-authentication"></a>用於驗證的 HTTP 訊息處理常式

您可以將驗證邏輯放入 [HTTP 訊息處理常式](../advanced/http-message-handlers.md)中，而不是使用主機進行驗證。 在此情況下，訊息處理常式會檢查 HTTP 要求並設定主體。

何時應該使用訊息處理常式進行驗證？ 以下是一些取捨：

- HTTP 模組會看到所有經過 ASP.NET 管線的要求。 訊息處理常式只會看到路由傳送至 Web API 的要求。
- 您可以設定每個路由的訊息處理常式，讓您將驗證配置套用至特定路由。
- HTTP 模組是 IIS 專用的。 訊息處理常式與主機無關，因此可以與 web 裝載和自我裝載一起使用。
- HTTP 模組會參與 IIS 記錄、審核等等。
- HTTP 模組會在管線中稍早執行。 如果您在訊息處理常式中處理驗證，則在執行處理常式之前，不會設定主體。 此外，當回應離開訊息處理常式時，主體會還原回上一個主體。

一般而言，如果您不需要支援自我裝載，HTTP 模組是較佳的選項。 如果您需要支援自我裝載，請考慮使用訊息處理常式。

### <a name="setting-the-principal"></a>設定主體

如果您的應用程式執行任何自訂驗證邏輯，您必須在兩個地方設定主體：

- **Thread.currentprincipal**。 這個屬性是在 .NET 中設定執行緒主體的標準方式。
- **HttpCoNtext. 目前的. 使用者**。 這個屬性是 ASP.NET 特有的。

下列程式碼顯示如何設定主體：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

針對 web 裝載，您必須在這兩個地方設定主體：否則安全性內容可能會不一致。 但是，如果是自我裝載， **HttpCoNtext** 就是 null。 為了確保您的程式碼與主機無關，因此，請先檢查是否有 null，再指派給 **HttpCoNtext. Current**，如下所示。

## <a name="authorization"></a>授權

稍後在管線中會有更接近控制器的授權。 這可讓您在授與資源的存取權時，進行更細微的選擇。

- *授權篩選準則* 會在控制器動作之前執行。 如果要求未獲授權，篩選準則會傳回錯誤回應，且不會叫用動作。
- 在控制器動作中，您可以從 **ApiController** 屬性取得目前的主體。 例如，您可能會根據使用者名稱篩選資源清單，只傳回屬於該使用者的資源。

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>使用 [授權] 屬性

Web API 提供內建的授權篩選準則 [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。 此篩選準則會檢查使用者是否經過驗證。 如果沒有，則會傳回 HTTP 狀態碼 401 (未經授權的) ，而不會叫用動作。

您可以在控制器層級或在個別動作的層級上，全域套用篩選。

**全域**：若要限制每個 Web API 控制器的存取，請將 **AuthorizeAttribute** 篩選器新增至全域篩選清單：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**控制器**：若要限制特定控制器的存取，請將篩選器新增為控制器的屬性：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**動作**：若要限制特定動作的存取權，請將屬性新增至動作方法：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

或者，您可以使用屬性來限制控制器，然後允許匿名存取特定動作 `[AllowAnonymous]` 。 在下列範例中， `Post` 方法會受到限制，但 `Get` 方法允許匿名存取。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

在先前的範例中，篩選準則允許任何已驗證的使用者存取受限制的方法;只會保留匿名使用者。您也可以限制特定使用者或特定角色中的使用者存取權：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Web API 控制器的 **AuthorizeAttribute** 篩選器位於 **HTTP.sys** 命名空間中。 MVC 命名空間中的 MVC 控制器有 **類似的篩選** ，與 Web API 控制器不相容。

### <a name="custom-authorization-filters"></a>自訂授權篩選準則

若要撰寫自訂授權篩選準則，請從下列其中一種類型衍生：

- **AuthorizeAttribute**。 擴充此類別，以根據目前的使用者和使用者的角色來執行授權邏輯。
- **AuthorizationFilterAttribute**。 擴充此類別，以執行不一定是以目前使用者或角色為基礎的同步授權邏輯。
- **IAuthorizationFilter**。 執行此介面來執行非同步授權邏輯;例如，如果您的授權邏輯會進行非同步 i/o 或網路呼叫。  (如果您的授權邏輯是受 CPU 限制，則從 **AuthorizationFilterAttribute**衍生會比較簡單，因為您不需要撰寫非同步方法。 ) 

下圖顯示 **AuthorizeAttribute** 類別的類別階層架構。

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>控制器動作內的授權

在某些情況下，您可能會允許要求繼續進行，但會根據主體來變更行為。 例如，您傳回的資訊可能會根據使用者的角色而變更。 在控制器方法中，您可以從 **ApiController** 屬性取得目前的主體。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
