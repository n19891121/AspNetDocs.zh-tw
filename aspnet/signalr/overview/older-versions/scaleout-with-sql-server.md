---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: SignalR 向外延展與 SQL Server (SignalR 1.x) |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: eb0d6cd23563f72bb382b3a3304d03294f783ad8
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/25/2019
ms.locfileid: "58425843"
---
<a name="signalr-scaleout-with-sql-server-signalr-1x"></a>使用 SQL Server 的向外延展 (SignalR 1.x)
====================
藉由[Mike Wasson](https://github.com/MikeWasson)， [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

在本教學課程中，您將使用 SQL Server 將訊息散發到部署兩個不同的 IIS 執行個體中的 SignalR 應用程式。 您也可以在單一測試電腦上，執行本教學課程中，但若要取得完整的效果，您需要部署兩個或多部伺服器的 SignalR 應用程式。 其中一部伺服器，或個別的專用伺服器上，您也必須安裝 SQL Server。 另一個選項是執行本教學課程使用 Azure 上的 Vm。

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a>必要條件

Microsoft SQL Server 2005 或更新版本。 後擋板支援桌上型電腦和伺服器版本的 SQL Server。 它不支援 SQL Server Compact Edition 或 Azure SQL Database。 （如果您的應用程式裝載在 Azure 中，請考慮服務匯流排後擋板改用。）

## <a name="overview"></a>總覽

我們會詳細的教學課程之前，以下是您將進行的快速概觀。

1. 建立新的空白資料庫。 後擋板將此資料庫中建立所需的資料表。
2. 將這些 NuGet 套件新增至您的應用程式中： 

    - [Microsoft.AspNet.SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft.AspNet.SignalR.SqlServer](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. 建立 SignalR 應用程式。
4. 若要設定的後擋板的 Global.asax 中加入下列程式碼： 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a>設定資料庫

決定應用程式是否會使用 Windows 驗證或 SQL Server 驗證來存取資料庫。 不論如何，請確定資料庫使用者具有登入，建立結構描述，然後建立資料表的權限。

建立後擋板，若要使用新的資料庫。 您可以提供該資料庫任何名稱。 您不需要在資料庫中建立任何資料表後擋板會建立所需的資料表。

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a>啟用 Service Broker

建議後擋板資料庫啟用 Service Broker。 Service Broker 提供傳訊和佇列可讓後擋板接收更新，更有效率的 SQL Server 中的原生支援。 （不過後, 擋板也適用於沒有 Service Broker。）

若要檢查是否啟用 Service Broker 時，請查詢**已\_broker\_啟用**中的資料行**sys.databases**目錄檢視。

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

若要啟用 Service Broker，請使用下列 SQL 查詢：

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> 如果此查詢似乎發生死結，請確定沒有連線到資料庫的應用程式。

如果您已啟用追蹤，追蹤也會顯示是否已啟用 Service Broker。

## <a name="create-a-signalr-application"></a>建立 SignalR 應用程式

依照下列其中一個這些教學課程中建立的 SignalR 應用程式：

- [開始使用 SignalR](../getting-started/tutorial-getting-started-with-signalr.md)
- [開始使用 SignalR 和 MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md)

接下來，我們將修改的聊天應用程式，以支援向外的延展與 SQL Server。 首先，將 SignalR.SqlServer NuGet 封裝加入您的專案。 在 Visual Studio 中，從**工具**功能表上，選取**NuGet 套件管理員**，然後選取**Package Manager Console**。 在 [套件管理員主控台] 視窗中，輸入下列命令：

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

接下來，開啟 Global.asax 檔案。 將下列程式碼加入**應用程式\_啟動**方法：

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a>部署和執行應用程式

準備您的 Windows Server 執行個體，若要部署的 SignalR 應用程式。

新增 IIS 角色。 包含 「 應用程式開發 」 功能，包括 WebSocket 通訊協定。

![](scaleout-with-sql-server/_static/image4.png)

也包含 「 管理 」 服務 （列在 [管理工具]）。

![](scaleout-with-sql-server/_static/image5.png)

**安裝 Web Deploy 3.0。** 當您執行 IIS 管理員，它會提示您安裝 Microsoft Web Platform，或者您可以[下載安裝程式](https://go.microsoft.com/fwlink/?LinkId=255386)。 在 平台安裝程式中，搜尋 Web Deploy，並安裝 Web Deploy 3.0

![](scaleout-with-sql-server/_static/image6.png)

檢查 Web 管理服務正在執行。 否則，請啟動服務。 （如果您沒有看到 Web 管理服務中的 Windows 服務清單，請確定您新增 IIS 角色時，安裝 「 管理服務。）

最後，開啟 TCP 連接埠 8172。 這是 Web Deploy 工具使用的連接埠。

現在，您已準備好要部署到伺服器的 從您的開發電腦的 Visual Studio 專案。 在 方案總管 中，以滑鼠右鍵按一下方案，然後按一下 **發佈**。

如需詳細的 web 部署的相關文件，請參閱[Visual Studio 及 ASP.NET 的 Web 部署內容對應](../../../whitepapers/aspnet-web-deployment-content-map.md)。

如果您部署兩部伺服器應用程式時，您可以在另一個瀏覽器視窗開啟每個執行個體，並查看他們都收到來自其他使用 SignalR 訊息。 （當然，在生產環境中，兩部伺服器會位於負載平衡器後方。）

![](scaleout-with-sql-server/_static/image7.png)

執行應用程式之後，您可以看到 SignalR，已自動建立資料表的資料庫中：

![](scaleout-with-sql-server/_static/image8.png)

SignalR 管理資料表。 只要部署應用程式，不刪除資料列、 修改資料表等。
