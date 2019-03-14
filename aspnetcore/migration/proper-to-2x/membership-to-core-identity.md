---
title: 從 ASP.NET 成員資格驗證移轉至 ASP.NET Core 2.0 身分識別
author: isaac2004
description: 了解如何移轉現有的 ASP.NET 應用程式使用 ASP.NET Core 2.0 身分識別的成員資格驗證。
ms.author: scaddie
ms.custom: mvc
ms.date: 01/10/2019
uid: migration/proper-to-2x/membership-to-core-identity
ms.openlocfilehash: 0b7001a311eeaaa78e3d52e2ec66d33ad057c381
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054495"
---
# <a name="migrate-from-aspnet-membership-authentication-to-aspnet-core-20-identity"></a>從 ASP.NET 成員資格驗證移轉至 ASP.NET Core 2.0 身分識別

作者：[Isaac Levin](https://isaaclevin.com)

本文示範如何使用 ASP.NET Core 2.0 身分識別的成員資格驗證的 ASP.NET 應用程式的資料庫結構描述移轉。

> [!NOTE]
> 本文件提供將 ASP.NET 成員資格為基礎的應用程式的資料庫結構描述移轉至使用 ASP.NET Core 身分識別的資料庫結構描述所需的步驟。 如需有關如何從 ASP.NET 成員資格為基礎的驗證移轉至 ASP.NET Identity 的詳細資訊，請參閱[將現有的應用程式從 SQL 成員資格移轉至 ASP.NET Identity](/aspnet/identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity)。 如需 ASP.NET Core 身分識別的詳細資訊，請參閱[ASP.NET core 身分識別簡介](xref:security/authentication/identity)。

## <a name="review-of-membership-schema"></a>檢閱的成員資格結構描述

在 ASP.NET 2.0 之前開發人員所負責建立整個的驗證和授權程序，為其應用程式。 使用 ASP.NET 2.0 成員資格引進，提供處理 ASP.NET 應用程式中的安全性與重複使用的解決方案。 開發人員現在便可以啟動結構描述載入到 SQL Server database [aspnet_regsql.exe](https://msdn.microsoft.com/library/ms229862.aspx)命令。 執行此命令之後，在資料庫中建立下列資料表。

  ![成員資格資料表](identity/_static/membership-tables.png)

若要將現有的應用程式移轉至 ASP.NET Core 2.0 身分識別，這些資料表中的資料必須移轉到新的身分識別結構描述所使用的資料表。

## <a name="aspnet-core-identity-20-schema"></a>ASP.NET Core 身分識別 2.0 結構描述

ASP.NET Core 2.0 會遵循[識別](/aspnet/identity/index)ASP.NET 4.5 中導入的原則。 雖然共用原則，架構之間的實作是不同版本的 ASP.NET Core 之間 (請參閱[移轉至 ASP.NET Core 2.0 的驗證和身分識別](xref:migration/1x-to-2x/index))。

若要檢視的 ASP.NET Core 2.0 身分識別的結構描述的最快方式是建立新的 ASP.NET Core 2.0 應用程式。 請遵循 Visual Studio 2017 中的下列步驟：

1. 選取 [檔案]  >  [新增]  >  [專案]。
1. 建立新**ASP.NET Core Web 應用程式**專案，命名為*CoreIdentitySample*。
1. 選取  **ASP.NET Core 2.0**下拉式清單中，然後選取**Web 應用程式**。 此範本會產生[Razor 頁面](xref:razor-pages/index)應用程式。 再按一下 **[確定]**，按一下**變更驗證**。
1. 選擇**個別使用者帳戶**身分識別的範本。 最後，按一下 **[確定]**，然後**確定**。 Visual Studio 建立專案，使用 ASP.NET Core 身分識別範本。
1. 選取 **工具** > **NuGet 套件管理員** > **Package Manager Console**開啟**Package Manager Console**(PMC) 視窗。
1. 巡覽至專案根目錄中 PMC 中，並執行[Entity Framework (EF) Core](/ef/core) `Update-Database`命令。

    ASP.NET Core 2.0 身分識別會同時使用 EF Core，在與儲存的驗證資料的資料庫互動。 為了讓新建立的應用程式運作，那里必須要儲存這項資料的資料庫。 建立新的應用程式之後, 檢查的資料庫環境中的結構描述的最快方式是建立資料庫使用[EF Core 移轉](/ef/core/managing-schemas/migrations/)。 此程序會建立資料庫、 在本機或其他位置，可以模擬該結構描述。 檢閱先前的文件，如需詳細資訊。

    EF Core 命令會使用連接字串中指定的資料庫*appsettings.json*。 下列連接字串為目標資料庫上*localhost*名為*asp net core-識別*。 在此設定時，EF Core 會設定為使用`DefaultConnection`連接字串。

    ```json
    {
      "ConnectionStrings": {
        "DefaultConnection": "Server=localhost;Database=aspnet-core-identity;Trusted_Connection=True;MultipleActiveResultSets=true"
      }
    }
    ```
1. 選取 **檢視** > **SQL Server 物件總管**。 展開對應至指定的資料庫名稱的節點`ConnectionStrings:DefaultConnection`的屬性*appsettings.json*。

    `Update-Database`命令所建立的結構描述所指定的資料庫和所需的應用程式初始化任何資料。 下圖說明使用上述步驟建立的資料表結構。

    ![身分識別的資料表](identity/_static/identity-tables.png)

## <a name="migrate-the-schema"></a>移轉結構描述

有的資料表結構和成員資格和 ASP.NET Core 身分識別的欄位中的細微差異。 使用 ASP.NET 和 ASP.NET Core 應用程式的驗證/授權已大幅變更模式。 仍會使用以身分識別的索引鍵物件*使用者*並*角色*。 以下是對應的資料表*使用者*，*角色*，並*UserRoles*。

### <a name="users"></a>使用者

|*Identity<br>(dbo.AspNetUsers)*        ||*Membership<br>(dbo.aspnet_Users / dbo.aspnet_Membership)*||
|----------------------------------------|-----------------------------------------------------------|
|**欄位名稱**                 |**Type**|**欄位名稱**                                    |**Type**|
|`Id`                           |字串  |`aspnet_Users.UserId`                             |字串  |
|`UserName`                     |字串  |`aspnet_Users.UserName`                           |字串  |
|`Email`                        |字串  |`aspnet_Membership.Email`                         |字串  |
|`NormalizedUserName`           |字串  |`aspnet_Users.LoweredUserName`                    |字串  |
|`NormalizedEmail`              |字串  |`aspnet_Membership.LoweredEmail`                  |字串  |
|`PhoneNumber`                  |字串  |`aspnet_Users.MobileAlias`                        |字串  |
|`LockoutEnabled`               |bit     |`aspnet_Membership.IsLockedOut`                   |bit     |

> [!NOTE]
> 並非所有的欄位對應類似於 ASP.NET Core 身分識別在從成員資格的一對一關聯性。 上表中的預設成員資格使用者結構描述並將它對應至 ASP.NET Core 身分識別結構描述。 任何其他自訂欄位所使用的成員資格，就必須手動對應。 在這個對應中，沒有任何對應的密碼，因為密碼 salt 和密碼條件可以兩者之間移轉。 **建議您讓密碼為 null，並要求重設其密碼的使用者。** 在 ASP.NET Core 身分識別`LockoutEnd`應該設定為在未來的某個日期中，如果使用者遭到鎖定。這是由移轉指令碼所示。

### <a name="roles"></a>角色

|*Identity<br>(dbo.AspNetRoles)*        ||*Membership<br>(dbo.aspnet_Roles)*||
|----------------------------------------|-----------------------------------|
|**欄位名稱**                 |**Type**|**欄位名稱**   |**Type**         |
|`Id`                           |字串  |`RoleId`         | 字串          |
|`Name`                         |字串  |`RoleName`       | 字串          |
|`NormalizedName`               |字串  |`LoweredRoleName`| 字串          |

### <a name="user-roles"></a>使用者角色

|*Identity<br>(dbo.AspNetUserRoles)*||*Membership<br>(dbo.aspnet_UsersInRoles)*||
|------------------------------------|------------------------------------------|
|**欄位名稱**           |**Type**  |**欄位名稱**|**Type**                   |
|`RoleId`                 |字串    |`RoleId`      |字串                     |
|`UserId`                 |字串    |`UserId`      |字串                     |

建立的移轉指令碼時，請參考上述對應表*使用者*並*角色*。 下列範例假設您有兩個資料庫的資料庫伺服器上。 一個資料庫包含現有的 ASP.NET 成員資格結構描述和資料。 另*CoreIdentitySample*使用稍早所述的步驟建立資料庫。 註解是包含的內嵌，如需詳細資訊。

```sql
-- THIS SCRIPT NEEDS TO RUN FROM THE CONTEXT OF THE MEMBERSHIP DB
BEGIN TRANSACTION MigrateUsersAndRoles
USE aspnetdb

-- INSERT USERS
INSERT INTO CoreIdentitySample.dbo.AspNetUsers
            (Id,
             UserName,
             NormalizedUserName,
             PasswordHash,
             SecurityStamp,
             EmailConfirmed,
             PhoneNumber,
             PhoneNumberConfirmed,
             TwoFactorEnabled,
             LockoutEnd,
             LockoutEnabled,
             AccessFailedCount,
             Email,
             NormalizedEmail)
SELECT aspnet_Users.UserId,
       aspnet_Users.UserName,
       -- The NormalizedUserName value is upper case in ASP.NET Core Identity
       UPPER(aspnet_Users.UserName),
       -- Creates an empty password since passwords don't map between the 2 schemas
       '',
       /*
        The SecurityStamp token is used to verify the state of an account and 
        is subject to change at any time. It should be initialized as a new ID.
       */
       NewID(),
       /*
        EmailConfirmed is set when a new user is created and confirmed via email.
        Users must have this set during migration to reset passwords.
       */
       1,
       aspnet_Users.MobileAlias,
       CASE
         WHEN aspnet_Users.MobileAlias IS NULL THEN 0
         ELSE 1
       END,
       -- 2FA likely wasn't setup in Membership for users, so setting as false.
       0,
       CASE
         -- Setting lockout date to time in the future (1,000 years)
         WHEN aspnet_Membership.IsLockedOut = 1 THEN Dateadd(year, 1000,
                                                     Sysutcdatetime())
         ELSE NULL
       END,
       aspnet_Membership.IsLockedOut,
       /*
        AccessFailedAccount is used to track failed logins. This is stored in
        Membership in multiple columns. Setting to 0 arbitrarily.
       */
       0,
       aspnet_Membership.Email,
       -- The NormalizedEmail value is upper case in ASP.NET Core Identity
       UPPER(aspnet_Membership.Email)
FROM   aspnet_Users
       LEFT OUTER JOIN aspnet_Membership
                    ON aspnet_Membership.ApplicationId =
                       aspnet_Users.ApplicationId
                       AND aspnet_Users.UserId = aspnet_Membership.UserId
       LEFT OUTER JOIN CoreIdentitySample.dbo.AspNetUsers
                    ON aspnet_Membership.UserId = AspNetUsers.Id
WHERE  AspNetUsers.Id IS NULL

-- INSERT ROLES
INSERT INTO CoreIdentitySample.dbo.AspNetRoles(Id, Name)
SELECT RoleId, RoleName
FROM aspnet_Roles;

-- INSERT USER ROLES
INSERT INTO CoreIdentitySample.dbo.AspNetUserRoles(UserId, RoleId)
SELECT UserId, RoleId
FROM aspnet_UsersInRoles;

IF @@ERROR <> 0
  BEGIN
    ROLLBACK TRANSACTION MigrateUsersAndRoles
    RETURN
  END

COMMIT TRANSACTION MigrateUsersAndRoles
```

在上述指令碼完成後之後, 稍早建立的 ASP.NET Core 身分識別應用程式會填入成員資格使用者。 使用者必須變更其密碼才能登入。

> [!NOTE]
> 如果成員資格系統有不符合其電子郵件地址的使用者名稱的使用者，需要變更就是要做到這一點稍早建立的應用程式。 預設範本會預期`UserName`和`Email`相同。 它們是不同的情況下，登入程序必須使用修改`UserName`而不是`Email`。

在 `PageModel`的登入頁面上，位於*Pages\Account\Login.cshtml.cs*，移除`[EmailAddress]`屬性從*電子郵件*屬性。 重新命名為*UserName*。 這需要變更任何地方`EmailAddress`所述，在*檢視*並*PageModel*。 結果看起來如下所示：

 ![固定的登入](identity/_static/fixed-login.png)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何移植到 ASP.NET Core 2.0 身分識別從 SQL 成員資格使用者。 如需 ASP.NET Core 身分識別的詳細資訊，請參閱[身分識別簡介](xref:security/authentication/identity)。
