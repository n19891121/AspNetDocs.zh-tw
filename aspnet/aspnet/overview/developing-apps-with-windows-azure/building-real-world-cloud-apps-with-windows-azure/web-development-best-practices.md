---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: " (使用 Azure) 建立 Real-World 雲端應用程式的 Web 開發最佳作法 |Microsoft Docs"
author: MikeWasson
description: 以 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會解釋13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: dfd8a3ac2328d3f17dfbe36e68b37d181177b0f4
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345506"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a> (使用 Azure) 建立 Real-World 雲端應用程式的 Web 開發最佳做法

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 或 [下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **以 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 它說明13個模式和實務，可協助您成功開發雲端 web 應用程式。 如需電子書的詳細資訊，請參閱 [第一章](introduction.md)。

前三個模式就是設定 agile 開發流程;其餘的則是關於架構和程式碼。 這是一系列的 網頁程式開發最佳做法：

- 智慧型負載平衡器後方的[無狀態 web 伺服器](#stateless)。
- 請[避免會話狀態](#sessionstate) (或者如果您無法避免，請使用分散式快取，而不是資料庫) 。
- [使用 CDN](#cdn) 將靜態檔案資產 (映射、腳本) 。
- [使用 .net 4.5 的非同步支援](#async) 來避免封鎖呼叫。

這些作法適用于所有 網頁程式開發，不只適用于雲端應用程式，但對於雲端應用程式來說特別重要。 它們會協助您更有效地使用這些由雲端環境提供的彈性調整空間。 如果您未遵循這些作法，當您嘗試調整應用程式時，將會遇到限制。

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>智慧型負載平衡器後方的無狀態 web 層

*無狀態 web 層* 表示您不會在 web 伺服器記憶體或檔案系統中儲存任何應用程式資料。 讓您的 web 層保持無狀態可讓您提供更好的客戶體驗並節省成本：

- 如果 web 層是無狀態的，且其位於負載平衡器後方，您可以藉由動態新增或移除伺服器，快速回應應用程式流量的變更。 在雲端環境中，只要您實際使用伺服器資源，只要使用這些資源，就能回應需求的變更，就能省下可觀的費用。
- 無狀態的 web 層在架構上，會比擴充應用程式更簡單。 這也可讓您更快速地回應調整需求，並在程式中減少開發和測試的金錢。
- 雲端伺服器（例如內部部署伺服器）必須偶爾修補和重新開機;而且，如果 web 層是無狀態的，當伺服器暫時關閉時，會重新路由傳送流量，並不會造成錯誤或非預期的行為。

大部分的真實世界應用程式都需要儲存 web 會話的狀態。此處的重點是不要將它儲存在 web 伺服器上。 您可以使用快取提供者，以其他方式（例如在 cookie 中的用戶端或超出進程的伺服器端） ASP.NET 會話狀態來儲存狀態。 您可以將檔案儲存在 [Windows Azure Blob 儲存體](unstructured-blob-storage.md) ，而不是儲存在本機檔案系統中。

例如，如果您的 web 層是無狀態，在 Windows Azure 網站中調整應用程式的難易度，請參閱管理入口網站中 Windows Azure 網站的 [ **調整** ] 索引標籤：

![調整索引標籤](web-development-best-practices/_static/image1.png)

如果您想要新增 web 伺服器，您可以直接將 [實例計數] 滑杆拖曳至右邊。 將它設定為5，然後按一下 [ **儲存**]，在幾秒內，Windows Azure 中有5部網頁伺服器處理您的網站流量。

![五個實例](web-development-best-practices/_static/image2.png)

您可以輕鬆地將實例計數設為3或向下設定為1。 當您相應減少時，會立即開始節省成本，因為 Windows Azure 會以分鐘為單位來收費，而不是以小時為單位。

您也可以告訴 Windows Azure 根據 CPU 使用量自動增加或減少網頁伺服器數目。 在下列範例中，當 CPU 使用率低於60% 時，web 伺服器的數目將降至最低為2，如果 CPU 使用量超過80%，則網頁伺服器的數目最多可增加到4。

![依 CPU 使用量調整規模](web-development-best-practices/_static/image3.png)

如果您知道您的網站只會在工作時間內忙碌，該怎麼辦？ 您可以告訴 Windows Azure 在白天執行多部伺服器，並減少為單一伺服器的夜晚、夜間和週末。 下列一系列的螢幕擷取畫面顯示如何設定網站，使其在上班時間（上午8點至下午5點）執行一部伺服器，以及4部伺服器。

![依排程調整規模](web-development-best-practices/_static/image4.png)

![設定排程時間](web-development-best-practices/_static/image5.png)

![日間排程](web-development-best-practices/_static/image6.png)

![Weeknight 排程](web-development-best-practices/_static/image7.png)

![週末排程](web-development-best-practices/_static/image8.png)

當然，這一切都可以在腳本中以及在入口網站中完成。

在 Windows Azure 中，您的應用程式向外延展的能力幾乎沒有限制，只要您避免阻礙動態新增或移除伺服器 Vm，只要讓 web 層保持無狀態即可。

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>避免會話狀態

在實際的雲端應用程式中，避免儲存使用者工作階段某種形式的狀態通常並非理想做法，但某些方法會比其他方法更加影響效能和延展性。 如果您需要儲存狀態，最好的方法是將狀態的數量控制得較低，並將其儲存在 Cookie 中。 如果這不可行，則下一個最佳解決方案是使用 ASP.NET 會話狀態搭配提供者來處理 [分散式記憶體](distributed-caching.md#sessionstate)內部快取。 從效能和延展性的觀點來看，最差的解決方法是使用資料庫備份的工作階段狀態提供者。

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>使用 CDN 來快取靜態檔案資產

CDN 是內容傳遞網路的縮寫。 您可將靜態檔案資產（例如影像和腳本檔案）提供給 CDN 提供者，而提供者會在世界各地的資料中心快取這些檔案，以便在使用者存取您的應用程式時，針對快取的資產取得相對快速的回應和低延遲。 這會加快網站的整體載入時間，並減少 web 伺服器的負載。 如果您觸及的物件是遍佈各地的物件，Cdn 就特別重要。

Windows Azure 具有 CDN，您可以在 Windows Azure 或任何 web 主控環境中執行的應用程式中使用其他 Cdn。

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>使用 .NET 4.5 的非同步支援來避免封鎖呼叫

.NET 4.5 強化了 c # 和 VB 程式設計語言，讓您更輕鬆地以非同步方式處理工作。 非同步程式設計的好處不只是在平行處理的情況下，例如當您想要同時啟動多個 web 服務呼叫時。 它也可讓您的 web 伺服器在高負載狀況下更有效率且可靠地執行。 Web 服務器的可用執行緒數目有限，而且當所有線程都在使用中時，在高負載情況下，連入要求必須等到執行緒釋放為止。 如果您的應用程式程式碼不會以非同步方式處理資料庫查詢和 web 服務呼叫等工作，則當伺服器正在等候 i/o 回應時，許多執行緒會不必要地進行系結。 這會限制伺服器在高負載情況下可以處理的流量量。 使用非同步程式設計時，等候 web 服務或資料庫傳回資料的執行緒會釋出以服務新的要求，直到收到的資料為止。 在忙碌的 web 伺服器中，可以立即處理數百或上千個要求，否則會等待中的執行緒釋放。

如您稍早所見，您可以輕鬆地減少處理網站的 web 伺服器數目，因為這樣會增加。 如此一來，如果伺服器可以達到更高的輸送量，您就不需要這麼多，而且您可以降低成本，因為指定的流量磁片區需要較少的伺服器，而不是其他。

.NET 4.5 非同步程式設計模型的支援包含在適用于 Web Form、MVC 和 Web API 的 ASP.NET 4.5;在 Entity Framework 6 和 [Windows AZURE 儲存體 API](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx)中。

### <a name="async-support-in-aspnet-45"></a>ASP.NET 4.5 中的非同步支援

在 ASP.NET 4.5 中，已將非同步程式設計的支援新增至語言，但也不只是 MVC、Web Form 和 Web API 架構。 例如，ASP.NET MVC 控制器動作方法會接收來自 web 要求的資料，並將資料傳遞至視圖，然後再建立要傳送至瀏覽器的 HTML。 動作方法通常需要從資料庫或 web 服務取得資料，才能將它顯示在網頁中，或是儲存在網頁中輸入的資料。 在這些案例中，您可以輕鬆地將動作方法設為非同步：而不是傳回*ActionResult*物件，而是傳回工作* &lt; ActionResult &gt; * ，並使用*async*關鍵字來標記方法。 在方法內部，當程式程式碼啟動涉及等候時間的作業時，您會使用 await 關鍵字來標示它。

以下是一個簡單的動作方法，它會呼叫資料庫查詢的儲存機制方法：

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

以下是以非同步方式處理資料庫呼叫的相同方法：

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

在幕後，編譯器會產生適當的非同步程式碼。 當應用程式進行呼叫時 `FindTaskByIdAsync` ，ASP.NET 會提出 `FindTask` 要求，然後回溯工作者執行緒，讓它可以處理另一個要求。 當 `FindTask` 要求完成時，執行緒會重新開機以繼續處理該呼叫之後的程式碼。 在 `FindTask` 起始要求和傳回資料之間的過渡期間，您可以使用執行緒來執行有用的工作，否則會將其系結至等候回應。

非同步程式碼會有一些額外負荷，但在低負載的情況下，這會造成額外負荷，但在高負載情況下，您可以處理要求，否則會等待可用的執行緒。

從 ASP.NET 1.1 開始，您可以執行這種非同步程式設計，但很難撰寫、容易出錯，而且難以進行調試。 既然我們已簡化 ASP.NET 4.5 中的程式碼撰寫程式碼，就不需要再這麼做。

### <a name="async-support-in-entity-framework-6"></a>Entity Framework 6 中的非同步支援

在4.5 的非同步支援中，我們已針對 web 服務呼叫、通訊端和檔案系統 i/o 提供非同步支援，但最常見的 web 應用程式模式就是叫用資料庫，而我們的資料連結庫不支援非同步。 現在 Entity Framework 6 新增資料庫存取的非同步支援。

在 Entity Framework 6 中，會將查詢或命令傳送至資料庫的所有方法都有非同步版本。 此處的範例會顯示 *Find* 方法的非同步版本。

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

這種非同步支援不僅適用于插入、刪除、更新和簡單尋找，也適用于 LINQ 查詢：

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

方法有一個 `Async` 版本， `ToList` 因為在此程式碼中，會導致將查詢傳送到資料庫的方法。 `Where`和 `OrderByDescending` 方法只會設定查詢，而方法會 `ToListAsync` 執行查詢並將回應儲存在 `result` 變數中。

## <a name="summary"></a>摘要

您可以在任何 web 程式設計架構和雲端環境中，執行此處所述的 網頁程式開發最佳做法，但我們在 ASP.NET 和 Windows Azure 中有工具可讓您輕鬆進行。 如果您遵循這些模式，您可以輕鬆地向外延展您的 web 層，並將您的費用降到最低，因為每部伺服器都可以處理更多流量。

[下一章](single-sign-on.md)探討雲端如何啟用單一登入案例。

## <a name="resources"></a>資源

如需詳細資訊，請參閱下列資源。

無狀態的 web 伺服器：

- [Microsoft 模式和實務-](https://msdn.microsoft.com/library/dn589774.aspx)自動調整指引。
- [在 Windows Azure 網站中停用 ARR 的實例親和性](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/)。 Erez Benari 撰寫的 Blog 文章會說明 Windows Azure 網站中的會話親和性。

Cdn：

- [安全：建立可調整的彈性雲端服務](https://channel9.msdn.com/Series/FailSafe)。 九部影片系列，Ulrich Homann、Marc Mercuri 和 Mark Simm。 請參閱第3集的 CDN 討論，起價為1:34:00。
- [Microsoft 模式和實務靜態內容裝載模式](https://msdn.microsoft.com/library/dn589776.aspx)
- [CDN 評論](http://www.cdnreviews.com/)。 許多 Cdn 的總覽。

非同步程式設計：

- [使用 ASP.NET MVC 4 中的非同步方法](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。 依 Rick Anderson 的教學課程。
- [使用 Async 和 Await 進行非同步程式設計 (c # 和 Visual Basic) ](https://msdn.microsoft.com/library/vstudio/hh191443.aspx)。 MSDN 白皮書，說明非同步程式設計的基本原理、其在 ASP.NET 4.5 中的運作方式，以及如何撰寫程式碼來加以執行。
- [Entity Framework Async 查詢並儲存](https://msdn.microsoft.com/data/jj819165)
- [如何使用 Async 建立 ASP.NET Web 應用程式](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7)。 Rowan 莎莎的影片簡報。 包含在高負載狀況下，非同步程式設計如何有助於大幅增加網頁伺服器輸送量的圖形示範。
- [安全：建立可調整的彈性雲端服務](https://channel9.msdn.com/Series/FailSafe)。 九部影片系列，Ulrich Homann、Marc Mercuri 和 Mark Simm。 如需非同步程式設計對擴充性影響的討論，請參閱第4集和第8集。
- [使用 ASP.NET 4.5 中非同步方法的神奇之處加上重要的陷阱](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx)。 Scott Hanselman 的 Blog 文章，主要是在 ASP.NET Web Forms 應用程式中使用 async。

如需其他 網頁程式開發的最佳作法，請參閱下列資源：

- [修正應用程式範例應用程式-最佳作法](the-fix-it-sample-application.md#bestpractices)。 這本電子書的附錄列出了在修正 It 應用程式中所實行的一些最佳作法。
- [Web 開發人員檢查清單](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [上一個](continuous-integration-and-continuous-delivery.md) 
> [下一步](single-sign-on.md)
