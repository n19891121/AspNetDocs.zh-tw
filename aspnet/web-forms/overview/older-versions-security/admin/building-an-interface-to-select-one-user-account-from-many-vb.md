---
uid: web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
title: 建立介面，從許多 (VB) 中選取一個使用者帳戶 |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將使用分頁的可篩選方格來建立使用者介面。 尤其是，我們的使用者介面是由一系列的 LinkButtons 所組成 .。。
ms.author: riande
ms.date: 04/01/2008
ms.assetid: da53380c-a16b-41c7-a20d-24343c735c52
msc.legacyurl: /web-forms/overview/older-versions-security/admin/building-an-interface-to-select-one-user-account-from-many-vb
msc.type: authoredcontent
ms.openlocfilehash: 625e27442c790e7a7228b8f78b8a40dbee8e3b03
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044580"
---
# <a name="building-an-interface-to-select-one-user-account-from-many-vb"></a>建置介面從許多個使用者帳戶中選取一個 (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.12.zip) 或 [下載 PDF](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial12_SelectUser_vb.pdf)

> 在本教學課程中，我們將使用分頁的可篩選方格來建立使用者介面。 尤其是，我們的使用者介面會包含一系列的 LinkButtons，以便根據使用者名稱的開始字母篩選結果，以及顯示符合使用者的 GridView 控制項。 我們會從列出 GridView 中的所有使用者帳戶開始。 然後，在步驟3中，我們將新增篩選 LinkButtons。 步驟4會查看篩選的結果分頁。 在步驟2到4中所建立的介面，將用於後續的教學課程中，以針對特定的使用者帳戶執行系統管理工作。

## <a name="introduction"></a>簡介

在 [將 <a id="_msoanchor_1"></a> [*角色指派給使用者*](../roles/assigning-roles-to-users-vb.md)] 教學課程中，我們建立了一個基本介面，讓系統管理員選取使用者並管理她的角色。 具體而言，介面會顯示系統管理員一個下拉式清單，其中包含所有使用者。 如果有數十個以上的使用者帳戶，這種介面相當適合，但對於具有數百或上千個帳戶的網站來說很難處理。 針對具有大型使用者群的網站，分頁的可篩選方格是更適合的使用者介面。

在本教學課程中，我們將建立這類使用者介面。 尤其是，我們的使用者介面會包含一系列的 LinkButtons，以便根據使用者名稱的開始字母篩選結果，以及顯示符合使用者的 GridView 控制項。 我們會從列出 GridView 中的所有使用者帳戶開始。 然後，在步驟3中，我們將新增篩選 LinkButtons。 步驟4會查看篩選的結果分頁。 在步驟2到4中所建立的介面，將用於後續的教學課程中，以針對特定的使用者帳戶執行系統管理工作。

現在就開始吧！

## <a name="step-1-adding-new-aspnet-pages"></a>步驟1：加入新的 ASP.NET 網頁

在本教學課程和接下來的兩個教學課程中，我們將探討各種系統管理相關的功能和功能。 我們將需要一系列的 ASP.NET 網頁，以實行在這些教學課程中所探討的主題。 讓我們建立這些頁面，並更新網站地圖。

首先，在名為的專案中建立新資料夾 `Administration` 。 接下來，在資料夾中加入兩個新的 ASP.NET 網頁，並將每個頁面連結至 `Site.master` 主版頁面。 為頁面命名：

- `ManageUsers.aspx`
- `UserInformation.aspx`

此外，請將兩個頁面新增至網站的根目錄： `ChangePassword.aspx` 和 `RecoverPassword.aspx` 。

這四個頁面現在應該有兩個內容控制項，每個主版頁面的 ContentPlaceHolders 都有一個： `MainContent` 和 `LoginContent` 。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample1.aspx)]

我們想要針對這些頁面顯示主版頁面的 ContentPlaceHolder 預設標記 `LoginContent` 。 因此，請移除內容控制項的宣告式標記 `Content2` 。 這麼做之後，頁面的標記應該只包含一個內容控制項。

