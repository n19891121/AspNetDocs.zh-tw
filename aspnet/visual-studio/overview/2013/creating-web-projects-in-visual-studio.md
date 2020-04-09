---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: 在可視化工作室創建ASP.NET Web 專案 2013 |微軟文件
author: tdykstra
description: 本主題介紹在 Visual Studio 2013 中創建ASP.NET Web 專案的選項,其中介紹了 Web 開發中的一些新功能。
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676045"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>在 Visual Studio 2013 中建立 ASP.NET Web 專案

湯姆[·戴克斯特拉](https://github.com/tdykstra)

> 本主題介紹使用 Update 3 在 Visual Studio 2013 中建立ASP.NET Web 專案的選項
> 
> 與早期版本的 Visual Studio 相比,以下是 Web 開發中的一些新功能:
> 
> - 用於建立支援[多個ASP.NET架構](#add)(Web 窗體、MVC 和 Web API)的專案的簡單 UI。
> - [ASP.NET標識](#indauth),一個新的ASP.NET成員系統,在所有ASP.NET框架中都工作相同,並且與IIS以外的Web託管軟體配合使用。
> - 使用[Bootstrap](#bootstrap)提供回應式設計和準備功能。
> - 以前只為 MVC 提供的 Web 窗體的新功能,例如[自動測試項目建立](#testproj)與 Intranet[網站樣本](#winauth)。
> 
> 有關如何為 Azure 雲端服務或 Azure 行動服務建立 Web 專案的資訊,請參閱[使用 Azure 雲端服務開始使用「ASP.NET」](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/)以及[使用 Azure 行動服務 .NET 後端建立排行榜應用](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)。

<a id="prerequisites"></a>
## <a name="prerequisites"></a>Prerequisites

本文適用於安裝了[更新 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409)的 Visual [Studio 2013。](https://go.microsoft.com/fwlink/?LinkId=306566)

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>Web 應用程式專案與網站專案

ASP.NET在兩種Web專案之間做出選擇 *:Web應用程式*專案和*網站專案*。 我們建議 Web 應用程式專案用於新開發,本文僅適用於 Web 應用程式專案。 有關詳細資訊,請參閱 MSDN 網站上的[Visual Studio 中的 Web 應用程式專案與網站專案](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx)。

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>Web 應用程式項目建立概述

以下步驟展示如何建立 Web 專案:

1. 按下 **「開始」** 頁或 **「檔案**」 選單中的 **「新專案**」 。
2. 在**新項目對話**框中,按下左方窗格中的**Web,** 並在中間窗格**中按下 ASP.NET Web 應用程式**。

    ![[新增專案] 對話方塊](creating-web-projects-in-visual-studio/_static/image1.png)

    可以選擇左邊窗格中的 **「雲**」來建立[Azure 雲端服務](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)[、Azure 行動服務](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)或[Azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)。 本主題不包括這些範本。
3. 在右邊窗格中,如果希望對應用程式進行運行狀況和使用方式監視,請按下 **「 將應用程式見解添加到專案**」複選框。 如需詳細資訊，請參閱[監視 Web 應用程式中的效能](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/)。
4. 指定項目**名稱**、**位置**和其他選項,然後按下 **「確定**」。

    [**新增 ASP.NET 專案**] 對話方塊隨即出現。

    ![[新增專案] 對話方塊](creating-web-projects-in-visual-studio/_static/image2.png)
5. 單擊範本。

    ![選取範本](creating-web-projects-in-visual-studio/_static/image3.png)
6. 如果要添加對範本中未包括的其他框架的支援,請單擊相應的複選框。 (在所示示例中,您可以將 MVC 和/或 Web API 添加到 Web 窗體專案中。

    ![新增框架](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>如果要添加單元測試專案,請按一下「**添加單元測試**」。

    ![新增單元測試](creating-web-projects-in-visual-studio/_static/image5.png)
8. 如果想要與範本預設提供的身份驗證方法不同的身份驗證方法,請單擊「**更改身份驗證**」。

    ![設定驗證按鈕](creating-web-projects-in-visual-studio/_static/image6.png)

    ![設定驗證對話框](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>在 Azure 建立 Web 應用或虛擬機器

Visual Studio 包含的功能,使使用 Azure 服務輕鬆託管 Web 應用程式。 例如,您可以在 Visual Studio IDE 執行以下所有操作:

- 創建和管理 Web 應用或虛擬機器,使應用程式在 Internet 上可用。
- 查看應用程式在雲端中執行時創建的紀錄。
- 應用程式在雲中運行時,在調試模式下遠端運行。
- 查看和管理其他 Azure 服務,如 SQL 資料庫。

您可以創建包含基本服務(如免費 Web 應用)的[Azure 帳戶](https://www.windowsazure.com/pricing/free-trial/),如果您是 MSDN 訂閱者,則可以[啟動每月](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/)為其他 Azure 服務提供積分的好處。 

預設情況下,「**新建ASP.NET專案」** 對話框使您能夠為新 Web 專案建立 Web 應用或虛擬機器。 如果不想創建新的 Web 應用或虛擬機,請清除**雲端中的「主機**」複選框。

![建立遠端資源](creating-web-projects-in-visual-studio/_static/image8.png)

複選框標題可能是**雲中的主機**或**創建遠端資源**,在這兩種情況下效果都相同。 如果選中選取中該複選框,Visual Studio 預設情況下會在 Azure 應用服務中創建 Web 應用。 如果您願意,可以使用下拉框將此方塊更改為**虛擬機器**。 如果您尚未登錄到 Azure,系統將提示您輸入 Azure 認證。 登錄後,一個對話框允許您配置 Visual Studio 將為專案創建的資源。 下圖顯示了 Web 應用的對話方塊;如果選擇創建虛擬機,則會出現不同的選項。

![設定 Azure 應用設定](creating-web-projects-in-visual-studio/_static/image9.png)

有關如何使用此過程建立 Azure 資源的詳細資訊,請參閱使用 Azure[啟動和 ASP.NET](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)以及[使用 Visual Studio 為網站建立虛擬機器](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)。

本文的其餘部分提供了有關可用範本及其選項的詳細資訊。 本文還介紹了範本中使用的 Bootstrap、佈局和準備框架。

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>視覺化工作室 2013 Web 專案範本

Visual Studio 使用範本創建 Web 專案。 專案範本可以在新項目中創建檔和資料夾,安裝 NuGet 包,並為基本工作應用程式提供範例代碼。 樣本實現最新的 Web 標準,旨在展示如何使用 ASP.NET 技術的最佳做法,並讓您開始創建自己的應用程式。

Visual Studio 2013 為針對 .NET 4.5 或更高版本的 .NET 框架的專案提供以下 Web 專案樣本選項:

- [空範本](#empty)
- [Web 表單範本](#wf)
- [MVC 範本](#mvc)
- [Web API 範本](#webapi)
- [單頁應用程式範本](#spa)
- [Azure 行動服務範本](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [視覺工作室 2012 範本](#vs2012)

您還可以安裝提供[Facebook 範本](#facebook)的視覺工作室擴展。

有關如何建立面向 .NET 4 的項目的資訊,請參閱本主題後面的[Visual Studio 2012 範本](#vs2012)。

有關如何為行動客戶端建立ASP.NET應用程式的資訊,請參閱 ASP.NET[中的行動支援](../../../mobile/overview.md)。

<a id="empty"></a>
### <a name="empty-template"></a>空範本

"空"樣本為ASP.NET Web 應用(如專案檔 *(.csproj*或 )提供最少的資料夾和檔。*vbproj*) 和*Web.config*檔。 您可以使用「**新增資料夾」 下的複選框和核心引用**:標籤,添加對 Web 窗體、MVC 和/或 Web API 的支援。

對於空範本,沒有可用的身份驗證選項。 身份驗證功能在示例應用程式中實現,空範本不建立範例應用程式。

<a id="wf"></a>
### <a name="web-forms-template"></a>Web 表單範本

Web 表單結構框架提供以下功能,讓您能夠快速產生具有豐富 UI 和資料存取功能的網站:

- 視覺工作室的 WYSIWYG 設計師。
- 呈現 HTML 的伺服器控制項,以及可以透過設定屬性和樣式進行自訂的伺服器控制項。
- 用於數據訪問和數據顯示的豐富類型控制項。
- 公開事件的事件模型,您可以像對用戶端應用程式(如 WPF)進行程式設計一樣進行程式設計。
- 自動在 HTTP 請求之間保留狀態(數據)。

通常,與使用ASP.NET MVC 框架創建同一應用程式相比,創建Web窗體應用程式所需的程式設計工作量更少。 但是,Web 窗體並不僅僅用於快速應用程式開發。 有許多複雜的商業應用程式和框架建立在 Web 窗體之上。

由於 Web 窗體頁和頁面上的控制器會自動生成發送到瀏覽器的大部分標記,因此您沒有 ASP.NET MVC 提供的 HTML 的細粒度控制。 用於配置頁面和控制的聲明性模型最大限度地減少了必須編寫的代碼量,但隱藏了 HTML 和 HTTP 的某些行為。 例如,並不總是能夠準確指定控制項可能生成哪些標記。

Web 表單框架不像 MVC ASP.NET 一樣容易適應基於模式的開發實作,例如[測試驅動開發](http://en.wikipedia.org/wiki/Test-driven_development)、[關注分離](http://en.wikipedia.org/wiki/Separation_of_concerns),[控制反向](http://en.wikipedia.org/wiki/Inversion_of_control)與[相依的 。](http://en.wikipedia.org/wiki/Dependency_injection) 如果要用這種方式編寫分解的代碼,可以;它只是不像ASP.NETMVC框架那樣自動。 [ASP.NET Web 窗體 MVP](http://webformsmvp.com/)專案展示了一種有助於區分關注點和可測試性的方法,同時保持 Web 窗體為交付而構建的快速開發。 微軟 SharePoint 建立在 Web 表單 MVP 之上。

Web 表單表板建立範例 Web 窗體應用程式,該應用程式使用[Bootstrap](#bootstrap)提供回應式設計和主發功能。 下圖顯示了主頁。

![Web 表單範本應用程式主頁](creating-web-projects-in-visual-studio/_static/image10.png)

有關 Web 表單的詳細資訊,請參閱[ASP.NET Web 窗體](https://asp.net/web-forms)。 有關 Web 表單樣本為您做什麼的資訊,請參閱使用[Visual Studio 2013 建構基本 Web 表單應用程式](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)。

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC 範本

ASP.NET MVC 旨在促進基於模式的開發實作,例如[測試驅動開發](http://en.wikipedia.org/wiki/Test-driven_development)、[關注分離](http://en.wikipedia.org/wiki/Separation_of_concerns)、[控制反轉](http://en.wikipedia.org/wiki/Inversion_of_control)與[相依法 。](http://en.wikipedia.org/wiki/Dependency_injection) 該框架鼓勵將 Web 應用程式的業務邏輯層與其表示層分開。 通過將應用程式劃分為模型 (M)、視圖 (V) 和控制器 (C),ASP.NET MVC 可以更輕鬆地管理較大應用程式中的複雜性。

使用ASP.NET MVC,您更直接地使用 HTML 和 HTTP 而不是 Web 窗體。 例如,Web 窗體可以在 HTTP 請求之間自動保留狀態,但您必須在 MVC 中顯式編寫代碼。 MVC 模型的優點是,它使您能夠完全控制應用程式正在執行的操作以及它在 Web 環境中的表現。 缺點是您必須編寫更多的代碼。

MVC 設計為可擴展,使電力開發人員能夠根據他們的應用程式需求自定義框架。 此外,ASP.NET MVC 原始程式碼在 OSI 許可證下可用。

MVC 模板創建一個範例 MVC 5 應用程式,該應用程式使用[Bootstrap](#bootstrap)提供回應式設計和主旋律功能。 下圖顯示了主頁。

![MVC 範例應用程式](creating-web-projects-in-visual-studio/_static/image11.png)

有關 MVC 的詳細資訊,請參閱[ASP.NET MVC](https://asp.net/mvc)。 有關如何選擇 MVC 4 樣本的資訊,請參閱本文後面的[Visual Studio 2012 樣本](#vs2012)。

<a id="webapi"></a>
### <a name="web-api-template"></a>Web API 範本

Web API 樣本基於 Web API 建立範例 Web 服務,包括基於 MVC 的 API 幫助頁。

ASP.NET Web API 是一個架構，可輕易建置 HTTP 服務並擴及廣大的用戶端範圍，包括瀏覽器和行動裝置。 ASP.NET Web API 是在 .NET 框架上構建 RESTful 服務的理想平臺。

Web API 範本建立範例 Web 服務。 下圖顯示了示例幫助頁。

![Web API 說明頁](creating-web-projects-in-visual-studio/_static/image12.png)

![用於 GET API 的 Web API 說明頁](creating-web-projects-in-visual-studio/_static/image13.png)

有關 Web API 的詳細資訊,請參閱[ASP.NET Web API](https://asp.net/web-api)。

<a id="spa"></a>
### <a name="single-page-application-template"></a>單一網頁應用程式範本

單頁應用程式 (SPA) 樣本建立一個範例應用程式,該應用程式在用戶端上使用 JavaScript、HTML 5 和[挖空JS,](http://knockoutjs.com/)並在伺服器上 ASP.NET Web API。

SPA 樣本的唯一身份驗證選項是[個人使用者帳戶](#indauth)。

下圖顯示了 SPA 範本生成的範例應用程式的初始狀態。

![SPA 範例應用程式](creating-web-projects-in-visual-studio/_static/image14.png)

有關如何使用 SPA 樣本建立應用程式的資訊,請參閱[Web API - 外部身份驗證服務](../../../web-api/overview/security/external-authentication-services.md)。

有關ASP.NET單頁應用程式以及使用 JAVAScript 框架(而不是挖空JS)的其他 SPA 樣本的詳細資訊,請參閱以下資源:

- [ASP.NET單頁應用程式](../../../single-page-application/index.md)。
- [瞭解 VS2013 RC SPA 樣本中的安全功能](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [單頁應用程式:使用ASP.NET建構現代、回應迅速的 Web 應用程式](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Facebook 樣本

您可以安裝一個[視覺工作室擴展,提供一個Facebook範本](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)。 此範本創建一個範例應用程式,該應用程式旨在在 Facebook 網站內運行。 它基於ASP.NET MVC,並使用Web API進行即時更新功能。

Facebook 範本沒有可用的身份驗證選項,因為 Facebook 應用程式在 Facebook 網站內運行,並且依賴於 Facebook 的身份驗證。

有關ASP.NET Facebook 應用程式的詳細資訊,請參閱[更新 MVC Facebook API](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)。

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>視覺工作室 2012 範本

Visual Studio 2013 Web 專案建立對話方塊不提供對 Visual Studio 2012 中提供的某些範本的訪問。 如果要使用這些範本之一,可以單擊"可視化工作室新項目"對話框左側窗格中的 Visual Studio 2012 節點。

![視覺化工作室 2012 範本](creating-web-projects-in-visual-studio/_static/image15.png)

**Visual Studio 2012**節點允許您在 Visual Studio 2013 的預設樣本清單中選擇您無法存取的以下 Web 樣本:

- ASP.NET MVC 4 Web 應用程式
- ASP.NET 動態資料實體 Web 應用程式
- ASP.NET AJAX 伺服器控制
- ASP.NET AJAX 伺服器控制擴充器
- ASP.NET 伺服器控制

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>視覺化工作室 2013 Web 專案範本中的引導

Visual Studio 2013 專案樣本使用[Bootstrap,](http://getbootstrap.com/)這是由 Twitter 創建的佈局和主框。 Bootstrap 使用 CSS3 提供回應式設計,這意味著佈局可以動態適應不同的瀏覽器視窗大小。 例如,在寬瀏覽器視窗中,Web 窗體範本建立的主頁如下所示:

![Web 表單範本應用程式主頁](creating-web-projects-in-visual-studio/_static/image16.png)

將視窗變窄,水平排列的欄移到垂直排列中:

![開機垂直柱排列](creating-web-projects-in-visual-studio/_static/image17.png)

稍微縮小視窗範圍,水平頂部選單將變為一個圖示,您可以按下該圖示以展開垂直方向的選單:

![開機選單圖示](creating-web-projects-in-visual-studio/_static/image18.png)

![開機垂直選單](creating-web-projects-in-visual-studio/_static/image19.png)

您還可以使用 Bootstrap 的「主」功能輕鬆影響應用程式的外觀和感覺的變化。 例如,您可以執行以下步驟來更改主題。

1. 在瀏覽器中,轉到[http://Bootswatch.com](http://Bootswatch.com),選擇主題,然後單擊"**下載**"。 (默認情況下,此下載*引導.min.css;* 如果要檢查 CSS 代碼,請獲取*引導.css*而不是小版本。
2. 複製下載的 CSS 檔的內容。
3. 在 Visual Studio 中,在*內容*資料夾中創建名為*bootstrap-thethe.css*的新**樣式表**檔,並將下載的 CSS 代碼貼上到其中。
4. 開啟*\_應用程式 開始/捆綁.設定*與變更*開機主機主題.css*.*bootstrap-theme.css*

再次運行專案,應用程式具有新外觀。 下圖顯示了阿米莉亞主題的效果:

![靴子阿米莉亞主題](creating-web-projects-in-visual-studio/_static/image20.png)

許多引導主題是可用的,無論是免費和高級版本。 Bootstrap 提供多種 UI 元件,如[下拉](http://twitter.github.io/bootstrap/components.html#dropdowns),[按鈕群組](http://twitter.github.io/bootstrap/components.html#buttonGroups)與[圖示](http://twitter.github.io/bootstrap/base-css.html#images)。 有關引導器的詳細資訊,請參閱[引導網站](http://twitter.github.io/bootstrap/)。

如果在 Visual Studio 中使用 Web 窗體設計器,請注意,設計器不支援 CSS3,因此無法準確顯示 Bootstrap 主題或回應式佈局更改的所有效果。 但是,使用瀏覽器查看時,Web 窗體頁面將正確顯示。

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>新增對附加框架

選擇範本時,將自動選擇範本所使用的框架的複選框。 例如,如果選擇 **「Web 窗體」** 樣本,則選中 **「Web 窗體」** 複選框,但無法清除該範本。

![選取範本](creating-web-projects-in-visual-studio/_static/image21.png)

![新增框架](creating-web-projects-in-visual-studio/_static/image22.png)

可以為範本中未包含的框架選擇複選框,以便在創建專案時添加對該框架的支援。 例如,要在選擇 MVC 範本時啟用 Web 窗體 *.aspx*頁面的使用,請選擇 **「Web 窗體」** 複選框。 或者,要在使用 Web 窗體範本時啟用 MVC,請單擊**MVC**複選框。 添加框架可實現設計時和運行時支援。 例如,如果將 MVC 支援添加到 Web 窗體專案,則可以對控制器和視圖進行基架。

如果在專案中組合 Web 窗體和 MVC 並在 Web 窗體中啟用[友好 URL,](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx)則可能存在意外的路由問題,其中一個 URL 具有多個可能的目標。 首先定義的路由將優先。 例如`Home`,如果您有控制器和*Home.aspx*頁,`http://contoso.com/home`則如果在`Home``MapRoute``EnableFriendlyUrls``EnableFriendlyUrls``MapRoute` *RouteConfig.cs*調用 該方法之前調用 該方法,則 URL 將轉到*Home.aspx,* 或者,如果之前調用,則相同的 URL 將轉到控制器的預設檢視。

添加框架不會添加任何範例應用程式功能。 例如,如果在選擇 MVC 樣本時添加 Web 窗體支援,則不會創建*Default.aspx*主頁檔。 僅添加支援框架所需的資料夾、檔案和引用。 因此,添加框架不會更改身份驗證選項,這些選項由範本創建的範例應用程式中的代碼實現。 例如,如果選擇「空範本」並添加 Web 窗體或 MVC 支援,則仍將禁用 **「設定身份驗證」** 按鈕。

以下各節簡要描述每個複選框的效果。

### <a name="add-web-forms-support"></a>新增 Web 表單支援

建立空*的應用\_資料和**模型*資料夾和*全域.asax*檔案。 這些範本已由空範本以外的所有範本創建,因此選擇"Web 窗體"複選框對其他範本沒有影響。

預設情況下,Web 窗體範本啟用友好 URL,但當您透過選擇「Web 窗體」複選框將 Web 窗體支援添加到其他樣本時,不會自動啟用"友好 URL"。

### <a name="add-mvc-support"></a>新增 MVC 支援

安裝 MVC、Razor 和 WebPages NuGet 套件,建立空*的應用\_資料*,*控制器*,*模型*與*檢視*資料夾,使用*RouteConfig.cs*檔案建立*\_應用程式啟動*資料夾,並創建*Global.asax*檔。

### <a name="add-web-api-support"></a>新增 Web API 支援

安裝 WebApi 和 Newtonsoft.Json NuGet 套件,建立空*的應用程式\_資料*,*控制器*和*模型*資料夾,建立包含*WebApiConfig.cs*檔案*\_的應用程式啟動*資料夾,並創建*Global.asax*檔案。

<a id="auth"></a>
## <a name="authentication-methods"></a>驗證方法

Visual Studio 2013 為 Web 窗體、MVC 和 Web API 樣本提供多個身份驗證選項:

- [沒有認證](#noauth)
- [個人使用者帳戶](#indauth)(ASP.NET標識,以前稱為ASP.NET成員資格)
- [組織帳號](#orgauth)(Windows 伺服器活動目錄或 Azure 活動目錄)
- [視窗認證](#winauth)(內聯網)

![設定驗證對話框](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>不需要驗證

如果選擇 **「無身份認證」 ,** 則範例將不包含用於登入的網頁、指示登入者使用的 UI、成員資格資料庫的實體類以及成員資格資料庫的連接字串。

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>個別使用者帳戶

如果選擇 **「個人使用者帳戶**」,則示例應用程式將配置為使用ASP.NET標識(以前稱為ASP.NET成員資格)進行使用者身份驗證。 ASP.NET身份允許使用者透過在網站上創建使用者名稱和密碼或與 Facebook、Google、微軟帳戶或 Twitter 等社交供應商登錄來註冊帳戶。 ASP.NET識別中使用者配置檔的預設資料儲存是 SQL Server LocalDB 資料庫,您可以將該資料庫部署到生產網站的 SQL Server 或 Azure SQL 資料庫。

在 Visual Studio 2013 中,這些功能與 Visual Studio 2012 中的功能相同,但 ASP.NET 成員資格系統的基礎代碼已被重寫。 新代碼庫的優點包括:

- 新的成員資格系統基於[OWIN](http://owin.org/)而不是ASP.NET窗體身份驗證模組。 這意味著無論您是在 IIS 中使用 Web 窗體還是 MVC,還是自託管 Web API 或 SignalR,您都可以使用相同的身份驗證機制。
- 新的成員資格資料庫由實體框架代碼優先管理,所有表都由可以修改的實體類表示。 這意味著您可以輕鬆地自定義資料庫架構和設定檔相關的 Web UI 以滿足您自己的需求,並且可以使用程式碼優先遷移輕鬆部署更新。

新的成員資格系統在新範本中自動實現,可以在以 .NET 4.5 或更高版本為目標的任何專案中手動實現。

ASP.NET身份是一個不錯的選擇,如果你正在創建一個互聯網網站,主要是為外部客戶。 如果您的組織使用 Active Directory 或 Office 365,並且希望創建一個為員工和業務合作夥伴啟用單一登錄的專案,則 **「組織帳戶」** 選項可能是一個更好的選擇。

有關「個人使用者帳戶」選項的詳細資訊,請參閱以下資源:

- [www.asp.net/identity](../../../identity/index.md). 有關ASP.NET網站上ASP.NET標識的文檔。
- [建立 ASP.NETMVC 5 應用程式與 Facebook 和 GoogleAuth2 和開放 ID 登錄](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。 還演示如何自定義使用者配置文件數據。
- [Web API - 外部認證服務](../../../web-api/overview/security/external-authentication-services.md)
- [在 Visual Studio 2013 中向 ASP.NET 應用程式新增外部登入](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>組織帳戶

如果選擇 **「組織帳戶**」,則示例應用程式將配置為使用 Windows 識別基礎 (WIF) 根據 Azure 活動目錄(Azure AD,包括 Office 365)或 Windows 伺服器活動目錄中的使用者帳戶進行身份驗證。 有關詳細資訊,請參閱本主題後面的[組織帳戶身份驗證選項](#orgauthoptions)。

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows 驗證

如果選擇**Windows 身份驗證**,則示例應用程式將配置為使用 Windows 身份驗證 IIS 模組進行身份驗證。 應用程式將顯示登入 Windows 但不包括使用者註冊或登入 UI 的 Active 目錄或本地電腦帳戶的網域和使用者 ID。 此選項適用於 Intranet 網站。

或者,您可以通過在[組織帳戶下選擇"本地"選項](#orgauthonprem)來創建使用 AD 身份驗證的 Intranet 網站。 「本地」選項使用 Windows 識別基礎 (WIF) 而不是 Windows 身份驗證模組。 需要執行一些其他步驟才能設置"本地"選項,但 WIF 啟用 Windows 身份驗證模組中不可用的功能。 例如,使用 WIF 可以在 Active Directory 和查詢目錄數據中設定應用程式訪問。

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>組織帳號身份驗證選項

**設定身份驗證對話**框為 Azure 活動目錄(Azure AD,包括 Office 365)或 Windows 伺服器活動目錄 (AD) 帳戶身份驗證提供了多個選項:

- [雲 - 單個組織](#orgauthsingle)(使用與 Azure AD 的目錄整合的 Azure AD 或 AD)
- [雲 - 多組織](#orgauthmulti)(使用目錄與 Azure AD 整合的 Azure AD 或 AD)
- [內部(AD)](#orgauthonprem)

如果要嘗試 Azure AD 選項之一,但尚未擁有帳戶,[請按下此處註冊 Azure AD 帳號](https://go.microsoft.com/fwlink/?LinkId=309942)。

> [!NOTE]
> 如果選擇 Azure AD 選項之一,則專案需要資料庫,並且必須登錄到 Azure AD 租戶的全域管理員帳戶。 輸入具有 Azure AD 租戶管理許可權的組織帳戶admin@contoso.onmicrosoft.com的名稱 和密碼。
> 
> **不要在登錄對話框中輸入 Microsoft 帳戶的認證(例如contoso@hotmail.com)。**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>雲 - 單一組織認證

![單一組織識別](creating-web-projects-in-visual-studio/_static/image24.png)

如果要為一個 Azure AD[租戶](https://technet.microsoft.com/library/jj573650.aspx)中定義的使用者帳戶啟用身份驗證,請選擇此選項。 例如,該網站contoso.com,它將提供給 Contoso 公司位於租戶contoso.onmicrosoft.com的員工。 您將無法將 Azure AD 設定為允許其他租戶的使用者存取應用程式。

#### <a name="domain"></a>網域

輸入要在 中設定應用程式的 Azure AD`contoso.onmicrosoft.com`網域,例如: 如果您有[自定義域](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)`contoso.com`,`contoso.onmicrosoft.com`例如 , 可以在此處輸入該域。

#### <a name="access-level"></a>存取層級

如果應用程式需要使用圖形 API 查詢或更新目錄資訊,請選擇**單一登入、讀取目錄資料**或**單一登入、讀取及寫入目錄資料**。 否則,請選擇**單一登入**。 有關詳細資訊,請參閱[應用程式存取等級](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels)和使用圖形[API 查詢 Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)。

#### <a name="application-id-uri"></a>應用程式識別碼

預設情況下,範本通過將專案名稱追加到 Azure AD 功能,為您創建應用程式 ID URI。 例如,如果專案名稱稱為`Example`,並且網`contoso.onmicrosoft.com`域為 ,則`https://contoso.onmicrosoft.com/Example`應用程式 ID URI 變為 。 如果要手動指定應用程式 ID URI,請展開 **「更多選項」** 部分,並在文字框中輸入應用程式 ID URI。 應用程式識別碼必須`https://`以開頭。

預設情況下,如果已在 Azure AD 中預配的應用程式具有與 Visual Studio 用於專案的應用程式 ID URI 相同的應用程式 ID URI,則專案將連接到現有應用程式,而不是預配新應用程式。 如果希望在這種情況下預配新應用程式,**請清除「覆蓋應用程式項目」(如果具有相同 ID 的應用程式條目已存在**)複選框。

如果清除 **「覆蓋**」複選框,並且 Visual Studio 尋找具有相同應用程式 ID URI 的現有應用程式,則透過將數位追加到要使用的 URI 來創建新 URI。 例如,假設專案名稱為`Example`,您將文本框留空,清除**覆蓋**複選框,Azure AD 租戶`https://contoso.onmicrosoft.com/Example`已具有帶有 URI 的應用程式。 在這種情況下,將預配一個新應用程式,並設定應用程式 ID URI,如`https://contoso.onmicrosoft.com/Example_20130619330903`。

#### <a name="provisioning-the-application-in-azure-ad"></a>在 Azure AD 中預先應用程式

為了在 Azure AD 中預配應用程式或將專案連接到現有應用程式,Visual Studio 需要域的全域管理員的認證。 在「**設定身份驗證**」對話框中按下 **「確定」** 時,系統會提示您輸入您指定的網域的全域管理員的使用者名稱和密碼。 稍後,當您按下 **「新建ASP.NET專案**」對話框中**創建專案**時,Visual Studio 在 Azure AD 中提供應用程式。 請注意,作為此過程的一部分,Visual Studio 會在 Web.config 檔中嵌入用戶端機密值,該檔在創建一年後過期。

有關如何建立使用**雲 - 單一組織**認證的應用程式的資訊,請參閱以下資源:

- [Azure 認證](../2012/windows-azure-authentication.md)
- [使用 Azure AD 將登入新增至 Web 應用程式](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [使用 Azure Active Dirctory 開發 ASP.NET 應用程式](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [使用 Azure AD 和 Microsoft OWIN 元件ASP.NET Web API 安全](https://msdn.microsoft.com/magazine/dn463788.aspx)

Visual Studio 2013 的教程尚未更新;教程指導您手動執行的一些操作在 Visual Studio 2013 中是自動化的。

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>雲 - 多組織認證

![多個組織身份驗證](creating-web-projects-in-visual-studio/_static/image25.png)

如果要為多個 Azure AD[租戶](https://technet.microsoft.com/library/jj573650.aspx)中定義的使用者帳戶啟用身份驗證,請選擇此選項。 例如,該網站contoso.com,它將提供給 contoso 公司位於contoso.onmicrosoft.com租戶的員工以及法布裡卡姆公司fabrikam.onmicrosoft.com租戶的員工。

輸入的設定與應用程式預先定義的步驟來顯示[單一個組織認證](#orgauthsingle)。

有關如何創建使用**雲 - 多組織**認證的應用程式的資訊,請參閱以下資源:

- [輕鬆 Web 應用程式與&amp;Azure 活動 目錄整合,ASP.NET活動目錄團隊部落格上的視覺化工作室](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx)。
- [使用 Azure AD 教學開發多租戶 Web 應用程式](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx)。 本教程尚未更新為 Visual Studio 2013;本教學指導您手動執行的一些操作在 Visual Studio 2013 中是自動化的。
- [您必須在應用程式ASP.NET使用自己的多個組織註冊,然後才能登錄](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/)。 Vittorio Bertocci 的部落格,解釋如何解決人們在創建使用多組織身份驗證的專案時遇到的常見問題。

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>本地組織身份驗證

![本地組織身份驗證](creating-web-projects-in-visual-studio/_static/image26.png)

如果要為 Windows 伺服器活動目錄 (AD) 中定義的使用者帳戶啟用身份驗證,並且不想使用 Azure AD,請選擇此選項。 您可以使用此選項創建 Intranet 網站或 Internet 網站。 對於 Internet 網站,請使用活動目錄聯合服務 (ADFS) 提供對 AD 的訪問。 有關詳細資訊,請參閱在[Visual Studio 2013 中使用具有ASP.NET的本地組織身份驗證選項 (ADFS)。](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)

對於 Intranet 網站,作為替代方法,您可以選擇[Windows 身份驗證](#winauth)而不是此選項。 對於 Windows 身份驗證選項,您不必提供中繼資料文件 URL。 但是,Windows 身份驗證無法控制活動目錄中的應用程序訪問或查詢目錄數據。

#### <a name="on-premises-authority"></a>內部管理局

輸入指向元資料文件的 URL。 元數據文件包含許可權的座標。 應用程式將使用這些座標來驅動 Web 登錄流。

#### <a name="application-id-uri"></a>應用程式識別碼

提供 AD 可用於識別此應用程式的唯一 URI,或留空以讓 Visual Studio 創建一個。

<a id="nextsteps"></a>
## <a name="next-steps"></a>後續步驟

本文件為在 Visual Studio 2013 中創建新 ASP.NET Web 專案提供了一些基本説明。 有關將 Visual Studio 用於 Web[https://www.asp.net/visual-studio/](../../index.md)開發的詳細資訊 ,請參閱。
