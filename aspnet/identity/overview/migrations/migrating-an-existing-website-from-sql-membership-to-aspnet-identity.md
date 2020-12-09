---
uid: identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
title: 將現有網站從 SQL 成員資格遷移至 ASP.NET Identity-ASP.NET 4。x
author: Rick-Anderson
description: 本教學課程說明將現有 web 應用程式與使用 SQL 成員資格建立的使用者和角色資料移轉至新 ASP.NET Identity s 的步驟 .。。
ms.author: riande
ms.date: 12/19/2014
ms.custom: seoapril2019
ms.assetid: 220d3d75-16b2-4240-beae-a5b534f06419
msc.legacyurl: /identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 2cfab96422340acc67ebb3b11f322ae1b258575d
ms.sourcegitcommit: 6727454a30f11ac2365e1cc8a37ef0005f5d15b3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/09/2020
ms.locfileid: "96934119"
---
# <a name="migrating-an-existing-website-from-sql-membership-to-aspnet-identity"></a>將現有的網站從 SQL 成員資格移轉至 ASP.NET Identity

依 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Suhas Joshi](https://github.com/suhasj)

> 本教學課程說明將現有 web 應用程式與使用 SQL 成員資格建立的使用者和角色資料移轉至新的 ASP.NET Identity 系統的步驟。 此方法牽涉到將現有的資料庫架構變更為 ASP.NET Identity 所需的架構，並將舊的/新類別連接到該架構。 在您採用這種方法之後，一旦遷移資料庫之後，將可輕鬆地處理未來的身分識別更新。

在本教學課程中，我們將使用 Visual Studio 2010 建立的 web 應用程式範本 (Web Form) 來建立使用者和角色資料。 接著，我們將使用 SQL 腳本，將現有的資料庫移轉到身分識別系統所需的資料表。 接下來，我們將會安裝必要的 NuGet 套件，並新增使用身分識別系統進行成員資格管理的新帳戶管理頁面。 作為遷移的測試，使用 SQL 成員資格建立的使用者應該能夠登入，而新的使用者應該能夠註冊。 您可以在[這裡](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/)找到完整的範例。 另請參閱 [從 ASP.NET 成員資格遷移至 ASP.NET Identity](https://travis.io/blog/2015/03/24/migrate-from-aspnet-membership-to-aspnet-identity/)。

## <a name="getting-started"></a>開始使用

### <a name="creating-an-application-with-sql-membership"></a>建立具有 SQL 成員資格的應用程式

1. 我們需要從使用 SQL 成員資格的現有應用程式開始，並擁有使用者和角色資料。 基於本文的目的，讓我們在 Visual Studio 2010 中建立 web 應用程式。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.jpg)
2. 使用 ASP.NET Configuration tool 建立2個使用者： **oldAdminUser** 和 **oldUser。**

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.jpg)
3. 建立名為 Admin 的角色，並將 ' oldAdminUser ' 新增為該角色中的使用者。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.png)
4. 使用 default.aspx 建立網站的管理員區段。 將 web.config 檔案中的授權標籤設定為只允許系統管理員角色中的使用者存取。 您可以在這裡找到詳細資訊 [https://www.asp.net/web-forms/tutorials/security/roles/role-based-authorization-cs](../../../web-forms/overview/older-versions-security/roles/role-based-authorization-cs.md)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.png)
5. 在伺服器總管中查看資料庫，以瞭解 SQL 成員資格系統所建立的資料表。 使用者登入資料儲存在 aspnet \_ Users 和 aspnet \_ 成員資格資料表中，而角色資料則儲存在 aspnet \_ Roles 資料表中。 哪些使用者是哪些角色儲存在 aspnet UsersInRoles 資料表中的相關資訊 \_ 。 針對基本的成員資格管理，將上述表格中的資訊移植到 ASP.NET Identity 系統就已足夠。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.png)

### <a name="migrating-to-visual-studio-2013"></a>遷移至 Visual Studio 2013