資料夾中的 ASP.NET 網頁 `Administration` 僅供系統管理使用者之用。 我們已在 [建立和管理角色] 教學課程中，將系統管理員角色新增至系統，將這 <a id="_msoanchor_2"></a> [*Creating and Managing Roles*](../roles/creating-and-managing-roles-vb.md)兩個頁面的存取許可權制為此角色。 若要完成此動作，請將檔案新增 `Web.config` 至 `Administration` 資料夾，並設定其元素以授與系統 `<authorization>` 管理員角色中的使用者，並拒絕所有其他使用者。

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample2.xml)]

此時專案的方案總管看起來應該會類似 [圖 1] 所示的螢幕擷取畫面。

[![網站已新增四個新頁面和 Web.config 檔案](building-an-interface-to-select-one-user-account-from-many-vb/_static/image2.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image1.png)

**圖 1**：有四個新頁面和檔案已 `Web.config` 新增至網站 ([按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image3.png)) 

最後，更新網站地圖 (`Web.sitemap`) 將專案加入至 `ManageUsers.aspx` 頁面。 在我們為角色教學課程新增的之後，新增下列 XML `<siteMapNode>` 。

[!code-xml[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample3.xml)]

更新網站地圖之後，請透過瀏覽器造訪網站。 如 [圖 2] 所示，左邊的導覽現在包含管理教學課程的專案。

[![網站地圖包含標題為 [使用者管理] 的節點。](building-an-interface-to-select-one-user-account-from-many-vb/_static/image5.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image4.png)

**圖 2**：網站地圖包含標題為 [使用者管理] 的節點 ([按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image6.png)) 

## <a name="step-2-listing-all-user-accounts-in-a-gridview"></a>步驟2：列出 GridView 中的所有使用者帳戶

本教學課程的最終目標是要建立一個分頁的可篩選方格，讓系統管理員可以選取要管理的使用者帳戶。 讓我們先列出 GridView 中的 *所有* 使用者。 完成之後，我們將新增篩選和分頁介面和功能。

開啟 `ManageUsers.aspx` 資料夾中的頁面， `Administration` 並新增 GridView，稍後再將其設定 `ID` 為 `UserAccounts` ，我們將撰寫程式碼，使用 `Membership` 類別的方法將使用者帳戶集合系結至 GridView `GetAllUsers` 。 如先前的教學課程中所述，此 `GetAllUsers` 方法 `MembershipUserCollection` 會傳回物件，也就是物件的集合 `MembershipUser` 。 `MembershipUser`集合中的每一個都包含屬性 `UserName` ，如、 `Email` 、 `IsApproved` 等等。

若要在 GridView 中顯示所需的使用者帳戶資訊，請將 GridView 的屬性設定為 False，並為、和屬性加入 BoundFields，並為 `AutoGenerateColumns` `UserName` 、和屬性加入 `Email` `Comment` CheckBoxFields `IsApproved` `IsLockedOut` `IsOnline` 。 這種設定可以透過控制項的宣告式標記或透過 [欄位] 對話方塊來套用。 [圖 3] 顯示 [自動產生欄位] 核取方塊已取消選取，且已加入並設定 BoundFields 和 CheckBoxFields 之後 [欄位] 對話方塊的螢幕擷取畫面。

[![將三個 BoundFields 和三個 CheckBoxFields 新增至 GridView](building-an-interface-to-select-one-user-account-from-many-vb/_static/image8.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image7.png)

**圖 3**：將三個 BoundFields 和三個 CheckBoxFields 新增至 GridView ([按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image9.png)) 

設定 GridView 之後，請確定其宣告式標記如下所示：

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample4.aspx)]

接下來，我們需要撰寫程式碼，將使用者帳戶系結至 GridView。 建立名為的方法 `BindUserAccounts` 以執行這項工作，然後從 `Page_Load` 第一頁上的事件處理常式呼叫它。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample5.vb)]

花點時間透過瀏覽器測試頁面。 如 [圖 4] 所示， `UserAccounts` GridView 會列出系統中所有使用者的使用者名稱、電子郵件地址和其他相關的帳戶資訊。

