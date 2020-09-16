---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
title: 設定 Web 服務器以 Web Deploy 發行 (離線部署) |Microsoft Docs
author: jrjlee
description: 本主題說明如何設定 IIS web 伺服器，以支援離線 web 發行和部署。 當您使用 Internet Information Services (.。。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ba92788f-9f03-44b1-b6b2-af8413e6a35d
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
msc.type: authoredcontent
ms.openlocfilehash: ed11720e6ea00df22f58d9afd32ccce95a5d1a60
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/16/2020
ms.locfileid: "90609665"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-offline-deployment"></a>設定 Web Deploy 發行的網頁伺服器 (離線部署)

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題說明如何設定 IIS web 伺服器，以支援離線 web 發行和部署。
> 
> 當您使用 Internet Information Services (IIS) Web 部署工具 (Web Deploy) 2.0 或更新版本時，有三種主要方法可用來將您的應用程式或網站放到 Web 服務器上。 您可以：
> 
> - 使用 *Web Deploy 遠端代理程式服務*。 這種方法需要較少的 web 伺服器設定，但您必須提供本機伺服器系統管理員的認證，才能將任何程式部署至伺服器。
> - 使用 *Web Deploy 處理常式*。 這種方法比較複雜，而且需要更多的初始工作來設定 web 伺服器。 不過，當您使用此方法時，您可以設定 IIS 以允許非系統管理員的使用者執行部署。 Web Deploy 處理常式僅適用于 IIS 7 版或更新版本。
> - 使用 *離線部署*。 這種方法需要最少的 web 伺服器設定，但是伺服器管理員必須手動將 web 套件複製到伺服器上，然後透過 IIS 管理員將它匯入。
> 
> 如需這些方法的主要功能、優點和缺點的詳細資訊，請參閱 [選擇 Web 部署的正確方法](choosing-the-right-approach-to-web-deployment.md)。

是，如果您的網路基礎結構或安全性限制會防止遠端部署。 這很可能是在網際網路對向生產環境中的情況，也就是從您的伺服器基礎結構的其餘部分&#x2014;的&#x2014;，將網頁伺服器隔離。

很明顯地，如果您的 web 應用程式會定期更新，這種方法就變得較不理想。 如果您的基礎結構允許，您可能會想要考慮使用 Web Deploy 處理常式或 Web Deploy 遠端代理程式服務來啟用遠端部署。

## <a name="task-overview"></a>工作總覽

若要將網頁伺服器設定為支援離線匯入和部署 web 封裝，您必須：

- 安裝 IIS 7.5 和 IIS 7 建議的設定。
- 安裝 Web Deploy 2.1 或更新版本。
- 建立 IIS 網站來裝載已部署的內容。
- 停用 Web Deployment Agent 服務。

若要特別裝載範例解決方案，您也需要：

- 安裝 .NET Framework 4.0。
- 安裝 ASP.NET MVC 3。

本主題將示範如何執行這些程式。 本主題中的工作和逐步解說假設您是從執行 Windows Server 2008 R2 的全新伺服器組建開始。 繼續之前，請確定：

- 已安裝 Windows Server 2008 R2 Service Pack 1 及所有可用的更新。
- 伺服器已加入網域。
- 伺服器具有靜態 IP 位址。

> [!NOTE]
> 如需將電腦加入網域的詳細資訊，請參閱將 [電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。 如需設定靜態 IP 位址的詳細資訊，請參閱 [設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。

## <a name="install-products-and-components"></a>安裝產品和元件

本節將引導您在 web 伺服器上安裝必要的產品和元件。 開始之前，最好先執行 Windows Update，以確保您的伺服器完全處於最新狀態。

在此情況下，您必須安裝下列專案：

- **IIS 7 建議**的設定。 這可讓 web 伺服器 ** (iis) ** 角色在您的 web 伺服器上，並安裝您所需的一組 iis 模組和元件，以便裝載 ASP.NET 應用程式。
- **.NET Framework 4.0**。 若要執行以此版本的 .NET Framework 建立的應用程式，這是必要的。
- **Web 部署工具2.1 或更新版本**。 這會在您的伺服器上安裝 Web Deploy (及其基礎可執行檔 MSDeploy.exe) 。 Web Deploy 與 IIS 整合，並可讓您匯入和匯出 web 封裝。
- **ASP.NET MVC 3**。 這會安裝執行 MVC 3 應用程式所需的元件。

> [!NOTE]
> 本逐步解說將說明如何使用 Web Platform Installer 來安裝和設定各種元件。 雖然您不需要使用 Web Platform Installer，但它會自動偵測相依性，並確保您一律取得最新的產品版本，藉此簡化安裝程式。 如需詳細資訊，請參閱 [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118)。

**若要安裝必要的產品和元件**

1. 下載並安裝 [Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。
2. 安裝完成時，Web Platform Installer 將會自動啟動。

    > [!NOTE]
    > 您現在可以從 [ **開始** ] 功能表啟動 Web Platform Installer。 若要這樣做，請在 [ **開始** ] 功能表上，按一下 [ **所有程式**]，然後按一下 [ **Microsoft Web Platform Installer**]。
3. 在 **Web Platform Installer 3.0** ] 視窗的頂端，按一下 [ **產品**]。
4. 在視窗的左側 **，按一下 [** 流覽] 窗格中的 [架構]。
5. 在 [ **Microsoft .NET Framework 4** ] 資料列中，如果尚未安裝 .NET Framework，請按一下 [ **新增**]。

    > [!NOTE]
    > 您可能已經透過 Windows Update 安裝了 .NET Framework 4.0。 如果已安裝產品或元件，Web Platform Installer 將會以**安裝**的文字取代 [**新增**] 按鈕來指出這一點。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image1.png)
6. 在 **ASP.NET MVC 3 (Visual Studio 2010) ** 資料列中，按一下 [ **新增**]。
7. 在流覽窗格中，按一下 [ **伺服器**]。
8. 在 [ **IIS 7 建議** 的設定] 列中，按一下 [ **新增**]。
9. 在 [ **Web 部署工具 2.1** ] 列中，按一下 [ **新增**]。
10. 按一下 [安裝]。 Web Platform Installer 將會顯示一份產品清單，其中包含要安裝之任何相關聯的相依性&#x2014;&#x2014;，並會提示您接受授權條款。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image2.png)
11. 請參閱授權條款，如果您同意條款，請按一下 [ **我接受**]。
12. 當安裝完成時，請按一下 **[完成]**，然後關閉 **Web Platform Installer 3.0** 視窗。

如果您在安裝 IIS 之前安裝了 .NET Framework 4.0，則必須執行 [ASP.NET Iis 註冊工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet \_regiis.exe) 向 IIS 註冊最新版本的 ASP.NET。 如果您沒有這麼做，您會發現 IIS 將提供靜態內容 (像是 HTML 檔案) 沒有任何問題，但它會傳回 **HTTP 錯誤404.0 –** 當您嘗試流覽至 ASP.NET 內容時，找不到此錯誤。 您可以使用下一個程式來確定 ASP.NET 4.0 已註冊。

**若要向 IIS 註冊 ASP.NET 4。0**

1. 按一下 [ **開始**]，然後輸入 **命令提示**字元。
2. 在搜尋結果中，以滑鼠右鍵按一下 [ **命令提示**字元]，然後按一下 [以 **系統管理員身分執行**]。
3. 在命令提示字元視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 目錄。
4. 輸入此命令，然後按 Enter：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample1.cmd)]
5. 如果您打算在任何時間點裝載64位的 web 應用程式，您也應該向 IIS 註冊64位版本的 ASP.NET。 若要這樣做，請在命令提示字元視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 目錄。
6. 輸入此命令，然後按 Enter：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample2.cmd)]

