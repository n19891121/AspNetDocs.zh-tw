---
uid: mvc/overview/deployment/docker
title: 將 ASP.NET MVC 應用程式遷移到 Windows 容器
description: 了解如何擷取現有的 ASP.NET MVC 應用程式並在 Windows Docker 容器中執行
keywords: Windows Containers,Docker,ASP.NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: ef184f4256c20e2a66de8fd2d4f8e67f07d9a086
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57053425"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a>將 ASP.NET MVC 應用程式遷移到 Windows 容器

在 Windows 容器中執行現有的 .NET Framework 架構應用程式，不需要對您的應用程式進行任何變更。 若要在 Windows 容器中執行您的應用程式，您可以建立包含您應用程式的 Docker 映像，然後啟動該容器。 本主題說明如何才能擷取現有 [ASP.NET MVC 應用程式 (ASP.NET MVC application)](http://www.asp.net/mvc) 並部署到 Windows 容器中。

您可以從現有的 ASP.NET MVC 應用程式開始，然後使用 Visual Studio 建置已發行的資產。 您可以使用 Docker，建立其中包含並會執行您應用程式的映像。 接著瀏覽到 Windows 容器中正在執行的網站，並確認應用程式可以正常運作。

本文假設您具備 Docker 的基本知識。 您可以閱讀 [Docker 概觀](https://docs.docker.com/engine/understanding-docker/)，以了解 Docker。

您將在容器中執行的應用程式是會隨機回答問題的簡單網站。 此應用程式是沒有驗證或資料庫儲存體的基本 MVC 應用程式，讓您著重於將 Web 層移至容器。 未來的主題將說明如何移動和管理容器化應用程式中的永續性儲存體。

移動您的應用程式包含下列步驟：

1. [建立發行工作以建置映像資產](#publish-script)
1. [建立用以執行應用程式的 Docker 映像](#build-the-image)
1. [啟動執行映像的 Docker 容器](#start-a-container)
1. [使用瀏覽器確認應用程式](#verify-in-the-browser)

[完成的應用程式](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator)在 GitHub 上。

## <a name="prerequisites"></a>必要條件

開發用的電腦必須具備下列軟體：

- [Windows 10 年度更新版](https://www.microsoft.com/software-download/windows10/)（或更新版本） 或[Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) （或更新版本）
- [Docker for Windows](https://docs.docker.com/docker-for-windows/) - 穩定版 1.13.0 或 1.12 Beta 26 (或更新版本)
- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> 如果您在使用 Windows Server 2016，請遵循[容器主機部署 - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment) 的指示。

安裝並啟動 Docker，以滑鼠右鍵按一下系統匣圖示，然後選取後**切換至 Windows 容器**。 如此才能根據 Windows 執行 Docker 映像。 此命令需要幾秒鐘的時間執行：

![Windows 容器][windows-container]

## <a name="publish-script"></a>發行指令碼

將您必須載入 Docker 映像的所有資產收集在某一位置。 您可以使用 Visual Studio 的 [發行] 命令來建立應用程式的發行設定檔。 此設定檔會將所有資產放在一個樹狀目錄中，您稍後會在本教學課程將此目錄複製到目標映像。

**發行步驟**

1. 以滑鼠右鍵按一下 Visual Studio 中的 Web 專案，然後選取 [發行]。
1. 按一下 [自訂設定檔] 按鈕，然後選取 [檔案系統] 作為方法。
1. 選擇目錄。 依照慣例，下載的範例會使用 `bin\Release\PublishOutput`。

![發行連線][publish-connection]

開啟 [設定] 索引標籤的 [檔案發行選項] 區段。選取 [發行期間預先編譯]。 此最佳化表示您將要編譯 Docker 容器中的檢視，而正在複製預先編譯的檢視。

![發行設定][publish-settings]

按一下 [發行]，Visual Studio 會將所有需要的資產複製到目的資料夾。

## <a name="build-the-image"></a>建立映像

建立新的檔案，名為*Dockerfile*來定義您的 Docker 映像。 *Dockerfile*包含指示，來建置最終映像，並包含任何基礎映像名稱、 所需的元件、 您想要執行的應用程式和其他組態映像。 *Dockerfile*是輸入`docker build`建立映像的命令。

針對此練習中，您將建置基礎的映像`microsoft/aspnet`映像位於[Docker Hub](https://hub.docker.com/r/microsoft/aspnet/)。
基礎映像 `microsoft/aspnet` 是 Windows Server 映像。 它包含 Windows Server Core、 IIS 和 ASP.NET 4.7.2。 當您在容器中執行此映像時，其將會自動啟動 IIS 和已安裝的網站。

建立映像的 Dockerfile 看起來像這樣：

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

此 Dockerfile 中沒有 `ENTRYPOINT` 命令。 您不需要此命令。 執行 Windows Server 與 IIS，IIS 處理序時，進入點，會設定為 aspnet 的基底映像中啟動。

執行 Docker 建置命令，建立會執行 ASP.NET 應用程式的映像。 若要這樣做，請在您的專案目錄中開啟 PowerShell 視窗並的方案目錄中，輸入下列命令：

```console
docker build -t mvcrandomanswers .
```

此命令會建立使用您的 Dockerfile 中的指示新的映像命名 (-t 標記) 為 mvcrandomanswers 映像。 這可能包括從 [Docker Hub](http://hub.docker.com) 提取基礎映像，然後將您的應用程式加入至該映像。

該命令完成之後，您可以執行 `docker images` 命令來了解新映像的相關資訊：

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

您電腦上的映像識別碼會有所不同。 現在，讓我們來執行應用程式。

## <a name="start-a-container"></a>啟動容器

執行下列 `docker run` 命令來啟動容器：

```console
docker run -d --name randomanswers mvcrandomanswers
```

`-d` 引數會指示 Docker 在離線模式中啟動映像。 這表示 Docker 映像可在與目前殼層中斷連線的情況下執行。

在許多 docker 範例中，您可能會看到對應的容器和主機的連接埠-p。 預設的 aspnet 映像已經設定要在連接埠 80 上接聽，並將它公開的容器。

`--name randomanswers` 提供執行中容器的名稱。 您可以使用此名稱，而不是大多數命令中的容器識別碼。

`mvcrandomanswers` 是要啟動之映像的名稱。

## <a name="verify-in-the-browser"></a>在瀏覽器中確認

一旦容器啟動時，連接到執行的容器使用`http://localhost`中所示的範例。 在您的瀏覽器中輸入該 URL，您應該會看到執行中的網站。

> [!NOTE]
> 某些 VPN 或 Proxy 軟體可能會阻止您瀏覽至您的網站。
> 您可以暫時停用，以確保您的容器可以正常運作。

GitHub 上的範例目錄包含 [PowerShell 指令碼](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1)，可為您執行這些命令。 開啟 PowerShell 視窗，將目錄變更為您的方案目錄，然後輸入：

```console
./run.ps1
```

上述命令會建置該映像、 映像清單會顯示您的電腦，並啟動容器。

若要停止容器，請發出 `docker stop` 命令：

```console
docker stop randomanswers
```

若要移除容器，請發出 `docker rm` 命令：

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "切換至 Windows 容器"
[publish-connection]: media/aspnetmvc/PublishConnection.png "發行至檔案系統"
[publish-settings]: media/aspnetmvc/PublishSettings.png "發行設定"