1. 安裝適用于 Web 或 Visual Studio 2013 的 Visual Studio Express 2013，以及 [最新的更新](https://www.microsoft.com/download/details.aspx?id=44921)。
2. 在安裝的 Visual Studio 版本中開啟上述專案。 如果電腦上未安裝 SQL Server Express，當您開啟專案時，就會出現提示，因為連接字串會使用 SQL Express。 您可以選擇安裝 SQL Express 或作為解決方法，將連接字串變更為 LocalDb。 在本文中，我們會將它變更為 LocalDb。
3. 開啟 web.config 並從變更連接字串。SQLExpress 來 (LocalDb) v 11.0。 從連接字串中移除 ' User Instance = true '。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.jpg)
4. 開啟伺服器總管，並確認可以觀察資料表架構和資料。
5. ASP.NET Identity 系統適用于版本4.5 或更高版本的架構。 將應用程式的目標重定為4.5 或更高版本。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image5.png)

    建立專案以確認沒有任何錯誤。

### <a name="installing-the-nuget-packages"></a>安裝 Nuget 套件

1. 在方案總管中，以滑鼠右鍵按一下 [ &gt; **管理 NuGet 套件**] 專案。 在搜尋方塊中，輸入「Asp.net Identity」。 在結果清單中選取封裝，然後按一下 [安裝]。 按一下 [我接受] 按鈕，接受授權合約。 請注意，此套件將會安裝相依性套件： EntityFramework 和 Microsoft ASP.NET 身分識別核心。 同樣地，如果您不想要啟用 OAuth 登入) ，請安裝下列套件 (略過最後4個 OWIN 套件：

   - Microsoft.AspNet.Identity.Owin
   - Microsoft.Owin.Host.SystemWeb
   - Owin。
   - Owin，Google
   - Owin. MicrosoftAccount
   - Owin. 安全性 Twitter

     ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image6.png)

### <a name="migrate-database-to-the-new-identity-system"></a>將資料庫移轉至新的身分識別系統

下一步是要將現有的資料庫移轉至 ASP.NET Identity 系統所需的架構。 為了達成此目的，我們會執行 SQL 腳本，其中包含一組命令來建立新的資料表，並將現有的使用者資訊遷移至新的資料表。 您可以在 [這裡](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/Migrations.sql)找到腳本檔。

此腳本檔是此範例特有的。 如果已自訂或修改使用 SQL 成員資格建立之資料表的架構，則必須據以變更腳本。

### <a name="how-to-generate-the-sql-script-for-schema-migration"></a>如何產生用於架構遷移的 SQL 腳本

若要讓 ASP.NET Identity 類別與現有使用者的資料一起運作，我們需要將資料庫架構遷移到 ASP.NET Identity 所需的架構。 我們可以藉由加入新的資料表，並將現有的資訊複製到這些資料表來完成這項作業。 根據預設，ASP.NET Identity 會使用 EntityFramework 將身分識別模型類別對應回資料庫，以儲存/取出資訊。 這些模型類別會執行定義使用者和角色物件的核心身分識別介面。 資料庫中的資料表和資料行是以這些模型類別為基礎。 Identity v 2.1.0 中的 EntityFramework 模型類別及其屬性如下所定義

| **IdentityUser** | **類型** | **IdentityRole** | **IdentityUserRole** | **IdentityUserLogin** | **IdentityUserClaim** |
| --- | --- | --- | --- | --- | --- |
| 識別碼 | 字串 | 識別碼 | RoleId | ProviderKey | 識別碼 |
| 使用者名稱 | 字串 | 名稱 | UserId | UserId | ClaimType |
| PasswordHash | 字串 |  |  | LoginProvider | ClaimValue |
| SecurityStamp | 字串 |  |  |  | 使用者 \_ 識別碼 |
| 電子郵件 | 字串 |  |  |  |  |
| EmailConfirmed | bool |  |  |  |  |
| PhoneNumber | 字串 |  |  |  |  |
| PhoneNumberConfirmed | bool |  |  |  |  |
| LockoutEnabled | bool |  |  |  |  |
| LockoutEndDate | Datetime |  |  |  |  |
| AccessFailedCount | int |  |  |  |  |

