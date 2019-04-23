---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
title: 設定 Web 伺服器的 Web Deploy 發行 （遠端代理程式） |Microsoft Docs
author: jrjlee
description: 本主題描述如何設定 Internet Information Services (IIS) web 伺服器以支援網頁發佈和使用 IIS Web 部署的部署...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 239c7aa8-d09a-4d02-9c0e-6bd52be5f0d5
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
msc.type: authoredcontent
ms.openlocfilehash: d915cb5d7d40bb2cc355a5e45befe124a7b60dc4
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59398484"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-remote-agent"></a>設定 Web Deploy 發行的網頁伺服器 (遠端代理程式)

藉由[Jason Lee](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何設定 Internet Information Services (IIS) web 伺服器以支援網頁發佈和使用 IIS Web Deployment Tool (Web Deploy) 的遠端代理程式服務的部署。
> 
> 當您使用 Web Deploy 2.0 或更新版本時，有三種主要的方法，可用來取得您的應用程式或 web 伺服器上的站台。 您可以：
> 
> - 使用*Web Deploy 遠端代理程式服務*。 此方法需要較少組態的 web 伺服器，但您必須提供本機伺服器系統管理員的認證，以將任何項目部署至伺服器。
> - 使用*Web Deploy 處理常式*。 這種方法更多複雜，而且需要更多的初步設定 web 伺服器。 不過，當您使用這個方法時，您可以設定 IIS 以允許非系統管理員使用者，進行部署。 只有在 IIS 7 或更新版本中使用 Web 部署處理常式。
> - 使用*離線部署*。 這種方法需要最低的網頁伺服器的設定，但伺服器系統管理員必須手動複製到伺服器上的 web 套件並匯入它透過 IIS 管理員。
> 
> 如需有關的主要功能、 優點和這些方法的缺點的詳細資訊，請參閱[選擇 Web 部署的權限方法](choosing-the-right-approach-to-web-deployment.md)。


## <a name="is-the-web-deploy-remote-agent-the-right-approach-for-you"></a>是 Web 部署為您的遠端代理程式正確的方法？

是，如果將部署內容的使用者可以提供的目的地伺服器上的系統管理員認證。 這種方法通常會希望出現在這種情況下：

- 開發或測試環境，其中的開發人員都有在目的地 web 伺服器和資料庫伺服器的完整控制權。
- 較小的組織，單一使用者或一小群使用者具有整個應用程式生命週期的控制權。

在許多大型組織，以及特別是針對預備環境或生產環境，它往往是不切實際，讓使用者在網頁伺服器上的系統管理員權限。 在裝載的 web 伺服器的情況下這是特別是不太可能發生此情況。 此外，如果您打算從組建伺服器的部署作業自動化，您可能不想要用於部署程序中的系統管理員認證。 在這些情況下，設定您的 web 伺服器，以支援使用部署[Web 部署的處理常式](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)可能會提供更令人滿意的選擇。

## <a name="task-overview"></a>工作概觀

本主題描述如何設定 Internet Information Services (IIS) 7.5 web 伺服器接受並部署 web 封裝，從遠端電腦使用網路部署遠端代理程式的方法。 您必須：

- 安裝 IIS 7.5 和 IIS 7 建議組態。
- 安裝 Web Deploy 2.1 或更新版本。
- 建立 IIS 網站來裝載部署的內容。
- 確定 Web Deployment Agent Service 正在執行。

若要特別裝載範例方案，您還需要以：

- 安裝.NET Framework 4.0。
- 安裝 ASP.NET MVC 3。

本主題將說明如何執行上述各程序。 工作與本主題中的逐步解說假設您從執行 Windows Server 2008 R2 的全新的伺服器組建。 在繼續之前，請確認：

- 安裝 Windows Server 2008 R2 Service Pack 1 和所有可用的更新。
- 伺服器已加入網域。
- 伺服器具有靜態 IP 位址。

> [!NOTE]
> 如需有關如何將電腦加入網域的詳細資訊，請參閱 <<c0> [ 將電腦加入網域並登入](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)。 如需有關如何設定靜態 IP 位址的詳細資訊，請參閱 <<c0> [ 設定靜態 IP 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。 遠端代理程式服務及更新版本支援的 IIS 6，並不需要加入網域。 不過，在本教學課程的步驟已開發及測試在 IIS 7.5 上，針對其他版本的程序可能會不同。


## <a name="install-products-and-components"></a>安裝的產品和元件

本節將引導您完成 web 伺服器上安裝必要的產品和元件。 在開始之前，理想的作法就是執行 Windows Update，以確保您的伺服器已完全更新。

在此情況下，您需要安裝這些項目：

- **IIS 7 建議組態**。 這可讓**網頁伺服器 (IIS)** web 伺服器上的角色，並安裝的一組 IIS 模組和元件，您需要以裝載 ASP.NET 應用程式。
- **.NET framework 4.0**。 如此才能執行這個版本的.NET Framework 所建置的應用程式。
- **Web Deployment Tool 2.1 或更新版本**。 這會在您的伺服器上安裝 Web Deploy （和其基礎可執行檔，MSDeploy.exe）。 此程序的一部分，它將會安裝並啟動 Web 部署代理程式服務。 這項服務可讓您從遠端電腦的 web 套件部署。
- **ASP.NET MVC 3**。 這會安裝您要執行 MVC 3 應用程式的組件。

> [!NOTE]
> 本逐步解說說明如何使用 Web Platform Installer 來安裝和設定必要的元件。 雖然您不需要使用 Web Platform Installer，它可以簡化安裝程序自動偵測相依性，並確保您一律取得最新的產品版本。 如需詳細資訊，請參閱 < [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118)。


**若要安裝必要的產品和元件**

1. 下載並安裝[Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。
2. 安裝完成時，Web Platform Installer 將會自動啟動。

    > [!NOTE]
    > 您現在可以隨時從啟動 Web Platform Installer**啟動**功能表。 若要這樣做，請在**開始**功能表上，按一下**所有程式**，然後按一下**Microsoft Web Platform Installer**。
3. 在頂端**Web Platform Installer 3.0**  視窗中，按一下**產品**。
4. 在左邊視窗中，在導覽窗格中，按一下 **架構**。
5. 在  **Microsoft.NET Framework 4**資料列，如果尚未安裝.NET Framework，按一下**新增**。

    > [!NOTE]
    > 您可能已經安裝.NET Framework 4.0，透過 Windows Update。 如果已安裝的產品或元件，Web Platform Installer 會指出這藉由取代**新增**按鈕，但文字**已安裝**。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image1.png)
6. 在  **ASP.NET MVC 3 (Visual Studio 2010)** 資料列中，按一下**新增**。
7. 在 [導覽] 窗格中，按一下**Server**。
8. 在  **IIS 7 建議組態**資料列中，按一下**新增**。
9. 在  **Web 部署工具 2.1**資料列中，按一下**新增**。
10. 按一下 [安裝] 。 Web Platform Installer 將會顯示您的產品清單&#x2014;以及任何相關聯相依性&#x2014;安裝就會提示您接受授權條款。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image2.png)
11. 檢閱授權條款，然後如果您同意這些條款，按一下**我接受**。
12. 安裝完成時，按一下**完成**，然後關閉**Web Platform Installer 3.0**視窗。

如果您安裝 IIS 之前，您就會安裝.NET Framework 4.0，您必須執行[ASP.NET IIS 註冊工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx)(aspnet\_regiis.exe) 向 IIS 註冊 ASP.NET 的最新版本。 如果沒有這麼做，您會發現，IIS 會提供靜態內容 （例如 HTML 檔案） 沒有任何問題，但它會傳回**HTTP 錯誤 404.0 – 找不到**當您嘗試瀏覽至 ASP.NET 內容。 您可以使用此程序，以確保已註冊 ASP.NET 4.0。

**若要向 IIS 註冊 ASP.NET 4.0**

1. 按一下 **開始**，然後輸入**命令提示字元**。
2. 在搜尋結果中，以滑鼠右鍵按一下**命令提示字元**，然後按一下**系統管理員身分執行**。
3. 在 [命令提示字元] 視窗中，瀏覽至 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319**目錄。
4. 輸入下列命令，並再按 Enter 鍵：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample1.cmd)]
5. 如果您打算裝載在任何時間點的 64 位元 web 應用程式時，則您也應該向 IIS 註冊 ASP.NET 的 64 位元版本。 若要這樣做，請在 [命令提示字元] 視窗中，巡覽至 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319**目錄。
6. 輸入下列命令，並再按 Enter 鍵：

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample2.cmd)]

