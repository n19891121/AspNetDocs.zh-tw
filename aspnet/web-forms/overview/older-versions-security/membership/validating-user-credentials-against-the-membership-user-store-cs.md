---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
title: '針對成員資格使用者存放區驗證使用者認證 (c # ) |Microsoft Docs'
author: rick-anderson
description: 在本教學課程中，我們將探討如何使用程式設計方式和登入控制項，針對成員資格使用者存放區驗證使用者的認證 .。。
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 61aa4e08-aa81-4aeb-8ebe-19ba7a65e04c
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-cs
msc.type: authoredcontent
ms.openlocfilehash: fd50f4e63c75cf77eb21629d0c11a859da6b357d
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045230"
---
# <a name="validating-user-credentials-against-the-membership-user-store-c"></a>針對成員資格使用者存放區驗證使用者認證 (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_CS.zip) 或 [下載 PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_cs.pdf)

> 在本教學課程中，我們將探討如何使用程式設計方式和登入控制項，針對成員資格使用者存放區驗證使用者的認證。 我們也將探討如何自訂登入控制項的外觀和行為。

## <a name="introduction"></a>簡介

在 <a id="Tutorial05"></a> [上述教學](creating-user-accounts-cs.md)課程中，我們探討了如何在成員資格架構中建立新的使用者帳戶。 我們先來看看如何透過類別的方法以程式設計方式建立使用者帳戶 `Membership` `CreateUser` ，然後使用 CreateUserWizard Web 控制項進行檢查。 不過，登入頁面目前會根據使用者名稱和密碼組的硬式編碼清單來驗證提供的認證。 我們需要更新登入頁面的邏輯，讓它針對成員架構的使用者存放區驗證認證。

如同建立使用者帳戶，認證可以用程式設計方式或宣告方式進行驗證。 成員資格 API 包含以程式設計方式向使用者存放區驗證使用者認證的方法。 和 ASP.NET 隨附登入 Web 控制項，它會呈現使用者介面，其中包含使用者名稱和密碼的文字方塊，以及用來登入的按鈕。

在本教學課程中，我們將探討如何使用程式設計方式和登入控制項，針對成員資格使用者存放區驗證使用者的認證。 我們也將探討如何自訂登入控制項的外觀和行為。 現在就開始吧！

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>步驟1：針對成員資格使用者存放區驗證認證

針對使用表單驗證的網站，使用者可以造訪登入頁面並輸入其認證，以登入網站。 然後，這些認證會與使用者存放區進行比較。 如果有效，則會將使用者授與表單驗證票證，這是一個安全性權杖，指出訪客的身分識別和真實性。

若要針對成員資格架構驗證使用者，請使用 `Membership` 類別的[ `ValidateUser` 方法](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)。 `ValidateUser`方法會接受兩個輸入參數， *`username`* 並傳回 *`password`* 布林值，指出認證是否有效。 如同 `CreateUser` 我們在上一個教學課程中所探討的方法，此方法會將 `ValidateUser` 實際的驗證委派給已設定的成員資格提供者。

會透過 `SqlMembershipProvider` 預存程式取得指定使用者的密碼，以驗證提供的認證 `aspnet_Membership_GetPasswordWithFormat` 。 回想一下，您會 `SqlMembershipProvider` 使用下列三種格式的其中一種來儲存使用者的密碼：清除、加密或雜湊。 `aspnet_Membership_GetPasswordWithFormat`預存程式會以其原始格式傳回密碼。 針對加密或雜湊的密碼， `SqlMembershipProvider` *`password`* 會將傳遞至方法的值轉換 `ValidateUser` 為其相等的加密或雜湊狀態，然後與資料庫傳回的值進行比較。 如果儲存在資料庫中的密碼符合使用者輸入的格式化密碼，則認證有效。

