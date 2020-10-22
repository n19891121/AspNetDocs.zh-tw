---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: 在 Visual Studio 2013 中建立 ASP.NET Web 專案 |Microsoft Docs
author: tdykstra
description: 本主題說明使用 Update 3 在 Visual Studio 2013 中建立 ASP.NET Web 專案的選項。以下是一些 web 程式開發的新功能 .。。
ms.author: riande
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: fbb4cd7afa2506879d47bce980bf0164aad40c2c
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345464"
---
# <a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>在 Visual Studio 2013 中建立 ASP.NET Web 專案

由 [Tom Dykstra](https://github.com/tdykstra)

> 本主題說明使用 Update 3 在 Visual Studio 2013 中建立 ASP.NET Web 專案的選項
> 
> 以下是與舊版 Visual Studio 相較之下，網頁程式開發的一些新功能：
> 
> - 用來建立專案的簡單 UI，可 [支援多個 ASP.NET](#add) 架構， (WEB FORM、MVC 和 Web API) 。
> - [ASP.NET Identity](#indauth)是一種新的 ASP.NET 成員系統，其在所有 ASP.NET 架構中的運作方式都相同，並且可與 IIS 以外的 web 裝載軟體搭配運作。
> - 使用 [啟動](#bootstrap) 程式來提供回應式設計和主題功能。
> - Web Form 的新功能，這些功能僅供 MVC 使用，例如 [自動測試專案建立](#testproj) 和 [內部網路網站範本](#winauth)。
> 
> 如需有關如何建立 Azure 雲端服務或 Azure 行動服務之 Web 專案的詳細資訊，請參閱[使用 Azure 雲端服務的開始，以及](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/)[使用 Azure 行動服務 .Net 後端建立排行榜應用程式](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)。

<a id="prerequisites"></a>
## <a name="prerequisites"></a>先決條件

本文適用于已安裝[Update 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409)的[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) 。

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>Web 應用程式專案與網站專案的比較

ASP.NET 可讓您選擇兩種 Web 專案： *web 應用程式專案* 和 *網站專案*。 我們建議用於新開發的 web 應用程式專案，而本文只適用于 web 應用程式專案。 如需詳細資訊，請參閱 MSDN 網站上 [Visual Studio 中的 Web 應用程式專案和網站專案](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) 。

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>Web 應用程式專案建立總覽

下列步驟示範如何建立 Web 專案：

1. 在 [**開始**] 頁面或 [檔案 **] 功能表中，按一下**[**新增專案**]。
2. 在 [ **新增專案** ] 對話方塊中，按一下左窗格中的 [ **web** ]，然後在中間窗格中 **ASP.NET web 應用程式** 。

    ![[新增專案] 對話方塊](creating-web-projects-in-visual-studio/_static/image1.png)

    您可以在左窗格中選擇 [ **雲端** ] 來 [建立 azure 雲端服務](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)、 [Azure 行動服務](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx)或 [azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)。 本主題未涵蓋這些範本。
3. 如果您想要應用程式的健全狀況和使用方式監視，請在右窗格中按一下 [ **將 Application Insights 新增至專案** ] 核取方塊。 如需詳細資訊，請參閱[監視 Web 應用程式中的效能](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/)。
4. 指定專案 **名稱**、 **位置**和其他選項，然後按一下 **[確定]**。

    [**新增 ASP.NET 專案**] 對話方塊隨即出現。

    ![[新增專案] 對話方塊](creating-web-projects-in-visual-studio/_static/image2.png)
5. 按一下範本。

    ![選取範本](creating-web-projects-in-visual-studio/_static/image3.png)
6. 如果您想要新增不包含在範本中其他架構的支援，請按一下適當的核取方塊。  (在顯示的範例中，您可以將 MVC 和/或 Web API 新增至 Web Form 專案。 ) 

    ![新增架構](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>如果您想要加入單元測試專案，請按一下 [ **加入單元**測試]。

    ![新增單元測試](creating-web-projects-in-visual-studio/_static/image5.png)
8. 如果您想要與範本預設提供的不同驗證方法，請按一下 [ **變更驗證**]。

    ![設定驗證按鈕](creating-web-projects-in-visual-studio/_static/image6.png)

    ![[設定驗證] 對話方塊](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>在 Azure 中建立 web 應用程式或虛擬機器

Visual Studio 包含的功能，可讓您輕鬆地使用 Azure 服務來裝載 web 應用程式。 例如，您可以從 Visual Studio IDE 進行下列擁有權限：

- 建立和管理 web 應用程式或虛擬機器，讓您的應用程式可透過網際網路使用。
- 查看應用程式在雲端中執行時所建立的記錄。
- 在雲端中執行應用程式時，從遠端執行偵錯工具模式。
- 查看和管理其他 Azure 服務，例如 SQL 資料庫。

您可以建立包含基本服務的 [Azure 帳戶](https://www.windowsazure.com/pricing/free-trial/) （例如免費的 web 應用程式），而且如果您是 MSDN 訂閱者，您可以 [啟用權益](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) ，讓您享有更多 Azure 服務的每月信用額度。 

依預設，[ **新增 ASP.NET 專案** ] 對話方塊可讓您建立新 Web 專案的 web 應用程式或虛擬機器。 如果您不想要建立新的 web 應用程式或虛擬機器，請清除 [ **雲端中的主機** ] 核取方塊。

![建立遠端資源](creating-web-projects-in-visual-studio/_static/image8.png)

核取方塊標題可能是 **雲端中的主機** 或 **建立遠端資源**，而且在任何一種情況下效果都相同。 如果您將核取方塊保留為已選取，Visual Studio 預設會在 Azure App Service 中建立 web 應用程式。 如果您想要的話，可以使用下拉式方塊來將其變更為 **虛擬機器** 。 如果您尚未登入 Azure，系統會提示您輸入 Azure 認證。 登入之後，對話方塊可讓您設定 Visual Studio 將為您的專案建立的資源。 下圖顯示 web 應用程式的對話方塊;如果您選擇建立虛擬機器，則會出現不同的選項。

![設定 Azure App 設定](creating-web-projects-in-visual-studio/_static/image9.png)

如需有關如何使用此程式來建立 Azure 資源的詳細資訊，請參閱 [使用 azure 進行開始和 ASP.NET](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) ，以及 [使用 Visual Studio 建立網站的虛擬機器](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)。

本文的其餘部分會提供可用範本及其選項的詳細資訊。 本文也引進了啟動程式，也就是範本中所使用的版面配置和主題架構。

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Visual Studio 2013 Web 專案範本

Visual Studio 會使用範本來建立 Web 專案。 專案範本可以在新專案中建立檔案和資料夾、安裝 NuGet 套件，以及提供基本工作應用程式的範例程式碼。 範本採用最新的 web 標準，旨在示範如何使用 ASP.NET 技術的最佳作法，並讓您快速開始建立自己的應用程式。

針對以 .NET 4.5 或更新版本的 .NET framework 為目標的專案，Visual Studio 2013 提供下列 Web 專案範本選項：

- [空白範本](#empty)
- [Web Form 範本](#wf)
- [MVC 範本](#mvc)
- [Web API 範本](#webapi)
- [單一頁面應用程式範本](#spa)
- [Azure 行動服務範本](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [Visual Studio 2012 範本](#vs2012)

您也可以安裝提供 [Facebook 範本](#facebook)的 Visual Studio 延伸模組。

如需有關如何建立以 .NET 4 為目標之專案的詳細資訊，請參閱本主題稍後的 [Visual Studio 2012 範本](#vs2012) 。

如需如何建立行動用戶端 ASP.NET 應用程式的相關資訊，請參閱 [ASP.NET 中](../../../mobile/overview.md)的行動支援。

<a id="empty"></a>
### <a name="empty-template"></a>空白範本

空白範本會提供 ASP.NET web 應用程式的最小資料夾和檔案，例如 (*.csproj* 或的專案檔。*vbproj*) 和 *Web.config* 檔。 您可以使用 [ **新增資料夾和核心參考：** 標籤] 下的核取方塊，以新增對 WEB FORM、MVC 和/或 Web API 的支援。

若為空白範本，則沒有可用的驗證選項。 驗證功能會在範例應用程式中執行，而空白範本不會建立範例應用程式。

<a id="wf"></a>
### <a name="web-forms-template"></a>Web Form 範本

Web Form framework 提供下列功能，可讓您快速建立豐富的 UI 和資料存取功能的網站：

- Visual Studio 中的 WYSIWYG 設計工具。
- 轉譯 HTML 以及您可以藉由設定屬性和樣式進行自訂的伺服器控制項。
- 豐富的資料存取和資料顯示控制項。
- 公開事件的事件模型，您可以使用程式設計，就像是設計 WPF 等用戶端應用程式。
- 自動將狀態 (資料保留在 HTTP 要求之間) 。

一般來說，建立 Web Form 應用程式所需的程式設計工作，比使用 ASP.NET MVC 架構建立相同的應用程式需要更少的程式設計工作。 不過，Web Form 並不只是為了快速開發應用程式。 在 Web Form 之上建有許多複雜的商業應用程式和架構。

由於 Web Form 頁面和頁面上的控制項會自動產生傳送至瀏覽器的大部分標記，因此您無法對 ASP.NET MVC 所提供的 HTML 進行細微的控制。 設定頁面和控制項的宣告式模型可將您必須撰寫的程式碼數量降到最低，但會隱藏一些 HTML 和 HTTP 的行為。 例如，您不一定可以明確地指定控制項可能產生的標記。

Web Form 架構本身並不像 ASP.NET MVC，也能作為以模式為基礎的開發實務，例如 [測試導向的開發](http://en.wikipedia.org/wiki/Test-driven_development)、 [考慮的分隔](http://en.wikipedia.org/wiki/Separation_of_concerns)、 [控制反轉](http://en.wikipedia.org/wiki/Inversion_of_control)，以及相依性 [插入](http://en.wikipedia.org/wiki/Dependency_injection)。 如果您想要以這樣的方式撰寫程式碼，您可以：它並不像在 ASP.NET MVC 架構中一樣自動。 [ASP.NET WEB FORMS MVP](http://webformsmvp.com/) project 示範了一種方法，可協助分隔考慮和可測試性，同時維持建立 Web Form 的快速開發。 Microsoft SharePoint 建基於 Web Form MVP。

Web Form 範本會建立使用 [啟動](#bootstrap) 程式的範例 Web Form 應用程式，以提供回應式設計和主題功能。 下圖顯示首頁。

![Web Form 範本應用程式首頁](creating-web-projects-in-visual-studio/_static/image10.png)

如需 Web Form 的詳細資訊，請參閱 [ASP.NET Web Forms](https://asp.net/web-forms)。 如需 Web Form 範本為您做什麼的詳細資訊，請參閱 [使用 Visual Studio 2013 建立基本的 Web Form 應用程式](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)。

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC 範本

ASP.NET MVC 的設計目的是為了促進以模式為基礎的開發實務，例如 [測試導向的開發](http://en.wikipedia.org/wiki/Test-driven_development)、 [考慮的分隔](http://en.wikipedia.org/wiki/Separation_of_concerns)、 [控制反轉](http://en.wikipedia.org/wiki/Inversion_of_control)，以及相依性 [插入](http://en.wikipedia.org/wiki/Dependency_injection)。 架構鼓勵將 web 應用程式的商務邏輯層與展示層分開。 藉由將應用程式分成 (M) 的模型、views (V) 和控制器 (C) ，ASP.NET MVC 可讓您更輕鬆地管理較大型應用程式的複雜度。

使用 ASP.NET MVC，您可以更直接使用 HTML 和 HTTP 來處理 Web Form 中的。 例如，Web Form 可以自動保留 HTTP 要求之間的狀態，但您必須在 MVC 中明確撰寫程式碼。 MVC 模型的優點是，它可讓您完全掌控應用程式的運作方式，以及它在 web 環境中的運作方式。 缺點是您必須撰寫更多程式碼。

MVC 是設計成可擴充的，讓 power 開發人員能夠自訂架構以滿足其應用程式需求。 此外，ASP.NET MVC 原始程式碼可在 OSI 授權下取得。

MVC 範本會建立使用 [啟動](#bootstrap) 程式的範例 MVC 5 應用程式，以提供回應式設計和主題功能。 下圖顯示首頁。

![MVC 範例應用程式](creating-web-projects-in-visual-studio/_static/image11.png)

如需有關 MVC 的詳細資訊，請參閱 [ASP.NET mvc](https://asp.net/mvc)。 如需有關如何選取 MVC 4 範本的詳細資訊，請參閱本文稍後的 [Visual Studio 2012 範本](#vs2012) 。

<a id="webapi"></a>
### <a name="web-api-template"></a>Web API 範本

Web API 範本會根據 Web API 來建立範例 web 服務，包括以 MVC 為基礎的 API 說明頁面。

ASP.NET Web API 是一個架構，可輕易建置 HTTP 服務並擴及廣大的用戶端範圍，包括瀏覽器和行動裝置。 ASP.NET Web API 是在 .NET Framework 上建立 RESTful 服務的理想平臺。

Web API 範本會建立 web 服務範例。 下圖顯示範例說明頁面。

![Web API 說明頁面](creating-web-projects-in-visual-studio/_static/image12.png)

![GET API 的 Web API 說明頁面](creating-web-projects-in-visual-studio/_static/image13.png)

如需 Web API 的詳細資訊，請參閱 [ASP.NET Web API](https://asp.net/web-api)。

<a id="spa"></a>
### <a name="single-page-application-template"></a>單一網頁應用程式範本

單一頁面應用程式 (SPA) 範本會建立在用戶端上使用 JavaScript、HTML 5 和 [KnockoutJS](http://knockoutjs.com/) 的範例應用程式，並在伺服器上 ASP.NET Web API。

SPA 範本的唯一驗證選項是個別的 [使用者帳戶](#indauth)。

下圖顯示 SPA 範本所建立之範例應用程式的初始狀態。

![SPA 範例應用程式](creating-web-projects-in-visual-studio/_static/image14.png)

如需有關如何使用 SPA 範本建立應用程式的詳細資訊，請參閱 [WEB API-外部驗證服務](../../../web-api/overview/security/external-authentication-services.md)。

如需有關 ASP.NET 單一頁面應用程式的詳細資訊，以及使用 KnockoutJS 以外 JavaScript 架構的其他 SPA 範本的詳細資訊，請參閱下列資源：

- [ASP.NET 單一頁面應用程式](../../../single-page-application/index.md)。
- [瞭解 VS2013 RC 的 SPA 範本中的安全性功能](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [單一頁面應用程式：使用 ASP.NET 打造新式、回應式 Web Apps](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Facebook 範本

您可以安裝 [提供 Facebook 範本的 Visual Studio 延伸模組](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)。 此範本會建立一個範例應用程式，其設計目的是要在 Facebook 網站內執行。 它是以 ASP.NET MVC 為基礎，並且使用 Web API 來取得即時更新功能。

Facebook 範本不提供任何驗證選項，因為 Facebook 應用程式是在 Facebook 網站內執行，並且依賴 Facebook 的驗證。

如需 ASP.NET Facebook 應用程式的詳細資訊，請參閱 [更新 MVC FACEBOOK API](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)。

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>Visual Studio 2012 範本

Visual Studio 2013 Web 專案建立] 對話方塊不會提供 Visual Studio 2012 中可用之某些範本的存取權。 如果您想要使用其中一個範本，您可以在 Visual Studio 新增專案] 對話方塊的左窗格中，按一下 [Visual Studio 2012] 節點。

![Visual Studio 2012 範本](creating-web-projects-in-visual-studio/_static/image15.png)

[ **Visual Studio 2012** ] 節點可讓您在 Visual Studio 2013 的預設範本清單中，選擇您無法存取的下列 web 範本：

- ASP.NET MVC 4 Web 應用程式
- ASP.NET 動態資料實體 Web 應用程式
- ASP.NET AJAX 伺服器控制項
- ASP.NET AJAX 伺服器控制項擴充項
- ASP.NET 伺服器控制項

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Visual Studio 2013 Web 專案範本中的啟動程式

Visual Studio 2013 的專案範本會使用 [啟動](http://getbootstrap.com/)程式，也就是 Twitter 所建立的版面配置和主題架構。 啟動程式會使用 CSS3 來提供回應式設計，這表示版面配置可動態適應不同的瀏覽器視窗大小。 例如，在寬瀏覽器視窗中，Web Form 範本所建立的首頁看起來如下圖所示：

![Web Form 範本應用程式首頁](creating-web-projects-in-visual-studio/_static/image16.png)

讓視窗變窄，且水準排列的資料行會進入垂直排列：

![啟動程式垂直資料行相片順序](creating-web-projects-in-visual-studio/_static/image17.png)

將視窗縮小一點，然後將水準上方功能表變成圖示，讓您可以按一下以展開到垂直方向的功能表中：

![啟動程式功能表圖示](creating-web-projects-in-visual-studio/_static/image18.png)

![啟動程式垂直功能表](creating-web-projects-in-visual-studio/_static/image19.png)

您也可以使用啟動程式的主題功能，輕鬆地對應用程式的外觀和操作產生變更。 例如，您可以執行下列步驟來變更主題。

1. 在您的瀏覽器中，移至 [http://Bootswatch.com](http://Bootswatch.com) ，選擇主題，然後按一下 [ **下載**]。  (預設會下載 *啟動程式 .css* 。如果您想要檢查 CSS 程式碼，請取得 *啟動程式 .css* ，而不是縮減版本。 ) 
2. 複製下載的 CSS 檔案的內容。
3. 在 Visual Studio 中，于*Content*資料夾中建立名為*Bootstrap-theme*的新**樣式表單**檔案，然後將下載的 css 程式碼貼入其中。
4. 開啟 *應用程式 \_ 啟動/Bundle.config* ，並將 *啟動程式 .css* 變更為 *bootstrap-theme .css*。

再次執行專案，應用程式就會有新的外觀。 下圖顯示 Amelia 主題的效果：

![啟動程式 Amelia 主題](creating-web-projects-in-visual-studio/_static/image20.png)

許多啟動程式主題都可供使用，包括免費版和 premium 版。 啟動程式也提供各式各樣的 UI 元件，例如 [下拉式](http://twitter.github.io/bootstrap/components.html#dropdowns)清單、 [按鈕群組](http://twitter.github.io/bootstrap/components.html#buttonGroups)和 [圖示](http://twitter.github.io/bootstrap/base-css.html#images)。 如需啟動程式的詳細資訊，請參閱 [啟動程式網站](http://twitter.github.io/bootstrap/)。

如果您在 Visual Studio 中使用 Web Form 設計工具，請注意設計工具不支援 CSS3，因此它不會正確地顯示啟動程式主題或回應式配置變更的所有效果。 不過，使用瀏覽器來觀看 Web Form 頁面時，將會正確顯示。

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>新增其他架構的支援

當您選取範本時，會自動選取該範本所使用之架構 (s) 的核取方塊。 例如，如果您選取 **Web Form** 範本，則會選取 [ **Web Form** ] 核取方塊，而且無法清除。

![選取範本](creating-web-projects-in-visual-studio/_static/image21.png)

![新增架構](creating-web-projects-in-visual-studio/_static/image22.png)

您可以針對不包含在範本中的架構選取其核取方塊，以便在建立專案時新增該架構的支援。 例如，若要在選取 MVC 範本時使用 Web Form *.aspx* 頁面，請選取 [ **Web Form** ] 核取方塊。 或者，若要在使用 Web Form 範本時啟用 MVC，請按一下 [ **mvc** ] 核取方塊。 加入架構可啟用設計階段和執行時間支援。 例如，如果您將 MVC 支援加入 Web Form 專案中，您將能夠 scaffold 控制器和查看。

如果您將 Web Form 和 MVC 合併在專案中，並在 Web Form 中啟用 [易記 url](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) ，可能會有一個 URL 有多個可能目標的非預期路由問題。 首先定義的路由會優先。 例如，如果您有一個 `Home` 控制器和一個*default.aspx*頁面，則 `http://contoso.com/home` 如果您在 RouteConfig.cs 中呼叫方法之前呼叫方法，url 將會移至*default.aspx* ， `EnableFriendlyUrls` `MapRoute` 否則*RouteConfig.cs* `Home` 如果您之前呼叫，則相同的 url 將會移至您控制器的預設視圖 `MapRoute` `EnableFriendlyUrls` 。

新增架構並不會加入任何範例應用程式功能。 例如，如果您在選取 MVC 範本時新增 Web Form 支援，則不會建立 *預設的 .aspx* 首頁檔。 只會新增支援架構所需的資料夾、檔案和參考。 基於這個理由，新增架構並不會變更驗證選項，這些選項是由範本所建立之範例應用程式中的程式碼所執行。 例如，如果您選取空白範本，並新增 Web Form 或 MVC 支援，則仍會停用 [ **設定驗證** ] 按鈕。

下列各節將簡短說明每個核取方塊的效果。

### <a name="add-web-forms-support"></a>新增 Web Form 支援

建立空的 *應用程式 \_ 資料* 和 *模型* 資料夾，以及 *global.asax* 檔案。 這些都是由空白範本以外的所有範本所建立，因此選取 [Web Form] 核取方塊不會與其他範本產生任何差異。

Web Form 範本預設會啟用易記 Url，但當您選取 Web Form 核取方塊的 [易記 Url] 時，不會自動啟用此功能，但會將 Web Form 支援新增至其他範本。

### <a name="add-mvc-support"></a>新增 MVC 支援

會安裝 MVC、Razor 和網頁 NuGet 套件、建立空白的*應用程式 \_ 資料*、*控制器*、*模型*和*Views*資料夾、使用*RouteConfig.cs*檔案建立*應用程式 \_ 啟動*資料夾，以及建立*global.asax*檔案。

### <a name="add-web-api-support"></a>新增 Web API 支援

安裝 NuGet 套件的 WebApi 和 Newtonsoft.Js、建立空白的*應用程式 \_ 資料*、*控制器*和*模型*資料夾、使用*WebApiConfig.cs*檔案建立*應用程式 \_ 啟動*資料夾，以及建立*global.asax*檔案。

<a id="auth"></a>
## <a name="authentication-methods"></a>驗證方法

Visual Studio 2013 針對 Web Form、MVC 和 Web API 範本提供數個驗證選項：

- [無驗證](#noauth)
- [個別使用者帳戶](#indauth) (ASP.NET Identity，先前稱為 ASP.NET 成員資格) 
-  (Windows Server Active Directory 或 Azure Active Directory 的[組織帳戶](#orgauth)) 
- [Windows 驗證](#winauth) (內部網路) 

![[設定驗證] 對話方塊](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>不需要驗證

如果您選取 [ **無驗證**]，範例應用程式將不會包含用於登入的網頁、沒有任何 UI 指出登入的使用者、成員資格資料庫沒有實體類別，以及成員資格資料庫沒有連接字串。

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>個別使用者帳戶

如果您選取 **個別的使用者帳戶**，範例應用程式將會設定為使用 ASP.NET Identity (之前稱為 ASP.NET 成員資格) 進行使用者驗證。 ASP.NET Identity 可讓使用者在網站上建立使用者名稱和密碼，或使用社交提供者（例如 Facebook、Google、Microsoft 帳戶或 Twitter）登入，以註冊帳戶。 ASP.NET Identity 中使用者設定檔的預設資料存放區是 SQL Server LocalDB 資料庫，您可以將其部署至生產網站 SQL Server 或 Azure SQL Database。

在 Visual Studio 2013 這些功能與 Visual Studio 2012 一樣，但 ASP.NET 成員資格系統的基礎程式碼已經重寫。 新程式碼基底的優點包括下列各項：

- 新的成員資格系統是以 [OWIN](http://owin.org/) 為基礎，而不是 ASP.NET Forms Authentication 模組。 這表示無論您是在 IIS 中使用 Web Form 或 MVC，或是您是自我裝載 Web API 或 SignalR，都可以使用相同的驗證機制。
- 新的成員資格資料庫是由 Entity Framework Code First 所管理，而且所有資料表都是以您可以修改的實體類別來表示。 這表示您可以輕鬆地自訂資料庫架構和與設定檔相關的 web UI，以符合您自己的需求，而且您可以使用 Code First 移轉輕鬆地部署更新。

新的成員資格系統會自動在新的範本中執行，而且可以在以 .NET 4.5 或更新版本為目標的任何專案中手動執行。

如果您要建立主要針對外部客戶的網際網路網站，ASP.NET Identity 是不錯的選擇。 如果您的組織使用 Active Directory 或 Office 365，而您想要建立可讓員工和商務夥伴進行單一登入的專案，則 [ **組織帳戶** ] 選項可能是較佳的選擇。

如需個別使用者帳戶選項的詳細資訊，請參閱下列資源：

- [www.asp.net/identity](../../../identity/index.md)。 有關 ASP.NET 網站上 ASP.NET Identity 的檔。
- [使用 Facebook 和 Google OAuth2 和 OpenID 登入來建立 ASP.NET MVC 5 應用程式](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。 另外也會顯示如何自訂使用者設定檔資料。
- [Web API-外部驗證服務](../../../web-api/overview/security/external-authentication-services.md)
- [在 Visual Studio 2013 中將外部登入新增至您的 ASP.NET 應用程式](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>組織帳戶

如果您選取 [ **組織帳戶**]，範例應用程式將會設定為使用 Windows Identity FOUNDATION (WIF) 進行驗證，以 Azure Active Directory (Azure AD 中的使用者帳戶為基礎，其中包括 Office 365) 或 Windows Server Active Directory。 如需詳細資訊，請參閱本主題稍後的「 [組織帳戶驗證」選項](#orgauthoptions) 。

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows 驗證

如果您選取 [ **Windows 驗證**]，則會將範例應用程式設定為使用 WINDOWS 驗證 IIS 模組進行驗證。 應用程式將會顯示登入 Windows 的 Active directory 或本機電腦帳戶的網域和使用者識別碼，但不會包含使用者註冊或登入 UI。 此選項適用于內部網路網站。

或者，您可以選擇 [ [組織帳戶] 下](#orgauthonprem)的 [內部部署] 選項，以建立使用 AD 驗證的內部網路網站。 內部部署選項會使用 Windows Identity Foundation (WIF) 而不是 Windows 驗證模組。 設定內部部署選項需要一些額外的步驟，但 WIF 會啟用 Windows 驗證模組無法使用的功能。 例如，透過 WIF，您可以在 Active Directory 中設定應用程式存取，並查詢目錄資料。

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>組織帳戶驗證選項

[ **設定驗證** ] 對話方塊提供數個選項，讓您 Azure Active Directory (Azure AD，包括 Office 365) 或 Windows Server ACTIVE DIRECTORY (AD) 帳戶驗證：

- [雲端單一組織](#orgauthsingle) (Azure AD，或使用與 Azure AD 的目錄整合進行 AD) 
- [雲端多組織](#orgauthmulti) (Azure AD，或使用與 Azure AD 的目錄整合進行 AD) 
- [內部部署](#orgauthonprem) (AD) 

如果您想要嘗試其中一個 Azure AD 選項但還沒有帳戶，請 [按一下這裡註冊 Azure AD 帳戶](https://go.microsoft.com/fwlink/?LinkId=309942)。

> [!NOTE]
> 如果您選擇其中一個 Azure AD 選項，您的專案就需要資料庫，而且您必須登入 Azure AD 租使用者的全域系統管理員帳戶。 輸入組織帳戶的名稱和密碼 (例如， admin@contoso.onmicrosoft.com) ，其具有 Azure AD 租使用者的系統管理許可權。
> 
> **請勿 contoso@hotmail.com 在 [登入] 對話方塊中輸入 Microsoft 帳戶 (例如) 的認證。**

<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>雲端-單一組織驗證

![單一組織驗證](creating-web-projects-in-visual-studio/_static/image24.png)

如果您想要針對一個 Azure AD [租](https://technet.microsoft.com/library/jj573650.aspx)使用者中定義的使用者帳戶啟用驗證，請選擇此選項。 例如，網站是 contoso.com 的，且會提供給 contoso.onmicrosoft.com 租使用者中 Contoso 公司的員工使用。 您將無法設定 Azure AD，以允許其他租使用者的使用者存取應用程式。

#### <a name="domain"></a>Domain

輸入您想要在其中設定應用程式的 Azure AD 網域，例如： `contoso.onmicrosoft.com` 。 如果您有 [自訂網域](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)（例如 `contoso.com` ，而不是 `contoso.onmicrosoft.com` ），可以在這裡輸入。

#### <a name="access-level"></a>存取層級

如果應用程式需要使用圖形 API 來查詢或更新目錄資訊，請選擇 [ **單一登入]、[讀取目錄資料** ] 或 [ **單一登入]、[讀取和寫入目錄資料**]。 否則，請選擇 [ **單一登入**]。 如需詳細資訊，請參閱 [應用程式存取層級](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) ，以及 [使用圖形 API 來查詢 Azure AD](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)。

#### <a name="application-id-uri"></a>應用程式識別碼 URI

根據預設，範本會將專案名稱附加至 Azure AD 網域，以為您建立應用程式識別碼 URI。 例如，如果專案名稱為 `Example` ，而且網域是 `contoso.onmicrosoft.com` ，則應用程式識別碼 URI 會成為 `https://contoso.onmicrosoft.com/Example` 。 如果您想要手動指定應用程式識別碼 URI，請展開 [ **更多選項** ] 區段，然後在文字方塊中輸入應用程式識別碼 uri。 應用程式識別碼 URI 的開頭必須是 `https://` 。

根據預設，如果已在 Azure AD 中布建的應用程式與 Visual Studio 用於專案的應用程式識別碼 URI 相同，則專案會連線至現有的應用程式，而不是布建新的應用程式。 如果您想要在該情況下布建新的應用程式，請清除 [ **覆寫應用程式專案（如果已有相同識別碼的應用程式專案** ）] 核取方塊。

如果清除 [ **覆寫** ] 核取方塊，且 Visual Studio 找到具有相同應用程式識別碼 URI 的現有應用程式，則會將數位附加至它要使用的 uri，以建立新的 uri。 例如，假設專案名稱是 `Example` ，您將文字方塊保留空白、清除 [ **覆寫** ] 核取方塊，且 Azure AD 租使用者已經有一個具有 URI 的應用程式 `https://contoso.onmicrosoft.com/Example` 。 在此情況下，將會以類似的應用程式識別碼 URI 布建新的應用程式 `https://contoso.onmicrosoft.com/Example_20130619330903` 。

#### <a name="provisioning-the-application-in-azure-ad"></a>在 Azure AD 中布建應用程式

為了在 Azure AD 中布建應用程式，或將專案連接至現有的應用程式，Visual Studio 需要網域的全域管理員認證。 當您在 [**設定驗證**] 對話方塊中按一下 **[確定**] 時，系統會提示您輸入所指定網域的全域管理員使用者名稱和密碼。 稍後，當您在 [**新增 ASP.NET 專案**] 對話方塊中按一下 [**建立專案**] 時，Visual Studio 會在 Azure AD 中布建應用程式。 請注意，在此程式中 Visual Studio 會將用戶端秘密值內嵌到 Web.config 檔案中，該檔案會在建立後一年內過期。

如需有關如何建立使用 **雲端單一組織** 驗證之應用程式的詳細資訊，請參閱下列資源：

- [Azure 驗證](../2012/windows-azure-authentication.md)
- [使用 Azure AD 將登入新增至 Web 應用程式](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [使用 Azure Active Dirctory 開發 ASP.NET 應用程式](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [使用 Azure AD 和 Microsoft OWIN 元件保護 ASP.NET Web API](https://msdn.microsoft.com/magazine/dn463788.aspx)

教學課程尚未針對 Visual Studio 2013 進行更新;在 Visual Studio 2013 中，您可以手動將某些教學課程引導您手動進行。

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>雲端-多組織驗證

![多個組織驗證](creating-web-projects-in-visual-studio/_static/image25.png)

如果您想要針對多 [個 Azure AD 租](https://technet.microsoft.com/library/jj573650.aspx)使用者中定義的使用者帳戶啟用驗證，請選擇此選項。 例如，網站是 contoso.com 的，且會提供給位於 contoso.onmicrosoft.com 租使用者的 Contoso 公司員工，以及 fabrikam.onmicrosoft.com 租使用者中 Fabrikam 公司的員工。

您輸入的設定和應用程式布建步驟類似于 [單一組織驗證](#orgauthsingle)。

如需有關如何建立使用 **雲端多組織** 驗證之應用程式的詳細資訊，請參閱下列資源：

- [使用 Azure Active Directory ASP.NET &amp; 的簡易 Web 應用程式整合](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) Active Directory Team blog 上的 Visual Studio。
- [使用 Azure AD 教學課程開發多租使用者 Web 應用程式](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) 。 本教學課程尚未針對 Visual Studio 2013 進行更新;本教學課程會引導您手動進行 Visual Studio 2013 中的部分。
- 您[必須先註冊自己的多組織 ASP.NET 應用程式，才能登入](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/)。 Vittorio Bertocci 的 Blog，說明如何解決在建立使用多組織驗證的專案時所遇到的常見問題。

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>內部部署組織驗證

![內部部署組織驗證](creating-web-projects-in-visual-studio/_static/image26.png)

如果您想要針對 Windows Server Active Directory (AD) 中定義的使用者帳戶啟用驗證，而且不想要使用 Azure AD，請選擇此選項。 您可以使用此選項來建立內部網路網站或網際網路網站。 若為網際網路網站，請使用 Active Directory 同盟服務 (ADFS) 來提供 AD 存取權。 如需詳細資訊，請參閱 [Visual Studio 2013 中的 (ADFS) 搭配 ASP.NET 使用內部部署組織驗證選項](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)。

針對內部網路網站，您可以選擇 [ [Windows 驗證](#winauth) ]，而不是此選項。 針對 [Windows 驗證] 選項，您不需要提供元資料檔案 URL。 不過，Windows 驗證並不能讓您控制 Active Directory 中的應用程式存取或查詢目錄資料。

#### <a name="on-premises-authority"></a>內部部署授權單位

輸入指向元資料檔案的 URL。 元資料檔案包含授權單位的座標。 應用程式會使用這些座標來驅動 web 登入流程。

#### <a name="application-id-uri"></a>應用程式識別碼 URI

提供可供 AD 用來識別此應用程式的唯一 URI，或保留空白讓 Visual Studio 建立一個。

<a id="nextsteps"></a>
## <a name="next-steps"></a>後續步驟

本檔提供在 Visual Studio 2013 中建立新 ASP.NET Web 專案的一些基本協助。 如需使用 for 網頁程式開發 Visual Studio 的詳細資訊，請參閱 [https://www.asp.net/visual-studio/](../../index.md) 。