每個模型都必須有對應至屬性之資料行的資料表。 類別和資料表之間的對應是在的方法中定義 `OnModelCreating` `IdentityDBContext` 。 這就是所謂的流暢 API 方法，您可以在 [這裡](https://msdn.microsoft.com/data/jj591617.aspx)找到更多詳細資訊。 類別的設定如下所述

| **類別** | **資料表** | **主要金鑰** | **外鍵** |
| --- | --- | --- | --- |
| IdentityUser | AspnetUsers | 識別碼 |  |
| IdentityRole | AspnetRoles | 識別碼 |  |
| IdentityUserRole | AspnetUserRole | UserId + RoleId | 使用者 \_ 識別碼- &gt; AspnetUsers RoleId- &gt; AspnetRoles |
| IdentityUserLogin | AspnetUserLogins | ProviderKey + UserId + LoginProvider | UserId- &gt; AspnetUsers |
| IdentityUserClaim | AspnetUserClaims | 識別碼 | 使用者 \_ 識別碼- &gt; AspnetUsers |

有了此資訊，我們就可以建立 SQL 語句來建立新的資料表。 我們可以個別撰寫每個語句，也可以使用 EntityFramework PowerShell 命令來產生整個腳本，然後再視需要進行編輯。 若要這樣做，請在 VS 中，從 [ **View** ] 或 [ **Tools** ] 功能表開啟 **封裝管理員主控台**

- 執行「啟用-遷移」命令以啟用 EntityFramework 遷移。
- 執行「新增-遷移初始」命令，其會建立初始安裝程式碼以在 c # 中建立資料庫/VB。
- 最後一個步驟是執行 "Update-Database – Script" 命令，此命令會根據模型類別產生 SQL 腳本。

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

您可以使用這個資料庫產生腳本做為起點，我們將會進行額外的變更，以加入新的資料行及複製資料。 這項功能的優點是，我們會產生 `_MigrationHistory` 資料表，讓 EntityFramework 在未來版本的身分識別版本變更時，修改資料庫架構。

除了身分識別使用者模型類別中的其他屬性以外，SQL 成員資格使用者資訊還有其他屬性，也就是電子郵件、密碼嘗試、上次登入日期、上次鎖定的日期等。這是很有用的資訊，我們想要將它傳送到身分識別系統。 將其他屬性加入至使用者模型，然後將它們對應回資料庫中的資料表資料行，即可完成這項工作。 我們可以加入子類別化模型的類別來完成這項作業 `IdentityUser` 。 我們可以將屬性新增至這個自訂類別，並編輯 SQL 腳本，以便在建立資料表時加入對應的資料行。 此類別的程式碼會在文章中進一步說明。 `AspnetUsers`加入新屬性之後，用來建立資料表的 SQL 腳本是

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample1.sql)]

接下來，我們需要將 SQL 成員資格資料庫中現有的資訊複製到新加入的資料表以進行識別。 這可以透過 SQL 直接將資料從一個資料表複製到另一個資料表來完成。 為了將資料加入資料表的資料列中，我們會使用 `INSERT INTO [Table]` 結構。 若要從另一個資料表複製，我們可以 `INSERT INTO` 搭配語句使用語句 `SELECT` 。 若要取得所有使用者資訊，我們需要查詢 *aspnet \_ 使用者* 和 *aspnet \_ 成員資格* 資料表，然後將資料複製到 *AspNetUsers* 資料表。 我們使用 `INSERT INTO` 和 `SELECT` 搭配 `JOIN` 和 `LEFT OUTER JOIN` 語句。 如需有關在資料表之間查詢和複製資料的詳細資訊，請參閱 [此](https://technet.microsoft.com/library/ms190750%28v=sql.105%29.aspx) 連結。 此外，AspnetUserLogins 和 AspnetUserClaims 資料表的開頭都是空的，因為 SQL 成員資格中預設不會對應到此資訊。 唯一複製的資訊是針對使用者和角色。 針對在先前步驟中建立的專案，將資訊複製到 users 資料表的 SQL 查詢會是

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample2.sql)]

在上述 SQL 語句中，會將來自 *aspnet \_ Users* 和 *aspnet \_ 成員資格* 資料表之每個使用者的相關資訊複製到 *AspnetUsers* 資料表的資料行中。 此處唯一進行的修改是複製密碼。 因為 SQL 成員資格中的密碼加密演算法使用 ' PasswordSalt ' 和 ' PasswordFormat '，所以我們也會連同雜湊密碼一起複製，以便用來依身分識別來解密密碼。 這在連結自訂密碼 hasher 時，會在文章中進一步說明。