讓我們將登入頁面更新 (~/ `Login.aspx`) ，讓它針對成員資格架構使用者存放區驗證提供的認證。 我們已在表單驗證教學課程的總覽中建立了此登入頁面 <a id="Tutorial02"></a> [*An Overview of Forms Authentication*](../introduction/an-overview-of-forms-authentication-cs.md) ，為使用者名稱和密碼建立具有兩個文字方塊的介面、記住我的核取方塊，以及登入按鈕 (請參閱 [圖 1]) 。 程式碼會根據使用者名稱和密碼組的硬式編碼清單來驗證輸入的認證 (Scott/密碼、Jisun/密碼和 Sam/密碼) 。 在 <a id="Tutorial03"></a> [*表單驗證設定和高級主題*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md)教學課程中，我們更新了登入頁面的程式碼，以在表單驗證票證的屬性中儲存其他資訊 `UserData` 。

[![登入頁面的介面包含兩個文字方塊： CheckBoxList 和按鈕](validating-user-credentials-against-the-membership-user-store-cs/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image1.png)

**圖 1**：登入頁面的介面包含兩個文字方塊： CheckBoxList，以及按鈕 ([按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image3.png)) 

登入頁面的使用者介面可以保持不變，但我們需要以 `Click` 驗證使用者的程式碼取代登入按鈕的事件處理常式和成員資格架構使用者存放區。 更新事件處理常式，使其程式碼出現，如下所示：

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample1.cs)]

這段程式碼很簡單。 我們一開始會先呼叫 `Membership.ValidateUser` 方法，傳遞提供的使用者名稱和密碼。 如果該方法傳回 true，則會透過 `FormsAuthentication` 類別的 RedirectFromLoginPage 方法，將使用者登入網站。 如我們在表單驗證教學課程中所討論的 (<a id="Tutorial2"></a> [*An Overview of Forms Authentication*](../introduction/an-overview-of-forms-authentication-cs.md) ，會 `FormsAuthentication.RedirectFromLoginPage` 建立表單驗證票證，然後將使用者重新導向至適當的頁面 ) 。若認證無效，則 `InvalidCredentialsMessage` 會顯示標籤，通知使用者其使用者名稱或密碼不正確。

就是這麼簡單！

若要測試登入頁面是否如預期般運作，請嘗試使用您在上一個教學課程中建立的其中一個使用者帳戶登入。 或者，如果您還沒有建立帳戶，請繼續進行，並從頁面建立一個帳戶 `~/Membership/CreatingUserAccounts.aspx` 。

> [!NOTE]
> 當使用者輸入自己的認證並提交登入頁面表單時，會以 *純文字*將認證（包括她的密碼）以網際網路傳送至 web 伺服器。 這表示任何駭客都能探查網路流量，以查看使用者名稱和密碼。 為了避免這種情況，您必須使用 [安全通訊端層 (SSL) ](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)來加密網路流量。 這可確保認證 (以及整個頁面的 HTML 標籤) 都會從離開瀏覽器一直加密，直到網頁伺服器收到這些認證為止。

### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>成員資格架構如何處理不正確登入嘗試

當造訪者抵達登入頁面並提交認證時，他們的瀏覽器會向登入頁面提出 HTTP 要求。 如果認證有效，HTTP 回應會在 cookie 中包含驗證票證。 因此，嘗試侵入您的網站的駭客可以建立一個程式，以有效的使用者名稱和猜測密碼的方式，將 HTTP 要求徹底傳送至登入頁面。 如果密碼猜測正確，登入頁面將會傳回驗證票證 cookie，此時程式知道它已偶然發現有效的使用者名稱/密碼組。 在暴力密碼破解的情況下，這類程式也許可以遇到使用者的密碼，特別是當密碼是弱的密碼時。

為了避免這類暴力密碼破解攻擊，如果在一段時間內有特定數目的失敗登入嘗試，則成員資格架構會鎖定使用者。 確切的參數可透過下列兩個成員資格提供者設定設定來設定：

- `maxInvalidPasswordAttempts` -指定在帳戶遭到鎖定之前，允許使用者在一段時間內允許的無效密碼嘗試次數。預設值為5。
- `passwordAttemptWindow` -指出指定的無效登入嘗試次數會導致帳戶遭到鎖定的時間週期（以分鐘為單位）。預設值為10。

