---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 使用視覺化工作室ASP.NET Web 部署:Web.config 檔案轉換 |微軟文件
author: tdykstra
description: 本教學系列介紹如何將ASP.NET Web 應用程式部署到 Azure 應用服務 Web 應用或第三方託管供應商(由 usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676122"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>使用視覺化工作室ASP.NET Web 部署:Web.config 檔案轉換

湯姆[·戴克斯特拉](https://github.com/tdykstra)

[下載初學者專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教學系列介紹如何使用 Visual Studio 2012 或 Visual Studio 2010 將ASP.NET Web 應用程式部署到 Azure 應用服務 Web 應用或第三方託管供應商。 有關該系列的資訊,請參閱[系列中的第一個教程](introduction.md)。

## <a name="overview"></a>概觀

本教學介紹如何在將*Web.config 檔部署到*不同目標環境時自動執行更改 Web.config 檔的過程。 大多數應用程式在*Web.config 檔中*具有設置,在部署應用程式時必須不同。 自動進行這些更改的過程使每次部署時都不必手動執行這些更改,這非常繁瑣且容易出錯。

鬧鐘:如果您收到錯誤訊息或內容在瀏覽此教學時不起作用,請務必檢視[故障排除頁面](troubleshooting.md)。

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.設定轉換與 Web 部署參數

有兩種方法可以自動變更*Web.config*檔設定的過程[:Web.config 轉換](https://msdn.microsoft.com/library/dd465326.aspx)與[Web 部署參數](https://msdn.microsoft.com/library/ff398068.aspx)。 *Web.config*轉換檔包含 XML 標籤,用於指定在部署*Web.config*檔時如何更改該檔。 您可以為特定生成配置和特定發佈設定檔指定不同的更改。 預設產生設定是除錯和發表,您可以創建自定義生成配置。 發佈配置檔通常對應於目標環境。 (您將瞭解有關在["作為測試環境"教程部署到 IIS](deploying-to-iis.md)中的發表配置檔的更多資訊。

Web Deploy 參數可用於指定在部署期間必須配置的許多不同類型的設置,包括*Web.config 檔中*的設置。 當用於指定*Web.config*檔更改時,Web Deploy 參數的設置更為複雜,但在部署之前不知道要設置的值時,這些參數很有用。 例如,在企業環境中,您可以創建*部署包*並將其交給 IT 部門的人員以在生產中安裝,並且此人必須能夠輸入您不知道的連接字串或密碼。

對於本教學系列介紹的方案,您事先知道必須對*Web.config*檔執行的所有操作,因此無需使用 Web Deploy 參數。 您將設定一些因所使用的生成配置而異的轉換,以及一些因使用的發佈配置檔而異的轉換。

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>在 Azure 中指定 Web.設定設定

如果要更改的*Web.config*檔`<connectionStrings>`設定`<appSettings>`位於 或 元素中,並且如果要在 Azure 應用服務中部署到 Web 應用,則可以在部署期間自動更改另一個選項。 您可以在 Web 應用程式的管理門戶頁的 **「設定」** 選項卡中輸入要在 Azure 中生效的設定(向下滾動到**應用設定**和**連接字串**部分)。 部署專案時,Azure 會自動應用更改。 有關詳細資訊,請參閱[Windows Azure 網站:應用程式字串和連接字串的工作原理](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。

## <a name="default-transformation-files"></a>預設轉換檔案

在**解決方案資源管理員**中,展開*Web.config*以檢視*Web.Debug.config*和*Web.Release.config*為兩個預設生成設定預設創建的轉換檔。

![Web.config_transform_files](web-config-transformations/_static/image1.png)

您可以通過右鍵單擊 Web.config 檔並從上下文選單中選擇 **「添加設定轉換」** 來建立自定義生成配置的轉換檔。 對於本教程,您不需要執行此操作,並且功能表選項已禁用,因為您尚未創建任何自定義生成配置。

稍後,您將再創建三個轉換檔,每個檔用於測試、暫存和生產發佈配置檔。 在發佈配置檔轉換檔中處理的設置的典型示例是 WCF 終結點,用於測試和生產。 在建立與它們一起的發佈設定檔後,您將在以後的教程中創建發佈設定檔轉換檔。

## <a name="disable-debug-mode"></a>關閉除錯模式

屬性是相依於產生設定而非目標環境的設定範`debug`例 。 對於發佈生成,您通常希望禁用調試,而不管要部署到哪個環境。 因此,預設情況下,Visual Studio 專案範本創建*Web.Release.config*轉換`debug`檔,這些轉換`compilation`檔案的代碼從 元素中刪除該屬性。 下面是預設的*Web.Release.config*:除了註釋掉的一些範例轉換程式碼外`compilation`,它還在元素`debug`中包括刪除 屬性的代碼:

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

該`xdt:Transform="RemoveAttributes(debug)"`屬性指定您希望從已`debug`部署`system.web/compilation`的*Web.config*檔中的元素中刪除該屬性。 這將在每次部署發佈版本時完成。

## <a name="limit-error-log-access-to-administrators"></a>限制管理者的錯誤紀錄

如果應用程式執行時發生錯誤,應用程式將顯示一個通用錯誤頁,以代替系統生成的錯誤頁,並且它使用[Elmah NuGet 套件](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)進行錯誤日誌記錄和報告。 應用程式`customErrors` *Web.config*檔案中的元素指定錯誤頁:

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

要查看錯誤頁,請暫時將`mode``customErrors`元素的屬性從"僅遠端"更改為"打開",並從 Visual Studio 運行應用程式。 通過請求無效 URL(如*學生xxx.aspx)* 導致錯誤。 您看到的不是 IIS 生成的"找不到資源"錯誤頁,而是看到*泛錯誤Page.aspx*頁面。

![錯誤頁](web-config-transformations/_static/image2.png)

要檢視錯誤紀錄,請將連接埠號後網址中的所有內容取代為*elmah.axd(* 例如`http://localhost:51130/elmah.axd`),然後按 Enter:

![ELMAH 頁面](web-config-transformations/_static/image3.png)

完成後,不要忘記將`customErrors`元素設置為"僅遠端"模式。

在開發電腦上,允許免費訪問錯誤日誌頁很方便,但在生產中,這將存在安全風險。 對於生產網站,要添加一個授權規則,該規則限制管理員對錯誤日誌的訪問,並確保該限制在測試和暫存中也正常工作。 因此,這是每次部署發佈生成時要實現的另一個更改,因此它屬於*Web.Release.config*檔。

打開*Web.Release.config,*`location``configuration`並在結束 標記之前添加新元素,如下所示。

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

屬性`Transform`值"Insert"會導致此`location`元素作為同級添加到*Web.config*`location`檔中的任何 現有元素。 (已經有一個`location`元素指定**更新積分**頁的授權規則。

現在,您可以預覽轉換,以確保正確編碼它。

在**解決方案資源管理器**中,右鍵單擊*Web.Release.config,* 然後單擊 **「預覽轉換**」。

![預覽轉換選單](web-config-transformations/_static/image4.png)

將打開一個頁面,顯示左側的開發*Web.config*檔以及部署的*Web.config*檔在右側的外觀,並突出顯示更改。

![除錯轉換預覽](web-config-transformations/_static/image5.png)

![位置轉換預覽](web-config-transformations/_static/image6.png)

(在預覽中,您可能會注意到一些未為這些更改編寫轉換的其他更改:這些更改通常涉及刪除不影響功能的空白。

部署後測試網站時,還將進行測試以驗證授權規則是否有效。

> [!NOTE] 
> 
> **安全說明**切勿在生產應用程式中向公眾顯示錯誤詳細資訊,也不要將該資訊存儲在公共位置。 攻擊者可以使用錯誤資訊來發現網站中的漏洞。 如果您在自己的應用程式中使用 ELMAH,請配置 ELMAH 以最大程度地降低安全風險。 本教程中的 ELMAH 示例不應視為推薦的配置。 這是一個範例,用於說明如何處理應用程式必須能夠在中創建文件的資料夾。 有關詳細資訊,請參閱保護[ELMAH 終結點](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)。

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>在設定檔轉換檔案中要處理的設定

常見方案是具有在部署到的每個環境中必須不同的*Web.config*檔設置。 例如,調用 WCF 服務的應用程式在測試和生產環境中可能需要不同的終結點。 康托索大學的申請還包括這種設置。 此設定控制網站頁面上的可見指示器,該指示器告訴您處於哪個環境,例如開發、測試或生產。 設定值確定應用程式是否會將「(Dev)」或「(測試)」追加到*Site.master*頁中的主標題:

![環境指示器](web-config-transformations/_static/image7.png)

當應用程式在暫存或生產中運行時,環境指示器將被省略。

Contoso 大學網頁讀取在*Web.config*`appSettings`檔中設定的值,以便確定應用程式在以下環境執行的環境:

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

在測試環境中的值應為"測試",對於暫存和生產來說應為"Prod"。

轉換檔案中的以下代碼將實現此轉換:

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

`xdt:Transform`屬性值「SetAttributes」表示此轉換的目的是更改*Web.config*檔中現有元素的屬性值。 `xdt:Locator`屬性值"Match(鍵)"表示要修改的元素是其`key`屬性與此處指定`key`的 屬性匹配的元素。 元素的唯一`add`其他屬性`value`是 ,這就是將在部署的*Web.config 檔中*更改的內容。 `value`此處顯示的代碼會導致`Environment``appSettings`元素的屬性設置為部署的*Web.config*檔中的"Test"。

此轉換屬於尚未建立的發佈設定檔轉換檔。 在為測試、暫存和生產環境創建發佈設定檔時,您將創建和更新實現此更改的轉換檔。 您將在[部署到 IIS](deploying-to-iis.md)並[部署到生產](deploying-to-production.md)教程中執行此操作。

> [!NOTE]
> 由於此設定位於`<appSettings>`元素中,因此在本主題前面介紹的 Azure 中,在 Azure 應用服務中部署到 Web 應用時,還有另一種用於指定轉換的替代方法。請參閱[在本主題前面指定 Azure 中的 Web.config 設定](#watransforms)。

## <a name="setting-connection-strings"></a>設定連接字串

儘管預設轉換檔包含一個範例,其中展示如何更新連接字串,但在大多數情況下,您不需要設定連接字串轉換,因為您可以在發佈設定檔中指定連接字串。 您將在[部署到 IIS](deploying-to-iis.md)並[部署到生產](deploying-to-production.md)教程中執行此操作。

## <a name="summary"></a>總結

現在,在創建發佈設定檔之前,您已經盡可能多地使用*Web.config*轉換,並且您已經看到了部署的 Web.config 檔中的內容的預覽。

![位置轉換預覽](web-config-transformations/_static/image8.png)

在下面的教學中,您將處理需要設置專案屬性的部署設置任務。

## <a name="more-information"></a>相關資訊

關於這個教學涵蓋的主題的詳細資訊,請參閱在 Visual Studio 和 ASP.NET 的 Web 部署內容映射中[使用 Web.config 轉換來更改目標 Web.config 檔或 app.config 檔中的設定](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms)。

> [!div class="step-by-step"]
> [前一個](preparing-databases.md)
> [下一個](project-properties.md)