好的做法是，此時再次使用 Windows Update，以下載並安裝您已安裝之新產品和元件的任何可用更新。

## <a name="configure-the-iis-website"></a>設定 IIS 網站

在您可以將 web 內容部署到伺服器之前，您必須先建立並設定 IIS 網站來裝載內容。 Web Deploy 只能將 web 套件部署到現有的 IIS 網站;它無法為您建立網站。 概括而言，您必須完成下列工作：

- 在檔案系統上建立資料夾來裝載您的內容。
- 建立 IIS 網站以提供內容，並將它與本機資料夾產生關聯。
- 將讀取權限授與本機資料夾上的應用程式集區身分識別。

雖然不會阻止您將內容部署至 IIS 中的預設網站，但不建議針對測試或示範情節以外的任何專案使用這種方法。 若要模擬生產環境，您應該建立新的 IIS 網站，其中包含您的應用程式需求特有的設定。

**若要建立及設定 IIS 網站**

1. 在本機檔案系統上建立資料夾，以儲存您的內容 (例如 **C:\DemoSite**) 。
2. 在 [ **開始** ] 功能表上，指向 [系統 **管理工具**]，然後按一下 [ **Internet Information Services (IIS) 管理員**。
3. 在 [IIS 管理員] 的 [ **連接** ] 窗格中，展開伺服器節點 (例如 **PROWEB1**) 。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image3.png)
4. 以滑鼠右鍵按一下 [ **網站** ] 節點，然後按一下 [ **新增網站**]。
5. 在 [ **網站名稱** ] 方塊中，輸入 IIS 網站的名稱 (例如， **DemoSite**) 。
6. 在 [ **實體路徑** ] 方塊中，輸入 (或流覽以) 本機資料夾的路徑 (例如， **C:\DemoSite**) ]。
7. 在 [ **埠** ] 方塊中，輸入您要用來裝載網站 (的埠號碼，例如 **85**) 。

    > [!NOTE]
    > 適用于 HTTP 的標準埠號碼是80，而 HTTPS 則是443。 但是，如果您在埠80上裝載此網站，您必須先停止預設網站，才能存取您的網站。
