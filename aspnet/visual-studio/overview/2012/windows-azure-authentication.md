---
uid: visual-studio/overview/2012/windows-azure-authentication
title: Windows Azure 驗證 |Microsoft Docs
author: Rick-Anderson
description: 適用于 Windows Azure Active Directory 的 Microsoft ASP.NET 工具可讓您輕鬆地針對 Windows Azure 網站上託管的 web 應用程式啟用驗證 .。。
ms.author: riande
ms.date: 02/20/2013
ms.assetid: a3cef801-a54b-4ebd-93c3-55764e2e14b1
msc.legacyurl: /visual-studio/overview/2012/windows-azure-authentication
msc.type: authoredcontent
ms.openlocfilehash: ab75218cbe3817c14a064e9816388aebc7e431f7
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240562"
---
# <a name="windows-azure-authentication"></a>Windows Azure 驗證

依[Rick Anderson](https://twitter.com/RickAndMSFT)

> 適用于 Windows Azure Active Directory 的 Microsoft ASP.NET 工具可讓您輕鬆地針對[Windows Azure 網站](https://www.windowsazure.com/home/features/web-sites/)上託管的 web 應用程式啟用驗證。 您可以使用 Windows Azure 驗證，向您的組織驗證 Office 365 使用者、從內部部署 Active Directory 同步處理的公司帳戶，或在您自己的自訂 Windows Azure Active Directory 網域中建立的使用者。 啟用 Windows Azure 驗證會將您的應用程式設定為使用單一[Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)租使用者來驗證使用者。
>
> 雲端服務中的 web 角色不支援 ASP.NET Windows Azure 驗證工具，但我們計畫在未來的版本中執行此操作。 Windows Azure web 角色支援[Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) （WIF）。
>
> 如需如何設定內部部署 Active Directory 與 Windows Azure Active Directory 租使用者之間同步處理的詳細資訊，請參閱[使用 AD FS 2.0 來執行和管理單一登入](https://technet.microsoft.com/library/jj205462.aspx)。
>
> Windows Azure Active Directory 目前以[免費預覽服務](https://azure.microsoft.com/free/dotnet/)的形式提供。

## <a name="requirements"></a>需求：

- Visual Studio 2012 或[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)
- 適用于 Visual Studio Express 2012 的 Visual Studio 2012 或[Web 工具擴充](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)功能的[web 工具擴充](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409)功能
- [適用于 windows Azure Active Directory 的 Microsoft ASP.NET 工具– Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306)或適用[于 Windows 的 Microsoft ASP.NET 工具 Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a>建立具有 Visual Studio 2012 的 ASP.NET Web 應用程式

您可以使用 Visual Studio 2012 建立任何 Web 應用程式，本教學課程會使用 ASP.NET MVC 內部網路範本。

1. 建立新的 ASP.NET MVC 4 內部網路應用程式，並接受所有預設值。 （它必須是**tra** net 中的，而不是 **&** net 專案中的）。
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a>啟用 Windows Azure 驗證（當您是原則的全域管理員時）

如果您沒有現有的 Windows Azure Active Directory 租使用者（例如，透過現有的 Office 365 帳戶），您可以註冊[新的 windows Azure Active Directory 帳戶](https://g.microsoftonline.com/0AX00en/5)來建立新的租使用者。

1. 從 [專案] 功能表中，選取 [**啟用 Windows Azure 驗證**]：

   ![](windows-azure-authentication/_static/image2.png)

2. 輸入 Windows Azure Active Directory 租使用者的網域（例如 contoso.onmicrosoft.com），然後按一下 [**啟用**]：

![](windows-azure-authentication/_static/image3.png)

3. 在 [Web 驗證] 對話方塊中，以您的 Windows Azure Active Directory 租使用者的系統管理員身分登入：

   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a>以非系統管理員的原則啟用 Window Azure

如果您沒有 Windows Azure Active Directory 租使用者的全域管理員許可權，您可以取消核取布建應用程式的核取方塊。

![](windows-azure-authentication/_static/image6.png)

對話方塊會顯示使用 Azure Active Directory 的原則布建應用程式時所需的 [**網域**]、[**應用程式主體識別碼**] 和 [**回復 URL** ]。 您必須將此資訊提供給具有足夠許可權的使用者來布建應用程式。 如需如何使用 Cmdlet 來手動建立服務主體的詳細資訊，請參閱[如何搭配 Windows Azure Active Directory ASP.NET 應用程式執行單一登入](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)。
成功布建應用程式之後，您可以按一下 **[繼續]，以選取的設定來更新 web.config**。 如果您想要在等候布建發生時繼續開發應用程式，您可以按一下 **[關閉]，以記住 [專案檔] 中的設定**。 下次您叫用 [啟用 Windows Azure 驗證] 並取消核取 [布建] 核取方塊時，您會看到相同的設定，而且您可以按一下 [**繼續**]，然後按一下 [**在 web.config中套用這些設定**。

1. 請等候您的應用程式設定為使用 windows Azure 驗證，並以 Windows Azure Active Directory 進行布建。
2. 啟用應用程式的 Windows Azure 驗證之後，請按一下 [**關閉]：**

    ![](windows-azure-authentication/_static/image7.png)
3. 按 F5 鍵執行您的應用程式。 您應該會自動重新導向至登入頁面。 使用目錄的 [原則] [使用者認證] 來登入應用程式。

    ![](windows-azure-authentication/_static/image1.jpg)
4. 因為您的應用程式目前使用自我簽署的測試憑證，所以您會收到來自瀏覽器的警告，指出憑證不是由受信任的憑證授權單位單位所發行。

    您可以按一下 [**繼續流覽此網站**]，安全地在本機開發期間忽略此警告：

    ![](windows-azure-authentication/_static/image8.png)
5. 您現在已使用 Windows Azure 驗證成功登入您的應用程式！

    ![](windows-azure-authentication/_static/image2.jpg)

啟用 Windows Azure 驗證會對您的應用程式進行下列變更：

- 已將反跨網站偽造要求（[CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))）類別（*應用程式 \_ Start\AntiXsrfConfig.cs* ）新增至您的專案。
- NuGet 套件 `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` 會新增至您的專案。
- 您應用程式中的 windows Identity Foundation 設定會設定為接受來自您 Windows Azure Active Directory 租使用者的安全性權杖。 按一下下方影像，以查看對*Web.config*檔案所做變更的展開。

     ![](windows-azure-authentication/_static/image9.png)
- 將會布建您的 Windows Azure Active Directory 租使用者中應用程式的服務主體。
- 已啟用 HTTPS。

## <a name="deploy-the-application-to-windows-azure"></a>將應用程式部署至 Windows Azure

如需完整指示，請參閱將[ASP.NET Web 應用程式部署至 Windows Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)網站。

若要將使用 Windows Azure 驗證的應用程式發行至 Azure 網站：

1. 以滑鼠右鍵按一下您的應用程式，然後選取 [**發佈]：**

    ![](windows-azure-authentication/_static/image3.jpg)
2. 從 [發行 Web] 對話方塊下載並匯入 Azure 網站的發行設定檔。

    ![](windows-azure-authentication/_static/image4.jpg)
3. [**連接**] 索引標籤會顯示**目的地 URL** （應用程式的公開 url）。 按一下 [**驗證**連線] 以測試您的連接：

    ![](windows-azure-authentication/_static/image5.jpg)
4. 如果您先前已發佈到這個 Azure 網站，請考慮勾選 [**移除目的地的其他**檔案] 設定，以確保您的應用程式能完全發行。 請注意，已選取 [**啟用 Windows Azure 驗證**] 核取方塊。

    ![](windows-azure-authentication/_static/image10.png)
5. 選擇性：在 [**預覽**] 索引標籤上，按一下 [**開始預覽**] 以查看已部署的檔案。

    ![](windows-azure-authentication/_static/image6.jpg)
6. 按一下 [**發佈]。**

    系統會提示您啟用目標主機的 Windows Azure 驗證。 按一下 [**啟用**] 以繼續：

    ![](windows-azure-authentication/_static/image11.png)
7. 輸入您的 Windows Azure Active Directory 租使用者的系統管理員認證：

    ![](windows-azure-authentication/_static/image7.jpg)
8. 成功發行應用程式之後，瀏覽器就會開啟發行的網站。

    > [!NOTE]
    > 在啟用目標主機的 Windows Azure 驗證之後，您的應用程式最多可能需要五分鐘（通常不會減少），才能完全布建 Windows Azure Active Directory。 當您第一次執行應用程式時，如果收到錯誤 ACS50001：找不到名稱為 ' [領域] ' 的信賴憑證者，請稍候幾分鐘，然後再次嘗試執行應用程式。
9. 出現提示時，以使用者身分登入您的目錄：

    ![](windows-azure-authentication/_static/image8.jpg)
10. 您現在已使用 Windows Azure 驗證成功登入您的 Azure 託管應用程式。

     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a>已知問題

#### <a name="role-based-authorization-fails-when-using-windows-azure-authentication"></a>使用 Windows Azure 驗證時以角色為基礎的授權失敗

Windows Azure 驗證目前未提供必要的角色宣告，因此可以執行以角色為基礎的授權。 已驗證使用者的角色必須以手動方式從 Windows Azure Active Directory 中取出。

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-sts"></a>流覽至具有 Windows Azure 驗證的應用程式會導致錯誤「ACS20016 登入使用者的網域（live.com）不符合此 STS 的任何允許網域」

如果您已經登入 Microsoft 帳戶（例如 hotmail.com、live.com、outlook.com），而您嘗試存取已啟用 Windows Azure 驗證的應用程式，您可能會收到400錯誤回應，因為 Windows Azure Active Directory 無法辨識 Microsoft 帳戶的網域。 若要登入應用程式，請先從您的 Microsoft 帳戶登出。

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificate"></a>登入已啟用 Windows Azure 驗證的應用程式，而非 [無] 的 X509certificatevalidationmode.custom 會導致 accounts.accesscontrol.windows.net 憑證的憑證驗證錯誤

憑證驗證不是必要的，應保持停用。 此簽發者憑證的指紋會由 WSFederationAuthenticationModule 驗證。

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-sts"></a>嘗試啟用 Windows Azure 驗證時，[Web 驗證] 對話方塊會顯示錯誤「ACS20016：登入使用者（contoso.onmicrosoft.com）的網域不符合此 STS 的任何允許網域」。

當您先前使用不同的 Windows Azure Active Directory 帳戶從相同的 Visual Studio 程式內成功登入時，可能會看到此錯誤。 從指定的帳號登出，或 Visual Studio 重新開機。 如果您先前已登入並選取 [讓我保持登入] 選項，您可能需要清除瀏覽器 cookie。

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message"></a>ACS20012：要求不是有效的 WS-同盟通訊協定訊息

如果您已經使用一些其他 Microsoft 識別碼登入其中一個 Azure 服務，就可能發生這種情況。 使用私用瀏覽器視窗（例如在 IE 中的 InPrivate 或 Chrome 中的 Incognito），或清除所有 cookie。

## <a name="additional-resources"></a>其他資源

- [適用于 Windows Azure Active Directory 的 Microsoft ASP.NET 工具– Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci
- [Windows Azure 功能：身分識別](https://docs.microsoft.com/azure/active-directory/)
- [TechNet： Windows Azure Active Directory](https://technet.microsoft.com/library/hh967619.aspx)
- [Windows Azure Active Directory：為您的組織開發應用程式](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [Windows Azure Active Directory：為多個組織開發應用程式](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [如何使用 Windows Azure Active Directory 執行單一登入](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- [使用 Windows Azure Active Directory 的單一登入：深入探討](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx)– Vittorio Bertocci
- [使用 AD FS 2.0 來執行和管理單一登入](https://technet.microsoft.com/library/jj205462.aspx)
