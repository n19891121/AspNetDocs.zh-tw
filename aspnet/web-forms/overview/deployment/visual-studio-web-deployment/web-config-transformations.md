---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 使用 Visual Studio 的 ASP.NET Web 部署： Web.config 檔轉換 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何部署 (發佈) ASP.NET web 應用程式，以 Azure App Service Web Apps 或協力廠商主機服務提供者，互動 .。。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345607"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>使用 Visual Studio 的 ASP.NET Web 部署： Web.config 檔轉換

由 [Tom Dykstra](https://github.com/tdykstra)

[下載入門專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教學課程系列會說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 (發佈) ASP.NET web 應用程式部署至 Azure App Service Web Apps 或協力廠商主機服務提供者。 如需此系列的詳細資訊，請參閱 [本系列的第一個教學](introduction.md)課程。

## <a name="overview"></a>概觀

本教學課程會示範如何在將 *Web.config* 檔案部署至不同的目的地環境時，自動進行變更。 大部分的應用程式都有 *Web.config* 檔案中的設定，在部署應用程式時必須不同。 將進行這些變更的程式自動化，讓您不必在每次部署時手動執行這些變更，這會很繁瑣且容易出錯。

提醒：如果您在進行本教學課程時收到錯誤訊息或某個內容無法運作，請務必檢查 [ [疑難排解] 頁面](troubleshooting.md)。

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config 轉換與 Web Deploy 參數的比較

有兩種方式可將變更 *Web.config* 檔設定的程式自動化： [Web.config 轉換](https://msdn.microsoft.com/library/dd465326.aspx) 和 [Web Deploy 參數](https://msdn.microsoft.com/library/ff398068.aspx)。 *Web.config*的轉換檔案包含 XML 標記，可指定如何在部署*Web.config*檔案時加以變更。 您可以針對特定組建設定和特定發行設定檔指定不同的變更。 預設組建設定為 Debug 和 Release，您可以建立自訂群組建設定。 發行設定檔通常會對應至目的地環境。  (您將會在 [部署至 IIS 作為測試環境](deploying-to-iis.md) 教學課程中，深入瞭解發佈設定檔。 ) 

Web Deploy 參數可以用來指定部署期間必須設定的許多不同類型的設定，包括在 *Web.config* 檔中找到的設定。 當用來指定 *Web.config* 檔變更時，Web Deploy 參數的設定比較複雜，但是當您在部署之前不知道要設定的值時，這些參數就很有用。 例如，在企業環境中，您可以建立 *部署套件* ，並將它提供給 it 部門中的人員，以便安裝在生產環境中，而且該人員必須能夠輸入您不知道的連接字串或密碼。

在本教學課程系列所涵蓋的案例中，您事先知道必須在 *Web.config* 檔案中完成的所有動作，因此您不需要使用 Web Deploy 參數。 您將會根據所使用的組建設定，設定不同的轉換，而有些則會根據所使用的發行設定檔而有所不同。

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>在 Azure 中指定 Web.config 設定

如果您要變更的 *Web.config* 檔案設定位於或專案中 `<connectionStrings>` `<appSettings>` ，而且如果您要部署至 Azure App Service 中的 Web Apps，您可以選擇在部署期間自動執行變更。 您可以在 web 應用程式的 [入口網站] 頁面的 [ **設定** ] 索引標籤中，輸入您想要在 Azure 中生效的設定 (向下) 的 [ **應用程式設定** ] 和 [ **連接字串** ] 區段。 當您部署專案時，Azure 會自動套用變更。 如需詳細資訊，請參閱 [Windows Azure 網站：應用程式字串與連接字串的運作方式](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。

## <a name="default-transformation-files"></a>預設轉換檔案

在 **方案總管**中，展開 [ *Web.config* ] 以查看預設為兩個預設組建設定所建立的 *Web.Debug.config* 和 *Web.Release.config* 轉換檔案。

![Web.config_transform_files](web-config-transformations/_static/image1.png)

您可以建立自訂群組建設定的轉換檔案，方法是以滑鼠右鍵按一下 Web.config 檔案，然後從操作功能表中選擇 [ **加入設定轉換** ]。 在本教學課程中，您不需要這樣做，而且功能表選項已停用，因為您尚未建立任何自訂群組建設定。

稍後，您將會建立三個轉換檔案，每個檔案分別用於測試、預備和生產發行設定檔。 您將在發行設定檔轉換檔案中處理的一般設定範例，是因為它相依于目的地環境是不同于測試與生產環境的 WCF 端點。 建立發行設定檔之後，您將在稍後的教學課程中建立發行設定檔轉換檔案。

## <a name="disable-debug-mode"></a>停用 debug 模式

相依于組建設定而非目的地環境的設定範例為 `debug` 屬性。 針對發行組建，您通常會想要讓偵錯工具停用，不論您要部署到哪個環境。 因此，Visual Studio 專案範本預設會建立 *Web.Release.config* 的轉換檔案，其中包含可從專案中移除屬性的程式碼 `debug` `compilation` 。 以下是預設 *Web.Release.config*：除了批註化的一些範例轉換程式碼之外，它還會在移除屬性的元素中包含程式碼 `compilation` `debug` ：

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

`xdt:Transform="RemoveAttributes(debug)"`屬性（attribute）會指定您想要 `debug` 從已部署之 `system.web/compilation` *Web.config*檔中的專案移除屬性（attribute）。 這將會在您每次部署發行組建時完成。

## <a name="limit-error-log-access-to-administrators"></a>限制系統管理員存取錯誤記錄檔

如果應用程式執行時發生錯誤，應用程式會顯示一般錯誤頁面取代系統產生的錯誤頁面，並使用 [Elmah NuGet 套件](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) 進行錯誤記錄和報告。 `customErrors`應用程式*Web.config*檔中的元素會指定錯誤頁面：

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

若要查看錯誤頁面，請暫時將 `mode` 元素的屬性 `customErrors` 從 "RemoteOnly" 變更為 "On"，然後從 Visual Studio 執行應用程式。 要求不正確 URL （例如 *Studentsxxx*），以產生錯誤。 您會看到 *GenericErrorPage .aspx* 頁面，而不是 IIS 產生的「找不到資源」錯誤頁面。

![錯誤頁面](web-config-transformations/_static/image2.png)

若要查看錯誤記錄檔，請將 URL 中的所有內容取代為 *elmah. axd* (例如， `http://localhost:51130/elmah.axd`) ，然後按 enter：

![ELMAH 頁面](web-config-transformations/_static/image3.png)

當您完成時，別忘了將 `customErrors` 元素設回「RemoteOnly」模式。

在您的開發電腦上，您可以輕鬆地存取錯誤記錄頁面，但在生產環境中會有安全性風險。 針對生產網站，您想要新增授權規則，以限制對系統管理員的錯誤記錄檔存取，並確保您在測試和預備環境中所需的限制也可以運作。 因此，這是您在每次部署發行組建時要執行的另一項變更，因此它屬於 *Web.Release.config* 檔。

開啟 *Web.Release.config* ，並在 `location` 結束記號之前加入新元素 `configuration` ，如下所示。

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

`Transform`"Insert" 的屬性值會將這個專案 `location` 加入為Web.config檔中任何現有元素的同級 `location` 。 *Web.config*  (已有一個 `location` 元素指定 [ **更新信用額度** ] 頁面的授權規則。 ) 

現在您可以預覽轉換，以確定您的程式碼正確。

在 **方案總管**中，以滑鼠右鍵按一下 *Web.Release.config* ，然後按一下 [ **預覽轉換**]。

![預覽轉換功能表](web-config-transformations/_static/image4.png)

隨即開啟頁面，顯示左側的開發 *Web.config* 檔案，以及已部署的 *Web.config* 檔案在右側顯示的樣子，並醒目提示變更。

![Debug 轉換的預覽](web-config-transformations/_static/image5.png)

![位置轉換預覽](web-config-transformations/_static/image6.png)

 ( 在預覽版本中，您可能會注意到一些您未寫入轉換的其他變更：這些變更通常包含移除不影響功能的空白字元。 ) 

當您在部署後測試網站時，也會進行測試以驗證授權規則是否有效。

> [!NOTE] 
> 
> **安全性注意事項** 絕對不要在實際執行應用程式中顯示公用的錯誤詳細資料，或將該資訊儲存在公用位置。 攻擊者可以使用錯誤資訊來探索網站中的弱點。 如果您在自己的應用程式中使用 ELMAH，請設定 ELMAH 以將安全性風險降至最低。 本教學課程中的 ELMAH 範例不應視為建議的設定。 這是為了說明如何處理應用程式必須能夠在其中建立檔案的資料夾所選的範例。 如需詳細資訊，請參閱 [保護 ELMAH 端點的安全](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)。

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>您將在發佈設定檔轉換檔案中處理的設定

常見的案例是在您部署至的每個環境中都有必須不同的 *Web.config* 檔案設定。 例如，呼叫 WCF 服務的應用程式在測試和生產環境中可能需要不同的端點。 Contoso 大學應用程式也包含這種類型的設定。 這項設定會控制網站頁面上的可見指標，告訴您所使用的環境，例如開發、測試或生產環境。 設定值會決定應用程式是否要將 " (Dev) " 或 " (Test) " 附加至 *網站* 主版頁面中的主要標題：

![環境指標](web-config-transformations/_static/image7.png)

當應用程式在預備環境或生產環境中執行時，會省略環境指標。

Contoso 大學網頁會讀取Web.config檔案中所設定的值， `appSettings` 以*Web.config*判斷應用程式執行所在的環境：

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

在測試環境中，此值應該是「測試」，而「生產」是用於預備和生產環境。

轉換檔案中的下列程式碼將會執行此轉換：

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

`xdt:Transform`屬性值 "SetAttributes" 表示此轉換的目的是要變更*Web.config*檔案中現有元素的屬性值。 `xdt:Locator`屬性值「符合 (索引鍵) 」表示要修改的元素是其 `key` 屬性符合 `key` 此處所指定之屬性的專案。 專案的唯一其他屬性 `add` 是 `value` ，而這也是要在已部署的 *Web.config* 檔案中變更的屬性。 此處顯示的程式碼會在部署的Web.config檔案中，將專案的 `value` 屬性 `Environment` `appSettings` 設定為*Web.config* "Test"。

這項轉換屬於您尚未建立的發行設定檔轉換檔案。 當您建立測試、預備和生產環境的發行設定檔時，您將會建立並更新執行這種變更的轉換檔案。 您將在「 [部署至 IIS](deploying-to-iis.md) 」中執行此作業，並 [部署至生產](deploying-to-production.md) 教學課程。

> [!NOTE]
> 因為此設定位於專案中 `<appSettings>` ，所以當您在中部署至 Web Apps 時，您可以使用另一個替代方式來指定轉換 Azure App Service 請參閱本主題稍早在 [Azure 中指定 Web.config 設定](#watransforms) 。

## <a name="setting-connection-strings"></a>設定連接字串

雖然預設轉換檔包含的範例會示範如何更新連接字串，但在大部分情況下，您不需要設定連接字串轉換，因為您可以在發行設定檔中指定連接字串。 您將在「 [部署至 IIS](deploying-to-iis.md) 」中執行此作業，並 [部署至生產](deploying-to-production.md) 教學課程。

## <a name="summary"></a>摘要

您現在可以在建立發行設定檔之前，以 *Web.config* 轉換的方式完成，而且您已瞭解所部署的 Web.config 檔案中將會有哪些內容的預覽。

![位置轉換預覽](web-config-transformations/_static/image8.png)

在下列教學課程中，您將負責需要設定專案屬性的部署設定工作。

## <a name="more-information"></a>相關資訊

如需本教學課程所涵蓋之主題的詳細資訊，請參閱 [使用 Web.config 轉換來變更目的地 Web.config 檔案中的設定，或在部署期間](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) 于 Visual Studio 和 ASP.NET 的 Web 部署內容對應中 app.config 檔案。

> [!div class="step-by-step"]
> [上一個](preparing-databases.md) 
> [下一步](project-properties.md)
