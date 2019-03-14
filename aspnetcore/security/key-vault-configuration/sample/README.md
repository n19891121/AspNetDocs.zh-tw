---
ms.openlocfilehash: 122088c1227df81114de77fd578769770c3f6fd1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045585"
---
# <a name="key-vault-configuration-provider-sample-app"></a>金鑰保存庫組態提供者範例應用程式

此範例說明如何使用 Azure 金鑰保存庫的組態提供者。

這個範例會執行所決定的兩個模式之一`#define`陳述式，在頂端*Program.cs*檔案。 如需相關指示，請參閱 <<c0> [ 範例程式碼中的前置處理器指示詞](https://docs.microsoft.com/aspnet/core#preprocessor-directives-in-sample-code):

* `Basic` &ndash; 示範如何使用 Azure 金鑰保存庫用戶端識別碼和祕密儲存在 Azure Key Vault 存取祕密。 從任何位置，部署至 Azure App Service 或任何能夠為 ASP.NET Core 應用程式的主機，可以執行此版本的範例。
* `Managed` &ndash; 示範如何使用 Azure[受控服務識別](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)驗證的應用程式至 Azure Key Vault 與 Azure AD 驗證，而不需要在應用程式的程式碼或組態中的認證。 Azure AD 用戶端識別碼和密碼不需要使用 Azure Key Vault 進行驗證的應用程式。 此範例必須部署至 Azure App Service，以探索受管理的身分識別 scearnio。

如需詳細資訊，請參閱 < [Azure 金鑰保存庫組態提供者](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration)。
