---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
title: 應用程式生命週期管理：從開發到生產環境 |Microsoft Docs
author: jrjlee
description: 本主題將說明一家虛構公司如何管理 ASP.NET web 應用程式部署透過測試、 預備及生產環境為 par...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f97a1145-6470-4bca-8f15-ccfb25fb903c
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
msc.type: authoredcontent
ms.openlocfilehash: 7cb9c949936c3af73d4c904d401c36d4d83f3e18
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045685"
---
<a name="application-lifecycle-management-from-development-to-production"></a>應用程式生命週期管理：從開發到生產
====================
藉由[Jason Lee](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題會說明一家虛構公司如何管理 ASP.NET web 應用程式部署透過測試、 預備及生產環境持續開發程序的一部分。 在主題中，會提供進一步資訊及如何執行特定工作的逐步解說的連結。
> 
> 本主題旨在提供的高階概觀[系列的教學課程](deploying-web-applications-in-enterprise-scenarios.md)在企業中的 web 部署。 別擔心，如果您不熟悉此處所述的概念&#x2014;遵循這些教學課程提供所有這些工作與技術的詳細的資訊。
> 
> > [!NOTE]
> > 尚未註冊起見，為了簡單起見，本主題不討論資料庫更新部署程序的一部分。 不過，對資料庫功能，進行累加式更新是許多的企業部署案例的需求，而且您可以找到有關如何完成這項作業，稍後在本教學課程系列中的指示。 如需詳細資訊，請參閱 <<c0> [ 部署資料庫專案](../web-deployment-in-the-enterprise/deploying-database-projects.md)。


## <a name="overview"></a>總覽

如下圖所示的部署程序根據 Fabrikam，Inc.部署案例中所述[企業 Web 部署：案例概觀](enterprise-web-deployment-scenario-overview.md)。 研讀本主題之前，您應該閱讀案例概觀。 基本上，此案例會檢查如何組織管理相當複雜的 web 應用程式部署[連絡管理員解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)，透過一般的企業環境中的各個不同階段。

概括而言，連絡管理員解決方案會透過這些階段，為開發和部署程序的一部分：

1. 開發人員檢查 Team Foundation Server (TFS) 2010年到的一些程式碼。
2. TFS 建置程式碼，並執行任何 team 專案相關聯的單元測試。
3. TFS 會部署到測試環境的解決方案。
4. 開發人員團隊會驗證，並驗證測試環境中的解決方案。
5. 預備環境系統管理員會執行"what if"部署到預備環境，以建立部署是否會造成任何問題。
6. 預備環境系統管理員會執行即時部署到預備環境。
7. 解決方案會進行使用者接受度測試預備環境中。
8. Web 部署套件會以手動方式匯入至生產環境。

這些階段會形成連續的開發週期的一部分。

![](application-lifecycle-management-from-development-to-production/_static/image1.png)

在實務上，您會發現當我們查看更多詳細資料的每個階段時，會稍微複雜一點，程序。 Fabrikam，Inc.會針對每個目標環境中使用不同的方法來部署。

![](application-lifecycle-management-from-development-to-production/_static/image2.png)

本主題的其餘部分會檢查此部署生命週期的這些重要階段：

- **必要條件**:您要設定您的伺服器基礎結構，才能將您的部署邏輯就地如何。
- **開發和部署的初始**:您需要先在您部署方案的第一次執行。
- **若要測試部署**:如何封裝，並將內容部署至測試環境會自動為開發人員簽入新的程式碼時。
- **部署至預備環境**:如何部署特定組建的預備環境，以及如何執行 「 假設 」 部署，以確保部署不會造成任何問題。
- **部署至生產環境**:如何將 web 將封裝匯入實際執行環境時的網路基礎結構即會阻止遠端部署。

## <a name="prerequisites"></a>必要條件

任何部署案例中的第一個工作是確保您的伺服器基礎結構符合您的部署工具和技術需求。 在此案例中，Fabrikam，Inc.已設定其伺服器基礎結構，就像這樣：

- TFS 會設定為包含 team 專案集合、 組建控制器和組建代理程式。 請參閱[自動化 Web 部署設定 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)如需詳細資訊。
- 測試環境設定為接受遠端的部署使用 Web Deployment Agent Service （「 遠端代理程式 」），如中所述[案例：設定 Web 部署的測試環境](../configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment.md)並[設定網頁伺服器，Web deploy 發行 （遠端代理程式）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。
- 預備環境設定為接受遠端的部署使用 Web 部署的處理常式的端點，如中所述[案例：設定 Web 部署的預備環境](../configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment.md)並[Web deploy 發行設定網頁伺服器 (Web Deploy 處理常式)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。
- 生產環境設定為允許系統管理員手動匯入網際網路資訊服務 (IIS) 中，web 部署套件中所述[案例：設定 Web 部署的生產環境](../configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment.md)並[設定網頁伺服器，Web deploy 發行 （離線部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。

## <a name="initial-development-and-deployment"></a>初始的開發和部署

Fabrikam，Inc.開發團隊可以在第一次部署連絡管理員解決方案之前，必須執行下列工作：

- 在 TFS 中建立新的 team 專案。
- 建立包含部署邏輯的 Microsoft Build Engine (MSBuild) 專案檔。
- 建立觸發程序部署程序的 TFS 組建定義。

### <a name="create-a-new-team-project"></a>建立新的 Team 專案

- TFS 系統管理員，Rob Walters 會建立新的 team 專案，則應用程式中所述[在 TFS 中建立 Team 專案](../configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs.md)。 接下來，開發組長，Matt 世昕，會建立基本架構的解決方案。 他會檢查他的檔案在 TFS 中，在新 team 專案中所述[新增內容至原始檔控制](../configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control.md)。

### <a name="create-the-deployment-logic"></a>建立部署邏輯

Matt 世昕建立各種自訂 MSBuild 專案檔，使用分割的專案檔案方法中所述[了解專案檔](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。 Matt 會建立：

- 專案檔名為*Publish.proj*執行部署程序。 此檔案包含 MSBuild 目標，建置方案中的專案、 建立 web 封裝和封裝部署到目的地伺服器的環境。
- 環境特定的專案檔名為*Env Dev.proj*並*Env Stage.proj*。 這些包含分別針對測試環境和預備環境，例如連接字串、 服務端點和將會收到 web 封裝的遠端服務的詳細資料的設定。 如需選擇特定的目的地環境的正確設定的指引，請參閱 <<c0> [ 設定的目標環境的部署屬性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

若要執行部署，使用者會執行*Publish.proj*檔案中，使用 MSBuild 或 Team Build，並指定相關的特定環境的專案檔的位置 (*Env Dev.proj* 或*Env Stage.proj*) 做為命令列引數。 *Publish.proj*檔然後匯入環境特定的專案檔案，以建立一組完整的發行的每個目標環境的指示。

> [!NOTE]
> 這些自訂的專案檔案的方式與您用來叫用 MSBuild 的機制無關。 例如，您可以使用 MSBuild 命令列直接中所述[了解專案檔](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。 中所述，您可以從 命令檔，執行專案檔[建立和執行部署命令檔](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)。 或者，您可以執行專案檔從 TFS 中的組建定義中所述[建立組建定義該支援部署](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。  
> 在每個案例的最終結果是相同&#x2014;MSBuild 執行合併的專案檔，並將您的解決方案部署到目標環境。 這會提供您足夠的彈性，您如何觸發您的發行程序。


一旦他已建立自訂的專案檔，Matt 會將它們加入至方案資料夾，並簽入至原始檔控制。

### <a name="create-build-definitions"></a>建立組建定義

為最終的準備工作，Matt 和 Rob 共同運作以建立新的 team 專案的三個組建定義：

- **DeployToTest**。 這會建置連絡管理員解決方案，並將其部署到測試環境中，每次簽入時，就會發生。
- **DeployToStaging**。 當開發人員組建排入佇列時，這會部署到預備環境指定的前一個組建的資源。
- **DeployToStaging-WhatIf**。 當開發人員組建排入佇列時，這會執行"what if"部署到預備環境。

下列各節提供更多詳細資料每一種組建定義。

## <a name="deployment-to-test"></a>部署至測試

在 Fabrikam，Inc.開發小組會維護測試環境，以進行各種不同的軟體測試活動，例如驗證和驗證、 可用性測試、 相容性測試，以及臨機操作或探勘測試。

開發小組已建立名為 TFS 中的組建定義**DeployToTest**。 此組建定義會使用持續整合觸發程序，這表示建置程序執行每次簽入時執行的 Fabrikam，Inc.開發小組的成員。 觸發組建時，便會將組建定義：

- 建置 ContactManager.sln 方案。 接著，這會建置方案中的每個專案。
- （如果已成功建置方案），請在方案資料夾結構中執行任何單元測試。
- 執行自訂的專案檔，以控制部署程序 （如果方案建置成功，且會傳遞任何單元測試）。

最終結果是將解決方案建置成功，並通過單元測試之後，如果網頁套件及任何其他部署的資源都部署到測試環境。

![](application-lifecycle-management-from-development-to-production/_static/image3.png)

### <a name="how-does-the-deployment-process-work"></a>部署程序如何運作？

**DeployToTest**組建定義提供 msbuild 的這些引數：


[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample1.cmd)]


**DeployOnBuild = true**並**DeployTarget = 封裝**Team Build 建置方案中的專案時，會使用屬性。 專案的 web 應用程式專案時，這些屬性會指示 MSBuild 來建立專案的 web 部署封裝。 **TargetEnvPropsFile**屬性會告知*Publish.proj*檔案尋找要匯入的特定環境的專案檔的位置。

> [!NOTE]
> 如需如何建立這類的組建定義的詳細逐步解說，請參閱 <<c0> [ 建立組建定義該支援部署](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。


*Publish.proj*檔案包含建置方案中的每個專案的目標。 不過，它也包含條件式邏輯，會略過這些建置目標如果您在 Team Build 中執行該檔案。 這可讓您利用 Team Build 提供的例如能夠執行單元測試的其他組建功能。 如果方案組建或單元測試失敗， *Publish.proj*檔案將不會執行，並將不會部署應用程式。

條件式邏輯法則是評估**BuildingInTeamBuild**屬性。 這是會自動設為 MSBuild 屬性 **，則為 true**當您使用 Team Build 來建置您的專案。

## <a name="deployment-to-staging"></a>部署至預備環境

當組建符合所有需求的開發人員小組在測試環境中時，小組可能會想要將相同的組建部署至預備環境。 預備環境通常會設定為符合生產環境或 「 即時 」 環境為密切越好，例如，根據伺服器規格、 作業系統和軟體和網路設定的特性。 預備環境通常用於負載測試、 使用者接受度測試，以及更廣泛的內部審查。 組建會部署到預備環境中，直接從組建伺服器。

![](application-lifecycle-management-from-development-to-production/_static/image4.png)

用來將方案部署到預備環境中，組建定義**DeployToStaging-WhatIf**並**DeployToStaging**，共用這些特性：

- 它們實際上不建立任何項目。 Rob 將方案部署到預備環境中，當他想要部署特定的現有組建的已驗證和測試環境中進行驗證。 組建定義只需要執行自訂的專案檔，以控制部署程序。
- 當 Rob 觸發組建時，他會使用組建參數來指定哪些組建包含他想要從組建伺服器部署的資源。
- 不會自動觸發的組建定義。 Rob 手動組建排入佇列時，他想要將方案部署到預備環境。

這是為了部署至預備環境的高階程序：

1. 預備環境的環境系統管理員，Rob Walters 排入佇列的組建，使用**DeployToStaging-WhatIf**組建定義。 Rob 會使用組建定義參數來指定他想要部署的組建。
2. **DeployToStaging-WhatIf**組建定義執行 「 假設 」 模式中的自訂專案檔。 這會產生記錄檔，好像 Rob 的執行狀況的即時部署，但它實際上不進行任何變更到目的地環境。
3. Rob 檢閱記錄檔，以確定在預備環境部署的影響。 特別是，Rob 想要檢查項目將會新增、 更新項目，和項目將會被刪除。
4. Rob 是否滿足，部署將不會進行任何不想要變更現有的資源或資料，他排入佇列的組建，使用**DeployToStaging**組建定義。
5. **DeployToStaging**組建定義執行自訂的專案檔。 這些發行至預備環境中的主要 web 伺服器的部署資源。
6. Web 伺服陣列架構 (WFF) 控制器會同步處理在預備環境中的 web 伺服器。 這可讓應用程式可以使用伺服器陣列中的所有 web 伺服器上。

### <a name="how-does-the-deployment-process-work"></a>部署程序如何運作？

**DeployToStaging**組建定義提供 msbuild 的這些引數：


[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample2.cmd)]


**TargetEnvPropsFile**屬性會告知*Publish.proj*檔案尋找要匯入的特定環境的專案檔的位置。 **OutputRoot**屬性會覆寫內建的值，表示組建資料夾包含您想要部署之資源的位置。 當 Rob 組建排入佇列時，他會使用**參數**索引標籤，以提供更新的值，如**OutputRoot**屬性。

![](application-lifecycle-management-from-development-to-production/_static/image5.png)

> [!NOTE]
> 如需有關如何建立這類的組建定義的詳細資訊，請參閱[部署特定建置](../configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build.md)。


**DeployToStaging-WhatIf**組建定義包含與相同的部署邏輯**DeployToStaging**組建定義。 不過，它包含額外的引數**WhatIf = true**:


[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample3.cmd)]


內*Publish.proj*檔案， **WhatIf**屬性會指出部署的所有資源，應該會在 「 假設 」 模式中都發佈。 換句話說，如同部署掉了，但不實際變更目的地環境中，會產生記錄檔。 這可讓您評估建議的部署的影響&#x2014;特定、 項目就會被新增、 項目將會更新，和項目將會刪除&#x2014;在實際進行任何變更之前。

> [!NOTE]
> 如需有關如何設定 「 假設 」 部署的詳細資訊，請參閱 <<c0> [ 執行 「 假設 」 部署](../advanced-enterprise-web-deployment/performing-a-what-if-deployment.md)。


一旦您部署到預備環境中的主要 web 伺服器應用程式，WFF 會自動同步應用程式在伺服器陣列中的所有伺服器。

> [!NOTE]
> 如需有關如何設定同步處理 web 伺服器 WFF 的詳細資訊，請參閱[使用 Web 伺服陣列架構建立伺服器陣列](../configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework.md)。


## <a name="deployment-to-production"></a>部署至生產環境

組建已核准在預備環境中，Fabrikam，Inc.小組可以發行至生產環境應用程式。 生產環境是應用程式會 「 即時 」 和達到其目標對象的一般使用者的位置。

生產環境是在網際網路對向周邊網路中。 這是與包含組建伺服器的內部網路隔離。 生產環境系統管理員，Lisa Andrews，必須以手動方式複製的 web 部署套件從組建伺服器和主要實際執行網頁伺服器上將它們匯入 IIS。

![](application-lifecycle-management-from-development-to-production/_static/image6.png)

這是為了部署至生產環境的高階程序：

1. 開發人員團隊建議 Lisa 組建可供部署至生產環境。 小組在組建伺服器上建議 Lisa 的置放資料夾內的 web 部署套件的位置。
2. Lisa 會收集網頁套件從組建伺服器，並將其複製到主要 web 伺服器，在生產環境中。
3. Lisa 會匯入和發佈網頁套件，在主要 web 伺服器上的使用 IIS 管理員。
4. WFF 控制器會同步處理生產環境中的 web 伺服器。 這可讓應用程式可以使用伺服器陣列中的所有 web 伺服器上。

### <a name="how-does-the-deployment-process-work"></a>部署程序如何運作？

IIS 管理員包含匯入應用程式套件精靈，可讓您輕鬆地將 web 套件發佈到 IIS 網站。 如需如何執行此程序的逐步解說，請參閱 <<c0> [ 手動安裝網頁套件](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)。

## <a name="conclusion"></a>結論

本主題提供一般的企業級 web 應用程式的部署生命週期的示範。

本主題會構成一系列的 web 應用程式部署的各種層面提供指導方針的教學課程的一部分。 在實務上，每個階段的部署程序中，有許多其他的工作和考量，並不可能在單一的逐步解說。 如需詳細資訊，請參閱這些教學課程：

- [Web 部署在企業中的](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教學課程提供使用 MSBuild 和 IIS Web Deployment Tool (Web Deploy) 的 web 部署技術的完整介紹。
- [設定 Web 部署的伺服器環境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教學課程提供有關如何設定 Windows server 環境，以支援各種部署案例的指引。
- [設定 Team Foundation Server 自動 Web 部署](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教學課程提供如何將部署邏輯整合到 TFS 的建置流程指引。
- [進階企業 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教學課程提供指引如何符合某些更複雜的部署挑戰該組織的臉部。

> [!div class="step-by-step"]
> [上一步](enterprise-web-deployment-scenario-overview.md)