8. 將 [ **主機名稱** ] 方塊保留空白，除非您要為網站設定網域名稱系統 (DNS) 記錄，然後按一下 **[確定]**。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image4.png)

    > [!NOTE]
    > 在生產環境中，您可能會想要在埠80上裝載您的網站，並設定主機標頭和相符的 DNS 記錄。 如需在 IIS 7 中設定主機標頭的詳細資訊，請參閱 [設定網站的主機標頭 (iis 7) ](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。 如需有關 Windows Server 2008 R2 中的 DNS 伺服器角色的詳細資訊，請參閱 [Dns 伺服器總覽](https://technet.microsoft.com/library/cc770392.aspx) 和 [dns 伺服器](https://technet.microsoft.com/windowsserver/dd448607)。
9. 在 [ **動作** ] 窗格的 [ **編輯站台**] 下方，按一下 [ **繫結**]。
10. 在 [站台繫結]**** 對話方塊中，按一下 [新增]****。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image5.png)
11. 在 [ **新增網站** 系結] 對話方塊中，將 [ **IP 位址** ] 和 [ **埠** ] 設定為符合您現有的網站設定。
12. 在 [ **主機名稱** ] 方塊中，輸入您的 web 伺服器名稱 (例如， **PROWEB1**) ，然後按一下 **[確定]**。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image6.png)

    > [!NOTE]
    > 第一個網站系結可讓您使用 IP 位址和埠或，在本機存取網站 `http://localhost:85` 。 第二個網站系結可讓您使用電腦名稱稱從網域上的其他電腦存取網站 (例如， http://proweb1:85) 。
13. 在 [站台繫結]**** 對話方塊中，按一下 [關閉]****。
14. 在 [連線]**** 窗格中，按一下 [應用程式集區]****。
15. 在 [ **應用程式** 集區] 窗格中，以滑鼠右鍵按一下應用程式集區的名稱，然後按一下 [ **基本設定**]。 根據預設，您的應用程式集區名稱會與您的網站名稱相符 (例如， **DemoSite**) 。
16. 在 [ **.NET Framework 版本** ] 清單中，選取 **.NET Framework v 4.0.30319**，然後按一下 **[確定]**。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image7.png)

    > [!NOTE]
    > 範例解決方案需要 .NET Framework 4.0。 這不是一般 Web Deploy 的需求。