此腳本檔是此範例特有的。 對於具有其他資料表的應用程式，開發人員可以遵循類似的方法，在使用者模型類別上加入其他屬性，並將其對應至 AspnetUsers 資料表中的資料行。 若要執行腳本，

1. 開啟 [伺服器總管]。 展開 [>iapplicationbuilder.applicationservices] 連接以顯示資料表。 以滑鼠右鍵按一下 [資料表] 節點，然後選取 [新增查詢] 選項

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image7.png)
2. 在查詢視窗中，複製並貼上從遷移 .sql 檔案中的整個 SQL 腳本。 藉由按下 [執行] 箭號按鈕來執行腳本檔案。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.jpg)

    重新整理伺服器總管視窗。 系統會在資料庫中建立五個新的資料表。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image8.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image9.png)

    以下是 SQL 成員資格資料表中資訊對應至新身分識別系統的方式。

    aspnet \_ 角色-- &gt; AspNetRoles

    asp \_ netUsers 和 asp \_ netMembership-- &gt; AspNetUsers

    aspnet \_ UserInRoles-- &gt; AspNetUserRoles

    如上一節所述，AspNetUserClaims 和 AspNetUserLogins 資料表是空的。 AspNetUser 資料表中的 ' 鑒別子欄位應與定義為下一個步驟的模型類別名稱相符。 此外，PasswordHash 資料行的格式為「加密密碼 | 密碼 salt | 密碼格式」。 這可讓您使用特殊的 SQL 成員資格加密邏輯，讓您可以重複使用舊密碼。 本文稍後將會說明。

### <a name="creating-models-and-membership-pages"></a>建立模型和成員資格頁面

如先前所述，根據預設，識別功能會使用 Entity Framework 來與資料庫通訊，以儲存帳戶資訊。 若要使用資料表中的現有資料，我們需要建立對應回資料表的模型類別，然後在身分識別系統中連結它們。 作為身分識別合約的一部分，模型類別應該執行在 Identity. 核心 dll 中定義的介面，或者可以擴充 EntityFramework 中可用的這些介面的現有實作為。

在我們的範例中，AspNetRoles、AspNetUserClaims、AspNetLogins 和 AspNetUserRole 資料表的資料行，類似于現有的身分識別系統執行。 因此，我們可以重複使用現有的類別來對應至這些資料表。 AspNetUser 資料表有一些額外的資料行，可用來儲存 SQL 成員資格資料表中的其他資訊。 這可以藉由建立模型類別來對應，以擴充現有的 ' IdentityUser ' 實作為，並新增其他屬性。

1. 在專案中建立 [模型] 資料夾，並加入類別使用者。 類別的名稱應該符合 ' AspnetUsers ' 資料表的 ' 鑒別子資料行中新增的資料。

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image10.png)

    User 類別應擴充在 *EntityFramework* dll 中找到的 IdentityUser 類別。 宣告對應回 AspNetUser 資料行之類別中的屬性。 屬性 ID、Username、PasswordHash 和 SecurityStamp 是在 IdentityUser 中定義，因此會省略。 以下是具有所有屬性之使用者類別的程式碼

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample3.cs)]
2. 需要 Entity Framework DbCoNtext 類別，才能將模型中的資料保存回資料表，並從資料表中取出資料以填入模型。 *EntityFramework* Dll 定義 IdentityDbCoNtext 類別，它會與識別資料表互動以取得和儲存資訊。 IdentityDbCoNtext &lt; tuser 採用的是 &gt; 可延伸 IdentityUser 類別的任何類別的 ' tuser ' 類別。

    建立新的類別 [ApplicationdbcoNtext，以擴充在 [模型] 資料夾下的 IdentityDbCoNtext，以在步驟1中建立的「使用者」類別傳遞

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample4.cs)]
3. 新身分識別系統中的使用者管理，是使用 &lt; &gt; *EntityFramework* Dll 中定義的 UserManager tuser 類別來完成。 我們需要建立擴充 UserManager 的自訂類別，並傳入在步驟1中建立的「使用者」類別。

    在 [模型] 資料夾中，建立擴充 UserManager 使用者的新類別 UserManager &lt;&gt;

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample5.cs)]
4. 應用程式使用者的密碼會經過加密，並儲存在資料庫中。 SQL 成員資格中使用的密碼編譯演算法與新的身分識別系統中的加密演算法不同。 若要重複使用舊密碼，我們需要在舊使用者使用 SQL 成員資格演算法登入時，選擇性地解密密碼，同時在新使用者的身分識別中使用加密演算法。

    UserManager 類別具有屬性 ' 並且 '，其會儲存實作為 ' IPasswordHasher ' 介面之類別的實例。 這是用來在使用者驗證交易期間加密/解密密碼。 在步驟3中定義的 UserManager 類別中，建立新的類別 SQLPasswordHasher，然後複製下列程式碼。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample6.cs)]

    匯入 system.string 和 system.string 命名空間，以解決編譯錯誤。

    EncodePassword 方法會根據預設的 SQL 成員資格加密執行來加密密碼。 這是取自 System.object dll。 如果舊的應用程式使用自訂的執行，則應該反映在此。 我們需要定義兩個其他方法 *HashPassword* 和 *VerifyHashedPassword* ，以使用 *EncodePassword* 方法來雜湊指定的密碼，或使用資料庫中現有的密碼來驗證純文字密碼。

    SQL 成員資格系統使用 PasswordHash、PasswordSalt 和 PasswordFormat 來雜湊使用者在註冊或變更其密碼時所輸入的密碼。 在遷移期間，會將三個欄位儲存在 AspNetUser 資料表的 PasswordHash 資料行中，並以 ' | ' 字元分隔。 當使用者登入，且密碼具有這些欄位時，我們會使用 SQL 成員資格加密來檢查密碼;否則，我們會使用身分識別系統的預設加密來驗證密碼。 如此一來，舊的使用者就不需要在應用程式遷移之後變更其密碼。
