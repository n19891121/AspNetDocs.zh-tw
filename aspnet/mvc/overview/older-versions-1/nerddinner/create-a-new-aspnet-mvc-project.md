---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 建立新ASP.NET MVC 專案 |微軟文件
author: rick-anderson
description: 步驟 1 演示如何將基本的 NerdDinner 應用程式結構放在原位。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 240c8a04cec3c07f434182775d1c519aab029761
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541477"
---
# <a name="create-a-new-aspnet-mvc-project"></a>建立新的 ASP.NET MVC 專案

由[微軟](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第 1 步,該教學示範如何使用 ASP.NET MVC 1 構建小型但完整的 Web 應用程式。
> 
> 步驟 1 演示如何將基本的 NerdDinner 應用程式結構放在原位。
> 
> 如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。

## <a name="nerddinner-step-1-file-gtnew-project"></a>神經晚餐步驟 1:&gt;檔案 - 新項目

我們將透過在 Visual Studio 2008 或免費的可視化 Web 開發人員 2008 Express 中選擇 **「檔-&gt;新專案**」功能表項來開始我們的NerdDinner應用程式。

這將彈出"新專案"對話框。 要建立新ASP.NET MVC 應用程式,我們將選擇對話框左側的「Web」節點,然後在右側選擇「ASP.NET MVC Web 應用程式」專案範本:

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*重要提示:請確保已下載並安裝 ASP.NET MVC - 否則它不會顯示在「新項目」對話框中。如果您尚未安裝[Microsoft Web 平臺安裝程式](https://www.microsoft.com/web/downloads/platform.aspx)的 V2(ASP.NET MVC 在"Web 平臺-&gt;框架和運行時"部分中可用)。*

我們將命名要創建「NerdDinner」的新項目,然後單擊「確定」按鈕創建它。

當我們按下「OK」Visual Studio 時,將彈出一個附加對話框,提示我們為新應用程式選擇創建單元測試專案。 此單元測試專案使我們能夠創建自動測試,以驗證應用程式的功能和行為(本教程稍後將介紹如何操作)。

![](create-a-new-aspnet-mvc-project/_static/image2.png)

上面對話方塊中的「測試框架」下拉清單填充了所有可用的ASP.NET MVC 單元測試專案範本安裝在電腦上。 可以為 NUnit、MBUnit 和 XUnit 下載版本。 還支援內置的可視化工作室單元測試框架。

*注意:可視化工作室單元測試框架僅適用於 Visual Studio 2008 專業版和更高版本。如果您使用的是 VS 2008 標準版或可視化 Web 開發人員 2008 Express,則需要下載並安裝 nUnit、MBUnit 或 XUnit 擴展,以便 ASP.NET MVC 才能顯示此對話方塊。如果沒有安裝任何測試框架,將不會顯示該對話方塊。*

我們將為我們創建的測試專案使用預設的「NerdDinner.Test」名稱,並使用「視覺化工作室單元測試」框架選項。 當我們點擊「ok」按鈕 Visual Studio 將為我們建立一個解決方案,其中包含兩個專案 - 一個用於我們的 Web 應用程式,一個用於我們的單元測試:

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>檢查 NerdDinner 目錄結構

當您使用 Visual Studio 建立新 ASP.NET MVC 應用程式時,它會自動向專案新增許多檔案和目錄:

![](create-a-new-aspnet-mvc-project/_static/image4.png)

預設的項目上ASP.NET MVC 專案有六個頂級目錄:

| **目錄** | **目的** |
| --- | --- |
| **/控制器** | 放置處理網址 要求的控制器類別的位置 |
| **/型號** | 放置並操作資料的類別的位置 |
| **/檢視** | 設定設定輸出的 UI 樣本檔案的位置 |
| **/文稿** | 放置 JavaScript 函式庫檔案與文稿的位置 (.js) |
| **/內容** | 放置 CSS 與影像檔以及其他非動態/非 JavaScript 內容的位置 |
| **/應用程式\_資料** | 儲存要讀取/寫入的資料檔的位置。 |

ASP.NET MVC 不需要此結構。 事實上,處理大型應用程式的開發人員通常會跨多個專案對應用程式進行分區,使其更易於管理(例如:資料模型類通常位於與 Web 應用程式不同的類庫專案中)。 但是,默認專案結構確實提供了一個不錯的默認目錄約定,我們可以用它來保持應用程序問題清潔。

當我們展開 /控制器目錄時,我們會發現 Visual Studio 預設為專案添加了兩個控制器類 - 主控制器和帳戶控制器:

![](create-a-new-aspnet-mvc-project/_static/image5.png)

當我們展開 /Views 目錄時,我們會發現三個子目錄 - /Home,//帳戶和 /共用 - 以及其中的幾個範本檔也添加到專案中,默認情況下:

![](create-a-new-aspnet-mvc-project/_static/image6.png)

當我們展開 /內容和 /script 檔:

![](create-a-new-aspnet-mvc-project/_static/image7.png)

當我們擴展NerdDinner.測試專案時,我們將找到兩個類,其中包含控制器類的單元測試:

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Visual Studio 添加的這些預設檔為我們提供了工作應用程式的基本結構 - 完整的主頁,關於頁面,帳戶登錄/註銷/註冊頁,和未處理的錯誤頁面(所有有線和開箱即用)。

### <a name="running-the-nerddinner-application"></a>執行內德晚餐應用程式

我們可以通過選擇**除錯&gt;- 啟動除錯**或**除錯 -&gt;不除錯選單項目**執行專案:

![](create-a-new-aspnet-mvc-project/_static/image9.png)

這會啟動 Visual Studio 附帶的內建ASP.NET Web 伺服器,並執行我們的應用程式:

![](create-a-new-aspnet-mvc-project/_static/image10.png)

以下是我們新專案的主頁(URL:"/")運行時:

![](create-a-new-aspnet-mvc-project/_static/image11.png)

按下「關於」選項卡將顯示一個有關頁面(URL:"/主頁/關於"):

![](create-a-new-aspnet-mvc-project/_static/image12.png)

按下右上角的「登錄」連結將我們帶到登錄頁面(URL:"/帳戶/登錄")

![](create-a-new-aspnet-mvc-project/_static/image13.png)

如果我們沒有登錄帳戶,我們可以單擊註冊連結(URL:"/帳戶/註冊")創建一個:

![](create-a-new-aspnet-mvc-project/_static/image14.png)

在創建新專案時,默認情況下添加了實現上述主頁、關於和註銷/寄存器功能的代碼。 我們將使用它作為應用程式的起點。

### <a name="testing-the-nerddinner-application"></a>測試內德晚餐應用程式

如果我們使用 Visual Studio 2008 的專業版或更高版本,我們可以在 Visual Studio 中使用內置單元測試 IDE 支援來測試專案:

![](create-a-new-aspnet-mvc-project/_static/image15.png)

選擇上述選項之一將在 IDE 中開啟「測試結果」窗格,並在新專案中包含的 27 個單元測試中提供通過/失敗狀態,這些測試涵蓋內置功能:

![](create-a-new-aspnet-mvc-project/_static/image16.png)

在本教程的後面部分,我們將介紹有關自動測試的更多資訊,並添加其他單元測試,這些測試涵蓋了我們實現的應用程式功能。

### <a name="next-step"></a>後續步驟

現在,我們已經有了一個基本的應用程序結構。 現在,讓我們[建立資料庫來儲存我們的應用程式資料](create-a-database.md)。

> [!div class="step-by-step"]
> [前一個](introducing-the-nerddinner-tutorial.md)
> [下一個](create-a-database.md)
