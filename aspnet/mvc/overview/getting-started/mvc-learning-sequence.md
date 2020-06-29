---
uid: mvc/overview/getting-started/mvc-learning-sequence
title: MVC 建議的教學課程和文章 |Microsoft Docs
author: Rick-Anderson
description: 此頁面包含 ASP.NET MVC 教學課程的連結，以及要遵循的建議順序。
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 8513a57a-2d45-4d6b-881c-15a01c5cbb1c
msc.legacyurl: /mvc/overview/getting-started/mvc-learning-sequence
msc.type: authoredcontent
ms.openlocfilehash: 7dc81cf09309194df4471fedfc74d4051f0fdb78
ms.sourcegitcommit: 8d34fb54e790cfba2d64097afc8276da5b22283e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85484213"
---
# <a name="mvc-recommended-tutorials-and-articles"></a>MVC 建議教學課程與文章

依[Rick Anderson](https://twitter.com/RickAndMSFT)

<a id="pwd"></a>
## <a name="getting-started"></a>開始使用

- [ASP.NET MVC 5 的消費者入門](introduction/getting-started.md)這一系列的11部分是不錯的開端。
- [Pluralsight ASP.NET MVC 5 基本](https://pluralsight.com/training/Player?author=scott-allen&amp;name=aspdotnet-mvc5-fundamentals-m1-introduction&amp;mode=live&amp;clip=0&amp;course=aspdotnet-mvc5-fundamentals)概念（影片課程）
- [ASP.NET MVC](https://channel9.msdn.com/Series/Introduction-to-ASP-NET-MVC) By Jon Galloway 和 Christopher Harrison 的簡介
- [ASP.NET MVC 5 應用程式的生命週期](lifecycle-of-an-aspnet-mvc-5-application.md)此 PDF 檔會圖表 ASP.NET MVC 5 應用程式的生命週期。

<a id="con"></a>
## <a name="working-with-data"></a>使用資料

- [使用 MVC 5 消費者入門與 EF 6 Code First](getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)Tom 作者: dykstra 的獲獎獲獎系列探討深入探討 EF。

<a id="wj"></a>
## <a name="security"></a>安全性

- [使用驗證和 SQL DB 建立 ASP.NET MVC 應用程式並部署至 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)這個熱門的教學課程會逐步引導您建立簡單的應用程式，以及新增成員資格和角色。
- [使用 Facebook、Twitter、LinkedIn 和 Google OAuth2 登入來建立 ASP.NET MVC 5 應用程式](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)本教學課程會示範如何建立 ASP.NET MVC 5 web 應用程式，讓使用者能夠使用 OAuth 2.0 搭配來自外部驗證提供者（例如 Facebook、Twitter、LinkedIn、Microsoft 或 Google）的認證來進行登入。
- [使用登入、電子郵件確認和密碼重設建立安全的 ASP.NET MVC 5 web 應用程式](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)首先在一系列的身分識別中，包含[重新傳送確認連結的](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md#rsend)程式碼。
- [使用 SMS 和電子郵件雙因素驗證 ASP.NET MVC 5 應用程式](../security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)在身分識別系列上為第二個。
- [將密碼和其他敏感性資料部署到 ASP.NET 和 Azure App Service 的最佳做法](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)
- [使用 SMS 的雙因素驗證與 ASP.NET Identity](../../../identity/overview/features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md) `isPersistent` 的電子郵件和安全性 cookie 的程式碼，要求使用者必須先擁有已驗證的電子郵件帳戶，才能登入、使用檢查是否有2FA 需求等等。
- [使用 ASP.NET Identity 進行帳戶確認和密碼](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)復原提供在[使用登入、電子郵件確認和密碼重設建立安全 ASP.NET MVC 5 web 應用程式](../security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)中找不到之識別的詳細資料，例如如何讓使用者重設其遺忘的密碼。

<a id="da"></a>
## <a name="azure"></a>Azure

- [在 Azure 中建立 ASP.NET web 應用程式](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)部署至 Azure 的簡短和簡單教學課程。
- [使用驗證和 SQL DB 建立 ASP.NET MVC 應用程式並部署至 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)

<a id="perf"></a>
## <a name="performance-and-debugging"></a>效能和調試

- [使用 Glimpse 分析 ASP.NET MVC 應用程式以對其進行偵錯](../performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse.md)

## <a name="aspnet-mvc-dropdownlistfor-with-selectlistitem"></a>具有 SelectListItem 的 ASP.NET MVC Html.dropdownlistfor

當您使用 <xref:System.Web.Mvc.Html.SelectExtensions.DropDownListFor%2A> helper 並將它傳遞至它的集合時，會在 `SelectListItem` `DropdownListFor` 呼叫它之後修改傳遞的集合。 `DropdownListFor`將 `SelectListItems` 選取的屬性變更為下拉式清單所選取的內容。 這會導致非預期的行為。

<xref:System.Web.Mvc.Html.SelectExtensions.DropDownListFor%2A>、 <xref:System.Web.Mvc.Html.SelectExtensions.DropDownList%2A> 、 <xref:System.Web.Mvc.Html.SelectExtensions.EnumDropDownListFor%2A> 、和會 <xref:System.Web.Mvc.Html.SelectExtensions.ListBox%2A> <xref:System.Web.Mvc.Html.SelectExtensions.ListBoxFor%2A> 更新 ViewData 中任何已 `IEnumerable<SelectListItem>` 傳遞或找到的已選取屬性。

因應措施是 `SelectListItem` 針對模型中的每個屬性建立個別的可列舉值，其中包含不同的實例。

如需相關資訊，請參閱

* [Html.dropdownlistfor 會修改傳遞給它的 SelectListItem 集合](http://web.archive.org/web/20140902031437/http://aspnetwebstack.codeplex.com/workitem/1913)
* [GetSelectListWithDefaultValue 修改 IEnumerable <SelectListItem> selectList](https://github.com/aspnet/AspNetWebStack/issues/271)