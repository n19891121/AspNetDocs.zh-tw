---
uid: web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
title: '在 SQL Server 中建立成員資格架構 (c # ) |Microsoft Docs'
author: rick-anderson
description: 本教學課程一開始先檢查將必要架構新增至資料庫以使用 SqlMembershipProvider 的技巧。 之後我們 .。。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: b4ac129d-1b8e-41ca-a38f-9b19d7c7bb0e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 8160c422d7a20b7c6954f960e73d5d59f7b90a5f
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044736"
---
# <a name="creating-the-membership-schema-in-sql-server-c"></a>在 SQL Server 中建立成員資格結構描述 (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_04_CS.zip) 或 [下載 PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial04_MembershipSetup_cs.pdf)

> 本教學課程一開始先檢查將必要架構新增至資料庫以使用 SqlMembershipProvider 的技巧。 接下來，我們將檢查架構中的重要資料表，並討論其用途和重要性。 本教學課程最後會探討如何告訴 ASP.NET 應用程式，成員資格架構應該使用哪一個提供者。

## <a name="introduction"></a>簡介

先前的兩個教學課程使用表單驗證來識別網站訪客。 表單驗證架構可讓開發人員輕鬆地將使用者登入網站，並透過使用驗證票證在頁面流覽期間記住這些使用者。 `FormsAuthentication`類別包含產生票證的方法，並將其新增至訪客的 cookie。 會 `FormsAuthenticationModule` 檢查所有傳入的要求，對於具有有效驗證票證的要求，則會建立一個物件，並使其 `GenericPrincipal` `FormsIdentity` 與目前的要求產生關聯。 表單驗證只是一種機制，可在登入時將驗證票證授與訪客，並在後續要求中剖析該票證，以判斷使用者的身分識別。 若要讓 web 應用程式支援使用者帳戶，我們仍然需要執行使用者存放區，並新增功能來驗證認證、註冊新的使用者，以及其他使用者帳戶相關的工作。

在 ASP.NET 2.0 之前，開發人員會在攔截，以執行所有使用者帳戶相關的工作。 幸運的是，ASP.NET 團隊已辨識出這種缺點，並引進了具有 ASP.NET 2.0 的成員資格架構。 成員資格架構是 .NET Framework 中的一組類別，可提供程式設計介面來完成核心使用者帳戶相關工作。 此架構是以 [提供者模型](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)為基礎，可讓開發人員將自訂的執行插入標準化的 API。