如果使用者已被鎖定，她將無法登入，直到系統管理員解除鎖定其帳戶為止。 當使用者被鎖定時， `ValidateUser` 方法 *一律* 會傳回 `false` ，即使有提供有效的認證。 雖然此行為可減少駭客透過暴力密碼破解方法侵入您的網站的可能性，但最終可能會鎖定只是忘記密碼的有效使用者，或是不小心出現 CAPS LOCK 或有錯誤的輸入日。

可惜的是，沒有任何內建工具可解除鎖定使用者帳戶。 為了將帳戶解除鎖定，您可以直接修改資料庫-變更 `IsLockedOut` `aspnet_Membership` 資料表中適當使用者帳戶的欄位，或是建立 web 介面，以列出已鎖定的帳戶，以及解除鎖定的選項。 在後續的教學課程中，我們將探討如何建立管理介面，以完成一般使用者帳戶和角色相關工作。

> [!NOTE]
> 方法的其中一個缺點 `ValidateUser` 是，當提供的認證無效時，它不會提供任何說明原因。 認證可能無效，因為使用者存放區中沒有相符的使用者名稱/密碼組，或是使用者尚未核准，或使用者已遭到鎖定。在步驟4中，我們將瞭解如何在使用者的登入嘗試失敗時，向使用者顯示更詳細的訊息。

## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>步驟2：透過登入 Web 控制項收集認證

[登入 Web 控制項](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)所呈現的預設使用者介面，與我們在 <a id="SKM5"></a> [*表單驗*](../introduction/an-overview-of-forms-authentication-cs.md)證教學課程的總覽中建立的使用者介面非常類似。 使用 Login 控制項可以節省建立介面的工作，以收集訪客的認證。 此外，登入控制項會自動登入使用者 (假設提交的認證有效) ，藉此讓我們不必撰寫任何程式碼。

讓我們更新 `Login.aspx` ，並以登入控制項取代手動建立的介面和程式碼。 從移除中現有的標記和程式碼開始 `Login.aspx` 。 您可以直接將其刪除，或直接將其批註。若要將宣告式標記標記為批註，請使用和分隔符號將它括住 `<%--` `--%>` 。 您可以手動輸入這些分隔符號，或如 [圖 2] 所示，您可以選取要加上批註的文字，然後按一下工具列中的 [將選取的線條標記為批註] 圖示。 同樣地，您可以使用批註化選取的行圖示，在程式碼後端類別中將選取的程式碼標記為批註。

