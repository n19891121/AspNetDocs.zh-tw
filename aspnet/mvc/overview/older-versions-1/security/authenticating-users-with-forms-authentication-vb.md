---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: 使用表單身份驗證 (VB) 對使用者進行身份驗證 |微軟文件
author: rick-anderson
description: 瞭解如何使用 [授權] 屬性來密碼保護 MVC 應用程式中的特定頁面。 您也瞭解如何使用網站管理...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 9e3117af55db2effed20b6421c2322f1c265f1c7
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540814"
---
# <a name="authenticating-users-with-forms-authentication-vb"></a>使用表單驗證驗證使用者 (VB)

由[微軟](https://github.com/microsoft)

> 瞭解如何使用 [授權] 屬性來密碼保護 MVC 應用程式中的特定頁面。 您將瞭解如何使用網站管理工具創建和管理使用者和角色。 您還瞭解如何配置使用者帳戶和角色資訊的儲存位置。

本教學的目的是說明如何使用表單身分驗證來密碼保護ASP.NET MVC 應用程式中的檢視。 您將瞭解如何使用網站管理工具創建使用者和角色。 您還學習如何防止未經授權的使用者呼叫控制器操作。 最後,您將瞭解如何配置使用者名和密碼的儲存位置。

#### <a name="using-the-web-site-administration-tool"></a>使用網站管理工具

在做其他事情之前,我們應該從創建一些使用者和角色開始。 創建新使用者和角色的最簡單方法是利用 Visual Studio 2008 網站管理工具。 您可以通過選擇選單選項 **「專案」ASP.NET 設定**啟動此工具。 或者,您可以通過單擊位於解決方案資源管理器視窗頂部的鎚子(有點可怕)圖示啟動網站管理工具(參見圖 1)。

**圖 1 - 啟動網站管理工具**

![clip_image002[4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

在網站管理工具中,您可以通過選擇「安全」選項卡創建新使用者和角色。按一下「**創建使用者**」連結以創建名為 Stephen 的新使用者(參見圖 2)。 向 Stephen 使用者提供所需的任何密碼(例如,*機密*)。

**圖 2 = 建立新使用者**

![clip_image004[4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

通過首先啟用角色和定義一個或多個角色來創建新角色。 以按下 **「啟用角色」連結啟用角色**。 接下來,通過單擊 **「創建或管理角色」連結創建**名為 *「管理員*」的角色(參見圖 3)。

**圖 3 • 建立新角色**

![clip_image006[4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

最後,通過單擊"創建使用者"連結並在創建 Sally 時選擇管理員(參見圖 4),創建名為 Sally 的新使用者並將 Sally 與管理員角色相關聯。

**圖 4 = 將使用者新增到角色**

![clip_image008[4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

當所有說和完成,你應該有兩個新的使用者叫斯蒂芬和莎莉。 您還應具有名為"管理員"的新角色。 Sally 是管理員角色的成員,而斯蒂芬不是。

#### <a name="requiring-authorization"></a>需要授權

在使用者調用控制器操作之前,可以通過將 [授權] 屬性添加到操作,要求使用者進行身份驗證。 您可以將 [授權] 屬性應用於單個控制器操作,也可以將此屬性應用於整個控制器類。

例如,清單 1 中的控制器公開名為「公司機密」的操作。 由於此操作使用 [授權] 屬性進行修飾,因此除非對使用者進行身份驗證,否則無法調用此操作。

**清單1 = 控制器\主控制器.vb**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

如果您在瀏覽器的位址列中輸入 URL/Home/CompanySecrets 來呼叫公司機密()操作,而您不是經過身份驗證的使用者,則將自動重定向到登入檢視(參見圖 5)。

**圖 5 = 登入檢視**

![clip_image010[4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

您可以使用「登錄」檢視輸入使用者名稱和密碼。 如果您不是註冊用戶,則可以按下**註冊**連結以導航到"註冊"視圖(參見圖 6)。 您可以使用"註冊"視圖創建新使用者帳戶。

**圖 6 = 寄存器檢視**

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

成功登錄后,您可以看到公司機密視圖(參見圖 7)。 預設情況下,您將繼續登錄,直到關閉瀏覽器視窗。

**圖 7 = 公司機密檢視**

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>依使用者名稱或使用者角色授權

可以使用 [授權] 屬性將對控制器操作的存取限制為一組特定使用者或一組特定的使用者角色。 例如,清單 2 中修改後的主控制器包含名為 StephenSecrets() 和管理員機密() 的兩個新操作。

**清單2 = 控制器\主控制器.vb**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

只有使用者名為 Stephen 的使用者才能調用 StephenSecrets() 操作。 所有其他使用者都重定向到「登錄」視圖。 「使用者」屬性接受使用者帳戶名稱的逗號分隔清單。

只有管理員角色中的用戶可以調用管理員機密() 操作。 例如,由於 Sally 是管理員組的成員,因此她可以調用管理員機密()操作。 所有其他使用者都重定向到「登錄」視圖。 角色屬性接受角色名稱的逗號分隔清單。

#### <a name="configuring-authentication"></a>設定認證

此時,您可能想知道使用者帳戶和角色資訊的存儲位置。 預設情況下,資訊存儲在 MVC 應用程式\_的應用程式數據資料夾中,名為 ASPNETDB.mdf 的 (RANU) SQL Express 資料庫中。 當您開始使用成員資格時,此資料庫由ASP.NET框架自動生成。

要查看解決方案資源管理器視窗中的 ASPNETDB.mdf 資料庫,首先需要選擇功能表選項"專案",顯示所有檔。

開發應用程式時,可以使用預設 SQL Express 資料庫。 但是,您很可能不希望為生產應用程式使用預設的 ASPNETDB.mdf 資料庫。 在這種情況下,您可以通過完成以下兩個步驟來更改使用者帳戶資訊的儲存位置:

1. 將應用程式服務資料庫物件新增到生產資料庫 - 變更應用程式連接字串以指向生產資料庫

第一步是將所有必要的資料庫物件(表和存儲過程)添加到生產資料庫中。 將這些物件添加到新資料庫的最簡單方法是利用ASP.NET SQL 伺服器設置嚮導(參見圖 8)。 您可以透過 Microsoft Visual Studio 2008 程式組開啟 Visual Studio 2008 指令提示符並從指令提示符執行以下指令來啟動此工具:

阿斯普內\_雷格斯

**圖 8 = ASP.NET SQL 伺服器設定精靈**

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

ASP.NET SQL 伺服器設置精靈使您能夠在網路上選擇 SQL Server 資料庫,並安裝 ASP.NET 應用程式服務所需的所有資料庫物件。 資料庫伺服器不需要位於本地電腦上。

> [!NOTE]
> 如果不想使用ASP.NET SQL 伺服器設定精靈,則可以在以下資料夾中找到用於添加應用程式服務資料庫物件的 SQL 文稿:
> 
> 
> C:[視窗]微軟.NET_框架_v2.0.50727

建立必要的資料庫物件後,需要修改 MVC 應用程式使用的資料庫連接。 修改 Web 設定 (Web.config) 檔案中的應用程式服務連接字串,以便它指向生產資料庫。 例如,清單中修改的連接指向名為 MyProductionDB 的資料庫(原始應用程式服務連接字串已註釋掉)。

**清單3 = Web.config**

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>設定資料庫權限

如果使用整合安全連接到資料庫,則需要添加正確的 Windows 使用者帳戶作為資料庫的登錄。 正確的帳戶取決於您是使用ASP.NET開發伺服器還是 Internet 資訊服務作為 Web 伺服器。 正確的使用者帳戶還取決於您的操作系統。

如果使用ASP.NET開發伺服器(Visual Studio 使用的預設Web伺服器),則應用程式將在Windows使用者帳戶的上下文中執行。 在這種情況下,您需要將 Windows 使用者帳戶添加為資料庫伺服器登錄名。

或者,如果您使用的是互聯網資訊服務,則需要將 ASPNET 帳戶或 NT AUTHORITY/網路服務帳戶添加為資料庫伺服器登錄名。 如果使用 Windows XP,則添加 ASPNET 帳戶作為資料庫的登錄名。 如果您使用的是較新的作業系統,如 Windows Vista 或 Windows Server 2008,則添加 NT AUTHORITY/網路服務帳戶作為資料庫登錄。

您可以使用 Microsoft SQL 伺服器管理工作室向資料庫添加新使用者帳戶(參見圖 9)。

**圖 9 = 建立新的 Microsoft SQL Server 登入名稱**

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

建立所需的登錄後,需要將登錄映射到具有正確資料庫角色的資料庫使用者。 按兩下登入名並選擇「使用者映射」選項卡。選擇一個或多個應用程式服務資料庫角色。 例如,為了對使用者進行身份驗證,您需要啟用 aspnet\_\_成員資格 基本訪問資料庫角色。 要建立新使用者,您需要啟用 aspnet\_\_成員資格 完全訪問資料庫角色(參見圖 10)。

**圖 10 = 新增應用程式服務資料庫角色**

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a>總結

在本教學中,您學習了在構建 ASP.NET MVC 應用程式時如何使用窗體身份驗證。 首先,您學習了如何通過利用網站管理工具創建新使用者和角色。 接下來,您學習了如何使用 [授權] 屬性來防止未經授權的使用者調用控制器操作。 最後,您學習了如何配置 MVC 應用程式以在生產資料庫中儲存使用者和角色資訊。

> [!div class="step-by-step"]
> [前一個](preventing-javascript-injection-attacks-cs.md)
> [下一個](authenticating-users-with-windows-authentication-vb.md)
