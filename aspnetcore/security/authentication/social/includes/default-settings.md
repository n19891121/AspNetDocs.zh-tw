---
ms.openlocfilehash: a7be92adffc06ac0f25b84ea15d1a8c4896f4f9d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57168626"
---
<!--Don't update this for 2.2, use the 2.2 version --> 若要在呼叫[AddIdentity](/dotnet/api/microsoft.extensions.dependencyinjection.identityservicecollectionuiextensions.adddefaultidentity)設定的預設配置設定。 [AddAuthentication(String)](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication#Microsoft_Extensions_DependencyInjection_AuthenticationServiceCollectionExtensions_AddAuthentication_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_String_)多載集[DefaultScheme](/dotnet/api/microsoft.aspnetcore.authentication.authenticationoptions.defaultscheme)屬性。 [AddAuthentication (動作&lt;AuthenticationOptions&gt;)](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication#Microsoft_Extensions_DependencyInjection_AuthenticationServiceCollectionExtensions_AddAuthentication_Microsoft_Extensions_DependencyInjection_IServiceCollection_System_Action_Microsoft_AspNetCore_Authentication_AuthenticationOptions__)多載可讓設定驗證選項，可用來設定預設的驗證配置，針對不同用途。 後續呼叫`AddAuthentication`先前設定的覆寫[AuthenticationOptions](/dotnet/api/microsoft.aspnetcore.builder.authenticationoptions)屬性。

[AuthenticationBuilder](/dotnet/api/microsoft.aspnetcore.authentication.authenticationbuilder)註冊驗證處理常式的擴充方法可能 lze volat pouze jednou 每個驗證配置。 多載的存在可供設定的配置內容、 結構描述名稱，以及顯示名稱。