5. 宣告 UserManager 類別的函式，並將其以 SQLPasswordHasher 形式傳遞至函式中的屬性。

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample7.cs)]

### <a name="create-new-account-management-pages"></a>建立新的帳戶管理頁面

遷移的下一個步驟是新增帳戶管理頁面，讓使用者註冊並登入。 SQL 成員資格的舊帳戶頁面會使用無法與新的身分識別系統搭配使用的控制項。 若要加入新的使用者管理頁面，請遵循此連結的教學課程， [https://www.asp.net/identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project](../getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md) 從「新增 Web Form 以便將使用者註冊至您的應用程式」步驟開始，因為我們已建立專案並新增 NuGet 套件。

我們需要對範例進行一些變更，才能使用我們在此提供的專案。

- Register.aspx.cs 和 Login.aspx.cs 程式碼後方類別會使用 `UserManager` 來自身分識別套件的來建立使用者。 在此範例中，請遵循稍早所述的步驟，使用 [模型] 資料夾中加入的 UserManager。
- 使用已建立的使用者類別，而不是 Register.aspx.cs 和 Login.aspx.cs 程式碼後置於類別中的 IdentityUser。 這會在我們的自訂使用者類別中攔截到身分識別系統。
- 您可以略過建立資料庫的部分。
- 開發人員必須為新的使用者設定 ApplicationId，以符合目前的應用程式識別碼。 這可以藉由在 Register.aspx.cs 類別中建立使用者物件之前先查詢此應用程式的 ApplicationId 來完成，並在建立使用者之前進行設定。

    範例：

    在 [Register.aspx.cs] 頁面中定義方法來查詢 aspnet \_ 應用程式資料表，並根據應用程式名稱取得應用程式識別碼

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample8.cs)]

    現在在使用者物件上設定此設定

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample9.cs)]

使用舊的使用者名稱和密碼來登入現有的使用者。 使用 [註冊] 頁面來建立新的使用者。 也請確認使用者是否符合預期的角色。

移植到身分識別系統可協助使用者將 Open Authentication (OAuth) 新增至應用程式。 請參閱 [這裡](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/) 已啟用 OAuth 的範例。

## <a name="next-steps"></a>後續步驟

在本教學課程中，我們示範了如何將 SQL 成員資格的使用者移植到 ASP.NET Identity，但我們並未移植設定檔資料。 在下一個教學課程中，我們將探討如何將 SQL 成員資格的設定檔資料移植至新的身分識別系統。

您可以在本文底部留下意見反應。

*感謝 Tom Dykstra 和 Rick Anderson，以複習文章。*