好的做法是，使用 Windows Update 一次此時下載並安裝任何可用的更新，新的產品及您已安裝的元件。

## <a name="configure-the-iis-website"></a>設定 IIS 網站

您可以將 web 內容部署到您的伺服器之前，您需要建立及設定 IIS 網站來裝載內容。 Web Deploy 只可以將 web 套件部署至現有的 IIS 網站;它不能為您建立網站。 概括而言，您將需要完成下列工作：

- 若要將內容裝載在檔案系統上建立資料夾。
- 建立 IIS 網站提供內容，並將它關聯的本機資料夾。
- 授與讀取權限的本機資料夾上的應用程式集區識別。

雖然沒有任何阻礙您將內容部署到預設的網站在 IIS 中，這種方法不會建議針對測試或示範的案例以外的任何項目。 若要模擬生產環境中，您應該建立新的 IIS 網站設定專屬於您的應用程式的需求。

**若要建立及設定 IIS 網站**

1. 在本機檔案系統上，建立資料夾來儲存您的內容 (例如**C:\DemoSite**)。
2. 在上**開始**功能表上，指向**系統管理工具**，然後按一下**Internet Information Services (IIS) 管理員**。
3. 在 [IIS 管理員] 中，在**連線**窗格中，展開伺服器節點 (例如**TESTWEB1**)。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image3.png)
4. 以滑鼠右鍵按一下**站台**節點，然後再按一下**新增網站**。
5. 在 **站台名稱**方塊中，輸入 IIS 網站的名稱 (例如**DemoSite**)。
6. 在**實體路徑**方塊中，輸入 （或瀏覽至） 您的本機資料夾的路徑 (例如**C:\DemoSite**)。
7. 在 **連接埠**方塊中，輸入您要裝載網站的連接埠號碼 (例如**85**)。

    > [!NOTE]
    > 標準連接埠號碼是 80 用於 HTTP 和 HTTPS 為 443。 不過，如果您主控此連接埠 80 上的網站，您必須停止預設網站，才能存取您的網站。