[![使用者帳戶會列在 GridView 中](building-an-interface-to-select-one-user-account-from-many-vb/_static/image11.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image10.png)

**圖 4**：使用者帳戶會列在 GridView ([按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image12.png)) 

## <a name="step-3-filtering-the-results-by-the-first-letter-of-the-username"></a>步驟3：依使用者名稱的第一個字母篩選結果

目前 `UserAccounts` GridView 會顯示 *所有* 的使用者帳戶。 對於具有數百或數千個使用者帳戶的網站，使用者必須能夠快速地向下削減顯示的帳戶。 將篩選 LinkButtons 新增至頁面即可完成這項作業。 讓我們在頁面中新增 27 LinkButtons：一個標題為 [全部]，另一個則是字母的 LinkButton。 如果造訪者按一下 [全部] LinkButton，GridView 將會顯示所有使用者。 如果他們按一下特定信件，則只會顯示使用者名稱開頭為所選字母的使用者。

我們的第一個工作是新增27個 LinkButton 控制項。 其中一個選項是以宣告方式建立 27 LinkButtons，一次一個。 更有彈性的方法是搭配使用中繼器控制項 `ItemTemplate` 和來呈現 LinkButton，然後再將篩選選項系結至中繼器做為 `String` 陣列。

首先，將中繼器控制項新增至 GridView 上方的頁面 `UserAccounts` 。 設定中繼器的 `ID` 屬性以設定 `FilteringUI` 中繼器的範本，使其 `ItemTemplate` 呈現 LinkButton `Text` ，其和屬性會系結 `CommandName` 至目前的陣列元素。 如我們在將 <a id="_msoanchor_3"></a> [*角色指派給使用者*](../roles/assigning-roles-to-users-vb.md)教學課程中所見，您可以使用資料系結語法來完成這項作業 `Container.DataItem` 。 使用中繼器 `SeparatorTemplate` 來顯示每個連結之間的垂直線。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample6.aspx)]

若要使用所需的篩選選項來填入此中繼器，請建立名為的方法 `BindFilteringUI` 。 請務必從 `Page_Load` 第一個頁面載入上的事件處理常式呼叫這個方法。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample7.vb)]

這個方法 `String` 會針對陣列中的每個元素將篩選選項指定為數組中的元素 `filterOptions` ，而中繼器會轉譯 LinkButton， `Text` 並將其 `CommandName` 屬性指派給陣列元素的值。

[圖 5] 顯示 `ManageUsers.aspx` 透過瀏覽器觀看的頁面。

[![中繼器會列出27個篩選 LinkButtons](building-an-interface-to-select-one-user-account-from-many-vb/_static/image14.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image13.png)

**圖 5**：中繼器列出27個篩選 LinkButtons ([按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image15.png)) 

> [!NOTE]
> 使用者名稱的開頭可能是任何字元，包括數位和標點符號。 為了查看這些帳戶，系統管理員必須使用 All LinkButton 選項。 或者，您也可以新增 LinkButton，以傳回以數位開頭的所有使用者帳戶。 我將此視為讀者的練習。

按一下任何篩選 LinkButtons 會導致回傳並引發中繼器 `ItemCommand` 事件，但是方格中沒有任何變更，因為我們尚未撰寫任何程式碼來篩選結果。 `Membership`類別包含的[ `FindUsersByName` 方法](https://technet.microsoft.com/library/system.web.security.membership.findusersbyname.aspx)會傳回使用者名稱符合指定搜尋模式的使用者帳戶。 我們可以使用這個方法來取得使用者帳戶，而這些使用者帳戶的使用者名稱是以已按下的篩選 LinkButton 所指定的字母為開頭 `CommandName` 。

首先 `ManageUser.aspx` ，更新頁面的程式碼後端類別，使它包含名為這個屬性的屬性， `UsernameToMatch` 在回傳之間保存使用者名稱篩選字串：

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample8.vb)]