為了讓您的網站提供內容，應用程式集區身分識別必須具有儲存內容的本機資料夾的 [讀取] 許可權。 在 IIS 7.5 中，應用程式集區預設會使用唯一的應用程式集區身分識別來執行 (與舊版的 IIS 相反，因為應用程式集區通常會使用網路服務帳戶) 來執行。 應用程式集區身分識別不是真正的使用者帳戶，也不會顯示在任何使用者或群組的清單上&#x2014;而是在應用程式集區啟動時動態建立。 每個應用程式集區身分識別都會新增至本機 **IIS \_ IUSRS** 安全性群組作為隱藏專案。

若要授與許可權給檔案或資料夾上的應用程式集區身分識別，您有兩個選項：

- 直接將許可權指派給應用程式集區身分識別，使用 **Iis AppPool \( 應用程式集區名稱 ** 的格式)  (例如 **iis AppPool\DemoSite**) 。
- 將許可權指派給 **IIS \_ IUSRS** 群組。

最常見的方法是將許可權指派給本機 **IIS \_ IUSRS** 群組，因為這種方法可讓您變更應用程式集區，而不需要重新設定檔案系統許可權。 下一個程式會使用這個以群組為基礎的方法。

> [!NOTE]
> 如需 IIS 7.5 中應用程式集區身分識別的詳細資訊，請參閱 [應用程式集](https://go.microsoft.com/?linkid=9805123)區身分識別。

**設定 IIS 網站的資料夾許可權**

1. 在 Windows 檔案總管中，流覽至本機資料夾的位置。
2. 在資料夾上按一下滑鼠右鍵，然後按一下 [內容]****。
3. 在 [**Security**] 索引標籤上按一下 [**Edit**]，然後按一下 [**Add**]。
4. 按一下 [位置]。 在 [ **位置** ] 對話方塊中，選取本機伺服器，然後按一下 **[確定]**。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image8.png)
5. 在 [ **選取使用者或群組** ] 對話方塊中，輸入 **IIS \_ IUSRS**，按一下 [ **檢查名稱**]，然後按一下 **[確定]**。
6. 在 [ ** (資料夾名稱的許可權) ** ] 對話方塊中，請注意，根據預設，已將 [ **讀取] & [執行**]、[ **列出資料夾內容**] 和 [ **讀取** ] 許可權指派給新群組。 保持不變，然後按一下 **[確定]**。
7. 按一下 **[確定** ]，關閉 ** (資料夾名稱) ** 內容] 對話方塊。

## <a name="disable-the-remote-agent-service"></a>停用遠端代理程式服務

當您安裝 Web Deploy 時，Web Deployment Agent 服務會自動安裝並啟動。 這種服務可讓您從遠端位置部署和發佈 web 套件。 在此案例中，您將不會使用遠端部署功能，因此您應該停止並停用服務。

> [!NOTE]
> 您不需要停止遠端代理程式服務，就能手動匯入和部署 web 封裝。 不過，如果您不打算使用服務，最好是停止並停用服務。

您可以使用各種命令列公用程式或 Windows PowerShell Cmdlet，以多種方式來停止和停用服務。 此程式描述以 UI 為基礎的簡單方法。

**停止和停用遠端代理程式服務**

1. 在 [開始]  功能表上，指向 [系統管理工具]  ，然後按一下 [服務]  。
2. 在 [服務] 主控台中，找出 **Web Deployment Agent 服務** 資料列。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image9.png)
3. 以滑鼠右鍵按一下 [ **Web Deployment Agent Service**]， **然後按一下 [** 內容]。
4. 在 **Web Deployment Agent 服務屬性** ] 對話方塊中，按一下 [ **停止**]。
5. 在 [ **啟動類型** ] 清單中，選取 [ **已停用**]，然後按一下 **[確定]**。

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image10.png)

## <a name="conclusion"></a>結論

至此，您的網頁伺服器已準備好進行離線 web 封裝部署。 在您嘗試將 web 套件匯入至 IIS 網站之前，您可能會想要檢查這些重點：

- 您是否已向 IIS 註冊 ASP.NET 4.0？
- 應用程式集區身分識別是否擁有您網站源資料夾的讀取存取權？
- 您是否已停止 Web Deployment Agent 服務？

> [!div class="step-by-step"]
> [上一個](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) 
> [下一步](configuring-a-database-server-for-web-deploy-publishing.md)
