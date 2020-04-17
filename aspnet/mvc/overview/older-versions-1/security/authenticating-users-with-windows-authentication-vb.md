---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
title: 使用 Windows 身份驗證 (VB) 對使用者進行身份驗證 |微軟文件
author: rick-anderson
description: 瞭解如何在 MVC 應用程式的上下文中使用 Windows 身份驗證。 您將瞭解如何在應用程式的 Web 身份驗證中開啟 Windows 身份認證...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 532fa051-7d5c-4d6d-87f6-339ce4b84c44
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 446dcc338f61e1f76478c1085773e7ad089c73f4
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540593"
---
# <a name="authenticating-users-with-windows-authentication-vb"></a>使用Windows 驗證驗證使用者 (VB)

由[微軟](https://github.com/microsoft)

> 瞭解如何在 MVC 應用程式的上下文中使用 Windows 身份驗證。 您將瞭解如何在應用程式的 Web 設定檔中啟用 Windows 身份驗證,以及如何使用 IIS 設定身份驗證。 最後,您將瞭解如何使用 [授權] 屬性將控制器操作的存取限制為特定的 Windows 使用者或組。

本教學的目的是說明如何利用 Internet 資訊服務中內置的安全功能來密碼保護 MVC 應用程式中的視圖。 您將瞭解如何僅允許特定 Windows 使用者或屬於特定 Windows 組的成員的使用者呼叫控制器操作。

當您構建內部公司網站(Intranet 網站)並希望使用者在瀏覽網站時能夠使用其標準 Windows 使用者名和密碼時,使用 Windows 身份驗證是有意義的。 如果您正在構建面向外的網站(Internet 網站),請考慮改用表單身份驗證。

#### <a name="enabling-windows-authentication"></a>開啟 Windows 認證

創建新ASP.NET MVC 應用程式時,預設情況下不會啟用Windows身份驗證。 表單身份驗證是為 MVC 應用程式啟用的預設身份驗證類型。 必須透過修改 MVC 應用程式的 Web 設定 (Web.config) 檔來啟用 Windows 身份驗證。 尋找&lt;認證&gt;管理系統並進行修改以使用 Windows 而不是窗體身份驗證,如下所示:

[!code-xml[Main](authenticating-users-with-windows-authentication-vb/samples/sample1.xml)]

啟用 Windows 身份驗證後,Web 伺服器將負責對使用者進行身份驗證。 通常,在創建和部署ASP.NET MVC 應用程式時,可以使用兩種不同類型的 Web 伺服器。

首先,在開發 MVC 應用程式時,您可以使用 Visual Studio 附帶的 ASP.NET 開發 Web 伺服器。 默認情況下,ASP.NET開發 Web 伺服器在當前 Windows 帳戶(用於登錄到 Windows 的任何帳戶)的上下文中執行所有頁面。

ASP.NET開發 Web 伺服器還支援 NTLM 身份驗證。 您可以透過在解決方案資源管理器視窗中右鍵單擊專案名稱並選擇「屬性」來啟用 NTLM 身份驗證。 接下來,選擇 Web 選項卡並選中 NTLM 複選框(參見圖 1)。

**圖 1 = 為 ASP.NET 開發 Web 伺服器啟用 NTLM 身份驗證**

![clip_image002](authenticating-users-with-windows-authentication-vb/_static/image1.jpg)

對於生產 Web 應用程式,使用 IIS 作為 Web 伺服器。 IIS 支援多種類型的身份驗證,包括:

- 基本身份驗證 – 定義為 HTTP1.0 協定的一部分。 在 Internet 上以明文(Base64 編碼)發送使用者名稱和密碼。 - 摘要身份驗證 – 通過互聯網發送密碼的哈希值,而不是密碼本身。 - 整合的 Windows (NTLM) 身份驗證 – 使用視窗在 Intranet 環境中使用的最佳身份驗證類型。 - 憑證身份驗證 – 使用用戶端證書啟用身份驗證。 證書映射到 Windows 使用者帳戶。

> [!NOTE] 
> 
> 有關這些不同類型的身份驗證的更詳細概述,請參閱[https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)。

您可以使用 Internet 資訊服務管理器啟用特定類型的身份驗證。 請注意,對於每個操作系統,所有類型的身份驗證都不可用。 此外,如果您將 IIS 7.0 與 Windows Vista 一起使用,則需要在 Internet 資訊服務管理器中顯示不同類型的 Windows 身份驗證之前啟用這些身份驗證。 打開**控制面板、程式、程式和功能,打開或關閉 Windows 功能**,並展開 Internet 資訊服務節點(參見圖 2)。

**圖 2 = 啟用 Windows IIS 功能**

![clip_image004](authenticating-users-with-windows-authentication-vb/_static/image2.jpg)

使用 Internet 資訊服務,您可以啟用或禁用不同類型的身份驗證。 例如,圖 3 演示了在使用 IIS 7.0 時禁用匿名身份驗證和啟用集成 Windows (NTLM) 身份驗證。

**圖 3 = 啟用整合 Windows 認證**

![clip_image006](authenticating-users-with-windows-authentication-vb/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>授權 Windows 使用者和群組

啟用 Windows 身份驗證後,&lt;可以使用&gt;「授權」 屬性來控制對控制器或控制器操作的訪問。 此屬性可以應用於整個 MVC 控制器或特定控制器操作。

例如,清單 1 中的主頁控制器公開了名為 Index()、公司機密()和 StephenSecrets() 的三個操作。 任何人都可以調用 Index() 操作。 但是,只有 Windows 本地經理組的成員才能調用公司機密()操作。 最後,只有名為 Stephen 的 Windows 功能變數使用者(在雷德蒙德域中)才能調用 StephenSecrets() 操作。

**清單1 = 控制器\主控制器.vb**

[!code-vb[Main](authenticating-users-with-windows-authentication-vb/samples/sample2.vb)]

> [!NOTE]
> 由於 Windows 使用者帳戶控制 (UAC),使用 Windows Vista 或 Windows 伺服器 2008 時,本地管理員組的行為將不同於其他組。 除非您&lt;&gt;修改 電腦的 UAC 設定,否則"授權"屬性將無法正確識別本地管理員組的成員。

當您嘗試調用控制器操作而不具有正確的許可權時,具體會發生什麼情況取決於啟用的身份驗證類型。 默認情況下,當使用ASP.NET開發伺服器時,只需獲得一個空白頁。 該頁面提供**401 未授權**HTTP 回應狀態。

另一方面,如果您使用的 IIS 禁用了匿名身份驗證並啟用了基本身份驗證,則每次請求受保護頁面時,您都會不斷收到登錄對話方塊提示(參見圖 4)。

**圖 4 = 基本身份驗證登入對話框**

![clip_image008](authenticating-users-with-windows-authentication-vb/_static/image4.jpg)

#### <a name="summary"></a>總結

本教程介紹了如何在ASP.NET MVC 應用程式的上下文中使用Windows身份驗證。 您學習了如何在應用程式的 Web 設定檔中啟用 Windows 身份驗證,以及如何使用 IIS 設定身份驗證。 最後,您學習了如何使用&lt;「授權&gt;」 屬性將控制器操作的存取限制為特定的 Windows 使用者或群組。

> [!div class="step-by-step"]
> [前一個](authenticating-users-with-forms-authentication-vb.md)
> [下一個](preventing-javascript-injection-attacks-vb.md)