`UsernameToMatch`屬性會儲存其值，並 `ViewState` 使用索引鍵 ' UsernameToMatch ' 將其指派至集合。 當讀取此屬性的值時，它會檢查值是否存在於 `ViewState` 集合中; 如果不是，則會傳回預設值，也就是空字串。 `UsernameToMatch`屬性會表現出一個常見的模式，也就是保存值以查看狀態，以便在回傳之間保存屬性的任何變更。 如需此模式的詳細資訊，請參閱 [瞭解 ASP.NET View State](https://msdn.microsoftn-us/library/ms972976.aspx)。

接下來，更新 `BindUserAccounts` 方法，如此一來，它就會呼叫，而不是呼叫，而是 `Membership.GetAllUsers` `Membership.FindUsersByName` 傳遞 `UsernameToMatch` 以 SQL 萬用字元（%）附加的屬性值。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample9.vb)]

若只要顯示使用者名稱以字母 A 開頭的使用者，請將 `UsernameToMatch` 屬性設定為，然後呼叫 `BindUserAccounts` 這會導致呼叫，這會傳回使用者 `Membership.FindUsersByName("A%")` 名稱開頭為的所有使用者。同樣地，若要傳回 *所有* 的使用者，請將空字串指派給屬性，如此一來，方法就會叫用，藉此傳回 `UsernameToMatch` 所有的 `BindUserAccounts` `Membership.FindUsersByName("%")` 使用者帳戶。

建立中繼器事件的事件處理常式 `ItemCommand` 。 每當按一下其中一個篩選準則 LinkButtons 時，就會引發此事件。它會透過物件傳遞已按一下的 LinkButton `CommandName` 值 `RepeaterCommandEventArgs` 。 我們必須將適當的值指派給 `UsernameToMatch` 屬性，然後呼叫 `BindUserAccounts` 方法。 如果 `CommandName` 是 all，請將空字串指派給， `UsernameToMatch` 以便顯示所有的使用者帳戶。 否則，請將 `CommandName` 值指派給 `UsernameToMatch`

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample10.vb)]

使用此程式碼時，請測試篩選功能。 第一次造訪網頁時，會顯示所有使用者帳戶 (請參閱 [圖 5]) 。 按一下 LinkButton 會導致回傳並篩選結果，只顯示以 A 開頭的使用者帳戶。

