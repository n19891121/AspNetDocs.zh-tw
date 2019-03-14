---
ms.openlocfilehash: 976cc58dfcd9bba0b88ddd5d0d886cbb99b418ae
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57026315"
---
# <a name="response-compression-sample-application-aspnet-core-2x"></a><span data-ttu-id="2325c-101">回應壓縮範例應用程式 (ASP.NET Core 2.x)</span><span class="sxs-lookup"><span data-stu-id="2325c-101">Response compression sample application (ASP.NET Core 2.x)</span></span>

<span data-ttu-id="2325c-102">此範例說明如何使用 ASP.NET Core 2.x 壓縮 HTTP 回應的回應壓縮中介軟體。</span><span class="sxs-lookup"><span data-stu-id="2325c-102">This sample illustrates the use of ASP.NET Core 2.x Response Compression Middleware to compress HTTP responses.</span></span> <span data-ttu-id="2325c-103">此範例示範 Gzip、 Brotli 和自訂壓縮提供者的文字和影像的回應，並示範如何加入壓縮的 MIME 類型。</span><span class="sxs-lookup"><span data-stu-id="2325c-103">The sample demonstrates Gzip, Brotli, and custom compression providers for text and image responses and shows how to add a MIME type for compression.</span></span> <span data-ttu-id="2325c-104">如需 ASP.NET Core 1.x 範例，請參閱[回應壓縮範例應用程式 (ASP.NET Core 1.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples/1.x)。</span><span class="sxs-lookup"><span data-stu-id="2325c-104">For the ASP.NET Core 1.x sample, see [Response compression sample application (ASP.NET Core 1.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/response-compression/samples/1.x).</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="2325c-105">這個範例中的範例</span><span class="sxs-lookup"><span data-stu-id="2325c-105">Examples in this sample</span></span>

* `BrotliCompressionProvider`
  * `text/plain`
    * <span data-ttu-id="2325c-106">**/** -Lorem Ipsum 文字檔案回應為 2,044 個位元組壓縮為 ~ 979 個位元組。</span><span class="sxs-lookup"><span data-stu-id="2325c-106">**/** - Lorem Ipsum text file response at 2,044 bytes that compresses to ~979 bytes.</span></span>
    * <span data-ttu-id="2325c-107">**/testfile1kb.txt** -1,033 位元組在文字檔案回應，會壓縮為 ~ 36 個位元組。</span><span class="sxs-lookup"><span data-stu-id="2325c-107">**/testfile1kb.txt** - Text file response at 1,033 bytes that compresses to ~36 bytes.</span></span>
    * <span data-ttu-id="2325c-108">**/ 緩慢**-在 1 秒的間隔發出為單一字元的回應。</span><span class="sxs-lookup"><span data-stu-id="2325c-108">**/trickle** - Response issued as single characters at 1 second intervals.</span></span>
* `GzipCompressionProvider`
  * `text/plain`
    * <span data-ttu-id="2325c-109">**/** -Lorem Ipsum 文字檔案回應為 2,044 個位元組壓縮為 ~ 927 個位元組。</span><span class="sxs-lookup"><span data-stu-id="2325c-109">**/** - Lorem Ipsum text file response at 2,044 bytes that compresses to ~927 bytes.</span></span>
    * <span data-ttu-id="2325c-110">**/testfile1kb.txt** -1,033 位元組在文字檔案回應，會壓縮為 ~ 47 個位元組。</span><span class="sxs-lookup"><span data-stu-id="2325c-110">**/testfile1kb.txt** - Text file response at 1,033 bytes that compresses to ~47 bytes.</span></span>
    * <span data-ttu-id="2325c-111">**/ 緩慢**-在 1 秒的間隔發出為單一字元的回應。</span><span class="sxs-lookup"><span data-stu-id="2325c-111">**/trickle** - Response issued as single characters at 1 second intervals.</span></span>
  * `image/svg+xml`
    * <span data-ttu-id="2325c-112">**/banner.svg** -可縮放向量圖形 (SVG) 映像回應 9,707 位元組可壓縮為 ~ 4,459 個位元組。</span><span class="sxs-lookup"><span data-stu-id="2325c-112">**/banner.svg** - A Scalable Vector Graphics (SVG) image response at 9,707 bytes that compresses to ~4,459 bytes.</span></span>
* `CustomCompressionProvider`<br><span data-ttu-id="2325c-113">示範如何實作與中介軟體搭配使用自訂壓縮提供者。</span><span class="sxs-lookup"><span data-stu-id="2325c-113">Shows how to implement a custom compression provider for use with the middleware.</span></span>

<span data-ttu-id="2325c-114">當要求包含`Accept-Encoding`標頭和回應的壓縮是成功中, 介軟體會自動將新增`Vary: Accept-Encoding`標頭至回應。</span><span class="sxs-lookup"><span data-stu-id="2325c-114">When the request includes the `Accept-Encoding` header and response compression is successful, the middleware automatically adds a `Vary: Accept-Encoding` header to the response.</span></span> <span data-ttu-id="2325c-115">`Vary`標頭會指示來維護多份的替代值為基礎的回應的快取`Accept-Encoding`，因此這兩個壓縮 （Gzip 或 Brotli） 和未壓縮的版本儲存在快取中的系統，可以接受壓縮或未壓縮的回應。</span><span class="sxs-lookup"><span data-stu-id="2325c-115">The `Vary` header instructs caches to maintain multiple copies of the response based on alternative values of `Accept-Encoding`, so both a compressed (Gzip or Brotli) and uncompressed version are stored in caches for systems that can either accept the compressed or the uncompressed response.</span></span>

## <a name="use-the-sample"></a><span data-ttu-id="2325c-116">使用範例</span><span class="sxs-lookup"><span data-stu-id="2325c-116">Use the sample</span></span>

1. <span data-ttu-id="2325c-117">請要求，使用[Fiddler](http://www.telerik.com/fiddler)， [Firebug](http://getfirebug.com/)，或[Postman](https://www.getpostman.com/)應用程式，而不需要`Accept-Encoding`標頭，並記下回應承載，回應大小和回應標頭。</span><span class="sxs-lookup"><span data-stu-id="2325c-117">Make a request using [Fiddler](http://www.telerik.com/fiddler), [Firebug](http://getfirebug.com/), or [Postman](https://www.getpostman.com/) to the application without an `Accept-Encoding` header and note the response payload, response size, and response headers.</span></span>
1. <span data-ttu-id="2325c-118">新增`Accept-Encoding: br`或`Accept-Encoding: gzip`標頭，並記下 壓縮的回應大小和回應標頭。</span><span class="sxs-lookup"><span data-stu-id="2325c-118">Add an `Accept-Encoding: br` or `Accept-Encoding: gzip` header and note the compressed response size and response headers.</span></span> <span data-ttu-id="2325c-119">回應大小會卸除，而`Content-Encoding`指出該以任一 Gzip 壓縮中介軟體會包含回應標頭或 Brotli 發生。</span><span class="sxs-lookup"><span data-stu-id="2325c-119">The response size drops, and the `Content-Encoding` response header is included by the middleware indicating that compression with either Gzip or Brotli occurred.</span></span> <span data-ttu-id="2325c-120">當您查看回應內文 Lorem Ipsum 或**testfile1kb.txt**回應，您會看到文字是壓縮的而且無法讀取。</span><span class="sxs-lookup"><span data-stu-id="2325c-120">When you look at the response body for the Lorem Ipsum or **testfile1kb.txt** response, you see that the text is compressed and unreadable.</span></span>
1. <span data-ttu-id="2325c-121">新增`Accept-Encoding: mycustomcompression`標頭，並記下回應標頭。</span><span class="sxs-lookup"><span data-stu-id="2325c-121">Add an `Accept-Encoding: mycustomcompression` header and note the response headers.</span></span> <span data-ttu-id="2325c-122">`CustomCompressionProvider`是空的實作，並不實際壓縮回應，但您可以建立自訂的壓縮資料流包裝函式`CreateStream()`方法。</span><span class="sxs-lookup"><span data-stu-id="2325c-122">The `CustomCompressionProvider` is an empty implementation that doesn't actually compress the response, but you can create a custom compression stream wrapper for the `CreateStream()` method.</span></span>
