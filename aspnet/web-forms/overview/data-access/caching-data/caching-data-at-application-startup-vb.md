---
uid: web-forms/overview/data-access/caching-data/caching-data-at-application-startup-vb
title: 在應用程式啟動時快取資料（VB） |Microsoft Docs
author: rick-anderson
description: 在任何 Web 應用程式中，會經常使用某些資料，而某些資料則不常使用。 我們可以改善 ASP.NET 應用程式 b 的效能 。
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 84afe4ac-cc53-4f2e-a867-27eaf692c2df
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-at-application-startup-vb
msc.type: authoredcontent
ms.openlocfilehash: 6c07b565329ab17496d2436f4c35bc4507694ed8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78576850"
---
# <a name="caching-data-at-application-startup-vb"></a>在應用程式啟動時快取資料 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載 PDF](caching-data-at-application-startup-vb/_static/datatutorial60vb1.pdf)

> 在任何 Web 應用程式中，會經常使用某些資料，而某些資料則不常使用。 我們可以預先載入經常使用的資料，這是一種稱為的技術，藉此改善 ASP.NET 應用程式的效能。 本教學課程示範主動式載入的其中一個方法，也就是在應用程式啟動時將資料載入快取中。

## <a name="introduction"></a>簡介

先前的兩個教學課程探討了如何在簡報和快取層中快取資料。 在[使用 objectdatasource](caching-data-with-the-objectdatasource-vb.md)快取資料時，我們探討了如何使用 objectdatasource 的快取功能來快取展示層中的資料。 在[架構中](caching-data-in-the-architecture-vb.md)快取資料會在新的個別快取層中檢查快取。 這兩個教學課程都在使用資料快取時使用了*被動式載入*。 使用被動式載入時，每次要求資料時，系統會先檢查快取中是否有。 如果不是，它會從原始來源抓取資料，例如資料庫，然後將它儲存在快取中。 被動式載入的主要優點是它的輕鬆執行。 其中一個缺點是它在要求之間的效能不平均。 假設有一個頁面使用上一個教學課程中的快取層來顯示產品資訊。 第一次造訪此頁面時，或在快取資料因為記憶體限制而收回或已達到指定的到期後第一次流覽時，必須從資料庫中取出資料。 因此，這些使用者的要求將會比快取所能提供的使用者要求更長的時間。

*主動式載入*提供替代的快取管理原則，藉由在需要時載入快取的資料，在要求之間平滑效能。 一般來說，主動式載入會使用一些進程，定期檢查或在更新基礎資料時收到通知。 然後，此程式會更新快取，使其保持在最新的。 如果基礎資料來自緩慢的資料庫連接、Web 服務或其他一些特別緩慢的資料來源，主動式載入就特別有用。 但這種主動式載入方法比較難以實現，因為它需要建立、管理和部署處理常式以檢查變更並更新快取。

在應用程式啟動時將資料載入快取中的另一種主動式載入類別，以及我們將在本教學課程中探索的類型。 這種方法特別適用于快取靜態資料，例如資料庫查閱資料表中的記錄。

