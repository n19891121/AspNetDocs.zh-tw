---
uid: web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
title: 在 ASP.NET 4.5 中使用非同步方法 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將教您如何使用 Visual Studio Express 2012 for Web （這是免費的）來建立異步 ASP.NET Web Forms 應用程式的基本概念 .。。
ms.author: riande
ms.date: 01/02/2019
ms.assetid: a585c9a2-7c8e-478b-9706-90f3739c50d1
msc.legacyurl: /web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: a0aed792c5a2e790eed10c1aecf84fe5e535cea4
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045152"
---
# <a name="using-asynchronous-methods-in-aspnet-45"></a>使用 ASP.NET 4.5 中的非同步方法

依 [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教學課程將教您如何使用 [Visual Studio Express 2012 For Web](https://www.microsoft.com/visualstudio/11)建立異步 ASP.NET Web Forms 應用程式的基本概念，這是免費的 Microsoft Visual Studio 版本。 您也可以使用 [Visual Studio 2012](https://www.microsoft.com/visualstudio/11)。 本教學課程包含下列各節。
> 
> - [執行緒集區處理要求的方式](#HowRequestsProcessedByTP)
> - [選擇同步或非同步方法](#ChoosingSyncVasync)
> - [範例應用程式](#SampleApp)
> - [Gizmos 同步頁面](#GizmosSynch)
> - [建立異步 Gizmos 頁面](#CreatingAsynchGizmos)
> - [同時執行多個作業](#Parallel)
> - [使用解除標記](#CancelToken)
> - [高平行存取/高延遲 Web 服務呼叫的伺服器設定](#ServerConfig)
> 
> 本教學課程會提供完整的範例，網址為：  
> [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/) 在 [GitHub](https://github.com/) 網站上。

ASP.NET 4.5 中結合 [.net 4.5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx) 的網頁，可讓您註冊傳回 [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)型別物件的非同步方法。 .NET Framework 4 引進 [了一個稱為工作的](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 非同步程式設計概念，ASP.NET 4.5 [則支援工作](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)。 工作會以[工作命名空間](https://msdn.microsoft.com/library/system.threading.tasks.aspx)中**的工作類型**和相關類型來表示。 .NET Framework 4.5 是以使用 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 和 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 關鍵字的非同步支援為基礎，而這些關鍵字的處理 [工作物件比](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 先前的非同步方法更簡單。 [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)關鍵字是語法速記，表示某段程式碼應該以非同步方式等候其他部分的程式碼。 [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx)關鍵字代表一個提示，可讓您用來將方法標示為以工作為基礎的非同步方法。 **Await**、 **async**和**Task**物件的組合可讓您更輕鬆地在 .net 4.5 中撰寫非同步程式碼。 非同步方法的新模型稱為以工作為 *基礎的非同步模式* (**點擊**) 。 本教學課程假設您已熟悉使用 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 和 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 關鍵字 [和工作命名空間的非同步](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 程式設計。

如需有關使用 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 和 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 關鍵字和 [工作命名空間的詳細](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 資訊，請參閱下列參考。

- [白皮書： .NET 中的非同步](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Async/Await 常見問題](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Visual Studio 非同步程式設計](https://msdn.microsoft.com/vstudio/gg316360)

## <a name="how-requests-are-processed-by-the-thread-pool"></a><a id="HowRequestsProcessedByTP"></a>  執行緒集區處理要求的方式

在 web 伺服器上，.NET Framework 會維護用來服務 ASP.NET 要求的執行緒集區。 要求到達網頁伺服器時，集區中會分派一個執行緒來處理該要求。 如果要求是以同步方式處理，處理要求的執行緒在處理要求時就會忙碌，而且該執行緒無法服務另一個要求。   
  
這可能不會造成問題，因為執行緒集區的大小足以容納許多忙碌的執行緒。 不過，執行緒集區中的執行緒數目有限 (.NET 4.5 的預設最大值是 5000) 。 在具有高並行處理長時間執行之要求的大型應用程式中，所有可用的執行緒可能都會忙碌。 這種狀況稱為「執行緒耗盡」(Thread Starvation)。 當達到這個條件時，web 伺服器會將要求排到佇列。 如果要求佇列已滿，則網頁伺服器會拒絕 HTTP 503 狀態的要求， (伺服器太忙碌) 。 CLR 執行緒集區具有新執行緒插入的限制。 如果並行暴增 (也就是，您的網站可能會突然得到大量的要求) 而且所有可用的要求執行緒都會因為具有高延遲的後端呼叫而忙碌，因此受限的執行緒插入速率可能會讓您的應用程式回應速度很差。 此外，新增至執行緒集區的每個新執行緒都有額外負荷 (例如 1 MB 的堆疊記憶體) 。 使用同步方法來服務高延遲呼叫的 web 應用程式，其中線程集區成長至 .NET 4.5 預設值最多5個，000個執行緒耗用的記憶體大約是 5 GB，而應用程式可使用非同步方法和只有50個執行緒來處理相同的要求。 當您在執行非同步工作時，不一定會使用執行緒。 例如，當您建立異步 web 服務要求時，ASP.NET 不會在 **async** 方法呼叫與 **await**之間使用任何執行緒。 使用執行緒集區來服務具有高延遲的要求，可能會導致大型的記憶體使用量和伺服器硬體的使用率不佳。

## <a name="processing-asynchronous-requests"></a>處理非同步要求

在啟動時看到大量並行要求的 web 應用程式中，或有暴增負載 (在並行增加) 的情況下，讓 web 服務呼叫非同步會提高應用程式的回應能力。 非同步要求所需的處理時間與同步要求相同。 例如，如果要求提出需要兩秒才能完成的 web 服務呼叫，則要求會花費兩秒鐘的時間，不論是以同步或非同步方式執行。 不過，在非同步呼叫期間，執行緒在等候第一個要求完成時，不會遭到封鎖而無法回應其他要求。 因此，當有許多並行要求叫用長時間執行的作業時，非同步要求會防止要求佇列和執行緒集區的成長。

## <a name="choosing-synchronous-or-asynchronous-methods"></a><a id="ChoosingSyncVasync"></a>  選擇同步或非同步方法

本節列出何時使用同步或非同步方法的指導方針。 這些只是指導方針;個別檢查每個應用程式，以判斷非同步方法是否有助於效能。

一般情況下，請在下列情況下使用同步方法：

- 作業很簡單或執行時間短暫。
- 簡潔比效率重要。
- 作業主要都是 CPU 作業，而非需要耗用大量磁碟或網路的作業。 在 CPU 系結作業上使用非同步方法不會提供任何好處，而且會產生更多的額外負荷。

一般情況下，請使用非同步方法來進行下列條件：

- 您正在呼叫可透過非同步方法取用的服務，而您使用的是 .NET 4.5 或更新版本。
- 作業受限於網路或 I/O，而非 CPU。
- 平行處理比簡化程式碼重要。
- 您想提供可讓使用者取消長期執行要求的機制。
- 當切換執行緒的優點超過內容切換的成本時。 一般而言，如果同步方法在不執行任何工作時封鎖 ASP.NET 要求執行緒，您應該將方法設為非同步。 藉由讓呼叫變成非同步，ASP.NET 要求執行緒在等候 web 服務要求完成時，不會遭到封鎖而無法執行任何工作。
- 測試顯示封鎖作業是網站效能的瓶頸，而且 IIS 可以針對這些封鎖呼叫使用非同步方法來服務更多要求。

  可下載的範例會示範如何有效地使用非同步方法。 提供的範例是設計來提供 ASP.NET 4.5 中非同步程式設計的簡單示範。 此範例不適合作為 ASP.NET 中非同步程式設計的參考架構。 範例程式會呼叫 [ASP.NET Web API](../../../web-api/index.md) 的方法，而此方法會接著呼叫工作 [。延遲](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) 以模擬長時間執行的 Web 服務呼叫。 大部分的實際執行應用程式都不會顯示使用非同步方法的明顯優勢。   
  
少數應用程式需要所有的方法都是非同步。 通常，將數個同步方法轉換為非同步方法，可為所需的工作量提供最佳的效率。

## <a name="the-sample-application"></a><a id="SampleApp"></a>  範例應用程式

您可以從 GitHub 網站下載範例應用程式 [https://github.com/RickAndMSFT/Async-ASP.NET](https://github.com/RickAndMSFT/Async-ASP.NET) 。 [GitHub](https://github.com/) 存放庫包含三個專案：

- *WebAppAsync*：使用 Web API **WebAPIpwg** 服務的 ASP.NET Web Forms 專案。 本教學課程的大部分程式碼都是來自這個專案。
- *WebAPIpgw*：用來執行控制器的 ASP.NET MVC 4 Web API 專案 `Products, Gizmos and Widgets` 。 它會提供 *WebAppAsync* 專案和 *Mvc4Async* 專案的資料。
- *Mvc4Async*：包含其他教學課程中所使用之程式碼的 ASP.NET MVC 4 專案。 它會對 **WebAPIpwg** 服務進行 Web API 呼叫。

## <a name="the-gizmos-synchronous-page"></a><a id="GizmosSynch"></a>  Gizmos 同步頁面

 下列程式碼顯示 `Page_Load` 用來顯示 gizmos 清單的同步方法。  (本文中的 gizmo 是虛構機械裝置。 )  

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample1.cs)]

下列程式碼顯示 `GetGizmos` gizmo 服務的方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample2.cs)]

方法會將 `GizmoService GetGizmos` URI 傳遞至 ASP.NET WEB API HTTP 服務，此服務會傳回 gizmos 資料的清單。 *WebAPIpgw*專案包含 Web API `gizmos, widget` 和控制器的執行 `product` 。  
下圖顯示範例專案中的 [gizmos] 頁面。

![Gizmos](using-asynchronous-methods-in-aspnet-45/_static/image1.png)

## <a name="creating-an-asynchronous-gizmos-page"></a><a id="CreatingAsynchGizmos"></a>  建立異步 Gizmos 頁面

此範例使用 .NET 4.5 中提供的新 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 和 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 關鍵字 (以及 Visual Studio 2012) ，讓編譯器負責維護非同步程式設計所需的複雜轉換。 編譯器可讓您使用 c # 的同步控制流程結構來撰寫程式碼，而編譯器會自動套用使用回呼所需的轉換，以避免封鎖執行緒。

ASP.NET 非同步頁面必須包含將[Page](https://msdn.microsoft.com/library/ydy4x04a.aspx) `Async` 屬性設為 "True" 的 Page 指示詞。 下列程式碼顯示[Page](https://msdn.microsoft.com/library/ydy4x04a.aspx) `Async` *GizmosAsync .aspx*頁面的屬性（attribute）設定為 "true" 的頁面指示詞。

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample3.aspx?highlight=1)]

下列程式碼顯示 `Gizmos` 同步 `Page_Load` 方法和 `GizmosAsync` 非同步網頁。 如果您的瀏覽器支援 [HTML 5 &lt; mark &gt; 元素](http://www.w3.org/wiki/HTML/Elements/mark)，您將會在 `GizmosAsync` 黃色醒目提示中看到變更。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample4.cs)]

非同步版本：

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample5.cs?highlight=3,6-7,9,11)]

 已套用下列變更，以允許 `GizmosAsync` 頁面為非同步。

- [Page](https://msdn.microsoft.com/library/ydy4x04a.aspx)指示詞必須將 `Async` 屬性設定為 "true"。
- `RegisterAsyncTask`方法是用來註冊非同步工作，其中包含以非同步方式執行的程式碼。
- 新 `GetGizmosSvcAsync` 方法會以 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 關鍵字標示，此關鍵字會告訴編譯器為主體的部分產生回呼，以及自動建立 `Task` 傳回的。
- &quot;&quot;非同步方法名稱已附加 Async。 不需要附加 "Async"，但這是撰寫非同步方法時的慣例。
- 新方法的傳回型別 `GetGizmosSvcAsync` 為 `Task` 。 的傳回型別 `Task` 代表進行中的工作，並提供方法的呼叫端，以及用來等候非同步作業完成的控制碼。
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)關鍵字已套用至 web 服務呼叫。
-  () 呼叫非同步 web 服務 API `GetGizmosAsync` 。

在 `GetGizmosSvcAsync` 方法主體內，會呼叫另一個非同步方法 `GetGizmosAsync` 。 `GetGizmosAsync` 立即傳回 `Task<List<Gizmo>>` ，當資料可供使用時，最終將會完成。 因為您不想要在擁有 gizmo 資料之前進行任何其他動作，程式碼會使用 **await** 關鍵字) 來等候工作 (。 您只能在以**async**關鍵字標注的方法中使用**await**關鍵字。

**Await**關鍵字不會封鎖執行緒，直到工作完成為止。 它會將方法的其餘部分註冊為工作的回呼，並立即傳回。 當等候的工作最後完成時，它會叫用該回呼，進而繼續執行該方法，並將它從左至右開始。 如需使用 [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) 和 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 關鍵字和 [工作命名空間的詳細](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) 資訊，請參閱 [非同步參考](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async)。

下列程式碼顯示 `GetGizmos` 和 `GetGizmosAsync` 方法。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample6.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample7.cs?highlight=1,4-8)]

 非同步變更類似于上述 **GizmosAsync** 所做的變更。 

- 方法簽章以 [async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) 關鍵字標注、傳回型別已變更為 `Task<List<Gizmo>>` ，而且 *async* 已附加至方法名稱。
- 使用非同步 [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) 類別，而不是同步 [WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx) 類別。
- [Await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx)關鍵字已套用至[HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)[GetAsync](https://msdn.microsoft.com/library/hh158944(VS.110).aspx)非同步方法。

下圖顯示非同步 gizmo 視圖。

![async](using-asynchronous-methods-in-aspnet-45/_static/image2.png)

Gizmos 資料的瀏覽器呈現與同步呼叫所建立的視圖相同。 唯一的差別是，非同步版本在繁重的負載下可能更具效能。

## <a name="registerasynctask-notes"></a>RegisterAsyncTask 注意事項

與搭配使用的方法， `RegisterAsyncTask` 將會在 [呈現](https://msdn.microsoft.com/library/ms178472.aspx)後立即執行。

如果您直接使用 async void 頁面事件，如下列程式碼所示：

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample8.cs)]

您不再擁有事件執行的完整控制權。 例如，如果是 .aspx 和。Master 定義 `Page_Load` 事件，其中之一或兩者都是非同步，因此無法保證執行的順序。 事件處理常式的相同不定順序 (例如 `async void Button_Click` ) 適用。

## <a name="performing-multiple-operations-in-parallel"></a><a id="Parallel"></a>  平行執行多個作業

當動作必須執行數個獨立的作業時，非同步方法會有相當大的優勢，而不是同步方法。 在提供的範例中，[產品]、[widget] 和 [) Gizmos] 的 [同步] 頁面 *PWG* (會顯示三個 web 服務呼叫的結果，以取得產品、widget 和 Gizmos 的清單。 提供這些服務的 [ASP.NET Web API](../../../web-api/index.md) 專案使用工作 [延遲](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) ，以模擬延遲或慢速網路呼叫。 當延遲設定為500毫秒時，非同步 *PWGasync .aspx* 頁面會需要超過500毫秒才能完成，而同步 `PWG` 版本則需要超過1500毫秒。 同步 *PWG .aspx* 頁面會顯示在下列程式碼中。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample9.cs)]

非同步 `PWGasync` 程式碼後向如下所示。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample10.cs?highlight=5,11,21)]

下圖顯示從非同步 *PWGasync .aspx* 頁面傳回的視圖。

![](using-asynchronous-methods-in-aspnet-45/_static/image3.png)

## <a name="using-a-cancellation-token"></a><a id="CancelToken"></a>  使用解除標記

傳回的非同步方法 `Task` 是可取消的，也就是當使用 Page 指示詞的屬性提供一個參數時，它們會採用[CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx)參數 `AsyncTimeout` 。 [Page](https://msdn.microsoft.com/library/ydy4x04a.aspx) 下列程式碼會顯示 GizmosCancelAsync 為秒的 *.aspx* 頁面。

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample11.aspx?highlight=1)]

下列程式碼顯示 *GizmosCancelAsync.aspx.cs* 檔案。

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample12.cs?highlight=6,9)]

在提供的範例應用程式中，選取 *GizmosCancelAsync* 連結會呼叫 *GizmosCancelAsync .aspx* 頁面，並藉由) 非同步呼叫來示範取消 (。 由於延遲時間是在隨機範圍內，因此您可能需要將頁面重新整理幾次，以取得逾時錯誤訊息。

## <a name="server-configuration-for-high-concurrencyhigh-latency-web-service-calls"></a><a id="ServerConfig"></a>  高平行存取/高延遲 Web 服務呼叫的伺服器設定

若要實現非同步 web 應用程式的優點，您可能需要對預設伺服器設定進行一些變更。 設定和測試非同步 web 應用程式的壓力時，請記住下列事項。

- Windows 7、Windows Vista、Window 8 和所有 Windows 用戶端作業系統最多可有10個並行要求。 您將需要 Windows Server 作業系統，才能在高負載下查看非同步方法的優點。
- 使用下列命令，從提升許可權的命令提示字元向 IIS 註冊 .NET 4.5：  
  %windir%\Microsoft.NET\Framework64 \v4.0.30319\aspnet \_ regiis-i  
  請參閱    [ASP.NET IIS 註冊工具 (Aspnet \_regiis.exe) ](https://msdn.microsoft.com/library/k6h9cz8h.aspx)
- 您可能需要將 [HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) 的佇列限制從預設值1000增加至5000。 如果設定太低，您可能會看到 [HTTP.sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) 拒絕 HTTP 503 狀態的要求。 若要變更 HTTP.sys 佇列限制：

    - 開啟 [IIS 管理員] 並流覽至 [應用程式集區] 窗格。
    - 以滑鼠右鍵按一下目標應用程式集區，然後選取 [ **Advanced Settings**]。  
        ![先進](using-asynchronous-methods-in-aspnet-45/_static/image4.png)
    - 在 [ **Advanced Settings** ] 對話方塊中，將 *佇列長度* 從1000變更為5000。  
        ![佇列長度](using-asynchronous-methods-in-aspnet-45/_static/image5.png)  
  
  請注意，在上圖中，即使應用程式集區使用 .NET 4.5，.NET framework 也會列為 v 4.0。 若要瞭解這項差異，請參閱下列各項：

- [.NET 版本設定和多目標-.NET 4.5 是 .NET 4.0 的就地升級](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
- [如何將 IIS 應用程式或 AppPool 設定為使用 ASP.NET 3.5 而非2。0](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
- [.NET Framework 版本和相依性](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)

- 如果您的應用程式使用 web 服務或 System.NET 透過 HTTP 與後端通訊，您可能需要增加 [connectionManagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx) 元素。 針對 ASP.NET 應用程式，這會受限於 Cpu 數目12倍的自動設定功能。 這表示在四個程式上，您最多可以有 12 \* 個 4 = 48 個與 IP 端點的並行連接。 因為這會系結[至](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx)自動設定，所以在 ASP.NET 應用程式中增加的最簡單方式， `maxconnection` 就是在 global.asax 檔案的 from 方法中，以程式設計的方式設定[ServicePointManager. >servicepointmanager.defaultconnectionlimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) 。 `Application_Start` *global.asax* 如需範例，請參閱範例下載。
- 在 .NET 4.5 中， [MaxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx) 的預設值是5000。

## <a name="contributors"></a>參與者

- [于 levi Broderick](http://stackoverflow.com/users/59641/levi)
- [Tom Dykstra](http://www.bing.com/search?q=site%3Aasp.net+%22Tom+Dykstra%22+-forums.asp.net&amp;qs=n&amp;form=QBRE&amp;pq=site%3Aasp.net+%22tom+dykstra%22+-forums.asp.net&amp;sc=8-42&amp;sp=-1&amp;sk=)
- [Brad Wilson](http://bradwilson.typepad.com/)
- [HongMei Ge](https://blogs.msdn.com/b/hongmeig/)
