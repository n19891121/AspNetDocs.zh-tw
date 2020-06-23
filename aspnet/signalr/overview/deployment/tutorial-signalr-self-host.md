---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: 教學課程： SignalR 自我裝載 |Microsoft Docs
author: bradygaster
description: 本教學課程說明如何建立自我裝載的 SignalR 2 伺服器，以及如何使用 JavaScript 用戶端連接到它。 教學課程中使用的軟體版本 .。。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 7470e0d6b68772ccfd979c834b7db81fbba3ca78
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240617"
---
# <a name="tutorial-signalr-self-host"></a>教學課程：SignalR 自我裝載

由[派翠克 Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本教學課程說明如何建立自我裝載的 SignalR 2 伺服器，以及如何使用 JavaScript 用戶端連接到它。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 第2版
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a>在本教學課程中使用 Visual Studio 2012
>
>
> 若要在本教學課程中使用 Visual Studio 2012，請執行下列動作：
>
> - 將您的[套件管理員](http://docs.nuget.org/docs/start-here/installing-nuget)更新為最新版本。
> - 安裝[Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)。
> - 在 [Web Platform Installer 中，搜尋並安裝**適用于 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1**。 這會為 SignalR 類別（例如**中樞**）安裝 Visual Studio 範本。
> - 有些範本（例如**OWIN Startup 類別**）將無法使用;為此，請改用類別檔案。
>
>
> ## <a name="questions-and-comments"></a>問題與意見
>
> 請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

## <a name="overview"></a>概觀

SignalR 伺服器通常裝載于 IIS 中的 ASP.NET 應用程式中，但也可以使用自我裝載程式庫自我裝載（例如主控台應用程式或 Windows 服務）。 此程式庫（例如所有的 SignalR 2）是以 OWIN （[開放式 Web 介面 for .net](http://owin.org)）為基礎。 OWIN 會定義 .NET web 伺服器和 web 應用程式之間的抽象概念。 OWIN 會將 web 應用程式與伺服器分離，讓 OWIN 非常適合在 IIS 以外的進程中自我裝載 web 應用程式。

未在 IIS 中裝載的原因包括：

- 無法使用或不需要 IIS 的環境，例如不含 IIS 的現有伺服器陣列。
- 必須避免 IIS 的效能負擔。
- SignalR 功能會新增至在 Windows 服務、Azure 背景工作角色或其他進程中執行的現有應用程式。

如果基於效能考慮，將解決方案開發為自我裝載，建議您也測試裝載于 IIS 中的應用程式，以判斷效能的優勢。

本教學課程包含下列各節：

- [建立伺服器](#server)
- [使用 JavaScript 用戶端存取伺服器](#js)

<a id="server"></a>

## <a name="creating-the-server"></a>建立伺服器

在本教學課程中，您將建立裝載于主控台應用程式中的伺服器，但伺服器可以裝載于任何類型的進程，例如 Windows 服務或 Azure 背景工作角色。 如需在 Windows 服務中裝載 SignalR 伺服器的範例程式碼，請參閱[Windows 服務中的自我裝載 SignalR](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3)。

1. 以系統管理員許可權開啟 Visual Studio 2013。 選取 **[** 檔案]、[**新增專案**]。 在 [**範本**] 窗格中的 [ **Visual c #** ] 節點下選取 [ **Windows** ]，然後選取 [**主控台應用程式**] 範本。 將新專案命名為 "SignalRSelfHost"，然後按一下 **[確定]**。

    ![](tutorial-signalr-self-host/_static/image1.png)
2. 選取 [**工具**] [  >  **nuget 套件管理員**] [  >  **套件管理員主控台**]，以開啟 NuGet 套件管理員主控台。
3. 在 [套件管理員主控台] 中，輸入下列命令：

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    此命令會將 SignalR 2 自我裝載程式庫新增至專案。
4. 在 [套件管理員主控台] 中，輸入下列命令：

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    此命令會將 Owin 程式庫新增至專案。 此程式庫將用於跨網域支援，這對於裝載 SignalR 的應用程式和不同網域中的網頁用戶端而言是必要的。 因為您將在不同的埠上裝載 SignalR 伺服器和 web 用戶端，這表示必須啟用跨網域，才能在這些元件之間進行通訊。
5. 以下列程式碼取代 Program.cs 的內容。

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    上述程式碼包含三個類別：

    - **程式**，包括定義執行主要路徑的**Main**方法。 在此方法中，**啟動**類型的 web 應用程式會在指定的 URL （ `http://localhost:8080` ）上啟動。 如果端點上需要安全性，則可以執行 SSL。 如需詳細資訊，請參閱[如何：使用 SSL 憑證設定埠](https://msdn.microsoft.com/library/ms733791.aspx)。
    - **啟動**，此類別包含 SignalR 伺服器的設定（本教學課程使用的唯一設定是的呼叫 `UseCors` ），而呼叫會 `MapSignalR` 針對專案中的任何中樞物件建立路由。
    - **MyHub**，這是應用程式將提供給用戶端的 SignalR 中樞類別。 此類別具有單一方法**Send**，用戶端會呼叫來將訊息廣播給所有其他已連線的用戶端。
6. 編譯並執行應用程式。 伺服器正在執行的位址應該會顯示在主控台視窗中。

    ![](tutorial-signalr-self-host/_static/image2.png)
7. 如果執行因例外狀況 `System.Reflection.TargetInvocationException was unhandled` 而失敗，您將需要以系統管理員許可權重新開機 Visual Studio。
8. 請先停止應用程式，再繼續進行下一節。

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a>使用 JavaScript 用戶端存取伺服器

在本節中，您將使用[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程中的相同 JavaScript 用戶端。 我們只會對用戶端進行一項修改，也就是明確定義中樞 URL。 使用自我裝載的應用程式時，伺服器可能不一定會與連線 URL 位於相同的位址（因為反向 proxy 和負載平衡器），因此必須明確定義 URL。

1. 在**方案總管**中，以滑鼠右鍵按一下方案，然後選取 [**加入**]、[**新增專案**]。 選取 [ **web** ] 節點，然後選取 [ **ASP.NET web 應用程式**] 範本。 將專案命名為 "JAVAscriptClient"，然後按一下 **[確定]**。

    ![](tutorial-signalr-self-host/_static/image3.png)
2. 選取 [**空白**] 範本，並將其餘選項保留為未選取狀態。 選取 [**建立專案**]。

    ![](tutorial-signalr-self-host/_static/image4.png)
3. 在 [套件管理員主控台] 中，選取 [**預設專案**] 下拉式集中的 "JAVAscriptClient" 專案，然後執行下列命令：

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    此命令會安裝用戶端中所需的 SignalR 和 JQuery 程式庫。
4. 以滑鼠右鍵按一下您的專案，然後選取 [**加入**]、[**新增專案**]。 選取 [ **Web** ] 節點，然後選取 [HTML 網頁]。 將頁面命名為**Default.html**。

    ![](tutorial-signalr-self-host/_static/image5.png)
5. 將新 HTML 網頁的內容取代為下列程式碼。 確認此處的腳本參考符合專案的 Scripts 資料夾中的腳本。

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    下列程式碼（在上述程式碼範例中反白顯示）是您對取得開始教學課程中所使用之用戶端的新增功能（除了將程式碼升級至 SignalR 第2版 Beta 版以外）。 這行程式碼會在伺服器上明確設定 SignalR 的基底連接 URL。

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. 以滑鼠右鍵按一下方案，然後選取 [**設定啟始專案**...]。選取 [**多個啟始專案**] 選項按鈕，並將兩個專案的 [**動作**] 設定為 [**啟動**]。

    ![](tutorial-signalr-self-host/_static/image6.png)
7. 以滑鼠右鍵按一下 [Default.html]，然後選取 [**設定為起始頁**]。
8. 執行應用程式。 隨即會啟動伺服器和頁面。 如果在伺服器啟動之前載入頁面，您可能需要重載網頁（或選取偵錯工具中的 [**繼續**]）。
9. 在瀏覽器中，于出現提示時提供使用者名稱。 將頁面的 URL 複製到另一個瀏覽器索引標籤或視窗中，並提供不同的使用者名稱。 如消費者入門教學課程所示，您可以將訊息從一個瀏覽器窗格傳送到另一個。
