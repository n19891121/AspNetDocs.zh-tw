---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: 使用 CAPTCHA 防止機器人使用您的ASP.NET網络剃刀)網站 |微軟文件
author: rick-anderson
description: 本文介紹如何使用 ReCaptcha(安全措施)來防止自動程式 (bot) 在 ASP.NET 網頁 (Razor) 中執行任務...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 65f414ae3fed5e2fa28b1e57f5327c6411a43d55
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543752"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>使用 CAPTCHA 防止機器人使用ASP.NET網路剃刀)網站

由[微軟](https://github.com/microsoft)

> 本文介紹如何使用 ReCaptcha(安全措施)來防止自動程式 (bot) 在ASP.NET網頁 (Razor) 網站中執行任務。
> 
> **您將學到什麼：** 
> 
> - 如何向您的網站添加 CAPTCHA 測試。
> 
> 以下是本文介紹的ASP.NET功能:
> 
> - 幫手`ReCaptcha`
> 
> > [!NOTE]
> > 本文中的資訊適用於ASP.NET網頁 1.0 和網頁 2。

## <a name="about-captchas"></a>關於 CAPTCHAs

任何時候,當你讓人們在您的網站註冊,甚至只是輸入一個名字和URL(如博客評論),你可能會得到大量的假名。 這些通常由自動程式(機器人)留下,這些程式(機器人)試圖在他們能找到的每個網站中保留 URL。 (一個常見的動機是發佈要銷售的產品的 URL。

通過使用*CAPTCHA*驗證使用者註冊或以其他方式輸入其名稱和網站時,可以幫助確保使用者是真實使用者而不是電腦程式。 CAPTCHA 代表完全自動化的公共圖靈測試,告訴計算機和人類分開。 CAPTCHA 是一種*質詢-回應*測試,要求使用者執行一些使用者容易做的事情,但自動化程式卻很難做到。 CAPTCHA的最常見類型是看到一些扭曲的字母並被要求鍵入它們。 (失真應該使機器人很難破譯這些字母。

## <a name="adding-a-recaptcha-test"></a>新增重新卡普查測試

在ASP.NET頁中`ReCaptcha`,可以使用説明程序呈現基於ReCaptcha服務[http://recaptcha.net](http://recaptcha.net)(的CAPTCHA測試)。 `ReCaptcha`説明程序顯示兩個扭曲的單詞的圖像,使用者在驗證頁面之前必須正確輸入這些單詞。 用戶回應由ReCaptcha.Net服務驗證。

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. 在ReCaptcha.Net註冊您的網站。[http://recaptcha.net](http://recaptcha.net) 完成註冊后,您將獲得公鑰和私鑰。
2. 將ASP.NET Web 幫助器庫添加到您的網站,如[在ASP.NET網頁網站中安裝説明程式](https://go.microsoft.com/fwlink/?LinkId=252372)(如果您尚未)中所述。
3. 如果您還沒有*\_AppStart.cshtml*檔,則在網站的根資料夾中創建名為*\_AppStart.cshtml*的檔。
4. `Recaptcha`*在\_AppStart.cshtml*檔加入以下說明程式設定: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. 使用您自己的`PublicKey``PrivateKey`公共和私密金鑰設定和屬性。
6. 保存*\_AppStart.cshtml*檔並關閉它。
7. 在網站的根資料夾中,創建名為*Recaptcha.cshtml*的新頁面。
8. 將現有內容取代為以下內容: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. 在瀏覽器中運行*Recaptcha.cshtml*頁面。 如果`PrivateKey`該值有效,則頁面將顯示 ReCaptcha 控件和一個按鈕。 如果未在*\_AppStart.html*中全域設置金鑰,則頁面將顯示錯誤。 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. 輸入測試的單詞。 如果通過 ReCaptcha 測試,則會看到一條達到該效果的消息。 否則,您將看到一條錯誤消息,並重新顯示 ReCaptcha 控件。

> [!NOTE]
> 如果您的電腦位於使用代理伺服器的域中,則可能需要配置*Web.config*`defaultproxy`檔案的元素。 下面的範例顯示了一個*Web.config*檔`defaultproxy`,該檔配置了元素以使 ReCaptcha 服務正常工作。
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他資源

- [為ASP.NET網頁網站自訂網站範圍行為](https://go.microsoft.com/fwlink/?LinkId=202906)
- [雷卡普查網站](https://www.google.com/recaptcha)