[![使用篩選 LinkButtons 來顯示使用者名稱以特定信件開頭的使用者](building-an-interface-to-select-one-user-account-from-many-vb/_static/image17.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image16.png)

**圖 6**：使用篩選 LinkButtons 來顯示使用者名稱以特定字母開頭的使用者 ([按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image18.png)) 

## <a name="step-4-updating-the-gridview-to-use-paging"></a>步驟4：更新 GridView 以使用分頁

[圖 5] 和 [6] 所示的 GridView 會列出方法所傳回的所有記錄 `FindUsersByName` 。 如果有數百或數千個使用者帳戶，這可能會在查看所有帳戶時導致資訊多載 (例如，按一下 [全部 LinkButton] 或一開始造訪頁面) 時。 為了協助將使用者帳戶呈現在更容易管理的區塊中，讓我們設定 GridView 一次顯示10個使用者帳戶。

GridView 控制項提供兩種類型的分頁：

- **預設分頁** -容易執行，但效率不佳。 總而言之，在預設分頁的情況下，GridView 預期其資料來源的 *所有* 記錄。 然後，它只會顯示適當的記錄頁面。
- **自訂分頁** -需要更多工作，但比預設分頁更有效率，因為使用自訂分頁，資料來源只會傳回要顯示的一組精確記錄。

預設和自訂分頁之間的效能差異，在分頁至數千筆記錄時可能相當龐大。 由於我們正在建立此介面（假設可能有數百個或數千個使用者帳戶），因此讓我們使用自訂分頁。

> [!NOTE]
> 如需有關預設和自訂分頁之間差異的更詳盡討論，以及執行自訂分頁時所牽涉到的挑戰，請參閱 [有效率地逐頁流覽大量資料](https://asp.net/learn/data-access/tutorial-25-vb.aspx)。 如需預設和自訂分頁之間效能差異的部分分析，請參閱 [ASP.NET 中的自訂分頁，SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)。

若要執行自訂分頁，我們首先需要一些機制來取得 GridView 所顯示的精確記錄子集。 好消息是， `Membership` 類別的方法有多載可 `FindUsersByName` 讓我們指定頁面索引和頁面大小，而且只會傳回落在該記錄範圍內的使用者帳戶。

特別是，這個多載具有下列簽章： [`FindUsersByName(usernameToMatch, pageIndex, pageSize, totalRecords)`](https://msdn.microsoft.com/library/fa5st8b2.aspx) 。

*PageIndex*參數會指定要傳回的使用者帳戶頁面;*pageSize*表示每頁顯示的記錄數目。 *TotalRecords*參數是傳回 `ByRef` 使用者存放區中使用者帳戶總數的參數。

> [!NOTE]
> 傳回的資料 `FindUsersByName` 是依使用者名稱排序，不能自訂排序準則。

GridView 可以設定為利用自訂分頁，但只能在系結至 ObjectDataSource 控制項時使用。 若要讓 ObjectDataSource 控制項執行自訂分頁，則需要兩個方法：一個是傳遞開始資料列索引和要顯示的記錄數目上限，並傳回落在該範圍內的精確記錄子集;以及傳回已分頁的記錄總數的方法。 多載會 `FindUsersByName` 接受頁面索引和頁面大小，並透過參數傳回記錄的總數 `ByRef` 。 這裡有介面不相符的情況。

其中一個選項是建立 proxy 類別，以公開 ObjectDataSource 預期的介面，然後在內部呼叫 `FindUsersByName` 方法。 另一個選項，也就是我們將在本文中使用的選項，就是建立自己的分頁介面，並使用它來取代 GridView 的內建分頁介面。

### <a name="creating-a-first-previous-next-last-paging-interface"></a>建立第一個、上一個、最後一個、最後一個分頁介面

讓我們使用 First、Previous、Next 和 Last LinkButtons 來建立分頁介面。 第一個 LinkButton 在按下時，會將使用者帶到第一頁的資料，而上一頁會讓他回到上一頁。 同樣地，下一個和最後一個會將使用者分別移至下一頁和最後一頁。 在 GridView 底下加入四個 LinkButton 控制項 `UserAccounts` 。

[!code-aspx[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample11.aspx)]

接下來，為每個 LinkButton 的事件建立事件處理常式 `Click` 。

[圖 7] 顯示透過 Visual Web Developer 設計檢視觀看的四個 LinkButtons。

[![在 GridView 下新增 First、Previous、Next 和 Last LinkButtons](building-an-interface-to-select-one-user-account-from-many-vb/_static/image20.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image19.png)

**圖 7**：在 GridView 下新增 First、Previous、Next 和 Last LinkButtons ([按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image21.png)) 

### <a name="keeping-track-of-the-current-page-index"></a>追蹤目前的頁面索引

當使用者第一次造訪 `ManageUsers.aspx` 頁面或按一下其中一個篩選按鈕時，我們想要在 GridView 中顯示第一頁的資料。 不過，當使用者按一下其中一個導覽 LinkButtons 時，我們需要更新頁面索引。 若要維護頁面索引和每頁顯示的記錄數目，請將下列兩個屬性新增至頁面的程式碼後端類別：

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample12.vb)]

如同 `UsernameToMatch` 屬性，屬性會 `PageIndex` 保存其值以查看狀態。 唯讀屬性會傳回 `PageSize` 硬式編碼的值10。 我邀請有興趣的讀者更新此屬性，以使用與相同的模式 `PageIndex` ，然後再擴大 `ManageUsers.aspx` 頁面，讓造訪頁面的人可以指定要顯示每頁的使用者帳戶數目。

### <a name="retrieving-just-the-current-pages-records-updating-the-page-index-and-enabling-and-disabling-the-paging-interface-linkbuttons"></a>只取出目前頁面的記錄、更新頁面索引，以及啟用和停用分頁介面 LinkButtons

使用分頁介面並 `PageIndex` `PageSize` 加入和屬性之後，我們就可以開始更新 `BindUserAccounts` 方法，讓它使用適當的多載 `FindUsersByName` 。 此外，我們還需要根據所顯示的頁面，啟用或停用分頁介面。 當您看到第一頁的資料時，應該停用第一個和先前的連結;在觀看最後一頁時，應該停用 [下一步] 和 [最後一個]

以下列程式碼更新 `BindUserAccounts` 方法：

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample13.vb)]

