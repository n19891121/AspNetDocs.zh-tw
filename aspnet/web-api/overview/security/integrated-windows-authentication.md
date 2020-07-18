---
uid: web-api/overview/security/integrated-windows-authentication
title: 整合式 Windows 驗證 |Microsoft Docs
author: MikeWasson
description: 描述如何在 ASP.NET Web API 中使用整合式 Windows 驗證。
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: c5fe57c4a20e28fa434659a75484e3a4c37195f8
ms.sourcegitcommit: 000cbcd1de66fe8a766f203ef2d6f009e4435f53
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2020
ms.locfileid: "86424788"
---
# <a name="integrated-windows-authentication"></a>整合式 Windows 驗證

由[Mike Wasson](https://github.com/MikeWasson)

整合式 Windows 驗證可讓使用者使用 Kerberos 或 NTLM，以其 Windows 認證登入。 用戶端會在授權標頭中傳送認證。 Windows 驗證最適合用於內部網路環境。 如需詳細資訊，請參閱 [Windows 驗證](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)。

| 優點 | 缺點 |
| --- | --- |
| 內建于 IIS 中。 | 不建議用於網際網路應用程式。 | 
| 不會傳送要求中的使用者認證。 | 需要用戶端中的 Kerberos 或 NTLM 支援。 |
| 如果用戶端電腦屬於網域（例如，內部網路應用程式），使用者就不需要輸入認證。 | 用戶端必須位於 Active Directory 網域。 |

> [!NOTE]
> 如果您的應用程式裝載于 Azure 上，而且您有內部部署 Active Directory 網域，請考慮將您的內部部署 AD 與 Azure Active Directory 同盟。 如此一來，使用者就可以使用其內部部署認證登入，但驗證是由 Azure AD 執行。 如需詳細資訊，請參閱[Azure 驗證](../../../visual-studio/overview/2012/windows-azure-authentication.md)。

若要建立使用整合式 Windows 驗證的應用程式，請選取 [MVC 4 專案] wizard 中的 [內部網路應用程式] 範本。 此專案範本會將下列設定放在 Web.config 檔案中：

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

在用戶端上，整合式 Windows 驗證可與任何支援[Negotiate](http://www.ietf.org/rfc/rfc4559.txt)驗證配置的瀏覽器搭配使用，其中包括大部分的主要瀏覽器。 針對 .NET 用戶端應用程式， **HttpClient**類別支援 Windows 驗證：

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

Windows 驗證容易遭受跨網站偽造要求（CSRF）攻擊。 請參閱[防止跨網站偽造要求（CSRF）攻擊](preventing-cross-site-request-forgery-csrf-attacks.md)。
