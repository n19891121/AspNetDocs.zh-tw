---
uid: mvc/overview/older-versions-1/overview/asp-net-mvc-overview
title: ASP.NET MVC 概述 |微軟文件
author: rick-anderson
description: 瞭解ASP.NET MVC 應用程式和 ASP.NET Web 窗體應用程式之間的差異。 瞭解如何決定何時構建ASP.NET MVC 應用程式。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2dcb44a4-5cbf-4d62-b363-718104082d86
msc.legacyurl: /mvc/overview/older-versions-1/overview/asp-net-mvc-overview
msc.type: authoredcontent
ms.openlocfilehash: 84810f168faa2e79a65ff3fb75e3654828bdb58f
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541009"
---
# <a name="aspnet-mvc-overview"></a>ASP.NET MVC 概觀

由[微軟](https://github.com/microsoft)

> 瞭解ASP.NET MVC 應用程式和 ASP.NET Web 窗體應用程式之間的差異。 瞭解如何決定何時構建ASP.NET MVC 應用程式。

模型檢視控制器 (Model-View-Controller，MVC) 架構模式會將應用程式分成三個主要元件：模型、檢視和控制器。 ASP.NET MVC 框架提供了ASP.NET Web 窗體模式的替代方法,用於創建基於 MVC 的 Web 應用程式。 ASP.NET MVC 架構是可高度測試的輕量型呈現架構，其中 (如同搭配 Web Form 應用程式) 整合了現有 ASP.NET 功能，例如主版頁面和成員資格驗證。 MVC 框架在**System.Web.Mvc**命名空間中定義,是**System.Web**命名空間中一個基本的、受支援的一部分。   
  
MVC 是許多開發人員熟悉的標準設計模式。 有些類型的 Web 應用程式將受益於 MVC 架構。 有些則繼續使用仰賴 Web Form 和回傳的傳統 ASP.NET 應用程式模式。 還有一些類型的 Web 應用程式將合併兩種方式；兩種方式並不互斥。   
  
MVC 架構包括下列元件：

[![呼叫需要參數值的控制器操作](asp-net-mvc-overview/_static/image1.jpg)](asp-net-mvc-overview/_static/image1.png)

**圖 01**: 呼叫需要參數值的控制器操作 ([按下以檢視全尺寸影像](asp-net-mvc-overview/_static/image2.png))

- **模型**。 模型對象是實現應用程序資料域邏輯的應用程式部分。 通常，模型物件會擷取和儲存資料庫中的模型狀態。 例如,Product 物件可能會從資料庫中檢索資訊,對資料庫進行操作,然後將更新的資訊寫回 SQL Server 中的 Product 表。

在小型應用程式中，模型通常是概念上的分隔而不是實體分隔。 例如,如果應用程式唯讀取資料集並將其發送到檢視,則應用程式沒有物理模型層和相關類。 在這種情況下,數據集將承擔模型物件的角色。

- **檢視 .** 視圖是顯示應用程式使用者介面 (UI) 的元件。 通常此 UI 是從模型資料建立。 例如,產品表的編輯檢視,該表根據 Products 物件的當前狀態顯示文本框、下拉清單和複選框。

- **控制器**. 控制器就是元件，可以處理使用者互動、使用模型並且在最後選擇可以轉譯要顯示 UI 的檢視。 在 MVC 應用程式中，檢視只會顯示資訊，而控制器則會處理及回應使用者輸入和互動。 例如,控制器處理查詢字串值,並將這些值傳遞給模型,模型又通過使用這些值查詢資料庫。

MVC 模式可幫助您建立分隔應用程式不同方面 (輸入邏輯、商務邏輯和 UI 邏輯) 的應用程式，同時在這些項目之間提供鬆散的結合。 此模式會指定每一種邏輯必須出現在應用程式中的位置。 UI 邏輯位於檢視。 輸入邏輯位於控制器。 商務邏輯則位於模型。 此分隔可幫助您在建置應用程式時管理複雜性，因為它可讓您一次專注於實作的一個方面。 例如，您可以專注在檢視上，而不需倚賴商務邏輯。   
  
除了管理複雜性之外，MVC 模式在測試應用程式上，比測試 Web Form ASP.NET Web 應用程式更為容易。 例如，在 Web Form ASP.NET Web 應用程式中，一個類別可以同時用來顯示輸出和回應使用者輸入。 為 Web Form ASP.NET 應用程式撰寫自動化測試可能相當複雜，因為您必須具現化網頁類別、類別的所有子控制項，以及應用程式中其他相依的類別，才能測試個別網頁。 由於必須具現化許多類別才能執行網頁，因此要撰寫應用程式的個別部分專用的測試並不容易。 因此，實作 Web Form ASP.NET 應用程式的測試可能比在 MVC 應用程式中進行測試更困難。 此外，Web Form ASP.NET 應用程式中的測試需要 Web 伺服器。 MVC 架構會解除元件之間的連結，並且大量使用介面，介面可讓個別元件獨立於架構的其他部分進行測試。   
  
MVC 應用程式三個主要元件之間的鬆散結合也有助於提升平行開發的效率。 例如,一個開發人員可以處理視圖,第二個開發人員可以處理控制器邏輯,第三個開發人員可以專注於模型中的業務邏輯。

## <a name="deciding-when-to-create-an-mvc-application"></a>決定何時建立 MVC 應用程式

您必須仔細考量要使用 ASP.NET MVC 架構或 ASP.NET Web Form 模型實作 Web 應用程式。 MVC 架構不會取代 Web Form 模型；因此您可以針對 Web 應用程式使用任一種架構  (如果您有現成的 Web Form 應用程式，這些應用程式會繼續如往常般執行)。   
  
在您決定針對特定網站使用 MVC 架構或 Web Form 模型之前，務必謹慎評估兩種方式的優勢。

### <a name="advantages-of-an-mvc-based-web-application"></a>MVC Web 應用程式的優點

ASP.NET MVC 架構提供下列優點：

- 透過將應用程式細分成模型、檢視和控制器的方式，讓管理複雜性更為容易。
- 此架構不使用檢視狀態或伺服器表單。 因此對於想要完全掌控應用程式行為的開發人員來說，MVC 架構相當理想。
- 此架構使用前端控制器模式，透過單一控制器處理 Web 應用程式要求。 如此可讓您設計支援豐富的路由基礎結構的應用程式。 有關詳細資訊,請參閱 MSDN 網站上的[前控制器](https://go.microsoft.com/fwlink/?LinkId=106357 "前控制器")。
- 能為測試為導向的開發工作 (Test-Driven Development，TDD) 提供更佳的支援。
- 它適用於需要對應用程式行為進行高度控制的開發人員和 Web 設計人員的大型團隊支援的 Web 應用程式。

### <a name="advantages-of-a-web-forms-based-web-application"></a>Web Form Web 應用程式的優點

Web Form 架構提供下列優點：

- 支援事件模型，會在 HTTP 上保留狀態，有益於業務線 Web 應用程式開發工作。 Web Form 應用程式提供數百種伺服器控制項中支援的許多種事件。
- 使用頁面控制器模式將功能加入至個別頁面。 有關詳細資訊,請參閱 MSDN 網站上的[網頁控制器](https://go.microsoft.com/fwlink/?LinkId=106359 "頁面控制器")。
- 它使用檢視狀態或基於伺服器的窗體,這可以使管理狀態資訊更容易。
- 適用於希望利用提供的大量元件快速開發應用程式的小型 Web 開發人員和設計人員團隊。
- 通常,應用程式開發不太複雜,因為元件 **(Page**類、控件等)集成緊密,通常需要比 MVC 模型更少的代碼。

## <a name="features-of-the-aspnet-mvc-framework"></a>ASP.NET MVC 架構的功能

ASP.NET MVC 架構提供下列功能：

- 默認情況下,應用程式任務(輸入邏輯、業務邏輯和 UI 邏輯)、可測試性和測試驅動開發 (TDD) 分離。 MVC 架構中的所有核心合約都是以介面為主，而且可以使用模擬物件測試，模擬物件是模仿應用程式中實際物件之行為的模擬物件。 您可以對應用程式進行單元測試，而不需在 ASP.NET 程序中執行控制器，如此使單元測試迅速而靈活。 您可以使用與 .NET Framework 相容的任何單元測試架構。
- 可擴充且可插入的架構。 ASP.NET MVC 架構的元件設計為能夠輕鬆取代或自訂。 您可以外掛自己的檢視引擎、URL 路由原則、動作方法參數序列化，以及其他元件。 ASP.NET MVC 架構還支援使用「相依性插入」(Dependency Injection，DI) 和「控制項反轉」(Inversion of Control，IOC) 容器模型。 DI 允許您將物件注入到類中,而不是依賴類來創建物件本身。 IOC 會指定，如果物件需要另一個物件，則第一個物件應從來源外部 (例如組態檔) 取得第二個物件。 如此可讓測試更為容易。
- 強大的 URL 映射元件,允許您建構具有可理解和可搜尋 URL 的應用程式。 URL 不必包含副檔名且設計為支援 URL 命名模式，適用於搜尋引擎最佳化 (Search Engine Optimization，SEO) 和代表性狀態傳輸 (Representational State Transfer，REST) 定址。
- 支援在現有 ASP.NET 網頁 (.aspx 檔)、使用者控制項 (.ascx 檔) 和主版頁面 (.master 檔) 標記檔中使用標記做為檢視範本。 您可以將現有ASP.NET功能與ASP.NET MVC 框架一起使用,例如嵌套母版頁、內聯運算式&lt;&gt;(%= %)、聲明性伺服器控制項、範本、資料綁定、當地語系化等。
- 支援現有的 ASP.NET 功能。 ASP.NET MVC 可讓您使用許多功能，例如表單驗證和 Windows 驗證、URL 授權、成員資格和角色、輸出和資料快取、工作階段和設定檔狀態管理、健康狀態監控、組態系統及提供者架構。