[![批註登入 .aspx 中現有的宣告式標記和原始程式碼](validating-user-credentials-against-the-membership-user-store-cs/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image4.png)

**圖 2**：在 `Login.aspx` ([按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image6.png) ，以將現有的宣告式標記和原始程式碼批註) 

> [!NOTE]
> 當您在 Visual Studio 2005 中查看宣告式標記時，無法使用批註選取的行圖示。 如果您不是使用 Visual Studio 2008，將需要手動新增 `<%--` 和 `--%>` 分隔符號。

接下來，將登入控制項從 [工具箱] 拖曳至頁面，並將其 `ID` 屬性設定為 `myLogin` 。 此時您的畫面看起來應該類似 [圖 3]。 請注意，登入控制項的預設介面包含 [使用者名稱] 和 [密碼] 的 TextBox 控制項、[下次記住我的時間] 核取方塊和 [登入] 按鈕。 另外還有 `RequiredFieldValidator` 兩個文字方塊的控制項。

[![將登入控制項新增至頁面](validating-user-credentials-against-the-membership-user-store-cs/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image7.png)

**圖 3**：將登入控制項新增至頁面 ([按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image9.png)) 

我們已經完成了！ 按一下 [登入] 控制項的 [登入] 按鈕時，將會發生回傳，而 Login 控制項將會呼叫 `Membership.ValidateUser` 方法，並傳入輸入的使用者名稱和密碼。 如果認證無效，登入控制項會顯示指出這類訊息的訊息。 但是，如果認證有效，則登入控制項會建立表單驗證票證，並將使用者重新導向至適當的頁面。

登入控制項會使用四個因素來決定適當的頁面，以便在成功登入時將使用者重新導向至：

- 登入控制項是否在登入頁面上，如 `loginUrl` 表單驗證設定中的設定所定義; 此設定的預設值為 `Login.aspx`
- `ReturnUrl`查詢字串參數是否存在
- 登入控制項的[ `DestinationUrl` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx)值
- `defaultUrl`在表單驗證設定設定中指定的值; 此設定的預設值為`Default.aspx`

[圖 4] 說明登入控制項如何使用這四個參數，以達成適當的頁面決策。

[![將登入控制項新增至頁面](validating-user-credentials-against-the-membership-user-store-cs/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image10.png)

**圖 4**：將登入控制項新增至頁面 ([按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image12.png)) 

請花點時間測試登入控制項，方法是透過瀏覽器造訪網站，並以成員資格架構中的現有使用者身分登入。

登入控制項的轉譯介面可高度設定。 有許多屬性會影響其外觀;然後，您可以將 Login 控制項轉換成範本，以精確控制使用者介面專案的版面配置。 此步驟的其餘部分會探討如何自訂外觀和版面配置。

### <a name="customizing-the-login-controls-appearance"></a>自訂登入控制項的外觀

登入控制項的預設屬性設定會轉譯使用者介面，其標題為使用者名稱和密碼輸入的標題 ( 登入 ) 、TextBox 和 Label 控制項、[下次記住我的時間] 核取方塊和 [登入] 按鈕。 這些元素的外觀全都可透過 Login 控制項的許多屬性來設定。 此外，您可以藉由設定一或兩個屬性，來新增其他使用者介面專案（例如頁面的連結以建立新的使用者帳戶）。

讓我們花幾分鐘的時間來 gussy 登入控制項的外觀。 因為 `Login.aspx` 頁面上已有文字位於顯示登入的頁面頂端，所以登入控制項的標題是多餘的。 因此，請清除[ `TitleText` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx)值，以便移除登入控制項的標題。

您可以 [`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx) 分別透過和[ `PasswordLabelText` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)，自訂兩個 TextBox 控制項左邊的使用者名稱：和密碼：標籤。 讓我們將使用者名稱： Label 變更為 read Username：。 標籤和 TextBox 樣式可 [`LabelStyle`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx) 分別透過和[ `TextBoxStyle` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx)來設定。

您可以透過登入控制項來設定 [記住我 next time] 核取方塊的 [Text] 屬性 [`RememberMeText property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx) ，而且其預設的 checked 狀態可透過 [`RememberMeSet property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx) 預設為 False) 的 (設定。 請繼續進行，並將 `RememberMeSet` 屬性設定為 True，如此一來，預設會核取 [記住我下一次] 核取方塊。

Login 控制項提供兩個屬性來調整其使用者介面控制項的版面配置。 [`TextLayout property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx)指出使用者名稱：和密碼：標籤是否出現在其對應文字方塊的左邊 (預設) 或上方。 [`Orientation property`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx)表示使用者名稱和密碼輸入是否以垂直方式放在另一個) 或水準的 (。 我要將這兩個屬性設定為預設值，但建議您嘗試將這兩個屬性設定為非預設值，以查看產生的效果。

> [!NOTE]
> 在下一節中，設定登入控制項的版面配置，我們將探討如何使用樣板來定義版面配置控制項使用者介面專案的精確版面配置。

藉由將 [`CreateUserText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx) 和[ `CreateUserUrl` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx)設定為 [尚未註冊]，來總結登入控制項的屬性設定？ 建立帳戶！ 和 `~/Membership/CreatingUserAccounts.aspx` 。 這會將超連結新增至登入控制項的介面，該介面指向我們在 <a id="SKM6"></a> [上一個教學](creating-user-accounts-cs.md)課程中建立的頁面。 登入控制項的 [`HelpPageText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx) 和[ `HelpPageUrl` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx)（property）和屬性 [`PasswordRecoveryText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx) （property）和屬性（property）和和[ `PasswordRecoveryUrl` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx)（property）會以相同的方式運作、轉譯說明頁面的連結和

在進行這些屬性變更之後，您的登入控制項的宣告式標記和外觀看起來應該類似 [圖 5] 所示。

[![登入控制項的屬性值會指示其外觀](validating-user-credentials-against-the-membership-user-store-cs/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image13.png)

**圖 5**：登入控制項的屬性值會指出其外觀 ([按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image15.png)) 

### <a name="configuring-the-login-controls-layout"></a>設定登入控制項的版面配置

登入 Web 控制項的預設使用者介面會將介面配置在 HTML 中 `<table>` 。 但是，如果我們需要更細微地控制轉譯的輸出呢？ 或許我們想要 `<table>` 使用一連串的標記來取代 `<div>` 。 如果我們的應用程式需要其他認證來進行驗證，該怎麼辦？ 比方說，許多財務網站都需要使用者提供使用者名稱和密碼，但也不能 (PIN) 或其他身分識別資訊。 無論原因為何，都可以將登入控制項轉換成範本，以便明確定義介面的宣告式標記。

我們需要執行兩項作業，才能更新登入控制項以收集其他認證：

1. 更新登入控制項的介面，以包含 Web 控制項 (s) 來收集其他認證。
2. 覆寫登入控制項的內部驗證邏輯，如此一來，只有在使用者的使用者名稱和密碼有效，且其他認證也有效時，才會驗證使用者。

若要完成第一項工作，我們必須將登入控制項轉換成範本，並新增必要的 Web 控制項。 就第二個工作而言，可以藉由建立控制項[ `Authenticate` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)的事件處理常式來取代登入控制項的驗證邏輯。

讓我們更新 Login 控制項，讓它提示使用者輸入其使用者名稱、密碼和電子郵件地址，而且只有在提供的電子郵件地址符合檔案的電子郵件地址時，才會驗證使用者。 我們必須先將登入控制項的介面轉換為範本。 從登入控制項的智慧標籤，選擇 [轉換成範本] 選項。

[![將登入控制項轉換成範本](validating-user-credentials-against-the-membership-user-store-cs/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image16.png)

**圖 6**：將登入控制項轉換成範本 ([按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image18.png)) 

> [!NOTE]
> 若要將登入控制項還原為其預先範本版本，請按一下控制項智慧標籤中的 [重設] 連結。

將登入控制項轉換成範本，會將加入 `LayoutTemplate` 至控制項的宣告式標記，並以 HTML 元素和 Web 控制項定義使用者介面。 如 [圖 7] 所示，將控制項轉換為範本會從屬性視窗移除許多屬性，例如 `TitleText` 、 `CreateUserUrl` 等等，因為使用範本時，會忽略這些屬性值。

[![當登入控制項轉換成範本時，可以使用較少的屬性](validating-user-credentials-against-the-membership-user-store-cs/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image19.png)

**圖 7**：當登入控制項轉換成範本時可使用的屬性較少 ([按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image21.png)) 

您 `LayoutTemplate` 可以視需要修改中的 HTML 標籤。 同樣地，您也可以在範本中加入任何新的 Web 控制項。 不過，登入控制項的核心 Web 控制項必須保留在範本中，並保留其指派 `ID` 值。 尤其是，請勿移除或重新命名 `UserName` 或 `Password` 文字方塊、 `RememberMe` 核取方塊、 `LoginButton` 按鈕、 `FailureText` 標籤或 `RequiredFieldValidator` 控制項。

若要收集訪客的電子郵件地址，我們需要在範本中新增 TextBox。 在資料表資料列 () 中加入下列宣告式標記 `<tr>` ，其中包含 `Password` 文字方塊，以及保留 [下次記住我的時間] 核取方塊的資料表列：

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample2.aspx)]

新增 TextBox 之後 `Email` ，請流覽瀏覽器中的頁面。 如 [圖 8] 所示，登入控制項的使用者介面現在包含第三個文字方塊。

[![登入控制項現在包含使用者電子郵件地址的文字方塊](validating-user-credentials-against-the-membership-user-store-cs/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image22.png)

**圖 8**： Login 控制項現在包含使用者電子郵件地址的文字方塊 ([按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image24.png)) 

此時，登入控制項仍在使用 `Membership.ValidateUser` 方法來驗證提供的認證。 同樣地，在文字方塊中輸入的值與 `Email` 使用者是否可以登入無關。 在步驟3中，我們將探討如何覆寫登入控制項的驗證邏輯，讓認證只有在使用者名稱和密碼有效，且提供的電子郵件地址符合檔案的電子郵件地址時才會被視為有效。

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>步驟3：修改登入控制項的驗證邏輯

當訪客提供自己的認證，並按一下 [登入] 按鈕時，回傳接踵而來和登入控制項會進行其驗證工作流程。 工作流程一開始會引發[ `LoggingIn` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx)。 任何與這個事件相關聯的事件處理常式，都可以藉由將 `e.Cancel` 屬性設定為，來取消登入作業 `true` 。

如果未取消登入作業，工作流程會藉由引發[ `Authenticate` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)來進行。 如果事件有事件處理常式，則 `Authenticate` 負責判斷所提供的認證是否有效。 如果未指定任何事件處理常式，登入控制項會使用 `Membership.ValidateUser` 方法來判斷認證的有效性。

如果提供的認證有效，則會建立表單驗證票證、引發[ `LoggedIn` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx)，然後將使用者重新導向至適當的頁面。 但是，如果認證被視為無效，則會引發[ `LoginError` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx)，並顯示一則訊息，通知使用者其認證無效。 根據預設，登入控制項會在失敗時，只 `FailureText` 會將其 Label 控制項的 Text 屬性設定為失敗訊息 ( 您的登入嘗試失敗。 請 ) 再試一次。 但是，如果登入控制項的[ `FailureAction` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx)設定為 `RedirectToLoginPage` ，則登入控制項會在 `Response.Redirect` 附加 querystring 參數的登入頁面上發出， `loginfailure=1` (這會導致登入控制項顯示失敗訊息) 。

圖9提供驗證工作流程的流程圖。

[![登入控制項的驗證工作流程](validating-user-credentials-against-the-membership-user-store-cs/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image25.png)

**圖 9**：登入控制項的驗證工作流程 ([按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image27.png)) 

> [!NOTE]
> 如果您想要使用的 `FailureAction` `RedirectToLogin` 頁面選項，請考慮下列案例。 現在我們的 `Site.master` 主版頁面，在匿名使用者流覽時，左邊的資料行中會顯示文字、Hello、stranger，但是假設我們想要使用登入控制項來取代該文字。 這可讓匿名使用者從網站上的任何頁面登入，而不需要直接造訪登入頁面。 不過，如果使用者無法透過主版頁面所呈現的登入控制項來登入，則將它們重新導向至登入頁面 (`Login.aspx`) ，因為該頁面可能包含其他指示、連結和其他說明（例如，建立新帳戶或抓取遺失密碼的連結），但未新增至主版頁面。

### <a name="creating-theauthenticateevent-handler"></a>建立 `Authenticate` 事件處理常式

為了插入我們的自訂驗證邏輯，我們必須為登入控制項的事件建立事件處理常式 `Authenticate` 。 建立事件的事件處理常式 `Authenticate` 將會產生下列事件處理常式定義：

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample3.cs)]

如您所見， `Authenticate` 事件處理常式會傳遞類型的物件 [`AuthenticateEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx) 做為它的第二個輸入參數。 `AuthenticateEventArgs`類別包含一個名為的布林值屬性 `Authenticated` ，用來指定所提供的認證是否有效。 接著，我們的工作是在這裡撰寫程式碼，以判斷提供的認證是否有效，以及是否據以設定 `e.Authenticate` 屬性。

### <a name="determining-and-validating-the-supplied-credentials"></a>判斷及驗證提供的認證

使用登入控制項的 [`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx) 和[ `Password` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx)來判斷使用者輸入的使用者名稱和密碼認證。 若要判斷輸入至任何其他 Web 控制項的值 (例如 `Email` 我們在上一個步驟中加入的文字方塊) ，請使用 *`LoginControlID`* `.FindControl` ( " *`controlID`* " ) ，在屬性等於的範本中取得 Web 控制項的程式設計參考 `ID` *`controlID`* 。 例如，若要取得 TextBox 的參考 `Email` ，請使用下列程式碼：

`TextBox EmailTextBox = myLogin.FindControl("Email") as TextBox;`

為了驗證使用者的認證，我們需要執行兩項作業：

1. 確定提供的使用者名稱和密碼有效
2. 確定輸入的電子郵件地址符合檔案的電子郵件地址，以供使用者嘗試登入

若要完成第一項檢查，我們可以直接使用 `Membership.ValidateUser` 方法，就像我們在步驟1中看到的一樣。 針對第二次檢查，我們需要判斷使用者的電子郵件地址，以便將其與輸入 TextBox 控制項中的電子郵件地址進行比較。 若要取得特定使用者的相關資訊，請使用 `Membership` 類別的[ `GetUser` 方法](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)。

`GetUser`方法有數個多載。 如果使用時未傳入任何參數，則會傳回目前登入使用者的相關資訊。 若要取得特定使用者的相關資訊，請呼叫 `GetUser` 傳入其使用者名稱。 無論何種方式，都會傳回 `GetUser` [ `MembershipUser` 物件](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)，其具有 `UserName` 、 `Email` 、 `IsApproved` 、 `IsOnline` 等屬性。

下列程式碼會執行這兩個檢查。 如果兩者都通過，則 `e.Authenticate` 會將設定為 `true` ，否則會被指派 `false` 。

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample4.cs)]

使用此程式碼時，請嘗試以有效使用者的身份登入，並輸入正確的使用者名稱、密碼和電子郵件地址。 再試一次，但這次特意使用不正確的電子郵件地址 (請參閱 [圖 10]) 。 最後，使用不存在的使用者名稱第三次嘗試。 在第一種情況下，您應該成功登入網站，但在最後兩個案例中，您應該會看到登入控制項的認證訊息無效。

[![提供不正確的電子郵件地址時，Tito 無法登入](validating-user-credentials-against-the-membership-user-store-cs/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image28.png)

**圖 10**：提供不正確的電子郵件地址時，Tito 無法登入 ([按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image30.png)) 

> [!NOTE]
> 如同在步驟1中，成員架構如何處理不正確登入嘗試一節中所述，當 `Membership.ValidateUser` 呼叫方法並傳遞了不正確認證時，它會追蹤不正確登入嘗試，並在指定的時間範圍內超過特定的無效嘗試臨界值時鎖定使用者。 由於我們的自訂驗證邏輯 `ValidateUser` 會呼叫方法，有效使用者名稱的錯誤密碼會遞增不正確登入嘗試計數器，但在使用者名稱和密碼有效的情況下，此計數器不會遞增，但電子郵件地址不正確。 這可能是因為駭客不太可能知道使用者名稱和密碼，但必須使用暴力密碼破解技術來判斷使用者的電子郵件地址，這種行為很適合。

## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>步驟4：改善登入控制項的無效認證訊息

當使用者嘗試使用不正確認證登入時，登入控制項會顯示一則訊息，說明登入嘗試失敗。 尤其是，控制項會顯示其[ `FailureText` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx)所指定的訊息，其預設值為登入嘗試失敗。 請再試一次。

回想一下，使用者的認證可能不正確原因有很多：

- 使用者名稱可能不存在
- 使用者名稱存在，但密碼無效
- 使用者名稱和密碼有效，但使用者尚未核准
- 使用者名稱和密碼是有效的，但因為使用者已超過指定時間範圍內不正確登入嘗試次數，所以使用者會被鎖定 (很有可能的情況) 

使用自訂驗證邏輯時，可能有其他原因。 例如，使用我們在步驟3中撰寫的程式碼，使用者名稱和密碼可能是有效的，但是電子郵件地址可能不正確。

無論認證為何無效，登入控制項會顯示相同的錯誤訊息。 如果使用者的帳戶尚未經過核准或被鎖定，可能會對此缺乏意見反應造成混淆。不過，只要一點工作，就可以讓 Login 控制項顯示更適當的訊息。

當使用者嘗試以不正確認證登入時，登入控制項會引發其 `LoginError` 事件。 請繼續並建立此事件的事件處理常式，並加入下列程式碼：

[!code-csharp[Main](validating-user-credentials-against-the-membership-user-store-cs/samples/sample5.cs)]

上述程式碼一開始會將登入控制項的 `FailureText` 屬性設定為預設值， ( 您的登入嘗試失敗。 請 ) 再試一次。 然後，它會檢查提供的使用者名稱是否對應至現有的使用者帳戶。 如果是的話，它會查閱產生的 `MembershipUser` 物件 `IsLockedOut` 和 `IsApproved` 屬性，以判斷帳戶是否已被鎖定或尚未核准。 在任一種情況下， `FailureText` 屬性會更新為對應的值。

若要測試此程式碼，特意嘗試以現有使用者的身份登入，但使用錯誤的密碼。 請在10分鐘的時間範圍內的資料列中執行這五次，此帳戶就會被鎖定。如 [圖 11] 所示，後續的登入嘗試一律會失敗 (即使使用正確的密碼) ，但現在會顯示更具描述性的帳戶因為不正確登入嘗試次數而遭到鎖定。 請洽詢系統管理員，以將您的帳戶解除鎖定訊息。

[![Tito 執行了太多不正確登入嘗試，且已被鎖定](validating-user-credentials-against-the-membership-user-store-cs/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-cs/_static/image31.png)

**圖 11**： Tito 執行了太多不正確登入嘗試，且已被鎖定 ([按一下以查看完整大小的影像](validating-user-credentials-against-the-membership-user-store-cs/_static/image33.png)) 

## <a name="summary"></a>摘要

在本教學課程之前，我們的登入頁面會針對使用者名稱/密碼組的硬式編碼清單，驗證提供的認證。 在本教學課程中，我們已更新頁面，以針對成員資格架構驗證認證。 在步驟1中，我們探討了如何以程式設計 `Membership.ValidateUser` 方式使用方法。 在步驟2中，我們以登入控制項取代了手動建立的使用者介面和程式碼。

登入控制項會轉譯標準登入使用者介面，並自動根據成員資格架構來驗證使用者的認證。 此外，如果是有效的認證，登入控制項會透過表單驗證將使用者登入。 簡單地說，只要將 Login 控制項拖曳到頁面上，就不需要額外的宣告式標記或程式碼，即可享有功能完整的登入使用者體驗。 更多，登入控制項可高度自訂，可讓您更精確地控制轉譯的使用者介面和驗證邏輯。

到目前為止，我們的網站訪客可以建立新的使用者帳戶並登入網站，但我們還沒看到根據已驗證的使用者來限制對頁面的存取。 目前，任何使用者（已驗證或匿名）都可以在我們的網站上查看任何頁面。 除了控制以使用者為基礎的網站網頁存取之外，我們也可能會有某些網頁的功能相依于該使用者。 下一個教學課程會探討如何根據已登入的使用者來限制存取和頁面內的功能。

快樂程式設計！

### <a name="further-reading"></a>深入閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [將自訂訊息顯示為鎖定和未核准的使用者](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [檢查 ASP.NET 2.0 的成員資格、角色和設定檔](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [如何：建立 ASP.NET 登入頁面](https://msdn.microsoft.com/library/ms178331.aspx)
- [登入控制技術檔](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [使用 Login 控制項](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>關於作者

Scott Mitchell 作者有多個 ASP/ASP. NET 書籍和創辦人 of 4GuysFromRolla.com，自1998起一直都在使用 Microsoft Web 技術。 Scott 以獨立顧問、訓練員和作者的形式運作。 他的最新書籍是 *[在24小時內 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 Scott 可于或透過他的 blog 來觸達 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) [http://ScottOnWriting.NET](http://scottonwriting.net/) 。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列是由許多有用的審核者所審核。 本教學課程的潛在客戶審核者 Teresa Murphy 和 Michael Olivero。 有興趣複習我即將推出的 MSDN 文章嗎？ 如果是的話，請在這裡放置一行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com) 。

> [!div class="step-by-step"]
> [上一個](creating-user-accounts-cs.md) 
> [下一步](user-based-authorization-cs.md)