如 <a id="Tutorial1"></a> [*安全性基本概念和 ASP.NET 支援*](../introduction/security-basics-and-asp-net-support-cs.md)教學課程中所述，.NET Framework 隨附兩個內建的成員資格提供者： [`ActiveDirectoryMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) 和 [`SqlMembershipProvider`](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) 。 顧名思義，會 `SqlMembershipProvider` 使用 Microsoft SQL Server 資料庫做為使用者存放區。 為了在應用程式中使用這個提供者，我們必須告訴提供者要使用哪個資料庫做為存放區。 您可能會想像，會 `SqlMembershipProvider` 預期使用者儲存資料庫必須有特定的資料庫資料表、views 和預存程式。 我們需要將此預期的架構新增至選取的資料庫。

本教學課程一開始會先檢查將必要架構新增至資料庫的技巧，以便使用 `SqlMembershipProvider` 。 接下來，我們將檢查架構中的重要資料表，並討論其用途和重要性。 本教學課程最後會探討如何告訴 ASP.NET 應用程式，成員資格架構應該使用哪一個提供者。

現在就開始吧！

## <a name="step-1-deciding-where-to-place-the-user-store"></a>步驟1：決定使用者存放區的放置位置

ASP.NET 應用程式的資料通常會儲存在資料庫的多個資料表中。 在執行 `SqlMembershipProvider` 資料庫架構時，我們必須決定是否將成員資格架構放在與應用程式資料相同的資料庫或替代資料庫中。

建議您在與應用程式資料相同的資料庫中找出成員資格架構，原因如下：

- 可**維護性**「將資料封裝在某個資料庫中的應用程式，比具有兩個不同資料庫的應用程式更容易瞭解、維護和部署。
- **關聯式完整性** 「藉由在與應用程式資料表相同的資料庫中找出成員資格相關資料表，可以在成員資格相關資料表和相關應用程式資料表的主鍵之間建立 [外鍵條件約束](http://en.wikipedia.org/wiki/Foreign_key) 。

如果您有多個應用程式都使用不同的資料庫，但需要共用一個通用的使用者存放區，則將使用者存放區和應用程式資料分離成不同的資料庫就有意義。

### <a name="creating-a-database"></a>建立資料庫

我們在第二個教學課程之後所建立的應用程式還不需要資料庫。 不過，我們現在需要一個使用者存放區。 讓我們建立一個，然後新增至提供者所需的架構 `SqlMembershipProvider` (請參閱步驟 2) 。

> [!NOTE]
> 在本教學課程系列中，我們將使用 [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) 資料庫來儲存應用程式資料表和 `SqlMembershipProvider` 架構。 這項決定的原因有兩個：首先，由於其成本免費，Express Edition 是 SQL Server 2005 的最牽扯不清可存取版本;其次，SQL Server 2005 Express Edition 資料庫可以直接放在 web 應用程式的 `App_Data` 資料夾中，讓它成為將資料庫和 web 應用程式封裝在單一 ZIP 檔案中的標準化，並在不需要任何特殊的設定指示或設定選項的情況下重新部署。 如果您想要遵循 SQL Server 的非 Express Edition 版本，請隨意使用。 這些步驟幾乎完全相同。 `SqlMembershipProvider`架構可搭配任何版本的 Microsoft SQL Server 2000 和更新版本使用。

在 [方案總管中，以滑鼠右鍵按一下 `App_Data` 資料夾，然後選擇 [加入新專案]。  (如果您沒有 `App_Data` 在專案中看到資料夾，請以滑鼠右鍵按一下方案總管中的專案，) 然後選取 `App_Data` [加入新專案] 對話方塊中的 [加入新專案] 對話方塊，加入宣告名為的新 SQL Database `SecurityTutorials.mdf` 。 在本教學課程中，我們會將 `SqlMembershipProvider` 此架構新增至這個資料庫; 在後續的教學課程中，我們會建立額外的資料表來捕捉我們的應用程式資料。

[![將名為 SecurityTutorials .mdf 資料庫的新 SQL Database 新增至 App_Data 資料夾](creating-the-membership-schema-in-sql-server-cs/_static/image2.png)](creating-the-membership-schema-in-sql-server-cs/_static/image1.png)

**圖 1**：將名為 Database 的新 SQL Database 新增 `SecurityTutorials.mdf` 至 `App_Data` 資料夾， ([按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image3.png)) 

將資料庫新增至 `App_Data` 資料夾，會自動將它包含在資料庫總管視圖中。  (在 Visual Studio 的非 Express 版本中，資料庫總管稱為伺服器總管。 ) 移至資料庫總管並展開剛剛加入的 `SecurityTutorials` 資料庫。 如果您在畫面上看不到資料庫總管，請移至 [View] 功能表並選擇 [資料庫總管]，或按 Ctrl + Alt + S。 如 [圖 2] 所示， `SecurityTutorials` 資料庫是空的，它不包含任何資料表、沒有任何視圖，而且沒有任何預存程式。

[![SecurityTutorials 資料庫目前是空的](creating-the-membership-schema-in-sql-server-cs/_static/image5.png)](creating-the-membership-schema-in-sql-server-cs/_static/image4.png)

**圖 2**： `SecurityTutorials` 資料庫目前為空白 ([按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image6.png)) 

## <a name="step-2-adding-thesqlmembershipproviderschema-to-the-database"></a>步驟2：將 `SqlMembershipProvider` 架構新增至資料庫

`SqlMembershipProvider`需要在使用者存放區資料庫中安裝一組特定的資料表、views 和預存程式。 您可以使用[ `aspnet_regsql.exe` 工具](https://msdn.microsoft.com/library/ms229862.aspx)新增這些必要的資料庫物件。 這個檔案位於 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\` 資料夾中。

> [!NOTE]
> 此 `aspnet_regsql.exe` 工具提供命令列功能和圖形化使用者介面。 圖形化介面比較容易使用，而且我們將在本教學課程中檢查。 當 `SqlMembershipProvider` 需要自動化新增架構時（例如在組建腳本或自動化測試案例中），命令列介面會很有用。

此 `aspnet_regsql.exe` 工具可用來將 *ASP.NET 應用程式服務* 新增或移除至指定的 SQL Server 資料庫。 ASP.NET 應用程式服務包含與的架構 `SqlMembershipProvider` ，以及 `SqlRoleProvider` 其他 ASP.NET 2.0 架構之 SQL 提供者的架構。 我們需要提供兩個位的資訊給 `aspnet_regsql.exe` 工具：

- 是否要新增或移除應用程式服務，以及
- 要從中新增或移除應用程式服務架構的資料庫

在提示資料庫使用 `aspnet_regsql.exe` 時，工具會要求我們提供資料庫所在的伺服器名稱、用於連接至資料庫的安全性認證，以及資料庫名稱。 如果您使用非 Express 版的 SQL Server，您應該已經知道這項資訊，因為這是您在透過 ASP.NET 網頁處理資料庫時，必須透過連接字串提供的相同資訊。 不過，在資料夾中使用 SQL Server 2005 Express Edition 資料庫時，判斷伺服器和資料庫名稱 `App_Data` 會比較複雜一點。

下一節將檢查在資料夾中指定 SQL Server 2005 Express Edition 資料庫之伺服器和資料庫名稱的簡單方式 `App_Data` 。 如果您不是使用 SQL Server 2005 Express Edition 請隨意跳到 [安裝應用程式服務] 區段。

### <a name="determining-the-server-and-database-name-for-a-sql-server-2005-express-edition-database-in-theapp_datafolder"></a>判斷資料夾中 SQL Server 2005 Express Edition 資料庫的伺服器和資料庫名稱 `App_Data`

為了使用此工具， `aspnet_regsql.exe` 我們必須知道伺服器和資料庫名稱。 伺服器名稱為 `localhost\InstanceName` 。 最有可能的是， *InstanceName* 是 `SQLExpress` 。 但是，如果您手動安裝 SQL Server 2005 Express Edition (亦即，您未在安裝 Visual Studio) 時自動安裝，則可能是您已選取不同的實例名稱。

資料庫名稱有點棘手，可以決定。 資料夾中的資料庫 `App_Data` 通常會有資料庫名稱，其中包含 [全域唯一識別碼](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) 以及資料庫檔案的路徑。 我們必須判斷此資料庫名稱，才能透過來新增應用程式服務架構 `aspnet_regsql.exe` 。

確定資料庫名稱最簡單的方式，就是透過 SQL Server Management Studio 檢查它。 SQL Server Management Studio 提供用來管理 SQL Server 2005 資料庫的圖形化介面，但未隨附 SQL Server 2005 的 Express 版。 好消息是， [您可以下載](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) 免費的 Express 版的 SQL Server Management Studio。

> [!NOTE]
> 如果您的電腦上也安裝了非 Express Edition 版本的 SQL Server 2005，則可能會安裝 Management Studio 的完整版本。 您可以使用完整版本來判斷資料庫名稱，並遵循下列與 Express Edition 相同的步驟。

從關閉 Visual Studio 開始，以確定資料庫檔案上 Visual Studio 所加諸的任何鎖定都已關閉。 接下來，啟動 SQL Server Management Studio，並連接至 `localhost\InstanceName` 資料庫以進行 SQL Server 2005 Express Edition。 如先前所述，實例名稱可能是 `SQLExpress` 。 在 [驗證] 選項中，選取 [Windows 驗證]。

[![連接到 SQL Server 2005 Express Edition 實例](creating-the-membership-schema-in-sql-server-cs/_static/image8.png)](creating-the-membership-schema-in-sql-server-cs/_static/image7.png)

**圖 3**：連接到 SQL Server 2005 Express Edition 實例 ([按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image9.png)) 

連接到 SQL Server 2005 Express Edition 實例之後，Management Studio 會顯示資料庫的資料夾、安全性設定、伺服器物件等等。 如果您展開 [資料庫] 索引標籤，您會看到 `SecurityTutorials.mdf` 資料庫 *未* 在資料庫實例中註冊，我們必須先附加資料庫。

以滑鼠右鍵按一下 [資料庫] 資料夾，然後從內容功能表中選擇 [附加]。 這會顯示 [附加資料庫] 對話方塊。 從這裡按一下 [加入] 按鈕，流覽至 `SecurityTutorials.mdf` 資料庫，然後按一下 [確定]。 [圖 4] 顯示在選取資料庫之後，[附加資料庫] 對話方塊 `SecurityTutorials.mdf` 。 [圖 5] 顯示成功附加資料庫之後 Management Studio 的物件總管。

[![附加 SecurityTutorials .mdf 資料庫](creating-the-membership-schema-in-sql-server-cs/_static/image11.png)](creating-the-membership-schema-in-sql-server-cs/_static/image10.png)

**圖 4**：附加 `SecurityTutorials.mdf` 資料庫 ([按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image12.png)) 

[![SecurityTutorials .mdf 資料庫會出現在 [資料庫] 資料夾中。](creating-the-membership-schema-in-sql-server-cs/_static/image14.png)](creating-the-membership-schema-in-sql-server-cs/_static/image13.png)

**圖 5**： `SecurityTutorials.mdf` 資料庫會出現在 [資料庫] 資料夾中， ([按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image15.png)) 

如 [圖 5] 所示， `SecurityTutorials.mdf` 資料庫的名稱是 abstruse。 讓我們將其變更為更容易記住的 (，並更輕鬆地輸入) 名稱。 以滑鼠右鍵按一下資料庫，從內容功能表中選擇 [重新命名]，然後將它重新命名 `SecurityTutorialsDatabase` 。 這不會變更檔案名，而是資料庫用來識別其本身以 SQL Server 的名稱。

[![將資料庫重新命名為 SecurityTutorialsDatabase](creating-the-membership-schema-in-sql-server-cs/_static/image17.png)](creating-the-membership-schema-in-sql-server-cs/_static/image16.png)

**圖 6**：重新命名資料庫以 `SecurityTutorialsDatabase` ([按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image18.png)) 

現在，我們知道資料庫檔案的伺服器和資料庫名稱 `SecurityTutorials.mdf` ： `localhost\InstanceName` 和 `SecurityTutorialsDatabase` 。 我們現在已準備好透過工具安裝應用程式服務 `aspnet_regsql.exe` 。

### <a name="installing-the-application-services"></a>安裝應用程式服務

若要啟動 `aspnet_regsql.exe` 工具，請移至 [開始] 功能表，然後選擇 [執行]。 `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\aspnet_regsql.exe`在文字方塊中輸入，然後按一下 [確定]。 或者，您可以使用 Windows 檔案總管向下切入至適當的資料夾，然後按兩下該檔案 `aspnet_regsql.exe` 。 這兩種方法都會得到相同的結果。

執行 `aspnet_regsql.exe` 沒有任何命令列引數的工具，會啟動 ASP.NET SQL Server 安裝 Wizard 圖形化使用者介面。 此嚮導可讓您輕鬆地在指定的資料庫上新增或移除 ASP.NET 的應用程式服務。 [圖 7] 所示的 wizard 第一個畫面會說明工具的用途。

[![使用 ASP.NET SQL Server 安裝 Wizard 新增成員資格架構](creating-the-membership-schema-in-sql-server-cs/_static/image20.png)](creating-the-membership-schema-in-sql-server-cs/_static/image19.png)

**圖 7**：使用 [ASP.NET SQL Server 安裝程式] 來新增成員資格架構 ([按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image21.png)) 

嚮導的第二個步驟會詢問我們是否要新增應用程式服務或移除它們。 由於我們想要加入所需的資料表、views 和預存程式 `SqlMembershipProvider` ，請選擇 [設定 SQL Server 的應用程式服務] 選項。 稍後，如果您想要從資料庫中移除此架構，請重新執行此嚮導，但改為選擇 [從現有的資料庫移除應用程式服務資訊] 選項。

[![選擇 [設定應用程式服務 SQL Server] 選項](creating-the-membership-schema-in-sql-server-cs/_static/image23.png)](creating-the-membership-schema-in-sql-server-cs/_static/image22.png)

**圖 8**：選擇 [設定應用程式服務 SQL Server] 選項 ([按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image24.png)) 

第三個步驟會提示您輸入資料庫資訊：伺服器名稱、驗證資訊，以及資料庫名稱。 如果您已遵循本教學課程，並已將資料庫附加至，並將它重新命名為，請 `SecurityTutorials.mdf` `App_Data` `localhost\InstanceName` `SecurityTutorialsDatabase` 使用下列值：

- 伺服器：`localhost\InstanceName`
- Windows 驗證
- 資料庫： `SecurityTutorialsDatabase`

[![輸入資料庫資訊](creating-the-membership-schema-in-sql-server-cs/_static/image26.png)](creating-the-membership-schema-in-sql-server-cs/_static/image25.png)

**圖 9**：輸入資料庫資訊 ([按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image27.png)) 

輸入資料庫資訊之後，請按 [下一步]。 最後一個步驟會摘要說明將採取的步驟。 按一下 [下一步] 以安裝應用程式服務，然後完成嚮導完成。

> [!NOTE]
> 如果您使用 Management Studio 附加資料庫，並重新命名資料庫檔案，請務必先卸離資料庫並關閉 Management Studio，然後再重新開啟 Visual Studio。 若要卸離 `SecurityTutorialsDatabase` 資料庫，請以滑鼠右鍵按一下資料庫名稱，然後從 [工作] 功能表選擇 [卸離]。

完成嚮導之後，請返回 Visual Studio，然後流覽至資料庫總管。 展開 [資料表] 資料夾。 您應該會看到一系列的資料表，其名稱開頭為前置詞 `aspnet_` 。 同樣地，您可以在 [Views] 和 [預存程式] 資料夾下找到各種不同的 views 和預存程式。 這些資料庫物件會構成應用程式服務架構。 我們將在步驟3中檢查成員資格和角色特定的資料庫物件。

[![資料庫中已加入各種資料表、Views 和預存程式](creating-the-membership-schema-in-sql-server-cs/_static/image29.png)](creating-the-membership-schema-in-sql-server-cs/_static/image28.png)

**圖 10**：已在資料庫中加入各種資料表、視圖及預存程式 ([按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image30.png)) 

> [!NOTE]
> `aspnet_regsql.exe`工具的圖形化使用者介面會安裝整個應用程式服務架構。 但是，當 `aspnet_regsql.exe` 您從命令列執行時，可以指定要安裝的特定應用程式服務元件 (或移除) 。 因此，如果您只想要加入和提供者所需的資料表、views 和預存程式 `SqlMembershipProvider` `SqlRoleProvider` ，請 `aspnet_regsql.exe` 從命令列執行。 或者，您可以手動執行所使用的適當 T-sql 建立腳本子集 `aspnet_regsql.exe` 。 這些腳本位於 `WINDIR%\Microsoft.Net\Framework\v2.0.50727\` 資料夾中，其名稱如、、、、等等 `InstallCommon.sql` `InstallMembership.sql` `InstallRoles.sql` `InstallProfile.sql` `InstallSqlState.sql` 。

至此，我們已建立所需的資料庫物件 `SqlMembershipProvider` 。 不過，我們仍然需要指示成員資格架構應該使用 (而不是 `SqlMembershipProvider` `ActiveDirectoryMembershipProvider`) ，而且 `SqlMembershipProvider` 應該使用 `SecurityTutorials` 資料庫。 我們將探討如何指定要使用的提供者，以及如何自訂步驟4中所選取提供者的設定。 但是首先，讓我們更深入探討剛建立的資料庫物件。

## <a name="step-3-a-look-at-the-schemas-core-tables"></a>步驟3：查看架構的核心資料表

在 ASP.NET 應用程式中使用成員資格和角色架構時，提供者會封裝執行詳細資料。 在後續的教學課程中，我們會透過 .NET Framework 的和類別，與這些架構進行介面 `Membership` `Roles` 。 使用這些高階 Api 時，我們不需要關注您自己的低層級詳細資料，例如執行的查詢或和所修改的資料表 `SqlMembershipProvider` `SqlRoleProvider` 。

如此一來，我們就可以安心地使用成員資格和角色架構，而不需要探索在步驟2中建立的資料庫架構。 不過，建立資料表來儲存應用程式資料時，可能需要建立與使用者或角色相關的實體。 在 `SqlMembershipProvider` `SqlRoleProvider` 建立應用程式資料表與步驟2中建立之資料表之間的外鍵條件約束時，有助於熟悉和架構。 此外，在某些罕見的情況下，我們可能需要直接在資料庫層級與使用者和角色存放區進行介面 (，而不是透過 `Membership` 或 `Roles` 類別) 。

### <a name="partitioning-the-user-store-into-applications"></a>將使用者存放區分割為應用程式

成員資格和角色架構的設計，就是可以在許多不同的應用程式之間共用單一使用者和角色存放區。 使用成員資格或角色架構的 ASP.NET 應用程式，必須指定要使用的應用程式分割區。 簡單地說，多個 web 應用程式可以使用相同的使用者和角色存放區。 圖11描述分割成三個應用程式的使用者和角色存放區： HRSite、CustomerSite 和 SalesSite。 這三個 web 應用程式都有自己的唯一使用者和角色，但它們都將其使用者帳戶和角色資訊實際儲存在相同的資料庫資料表中。

[![使用者帳戶可能會分割成多個應用程式](creating-the-membership-schema-in-sql-server-cs/_static/image32.png)](creating-the-membership-schema-in-sql-server-cs/_static/image31.png)

**圖 11**：使用者帳戶可能會分割成多個應用程式 ([按一下以查看完整大小的影像](creating-the-membership-schema-in-sql-server-cs/_static/image33.png)) 

`aspnet_Applications`資料表是定義這些資料分割的定義。 使用資料庫儲存使用者帳戶資訊的每個應用程式都是以這個資料表中的資料列來表示。 `aspnet_Applications`資料表有四個數據行： `ApplicationId` 、 `ApplicationName` 、 `LoweredApplicationName` 和 `Description` 。 `ApplicationId` 的類型是 [`uniqueidentifier`](https://msdn.microsoft.com/library/ms187942.aspx) ，而且是資料表的主鍵; 為 `ApplicationName` 每個應用程式提供獨特的易記名稱。

其他成員資格和角色相關資料表會連結回 `ApplicationId` 中的欄位 `aspnet_Applications` 。 例如， `aspnet_Users` 資料表（其中包含每個使用者帳戶的記錄）有 `ApplicationId` 外鍵欄位; 資料表的 ditto `aspnet_Roles` 。 `ApplicationId`這些資料表中的欄位會指定使用者帳戶或角色所屬的應用程式磁碟分割。

### <a name="storing-user-account-information"></a>儲存使用者帳戶資訊

使用者帳戶資訊會保存在兩個數據表中： `aspnet_Users` 和 `aspnet_Membership` 。 `aspnet_Users`資料表包含保存必要使用者帳戶資訊的欄位。 最相關的三個數據行是：

- `UserId`
- `UserName`
- `ApplicationId`

`UserId` 這是主鍵 (和類型 `uniqueidentifier`) 。 `UserName` 的型別 `nvarchar(256)` 和密碼都組成使用者的認證。  (使用者的密碼會儲存在資料表中 `aspnet_Membership` 。 ) 將 `ApplicationId` 使用者帳戶連結至中的特定應用程式 `aspnet_Applications` 。 和資料行上有一個複合[ `UNIQUE` 條件約束](https://msdn.microsoft.com/library/ms191166.aspx) `UserName` `ApplicationId` 。 這可確保在指定的應用程式中，每個使用者名稱都是唯一的，但它允許在 `UserName` 不同的應用程式中使用相同的使用者名稱。

此 `aspnet_Membership` 表格包含其他使用者帳戶資訊，例如使用者的密碼、電子郵件地址、上次登入日期和時間等等。 和資料表中的記錄之間有一對一的對應關係 `aspnet_Users` `aspnet_Membership` 。 此關聯性是由中的欄位來確保 `UserId` ，此欄位 `aspnet_Membership` 可做為資料表的主鍵。 `aspnet_Users`和資料表一樣， `aspnet_Membership` 包含將 `ApplicationId` 此資訊系結至特定應用程式分割區的欄位。

### <a name="securing-passwords"></a>保護密碼

密碼資訊會儲存在 `aspnet_Membership` 資料表中。 `SqlMembershipProvider`可以使用下列三種技術的其中一種，將密碼儲存在資料庫中：

- **Clear** -密碼會以純文字的形式儲存在資料庫中。 我強烈建議您不要使用這個選項。 如果資料庫遭到入侵，則是由尋找後門的駭客或具有資料庫存取權的不滿意員工所提供-每一位使用者的認證都可供採用。
- **哈** 希-密碼會使用單向雜湊演算法和隨機產生的 salt 值進行雜湊處理。 此雜湊值 (以及 salt) 會儲存在資料庫中。
- 已**加密**-加密版本的密碼會儲存在資料庫中。

使用的密碼儲存技術取決於 `SqlMembershipProvider` 中指定的設定 `Web.config` 。 我們將探討如何自訂 `SqlMembershipProvider` 步驟4中的設定。 預設行為是儲存密碼的雜湊。

負責儲存密碼的資料行為 `Password` 、 `PasswordFormat` 和 `PasswordSalt` 。 `PasswordFormat` 這是類型的欄位， `int` 其值表示用於儲存密碼的技術：0表示清除，1表示雜湊，2表示加密。 `PasswordSalt` 無論使用的密碼儲存技術為何，都會指派隨機產生的字串。 `PasswordSalt` 只有在計算密碼的雜湊時，才會使用的值。 最後， `Password` 資料行包含實際的密碼資料，也就是純文字密碼、密碼的雜湊或加密密碼。

[表 1] 說明在儲存密碼 MySecret 時，這三個數據行的各種儲存技巧可能會有什麼樣子！ .

| **儲存技術 &lt; \_ o3a \_ p/&gt;** | **密碼 &lt; \_ o3a \_ p/&gt;** | **PasswordFormat &lt; \_ o3a \_ p/&gt;** | **PasswordSalt &lt; \_ o3a \_ p/&gt;** |
| --- | --- | --- | --- |
| Clear | MySecret! | 0 | tTnkPlesqissc2y2SMEygA = = |
| 散 列 | 2oXm6sZHWbTHFgjgkGQsc2Ec9ZM = | 1 | wFgjUfhdUFOCKQiI61vtiQ = = |
| 已加密 | 62RZgDvhxykkqsMchZ0Yly7HS6onhpaoCYaRxV8g0F4CW56OXUU3e7Inza9j9BKp | 2 | LSRzhGS/aa/oqAXGLHJNBw = = |

**表 1**：儲存密碼 MySecret 時，密碼相關欄位的範例值！

> [!NOTE]
> 使用的特定加密或雜湊演算法 `SqlMembershipProvider` 取決於元素中的設定 `<machineKey>` 。 我們已在 <a id="Tutorial3"></a> [*表單驗證設定和高級主題*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)教學課程的步驟3中討論過這個設定元素。

### <a name="storing-roles-and-role-associations"></a>儲存角色和角色關聯

角色架構可讓開發人員定義一組角色，並指定哪些使用者屬於哪些角色。 這項資訊會透過兩個數據表，在資料庫中加以捕獲： `aspnet_Roles` 和 `aspnet_UsersInRoles` 。 資料表中的每一筆記錄都 `aspnet_Roles` 代表特定應用程式的角色。 資料表很類似于 `aspnet_Users` 資料表， `aspnet_Roles` 有三個與我們討論相關的資料行：

- `RoleId`
- `RoleName`
- `ApplicationId`

`RoleId` 這是主鍵 (和類型 `uniqueidentifier`) 。 `RoleName` 是 `nvarchar(256)` 類型。 並將 `ApplicationId` 使用者帳戶連結至中的特定應用程式 `aspnet_Applications` 。 和資料行上有一個複合 `UNIQUE` 條件約束 `RoleName` ，可 `ApplicationId` 確保在指定的應用程式中，每個角色名稱都是唯一的。

`aspnet_UsersInRoles`資料表可做為使用者和角色之間的對應。 只有兩個數據行 `UserId` ，而且 `RoleId` 它們組成複合主鍵。

## <a name="step-4-specifying-the-provider-and-customizing-its-settings"></a>步驟4：指定提供者和自訂其設定

所有支援提供者模型的架構（例如成員資格和角色架構）本身缺乏實作為本身，而是將該責任委派給提供者類別。 在成員資格架構的情況下， `Membership` 類別會定義用來管理使用者帳戶的 API，但不會直接與任何使用者存放區互動。 相反地， `Membership` 類別的方法會將要求交給設定的提供者，我們將使用 `SqlMembershipProvider` 。 當我們叫用類別中的其中一個方法時 `Membership` ，成員資格架構如何知道將呼叫委派給 `SqlMembershipProvider` ？

`Membership`類別具有[ `Providers` 屬性](https://msdn.microsoft.com/library/system.web.security.membership.providers.aspx)，其中包含可供成員資格架構使用的所有已註冊提供者類別的參考。 每個已註冊的提供者都有相關聯的名稱和類型。 此名稱提供了方便使用的方式來參考集合中的特定提供者 `Providers` ，而類型則會識別提供者類別。 此外，每個已註冊的提供者都可能包含設定。 成員資格架構的設定設定包括 `passwordFormat` 與 `requiresUniqueEmail` 其他許多專案。 如需所使用之設定設定的完整清單，請參閱 [表 2] `SqlMembershipProvider` 。

`Providers`屬性的內容是透過 web 應用程式的設定來指定。 根據預設，所有的 web 應用程式都有一個名為的提供者 `AspNetSqlMembershipProvider` 類型 `SqlMembershipProvider` 。 此預設成員資格提供者是在 (登錄于 `machine.config` `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG)` 下列位置：

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample1.xml)]

如上面的[ `<membership>` 標記所示](https://msdn.microsoft.com/library/1b9hw62f.aspx)，專案會定義成員資格架構的設定，而[ `<providers>` 子項目](https://msdn.microsoft.com/library/6d4936ht.aspx)會指定已註冊的提供者。 您可以使用或元素來新增或移除提供者 [`<add>`](https://msdn.microsoft.com/library/whae3t94.aspx) [`<remove>`](https://msdn.microsoft.com/library/aykw9a6d.aspx) ; 使用 [`<clear>`](https://msdn.microsoft.com/library/t062y6yc.aspx) 元素可移除所有目前註冊的提供者。 如上面的標記所示，會 `machine.config` 加入名為的提供者，其 `AspNetSqlMembershipProvider` 類型為 `SqlMembershipProvider` 。

除了 `name` 和 `type` 屬性之外，元素還 `<add>` 包含定義各種設定設定值的屬性。 [表 2] 列出可用的 `SqlMembershipProvider` 特定設定，以及每個設定的描述。

> [!NOTE]
> 表2中記下的任何預設值都會參考類別中定義的預設值 `SqlMembershipProvider` 。 請注意，並非所有的設定都 `AspNetSqlMembershipProvider` 對應至類別的預設值 `SqlMembershipProvider` 。 例如，如果未在成員資格提供者中指定，此 `requiresUniqueEmail` 設定會預設為 true。 但是，會 `AspNetSqlMembershipProvider` 明確指定的值來覆寫這個預設值 `false` 。

| **設定 &lt; \_ o3a \_ p/&gt;** | **描述 &lt; \_ o3a \_ p/&gt;** |
| --- | --- |
| `ApplicationName` | 回想一下，成員架構可讓單一使用者存放區跨多個應用程式進行分割。 這項設定表示成員資格提供者所使用的應用程式資料分割名稱。 如果未明確指定此值，則會在執行時間將其設定為應用程式的虛擬根路徑的值。 |
| `commandTimeout` | 以秒為單位指定 SQL 命令逾時值 () 。 預設值是 30。 |
| `connectionStringName` | 專案中 `<connectionStrings>` 用來連接到使用者存放區資料庫的連接字串名稱。 這是必要的值。 |
| `description` | 提供已註冊之提供者的易記描述。 |
| `enablePasswordRetrieval` | 指定使用者是否可以取出忘記的密碼。 預設值是 `false`。 |
| `enablePasswordReset` | 指出是否允許使用者重設其密碼。 預設為 `true`。 |
| `maxInvalidPasswordAttempts` | 在使用者被鎖定之前，指定使用者在指定期間內可能發生的失敗登入嘗試次數上限 `passwordAttemptWindow` 。預設值為5。 |
| `minRequiredNonalphanumericCharacters` | 必須出現在使用者密碼中的非英數位元數目下限。 此值必須介於0到128之間;預設值為1。 |
| `minRequiredPasswordLength` | 密碼中所需的字元數下限。 此值必須介於0到128之間;預設值為7。 |
| `name` | 已註冊之提供者的名稱。 這是必要的值。 |
| `passwordAttemptWindow` | 追蹤失敗的登入嘗試的分鐘數。 如果使用者 `maxInvalidPasswordAttempts` 在此指定的時間範圍內提供不正確登入認證，則會被鎖定。預設值為10。 |
| `PasswordFormat` | 密碼儲存格式： `Clear` 、 `Hashed` 或 `Encrypted` 。 預設為 `Hashed`。 |
| `passwordStrengthRegularExpression` | 如果有提供此正則運算式，會在建立新帳戶或變更其密碼時，用來評估使用者所選取密碼的強度。 預設值為空字串。 |
| `requiresQuestionAndAnswer` | 指定使用者是否必須在抓取或重設其密碼時回答他的安全性問題。 預設值是 `true`。 |
| `requiresUniqueEmail` | 指出指定之應用程式分割區中的所有使用者帳戶是否都必須有唯一的電子郵件地址。 預設值是 `true`。 |
| `type` | 指定提供者的類型。 這是必要的值。 |

**表 2**：成員資格和 `SqlMembershipProvider` 設定

除了 `AspNetSqlMembershipProvider` 之外，其他成員資格提供者也可以在應用程式上註冊，方法是將類似的標記新增至檔案 `Web.config` 。

> [!NOTE]
> 角色架構的運作方式大致相同：在中有預設的已登錄角色提供者 `machine.config` ，而且可在中依應用程式來自訂已註冊的提供者 `Web.config` 。 我們將在未來的教學課程中詳細檢查角色架構及其設定標記。

### <a name="customizing-thesqlmembershipprovidersettings"></a>自訂 `SqlMembershipProvider` 設定

預設的 `SqlMembershipProvider` (`AspNetSqlMembershipProvider`) 將其 `connectionStringName` 屬性設定為 `LocalSqlServer` 。 與 `AspNetSqlMembershipProvider` 提供者一樣，連接字串名稱 `LocalSqlServer` 是在中定義 `machine.config` 。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample2.xml)]

如您所見，此連接字串會定義 SQL 2005 Express Edition 資料庫，位於 |DataDirectory | aspnetdb.mdf .mdf '。 字串 |DataDirectory |會在執行時間轉譯以指向 `~/App_Data/` 目錄，因此資料庫路徑 |DataDirectory | aspnetdb.mdf .mdf 會轉譯為 `~/App_Data` / `aspnet.mdf` 。

如果我們未在應用程式的檔案中指定任何成員資格提供者資訊 `Web.config` ，應用程式會使用預設註冊的成員資格提供者 `AspNetSqlMembershipProvider` 。 如果 `~/App_Data/aspnet.mdf` 資料庫不存在，ASP.NET 執行時間會自動建立該資料庫，並新增應用程式服務架構。 不過，我們不想要使用 `aspnet.mdf` 資料庫，而是想要使用 `SecurityTutorials.mdf` 我們在步驟2中建立的資料庫。 您可以透過下列兩種方式之一來完成這項修改：

- <strong>指定值給</strong> <strong>`LocalSqlServer`</strong><strong>中的</strong> <strong>`Web.config`</strong> 連接字串名稱<strong>.</strong> 藉由覆寫 `LocalSqlServer` 中的連接字串名稱值 `Web.config` ，我們可以使用預設註冊的成員資格提供者 (`AspNetSqlMembershipProvider`) ，並讓它正確地使用 `SecurityTutorials.mdf` 資料庫。 如果您是具有所指定之設定設定的內容，這種方法就很好用 `AspNetSqlMembershipProvider` 。 如需這項技術的詳細資訊，請參閱 [Scott Guthrie](https://weblogs.asp.net/scottgu/)的 blog 文章、設定 [ASP.NET 2.0 應用程式服務以使用 SQL Server 2000 或 SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)。
- <strong>新增類型</strong> <strong>`SqlMembershipProvider`</strong> 的已註冊提供者<strong>並設定其</strong> <strong>`connectionStringName`</strong><strong>將設定為指向</strong> <strong>`SecurityTutorials.mdf`</strong><strong>資料庫。</strong> 如果您想要自訂資料庫連接字串以外的其他設定屬性，此方法很有用。 在我自己的專案中，我一直都是使用這個方法，因為它的彈性和可讀性。

在加入參考資料庫的新已註冊提供者之前 `SecurityTutorials.mdf` ，我們必須先在的區段中加入適當的連接字串值 `<connectionStrings>` `Web.config` 。 下列標記會新增名為的新連接字串 `SecurityTutorialsConnectionString` ，這個連接字串會參考 `SecurityTutorials.mdf` 資料夾中的 SQL Server 2005 Express Edition 資料庫 `App_Data` 。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample3.xml)]

> [!NOTE]
> 如果您使用替代資料庫檔案，請視需要更新連接字串。 如需有關形成正確連接字串的詳細資訊，請參閱 [ConnectionStrings.com](http://www.connectionstrings.com/)。

接下來，將下列成員資格設定標記新增至檔案 `Web.config` 。 此標記會註冊名為的新提供者 `SecurityTutorialsSqlMembershipProvider` 。

[!code-xml[Main](creating-the-membership-schema-in-sql-server-cs/samples/sample4.xml)]

除了註冊 `SecurityTutorialsSqlMembershipProvider` 提供者之外，上述標記還會透過 `SecurityTutorialsSqlMembershipProvider`) 專案中的屬性，將作為預設的提供者 (`defaultProvider` `<membership>` 。 回想一下，成員資格架構可以有多個已註冊的提供者。 因為 `AspNetSqlMembershipProvider` 是註冊為中的第一個提供者 `machine.config` ，所以它會作為預設提供者，除非我們另外指出。

目前，我們的應用程式有兩個已註冊的提供者： `AspNetSqlMembershipProvider` 和 `SecurityTutorialsSqlMembershipProvider` 。 不過，在註冊 `SecurityTutorialsSqlMembershipProvider` 提供者之前，我們可以先在專案之前加入一個[ `<clear />` 元素](https://msdn.microsoft.com/library/t062y6yc.aspx)，以清除所有先前註冊的提供者 `<add>` 。 這會 `AspNetSqlMembershipProvider` 從已註冊的提供者清單中清除，這表示會 `SecurityTutorialsSqlMembershipProvider` 是唯一註冊的成員資格提供者。 如果使用此方法，則不需要將設 `SecurityTutorialsSqlMembershipProvider` 為預設提供者，因為它會是唯一註冊的成員資格提供者。 如需使用的詳細資訊 `<clear />` ，請參閱 [ `<clear />` 加入提供者時使用](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)。

請注意， `SecurityTutorialsSqlMembershipProvider` 的 `connectionStringName` 設定會參考剛加入的 `SecurityTutorialsConnectionString` 連接字串名稱，而且其 `applicationName` 設定已設定為 SecurityTutorials 的值。 此外，此 `requiresUniqueEmail` 設定已設定為 `true` 。 所有其他設定選項與中的值相同 `AspNetSqlMembershipProvider` 。 如果您想要的話，可以隨意在這裡進行任何設定修改。 例如，您可以藉由要求兩個非英數位元（而不是一個），或將密碼長度增加為8個字元（而不是七個字元）來加強密碼強度。

> [!NOTE]
> 回想一下，成員架構可讓單一使用者存放區跨多個應用程式進行分割。 成員資格提供者的 `applicationName` 設定會指出提供者在使用使用者存放區時所使用的應用程式。 請務必明確設定設定設定的值 `applicationName` ，因為如果 `applicationName` 未明確設定，則會在執行時間將它指派給 web 應用程式的虛擬根路徑。 只要應用程式的虛擬根路徑不會變更，這就可以正常運作，但如果您將應用程式移到不同的路徑，此 `applicationName` 設定也會變更。 發生這種情況時，成員資格提供者將會開始使用與先前所用不同的應用程式分割區。 移動之前建立的使用者帳戶會位於不同的應用程式分割區，而且這些使用者將無法再登入網站。 如需這項功能的深入討論，請參閱 [設定 `applicationName` ASP.NET 2.0 成員資格和其他提供者時，一律設定屬性](https://weblogs.asp.net/scottgu/443634)。

## <a name="summary"></a>摘要

到目前為止，我們有一個具有已設定之應用程式服務 () 的資料庫 `SecurityTutorials.mdf` ，並已設定 web 應用程式，讓成員資格架構可以使用 `SecurityTutorialsSqlMembershipProvider` 我們剛剛註冊的提供者。 這個已註冊的提供者屬於型別 `SqlMembershipProvider` ，而且會 `connectionStringName` 將其設定為適當的連接字串 (`SecurityTutorialsConnectionString`) ，並 `applicationName` 明確設定其值。

我們現在已準備好使用應用程式的成員資格架構。 在下一個教學課程中，我們將探討如何建立新的使用者帳戶。 之後，我們將探索驗證使用者、執行以使用者為基礎的授權，以及在資料庫中儲存其他與使用者相關的資訊。

快樂程式設計！

### <a name="further-reading"></a>深入閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [設定 `applicationName` ASP.NET 2.0 成員資格和其他提供者時，一律設定屬性](https://weblogs.asp.net/scottgu/443634)
- [將 ASP.NET 2.0 應用程式服務設定為使用 SQL Server 2000 或 SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx)
- [下載 SQL Server Management Studio Express Edition](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)
- [檢查 ASP.NET 2.0 的成員資格、角色和設定檔](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [`<add>`成員資格提供者的元素](https://msdn.microsoft.com/library/whae3t94.aspx)
- [`<membership>`元素](https://msdn.microsoft.com/library/1b9hw62f.aspx)
- [`<providers>`成員資格的元素](https://msdn.microsoft.com/library/6d4936ht.aspx)
- [`<clear />`加入提供者時使用](https://weblogs.asp.net/scottgu/archive/2006/11/20/common-gotcha-don-t-forget-to-clear-when-adding-providers.aspx)
- [直接使用 `SqlMembershipProvider`](http://aspnet.4guysfromrolla.com/articles/091207-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>本教學課程所包含主題的影片訓練

- [了解 ASP.NET 成員資格](../../../videos/authentication/understanding-aspnet-memberships.md)
- [設定 SQL 使用成員資格結構描述](../../../videos/authentication/configuring-sql-to-work-with-membership-schemas.md)
- [變更預設成員資格結構描述中的成員資格設定](../../../videos/authentication/changing-membership-settings-in-the-default-membership-schema.md)

### <a name="about-the-author"></a>關於作者

Scott Mitchell 作者有多個 ASP/ASP. NET 書籍和創辦人 of 4GuysFromRolla.com，自1998起一直都在使用 Microsoft Web 技術。 Scott 以獨立顧問、訓練員和作者的形式運作。 他的最新書籍是 *[在24小時內 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 Scott 可于或透過他的 blog 來觸達 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) [http://ScottOnWriting.NET](http://scottonwriting.net/) 。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列是由許多有用的審核者所審核。 本教學課程的潛在客戶審核 Alicja Maziarz。 有興趣複習我即將推出的 MSDN 文章嗎？ 如果是的話，請在這裡放置一行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com) 。

> [!div class="step-by-step"]
> [下一個](creating-user-accounts-cs.md)
