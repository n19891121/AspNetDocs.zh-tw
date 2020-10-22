---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: 分散式快取 (使用 Azure) 建立 Real-World 雲端應用程式 |Microsoft Docs
author: MikeWasson
description: 以 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會解釋13個模式和實務，
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 87a7516415895e761d1589fd459b93e5c15c0f85
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345524"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>分散式快取 (使用 Azure) 建立 Real-World 雲端應用程式

[Mike Wasson](https://github.com/MikeWasson)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Tom Dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 或 [下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **以 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 它說明13個模式和實務，可協助您成功開發雲端 web 應用程式。 如需電子書的詳細資訊，請參閱 [第一章](introduction.md)。

上一章探討暫時性錯誤處理和提及的快取做為斷路器策略。 本章提供有關快取的更多背景資訊，包括使用時機、使用它的一般模式，以及如何在 Azure 中執行。

## <a name="what-is-distributed-caching"></a>什麼是分散式快取

快取可讓您將資料儲存在記憶體中，以提供高輸送量、低延遲的存取權，存取經常存取的應用程式資料。 對於雲端應用程式而言，最有用的快取類型是分散式快取，這表示資料不會儲存在個別的 web 伺服器記憶體中，而是儲存在其他雲端資源上，而且會將快取的資料提供給應用程式) 所使用的所有應用程式 web 伺服器 (或其他雲端 Vm。

![顯示多部網頁伺服器存取相同快取伺服器的圖表](distributed-caching/_static/image1.png)

當應用程式透過新增或移除伺服器來調整規模，或由於升級或錯誤而取代伺服器時，快取的資料仍可供執行應用程式的每一部伺服器存取。

藉由避免持續性資料存放區的高延遲資料存取，快取可以大幅改善應用程式的回應性。 例如，從快取中抓取資料的速度，會比從關係資料庫取出資料快得多。

快取的一項好處是減少持續性資料存放區的流量，當持續性資料存放區有資料輸出費用時，這可能會降低成本。

## <a name="when-to-use-distributed-caching"></a>使用分散式快取的時機

快取最適合用於執行比寫入資料更多讀取的應用程式工作負載，以及資料模型支援您用來在快取中儲存和取出資料的索引鍵/值組織。 當應用程式使用者共用許多常見的資料時，也會更有用;例如，如果每個使用者通常會抓取該使用者專屬的資料，則快取不會提供許多優點。 快取可能很有説明的範例是產品目錄，因為資料不會經常變更，而且所有客戶都會查看相同的資料。

快取的優點逐漸增加了應用程式的規模，因為持續性資料存放區的輸送量限制和延遲延遲會成為整體應用程式效能的限制。 不過，您也可以針對其他原因來執行快取，而不是效能。 對於向使用者顯示的資料不一定是最新的資料，當持續性資料存放區沒有回應或無法使用時，快取存取可作為斷路器。

## <a name="popular-cache-population-strategies"></a>常用的快取擴展策略

為了能夠從快取中取出資料，您必須先將資料儲存在該處。 有幾個策略可將您需要的資料放入快取中：

- 視需要/快取

    應用程式會嘗試從快取中取出資料，而且當快取的資料沒有 (「) 遺漏」的資料時，應用程式會將資料儲存在快取中，以便下一次可供使用。 當應用程式下次嘗試取得相同的資料時，它會在快取中找到它要尋找的內容 (「點擊」 ) 。 為了避免提取資料庫上已變更的快取資料，您會在對資料存放區進行變更時使快取失效。
- 背景資料推送

    背景服務會定期將資料推送至快取，而應用程式一律會從快取中提取。 這種方法適用于高延遲的資料來源，不需要您一律傳回最新的資料。
- 斷路器

    應用程式通常會直接與持續性資料存放區通訊，但當持續性資料存放區有可用性問題時，應用程式就會從快取中取出資料。 資料可能已使用另行快取或背景資料推送策略放置於快取中。 這是一項錯誤處理策略，而不是效能增強策略。

若要將資料保留在目前的快取中，您可以在應用程式建立、更新或刪除資料時，刪除相關的快取專案。 如果您的應用程式有時可以取得稍微過期的資料，您可以依賴可設定的到期時間來設定舊快取資料的限制。

您可以設定從快取專案建立以來的絕對到期時間 (時間量) 或自上次) 存取快取專案之後 (的時間長度。 當您根據快取到期機制來防止資料變成過時時，會使用絕對到期。 在修正 It 應用程式中，我們將手動收回過時的快取專案，並使用滑動期限將最新資料保留在快取中。 無論您選擇的到期原則為何，快取都會在達到快取的記憶體限制時，自動收回最舊的 (最近最少使用或 LRU) 專案。

## <a name="sample-cache-aside-code-for-fix-it-app"></a>用來修正 It 應用程式的快取程式碼範例

在下列範例程式碼中，我們會先檢查快取，然後再進行修正。 如果在快取中找到此工作，我們會將它傳回;如果找不到，我們會從資料庫取得，並將它儲存在快取中。 您要將快取新增至方法所做的變更， `FindTaskByIdAsync` 會反白顯示。

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

當您更新或刪除修正 It 工作時，您必須使 (移除) 快取的工作。 否則，未來嘗試讀取該工作將會繼續從快取中取得舊的資料。

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

這些範例可說明簡單的快取程式碼;尚未在可下載的 Fix It 專案中實行快取。

## <a name="azure-caching-services"></a>Azure 快取服務

Azure 提供下列快取服務： [Azure Redis](https://msdn.microsoft.com/library/dn690523.aspx) 快取和 [azure 受控](https://msdn.microsoft.com/library/dn386094.aspx)快取。 Azure Redis 快取是以常用的 [開放原始碼 Redis](http://redis.io/) 快取為基礎，而且是大部分快取案例的第一個選擇。

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>使用快取提供者 ASP.NET 會話狀態

如「網頁程式 [開發最佳做法」一章](web-development-best-practices.md)所述，最佳作法是避免使用會話狀態。 如果您的應用程式需要會話狀態，則下一個最佳作法是避免預設的記憶體內部提供者，因為這不會讓 (多個 web 伺服器實例) 。 ASP.NET SQL Server 會話狀態提供者可讓在多部網頁伺服器上執行的網站使用會話狀態，但相較于記憶體中的提供者，它會產生高延遲的成本。 如果您必須使用「快取」提供者（例如 Azure 快取的 [會話狀態提供者](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)），最好的解決方案就是使用「會話狀態」。

## <a name="summary"></a>摘要

您已瞭解修正 It 應用程式如何執行快取，以改善回應時間和擴充性，並讓應用程式能夠在資料庫無法使用時，繼續回應讀取作業。 在 [下一章](queue-centric-work-pattern.md) 中，我們將示範如何進一步改善擴充性，並讓應用程式繼續回應寫入作業。

## <a name="resources"></a>資源

如需快取的詳細資訊，請參閱下列資源。

文件

- [Azure](https://msdn.microsoft.com/library/gg278356.aspx)快取。 有關在 Azure 中快取的官方 MSDN 檔。
- [Microsoft 模式和實務-Azure 指引](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱快取指引和 Cache-Aside 模式。
- [安全：恢復雲端架構的指引](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 Marc Mercuri、Ulrich Homann 和 Andrew Townhill 的白皮書。 請參閱快取一節。
- [Azure 雲端服務上 Large-Scale 服務設計的最佳做法](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 W. 以標記 Simm 和 Michael Thomassy 的白皮書。 請參閱分散式快取一節。
- 在擴充[性的路徑上進行分散式](https://msdn.microsoft.com/magazine/dd942840.aspx)快取。 舊版的 (2009) MSDN 雜誌文章，但在一般情況下已清楚撰寫分散式快取的簡介;更深入的探討：安全和最佳作法白皮書的快取區段。

影片

- [安全：建立可調整的彈性雲端服務](https://channel9.msdn.com/Series/FailSafe)。 Ulrich Homann、Marc Mercuri 和 Mark Simm 的九部分系列。 提供如何設計雲端應用程式的400層級觀點。 本系列著重于理論和理由;如需詳細資訊，請參閱以標記 Simm 建立大型數列。 請參閱第3集的快取討論，起價為1:24:14。
- [打造 Big：從 Azure 客戶學習的課程-第一部分](https://channel9.msdn.com/Events/Build/2012/3-029)。Simon Davies 將討論從46:00 開始的分散式快取。 類似于安全性群組，但深入探討如何詳細資料。 此簡報已于2012年10月31日推出，因此未涵蓋2013中所導入 Azure App Service Web Apps 的快取服務。

程式碼範例

- [Azure 中的雲端服務基本](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)概念。 執行分散式快取的範例應用程式。 請參閱隨附的「 [雲端服務基本概念-快取基本知識](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx)」文章。

> [!div class="step-by-step"]
> [上一個](transient-fault-handling.md) 
> [下一步](queue-centric-work-pattern.md)
