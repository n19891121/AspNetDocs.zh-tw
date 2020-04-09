---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: 將訊號R使用者映射到連線 |微軟文件
author: bradygaster
description: 本主題演示如何保留有關使用者及其連接的資訊。 派翠克·弗萊徹説明寫了這個話題。 本主題中使用的軟體版本...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676157"
---
# <a name="mapping-signalr-users-to-connections"></a>將 SignalR 使用者對應至連線

 作者：[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主題演示如何保留有關使用者及其連接的資訊。
>
> 派翠克·弗萊徹説明寫了這個話題。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - 信號R版本 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主題的早期版本
>
> 有關早期版本的 SignalR 的資訊,請參閱[SignalR 舊版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>問題和評論
>
> 請留下反饋,關於你喜歡本教程的方式,以及我們可以在頁面底部的評論中改進什麼。 如果您有與本教學沒有直接關係的問題,您可以將它們發表到[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

## <a name="introduction"></a>簡介

連接到集線器的每個用戶端傳遞一個唯一的連接 ID。您可以在中心上下文的屬性中`Context.ConnectionId`檢索此值。 如果應用程式需要將使用者映射到連接 ID 並保留該映射,則可以使用以下方式之一:

- [使用者識別碼提供者 (信號器 2)](#IUserIdProvider)
- [記憶體中儲存](#inmemory),如字典
- [每個使用者的訊號R組](#groups)
- [永久外部儲存](#database),如資料庫表或 Azure 儲存

本主題中顯示了每個實現。 使用類`OnConnected``OnDisconnected`的`OnReconnected`和方法`Hub`來跟蹤使用者連接狀態。

最適合您的應用程式的方法取決於:

- 託管應用程式的 Web 伺服器數。
- 是否需要獲取當前連接的使用者的清單。
- 在應用程式或伺服器重新啟動時是否需要保留組和使用者資訊。
- 調用外部伺服器的延遲是否是一個問題。

下表顯示了哪種方法適用於這些注意事項。

|  | 多台伺服器 | 取得目前連線使用者的清單 | 重新啟動後保留資訊 | 最佳性能 |
| --- | --- | --- | --- | --- |
| 使用者識別碼提供者 | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| 記憶體內 |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| 單使用者群組 | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| 永久外部 | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>IUserID 供應商

此功能允許用戶透過新介面IUserIdProvider指定使用者Id基於IRequest的內容。

**IUserId 供應商**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

默認情況下,將有一個使用用戶`IPrincipal.Identity.Name`作為使用者名的實現。 要更改此項,請在應用程式啟動`IUserIdProvider`時向全域主機註冊實現:

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

從集線器中,您可以通過以下 API 向這些使用者發送訊息:

**傳送使用者傳送訊息**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>記憶體中儲存

以下範例展示如何在儲存在記憶體中的字典中保留連接和使用者資訊。 字典使用儲存`HashSet`連接ID。在任何時候,使用者都可以與 SignalR 應用程式建立多個連接。 例如,透過多個設備或多個瀏覽器選項卡連接的使用者將具有多個連接 ID。

如果應用程式關閉,所有資訊都將丟失,但在使用者重新建立其連接時將重新填充該資訊。 如果環境包含多個 Web 伺服器,則記憶體中儲存不起作用,因為每台伺服器都將具有單獨的連接集合。

第一個範例顯示了管理使用者映射到連接的類。 哈希集的鍵將是使用者名。

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

下一個範例展示如何使用中心的連接映射類。 類的實例存儲在變數名稱`_connections`中。

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>單使用者群組

您可以為每個使用者創建一個組,然後在您只想聯繫該使用者時向該組發送消息。 每個組的名稱是使用者的名稱。 如果使用者有多個連接,則每個連接 ID 將添加到使用者的組中。

當用戶斷開連接時,不應手動從組中刪除使用者。 此操作由 SignalR 框架自動執行。

下面的範例示範如何實現單使用者組。

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>永久外部儲存

本主題演示如何使用資料庫或 Azure 表儲存來儲存連接資訊。 當您有多個 Web 伺服器時,此方法有效,因為每個 Web 伺服器都可以與同一數據儲存庫進行交互。 如果 Web 伺服器停止工作或應用程式重新啟動,`OnDisconnected`則不調用該方法。 因此,數據存儲庫可能具有不再有效的連接ID記錄。 要清理這些孤立記錄,您可能希望使在與您的應用程式相關的時間範圍之外創建的任何連接無效。 本節中的範例包括用於跟蹤創建連接時間的值,但不顯示如何清理舊記錄,因為您可能希望作為後台進程執行此操作。

### <a name="database"></a>資料庫

以下範例展示如何在資料庫中保留連接和使用者資訊。 您可以使用任何數據存取技術;但是,下面的示例演示如何使用實體框架定義模型。 這些實體模型對應於資料庫表和欄位。 您的數據結構可能因應用程式的要求而有很大差異。

第一個範例展示如何定義可以與許多連接實體關聯的用戶實體。

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

然後,從集線器,您可以使用下面顯示的代碼跟蹤每個連接的狀態。

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure 表格儲存體

以下 Azure 表存儲範例與資料庫範例類似。 它不包括開始使用 Azure 表存儲服務所需的所有資訊。 有關詳細資訊,請參閱[如何使用 .NET 中的表儲存](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)。

下面的範例顯示了用於存儲連接資訊的表實體。 它按使用者名對數據進行分區,並通過連接 ID 標識每個實體,以便用戶可以隨時具有多個連接。

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

在集線器中,您可以追蹤每個使用者的連接狀態。

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