> [!NOTE]
> 如需深入瞭解主動式和被動式載入之間的差異，以及優缺點的詳細資訊、缺點和實施建議，請參閱[.NET Framework 應用程式](https://msdn.microsoft.com/library/ms978498.aspx)的快取架構指南的管理快取的[內容](https://msdn.microsoft.com/library/ms978503.aspx)一節。

## <a name="step-1-determining-what-data-to-cache-at-application-startup"></a>步驟1：決定要在應用程式啟動時快取的資料

使用在前兩個教學課程中所檢查的「回應式載入」的快取範例，適用于可能定期變更且不會花費 exorbitantly 長時間產生的資料。 但是，如果快取的資料永遠不會變更，則被動式載入所使用的過期就是多餘的。 同樣地，如果要快取的資料花很長的時間來產生，則在抓取基礎資料時，要求將快取設為空白的使用者就必須忍受冗長的等候。 請考慮快取在應用程式啟動時，需要很長時間才會產生的靜態資料和資料。

雖然資料庫有許多動態且經常變更的值，但大部分也有相當大量的靜態資料。 例如，幾乎所有的資料模型都有一或多個資料行，其中包含一組固定選擇的特定值。 `Patients` 資料庫資料表可能有 `PrimaryLanguage` 的資料行，其值的集合可以是英文、西班牙文、法文、俄文、日文等等。 這些類型的資料行經常使用*查閱資料表*來執行。 並不是將字串英文或法文儲存在 `Patients` 資料表中，而是建立第二個數據表，其中通常包含兩個數據行-唯一識別碼和字串描述，並具有每個可能值的記錄。 `Patients` 資料表中的 `PrimaryLanguage` 資料行，會將對應的唯一識別碼儲存在查閱資料表中。 在 [圖 1] 中，患者 John Doe s 主要語言是英文，而 Ed Johnson s 是俄文。

![[語言] 資料表是病人資料表所使用的查閱資料表](caching-data-at-application-startup-vb/_static/image1.png)

**圖 1**： `Languages` 資料表是 `Patients` 資料表所使用的查閱資料表

編輯或建立新患者的使用者介面，會包含 [`Languages`] 資料表中的記錄所填入的允許語言下拉式清單。 在沒有快取的情況下，每次造訪此介面時，系統都必須查詢 `Languages` 資料表。 這很浪費和不必要，因為如果有的話，查閱資料表值不常變更。

我們可以使用先前教學課程中所檢查的相同「回應式載入」技術，來快取 `Languages` 的資料。 不過，被動式載入會使用以時間為基礎的到期日，這不是靜態查閱資料表資料所需的。 雖然使用「被動」載入的快取比完全沒有 caching，但最好的方法是在應用程式啟動時主動將查閱資料表資料載入快取中。

在本教學課程中，我們將探討如何快取查閱資料表資料和其他靜態資訊。

## <a name="step-2-examining-the-different-ways-to-cache-data"></a>步驟2：檢查快取資料的不同方式

您可以使用各種方法，以程式設計方式在 ASP.NET 應用程式中快取資訊。 我們已瞭解如何在先前的教學課程中使用資料快取。 或者，可以使用*靜態成員*或*應用程式狀態*，以程式設計方式快取物件。

使用類別時，通常必須先將類別具現化，才能存取其成員。 例如，若要從我們的商務邏輯層中的其中一個類別叫用方法，我們必須先建立類別的實例：

[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample1.vb)]

在我們可以叫用*SomeMethod*或使用*SomeProperty*之前，我們必須先使用 `New` 關鍵字來建立類別的實例。 *SomeMethod*和*SomeProperty*會與特定實例相關聯。 這些成員的存留期會系結至其相關聯物件的存留期。 另一方面，*靜態成員*是在類別的*所有*實例之間共用的變數、屬性和方法，因此，其存留期會與類別相同。 靜態成員是以關鍵字 `Shared`表示。

除了靜態成員之外，還可以使用應用程式狀態來快取資料。 每個 ASP.NET 應用程式都會維護一個名稱/值集合，其會在應用程式的所有使用者和頁面之間共用。 您可以使用[`HttpContext` 類別](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)的[`Application` 屬性](https://msdn.microsoft.com/library/system.web.httpcontext.application.aspx)來存取這個集合，並從 ASP.NET 網頁的程式碼後置類別中使用，如下所示：

[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample2.vb)]

資料快取可提供更豐富的 API 來快取資料、提供時間和相依性 expiries 的機制、快取專案優先順序等等。 使用靜態成員和應用程式狀態時，網頁開發人員必須手動加入這類功能。 不過，在應用程式啟動時快取資料以在應用程式的存留期間，資料快取的優點是想法。 在本教學課程中，我們將探討使用這三種方法來快取靜態資料的程式碼。

## <a name="step-3-caching-thesupplierstable-data"></a>步驟3：快取`Suppliers`資料表資料

我們已實作為日期的 Northwind 資料庫資料表不包含任何傳統查閱資料表。 這四個 Datatable 在 DAL 中實作為所有模型資料表，其值為非靜態。 在此教學課程中，您不需要花費時間將新的 DataTable 新增至 DAL，然後將新的類別和方法加入到 BLL 中，因此，我們只會假設 `Suppliers` 資料表的資料是靜態的。 因此，我們可以在應用程式啟動時快取此資料。

若要開始，請在 `CL` 資料夾中建立名為 `StaticCache.cs` 的新類別。

![在 CL 資料夾中建立 StaticCache 類別](caching-data-at-application-startup-vb/_static/image2.png)

**圖 2**：在 `CL` 資料夾中建立 `StaticCache.vb` 類別

我們需要新增方法，將啟動時的資料載入至適當的快取存放區，以及從這個快取傳回資料的方法。

[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample3.vb)]

上述程式碼會使用靜態成員變數 `suppliers`，以保存來自 `SuppliersBLL` 類別 s `GetSuppliers()` 方法（從 `LoadStaticCache()` 方法呼叫）的結果。 在應用程式啟動期間，應該呼叫 `LoadStaticCache()` 方法。 一旦在應用程式啟動時載入此資料，任何需要使用供應商資料的頁面都可以呼叫 `StaticCache` 類別 `GetSuppliers()` 方法。 因此，在應用程式啟動時，對資料庫的呼叫只會出現一次。

