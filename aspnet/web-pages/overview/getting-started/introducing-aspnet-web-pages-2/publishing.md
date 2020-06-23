---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: 簡介 ASP.NET Web Pages 使用 WebMatrix 發佈網站 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程是教學課程集中的最後一篇介紹 ASP.NET Web Pages 和 Microsoft WebMatrix 的文章。 它會討論如何發佈您的網站 t .。。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: a09339a833ea0b4a2d3c3a9323cce777577ea048
ms.sourcegitcommit: 0cf7d06071a8ff986e6c028ac9daf0c0e7490412
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85240590"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a>簡介 ASP.NET Web Pages 使用 WebMatrix 發佈網站

 作者：[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程是教學課程集中的最後一篇介紹 ASP.NET Web Pages 和 Microsoft WebMatrix 的文章。 它會討論如何將您的網站發佈至網際網路，讓其他人可以使用它。 它假設您已完成[建立 ASP.NET Web Pages 網站一致外觀](https://go.microsoft.com/fwlink/?LinkId=251585)的系列。
> 
> 您將瞭解如何使用發佈您的網站：
> 
> - Microsoft Azure
> - Web 主控公司

## <a name="about-publishing-your-site"></a>關於發佈您的網站

到目前為止，您已在本機電腦上完成所有工作，包括測試您的頁面。 若要執行您的<em>cshtml</em>頁面，您已使用內建于 WebMatrix 的 web 伺服器，也就是 IIS Express。 但當然，沒有人可以看到您所建立的網站。 若要讓其他人可以使用您的網站，您必須將它發佈到網際網路。

除非您已經有公用 web 伺服器的存取權，否則發佈表示您必須擁有具有*雲端平臺*或*主機服務提供者*的帳戶。 雲端平臺（例如 Microsoft Azure）會為您的應用程式提供隨選基礎結構。 主機服務提供者是擁有可公開存取之網頁伺服器的公司，可出租您網站的空間。 針對高容量的商業網站，主控方案會從數個月（或甚至免費）到每個月數百美元的小型網站執行。

> [!NOTE]
> 您可以透過網際網路服務提供者（ISP）存取公用 web 伺服器，以供家裡取得網際網路服務。 不過，您的主控提供者必須支援 ASP.NET Web Pages。 許多 Isp 都不這麼做，但還是值得一次檢查。

在本教學課程中，我們將概述如何發佈。 提供所有專案的確切詳細資料並不實用，因為每個主機服務提供者的進程會有所不同。 但是，您將能瞭解此程式的運作方式。

本教學課程包含四個區段：

1. [設定預設頁面](#defaultpage)
2. 發行（選擇下列其中一項）  
 a. [將您的網站發佈至 Microsoft Azure](#azure)  
 b. [將您的網站發佈至虛擬主機公司](#host)
3. [更新即時網站：重新發佈](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a>設定預設頁面

當使用者流覽至您網站的基底位址時，會向使用者顯示網站的預設頁面。 例如，當*Default.htm*設定為網站的預設頁面時 `www.contoso.com` ，流覽至與 `www.contoso.com` 流覽至相同 `www.contoso.com/Default.htm` 。

目前，您的網站會使用**預設的. cshtml**做為預設頁面。 此頁面適用于您的預設頁面，但在本教學課程中，您尚未將任何內容新增至該頁面，因此會顯示空白頁面。 開啟 Default. cshtml，並以下列程式碼取代內容。

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

現在您的網站已準備好發行。 首先，您將瞭解如何將網站部署至 Azure，以及如何將其部署至虛擬主機公司。 其中一個選項適用于您的網站，而您只需要遵循其中一個部署選項。

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a>將您的網站發佈至 Microsoft Azure

本教學課程會先示範如何將您的網站部署至 Microsoft Azure。 藉由使用 Microsoft 帳戶登入，您可以在 Azure 上建立多達10個免費網站。 這些免費網站提供便利的方式來測試您的網站。 您稍後可以隨時刪除此範例網站，以避免使用您所有的免費網站。 只需要幾分鐘的時間，您就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/dotnet/)。

在 [WebMatrix] 功能區中，按一下 [**發佈**] 按鈕。

![WebMatrix 功能區中的 [發佈] 按鈕](publishing/_static/image1.png)

[**發佈您的網站**] 對話方塊隨即顯示。 如果您尚未登入您的 Microsoft 帳戶，對話方塊會包含**開始使用 Azure**連結。 按一下此連結。

![發佈您的網站](publishing/_static/image2.png)

如果您尚未登入 Microsoft 帳戶，系統會再次提供您登入的機會。 您必須登入 Microsoft 帳戶，才能在 Azure 上發佈您的網站。

![Sign In](publishing/_static/image3.png)

登入您的 Microsoft 帳戶之後，對話方塊中會包含在 Azure 上建立新網站或連線至 Azure 上的其中一個現有網站的連結。

![建立新網站](publishing/_static/image4.png)

選取 [**建立新網站**]。

如果您將專案命名為**WebPagesMovies**，您網站的預設名稱將會是**webpagesmovies.azurewebsites.net**。 此預設名稱很可能無法使用，如紅色驚嘆號所示。

![預設的網站名稱](publishing/_static/image5.png)

將網站名稱變更為可用的專案，然後選取靠近您的位置的位置。

![變更的網站名稱](publishing/_static/image6.png)

按一下 [確定]。

WebMatrix 會 performss 測試以判斷伺服器是否與您的網站相容。

![相容性測試](publishing/_static/image7.png)

選取 [繼續]。

即會顯示相容性測試的結果。

![相容性結果](publishing/_static/image8.png)

選取 [繼續]。

WebMatrix 會顯示要發佈至網站的檔案和資料庫。 由於這是您第一次發佈網站，因此會列出所有檔案。 您可以取消選取尚未準備好要發行的檔案。 在後續的發行集中，只會顯示已變更的檔案。 請參閱[更新即時網站：重新發佈](#update)。

![publish preview](publishing/_static/image9.png)

選取 [繼續]。

網站部署至 Azure 之後，會顯示一則訊息，指出部署已完成。

![publish complete](publishing/_static/image10.png)

您的網站和資料庫已發佈至 Azure，且現已開放給公眾使用。 按一下指出發行已完成的訊息中的連結，您現在會看到已部署的網站。 您或具有網際網路存取權的任何人都可以新增或修改資料庫中的記錄。

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a>將您的網站發佈至虛擬主機公司

如果您決定不要發佈至 Azure，您可以改為將您的網站發佈至虛擬主機公司。

按一下 [**尋找 web 裝載**] 連結。

![[發行設定] 對話方塊中的 [尋找 web 裝載] 按鈕](publishing/_static/image12.png)

您會前往 Microsoft 網站上的頁面，其中列出支援 ASP.NET 的主控提供者。

![列出主控提供者的 Microsoft 網站頁面](publishing/_static/image13.png)

很明顯地，現在可能很難以得知您長期所需要的裝載功能。 以下是幾個要考慮的事項：

- 基於 WebPagesMovies 網站的目的，您不需要有個別的 SQL Server 附加元件，這通常會產生額外的成本。 在您的網站中，您使用的是獨立的 SQL Server Compact Edition。 不過，您可能需要 SQL Server 存取權，才能進行某些未來的網站工作。 如果您認為可能的話，請確定您可以在稍後新增 SQL Server 功能。
- 檢查主控提供者是否支援 Web Deploy 發佈通訊協定。 您可以使用 FTP 通訊協定來發行，但使用 Web Deploy 會比較方便。

有些網站提供免費的試用期限。 當您仍在試驗 WebMatrix 和 ASP.NET Web Pages 時，免費試用是嘗試發佈和裝載的好方法。

挑選您想要的一個。 在本教學課程中，我們選取了 [DiscountASP.NET]，因為我們在建立教學課程時，該公司已有促銷活動，可讓人們免費裝載網站數個月。

> [!NOTE]
> 我們在本教學課程中選擇的主機服務提供者，不應被視為該公司對其他人的背書。 但我們必須挑選一個來說明，而 DiscountASP.NET 是支援 ASP.NET Web Pages 的眾多公司，以及用於發佈的 Web Deploy 通訊協定之一。

一般而言，在您註冊主控提供者之後，公司會傳送電子郵件給您，其中包含使用者名稱和密碼、網頁伺服器的 URL 等等。 如果主控公司支援 Web Deploy 通訊協定，他們可能會將包含發佈設定的檔案傳送給您，或讓您下載一個檔案。 發行設定檔案可簡化您的程式。

當您已註冊並準備好發佈時，請按一下 [WebMatrix] 功能區中的 [**發佈**] 按鈕。 [**發行設定**] 對話方塊隨即顯示。

如果主機服務提供者將發佈設定檔案傳送給您，請按一下 [匯**入發行設定**] 連結並匯入檔案。 如果您沒有發佈設定檔案，請使用主控公司在電子郵件中傳送給您的值來填入欄位。 當您完成時，[**發行設定**] 對話方塊看起來可能會像這樣：

![在 [發行設定] 對話方塊中填入的發行設定](publishing/_static/image14.png)

按一下 [**驗證連接**]。 如果一切都沒問題，對話方塊會報告 [已**成功連線**]，這表示它可以與主控提供者的伺服器通訊。

![如果發行設定正確，則為成功訊息](publishing/_static/image15.png)

如果發生問題，WebMatrix 會盡力告訴您問題的原因：

![如果發行設定發生問題，則會出現錯誤訊息](publishing/_static/image16.png)

按一下 [Save] **** 儲存您的設定。 WebMatrix 提供來執行測試，以確保它可以與主控網站正確通訊：

![用來執行發佈程式測試的訊息供應專案](publishing/_static/image17.png)

按一下 [是] 。 WebMatrix 將一些範例檔案上傳到主控提供者。 當相容性測試完成時，WebMatrix 會報告結果：

![發佈測試的結果](publishing/_static/image18.png)

如果您已經準備好開始進行，請繼續進行，然後按一下 [**繼續**] 來啟動實際的發佈程式。 WebMatrix 會找出您的網站中已有哪些檔案，而且已經在主機伺服器上（現在就是無），並提供您發佈程式的預覽：

![預覽發佈程式將要上傳的檔案](publishing/_static/image19.png)

要發佈的檔案清單包含您建立的網頁，如 [*電影*]。 此清單也包含您已安裝之協助程式的檔案、要針對您的資料庫 SQL Server Compact 版本執行的檔案等等。 因此，初始發佈程式可能很可觀。

按一下 **[繼續]** 。 WebMatrix 會將您的檔案複製到主控提供者的伺服器。 完成時，會在狀態列中報告結果：

![當發行程式成功完成時的狀態列訊息](publishing/_static/image20.png)

若要查看您的即時網站，請按一下狀態列中的連結。 將*電影*新增至 URL，您會看到您所建立的*電影. cshtml*檔案：

![顯示 [電影] 頁面的即時網站](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a>更新即時網站：重新發佈

一旦您發佈網站（至 Azure 或虛擬主機公司）之後，您的電腦上會有兩個版本， &mdash; 以及服務提供者上的版本。 您可能會想要繼續開發網站（如果沒有其他，則是下一個教學課程集的一部分）。 當您這麼做時，必須重新發佈網站，才能將變更從電腦複製到服務提供者。 WebMatrix 中的發佈程式可判斷您的網站上有哪些檔案已變更，並只發行那些檔案。

若要查看重新發行的運作方式，請開啟 [*電影*] 網站，進行一些小變更，然後儲存檔案。 例如，將標題變更為 `Movies - Updated` 。

按一下功能區中的 [**發佈**] 按鈕。 WebMatrix 會決定已變更的內容，並顯示其將發佈之檔案的預覽。

![[發行] 對話方塊顯示已變更的檔案準備好重新發行](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> 根據預設，WebMatrix 只會在您第一次發行網站時發行您的資料庫（*.sdf*檔案）。 一旦您的網站發佈，而人們與網站互動之後，即時網站上的資料庫通常會有網站的實際資料。 您必須小心不要使用電腦上的 *.sdf*檔案來覆寫即時資料庫，這通常只包含測試資料。 這就是為什麼您會看到警告**發佈會覆寫任何遠端資料庫**，以及為什麼預設會清除*WebPagesMovies*的核取方塊。

按一下 **[繼續]** 。 WebMatrix 會發佈變更的檔案，並顯示成功的訊息，就像您第一次發佈一樣。

前往即時網站（如果仍顯示，您可以按一下成功訊息中的連結），並確認您的變更已發佈。

> [!TIP] 
> 
> **從遠端編輯檔案**
> 
> 除了變更您的網站再重新發行以外，您也可以直接在 WebMatrix 中編輯遠端檔案。 在此案例中，您會開啟服務提供者上的檔案，而 WebMatrix 會下載該檔案的複本供您編輯。 每次您儲存檔案時，WebMatrix 都會將變更傳送至網站。
> 
> 遠端編輯是對您的即時網站進行變更的簡單方式。 不過，您以這種方式進行的變更不會與本機網站中的檔案同步處理。 若要將本機檔案與遠端網站同步處理，您可以下載遠端檔案。 此程式的運作方式非常類似發行，但相反。
> 
> 我們不會在這裡詳細說明 WebMatrix 的遠端編輯和遠端下載功能。 如果多人必須在不同電腦上的相同網站上工作，它們就很有用。 如需詳細資訊，請參閱[使用 WebMatrix 2 Beta 發佈和編輯遠端網站](https://go.microsoft.com/fwlink/?LinkId=251591)。

## <a name="additional-resources"></a>其他資源

- [ASP.NET WebMatrix ASP.NET Web Pages 論壇](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages)，這是張貼問題和獲得解答的絕佳地方。

> [!div class="step-by-step"]
> [上一步](layouts.md)
