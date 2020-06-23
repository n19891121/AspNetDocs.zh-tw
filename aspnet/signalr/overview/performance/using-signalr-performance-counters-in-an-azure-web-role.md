---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: 在 Azure Web 角色中使用 SignalR 效能計數器 |Microsoft Docs
author: guardrex
description: 如何在 Azure Web 角色中安裝和使用 SignalR 效能計數器。
keywords: ASP.NET，signalr，效能計數器，azure web 角色
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 3de42435887113f93c6b8c36145793952af4d735
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240643"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a>使用 Azure Web 角色中的 SignalR 效能計數器

作者：[Luke Latham](https://github.com/guardrex)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

SignalR 效能計數器是用來監視您的應用程式在 Azure Web 角色中的效能。 這些計數器是由 Microsoft Azure 診斷所捕捉。 您可以使用*signalr.exe*（用於獨立或內部部署應用程式的相同工具），在 Azure 上安裝 SignalR 效能計數器。 由於 Azure 角色是暫時性的，因此您可以設定應用程式在啟動時安裝並註冊 SignalR 效能計數器。

## <a name="prerequisites"></a>必要條件

* Visual Studio 2015 或[2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
* [Visual Studio 的 MICROSOFT AZURE SDK](https://azure.microsoft.com/downloads/) **附注：安裝 sdk 之後，請重新開機您的電腦。**
* Microsoft Azure 訂用帳戶：若要註冊免費的 Azure 試用帳戶，請參閱[Azure 免費試用](https://azure.microsoft.com/free/dotnet/)。

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a>建立可公開 SignalR 效能計數器的 Azure Web 角色應用程式

1. 開啟 Visual Studio。

2. 在 Visual Studio 中，選取 [檔案] >  [新增] >  [專案]。

3. 在 [**新增專案**] 對話方塊中，選取左側的 [ **Visual c #**  >  **雲端**] 類別，然後選取 [ **Azure 雲端服務**] 範本。 將應用程式命名為**SignalRPerfCounters** ，然後選取 **[確定]**。

   ![新的雲端應用程式](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > 如果您沒有看到 [**雲端**範本] 類別或 [ **azure 雲端服務**] 範本，則需要安裝適用于 Visual Studio 2017 的**Azure 開發**工作負載。 選擇 [**新增專案**] 對話方塊左下角的 [**開啟 Visual Studio 安裝程式**] 連結，以開啟 Visual Studio 安裝程式。 選取 [ **Azure 開發**] 工作負載，然後選擇 [**修改**] 以開始安裝工作負載。
   >
   > ![Visual Studio 安裝程式中的 Azure 開發工作負載](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. 在 [**新增 Microsoft Azure 雲端服務**] 對話方塊中，選取 [ **ASP.NET Web 角色**]，然後選取 [>] 按鈕，將角色新增至專案。 選取 [確定]。

   ![新增 ASP.NET Web 角色](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. 在 [**新增 ASP.NET Web 應用程式-WebRole1** ] 對話方塊中，選取 [ **MVC** ] 範本，然後選取 **[確定]**。

   ![新增 MVC 和 Web API](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. 在**方案總管**中，開啟**WebRole1**下的*diagnostics.wadcfgx*檔案。

   ![方案總管診斷 diagnostics.wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. 以下列設定取代檔案的內容，並儲存檔案：

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. 從 [**工具**] [NuGet 套件管理員] 開啟 [**套件管理員主控台**]  >  ** **。 輸入下列命令以安裝最新版本的 SignalR 和 SignalR 公用程式套件：

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. 設定應用程式，以便在啟動或回收時，將 SignalR 效能計數器安裝到角色實例。 在**方案總管**中，以滑鼠右鍵按一下**WebRole1**專案，然後選取 [**加入**  >  **新資料夾**]。 將新資料夾命名為*Startup*。

   ![加入開機檔案夾](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. 從**Microsoft.AspNet.SignalR.Utils** /SignalRPerfCounters/packages/Microsoft.AspNet.SignalR.Utils. *signalr.exe* \<project folder> 複製 \<version>signalr.exe檔案（以 Utils 套件新增）/tools 至您在上一個步驟中建立的 [*啟動*] 資料夾。

11. 在**方案總管**中，以滑鼠右鍵按一下 [*啟動*] 資料夾，然後選取 [**新增**] [  >  **現有專案**]。 在出現的對話方塊中，選取 [ *signalr.exe* ]，然後選取 [**新增**]。

    ![將 signalr.exe 新增至專案](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. 以滑鼠右鍵按一下您所建立的 [*啟動*] 資料夾。 選取 [**加入**  >  **新專案**]。 選取 [**一般**] 節點，選取 [**文字檔**]，並將新專案命名為*SignalRPerfCounterInstall。* 此命令檔會將 SignalR 效能計數器安裝到 web 角色。

    ![建立 SignalR 效能計數器安裝批次檔](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. 當 Visual Studio 建立*SignalRPerfCounterInstall .cmd*檔案時，它會自動在主視窗中開啟。 使用下列腳本來取代檔案的內容，然後儲存並關閉檔案。 此腳本會執行*signalr.exe*，這會將 SignalR 效能計數器新增至角色實例。

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. 選取**方案總管**中的*signalr.exe*檔案。 在檔案的**屬性**中，將 [**複製到輸出目錄**] 設定為 [**永遠複製**]。

    ![將 [複製到輸出目錄] 設定為 [永遠複製]](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. 針對*SignalRPerfCounterInstall* ，重複上一個步驟。

16. 以滑鼠右鍵按一下 [ *SignalRPerfCounterInstall* ] 檔案，然後選取 [**開啟方式**]。 在出現的對話方塊中，選取 [**二進位編輯器**]，然後選取 **[確定]**。

    ![以二進位編輯器開啟](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. 在二進位編輯器中，選取檔案中的任何前置位元組並加以刪除。 儲存並關閉檔案。

    ![刪除前置位元組](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. 開啟*ServiceDefinition* ，並新增啟動工作，以在服務啟動時執行*SignalrPerfCounterInstall .cmd*檔案：

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. 開啟 `Views/Shared/_Layout.cshtml` 並移除檔案結尾的 jQuery 配套腳本。

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. 新增會持續在伺服器上呼叫方法的 JavaScript 用戶端 `increment` 。 開啟 `Views/Home/Index.cshtml` ，並將內容取代為下列程式碼：

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. 在名為*hub*的**WebRole1**專案中建立新的資料夾。 以滑鼠右鍵按一下**方案總管**中的 [*中樞*] 資料夾，**然後選取 [**  >  **新增專案**]。 在 [**加入新專案**] 對話方塊中，選取 [ **Web**  >  **SignalR** ] 類別，然後選取 [ **SignalR Hub Class （v2）** ] 專案範本。 將新的中樞命名為*MyHub.cs* ，然後選取 [**新增**]。

    ![將 SignalR 中樞類別新增至 [新增專案] 對話方塊中的 [中樞] 資料夾](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. *MyHub.cs*會自動在主視窗中開啟。 將內容取代為下列程式碼，然後儲存並關閉檔案：

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. *[Crank.exe](signalr-connection-density-testing-with-crank.md)* 是 SignalR 程式碼基底所提供的連接密度測試控管。 由於迅速地建立需要持續連線，因此您可以將其新增至您的網站，以便在測試時使用。 將新資料夾新增至名為*PersistentConnections*的**WebRole1**專案。 以滑鼠右鍵按一下此資料夾，然後選取 [**新增**  >  **類別**]。 將新的類別檔案命名為*MyPersistentConnections.cs* ，**然後選取 [新增]**。

24. Visual Studio 會在主視窗中開啟*MyPersistentConnections.cs*檔案。 將內容取代為下列程式碼，然後儲存並關閉檔案：

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. 使用 `Startup` 類別時，SignalR 物件會在 OWIN 啟動時啟動。 開啟或建立*Startup.cs* ，並將內容取代為下列程式碼：

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    在上述程式碼中， `OwinStartup` 屬性會標示此類別以開始 OWIN。 `Configuration`方法會啟動 SignalR。

26. 按**F5**在 Microsoft Azure 模擬器中測試您的應用程式。

    > [!NOTE]
    > 如果您在**MapSignalR**遇到**FileLoadException** ，請將*web.config*中的系結重新導向變更為下列內容：

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. 等待約一分鐘。 在 Visual Studio 中開啟 [Cloud Explorer 工具] 視窗（**View**  >  **Cloud Explorer**），然後展開路徑 `(Local)/Storage Accounts/(Development)/Tables` 。 按兩下 [ **WADPerformanceCountersTable**]。 您應該會在資料表資料中看到 SignalR 計數器。 如果您看不到資料表，可能需要重新輸入您的 Azure 儲存體認證。 您可能需要選取 [重新整理] 按鈕來查看**Cloud Explorer**中的資料表，或選取 [開啟資料表] 視窗中的 [重新整理 **] 按鈕，** 以查看資料表**中的資料**。

    ![選取 Visual Studio Cloud Explorer 中的 WAD 效能計數器資料表](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![顯示 WAD 效能計數器資料表中收集的計數器](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. 若要在雲端中測試您的應用程式，請更新**serviceconfiguration.cscfg** ，並將設定 `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 為有效的 Azure 儲存體帳戶連接字串。

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. 將應用程式部署至您的 Azure 訂用帳戶。 如需如何將應用程式部署至 Azure 的詳細資訊，請參閱[如何建立和部署雲端服務](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)。

30. 請等待數分鐘。 在**Cloud Explorer**中，找出您在上面設定的儲存體帳戶，並 `WADPerformanceCountersTable` 在其中尋找資料表。 您應該會在資料表資料中看到 SignalR 計數器。 如果您看不到資料表，可能需要重新輸入您的 Azure 儲存體認證。 您可能需要選取 [重新整理] 按鈕來查看**Cloud Explorer**中的資料表，或選取 [開啟資料表] 視窗中的 [重新整理 **] 按鈕，** 以查看資料表**中的資料**。

特別感謝這個教學課程中使用的原始內容的[聖馬丁 Richard](https://social.msdn.microsoft.com/profile/Martin+Richard) 。
