---
title: ASP.NET Core SignalR 實際執行裝載和擴充
author: bradygaster
description: 了解如何避免效能和調整使用 ASP.NET Core SignalR 應用程式中的問題。
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 11/28/2018
uid: signalr/scale
ms.openlocfilehash: 4ac4509acc89d0091a3757c7cfbc9981614f29ad
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037735"
---
# <a name="aspnet-core-signalr-hosting-and-scaling"></a>ASP.NET Core SignalR 裝載和擴充

藉由[Andrew Stanton-nurse](https://twitter.com/anurse)， [Brady Gaster](https://twitter.com/bradygaster)，並[Tom Dykstra](https://github.com/tdykstra)，

這篇文章說明裝載及調整高流量的應用程式使用 ASP.NET Core SignalR 的考量。

## <a name="tcp-connection-resources"></a>TCP 連線資源

僅限於 web 伺服器可支援的並行 TCP 連線數目。 使用標準的 HTTP 用戶端*暫時*連線。 用戶端進入閒置，並稍後再重新開啟時，就可以關閉這些連線。 相反地，SignalR 連線已*永續性*。 SignalR 連線保持開啟甚至當用戶端變成閒置時。 在許多用戶端提供服務的高流量應用程式，這些持續性連線可能會導致叫用其最大連接數目的伺服器。

持續連線也會使用一些額外的記憶體，來追蹤每個連線。

連線相關的資源，由 SignalR 大量使用可能會影響其他裝載在相同的伺服器的 web 應用程式。 當 SignalR 便會開啟，並保留最後一個可用的 TCP 連線時，在相同伺服器上的其他 web 應用程式也會有沒有更多的連線提供給他們。

當伺服器連線，您會看到隨機通訊端錯誤，以及連接重設錯誤。 例如: 

```
An attempt was made to access a socket in a way forbidden by its access permissions...
```

若要防止 SignalR 資源使用狀況導致錯誤，其他的 web 應用程式中，執行 SignalR 比其他 web 應用程式的不同伺服器上。

為了避免 SignalR 資源使用狀況導致錯誤的 SignalR 應用程式中，向外延展至限制的伺服器必須處理的連線數目。

## <a name="scale-out"></a>向外擴充

使用 SignalR 的應用程式需要追蹤的所有連線，這會建立伺服器陣列的問題。 新增伺服器，，然後它會取得其他伺服器不了解的新連線。 比方說下, 圖中的每部伺服器上的 SignalR 會察覺有其他伺服器上的連線。 當一部伺服器上的 SignalR 想要將訊息傳送至所有用戶端時，訊息只會連線到該伺服器的用戶端。

![調整 SignalR 後擋板沒有](scale/_static/scale-no-backplane.png)

解決此問題的選項都會[Azure SignalR 服務](#azure-signalr-service)並[Redis 後擋板](#redis-backplane)。

## <a name="azure-signalr-service"></a>Azure SignalR Service

Azure SignalR 服務是 proxy，而不是後擋板。 用戶端啟動連線到伺服器，每次用戶端重新導向連線到服務。 下圖說明這個程序：

![建立 Azure SignalR 服務的連接](scale/_static/azure-signalr-service-one-connection.png)

結果會是服務管理的所有用戶端連線，而每部伺服器都必須只有常數少數，連線至服務，如下圖所示：

![用戶端連接至服務，連接至服務的伺服器](scale/_static/azure-signalr-service-multiple-connections.png)

向外延展至這個方法有幾項優點 Redis 後擋板替代方案：

* 黏性工作階段，也稱為[用戶端親和性](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing#step-3---configure-client-affinity)，不需要，因為用戶端會立即重新導向至 Azure SignalR 服務連線時。
* SignalR，應用程式可以相應放大為基礎的 Azure SignalR 服務自動進行調整以處理任何數量的連線時傳送的訊息數目。 比方說，可能有數千個用戶端，但如果只傳送幾秒的訊息，SignalR 應用程式不需要向外延展至多部伺服器，只是為了處理本身的連線。
* SignalR 應用程式不會使用比沒有 SignalR 的 web 應用程式的更多連線資源。

基於這些理由，我們建議 Azure SignalR 服務的所有裝載於 Azure，包括應用程式服務、 Vm 和容器上的 ASP.NET Core SignalR 應用程式。

如需詳細資訊，請參閱[Azure SignalR 服務文件](/azure/azure-signalr/signalr-overview)。

## <a name="redis-backplane"></a>Redis 後擋板

[Redis](https://redis.io/)是記憶體中索引鍵-值存放區支援發行/訂閱模型的傳訊系統。 Redis 的 SignalR 後擋板會使用發佈/訂閱功能，將訊息轉送到其他伺服器。 當用戶端連接，連接資訊會傳遞至後擋板。 當伺服器想要將訊息傳送至所有用戶端時，它會傳送至後擋板。 後擋板知道所有已連線的用戶端和它們在上伺服器。 會透過其個別的伺服器的所有用戶端傳送的訊息。 下圖說明此程序：

![Redis 後擋板，從一部伺服器傳送至所有用戶端的訊息](scale/_static/redis-backplane.png)

Redis 後擋板是建議的向外延展方法，在您自己的基礎結構上託管的應用程式。 Azure SignalR 服務並不是實際的選項，用於在內部部署應用程式，因為您的資料中心與 Azure 資料中心之間的連線延遲時間與實際執行環境。

稍早所述 Azure SignalR 服務的優點是 Redis 後擋板的缺點：

* 黏性工作階段，也稱為[用戶端親和性](/iis/extensions/configuring-application-request-routing-arr/http-load-balancing-using-application-request-routing#step-3---configure-client-affinity)，需要。 一旦在伺服器啟動連線，連線內必須停留在該伺服器上。
* SignalR 應用程式必須相應放大的用戶端數量中，即使傳送一些訊息。
* SignalR 應用程式會使用比沒有 SignalR 的 web 應用程式的更多連線資源。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱下列資源：

* [Azure SignalR 服務文件](/azure/azure-signalr/signalr-overview)
* [設定 Redis 後擋板](xref:signalr/redis-backplane)
