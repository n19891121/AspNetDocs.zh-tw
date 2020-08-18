---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
title: 使用 Visual Studio：部署到生產環境的 ASP.NET Web 部署 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何部署 (發佈) ASP.NET web 應用程式，以 Azure App Service Web Apps 或協力廠商主機服務提供者，互動 .。。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 416438a1-3b2f-4d27-bf53-6b76223c33bf
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-production
msc.type: authoredcontent
ms.openlocfilehash: ec025e757d00cbfbfbcda9408739d2593908bc07
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240625"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-production"></a>使用 Visual Studio：部署到生產環境的 ASP.NET Web 部署

由 [Tom Dykstra](https://github.com/tdykstra)

[下載入門專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教學課程系列會說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 (發佈) ASP.NET web 應用程式部署至 Azure App Service Web Apps 或協力廠商主機服務提供者。 如需此系列的詳細資訊，請參閱 [本系列的第一個教學](introduction.md)課程。

## <a name="overview"></a>總覽

在本教學課程中，您會設定 Microsoft Azure 帳戶、建立預備環境和生產環境，並使用 Visual Studio 單鍵發佈功能將 ASP.NET web 應用程式部署到預備環境和生產環境。

如果您想要的話，也可以部署到協力廠商主機服務提供者。 本教學課程中所述的大部分程式都與主機服務提供者或 Azure 相同，不同之處在于每個提供者都有自己的使用者介面來進行帳戶和網站管理。 您可以在 Microsoft.com 網站上的提供者資源 [庫](https://www.microsoft.com/web/hosting) 中找到主機服務提供者。

提醒：如果您在進行本教學課程時收到錯誤訊息或某個內容無法運作，請務必查看此教學課程系列中的 [疑難排解] 頁面。

## <a name="get-a-microsoft-azure-account"></a>取得 Microsoft Azure 帳戶

如果您還沒有 Azure 帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/dotnet/)。

## <a name="create-a-staging-environment"></a>建立預備環境

> [!NOTE]
> 自從撰寫本教學課程之後，Azure App Service 加入了一項新功能，可將許多建立預備環境和生產環境的程式自動化。 請參閱 [在 Azure App Service 中設定 web apps 的預備環境](https://azure.microsoft.com/documentation/articles/web-sites-staged-publishing/)。

如同「 [部署至測試環境」教學](deploying-to-iis.md)課程中所述，最可靠的測試環境是主機服務提供者的網站，就像生產網站一樣。 在許多主機服務提供者中，您必須將此項的優點降低為額外成本，但在 Azure 中，您可以建立額外的免費 web 應用程式作為預備應用程式。 您也需要資料庫，而且在實際執行資料庫中的費用可能會是無或最小量的額外費用。 在 Azure 中，您需支付所使用的資料庫儲存體數量，而不是每個資料庫的費用，而您將在預備環境中使用的額外儲存體量將會降至最低。

如同「 [部署至測試環境」教學](deploying-to-iis.md)課程中所述，在預備和生產環境中，您會將兩個資料庫部署到一個資料庫。 如果您想要將它們分開，程式會相同，不同之處在于您會為每個環境建立額外的資料庫，而且當您建立發行設定檔時，會為每個資料庫選取正確的目的地字串。

在本教學課程的這一節中，您將建立要用於預備環境的 web 應用程式和資料庫，而且您將在建立和部署到生產環境之前，部署至預備環境並在該處進行測試。

> [!NOTE]
> 下列步驟說明如何使用 Azure 入口網站，在 Azure App Service 中建立 web 應用程式。 在最新版的 Azure SDK 中，您也可以使用伺服器總管在不離開 Visual Studio 的情況下進行。 在 Visual Studio 2013 中，您也可以直接從 [發行] 對話方塊中建立 web 應用程式。 如需詳細資訊，請參閱 [在 Azure App Service 中建立 ASP.NET web 應用程式。](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)

1. 在 [Azure 管理入口網站](https://manage.windowsazure.com/)中，按一下 [ **網站**]，然後按一下 [ **新增**]。
2. 按一下 [ **網站**]，然後按一下 [ **自訂建立**]。

    **新的網站-自訂建立**嚮導隨即開啟。 **自訂建立**嚮導可讓您同時建立網站和資料庫。
3. 在嚮導的 [ **建立網站** ] 步驟中，于 [ **URL** ] 方塊中輸入字串，以作為應用程式預備環境的唯一 URL。 例如，輸入 ContosoUniversity-staging123 (包含在結尾的亂數字，以使其成為唯一的，以防 ContosoUniversity 暫存) 。

    完整的 URL 將包含您在此處輸入的字串，加上您在文字方塊旁看到的尾碼。
4. 在 [ **區域** ] 下拉式清單中，選擇最接近您的區域。

    這項設定會指定您的 web 應用程式將在哪一個資料中心執行。
5. 在 [ **資料庫** ] 下拉式清單中，選擇 [ **建立新的 SQL Database**]。
6. 在 [ **DB 連接字串名稱** ] 方塊中，保留預設值 *DefaultConnection*。
7. 按一下指向方塊底部右邊的箭號。

    下圖顯示內含範例值的 [ **建立網站** ] 對話方塊。 您輸入的 URL 和區域將會不同。

    ![建立網站步驟](deploying-to-production/_static/image1.png)

    精靈隨即前進至 [指定資料庫設定] **** 步驟。
8. 在 [ **名稱** ] 方塊中，輸入 *ContosoUniversity* 加上一個亂數字，以使其成為唯一的，例如 *ContosoUniversity123*。
9. 在 [ **伺服器** ] 方塊中，選取 [ **新增 SQL Database 伺服器**]。
10. 輸入系統管理員名稱和密碼。

    您不會在這裡輸入現有的名稱和密碼。 而是輸入新的名稱和密碼；您現在定義的名稱和密碼將供未來存取資料庫時使用。
11. 在 [ **區域** ] 方塊中，選擇您為 web 應用程式選擇的相同區域。

    將網頁伺服器和資料庫伺服器保持在相同區域，可讓您獲得最佳效能，並將費用降至最低。
12. 按一下方塊底部的核取記號，表示您已完成。

    下圖顯示 [ **指定資料庫設定** ] 對話方塊，其中包含範例值。 您輸入的值可能會不同。

    ![新網站的資料庫設定步驟-使用資料庫建立嚮導建立](deploying-to-production/_static/image2.png)

    管理入口網站回到 [網站] 頁面，[ **狀態** ] 欄會顯示正在建立 web 應用程式。 在一段時間後 (通常不到一分鐘的) ，[ **狀態** ] 欄會顯示已成功建立 web 應用程式。 在左側導覽列中，您帳戶中的 web 應用程式數目會出現在 [ **網站** ] 圖示旁，而資料庫數目會出現在 [ **SQL 資料庫** ] 圖示旁。

    ![Web Sites 管理入口網站的網站頁面](deploying-to-production/_static/image3.png)

    您的 web 應用程式名稱將會與圖中的範例應用程式不同。

## <a name="deploy-the-application-to-staging"></a>將應用程式部署至預備環境

現在您已建立預備環境的 web 應用程式和資料庫，您可以將專案部署至該環境。

> [!NOTE]
> 這些指示說明如何藉由下載 *.publishsettings* 檔案來建立發行設定檔，此檔案不僅適用于 Azure，也適用于協力廠商主機服務提供者。 最新的 Azure SDK 也可讓您從 Visual Studio 直接連線到 Azure，並從您的 Azure 帳戶中的 web 應用程式清單中選擇。 在 Visual Studio 2013 中，您可以從 [ **Web 發佈** ] 對話方塊或從 [ **伺服器總管** ] 視窗登入 Azure。 如需詳細資訊，請參閱 [在 Azure App Service 中建立 ASP.NET web 應用程式](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)。

### <a name="download-the-publishsettings-file"></a>下載 .publishsettings 檔案

1. 按一下您剛才建立的 web 應用程式名稱。

    ![按一下網站以移至儀表板](deploying-to-production/_static/image4.png)
2. 在 [**儀表板**] 索引標籤的 [**快速概覽**] 底下，按一下 [**下載發行設定檔**

    ![下載發行設定檔連結](deploying-to-production/_static/image5.png)

    此步驟會下載包含您將應用程式部署至 web 應用程式所需之所有設定的檔案。 您會將此檔案匯入 Visual Studio，因此您不需要手動輸入此資訊。
3. 將 *.publishsettings* 檔案儲存在您可以從 Visual Studio 存取的資料夾中。

    ![儲存 .publishsettings 檔案](deploying-to-production/_static/image6.png)

    > [!WARNING]
    > 安全性- *.publishsettings* 檔案包含您的認證 (未編碼的) ，用來管理您的 Azure 訂用帳戶和服務。 這個檔案的安全性最佳作法是暫時儲存在來源目錄之外 (例如在 Libraries\Documents 資料夾)，然後在匯入完成後予以刪除。 取得 *.publishsettings* 檔案存取權的惡意使用者可以編輯、建立及刪除您的 Azure 服務。

### <a name="create-a-publish-profile"></a>建立發行設定檔

1. 在 Visual Studio 中，以滑鼠右鍵按一下 **方案總管** 中的 ContosoUniversity 專案，然後從內容功能表中選取 [ **發行** ]。

    此時會開啟 [發行 Web] **** 精靈。
2. 按一下 [個人資料]**** 索引標籤。
3. 按一下 [匯入]  。
4. 流覽至您稍早下載的 *.publishsettings* 檔案，然後按一下 [ **開啟**]。

    ![匯入發行設定對話方塊](deploying-to-production/_static/image7.png)
5. 在 [ **連接** ] 索引標籤中，按一下 [ **驗證連接** ]，確認設定正確無誤。

    驗證連接之後，[ **驗證** 連線] 按鈕旁邊會顯示綠色核取記號。

    針對某些主控提供者，當您按一下 [ **驗證連接**] 時，可能會看到 [ **憑證錯誤** ] 對話方塊。 如果您這樣做，請確認伺服器名稱是否符合您的預期。 如果伺服器名稱正確，請選取 [ **儲存此憑證以供 Visual Studio 的未來會話** ]，然後按一下 [ **接受**]。  (此錯誤表示主控提供者已選擇避免針對您要部署的 URL 購買 SSL 憑證。 如果您想要使用有效的憑證來建立安全連線，請洽詢您的主機服務提供者。 ) 
6. 按一下 [下一步]  。

    ![連線索引標籤中的 [連接成功] 圖示和 [下一頁] 按鈕](deploying-to-production/_static/image8.png)
7. 在 [ **設定** ] 索引標籤中，展開 [檔案 **發佈選項**]，然後選取 **[從應用程式 \_ 資料檔案夾中排除**檔案]。

    如需 [檔案 **發行選項**] 下其他選項的詳細資訊，請參閱 [部署至 IIS](deploying-to-iis.md) 教學課程。 顯示此步驟結果和下列資料庫設定步驟的螢幕擷取畫面，位於資料庫設定步驟的結尾。
8. 在 [**資料庫**] 區段的 [ **DefaultConnection** ] 下，為成員資格資料庫設定資料庫部署。
9. 1. 選取 [ **更新資料庫**]。

        緊接在**DefaultConnection**下方的 [**遠端連線字串**] 方塊會填入 .publishsettings 檔案中的連接字串。連接字串包含 SQL Server 的認證，以純文字格式儲存在 *.pubxml*檔案中。 如果您不想將它們永久儲存在該處，您可以在部署資料庫之後，將其從發行設定檔中移除，並將其儲存在 Azure 中。 如需詳細資訊，請參閱 Scott Hanselman 的 blog 上 [從來源部署至 Azure 時，如何確保 ASP.NET 資料庫連接字串的安全性](http://www.hanselman.com/blog/HowToKeepYourASPNETDatabaseConnectionStringsSecureWhenDeployingToAzureFromSource.aspx) 。
      2. 按一下 [ **設定資料庫更新**]。
      3. 在 [ **設定資料庫更新** ] 對話方塊中，按一下 [ **加入 SQL 腳本**]。
      4. 在 [ **加入 SQL 腳本** ] 方塊中，流覽至您稍早在方案資料夾中儲存的 *aspnet-data-prod .sql* 腳本，然後按一下 [ **開啟**]。
      5. 關閉 [ **設定資料庫更新** ] 對話方塊。
10. 在 [**資料庫**] 區段的 [ **SchoolCoNtext** ] 底下，選取 [**執行 Code First 移轉 (在應用程式啟動) 上執行**。

    Visual Studio 會顯示 **執行 Code First 移轉** ，而不是類別的 **更新資料庫** `DbContext` 。 如果您想要使用用於 dbdacfx 提供者（而不是遷移）來部署使用類別存取的資料庫 `DbContext` ，請參閱 MSDN 上 Visual Studio 和 ASP.NET 的 Web 部署常見問題中的 [如何? 部署不含遷移的 Code First 資料庫？](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) 。

    [ **設定** ] 索引標籤現在看起來如下列範例所示：

    ![預備環境的 [設定] 索引標籤](deploying-to-production/_static/image9.png)
11. 請執行下列步驟來儲存設定檔，並將其重新命名為 *預備*環境：

    1. 按一下 [ **設定檔** ] 索引標籤，然後按一下 [ **管理設定檔**]。
    2. 匯入會建立兩個新的設定檔，一個用於 FTP，另一個用於 Web Deploy。 您已設定 Web Deploy 設定檔：將此設定檔重新命名為 *預備*環境。

        ![將設定檔重新命名為預備環境](deploying-to-production/_static/image10.png)
    3. 關閉 [ **編輯 Web 發行設定檔** ] 對話方塊。
    4. 關閉 [ **發行 Web** wizard]。

### <a name="configure-a-publish-profile-transform-for-the-environment-indicator"></a>設定環境指標的發行設定檔轉換

> [!NOTE]
> 本節說明如何設定環境指標的 Web.config 轉換。 因為指標位於專案中，所以您可以在 `<appSettings>` 部署到 Azure App Service 時，有另一個指定轉換的替代方法。 如需詳細資訊，請參閱 [在 Azure 中指定 Web.config 設定](web-config-transformations.md#watransforms)。

1. 在 **方案總管**中，展開 [ **屬性**]，然後展開 [ **PublishProfiles**]。
2. 以滑鼠右鍵按一下 [ *.pubxml*]，然後按一下 [ **新增設定轉換**]。

    ![新增用於暫存的設定轉換](deploying-to-production/_static/image11.png)

    Visual Studio 建立 *Web.Staging.config* 轉換檔案並加以開啟。
3. 在 *Web.Staging.config* 轉換檔中，將下列程式碼插入緊接在開頭 `configuration` 標記之後。

    [!code-xml[Main](deploying-to-production/samples/sample1.xml)]

    當您使用預備發行設定檔時，這種轉換會將環境指標設定為「生產」。 在已部署的 web 應用程式中，您將不會在 "Contoso 大學" H1 標題之後看到任何尾碼，例如 " (Dev) " 或 " (Test) "。
4. 以滑鼠右鍵按一下 *Web.Staging.config* 檔案，然後按一下 [ **預覽轉換** ] 以確定您編碼的轉換會產生預期的變更。

    Web.config 的 [ ** 預覽** ] 視窗會顯示套用 *Web.Release.config* 轉換和 *Web.Staging.config* 轉換的結果。

### <a name="prevent-public-use-of-the-test-app"></a>防止公開使用測試應用程式

預備應用程式的重要考慮是它會存留在網際網路上，但您不想讓公用使用它。 您可以使用下列一種或多種方法，以將人員發現和使用的可能性降至最低：

- 設定防火牆規則，僅允許從您用來測試預備環境的 IP 位址存取暫存應用程式。
- 請使用不可能猜測的模糊 URL。
- 建立 *robots.txt* 檔案，以確保搜尋引擎不會在搜尋結果中將測試應用程式與報表連結進行編目。

這些方法的第一種是最有效的，但不在本教學課程中討論，因為它會要求您部署至 Azure 雲端服務，而不是 Azure App Service。 如需 Azure 中的雲端服務和 IP 限制的詳細資訊，請參閱 [Azure 提供的計算裝載選項](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) ，以及 [封鎖特定 IP 位址，使其無法存取 Web 角色](https://msdn.microsoft.com/library/windowsazure/jj154098.aspx)。 如果您要部署到協力廠商主機服務提供者，請洽詢提供者，以瞭解如何實行 IP 限制。

在本教學課程中，您將建立 *robots.txt* 檔案。

1. 在 **方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [ **加入新專案**]。
2. 建立名為*robots.txt*的新**文字檔**，然後在其中放入下列文字：

    [!code-console[Main](deploying-to-production/samples/sample2.cmd)]

    `User-agent`該行會告知搜尋引擎，檔案中的規則會套用到所有搜尋引擎的 web 編目程式 (機器人) ，而 `Disallow` 這一行會指定網站上的任何頁面都不應進行編目。

    您需要搜尋引擎來為您的生產應用程式進行編目，因此您需要將此檔案從生產環境部署中排除。 若要這樣做，您將在建立生產發行設定檔時，設定其設定。

### <a name="deploy-to-staging"></a>部署至預備環境

1. 以滑鼠右鍵按一下 Contoso 大學專案，然後按一下 [**發佈**]，開啟 [**發佈 Web** ]。
2. 請確定已選取 [ **暫存** 設定檔]。
3. 按一下 [發佈] 。

    [輸出] **** 視窗會顯示已採取的部署動作，並報告部署作業已順利完成。 預設瀏覽器會自動開啟至已部署 web 應用程式的 URL。

## <a name="test-in-the-staging-environment"></a>在預備環境中測試

請注意，環境指示器不存在 (在 H1 標題之後沒有 " (Test) " 或 " (Dev) "，這會顯示環境指標的 *Web.config* 轉換成功。

![首頁預備環境](deploying-to-production/_static/image12.png)

執行 [ **學生** ] 頁面，確認已部署的資料庫沒有任何學生。

執行 **講師** 頁面，確認 Code First 使用講師資料植入資料庫：

選取 [**學生**] 功能表中的 [**加入學生**]、新增學生，然後在 [**學生**] 頁面中查看新的學生，確認您可以成功寫入資料庫。

在 [ **課程** ] 頁面中，按一下 [ **更新點數**]。 [ **更新點數** ] 頁面需要系統管理員許可權，因此會顯示 [ **登入** ] 頁面。 輸入您稍早建立的系統管理員帳號憑證 ( "admin" 和 "prodpwd" ) 。 [ **更新點數** ] 頁面隨即顯示，確認您在上一個教學課程中建立的系統管理員帳戶已正確部署至測試環境。

要求不正確 URL，以產生 ELMAH 將追蹤的錯誤，然後要求 ELMAH 錯誤報表。 如果您要部署到協力廠商主機服務提供者，您可能會發現報表是空的，因為它在上一個教學課程中是空的。 您必須使用主控提供者的帳戶管理工具來設定資料夾許可權，以讓 ELMAH 寫入至記錄資料夾。

您所建立的應用程式現在會在 web 應用程式中于雲端中執行，就像您將用於生產環境的應用程式一樣。 因為一切都能正常運作，下一步是部署到生產環境。

## <a name="deploy-to-production"></a>部署到生產

建立生產 web 應用程式並部署至生產環境的程式與預備環境的程式相同，不同之處在于您需要從部署中排除 *robots.txt* 。 若要這樣做，您要編輯發行設定檔。

### <a name="create-the-production-environment-and-the-production-publish-profile"></a>建立生產環境和生產發行設定檔

1. 遵循您用於預備環境的相同程式，在 Azure 中建立生產環境 web 應用程式和資料庫。

    當您建立資料庫時，您可以選擇將它放在您稍早建立的相同伺服器上，或建立新的伺服器。
2. 下載 *.publishsettings* 檔案。
3. 匯入 *.publishsettings* 檔案以建立發行設定檔，並遵循您用於預備環境的相同程式。

    別忘了在 [**設定**] 索引標籤的 [**資料庫**] 區段中，于 [ **DefaultConnection** ] 下設定資料部署腳本。
4. 將發行設定檔重新命名為 *生產環境*。
5. 設定環境指標的發行設定檔轉換，遵循您用於預備的相同程式。

### <a name="edit-the-pubxml-file-to-exclude-robotstxt"></a>編輯 .pubxml 檔案以排除 robots.txt

發行設定檔的名稱為 &lt; profilename &gt; *.pubxml* ，而且位於*PublishProfiles*資料夾中。 [ *PublishProfiles* ] 資料夾位於 c # web 應用程式專案的 [ *Properties* ] 資料夾底下、VB web 應用程式專案中的 [ *我的專案* ] 資料夾底下，或是在 Web 應用程式專案的 [ *應用程式 \_ 資料* ] 資料夾底下。 每個 *.pubxml* 檔案都包含適用于一個發行設定檔的設定。 您在 [發佈 Web] 中輸入的值會儲存在這些檔案中，您可以編輯這些值，以建立或變更 Visual Studio UI 中未提供的設定。

依預設，當您建立發行設定檔時，專案中會包含 *.pubxml* 檔案，但您可以將它們從專案中排除，Visual Studio 仍會使用這些檔案。 Visual Studio 會在 *.pubxml*檔案的*PublishProfiles*資料夾中尋找，不論專案中是否包含這些檔案。

每個 *.pubxml* 檔案都有 *.pubxml. 使用者* 檔案。 如果您選取了 [**儲存密碼**] 選項， *.pubxml*就會包含加密的密碼，而且根據預設，它會從專案中排除。

*.Pubxml*檔案包含與特定發行設定檔相關的設定。 如果您想要設定適用于所有設定檔的設定，您可以建立一個 *wpp .targets* 檔案。 組建程式會將這些檔案匯入 *.csproj* 或 *vbproj* 專案檔中，因此您可以在專案檔中設定的大部分設定都可以在這些檔案中進行設定。 如需有關 *.Pubxml* 檔案和 *wpp .targets* 檔案的詳細資訊，請參閱 [如何：編輯發行設定檔中的部署設定 (. .Pubxml) 檔和 Visual Studio Web 專案中的 wpp .targets](https://msdn.microsoft.com/library/ff398069.aspx)檔案。

1. 在 **方案總管**中，展開 [ **屬性** ]，然後展開 [ **PublishProfiles**]。
2. 以滑鼠右鍵按一下 [ *.pubxml* ]，然後按一下 [ **開啟**]。

    ![開啟 .pubxml 檔案](deploying-to-production/_static/image13.png)
3. 以滑鼠右鍵按一下 [ *.pubxml* ]，然後按一下 [ **開啟**]。
4. 緊接在結尾元素之前加入下列幾行 `PropertyGroup` ：

    [!code-xml[Main](deploying-to-production/samples/sample3.xml)]

    .Pubxml 檔案現在看起來類似下列範例：

    [!code-xml[Main](deploying-to-production/samples/sample4.xml?highlight=18-20)]

    如需有關如何排除檔案和資料夾的詳細資訊，請參閱 MSDN 上的**Visual Studio 和 ASP.NET 的 Web 部署常見問題**中的「[我可以從部署中排除特定檔案或資料夾嗎？](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment) 」。

### <a name="deploy-to-production"></a>部署到生產

1. 開啟 [**發佈 Web** ] 嚮導，確認已選取 [**生產**發行設定檔]，然後按一下 [**預覽**] 索引標籤上的 [**開始預覽**]，以確認*robots.txt*檔案不會複製到生產應用程式。

    ![要發行至生產環境的檔預覽](deploying-to-production/_static/image14.png)

    檢查將複製的檔案清單。 您會看到所有的 *.cs* 檔案，包括 *aspx.cs*、 *. aspx.designer.cs*、 *Master.cs*和 *Master.designer.cs* 檔案。 此程式碼的所有程式碼都已編譯成*ContosoUniversity.dll* ，並 ContosoUniversity 您將在*bin*資料夾中找到的 *.pdb*檔。 因為只需要 *.dll* 來執行應用程式，而且您先前指定只有執行應用程式所需的檔案才會進行部署，所以不會將 *.cs* 檔案複製到目的地環境。 *Obj*資料夾和*ContosoUniversity .csproj*和 *.csproj. 使用者*檔案會因相同原因而省略。

    按一下 [ **發佈** ] 以部署至生產環境。
2. 在生產環境中測試，遵循您用於預備的相同程式。

    除了 URL 和缺少 *robots.txt* 檔案之外，所有專案都與預備環境相同。

## <a name="summary"></a>摘要

您現在已成功部署並測試您的 web 應用程式，並可透過網際網路公開使用。

![首頁生產](deploying-to-production/_static/image15.png)

在下一個教學課程中，您將更新應用程式程式碼，並將變更部署到測試、預備和生產環境。

> [!NOTE]
> 當您的應用程式在生產環境中使用時，您應該執行復原方案。 也就是說，您應該定期將資料庫從生產環境應用程式備份到安全的儲存位置，而且您應該保留數個這類備份的層代。 當您更新資料庫時，您應該在變更前立即建立備份複本。 然後，如果您在將它部署到生產環境之後不會發現錯誤，您仍然可以將資料庫復原到它損毀之前的狀態。 如需詳細資訊，請參閱 [Azure SQL Database 備份和還原](https://msdn.microsoft.com/library/windowsazure/jj650016.aspx)。
> 
> 
> [!NOTE]
> 在本教學課程中，您要部署的 SQL Server 版本 Azure SQL Database。 雖然部署程式與其他版本的 SQL Server 很類似，但實際的生產環境應用程式在某些情況下可能需要特殊的程式碼才能 Azure SQL Database。 如需詳細資訊，請參閱 [使用 Azure SQL Database](../../../../whitepapers/aspnet-data-access-content-map.md#ssdb) 以及 [在 SQL Server 和 Azure SQL Database 之間進行選擇](../../../../whitepapers/aspnet-data-access-content-map.md#ssdbchoosing)。
> 
> [!div class="step-by-step"]
> [上一個](setting-folder-permissions.md) 
> [下一步](deploying-a-code-update.md)
