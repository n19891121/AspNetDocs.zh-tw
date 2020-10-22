---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: 將 SignalR 使用者對應至連接 |Microsoft Docs
author: bradygaster
description: 本主題說明如何保留使用者和其連線的相關資訊。 派翠克 Fletcher 有助於撰寫本主題。 本主題中使用的軟體版本 .。。
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345421"
---
# <a name="mapping-signalr-users-to-connections"></a>將 SignalR 使用者對應至連線

 作者：[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主題說明如何保留使用者和其連線的相關資訊。
>
> 派翠克 Fletcher 有助於撰寫本主題。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 第2版
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主題的先前版本
>
> 如需舊版 SignalR 的詳細資訊，請參閱 [SignalR 較舊版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>問題與意見
>
> 請針對您喜歡本教學課程的方式，以及我們可以在頁面底部的批註中改進的內容，留下意見反應。 如果您有與本教學課程不直接相關的問題，您可以將這些問題張貼至 [ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 或 [StackOverflow.com](http://stackoverflow.com/)。

## <a name="introduction"></a>簡介

連接至中樞的每個用戶端都會傳遞唯一的連線識別碼。您可以在中樞內容的屬性中取得此值 `Context.ConnectionId` 。 如果您的應用程式需要將使用者對應到連接識別碼並保存該對應，您可以使用下列其中一項：

- [使用者識別碼提供者 (SignalR 2) ](#IUserIdProvider)
- [記憶體內部儲存體](#inmemory)，例如字典
- [每位使用者的 SignalR 群組](#groups)
- [永久的外部儲存體](#database)，例如資料庫資料表或 Azure 資料表儲存體

本主題會顯示上述各項的各項。 您可以使用 `OnConnected` 類別的、 `OnDisconnected` 和 `OnReconnected` 方法 `Hub` 來追蹤使用者的連接狀態。

您應用程式的最佳方法取決於：

- 裝載應用程式的 web 伺服器數目。
- 您是否需要取得目前已連線使用者的清單。
- 您是否需要在應用程式或伺服器重新開機時保存群組和使用者資訊。
- 呼叫外部伺服器的延遲是否為問題。

下表說明哪些方法適用于這些考慮。

|  | 一部以上的伺服器 | 取得目前連線的使用者清單 | 重新開機後保存資訊 | 最佳效能 |
| --- | --- | --- | --- | --- |
| UserID 提供者 | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| 記憶體內 |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| 單一使用者群組 | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| 永久性、外部 | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>IUserID 提供者

這項功能可讓使用者透過新的介面 IUserIdProvider，指定 userId 是以 IRequest 為基礎。

**IUserIdProvider**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

依預設，會有一個使用使用者 `IPrincipal.Identity.Name` 做為使用者名稱的實作為使用者名稱。 若要變更此項，請 `IUserIdProvider` 在您的應用程式啟動時，使用全域主機註冊您的執行：

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

從中樞內，您將能夠透過下列 API 將訊息傳送給這些使用者：

**將訊息傳送給特定使用者**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>記憶體內部儲存體

下列範例示範如何在儲存在記憶體中的字典中保留連接和使用者資訊。 字典會使用 `HashSet` 來儲存連接識別碼。使用者在任何時候都可以有一個以上的 SignalR 應用程式連接。 例如，透過多個裝置或多個瀏覽器索引標籤連線的使用者，將會有一個以上的連接識別碼。

如果應用程式關閉，所有資訊都會遺失，但會在使用者重新建立連線時重新填入。 如果您的環境包含一部以上的網頁伺服器，記憶體內部儲存體將無法運作，因為每部伺服器都有個別的連接集合。

第一個範例顯示的類別會管理使用者與連接的對應。 HashSet 的索引鍵將會是使用者的名稱。

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

下一個範例顯示如何使用中樞的連接對應類別。 類別的實例會儲存在變數名稱中 `_connections` 。

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>單一使用者群組

您可以為每個使用者建立群組，然後當您只想要存取該使用者時，將訊息傳送至該群組。 每個群組的名稱都是使用者的名稱。 如果使用者有一個以上的連線，則每個連接識別碼都會新增至使用者的群組。

當使用者中斷連線時，您不應該從群組手動移除該使用者。 SignalR 架構會自動執行此動作。

下列範例顯示如何執行單一使用者群組。

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>永久的外部儲存體

本主題說明如何使用資料庫或 Azure 資料表儲存體來儲存連接資訊。 當您有多部網頁伺服器時，這個方法會運作，因為每一部網頁伺服器都可以與相同的資料存放庫互動。 如果您的 web 伺服器停止運作或應用程式重新開機，則 `OnDisconnected` 不會呼叫該方法。 因此，您的資料存放庫可能會有不再有效之連接識別碼的記錄。 若要清除這些孤立的記錄，您可能會想要讓任何在與您應用程式相關的時間範圍以外建立的連線失效。 本章節中的範例包含在建立連線時追蹤的值，但不會顯示如何清除舊的記錄，因為您可能會想要以背景進程的形式來進行。

### <a name="database"></a>資料庫

下列範例示範如何在資料庫中保留連接和使用者資訊。 您可以使用任何資料存取技術;但是，下列範例顯示如何使用 Entity Framework 定義模型。 這些實體模型會對應至資料庫資料表和欄位。 視應用程式的需求而定，您的資料結構可能會有很大的差異。

第一個範例顯示如何定義可以與許多連接實體相關聯的使用者實體。

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

然後，您可以從中樞使用如下所示的程式碼來追蹤每個連接的狀態。

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure 表格儲存體

下列 Azure 資料表儲存體範例類似于資料庫範例。 它不包含開始使用 Azure 資料表儲存體服務所需的所有資訊。 如需詳細資訊，請參閱 [如何使用 .net 的資料表儲存體](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)。

下列範例顯示用來儲存連接資訊的資料表實體。 它會依使用者名稱來分割資料，並依連線識別碼來識別每個實體，讓使用者可以隨時擁有多個連接。

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

在中樞內，您可以追蹤每個使用者連接的狀態。

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
