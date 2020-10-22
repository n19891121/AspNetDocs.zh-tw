---
uid: web-api/overview/advanced/dependency-injection
title: ASP.NET Web API 2 中的相依性插入-ASP.NET 4。x
author: MikeWasson
description: 本教學課程說明如何將相依性插入 ASP.NET 4.x 的 ASP.NET Web API 控制器。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 3342d93340215d937cf7161ee1c4b32931d516a3
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345268"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的相依性插入

由 [Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> 本教學課程說明如何將相依性插入 ASP.NET Web API 控制器。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教學課程中使用的軟體版本
> 
> 
> - Web API 2
> - [Unity 應用程式區塊](https://www.nuget.org/packages/Unity/)
> - Entity Framework 6 (第5版也適用) 

## <a name="what-is-dependency-injection"></a>什麼是相依性插入？

「相依性」** 是另一個物件所需的任何物件。 例如，通常會定義可處理資料存取的 [儲存](http://martinfowler.com/eaaCatalog/repository.html) 機制。 讓我們以範例來說明。 首先，我們將定義領域模型：

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

以下是簡單的儲存機制類別，可使用 Entity Framework 將專案儲存在資料庫中。

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

現在讓我們來定義 Web API 控制器，以支援實體的 GET 要求 `Product` 。  (我為了簡單起見，會留下 POST 和其他方法。 ) 第一次嘗試：

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

請注意，控制器類別相依于 `ProductRepository` ，而我們正讓控制器建立 `ProductRepository` 實例。 不過，基於許多原因，以這種方式硬編碼相依性是個不錯的主意。

- 如果您想要以 `ProductRepository` 不同的實作為取代，您也需要修改控制器類別。
- 如果有相依性 `ProductRepository` ，您必須在控制器內部設定這些相依性。 針對具有多個控制器的大型專案，您的設定程式碼會在您的專案中散佈。
- 由於控制器是以硬式編碼方式來查詢資料庫，因此很難進行單元測試。 針對單元測試，您應該使用模擬或存根儲存機制，但目前的設計並不可能這樣做。

我們可以將存放庫插入 *控制器來解決* 這些問題。 首先，將 `ProductRepository` 類別重構為介面：

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

然後提供作為函式 `IProductRepository` 參數：

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

此範例會使用函式 [插入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)。 您也可以使用 *setter 插入*，也就是透過 setter 方法或屬性來設定相依性。

但現在有問題，因為您的應用程式不會直接建立控制器。 Web API 會在路由要求時建立控制器，而 Web API 不會知道任何相關資訊 `IProductRepository` 。 這就是 Web API 相依性解析程式的來源。

## <a name="the-web-api-dependency-resolver"></a>Web API 相依性解析程式

Web API 會定義用來解析相依性的 **IDependencyResolver** 介面。 以下是介面的定義：

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

**IDependencyScope**介面有兩種方法：

- **GetService** 會建立一個類型的實例。
- **GetServices** 會建立指定之類型的物件集合。

**IDependencyResolver**方法會繼承**IDependencyScope**並加入**BeginScope**方法。 我稍後會在本教學課程中討論範圍。

當 Web API 建立控制器實例時，它會先呼叫 **IDependencyResolver GetService**，並傳入控制器型別。 您可以使用這個擴充性攔截來建立控制器，並解析任何相依性。 如果 **GetService** 傳回 Null，Web API 會在控制器類別上尋找無參數的函式。

## <a name="dependency-resolution-with-the-unity-container"></a>Unity 容器的相依性解析

雖然您可以從頭開始撰寫完整的 **IDependencyResolver** 程式，但介面實際上是設計來作為 Web API 和現有 IoC 容器之間的橋樑。

IoC 容器是負責管理相依性的軟體元件。 您會向容器註冊類型，然後使用容器來建立物件。 容器會自動找出相依性關係。 許多 IoC 容器也可讓您控制物件存留期和範圍等專案。

> [!NOTE]
> 「IoC」代表「控制反轉」，這是架構呼叫應用程式程式碼的一般模式。 IoC 容器會為您建立物件，這會「反轉」常用的控制流程。

在本教學課程中，我們將使用來自 Microsoft 模式實務的 [Unity](https://msdn.microsoft.com/library/ff647202.aspx) &amp; 。  (其他熱門程式庫，包括 [Castle Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Ninject](http://www.ninject.org/)和 [StructureMap](http://structuremap.github.io/documentation/)。 ) 您可以使用 NuGet 封裝管理員來安裝 Unity。 從 Visual Studio 的 [ **工具** ] 功能表中，選取 [ **NuGet 封裝管理員**]，然後選取 [ **封裝管理員主控台**]。 在封裝管理員主控台] 視窗中，輸入下列命令：

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

以下是包裝 Unity 容器的 **IDependencyResolver** 執行。

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

## <a name="configuring-the-dependency-resolver"></a>設定相依性解析程式

針對 global **HttpConfiguration**物件的**DependencyResolver**屬性設定相依性解析程式。

下列程式碼會 `IProductRepository` 向 Unity 註冊介面，然後建立 `UnityResolver` 。

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a>相依性範圍和控制器存留期

每個要求都會建立控制器。 為了管理物件存留期， **IDependencyResolver** 會使用 *範圍*的概念。

附加至 **HttpConfiguration** 物件的相依性解析程式具有全域範圍。 當 Web API 建立控制器時，它會呼叫 **BeginScope**。 這個方法會傳回代表子範圍的 **IDependencyScope** 。

然後，Web API 會在子範圍上呼叫 **GetService** 來建立控制器。 當要求完成時，Web API 會在子範圍上呼叫 **Dispose** 。 使用 **dispose** 方法來處置控制器的相依性。

您如何執行 **BeginScope** 取決於 IoC 容器。 針對 Unity，範圍會對應至子容器：

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

大部分 IoC 容器都有類似的對等專案。
