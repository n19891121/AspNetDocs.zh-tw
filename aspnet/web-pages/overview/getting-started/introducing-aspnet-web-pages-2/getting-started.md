---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: 開始使用 | Microsoft Docs
author: Rick-Anderson
description: 不再建議使用 WebMatrix 做為 ASP.NET Web Pages 的整合式開發環境。 使用 Visual Studio 或 Visual Studio Code。 本指導方針 .。。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ac2111980e6393388a0530375fb9ef78dbbfaff6
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240752"
---
# <a name="getting-started"></a>開始使用

 作者：[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > 不再建議使用 WebMatrix 做為 ASP.NET Web Pages 的整合式開發環境。 使用[Visual Studio](../program-asp-net-web-pages-in-visual-studio.md)或[Visual Studio Code](https://code.visualstudio.com/)。
> 
> 
> 本指引和應用程式可讓您大致瞭解 ASP.NET Web Pages （第2版或更新版本）和 Razor 語法，這是建立動態網站的輕量架構。 它也引進了 WebMatrix，這是用來建立頁面和網站的工具。
> 
> **層級**： ASP.NET Web Pages 的新。  
> **假設的技能**： HTML、基本級聯樣式表（CSS）。
> 
> 您將在第一組教學課程中瞭解的內容：
> 
> - 什麼是 ASP.NET Web Pages 技術及其用途。
> - WebMatrix 是什麼。
> - 如何安裝所有專案。
> - 如何使用 WebMatrix 建立網站。
>   
> 
> 討論的功能/技術：
> 
> - Microsoft Web Platform Installer。
> - WebMatrix.
> - *cshtml*頁面
>   
> 
> Mike Pope 原本寫了本教學課程。 Tom FitzMacken 已針對 Microsoft WebMatrix 3 進行更新。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
> 
> 
> - ASP.NET Web Pages （Razor）2
> - WebMatrix 3

## <a name="what-should-you-know"></a>您應該知道什麼？

我們假設您已經熟悉：

- **HTML**。 不需要深入的專業知識。 我們不會說明 HTML，但我們也不會使用任何複雜的專案。 我們會提供 HTML 教學課程的連結，我們認為這些是有用的。
- **級聯樣式表（CSS）**。 與 HTML 相同。
- **基本資料庫的想法**。 如果您使用試算表來儲存資料，並將資料排序和篩選，這就是我們通常會在本教學課程中假設的專業知識層級。

我們也假設您有興趣學習基本程式設計。 ASP.NET Web Pages 使用稱為 c # 的程式設計語言。 您不需要在程式設計中擁有任何背景，只是其中的重點。 如果您之前曾在網頁中撰寫過任何 JavaScript，就有許多背景。

請注意，如果您熟悉程式設計，您可能會發現，本教學課程最初的設定速度會變慢，而我們會讓新的程式開發人員加快速度。 不過，我們在過去的幾個教學課程中，將會有較少的基本程式設計，而且會以更快速的剪輯來移動專案。

## <a name="what-do-you-need"></a>您需要什麼？

以下是您需要的內容：

- 執行 Windows 8、Windows 7、Windows Server 2008 或 Windows Server 2012 的電腦。
- 即時網際網路連線。
- 系統管理員許可權（安裝程式所需）。

## <a name="what-is-aspnet-web-pages"></a>什麼是 ASP.NET Web Pages？

ASP.NET Web Pages 是一種架構，可讓您用來建立動態網頁。 簡單的 HTML 網頁是靜態的;其內容取決於頁面中的固定 HTML 標籤。 像您使用 ASP.NET Web Pages 建立的動態頁面，可讓您使用程式碼，即時建立網頁內容。

動態頁面可讓您執行各種動作。 您可以使用表單來要求使用者輸入，然後變更頁面所顯示的內容或外觀。 您可以從使用者中取出資訊，將它儲存在資料庫中，然後稍後再列出。 您可以從您的網站傳送電子郵件。 您可以與網路上的其他服務（例如，對應服務）互動，並產生可整合來自這些來源之資訊的頁面。

## <a name="what-is-webmatrix"></a>什麼是 WebMatrix？

WebMatrix 是一種工具，可整合網頁編輯器、資料庫公用程式、測試頁面的 web 伺服器，以及將您的網站發佈至網際網路的功能。 WebMatrix 是免費的，而且容易安裝且便於使用。 （它也適用于純 HTML 網頁，以及其他像是 PHP 的技術）。

您實際上不*需要*使用 WebMatrix 來處理 ASP.NET Web Pages。 例如，您可以使用文字編輯器來建立頁面，並使用您可以存取的網頁伺服器來測試頁面。 不過，WebMatrix 讓它變得非常簡單，因此這些教學課程會在整個過程中使用 WebMatrix。

## <a name="about-these-tutorials"></a>關於這些教學課程

本教學課程集是如何使用 ASP.NET Web Pages 的簡介。 本簡介教學課程集中有9個教學課程總計。 它是一系列教學課程集合的一部分，可讓您從 ASP.NET Web Pages 新手，建立真正、專業型式的網站。

第一個教學課程設定著重于說明如何使用 ASP.NET Web Pages 的基本概念。 當您完成時，您可以使用其他教學課程集合，以取得此端點的結尾，並深入探索網頁。

我們刻意開始簡單的說明。 當我們顯示某個專案時，在本教學課程中設定我們一定會選擇最容易瞭解的方式。 稍後的教學課程集會更深入探討，並顯示更有效率或更有彈性的方法（也更有趣）。 但這些教學課程需要您先瞭解基本概念。

您剛開始的教學課程集涵蓋了 ASP.NET Web Pages 的下列功能：

- 簡介並讓所有專案都已安裝。 （這是在您所閱讀的教學課程中）。
- ASP.NET Web Pages 程式設計的基本概念。
- 建立資料庫。
- 建立和處理使用者輸入表單。
- 加入、更新和刪除資料庫中的資料。

## <a name="what-will-you-create"></a>您會建立什麼？

本教學課程的設定和後續工作會在網站上進行，您可以在其中列出您喜歡的電影。 您將能夠輸入電影、加以編輯並列出它們。 以下是您將在本教學課程中建立的幾個頁面。 第一個範例會顯示您將建立的電影清單頁面：

![顯示電影清單的完成電影應用程式](getting-started/_static/image1.png)

以下是可讓您將新電影資訊新增至網站的頁面：

![顯示 [新增電影] 頁面的已完成電影應用程式](getting-started/_static/image2.png)

後續的教學課程會在此集合上設定組建，並新增更多功能，例如上傳圖片、讓使用者登入、傳送電子郵件，以及與社交媒體整合。

## <a name="see-this-app-running-on-azure"></a>請參閱此應用程式在 Azure 上執行

您是否想要查看已完成的網站以即時 web 應用程式的形式執行？ 只要按一下下列按鈕，您就可以將應用程式的完整版本部署至您的 Azure 帳戶。

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

您需要 Azure 帳戶，才能將此解決方案部署至 Azure。 如果您還沒有帳戶，您可以使用下列選項：

- [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-您將取得可試用付費 azure 服務的額度，且即使在用完後，您仍可保留帳戶，並使用免費的 azure 服務。
- [啟用 msdn 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-您的 msdn 訂用帳戶每月會提供您額度，供您用於付費 Azure 服務。

## <a name="installing-everything"></a>安裝所有專案

您可以使用 Microsoft 的 Web Platform Installer 來安裝所有專案。 實際上，您會安裝安裝程式，然後使用它來安裝其他專案。

若要使用網頁，您至少必須安裝 Windows XP 含 SP3，或 Windows Server 2008 或更新版本。

在 ASP.NET 網站的 [ [Web Pages] 頁面](../../../index.md)上，按一下 [**安裝**]。

![顯示 [ &quot; 安裝 WebMatrix] 按鈕的 ASP.NET 網站 &quot;](getting-started/_static/image3.png)

在安裝 WebMatrix 之前，系統會要求您接受授權條款和隱私權聲明。

![接受詞彙以開始安裝](getting-started/_static/image4.png)

按一下 [**執行**] 開始安裝。 （如果您想要儲存安裝程式，請按一下 [**儲存**]，然後從儲存的資料夾執行安裝程式）。

![](getting-started/_static/image5.png)

隨即顯示 Web Platform Installer，準備好安裝 WebMatrix。 按一下 [Install] 。

![](getting-started/_static/image6.png)

安裝程式會找出它必須安裝在您電腦上的內容，並開始處理。 視必須安裝的內容而定，此程式可能需要數分鐘到數分鐘的時間。 選取 [**我接受**] 以接受授權條款。

## <a name="hello-webmatrix"></a>您好，WebMatrix

完成後，安裝程式就可以自動啟動 WebMatrix。 如果沒有，請在 Windows 中，從 [**開始**] 功能表啟動**Microsoft WebMatrix**。

當您第一次啟動 WebMatrix 時，您有機會使用您的 Microsoft 帳戶登入 Microsoft Azure。 藉由登入，您將可透過 Azure 獲得10個免費的 web 應用程式。 這些免費的 web 應用程式提供便利的方式來測試您的應用程式。 如果您還沒有 Azure 帳戶，但是有 MSDN 訂閱，則可以[啟用您的 msdn 訂閱權益](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)。 否則，您只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/dotnet/)。

您不需要立即登入，即可繼續進行本教學課程。 如果您目前未登入，您仍然可以選擇稍後再登入。 本教學課程系列中的最後一個[主題](publishing.md)涵蓋如何將您的網站部署至 Azure;因此，您必須登入才能完成該主題。

此時，請使用您的 Microsoft 帳戶登入，或選取右下角的 [**不是現在**]。

![Sign In](getting-started/_static/image7.png)

首先，您將建立空白網站並新增頁面。 在此集合稍後的教學課程中，您將會使用其中一個內建網站範本來播放。

在 [開始] 視窗中，按一下 [**新增**]。

![WebMatrix 啟動畫面](getting-started/_static/image8.png)

範本是針對不同類型的網站預先建立的檔案和頁面。 若要查看預設可用的所有範本，請選取 [範本資源庫] 選項。

![選取範本庫](getting-started/_static/image9.png)

在 [**快速入門**] 視窗中，從 [ **ASP.NET** ] 群組選取 [**空白網站**]，並將新網站命名為 "WebPagesMovies"。

![已選取空白網站範本的 WebMatrix [快速入門] 視窗](getting-started/_static/image10.png)

按 [下一步] 。

如果您已登入 Microsoft 帳戶，系統會提供您在 Azure 上建立網站的機會。 根據您的網站名稱，建議**WebPagesMovies.azurewebsites.net**的預設名稱。不過，驚嘆號表示此名稱無法在 Windows Azure 上使用。 為求簡化，請選取 [**跳過**]，立即略過在 Azure 上建立網站。 稍後在此系列中，我們會將網站發佈至 Azure。

![建立 azure 網站](getting-started/_static/image11.png)

WebMatrix 會建立並開啟網站：

![在 WebMatrix 中開啟新的 WebPagesMovies 網站](getting-started/_static/image12.png)

在頂端，有一個快速存取工具列和一個功能區。 在左下方，您會看到工作區選取**器，您**可以在其中切換工作（**網站**、檔案、**資料庫**、**報表**）。 右邊是編輯器和報表的內容窗格。 而在底部，您偶爾會看到訊息的通知列。

當您完成這些教學課程時，您將會深入瞭解 WebMatrix 及其功能。

## <a name="creating-a-web-page"></a>建立網頁

若要熟悉 WebMatrix 和 ASP.NET Web Pages，您將建立簡單的頁面。

在工作區選取器中，選取 [檔案 **] 工作區**。 此工作區可讓您使用檔案和資料夾。 左窗格會顯示您網站的檔案結構。 功能區會變更以顯示檔案相關的工作。

![WebMatrix 中的檔案工作區](getting-started/_static/image13.png)

在功能區中，按一下 [**新增**] 底下的箭號，然後按一下 [**新增**檔案]。

![使用 &quot; 功能區中的 [新增] &quot; 命令來建立新檔案](getting-started/_static/image14.png)

WebMatrix 會顯示檔案類型的清單。 選取 [ **CSHTML**]，然後在 [**名稱**] 方塊中輸入 "HelloWorld"。 CSHTML 頁面是 ASP.NET Web Pages 頁面。

![建立名為 HelloWorld 的新 CSHTML 頁面](getting-started/_static/image15.png)

按一下 [確定]。

WebMatrix 會建立頁面，並在編輯器中開啟它。

![WebMatrix 編輯器中的新 HelloWorld 頁面](getting-started/_static/image16.png)

如您所見，此頁面大多包含一般的 HTML 標籤，但頂端的區塊除外，如下所示：

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

這是為了新增程式碼，您很快就會看到。

請注意，頁面的不同部分（專案 &mdash; 名稱、屬性和文字，以及頂端的區塊）都是不同的色彩。 這稱為語法反白*顯示*，可讓您更輕鬆地保持所有專案的清晰。 它是可讓您在 WebMatrix 中輕鬆使用網頁的其中一項功能。

加入和元素的內容， `<head>` `<body>` 如下列範例所示。 （如有需要，您可以只複製下列區塊，並將整個現有的頁面取代為此程式碼）。

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

在 [快速存取] 工具列或 [檔案 **] 功能表中**，按一下 [**儲存**]。

![WebMatrix 快速存取工具列中的 [儲存] 按鈕](getting-started/_static/image17.png)

## <a name="testing-the-page"></a>測試頁面

在 [檔案 **] 工作區**中，以滑鼠右鍵按一下 [ *HelloWorld* ] 頁面，然後按一下 [**在瀏覽器中啟動**]。

![使用 WebMatrix 功能區中的 [執行] 按鈕執行頁面](getting-started/_static/image18.png)

WebMatrix 啟動內建的網頁伺服器（IIS Express），您可以用來測試電腦上的頁面。 （不 IIS Express 在 WebMatrix 中，您必須先將頁面發佈到 web 伺服器，然後才能進行測試）。頁面會顯示在您的預設瀏覽器中。

![&quot;&quot;在瀏覽器中執行 Hello World 頁面](getting-started/_static/image19.png)

請注意，當您在 WebMatrix 中測試頁面時，瀏覽器中的 URL 會是 `http://localhost:33651/HelloWorld.cshtml.` 名稱*localhost*參照本機伺服器，這表示網頁是由自己電腦上的網頁伺服器所提供。 如先前所述，WebMatrix 包含名為 IIS Express 的 web 伺服器程式，會在您啟動頁面時執行。

*Localhost*之後的數位（例如， *localhost： 33651*）會參考您電腦上的*埠號碼*。 這是 IIS Express 用於此特定網站的「通道」數目。 當您建立網站時，會從範圍1024到65536隨機選取埠號碼，而且您建立的每個網站都有不同的通訊埠編號。 （當您測試自己的網站時，埠號碼幾乎一定會與33561不同）。藉由對每個網站使用不同的埠，IIS Express 可以將其與您的網站進行直接的溝通。

稍後當您將網站發佈至公用 web 伺服器時，URL 中就不會再看到*localhost* 。 此時，您會看到較典型的 URL，例如 `http://myhostingsite/mywebsite/HelloWorld.cshtml` 或頁面是什麼。 您稍後會在本教學課程系列中深入瞭解如何發佈網站。

## <a name="adding-some-server-side-code"></a>新增一些伺服器端程式碼

關閉瀏覽器並返回 WebMatrix 中的頁面。

在程式碼區塊中新增一行，使其看起來像下列程式碼：

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

這有點 Razor 程式碼。 這可能會清楚地取得目前的日期和時間，並將該值放入名為的*變數*中 `currentDateTime` 。 您將在下一個教學課程中深入瞭解 Razor 語法。

在頁面主體中，于 `<p>Hello World!</p>` 元素後面新增下列專案：

[!code-html[Main](getting-started/samples/sample4.html)]

此程式碼會取得您放入 `currentDateTime` 變數頂端的值，並將它插入至頁面的標記中。 `@`字元會標示頁面中的 ASP.NET Web Pages 程式碼。

再次執行頁面（WebMatrix 會在執行頁面之前為您儲存變更）。 這次您會在頁面中看到日期和時間。

![&quot;以 &quot; 動態方式產生的時間顯示，在瀏覽器中執行的 Hello World 頁面](getting-started/_static/image20.png)

請稍候片刻，然後在瀏覽器中重新整理頁面。 日期和時間顯示會更新。

在瀏覽器中，查看頁面來源。 它看起來會像下面這樣的標記：

[!code-html[Main](getting-started/samples/sample5.html)]

請注意， `@{ }` 頂端的區塊不存在。 另請注意，日期和時間顯示會顯示實際的字元字串（ `1/18/2012 2:49:50 PM` 或任何內容），而不 `@currentDateTime` 像您在*cshtml*頁面中的一樣。 這裡發生的情況是，當您執行頁面時，ASP.NET 已處理標記為的所有程式碼（在此案例中很少） `@` 。 程式碼會產生輸出，並將該輸出插入頁面中。

## <a name="this-is-what-aspnet-web-pages-are-about"></a>這就是 ASP.NET Web Pages 的相關資訊

當您閱讀該 ASP.NET Web Pages 會產生動態 Web 內容時，您在這裡看到的就是這個概念。 您剛才建立的頁面包含您之前看到的相同 HTML 標籤。 它也可以包含可執行各種工作的程式碼。 在此範例中，它執行的是取得目前日期和時間的簡單工作。 如您所見，您可以使用 HTML 來散置程式碼，以在頁面中產生輸出。 當有人在瀏覽器中要求 [ *cshtml* ] 頁面時，ASP.NET 會在網頁伺服器仍在手中時處理該頁面。 ASP.NET 會將程式碼的輸出（如果有的話）插入頁面中做為 HTML。 當程式碼處理完成時，ASP.NET 會將產生的頁面傳送到瀏覽器。 所有瀏覽器都是 HTML。 圖表如下：

![ASP.NET 如何動態產生 HTML 的概念流程](getting-started/_static/image21.png)

概念很簡單，但程式碼可以執行許多有趣的工作，而且有很多有趣的方式可讓您將 HTML 內容動態新增至頁面。 而 ASP.NET *，* 如同任何 HTML 網頁，也可以包含在瀏覽器本身（JavaScript 和 jQuery 程式碼）中執行的程式碼。 在本教學課程中，您將會探索所有這些專案，並在後續設定。

## <a name="coming-up-next"></a>下一步

在此系列的下一個教學課程中，您將深入探索 ASP.NET Web Pages 程式設計。

## <a name="additional-resources"></a>其他資源

[從頭開始建立 ASP.NET 網站](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)。 本教學課程特別說明如何使用 WebMatrix （不 ASP.NET Web Pages）。 另外還有一些關於 WebMatrix 的其他功能，我們將不會在本教學課程中討論到的詳細資訊。

> [!div class="step-by-step"]
> [下一步](intro-to-web-pages-programming.md)
