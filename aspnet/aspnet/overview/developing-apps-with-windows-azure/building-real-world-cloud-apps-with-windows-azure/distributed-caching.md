---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: 分散式緩存(使用 Azure 構建真實世界雲應用) |微軟文件
author: MikeWasson
description: 使用 Azure 電子書建構真實世界雲端應用基於 Scott Guthrie 開發的演示文稿。 它解釋了13種模式和做法,他可以...
ms.author: riande
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 87a7516415895e761d1589fd459b93e5c15c0f85
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676017"
---
# <a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>分散式緩存(使用 Azure 建構真實世界雲應用)

由[邁克·瓦森](https://github.com/MikeWasson),[里克·安德森](https://twitter.com/RickAndMSFT),[湯姆·戴克斯特拉](https://github.com/tdykstra)

[下載修復項目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 使用 Azure 電子書**建構真實世界雲端應用**基於 Scott Guthrie 開發的演示文稿。 它解釋了 13 種模式和做法,這些模式和做法可以説明您成功開發雲端的 Web 應用。 有關電子書的資訊,請參閱[第一章](introduction.md)。

上一章研究了瞬態故障處理,並提到緩存作為斷路器策略。 本章提供了有關緩存的更多背景,包括何時使用它、使用它的常見模式以及如何在 Azure 中實現緩存。

## <a name="what-is-distributed-caching"></a>什麼是分散式緩存

緩存通過將數據存儲在記憶體中,提供對通常訪問的應用程序數據的高輸送量、低延遲訪問。 對於雲端應用,最有用的緩存類型是分散式緩存,這意味著數據不是存儲在單個 Web 伺服器的記憶體上,而是存儲在其他雲端資源上,緩存的數據可供應用程式的所有 Web 伺服器(或應用程式使用的其他雲端 VM)使用。

![顯示存取同一快取伺服器的多個 Web 伺服器的圖表](distributed-caching/_static/image1.png)

當應用程式通過添加或刪除伺服器進行擴展,或者當伺服器由於升級或故障而更換時,緩存的數據仍可供運行該應用程式的每個伺服器訪問。

通過避免持久數據存儲的高延遲數據訪問,緩存可以顯著提高應用程式的回應能力。 例如,從緩存檢索數據比從關係資料庫檢索數據要快得多。

緩存的一個附帶好處是減少了持久數據存儲的流量,當持久數據存儲需要數據出口費用時,這可能會導致更低的成本。

## <a name="when-to-use-distributed-caching"></a>何時使用分散式快取

快取最適合使用比寫入資料更多的讀取工作負荷,以及當資料模型支援用於在快取中儲存和檢索資料的鍵/值組織時。 當應用程式使用者共用大量常見數據時,它也更有用;例如,如果每個使用者通常檢索該用戶獨有的數據,則緩存不會提供盡可能多的好處。 緩存可能非常有益的一個範例是產品目錄,因為資料不會頻繁更改,並且所有客戶都在查看相同的數據。

緩存的好處越來越可衡量,應用程式越擴展,持久數據存儲的輸送量限制和延遲延遲就對整體應用程式性能造成更大的限制。 但是,您可能出於其他原因實現緩存,而不是性能。 對於在向用戶顯示時不必完全最新的數據,緩存訪問可以作為斷路器,用於持久數據存儲無回應或不可用時的數據。

## <a name="popular-cache-population-strategies"></a>流行的快取填充原則

為了能夠從快取中檢索資料,您必須先將其儲存在該緩存中。 有幾種策略用於將資料放入快取中:

- 按需/快取旁

    應用程序嘗試從快取中檢索資料,當快取沒有資料("錯誤")時,應用程式將資料存儲在快取中,以便下次資料可用。 下次應用程序嘗試獲取相同的數據時,它會在緩存中找到它要查找的內容("命中")。 為了防止獲取資料庫中已更改的緩存數據,在更改數據存儲時使緩存無效。
- 背景推送

    後台服務會定期將數據推送到緩存中,並且應用始終從緩存中拉出。 此方法非常適合不需要始終返回最新數據的高延遲數據源。
- 斷路器

    應用程式通常直接與持久數據存儲通信,但當持久數據存儲存在可用性問題時,應用程式將從緩存中檢索數據。 數據可能已使用緩存旁或後台數據推送策略放入緩存中。 這是一種故障處理策略,而不是性能增強策略。

為了保持快取中的數據最新,可以在應用程式創建、更新或刪除資料時刪除相關的緩存條目。 如果應用程式有時可以獲取稍微過時的數據,則可以依靠可配置的過期時間來設置緩存數據可能有多舊的限制。

您可以設定絕對過期(自創建緩存項以來的時間量)或滑動過期(自上次存取緩存項以來的時間量)。 當您依賴於緩存過期機制以防止數據變得過於陳舊時,將使用絕對過期。 在 Fix It 應用中,我們將手動驅逐陳舊的緩存項,我們將使用滑動過期來將最新的數據保存在緩存中。 無論您選擇哪種過期策略,當達到緩存的記憶體限制時,緩存將自動驅逐最舊的(最近使用或 LRU)專案。

## <a name="sample-cache-aside-code-for-fix-it-app"></a>修復用應用程式的範例快取的程式碼

在以下示例代碼中,在檢索修復 It 任務時,我們首先檢查緩存。 如果在緩存中找到任務,我們會返回它;如果任務在緩存中找到,則返回它。如果未找到,我們會從資料庫中獲取它並將其存儲在緩存中。 要向`FindTaskByIdAsync`方法添加緩存所做的更改將突出顯示。

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

更新或刪除修復 It 工作時,必須使快取的任務無效(刪除)。 否則,將來嘗試讀取該任務將繼續從快取中獲取舊資料。

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

這些示例說明了簡單的緩存代碼;緩存尚未在可下載的修復 It 專案中實現。

## <a name="azure-caching-services"></a>Azure 快取服務

Azure 提供以下快取服務[:Azure Redis 快取](https://msdn.microsoft.com/library/dn690523.aspx)與[Azure 託管快取](https://msdn.microsoft.com/library/dn386094.aspx)。 Azure Redis 緩存基於流行的[開源 Redis 緩存](http://redis.io/),是大多數緩存方案的首選。

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>使用快取提供者ASP.NET工作階段狀態

如 Web[開發最佳實踐章節](web-development-best-practices.md)所述,最佳做法是避免使用會話狀態。 如果應用程式需要會話狀態,則下一個最佳做法是避免預設記憶體中提供程式,因為這不會啟用橫向擴展(Web 伺服器的多個實例)。 ASP.NET SQL Server 工作階段狀態提供程式使在多個 Web 伺服器上運行的網站能夠使用作業階段狀態,但與記憶體中提供程式相比,它會產生較高的延遲成本。 如果必須使用工作階段狀態,則最佳解決方案是使用快取提供者,例如[Azure 快取的作業階段狀態提供者](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)。

## <a name="summary"></a>總結

您已經看到 Fix It 應用如何實現緩存,以提高回應時間和可伸縮性,並使應用在資料庫不可用時繼續為讀取操作回應。 [在下一章](queue-centric-work-pattern.md)中,我們將介紹如何進一步提高可伸縮性,並使應用繼續對寫入操作進行回應。

## <a name="resources"></a>資源

有關緩存的詳細資訊,請參閱以下資源。

文件

- [Azure 快取](https://msdn.microsoft.com/library/gg278356.aspx)。 有關 Azure 快取的官方 MSDN 文檔。
- [微軟模式與實作 - Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 請參閱緩存指南和緩存放置模式。
- [容錯保護:彈性雲體系結構指南](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 馬克·默庫里、烏爾里希·霍曼和安德魯·湯希爾的白皮書。 請參閱有關緩存的部分。
- [Azure 雲服務上大規模服務設計的最佳做法](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 W. 馬克·西姆斯和邁克爾·托馬斯的白皮書。 請參閱有關分散式緩存的部分。
- [分散式緩存在可伸縮性路徑上](https://msdn.microsoft.com/magazine/dd942840.aspx)。 一篇較老的(2009)MSDN雜誌文章,但一般對分散式緩存的清晰書面介紹;比故障安全和最佳實踐白皮書的緩存部分更深入。

影片

- [容解安全:建譯可擴充的、有彈性的雲端服務](https://channel9.msdn.com/Series/FailSafe)。 由烏爾里希·霍曼、馬克·默庫里和馬克·西姆斯的九集系列。 提供如何構建雲應用的 400 級視圖。 本系列主要探討理論和原因;有關更多如何使用的詳細資訊,請參閱馬克·西姆斯的"建築大"系列。 請參閱第 3 集的緩存討論,從 1:24:14 開始。
- [建構大:從 Azure 客戶那裡吸取的教訓 - 第 I 部分](https://channel9.msdn.com/Events/Build/2012/3-029)。西蒙·戴維斯討論從46:00開始的分散式緩存。 類似於故障安全系列,但進入更多如何使用的詳細資訊。 該演示文稿於 2012 年 10 月 31 日提供,因此不包括 2013 年推出的 Azure 應用服務中的 Web 應用緩存服務。

程式碼範例

- [Azure 的雲服務基礎知識](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。 實現分散式緩存的範例應用程式。 請參閱隨附的博客文章[「雲服務基礎知識 + 緩存基礎知識](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx)」 "。

> [!div class="step-by-step"]
> [前一個](transient-fault-handling.md)
> [下一個](queue-centric-work-pattern.md)
