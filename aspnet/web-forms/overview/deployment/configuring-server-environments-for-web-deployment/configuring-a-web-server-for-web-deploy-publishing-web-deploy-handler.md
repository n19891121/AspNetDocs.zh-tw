---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: 設定 Web Deploy 發行的網頁伺服器 (Web Deploy 處理常式)
author: jrjlee
description: 本主題說明如何設定 Internet Information Services (IIS) web 伺服器，以支援使用 IIS Web Deploy 漢字的 web 發佈和部署 .。。
ms.author: riande
ms.date: 01/29/2017
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: af46b5a74309fbae4b5db072363e71d965445f9a
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/16/2020
ms.locfileid: "90609688"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a>設定 Web Deploy 發行的網頁伺服器 (Web Deploy 處理常式)

[PDF 下載](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題說明如何使用 IIS Web Deploy 處理常式，設定 Internet Information Services (IIS) web 伺服器來支援 web 發行和部署。
> 
> 當您使用 Web Deploy 2.0 或更新版本時，有三種主要方法可用來將您的應用程式或網站放到 Web 服務器上。 您可以：
> 
> - 使用 *Web Deploy 遠端代理程式服務*。 這種方法需要較少的 web 伺服器設定，但您必須提供本機伺服器系統管理員的認證，才能將任何程式部署至伺服器。
> - 使用 *Web Deploy 處理常式*。 這種方法比較複雜，而且需要更多的初始工作來設定 web 伺服器。 不過，當您使用此方法時，您可以設定 IIS 以允許非系統管理員的使用者執行部署。 Web Deploy 處理常式僅適用于 IIS 7 版或更新版本。
> - 使用 *離線部署*。 這種方法需要最少的 web 伺服器設定，但是伺服器管理員必須手動將 web 套件複製到伺服器上，然後透過 IIS 管理員將它匯入。
> 
> 如需這些方法的主要功能、優點和缺點的詳細資訊，請參閱 [選擇 Web 部署的正確方法](choosing-the-right-approach-to-web-deployment.md)。

是，如果您想要允許非系統管理員的使用者將內容部署到特定的 IIS 網站。 在這些類型的案例中，通常會需要這種方法：

- 暫存或生產環境，在此環境中，觸發遠端部署的人員或服務帳戶不太可能存取伺服器管理員的認證。
- 裝載的環境，您想要讓遠端使用者能夠更新其網站，而不需讓他們完全掌控您的 web 伺服器 (或存取任何其他網站) 。

在開發或測試案例中，或在小型組織中，使用伺服器管理員認證來部署內容通常較不之間爭論。 在這些情況下，將您的網頁伺服器設定為支援使用 [Web Deploy 遠端代理程式服務](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) 進行部署，可提供更簡單的方法。

## <a name="task-overview"></a>工作總覽

若要使用 Web Deploy 處理常式方法，將網頁伺服器設定為從遠端電腦接受及部署 web 封裝，您必須：

- 建立或選擇網域使用者帳戶 (「非系統管理員使用者」 ) 您將用來執行部署的認證。
- 安裝 IIS 7.5，包括 Web 管理服務和基本驗證模組。
- 安裝 Web Deploy 2.1 或更新版本。
- 將 Web 管理服務設定為允許遠端連線，並啟動服務。
- 建立 IIS 網站來裝載已部署的內容。
- 在 IIS 管理員中，為您的網站授與非系統管理員的使用者許可權。
- 確定 Web 管理服務委派規則允許服務使用您的非系統管理員使用者帳戶來新增和變更網站內容。
- 設定任何防火牆，以允許埠8172上的連入連線。

若要特別裝載 ContactManager 範例解決方案，您也需要：

- 安裝 .NET Framework 4.0。
- 安裝 ASP.NET MVC 3。

本主題將示範如何執行這些程式。 本主題中的工作和逐步解說假設您是從執行 Windows Server 2016 的全新伺服器組建開始。 繼續之前，請確定：

- Windows Server 2016
- 伺服器已加入網域。
- 伺服器具有靜態 IP 位址。

> [!NOTE]
> 如需將電腦加入網域的詳細資訊，請參閱將 [電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。 如需設定靜態 IP 位址的詳細資訊，請參閱 [設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。

## <a name="install-products-and-components"></a>安裝產品和元件

本節將引導您在 web 伺服器上安裝必要的產品和元件。 開始之前，最好先執行 Windows Update，以確保您的伺服器完全處於最新狀態。

在此情況下，您必須安裝下列專案：

- **IIS 7 建議**的設定。 這可讓 web 伺服器 ** (iis) ** 角色在您的 web 伺服器上，並安裝您所需的一組 iis 模組和元件，以便裝載 ASP.NET 應用程式。
- **IIS：管理服務**。 這會在 IIS 中安裝 Web 管理服務 (WMSvc) 。 這項服務可讓您從遠端系統管理 IIS 網站，並向用戶端公開 Web Deploy 處理常式端點。
- **IIS：基本驗證**。 這會安裝 IIS 基本驗證模組。 這可讓 Web 管理服務 (WMSvc) 驗證您所提供的認證。
- **Web 部署工具2.1 或更新版本**。 這會在您的伺服器上安裝 Web Deploy (及其基礎可執行檔 MSDeploy.exe) 。 在這個程式中，它會安裝 Web Deploy 處理常式，並將它與 Web 管理服務整合。
- **.NET Framework 4.0**。 若要執行以此版本的 .NET Framework 建立的應用程式，這是必要的。
- **ASP.NET MVC 3**。 這會安裝執行 MVC 3 應用程式所需的元件。

> [!NOTE]
> 本逐步解說將說明如何使用 Web Platform Installer 來安裝和設定各種元件。 雖然您不需要使用 Web Platform Installer，但它會自動偵測相依性，並確保您一律取得最新的產品版本，藉此簡化安裝程式。 如需詳細資訊，請參閱 [Microsoft Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。

**若要安裝必要的產品和元件**

1. 下載並安裝 [Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。
2. 安裝完成時，Web Platform Installer 將會自動啟動。

    > [!NOTE]
    > 您現在可以從 [ **開始** ] 功能表啟動 Web Platform Installer。 若要這樣做，請在 [ **開始** ] 功能表上，按一下 [ **所有程式**]，然後按一下 [ **Microsoft Web Platform Installer**]。
3. 在 [Web Platform Installer]**** 視窗的頂端，按一下 [產品]****。
4. 在視窗的左側 **，按一下 [** 流覽] 窗格中的 [架構]。
5. 在 [ **Microsoft .NET Framework 4** ] 資料列中，如果尚未安裝 .NET Framework，請按一下 [ **新增**]。

    > [!NOTE]
    > 您可能已經透過 Windows Update 安裝了 .NET Framework 4.0。 如果已安裝產品或元件，Web Platform Installer 將會以**安裝**的文字取代 [**新增**] 按鈕來指出這一點。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. 在 **ASP.NET MVC 3 (Visual Studio 2010) ** 資料列中，按一下 [ **新增**]。
7. 在流覽窗格中，按一下 [ **伺服器**]。
8. 在 [ **IIS 7 建議** 的設定] 列中，按一下 [ **新增**]。
9. 在 [ **Web 部署工具 2.1** ] 列中，按一下 [ **新增**]。
10. 在 [ **IIS：基本驗證** ] 列中，按一下 [ **新增**]。
11. 在 [ **IIS：管理服務** ] 列中，按一下 [ **新增**]。
12. 按一下 [安裝]。 Web Platform Installer 將會顯示一份產品清單，其中包含要安裝之任何相關聯的相依性&#x2014;&#x2014;，並會提示您接受授權條款。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. 請參閱授權條款，如果您同意條款，請按一下 [ **我接受**]。
14. 當安裝完成時，請按一下 **[完成**]，然後關閉 **Web Platform Installer** 視窗。

如果您在安裝 IIS 之前安裝了 .NET Framework 4.0，則必須執行 [ASP.NET Iis 註冊工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet \_regiis.exe) 向 IIS 註冊最新版本的 ASP.NET。 如果您沒有這麼做，您會發現 IIS 將提供靜態內容 (像是 HTML 檔案) 沒有任何問題，但它會傳回 **HTTP 錯誤404.0 –** 當您嘗試流覽至 ASP.NET 內容時，找不到此錯誤。 您可以使用下一個程式來確定 ASP.NET 4.0 已註冊。

**若要向 IIS 註冊 ASP.NET 4。0**

1. 按一下 [ **開始**]，然後輸入 **命令提示**字元。
2. 在搜尋結果中，以滑鼠右鍵按一下 [ **命令提示**字元]，然後按一下 [以 **系統管理員身分執行**]。
3. 在命令提示字元視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** 目錄。
4. 輸入此命令，然後按 Enter：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. 如果您打算在任何時間點裝載64位的 web 應用程式，您也應該向 IIS 註冊64位版本的 ASP.NET。 若要這樣做，請在命令提示字元視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** 目錄。
6. 輸入此命令，然後按 Enter：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

好的做法是，此時再次使用 Windows Update，以下載並安裝您已安裝之新產品和元件的任何可用更新。

## <a name="configure-the-web-management-service"></a>設定 Web 管理服務

現在您已安裝所需的所有專案，下一步是在 IIS 中設定 Web 管理服務。 概括而言，您必須完成下列工作：

- 在伺服器層級啟用基本驗證。
- 將 Web 管理服務設定為接受遠端連線。
- 啟動 Web 管理服務。
- 檢查必要的 Web 管理服務委派規則是否已就緒。

**設定 Web 管理服務**

1. 在 [ **開始** ] 功能表上，指向 [系統 **管理工具**]，然後按一下 [ **Internet Information Services (IIS) 管理員**。
2. 在 [IIS 管理員] 的 [ **連接** ] 窗格中，按一下 [伺服器] 節點 (例如 **STAGEWEB1**) 。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. 在中央窗格的 [ **IIS**] 底下，按兩下 [ **驗證**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image20.png)
4. 以滑鼠右鍵按一下 [ **基本驗證**]，然後按一下 [ **啟用**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. **在 [連線] 窗格**中，再次按一下伺服器節點，返回最上層設定。
6. 在中央窗格的 [ **管理**] 下，按兩下 [ **管理服務**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. 在中央窗格中，選取 [ **啟用遠端連線**]。

    > [!NOTE]
    > 如果 Web 管理服務已在執行，您必須先將它停止。
8. 在 [ **動作** ] 窗格中，按一下 [ **啟動** ] 以啟動 Web 管理服務。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. 如果系統提示您儲存設定，請按一下 **[是]**。

    > [!NOTE]
    > 您也可能想要將服務設定為自動啟動。 若要這樣做，請開啟 [服務] 主控台，在 [ **Web 管理服務**] 上 **按一下滑鼠**右鍵，然後按一下 [內容]。 在 [ **啟動類型** ] 下拉式清單中，選取 [ **自動**]，然後按一下 **[確定]**。
10. **在 [連線] 窗格**中，再次按一下伺服器節點，返回最上層設定。
11. 在中央窗格的 [ **管理**] 下，按兩下 [ **管理服務委派**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. 確認中央窗格包含一組規則。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    這些規則可讓已授權的 Web 管理服務使用者使用各種 Web Deploy 提供者。 例如，若要透過 Web Deploy 處理常式，將 web 應用程式和內容部署至 IIS，則必須有委派規則，讓所有已驗證的 Web 管理服務使用者使用 **contentPath** 和 **iisApp** 提供者， (您可以在螢幕擷取畫面) 中看到的最後一個規則。

    如果您依照本主題所述的順序安裝產品和元件，最新版本的 Web Deploy 應該會自動將所有必要的委派規則新增至 Web 管理服務。 如果 [管理服務委派] 頁面未顯示任何規則，您必須自行建立。 如需有關如何進行此動作的指示，請參閱 [設定 Web 部署處理常式](https://go.microsoft.com/?linkid=9805124)。
13. **在 [連線] 窗格**中，再次按一下伺服器節點，返回最上層設定。

## <a name="create-and-configure-an-iis-website"></a>建立和設定 IIS 網站

在您可以將 web 內容部署到伺服器之前，您必須先建立並設定 IIS 網站來裝載內容。 Web Deploy 只能將 web 套件部署到現有的 IIS 網站;它無法為您建立網站。 您也需要進行一些額外的設定，以允許您的非系統管理員帳戶從遠端部署內容。 概括而言，您必須完成下列工作：

- 在檔案系統上建立資料夾來裝載您的內容。
- 建立 IIS 網站以提供內容，並將它與本機資料夾產生關聯。
- 將讀取權限授與本機資料夾上的應用程式集區身分識別。
- 將部署 web 應用程式所需的 IIS 許可權授與網域帳戶。

雖然不會阻止您將內容部署至 IIS 中的預設網站，但不建議針對測試或示範情節以外的任何專案使用這種方法。 若要模擬生產環境，您應該建立新的 IIS 網站，其中包含您的應用程式需求特有的設定。

**若要建立 IIS 網站**

1. 在本機檔案系統上建立資料夾，以儲存您的內容 (例如 **C:\DemoSite**) 。
2. 在 [ **開始** ] 功能表上，指向 [系統 **管理工具**]，然後按一下 [ **Internet Information Services (IIS) 管理員**。
3. 在 [IIS 管理員] 的 [ **連接** ] 窗格中，展開伺服器節點 (例如 **STAGEWEB1**) 。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. 以滑鼠右鍵按一下 [ **網站** ] 節點，然後按一下 [ **新增網站**]。
5. 在 [ **網站名稱** ] 方塊中，輸入 IIS 網站的名稱 (例如， **DemoSite**) 。
6. 在 [ **實體路徑** ] 方塊中，輸入 (或流覽以) 本機資料夾的路徑 (例如， **C:\DemoSite**) ]。
7. 在 [ **埠** ] 方塊中，輸入您要用來裝載網站 (的埠號碼，例如 **85**) 。

    > [!NOTE]
    > 適用于 HTTP 的標準埠號碼是80，而 HTTPS 則是443。 但是，如果您在埠80上裝載此網站，您必須先停止預設網站，才能存取您的網站。
8. 將 [ **主機名稱** ] 方塊保留空白，除非您要為網站設定網域名稱系統 (DNS) 記錄，然後按一下 **[確定]**。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > 在生產環境中，您可能會想要在埠80上裝載您的網站，並設定主機標頭和相符的 DNS 記錄。 如需在 IIS 7 中設定主機標頭的詳細資訊，請參閱 [設定網站的主機標頭 (iis 7) ](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。 如需 Windows Server 中的 DNS 伺服器角色的詳細資訊，請參閱 [Dns 伺服器總覽](https://technet.microsoft.com/library/cc770392.aspx) 和 [dns 伺服器](https://technet.microsoft.com/windowsserver/dd448607)。
9. 在 [ **動作** ] 窗格的 [ **編輯站台**] 下方，按一下 [ **繫結**]。
10. 在 [站台繫結]**** 對話方塊中，按一下 [新增]****。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. 在 [ **新增網站** 系結] 對話方塊中，將 [ **IP 位址** ] 和 [ **埠** ] 設定為符合您現有的網站設定。
12. 在 [ **主機名稱** ] 方塊中，輸入您的 web 伺服器名稱 (例如， **STAGEWEB1**) ，然後按一下 **[確定]**。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > 第一個網站系結可讓您使用 IP 位址和埠或，在本機存取網站 `http://localhost:85` 。 第二個網站系結可讓您使用電腦名稱稱從網域上的其他電腦存取網站 (例如， http://stageweb1:85) 。
13. 在 [站台繫結]**** 對話方塊中，按一下 [關閉]****。
14. 在 [連線]**** 窗格中，按一下 [應用程式集區]****。
15. 在 [ **應用程式** 集區] 窗格中，以滑鼠右鍵按一下應用程式集區的名稱，然後按一下 [ **基本設定**]。 根據預設，您的應用程式集區名稱會與您的網站名稱相符 (例如， **DemoSite**) 。
16. 在 [ **.NET clr 版本** ] 清單中，選取 [ **.net Clr v 4.0.30319**]，然後按一下 **[確定]**。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image21.png)

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

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. 在 [ **選取使用者或群組** ] 對話方塊中，輸入 **IIS \_ IUSRS**，按一下 [ **檢查名稱**]，然後按一下 **[確定]**。
6. 在 [ ** (資料夾名稱的許可權) ** ] 對話方塊中，請注意，根據預設，已將 [ **讀取 &amp; 執行**]、[ **列出資料夾內容**] 和 [ **讀取** ] 許可權指派給新群組。 保持不變，然後按一下 **[確定]**。
7. 按一下 **[確定** ]，關閉 ** (資料夾名稱) ** 內容] 對話方塊。

在最後一個工作中，您必須將適當的許可權授與您將用來部署內容的非系統管理員使用者。 此使用者需要許可權，才能從遠端將內容部署至您的網站。

**設定非系統管理員網域使用者的 IIS 網站許可權**

1. 在 [IIS 管理員] 的 [連線] 窗格中，以滑鼠右鍵按一下 **您的網站** 節點 (例如， **DemoSite**) ，指向 [ **部署**]，然後按一下 [ **設定 Web Deploy 發佈**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. 在 [ **設定 Web Deploy 發佈** ] 對話方塊中，于 [ **選取使用者以提供發佈許可權** ] 清單的右邊，按一下省略號按鈕。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. 在 [ **允許使用者** ] 對話方塊中，輸入您要用來部署內容之帳戶的網域和使用者名稱，然後按一下 **[確定]**。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. 在 [ **設定 Web Deploy 發佈** ] 對話方塊中，按一下 [ **安裝**]。

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > 這項作業會在一個步驟中執行兩個主要功能。 首先，它會根據您在上一節中檢查的委派規則，授與使用者透過 Web 管理服務遠端修改網站的許可權。 其次，它會授與使用者對網站源資料夾的完全控制權，讓使用者能夠新增、修改及設定網站內容的許可權。
5. 在 [ **設定 Web Deploy 發佈** ] 對話方塊中，按一下 [ **關閉**]。

## <a name="configure-firewall-exceptions"></a>設定防火牆例外狀況

根據預設，IIS Web 管理服務會接聽 TCP 通訊埠8172。 如果您的 web 伺服器啟用了 Windows 防火牆，您將需要建立新的輸入規則，以允許埠8172上的 TCP 流量 (Windows 防火牆) 預設允許所有輸出流量。 如果您使用協力廠商防火牆，您必須建立規則以允許流量。

| 方向 | 從埠 | 到埠 | 連接埠類型 |
| --- | --- | --- | --- |
| 輸入 | 任意 | 8172 | TCP |
| 輸出 | 8172 | 任意 | TCP |

如需在 Windows 防火牆中設定規則的詳細資訊，請參閱設定 [防火牆規則](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。 如需協力廠商防火牆，請參閱您的產品檔。

## <a name="conclusion"></a>結論

您的網頁伺服器現在應該已經準備好接受透過 Web 管理服務對 Web Deploy 處理常式進行遠端部署。 在您嘗試將 web 應用程式部署到伺服器之前，您可能會想要檢查這些重點：

- 您是否已在 IIS 的伺服器層級上啟用基本驗證？
- 您是否已啟用 Web 管理服務的遠端連線？
- 您是否已啟動 Web 管理服務？
- 是否已有管理服務委派規則？
- 應用程式集區身分識別是否擁有您網站源資料夾的讀取存取權？
- 非系統管理員的使用者帳戶是否有 IIS 中的網站層級許可權？
- 您的防火牆是否允許 TCP 埠8172上的伺服器進行連入連線？

## <a name="further-reading"></a>深入閱讀

如需有關如何設定自訂 Microsoft Build Engine (MSBuild) 專案檔，以將 web 封裝部署至 Web Deploy 處理常式的指引，請參閱 [設定目標環境的部署屬性](configuring-deployment-properties-for-a-target-environment.md)。

> [!div class="step-by-step"]
> [上一個](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) 
> [下一步](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