8. 離開**主機名稱**空白，除非您想要設定之網站中，網域名稱系統 (DNS) 記錄，然後按一下方塊**確定**。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image4.png)

    > [!NOTE]
    > 在生產環境中，您可能會想要裝載您的網站連接埠 80 上，並設定主機標頭，以及比對 DNS 記錄。 如需有關如何在 IIS 7 中設定主機標頭的詳細資訊，請參閱 <<c0> [ 網站 (IIS 7) 中設定主機標頭](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。 如需有關 Windows Server 2008 R2 中 DNS 伺服器角色的詳細資訊，請參閱 < [DNS 伺服器概觀](https://technet.microsoft.com/en-gb/library/cc770392.aspx)並[DNS 伺服器](https://technet.microsoft.com/windowsserver/dd448607)。
9. 在 [ **動作** ] 窗格的 [ **編輯站台**] 下方，按一下 [ **繫結**]。
10. 在 [**站台繫結**] 對話方塊中，按一下**新增**。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image5.png)
11. 在**新增網站繫結** 對話方塊中，將**IP 位址**並**連接埠**以符合您現有的站台設定。
12. 中**主機名稱**方塊中，輸入您的 web 伺服器的名稱 (例如**TESTWEB1**)，然後按一下 **確定**。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image6.png)

    > [!NOTE]
    > 第一個站台繫結可讓您存取使用的 IP 位址和連接埠，在本機站台或 `http://localhost:85` 。 第二個網站繫結可讓您從使用電腦名稱在網域上其他電腦存取站台 (例如 http://testweb1:85) 。
13. 在 [**站台繫結**] 對話方塊中，按一下**關閉**。
14. 在 **連線**窗格中，按一下**應用程式集區**。
15. 在 **應用程式集區**窗格中，以滑鼠右鍵按一下您的應用程式集區的名稱，然後按一下**基本設定**。 根據預設，應用程式集區的名稱會符合您網站的名稱 (例如**DemoSite**)。
16. 在  **.NET Framework 版本**清單中，選取 **.NET Framework v4.0.30319**，然後按一下**確定**。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image7.png)

    > [!NOTE]
    > 範例解決方案需要.NET Framework 4.0。 這不是 Web Deploy 的需求在一般情況下。

為了讓您的網站提供內容，應用程式集區識別必須擁有讀取權限儲存內容的本機資料夾。 在 IIS 7.5 中應用程式集區執行具有唯一的應用程式集區身分識別 （相較於舊版的 IIS，其中應用程式集區會通常執行使用 Network Service 帳戶） 的預設值。 應用程式集區識別不是真正的使用者帳戶，以及未顯示任何使用者或群組的清單上&#x2014;相反地，它會動態建立啟動應用程式集區時。 每個應用程式集區身分識別加入至本機**IIS\_IUSRS**安全性群組做為隱藏的項目。

