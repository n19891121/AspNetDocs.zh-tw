---
uid: web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 使用視覺化工作室程式設計ASP.NET網頁 (Razor) |微軟文件
author: Rick-Anderson
description: 本附錄說明如何使用 Visual Studio 2010 或可視化 Web 開發人員 2010 Express 使用 Razor 語法對 ASP.NET 網頁進行程式設計。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: e586a116fc48a797bdd40befad5851a548282ce6
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542894"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>使用視覺化工作室ASP.NET網頁 (Razor) 程式設計

 作者：[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介紹如何使用可視化工作室或可視化 Web 開發人員快速程式 ASP.NET 網頁 (Razor) 網站。
>
> 您將學到什麼
>
> - 您需要安裝的內容(如果有的話)才能在 Visual Studio 版本中使用 ASP.NET 網頁。
> - 如何向視覺化 Web 開發人員 2010 Express 添加對ASP.NET網頁的支援。
> - 如何使用 Visual Studio 中的功能使用 ASP.NET Razor 頁面,包括 IntelliSense 和調試器。
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教學中使用的軟體版本
>
>
> - ASP.NET網頁 (剃鬚刀) 3
> - Visual Studio 2013
> - Web矩陣 3
>
>
> 本教學還適用於ASP.NET網頁 2、Visual Studio 2012、Visual Studio 2010 和 WebMatrix 2。

您可以使用 WebMatrix 或許多其他程式碼編輯器使用 Razor 語法對 ASP.NET 網頁進行程式設計。 您還可以使用 Microsoft Visual Studio,這是一個功能齊全的集成開發環境 (IDE),它提供了一組功能強大的工具來創建多種類型的應用程式(而不僅僅是網站)。 要使用ASP.NET Razor 頁面,您可以使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。

Visual Studio 為使用 ASP.NET Razor 網頁進行程式設計提供的兩個特別有用的功能是:

- *內泰利感知*。 視覺工作室內置的 IntelliSense 功能比 WebMatrix 中的 IntelliSense 更為全面。
- *除錯器*。 除錯器允許您在程式執行時停止程式、檢查變數和逐行執行代碼,從而對代碼進行故障排除。

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>將視覺工作室與不同版本的ASP.NET網頁使用

要在 Visual Studio 2017 中開發ASP.NET Web 應用,請安裝**ASP.NET和 Web 開發**工作負載。

Visual Studio 2012 和 Visual Studio 2013 包括對ASP.NET網頁的支援。 (安裝 Visual Studio 時,將安裝支援ASP.NET網頁所需的套件。

默認情況下,Visual Studio 2010 不包括對 ASP.NET 網頁的支援。 要將 ASP.NET 網頁與 Visual Studio 2010 一起使用,您必須安裝 ASP.NET MVC 套件。 要取得 ASP.NET 網頁 2,請安裝ASP.NET MVC 4。

下表總結了不同版本的 Visual Studio 中對 ASP.NET 網頁的支援。

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET Web Pages 2** | 安裝ASP.NET MVC 4 | (包括) | (包括) |
| **ASP.NET Web Pages 3** |  | 透過 NuGet 更新到ASP.NET網頁 3 | (包括) |

要使用 Visual Studio 2010,請參閱[在 Visual Studio 2010 中安裝支援 ASP.NET 網頁](#vs2010support)。

## <a name="launching-visual-studio-from-webmatrix"></a>從 WebMatrix 啟動視覺化工作室

如果您在 WebMatrix 中啟動了一個專案,並希望切換到 Visual Studio,WebMatrix 提供了一個按鈕,用於在 Visual Studio 中輕鬆打開專案。 您必須在電腦上安裝 Visual Studio 才能啟用此按鈕。 下圖顯示了 WebMatrix 中的按鈕。

![啟動視覺工作室](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

單擊該按鈕時,專案在可視化工作室中打開。 您可以在 WebMatrix 和 Visual Studio 之間來回切換,沒有任何問題。 如果其他環境中的任何檔已更改,需要重新載入以獲取最新更改,您將收到通知。

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>在視覺工作室建立ASP.NET剃刀網站

要在視覺工作室中創建ASP.NET剃刀網站:

1. 開啟 Visual Studio。
2. 在 **「檔案**」選單中,按下 **「新建網站**」 。。

    ![建立新網站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. 在 **"新建網站'** 對話框中,選擇要使用的語言(可視 C# 或可視基本)。
4. 選擇**ASP.NET網站(Razor)** 範本。

    ![剃鬚刀網站](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. 按一下 [確定]  。

新專案存在,並且填充了一些默認網頁,以説明您入門。

### <a name="using-intellisense"></a>Using IntelliSense

現在,您已經創建了一個網站,您可以看到 IntelliSense 在視覺工作室中是如何工作的。

1. 在您剛剛創建的網站中,打開*Default.cshtml*頁面。
2. 在頁面`<h3>`中的標記之後,鍵`@ServerInfo.`入 (包括點)。 請注意 IntelliSense 如何在下拉清單`ServerInfo`中顯示 説明程式的可用方法。

    ![IntelliSense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. 從`GetHtml`清單中選擇方法,然後按 Enter。 IntelliSense 會自動填充該方法。 (與 C# 中的任何方法一樣,`()`必須在 方法之後添加字元。方法的`GetHtml`已完成代碼類似於以下範例:

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. 按 Ctrl+F5 以運行該頁。 這是頁面在瀏覽器中顯示時的外觀:

    ![瀏覽器中的預設頁面](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. 關閉瀏覽器。

### <a name="using-the-debugger"></a>使用除錯器

1. 在*Default.cshtml*頁面的頂部`Page.Title`,以 開頭的行後添加以下代碼行:

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. 在片段左側編輯器的灰色邊距中,按一次新行的旁邊以新增*斷點*。 斷點是一個標記,它告訴調試器在此時停止運行程式,以便您可以看到發生了什麼。

    ![設定中斷點](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. 刪除對 方法`ServerInfo.GetHtml`的 調用,並將調用`@myTime`添加到 變數的位置。 此調用顯示新代碼行返回的當前時間值。
4. 按 F5 以在調試器中運行頁面。 頁面在您設置的斷點上停止。 下圖顯示了具有斷點(黃色)的編輯器中頁面的外觀。

    ![除錯中斷點](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. 在「調試」工具列中,按下 **「進入」** 按鈕(或按 F11)以執行下一行代碼。 每次按下此按鈕時,都會將執行提前到下一行代碼。

    ![單步進入按鈕](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. 通過將滑鼠指標放在變數`myTime`上或透過檢查 **「局部變數**」和 **「調用堆疊**」視窗中顯示的值來檢查變數的值。 可視化工作室顯示變數的值。

    ![顯示時間值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. 檢查完變數並單步執行代碼後,按 F5 繼續運行頁面,而無需在每行停止。 完成所有代碼後,瀏覽器將顯示頁面。

要瞭解有關除錯器以及如何在 Visual Studio 中除錯程式碼的資訊,請參閱[演練:在視覺化 Web 開發人員中除錯網頁](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>使用 Razor 在 ASP.NET MVC 專案中使用 Visual Studio

Razor 語法還廣泛用於ASP.NET MVC 專案中。 MVC 是構建動態網站的強大、基於模式的方法。 如果ASP.NET網頁網站變得難以維護,您可能需要考慮將其轉換為ASP.NET MVC 應用程式。 有關建立 MVC 應用程式的範例,請參閱[使用 mVC 5 ASP.NET 入門](../../../mvc/overview/getting-started/introduction/getting-started.md)。

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>2010 年在可視化工作室安裝對 ASP.NET 網頁的支援

本節演示如何安裝 Visual Web 開發人員 Express 2010 和可視化工作室的ASP.NET網頁工具。

1. 如果您尚未網路平台安裝程式,請從以下網址下載它:

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. 運行 Web 平臺安裝程式。
3. 按**下產品**「選項卡。

    ![WebPI 產品選項卡](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. 搜索**ASP.NET MVC 4(ASP.NET**網頁 2),然後按下「**添加**」。。 這些產品包括用於構建ASP.NET Razor 網站的視覺工作室工具。

    ![WebPi 安裝選項](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. 單擊「**安裝**」以完成安裝。
