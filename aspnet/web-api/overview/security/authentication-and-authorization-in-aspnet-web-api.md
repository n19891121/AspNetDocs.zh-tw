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
# <a name="authentication-and-authorization-in-aspnet-web-api"></a>ASP.NET Web API 中的驗證和授權

由[邁克·瓦森](https://github.com/MikeWasson)

您已經創建了 Web API,但現在要控制對它的訪問。 在本系列文章中,我們將介紹一些保護 Web API 免受未經授權的使用者訪問的選項。 本系列將涵蓋身份驗證和授權。

- *身份驗證*是知道使用者的身份。 例如,Alice 使用使用者名稱和密碼登錄,伺服器使用密碼對 Alice 進行身份驗證。
- *授權*是決定是否允許使用者執行操作。 例如,Alice 有權獲取資源,但不能創建資源。

本系列的第一篇文章概述了ASP.NET Web API 中的身份驗證和授權。 其他主題描述 Web API 的常見身份驗證方案。

> [!NOTE]
> 感謝那些回顧這個系列並提供寶貴反饋的人:里克·安德森、利維·布羅德里克、巴里·多蘭斯、湯姆·戴克斯特拉、葛紅梅、大衛·馬特森、丹尼爾·羅斯、蒂姆·蒂肯。

## <a name="authentication"></a>驗證

Web API 假定身份驗證發生在主機中。 對於 Web 託管,主機是 IIS,它使用 HTTP 模組進行身份驗證。 您可以將專案配置為使用 IIS 或 ASP.NET 內置的任何身份驗證模組,或者編寫自己的 HTTP 模組以執行自定義身份驗證。

當主機對使用者進行身份驗證時,它會創建一個*主體*,它是一個[IThe 物件](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx),表示代碼運行的安全上下文。 主機通過設置**Thread.Currentthe 將**主體附加到當前線程。 主體包含一個關聯的**標識**物件,該物件包含有關使用者的資訊。 如果使用者已使用身份認證,**識別.Is 認證**屬性會傳回**true**。 對匿名要求 **,已身份驗證****傳回 false**。 有關主體的詳細資訊,請參閱[基於角色的安全性](https://msdn.microsoft.com/library/shz8h065.aspx)。

### <a name="http-message-handlers-for-authentication"></a>驗證的 HTTP 訊息處理程式

您可以將身份驗證邏輯放入[HTTP 消息處理程式](../advanced/http-message-handlers.md)中,而不是使用主機進行身份驗證。 在這種情況下,消息處理程序檢查 HTTP 請求並設置主體。

何時應該使用消息處理程序進行身份驗證? 以下是一些權衡:

- HTTP 模組看到通過ASP.NET管道的所有請求。 消息處理程式只看到路由到 Web API 的請求。
- 您可以設置每個路由的消息處理程式,這允許您將身份驗證方案應用於特定路由。
- HTTP 模組特定於 IIS。 消息處理程式與主機無關,因此可以同時用於 Web 託管和自託管。
- HTTP 模組參與 IIS 日誌記錄、審核等。
- HTTP 模組在管道中運行較早。 如果在消息處理程序中處理身份驗證,則在處理程式運行之前不會設置主體。 此外,當回應離開消息處理程式時,主體將還原到上一個主體。

通常,如果您不需要支援自託管,HTTP 模組是一個更好的選擇。 如果需要支援自託管,請考慮消息處理程式。

### <a name="setting-the-principal"></a>設置主體

如果應用程式執行任何自定義身份驗證邏輯,則必須在以下兩個位置設置主體:

- **執行緒.電流主體**。 此屬性是在 .NET 中設置線程主體的標準方法。
- **HTTPContext.當前.使用者**。 此屬性特定於ASP.NET。

以下代碼展示如何設定主體:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

對於 Web 託管,必須在兩個位置設置主體;否則,安全上下文可能會變得不一致。 但是,對於自託管 **,HTTPContext.current**為 null。 因此,為了確保代碼與主機無關,請在分配給**HTTPContext.Current**之前檢查空。

## <a name="authorization"></a>授權

授權在管道中稍後發生,更接近控制器。 這樣,在授予對資源的許可權時,可以做出更精細的選擇。

- *授權篩選器在*控制器操作之前運行。 如果請求未獲授權,篩選器將返回錯誤回應,並且不會調用該操作。
- 在控制器操作中,可以從**ApiController.User**屬性獲取當前主體。 例如,您可以根據使用者名篩選資源清單,僅返回屬於該使用者的資源。

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>使用授權設定屬性

Web API 提供一個內建的授權篩選器,[授權屬性](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。 此篩選器檢查使用者是否經過身份驗證。 如果沒有,它將返回 HTTP 狀態代碼 401(未授權),而不調用該操作。

您可以全域、控制器等級或單一次操作等級應用篩選器。

**全域**:要限制每個 Web API 控制器的存取,將**授權屬性**篩選器加入到全域篩選器清單中:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**控制器**:要限制特定控制器的存取,將篩選器作為屬性新增到控制器:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**操作**:要限制特定操作的存取,將屬性加入操作方法:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

或者,您可以限制控制器,然後允許使用`[AllowAnonymous]`屬性 匿名訪問特定操作。 在下面的範例中,`Post`該方法受到限制`Get`, 但該方法允許匿名訪問。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

在前面的示例中,篩選器允許任何經過身份驗證的使用者訪問受限制的方法;只有匿名使用者被擋在外。您還可以限制對特定使用者或特定角色的使用者的訪問:

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> Web API 控制器的授權**屬性**篩選器位於**System.Web.http**命名空間中。 **系統.Web.Mvc**命名空間中有 MVC 控制器的類似篩選器,該篩選器與 Web API 控制器不相容。

### <a name="custom-authorization-filters"></a>自訂授權篩選器

要編寫自訂授權篩選器,請派生自以下類型之一:

- **授權屬性**. 擴展此類以基於當前使用者和使用者的角色執行授權邏輯。
- **授權篩選器屬性**. 擴展此類以執行不一定基於當前使用者或角色的同步授權邏輯。
- **I 授權篩選器**。 實現此介面以執行非同步授權邏輯;例如,如果授權邏輯進行非同步 I/O 或網路調用。 (如果授權邏輯是 CPU 綁定的,則從**授權篩選器屬性**派生會更簡單,因為則不需要編寫非同步方法。

下圖顯示了**授權屬性**類的類層次結構。

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>控制器操作的授權

在某些情況下,您可以允許請求繼續,但基於主體更改行為。 例如,返回的資訊可能會根據使用者的角色而變化。 在控制器方法中,可以從**ApiController.User**屬性獲取當前主體。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