若要授與權限到檔案或資料夾上的應用程式集區身分識別，您會有兩個選項：

- 指派的權限的應用程式集區識別，直接使用的格式<strong>IIS AppPool\</ s t ><em>[應用程式集區名稱]</em>(比方說， <strong>IIS AppPool\DemoSite</strong>).
- 指派權限**IIS\_IUSRS**群組。

最常見的方法是將權限指派給本機**IIS\_IUSRS**群組，因為此方法可讓您變更應用程式集區，不需要重新設定檔案系統權限。 下一個程序會使用此群組為基礎的方法。

> [!NOTE]
> 如需有關在 IIS 7.5 中的應用程式集區身分識別的詳細資訊，請參閱[應用程式集區識別](https://go.microsoft.com/?linkid=9805123)。


**若要設定 IIS 網站的資料夾權限**

1. 在 Windows 檔案總管中，瀏覽至您本機資料夾的位置。
2. 以滑鼠右鍵按一下資料夾，然後按一下**屬性**。
3. 在上**安全性**索引標籤上，按一下**編輯**，然後按一下**新增**。
4. 按一下 **位置**。 在 **位置** 對話方塊中，選取 本機伺服器，然後按一下**確定**。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image8.png)
5. 中**選取使用者或群組** 對話方塊中，輸入**IIS\_IUSRS**，按一下**檢查名稱**，然後按一下**確定**。
6. 在 <strong>權限</strong><em>[資料夾名稱]</em>對話方塊中，請注意，已被指派新的群組<strong>讀取&amp;執行</strong>，<strong>列出資料夾內容</strong>，並<strong>讀取</strong>預設的權限。 保留不變，然後按一下 <strong>確定</strong>。
7. 按一下 [ <strong>[確定]</strong>以關閉<em>[資料夾名稱]</em><strong>屬性</strong>] 對話方塊。

為最後一項工作您嘗試將任何 web 套件部署到您的伺服器之前, 您應該確定 Web Deployment Agent Service 正在執行。 當您部署封裝，以從遠端電腦時，Web Deployment Agent Service 負責擷取和安裝封裝的內容。 當您安裝 Web Deployment Tool 時，會預設為啟動服務，並會在 Network Service 身分識別下執行。

您可以檢查服務是否正在執行多個不同的方式，使用各種命令列公用程式或 Windows PowerShell cmdlet。 此程序描述直接以 UI 為基礎的方法。

**若要檢查 Web Deployment Agent Service 正在執行**

1. 在 [開始]  功能表上，指向 [系統管理工具] ，然後按一下 [服務] 。
2. 找出**Web Deployment Agent Service**資料列，並確認**狀態**設定為**Started**。

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image9.png)
3. 如果服務尚未啟動，請按一下**啟動**。

## <a name="configure-firewall-exceptions"></a>設定防火牆例外

根據預設，遠端代理程式服務會接聽 TCP 連接埠 80，在此 URL:

<http://servername.com/MSDEPLOYAGENTSERVICE>

在大部分情況下，您不需要任何額外的防火牆規則設定為遠端代理程式服務，因為網頁伺服器通常會接聽連接埠 80 上的 HTTP 要求。 如果您自訂您的安裝以非標準連接埠上接聽，您必須視需要設定防火牆例外狀況。

## <a name="conclusion"></a>結論

此時，您的 web 伺服器已準備好接受與安裝網頁套件從遠端電腦。 您嘗試部署 web 應用程式到伺服器之前，您可能想要檢查的這些關鍵點：

- 您已向 IIS 註冊 ASP.NET 4.0？
- 應用程式集區識別是否有讀取權限為您的網站的 [來源] 資料夾？
- Web Deployment Agent Service 正在執行？

## <a name="further-reading"></a>進一步閱讀

如需如何設定自訂的 Microsoft Build Engine (MSBuild) 專案檔，以將 web 套件部署至遠端代理程式服務的指引，請參閱 <<c0> [ 設定目標環境的部署屬性](configuring-deployment-properties-for-a-target-environment.md)。

> [!div class="step-by-step"]
> [上一頁](scenario-configuring-a-production-environment-for-web-deployment.md)
> [下一頁](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
