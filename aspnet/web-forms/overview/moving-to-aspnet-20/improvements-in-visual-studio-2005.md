---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: 視覺工作室改進 2005 |微軟文件
author: rick-anderson
description: Visual Studio 2005 為 Web 應用程式開發人員提供了 Web 專案改進和增強的一長串。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: e98771614bf4e0095f8ff596e7cdb26c8c9de1ad
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542972"
---
# <a name="improvements-in-visual-studio-2005"></a>Visual Studio 2005 中的改善

由[微軟](https://github.com/microsoft)

> Visual Studio 2005 為 Web 應用程式開發人員提供了 Web 專案改進和增強的一長串。

Visual Studio 2005 為 Web 應用程式開發人員提供了 Web 專案改進和增強的一長串。 與 Visual Studio .NET 2002 和 2003 一樣強大,但處理 Web 專案的方式也有很多投訴。 Visual Studio 2005 增加了大量新功能,以解決這些投訴。 對於那些喜歡 Visual Studio .NET 2003 處理 Web 應用程式編譯的方式的使用者,請參閱[Web 應用程式專案](https://go.microsoft.com/fwlink/?LinkId=57870)。

在本模組中,很好地涵蓋了 Web 專案創建、管理和開發方面的改進。 在後面的模組中,很好地涵蓋了構建 Web 專案並部署它們的改進。

## <a name="frontpage-server-extensions"></a>首頁伺服器延伸

Visual Studio .NET 2002 和 2003 需要框上的 FrontPage 伺服器擴展,以便創建或生成 Web 專案。 開發人員在兩種不同的訪問模式(FrontPage 伺服器擴展名或文件存取模式)之間進行選擇,這兩種模式都使用 FrontPage 伺服器擴展程式執行諸如在 IIS 中設置應用程式根等任務。

Visual Studio 2005 消除了對本地專案 FrontPage 伺服器擴展的依賴。 Visual Studio 2005 現在直接存取IIS元庫,而不是使用FrontPage伺服器擴展。 Visual Studio 2005 還添加了對 FTP 的支援,該支援允許遠端項目訪問,而無需 FrontPage 伺服器擴展。

對於那些想要在其專案中使用 FrontPage 伺服器擴展的開發人員,該選項仍然可用。 但是,根據ASP.NET開發人員社區的強烈反饋,這不是一項要求。

> [!NOTE]
> 遠端項目創建、打開等仍然需要 FrontPage 伺服器擴展。

## <a name="aspnet-development-server"></a>ASP.NET 程式開發伺服器

Visual Studio 2005 附帶了一個名為ASP.NET開發伺服器的新 Web 伺服器。 (此 Web 伺服器以前稱為卡西尼。

ASP.NET開發伺服器有幾個好處。

- 現在,非管理員可以針對 Web 伺服器開發和調試。
- ASP.NET開發伺服器動態地將虛擬目錄映射到檔案系統中的任何位置,從而允許靈活的專案位置。
- Windows XP 專業版上已經使用 IIS 的使用者現在將能夠創建新的 Web 應用程式,這些應用程式不會影響其在 IIS 中的預設網站的檔案或資料夾結構。

無需特殊配置即可利用ASP.NET開發伺服器。 當檔案系統上託管的 Web 專案被調試或流覽時,Visual Studio 2005 將自動啟動隨機埠上的 ASP.NET 開發伺服器的實例來為請求提供服務。

本模組稍後將介紹ASP.NET開發伺服器的詳細資訊。

## <a name="improved-file-management"></a>改進的檔案管理

在 Visual Studio 2002 和 2003 中,一個專案檔(VB.NET.vbproj 和 .csproj 表示 C#)儲存了 Web 應用程式中所有檔案的資訊。 解決方案資源管理員顯示基於專案檔中的檔資訊。 因此,在使用外部編輯器的情況下,解決方案資源管理器通常會顯示不準確的資訊。 Visual Studio 2002 和 2003 通常會覆蓋檔更改或不顯示最新版本的檔。

Visual Studio 2005 不需要使用專案檔。 相反,它直接從磁碟讀取檔和資料夾資訊,從而準確顯示專案中的檔。 由於 Visual Studio 2002 和 2003 中的「引用」資料夾不表示 Web 應用程式中的實際資料夾,因此 Visual Studio 2005 還會從解決方案資源管理器中刪除"引用"資料夾。 要造訪 Visual Studio 2005 中的專案的引用,應使用專案的屬性頁。

## <a name="creating-web-projects"></a>建立 Web 專案

Web 開發人員在 Visual Studio 2005 中有許多可用於專案創建的新選項。 網站現在可以在檔案系統的任意位置創建,然後可以使用新的ASP.NET開發伺服器進行調試或流覽。 開發人員還可以使用 FTP 創建新的網站。

按一下此處查看 Visual Studio 2005 中創建 Web 專案的影片演練。

![](improvements-in-visual-studio-2005/_static/image1.png)

[開啟全螢幕視訊](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a>檔案系統專案

正如您在影片演練中所看到的,您可以選擇透過檔共享在檔案系統上或在遠端位置創建網站。 使用ASP.NET開發伺服器瀏覽和除錯在檔案系統上創建的網站。

> [!NOTE]
> ASP.NET開發伺服器可能會給客戶帶來一些混亂。 如果在 IS 目錄結構(即 c:/inetpub/wwwroot)的檔案系統上創建了 Web 專案,則從 Visual Studio 2005 內部啟動時,該網站仍將通過 ASP.NET 開發伺服器進行流覽。 因此,任何IIS配置(即身份驗證方法)都不適用。

默認 Web 專案還僅包括 Default.aspx 頁、default.cs 檔和 App/_Data 資料夾,從而刪除了大量開銷。 根據需要添加 Web.config 和特殊資料夾(即應用/_code)。 您的 Web 專案僅包括所需的檔案和資料夾。

### <a name="http-projects"></a>HTTP 專案

HTTP 專案可以是在本地 IIS 網站或遠端網站上創建的專案。 預設項目位置為`http://localhost`。 如果按下「瀏覽」按鈕,則有兩個 HTTP 選項:本地 IIS 和遠端網站。 這兩個選項的主要區別是在"選擇位置"對話框中顯示網站資訊的方法以及檔案複製到 Web 伺服器的方式。

"本地 IIS"選項從本地電腦上的中式庫讀取網站資訊,並使用檔案系統複製檔。 遠端站點選項使用 FrontPage 伺服器擴展名,網站資訊和檔使用 HTTP 和 FrontPage 伺服器擴展程式 RPC 呼叫進行複製。

> [!NOTE]
> vs_/_tmp.htm 檔和 get/_aspx/_ver.aspx 不再用於確定版本資訊。

默認 HTTP 選項為本地 IIS。 此選項讀取 IIS 中庫以確定哪些網站可用以及創建內容的位置。 您可以透過在樹檢視中選擇其他資料夾或虛擬目錄來選擇它。 您還可以創建新的虛擬目錄、將資料夾標記為應用程式,以及從此對話框中刪除現有的虛擬目錄。

![選擇位置對話框](improvements-in-visual-studio-2005/_static/image1.gif)

**圖 1**: 選擇位置對話框

與早期版本的 Visual Studio 不同,如果選中 **「使用安全套接字層」** 複選框,並且 SSL 證書與您正在流覽的 URL 不匹配,則將顯示一個安全警報對話框,詢問您是否要繼續。 使用 Visual Studio .NET 2003,如果證書不是匹配的,則創建項目將失敗。

![有關 SSL 憑證的安全警示](improvements-in-visual-studio-2005/_static/image2.gif)

**圖 2**: 有關 SSL 憑證的安全警示

### <a name="note-on-host-headers"></a>主機標題上的註解

如果要在綁定到特定 IP 的站台上創建 Web 應用程式,則需要確保配置主機標頭。 否則,Visual Studio`http://localhost`將在中創建網站,但當從 IDE 內部流覽或調試網站時,IP 位址將無法正確解析。

如果選擇「遠端網站」選項,則對話框將更改以允許您輸入新網站的目標 URL。 此 URL 必須位於已啟用了 FrontPage 伺服器擴展名的伺服器上。 如果要使用 FrontPage 伺服器擴展程式使用本地 Web 伺服器,可以使用「遠端網站」選項並指定本地網址。

![在遠端伺服器上建立網站](improvements-in-visual-studio-2005/_static/image1.jpg)

**圖 3**: 在遠端伺服器上建立網站

通過 SSL 在遠端網站上創建應用程式時,如果 SSL 證書不匹配,則確認對話方塊與使用本地 IIS 選項時顯示的對話方塊略有不同。

![遠端網站安全警報](improvements-in-visual-studio-2005/_static/image3.gif)

**圖 4**: 遠端站台安全警示

<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005 引入了透過 FTP 創建網站的選項。 使用此選項時,IDE 會在使用者臨時資料夾中在本地創建檔案,然後使用 FTP 將檔案移動到 FTP 位置。

> [!NOTE]
> 暫存資料夾位置為 c:/文件與&lt;設定&gt;/ 使用者 /本地設定/Temp/VWDWebCache/&lt;伺服器&gt;/=&lt;應用程式名稱&gt;

使用 FTP 選項時,將顯示「選擇位置」對話方塊。 在此對話框中輸入所需的 FTP 連接資訊,如下所示。

![FTP 選擇位置對話框](improvements-in-visual-studio-2005/_static/image2.jpg)

**圖 5**: FTP 的"選擇位置對話方塊"

## <a name="lab-setup-ftp-site-and-create-a-project"></a>實驗室:設定 FTP 網站並建立專案

以下步驟配置 FTP 網站,以便使用者具有只有他們才能通過 FTP 上載到的位置。

### <a name="install-the-ftp-service"></a>安裝 FTP 服務

1. 打開"添加刪除程式",選擇"添加/刪除 Windows 元件"
2. 選擇互聯網資訊服務(Windows 2003 上的應用程式伺服器),然後單擊 **「詳細資訊**」。
3. 檢查**檔案傳輸協定 (FTP) 服務**,然後按一下 **「確定**」。
4. 按下 **「下一步**」以安裝 FTP 服務。

### <a name="create-a-new-folder-for-content"></a>建立新資料夾

1. 在 Windows 資源管理器中,在 c:/inetpub/wwwroot 內部創建名為**User1**的新資料夾。

#### <a name="configure-folders-and-permissions-on-folders"></a>配置資料夾和資料夾的許可權。

1. 從管理工具打開互聯網資訊服務快照。 現在,您的電腦名稱節點下將有一個 FTP Sites 資料夾。
2. 延伸**FTP 網站**。
3. 右鍵按一下**預設 FTP 網站**,選擇 **"新建**",然後按一下 **「****下一步**」。
4. 輸入虛擬目錄名稱**的使用者 1,** 然後按下 **「下一步**」 。
5. 輸入**路徑的 c:/inetpub/wwwroot/User1,** 然後單擊 **"下一步**"。
6. 按下 **「下一步****」,然後單擊"完成"** 以完成嚮導。
7. 右鍵按這裏預設 FTP 網站下的**User1**虛擬目錄,然後選擇**屬性**。
8. 選中 **「寫入」** 複選框,然後按下 **「 確定」** 以關閉對話框。
9. 右鍵按下**預設 FTP 網站**並選擇**屬性**。
10. 在「**安全帳戶」** 選項卡上,取消選中 **「允許匿名連接**」。。
11. 在對話框中按下 **「是**」,詢問是否要繼續。
12. 按一下 **[確定]** 關閉對話方塊。
13. 在 **「網站」** 節點下展開**預設網站**。
14. 右鍵單擊**User1**目錄並選擇 **"屬性"**
15. 在「**應用程式設定」** 部分中,按一下「**創建**」 將資料夾標記為應用程式。
16. 按一下 **[確定]** 關閉對話方塊。
17. 關閉互聯網資訊服務卡入。

### <a name="create-web-project"></a>建立 Web 專案

1. 開放視覺工作室 2005.
2. 在 **「檔案」** 選單中,選擇 **「新建網站**」 。。
3. 在 **'位置**' 下拉下清單中, 選擇**FTP**。
4. 按一下 [瀏覽]****。
5. 輸入**本地**端的伺服器文字盒中輸入**本地端主機**。
6. 在「目錄」文字框中輸入**使用者 1。**
7. 按一下 [開啟]****。 FTP 位置將輸入到"新建網站"對話框中。
8. 按一下 [確定]  。
9. 取消在 FTP 登入對話方塊中**打開匿名登錄**,輸入認證,然後單擊「**確定**」。
10. 專案的 URL 是什麼? (專案的網址將顯示在解決方案資源管理員中。
11. 在 **「生成」** 選單中,選擇 **「生成網站**」或 **「生成解決方案**」 。
12. 右鍵單擊解決方案資源管理器中的 Default.aspx,然後選擇 **「瀏覽器中的檢視**」。。
13. 在「網站網址必需」對話框中,`http://localhost/user1`輸入 URL 並按一下「**確定**」。

> [!NOTE]
> 如果收到指示無法載入類型 /_Default的錯誤,請確保在 Web 網站上運行 ASP.NET 2.0,而不是早期版本。 您可以在「互聯網資訊服務」 中的 ASP.NET 選項卡上執行此操作。

## <a name="opening-web-projects"></a>開啟網頁專案

打開 Web 專案類似於建立專案。 以下各節會標註在IDE中工作時注意的區域。 它還涵蓋使用 HTTP 和 FTP 處理 Web 專案。

要打開 Web 專案,請從「檔」功能表中選擇「打開網站」。 系統、本地 IIS、FTP 和遠端網站,系統將提示您使用以前介紹的相同"選擇位置"對話框,並且有相同的四個選項可供您使用。

<a id="_Toc116100245"></a>

## <a name="file-system"></a>檔案系統

如本模組前面所述,Visual Studio 不再使用專案檔。 因此,如果您選擇從檔案系統打開網站,則實際上可以選擇任何希望選擇的資料夾,即使您選擇的資料夾最初未在 Visual Studio 中作為 Web 專案創建。 例如,您可以選擇以網站身份打開"我的文檔"資料夾,Visual Studio 將愉快地打開該資料夾並顯示您的檔,如下所示。

![我的文件作為網站開啟](improvements-in-visual-studio-2005/_static/image3.jpg)

**圖 6**:*我的文件*作為網站開啟

由於 Visual Studio 僅在必要時創建其他檔和資料夾,因此不會將其他檔案或資料夾添加到您打開的位置。 此體系結構的副作用是,它可以防止您在文件系統上嵌套網站。 例如,請考慮以下目錄結構。

C:/我的Web網站網路專案

C:/MyWebSite/嵌套的另一個 Web 專案

當您在 c:/MyWebSite 打開網站時,「嵌套」資料夾將顯示為該應用程式的子資料夾。

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

通過 HTTP 打開網站時,可以從 IIS 中庫(本地 IIS)或使用 FrontPage 伺服器擴展(遠端網站)讀取設置。如果有嵌套 Web 應用程式,則這些應用程式將顯示,並帶有一個圖示,用於標識它們為應用程式。 如果您熟悉在 FrontPage 中處理 Web 應用程式,則 Visual Studio 2005 中的行為類似。

即使 Visual Studio 將顯示嵌套在 IDE 中當前打開的應用程式下方的應用程式的圖示,但它也不允許擴展它們以查看其內容。 但是,您可以雙擊它們以打開它們。 執行此操作時,將顯示一個對話框,提示您打開 Web 應用程式(並取代當前打開的解決方案)或將 Web 應用程式添加到當前解決方案。

![按兩下嵌 sotcrit 的資訊標示會顯示此對話框](improvements-in-visual-studio-2005/_static/image4.jpg)

**圖 7**: 雙擊嵌套應用程式圖示將為您提供此對話框

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>FTP 站台

當您透過 FTP 打開網站時,這些檔都將在本地複製到暫存資料夾。 本地儲存位置的完整路徑顯示在專案的"屬性"窗格中,並使用以下格式創建。

C:/文件與設定/&lt;&gt;使用者 /本地設定/Temp/VWDWebCache/&lt;伺服器&gt;/=&lt;應用程式名稱&gt;

使用 FTP 時,Visual Studio 需要指定專案的基本 URL,以便可以流覽它,如下所示。 如果不指定基本 URL,Visual Studio 將在您首次嘗試瀏覽網站中的頁面時詢問它。

![為 FTP 網站指定基本網址](improvements-in-visual-studio-2005/_static/image5.jpg)

**圖 8**: 為 FTP 網站指定基本網址

## <a name="improvements-in-compilation"></a>編譯的改進

在 Visual Studio 2005 中處理 Web 應用程式的速度明顯快於以前的版本。 這在很大程度上是由於編譯體系結構的更改。

在 Visual Studio 2002 和 2003 中,Web 應用程式被編譯為駐留在 /bin 資料夾中的一個主程式集。 在 Visual Studio 2005 中,添加了一個應用/_Code資料夾。 類和其他非 UI 代碼將添加到應用/_Code資料夾。 當 Visual Studio 生成專案時,App/_Code 資料夾中的所有檔都將編譯為單個 App/_Code.dll 檔。 此更改的結果是後續生成比早期版本快得多。

> [!NOTE]
> MSBuild 命令行實用程式還可用於建構ASP.NET Web 應用程式。 該工具將在第 9 單元中介紹。

另一個編譯增強功能是"生成"功能表上的新"生成頁"選項。 此功能允許開發人員僅重建當前頁面(當然,以及依賴項),以便可以更快地編譯更改。 由於 C# 不提供用於更新 IntelliSense 等的背景編譯,因此它們將從此功能中獲益匪淺,因為它將允許通過僅重建單個頁面快速更新 IntelliSense。

專案的生成屬性允許您設定在執行啟動頁之前發生的生成類型。 開發人員可以選擇僅生成當前頁面,以便 Visual Studio 可以在代碼更改後更快地開始調試應用程式。

![製作頁啟動](improvements-in-visual-studio-2005/_static/image6.jpg)

**圖 9**: 產生頁面開始操作

Visual Studio 和 ASP.NET架構的另一大增強是在編輯和繼續方面。 在 Visual Studio 2005 中,開發人員可以開始調試專案,並在專案上進行代碼更改,而無需分離調試器。 事實上,您可以從字面上開始調試專案、添加新類、向該類添加代碼、向創建該類的新實例的頁面添加代碼以及執行類的方法,所有這些都不分離調試器。 執行新代碼實際上和刷新瀏覽器一樣簡單!

按一下此處查看 Visual Studio 2005 中編輯影片演練並繼續功能。

![](improvements-in-visual-studio-2005/_static/image2.png)

[開啟全螢幕視訊](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

ASP.NET 2.0 和 Visual Studio 2005 中強大的編輯和繼續功能是由於ASP.NET應用程式的體系結構更改。 在 ASP.NET 1.x 中,在 Visual Studio 2002/2003 中創建的應用程式編譯為存儲在 /bin 資料夾中的主程式集。 應用程式的所有類、頁面等都編譯到該 DLL 中。 然後在運行時,ASP.NET將編譯頁面中的所有控制件、標記和ASP.NET代碼,並將這些DLL複製到ASP.NET臨時資料夾中。

在使用 ASP.NET 2.0 的 Visual Studio 2005 中,上述兩個編譯模型(一個用於 Visual Studio,一個用於運行時 ASP.NET)已合併為一個通用編譯模型。 這意味著所有編譯問題現在都在開發階段而不是運行時捕獲。 它還允許設計器和 IntelliSense 支援使用者控制件和母版頁等功能。

按一次檢視設計器對使用者控制的影片演練。

![](improvements-in-visual-studio-2005/_static/image3.png)

[開啟全螢幕視訊](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> 從頁面中刪除使用者控制項時,@Register該指令將保留在標記中,並且應手動刪除,以避免在從網站中刪除使用者控制項時解析器錯誤。

可視化工作室編譯模型的另一個改進是發佈網站功能。 由於「發佈」功能預先編譯了網站,因此開發人員可以享受無需按需編譯任何內容的額外性能。 它還將 App/_Code 資料夾中的所有原始程式碼預編譯為 DLL,以便無需部署原始碼。

![發布網站對話框](improvements-in-visual-studio-2005/_static/image7.jpg)

**圖 10**: 發布網站對話框

> [!NOTE]
> aspnet/_compile.exe 實用程式也可用於預編譯ASP.NET Web 應用程式。 該工具將在第 9 單元中介紹。

發佈網站時,預編譯檔將存儲在臨時ASP.NET檔資料夾中,如下所示。 具有 *.ssd*檔案副檔名的檔案是定義特定 DLL 依賴項的 XML 檔。 任何 Web 窗體或使用者控制器都編譯為以*應用 _/Web/_* 開頭的隨機 DLL。

如果選擇「*允許此預編譯網站可升級」* 複選框,則 Web 窗體和使用者控制件內的標記將不會預先編譯為 DLL,從而允許您在部署後進行更改。 如果您希望鎖定標記以不允許更改已部署的內容,請取消選中此框。

*使用固定命名和單頁程式集*複選框允許您禁用批處理編譯,以便將每個頁面編譯為固定命名的程式集。 未勾選此方塊允許您利用批次處理編譯。

*啟用預編譯程式集上的強命名*複選方塊允許您對預編譯程式集進行強名稱。

> [!NOTE]
> 在 ASP.NET 1.x 中,必須將強名稱程式集安裝到全域程式集緩存 (GAC)。 在 ASP.NET 2.0 中,您不需要在 GAC 中安裝強名稱程式集。

![ASP.NET應用程式預先編譯檔](improvements-in-visual-studio-2005/_static/image8.jpg)

**圖11:ASP.NET**應用程式預編譯檔

> [!NOTE]
> 在上面的應用程式中,沒有 Web.config 檔。 如果有,它將在發佈網站過程后稱為*預編譯App.config。*

## <a name="improvements-in-deployment"></a>部署的改進

與 Visual Studio 2002 和 2003 一樣,Visual Studio 2005 提供了複製專案功能。 但是,該功能已在 Visual Studio 2005 中進行了增強,現在稱為"複製網站"。

複製網站"對話框將拆分為左側框架和右框架。 左幀稱為源網站,右框架稱為遠程網站。 有一件事可能會令一些開發人員感到困惑,那就是顯示在正確框架中的網站不一定是遠端網站。 它可以是本地文件系統或IIS本地實例上的網站。 此外,左側框架中顯示的網站不一定是源網站,因為對話框允許您從遠端網站*發佈到*源網站。

如果要將專案複製到遠端網站,則該站點必須安裝 FrontPage 伺服器擴展程式。 如果沒有,則需要使用 FTP 進行連接。 另一方面,如果要將專案複製到本地 IIS 實例,則不需要 FrontPage 伺服器擴展。

> [!NOTE]
> 如果您嘗試在本地 IIS 實例上創建新網站,並且安裝了 FrontPage 2002 伺服器擴展程式,則會收到一條錯誤消息,告訴您在 SharePoint 伺服器上不支援創建網站。 在這種情況下,您可以選擇安裝 FrontPage 2000 伺服器擴展或刪除 FrontPage 伺服器擴展名。

按一下此處查看複製網站功能的視頻演練。

![](improvements-in-visual-studio-2005/_static/image4.png)

[開啟全螢幕視訊](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a>除錯改進

Visual Studio 2005 中的調試有四個關鍵改進。

- 以非管理員身份在本地進行調試可以開箱即用。
- 默認情況下,編譯元素的調試屬性現在為 false。
- 遠端調試設置和配置比以前更容易。
- 現在,您可以調試通過 FTP 位置打開的網站。

## <a name="debugging-as-a-non-administrator"></a>作為非管理員進行除錯

添加ASP.NET開發伺服器允許非管理員輕鬆調試ASP.NET應用程式開箱即用。 除錯本地檔案系統上執行ASP.NET應用程式時,Visual Studio在登入使用者的上下文中啟動ASP.NET開發伺服器。 然後,該使用者可以調試該應用程式,而無需任何其他配置。

## <a name="debug-is-false-by-default"></a>預設情況下,除錯為 false

在 ASP.NET 1.x 中,預設情況下,Web.config 檔*編譯*元素中的*調試*屬性設置為*true。* 始終建議開發人員在將應用程式部署到生產之前將此屬性設置為*false,* 但由於大多數開發人員並不完全瞭解將調試屬性設置為 true 的後果,因此他們只是將其保留原樣。

將除錯屬性設定為 true 的最嚴重的問題是禁用 ASP.NETs 批次處理編譯模型。 因此,每個頁面都編譯成一個單獨的 DLL。 如果 Web 應用程式由數千個頁面組成(並非任何方法所聞所未聞),則這意味著該應用程式將創建數千個小型 DLL。 雖然這些 DLL 大小較小,但它們不會載入到記憶體中的任何特定位置。 因此,它們會導致系統記憶體中的碎片,並可能導致記憶體外異常事件。

在 ASP.NET 2.0 中,默認情況下調試屬性設置為 false。 正如您已經看到的那樣,當開發人員在 Visual Studio 2005 中調試ASP.NET應用程式時,系統會提示他們添加啟用調試的 Web.config 檔。 這樣做會產生與ASP.NET 1.x 中相同的缺點,但現在開發人員被明確警告,在將應用程式移動到生產之前,應將屬性重置為 false。

## <a name="remote-debugging-setup-and-configuration"></a>遠端除錯設定與設定

在 Visual Studio 2002/2003 中,遠端調試依賴於電腦調試管理器 (mdm.exe) 和 vs7jit.exe 過程。 因此,排除遠端調試問題的故障通常是客戶的一個黑匣子,對 PSS 通常沒有多大説明。

Visual Studio 2005 消除了對 mdm.exe 和 vs7jit.exe 進程的依賴。 相反,它現在使用遠端除錯監視器服務 (msvsmon.exe.)

Visual Studio 2005 遠程調試的要求非常簡單。 在除錯之前,您需要在遠端伺服器上執行 msvsmon.exe。 可以從 Visual Studio CD 安裝遠端除錯監視器,也可以簡單地從共享運行 msvsmon.exe,而無需在 Web 伺服器上安裝任何內容。

運行 msvsmon.exe 時,可能會抱怨埠被阻止進行遠端調試。 幸運的是,您可以在警告對話框中輕鬆取消阻止埠,如下所示。

![通知 Windows 防火牆封鎖遠端除錯](improvements-in-visual-studio-2005/_static/image9.jpg)

**圖 12**: 通知 Windows 防火牆封鎖遠端除錯

取消阻止調試所需的埠後,您將看到遠端調試監視器,如下所示。 通過此介面,您可以輕鬆監視連接並更改調試許可權。

![遠端除錯監視器](improvements-in-visual-studio-2005/_static/image10.jpg)

**圖 13**: 遠端除錯監視器

還可以遠端除錯透過 FTP 打開的 Web 應用程式。 步驟與之前介紹的步驟相同。 但是,您需要指定用於瀏覽本模組前面概述的 FTP 專案的基本 URL。

## <a name="lab-2"></a>實驗室 2

## <a name="remote-debugging-with-visual-studio-2005"></a>使用視覺化工作室 2005 進行遠端除錯

本實驗將引導您透過 Visual Studio 2005 進行遠端調試。

按一下此處查看本實驗的視頻演練。

![](improvements-in-visual-studio-2005/_static/image5.png)

[開啟全螢幕視訊](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

本實驗要求您擁有兩台電腦,一台運行 Visual Studio 2005,另一台運行 IIS 5 或更高。

1. 打開 Visual Studio 2005 並在遠端伺服器上創建新的網站。

> [!NOTE]
> 您可以在遠端 IIS 實體上或透過 FTP 創建網站。

1. 從遠端 Web 伺服器,使用 UNC 路徑在開發電腦上找到 msvsmon.exe 並將其執行。  
 msvsmon.exe 的預設位置是 //伺服器/c$/程式檔/微軟視覺工作室 8/Common7/IDE/遠端調試器/x86。
2. 如果提示取消阻止埠進行遠端調試,則執行此操作。
3. 從開發電腦打開 Default.aspx 的代碼後面,並在 page/_Load 方法中設置斷點。
4. 從開發電腦開始調試。

您應該按預期命中斷點。

## <a name="aspnet-development-server"></a>ASP.NET 程式開發伺服器

正如我們已經討論過的,Visual Studio 2005 附帶了一個名為ASP.NET開發伺服器的 Web 伺服器。 (ASP.NET開發伺服器有時稱為卡西尼。此 Web 伺服器是瀏覽和除錯檔案系統執行的 Web 應用程式的便捷方法。

ASP.NET開發伺服器是受限的 Web 伺服器。 它不允許遠端連接,它不允許來自除啟動 Web 伺服器的使用者以外的任何使用者的任何請求。 它還不能為 ASP 頁提供服務。 僅提供ASP.NET資源和 HTML 資源(包括圖像、CSS 檔等)。

ASP.NET開發伺服器可以通過命令行啟動,通過運行位於 c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/*的 WebDev.WebServer.exe 檔。 以下對話框顯示可用的參數。

![](improvements-in-visual-studio-2005/_static/image11.jpg)

**圖 14**

> [!NOTE]
> 通過命令行顯式啟動時,不支援ASP.NET開發伺服器。