我們不會使用靜態成員變數做為快取存放區，而是也可以使用應用程式狀態或資料快取。 下列程式碼顯示類別改良以使用應用程式狀態：

[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample4.vb)]

在 `LoadStaticCache()`中，供應商資訊會儲存至應用程式變數索引*鍵*。 它會從 `GetSuppliers()`傳回為適當的類型（`Northwind.SuppliersDataTable`）。 雖然您可以使用 `Application("key")`，在 ASP.NET 網頁的程式碼後置類別中存取應用程式狀態，但在架構中，我們必須使用 `HttpContext.Current.Application("key")`，才能取得目前的 `HttpContext`。

同樣地，資料快取也可以當做快取存放區使用，如下列程式碼所示：

[!code-vb[Main](caching-data-at-application-startup-vb/samples/sample5.vb)]

若要將專案新增至資料快取，但沒有以時間為基礎的到期日，請使用 `System.Web.Caching.Cache.NoAbsoluteExpiration` 和 `System.Web.Caching.Cache.NoSlidingExpiration` 值做為輸入參數。 已選取資料快取的這個特定多載 `Insert` 方法，讓我們可以指定快取專案的*優先順序*。 優先順序是用來決定可用記憶體不足時，要從快取中清除哪些專案。 在此，我們使用優先順序 `NotRemovable`，以確保不會清除此快取專案。

> [!NOTE]
> 本教學課程的下載會使用靜態成員變數方法來執行 `StaticCache` 類別。 應用程式狀態和資料快取技術的程式碼可在類別檔案的批註中取得。

## <a name="step-4-executing-code-at-application-startup"></a>步驟4：在應用程式啟動時執行程式碼

若要在 web 應用程式第一次啟動時執行程式碼，我們需要建立一個名為 `Global.asax`的特殊檔案。 這個檔案可以包含應用程式、會話和要求層級事件的事件處理常式，而且可以在這裡新增應用程式啟動時所要執行的程式碼。

以滑鼠右鍵按一下 Visual Studio s 方案總管中的網站專案名稱，然後選擇 [加入新專案]，將 `Global.asax` 檔案加入至 web 應用程式的根目錄。 從 [加入新專案] 對話方塊中，選取 [全域應用程式類別] 專案類型，然後按一下 [加入] 按鈕。

> [!NOTE]
> 如果您的專案中已經有 `Global.asax` 檔案，全域應用程式類別專案類型將不會列在 [加入新專案] 對話方塊中。

[![將 global.asax 檔案新增至 Web 應用程式的根目錄](caching-data-at-application-startup-vb/_static/image4.png)](caching-data-at-application-startup-vb/_static/image3.png)

**圖 3**：將 `Global.asax` 檔案加入至 Web 應用程式的根目錄（[按一下以查看完整大小的影像](caching-data-at-application-startup-vb/_static/image5.png)）

預設 `Global.asax` 檔案範本包含伺服器端 `<script>` 標記中的五個方法：

- **`Application_Start`** 在 web 應用程式第一次啟動時執行
- 應用程式關閉時執行 **`Application_End`**
- 每當未處理的例外狀況到達應用程式時，就會執行 **`Application_Error`**
- 建立新的會話時， **`Session_Start`** 執行
- 當會話已過期或已放棄時， **`Session_End`** 執行