請注意，透過方法的最後一個參數，會決定要進行分頁的記錄總數 `FindUsersByName` 。 傳回指定的使用者帳戶頁面之後，系統會根據資料的第一頁或最後一頁，啟用或停用四個 LinkButtons。

最後一個步驟是撰寫四個 LinkButtons 的 `Click` 事件處理常式程式碼。 這些事件處理常式需要更新 `PageIndex` 屬性，然後透過呼叫 `BindUserAccounts` 第一個、先前的和下一個事件處理常式來將資料重新系結至 GridView，非常簡單。 `Click`不過，最後一個 LinkButton 的事件處理常式有點複雜，因為我們需要決定要顯示多少筆記錄來判斷最後一個頁面索引。

[!code-vb[Main](building-an-interface-to-select-one-user-account-from-many-vb/samples/sample14.vb)]

圖8和9顯示自訂分頁介面的作用。 [圖 8] 顯示每 `ManageUsers.aspx` 個使用者帳戶的第一頁數據時的頁面。 請注意，只會顯示13個帳戶中的10個。 按一下 [下一步] 或 [上一步] 連結會導致回傳、將更新 `PageIndex` 為1，然後將使用者帳戶的第二頁系結至方格 (請參閱 [圖 9]) 。

[![系統會顯示前10個使用者帳戶](building-an-interface-to-select-one-user-account-from-many-vb/_static/image23.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image22.png)

**圖 8**：顯示前10個使用者帳戶 ([按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image24.png)) 

[![按一下下一個連結會顯示使用者帳戶的第二頁](building-an-interface-to-select-one-user-account-from-many-vb/_static/image26.png)](building-an-interface-to-select-one-user-account-from-many-vb/_static/image25.png)

**圖 9**：按一下 [下一步] 連結會顯示使用者帳戶的第二頁 ([按一下以查看完整大小的影像](building-an-interface-to-select-one-user-account-from-many-vb/_static/image27.png)) 

## <a name="summary"></a>摘要

系統管理員通常需要從帳戶清單中選取使用者。 在先前的教學課程中，我們探討了如何使用以使用者填入的下拉式清單，但這種方法無法妥善調整。 在本教學課程中，我們探討了更好的替代方案：其結果會顯示在分頁式 GridView 中的可篩選介面。 透過此使用者介面，系統管理員可以快速且有效率地尋找並選取數千個使用者帳戶。

快樂程式設計！

### <a name="further-reading"></a>深入閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [ASP.NET 中的自訂分頁與 SQL Server 2005](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx)
- [有效率地分頁大量資料](https://asp.net/learn/data-access/tutorial-25-vb.aspx)
- [推出您自己的網站管理工具](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>關於作者

Scott Mitchell 作者有多個 ASP/ASP. NET 書籍和創辦人 of 4GuysFromRolla.com，自1998起一直都在使用 Microsoft Web 技術。 Scott 以獨立顧問、訓練員和作者的形式運作。 他的最新書籍是 *[在24小時內 ASP.NET 2.0](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*。 Scott 可于或透過他的 blog 來觸達 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) [http://ScottOnWriting.NET](http://scottonwriting.net/) 。

### <a name="special-thanks-to"></a>特別感謝

本教學課程系列是由許多有用的審核者所審核。 本教學課程的潛在客戶審核 Alicja Maziarz。 有興趣複習我即將推出的 MSDN 文章嗎？ 如果是的話，請在下列位置放置一行

> [!div class="step-by-step"]
> [上一個](unlocking-and-approving-user-accounts-cs.md) 
> [下一步](recovering-and-changing-passwords-vb.md)
