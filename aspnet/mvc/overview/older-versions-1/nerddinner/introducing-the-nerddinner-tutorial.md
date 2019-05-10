---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: 簡介 NerdDinner 教學課程 |Microsoft Docs
author: shanselman
description: 若要了解新架構的最佳方式是建置與它的一些項目。 本教學課程逐步解說如何建置使用 ASP.NET 的小，但完整的應用程式...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65122312"
---
# <a name="introducing-the-nerddinner-tutorial"></a>NerdDinner 教學課程簡介

藉由[Scott Hanselman](https://github.com/shanselman)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 若要了解新架構的最佳方式是建置與它的一些項目。 本教學課程會逐步解說如何建置一個小型的但在完成時，使用 ASP.NET MVC 1，應用程式，並介紹一些其背後的核心概念。
> 
> 如果您使用 ASP.NET MVC 3，我們建議您遵循[取得開始使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或是[MVC Music 市集](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程。

## <a name="nerddinner-tutorial"></a>NerdDinner 教學課程

若要了解新架構的最佳方式是建置與它的一些項目。 本教學課程會逐步解說如何建置一個小型的但在完成時，使用 ASP.NET MVC 應用程式，並介紹一些其背後的核心概念。

我們將建置的應用程式稱為 「 NerdDinner"。 NerdDinner 提供簡單的方法讓人們尋找和組織 dinners 線上：

![](introducing-the-nerddinner-tutorial/_static/image1.png)

NerdDinner 可讓已註冊的使用者，來建立、 編輯和刪除 dinners。 它會強制整個應用程式執行一組一致的驗證和商務規則：

![](introducing-the-nerddinner-tutorial/_static/image2.png)

訪客可以使用 AJAX 為基礎的地圖，來搜尋即將推出的 dinners 持有接近它們：

![](introducing-the-nerddinner-tutorial/_static/image3.png)

按一下 dinner 會移至詳細資料頁面讓他們從中學習更多關於此：

![](introducing-the-nerddinner-tutorial/_static/image4.png)

如果他們有興趣參加的 dinner 他們可以登入或註冊網站：

![](introducing-the-nerddinner-tutorial/_static/image5.png)

它們可以然後按一下 參加的 AJAX 為基礎的 RSVP 連結：

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>實作 NerdDinner

我們將從我們的 NerdDinner 應用程式使用 [檔案]-&gt;新專案在 Visual Studio 中的命令來建立全新的 ASP.NET MVC 專案。 我們接著會以累加方式新增功能和功能。 在過程中，我們將討論：

1. [如何建立新的 ASP.NET MVC 專案](create-a-new-aspnet-mvc-project.md)
2. [如何建立資料庫](create-a-database.md)
3. [如何建立使用商務規則驗證模型](build-a-model-with-business-rule-validations.md)
4. [如何使用控制器和檢視來實作清單/詳細資料 UI](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [如何提供 CRUD （建立、 讀取、 更新、 刪除） 資料表單項目支援](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [如何使用 ViewData 和實作 ViewModel 類別](use-viewdata-and-implement-viewmodel-classes.md)
7. [如何重新使用使用主版頁面及部分的 UI](re-use-ui-using-master-pages-and-partials.md)
8. [如何實作有效率的資料分頁](implement-efficient-data-paging.md)
9. [如何保護應用程式使用驗證和授權](secure-applications-using-authentication-and-authorization.md)
10. [如何使用 AJAX 傳送動態更新](use-ajax-to-deliver-dynamic-updates.md)
11. [如何使用 AJAX 實作對應實例](use-ajax-to-implement-mapping-scenarios.md)
12. [如何啟用自動化的單元測試](enable-automated-unit-testing.md)

您可以建置自己的 NerdDinner 從頭開始，藉由完成每個步驟中我們在這一章中的逐步解說。 或者，您可以下載原始碼的完整的版本：[在 GitHub 上的 NerdDinner](https://github.com/AspNetMVPSamples/NerdDinner)。 您可以選擇性地也[下載免費的 PDF 版本，本教學課程的](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)如果您想要讀取的離線教學課程。

您可以使用 Visual Studio 2008 或免費 Visual Web Developer 2008 Express 建置應用程式。 您可以使用 SQL Server 或免費的 SQL Server Express 資料庫。

您可以安裝 ASP.NET MVC、 Visual Web Developer 2008 Express，和 SQL Server Express （所有免費） 使用的 V2 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)

### <a name="now-lets-get-started"></a>現在讓我們開始...

既然我們已涵蓋 NerdDinner 的功能，讓我們彙總我們套筒，並撰寫一些程式碼。

首先我們使用檔案-&gt;建立 NerdDinner 應用程式的 Visual Studio 中的新專案。

> [!div class="step-by-step"]
> [下一步](create-a-new-aspnet-mvc-project.md)