`Application_Start` 事件處理常式只會在應用程式的生命週期中呼叫一次。 應用程式會在第一次從應用程式要求 ASP.NET 資源時啟動，並繼續執行直到重新開機應用程式為止，這可能是因為修改 `/Bin` 資料夾的內容、修改 `Global.asax`、修改 `App_Code` 資料夾中的內容，或是修改 `Web.config` 檔案，還有其他原因。 如需應用程式生命週期的詳細討論，請參閱[ASP.NET 應用程式生命週期總覽](https://msdn.microsoft.com/library/ms178473.aspx)。

在這些教學課程中，我們只需要將程式碼新增至 `Application_Start` 方法，因此您可以自由移除其他專案。 在 `Application_Start`中，只要呼叫 `StaticCache` 類別 s `LoadStaticCache()` 方法，就會載入並快取供應商資訊：

[!code-aspx[Main](caching-data-at-application-startup-vb/samples/sample6.aspx)]

這樣就大功告成了！ 在應用程式啟動時，`LoadStaticCache()` 方法會從 BLL 抓取供應商資訊，並將其儲存在靜態成員變數中（或您在 `StaticCache` 類別中使用的任何快取存放區）。 若要確認此行為，請在 `Application_Start` 方法中設定中斷點，並執行您的應用程式。 請注意，啟動應用程式時，會叫用中斷點。 不過，後續要求並不會造成 `Application_Start` 方法執行。

[![使用中斷點來確認正在執行 Application_Start 事件處理常式](caching-data-at-application-startup-vb/_static/image7.png)](caching-data-at-application-startup-vb/_static/image6.png)

**圖 4**：使用中斷點來確認正在執行 `Application_Start` 事件處理常式（[按一下以查看完整大小的影像](caching-data-at-application-startup-vb/_static/image8.png)）

> [!NOTE]
> 如果您在第一次啟動偵錯工具時未按下 `Application_Start` 中斷點，這是因為您的應用程式已啟動。 請修改您的 `Global.asax` 或 `Web.config` 檔案，強制重新開機應用程式，然後再試一次。 您可以直接在上述其中一個檔案的結尾加入（或移除）空白行，以快速重新開機應用程式。

## <a name="step-5-displaying-the-cached-data"></a>步驟5：顯示快取的資料

此時，`StaticCache` 類別具有在應用程式啟動時快取的供應商資料版本，可以透過其 `GetSuppliers()` 方法來存取。 若要從展示層使用此資料，我們可以使用 ObjectDataSource，或以程式設計方式從 ASP.NET 網頁的程式碼後置類別叫用 `StaticCache` 類別 s `GetSuppliers()` 方法。 讓我們看看如何使用 ObjectDataSource 和 GridView 控制項來顯示快取的供應商資訊。

從開啟 [`Caching`] 資料夾中的 [`AtApplicationStartup.aspx`] 頁面開始。 將 GridView 從 [工具箱] 拖曳至設計工具，將其 [`ID`] 屬性設定為 [`Suppliers`]。 接下來，從 GridView 的智慧標籤選擇建立名為 `SuppliersCachedDataSource`的新 ObjectDataSource。 設定 ObjectDataSource 以使用 `StaticCache` 類別的 `GetSuppliers()` 方法。

[![將 ObjectDataSource 設定為使用 StaticCache 類別](caching-data-at-application-startup-vb/_static/image10.png)](caching-data-at-application-startup-vb/_static/image9.png)

**圖 5**：設定 ObjectDataSource 使用 `StaticCache` 類別（[按一下以查看完整大小的影像](caching-data-at-application-startup-vb/_static/image11.png)）

[![使用 GetSuppliers （）方法來取出快取的供應商資料](caching-data-at-application-startup-vb/_static/image13.png)](caching-data-at-application-startup-vb/_static/image12.png)

**圖 6**：使用 `GetSuppliers()` 方法來抓取快取的供應商資料（[按一下以查看完整大小的影像](caching-data-at-application-startup-vb/_static/image14.png)）

完成 wizard 之後，Visual Studio 會自動為 `SuppliersDataTable`中的每個資料欄位加入 BoundFields。 您的 GridView 和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](caching-data-at-application-startup-vb/samples/sample7.aspx)]

[圖 7] 顯示透過瀏覽器觀看的頁面。 輸出會與我們從 BLL `SuppliersBLL` 類別中提取資料相同，但使用 `StaticCache` 類別會傳回供應商資料，如在應用程式啟動時快取。 您可以在 `StaticCache` 類別 s `GetSuppliers()` 方法中設定中斷點，以驗證此行為。

[![已快取的供應商資料會顯示在 GridView 中](caching-data-at-application-startup-vb/_static/image16.png)](caching-data-at-application-startup-vb/_static/image15.png)

**圖 7**：快取的供應商資料會顯示在 GridView 中（[按一下以觀看完整大小的影像](caching-data-at-application-startup-vb/_static/image17.png)）

## <a name="summary"></a>總結

大部分的資料模型都包含相當大量的靜態資料，通常是以查閱資料表的形式來執行。 由於這項資訊是靜態的，因此在每次需要顯示此資訊時，都沒有理由持續存取資料庫。 此外，由於它的靜態本質，因此在快取資料時，不需要到期。 在本教學課程中，我們已瞭解如何採用這類資料，並將它快取到資料快取、應用程式狀態，以及透過靜態成員變數。 這項資訊會在應用程式啟動時快取，並在整個應用程式的存留期間保留在快取中。

在本教學課程和過去的兩個中，我們已探討在應用程式的存留期間內快取資料，以及使用以時間為基礎的 expiries。 不過，當快取資料庫資料時，以時間為基礎的到期可能會小於理想的。 並不會定期清除快取，因此只有在修改基礎資料庫資料時才收回快取的專案是最佳做法。 這是使用 SQL 快取相依性的理想選擇，我們將在下一個教學課程中進行檢查。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的潛在客戶審核者為 Teresa Murphy 和 Zack。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](caching-data-in-the-architecture-vb.md)
> [下一頁](using-sql-cache-dependencies-vb.md)
