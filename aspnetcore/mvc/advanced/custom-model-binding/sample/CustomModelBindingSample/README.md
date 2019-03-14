---
ms.openlocfilehash: 71a40fcab8f1d1005cbe9327d01a42484765a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57059635"
---
# <a name="custom-model-binding-demo"></a><span data-ttu-id="7d2ad-101">自訂模型繫結示範</span><span class="sxs-lookup"><span data-stu-id="7d2ad-101">Custom Model Binding Demo</span></span>

<span data-ttu-id="7d2ad-102">執行應用程式，並將 base64 編碼的字串張貼到`ImageController`端點 (`/api/image/`)，以測試 `ByteArrayModelBinder`。</span><span class="sxs-lookup"><span data-stu-id="7d2ad-102">Test `ByteArrayModelBinder` by running the app and POSTing a base64-encoded string to the `ImageController` endpoint (`/api/image/`).</span></span> <span data-ttu-id="7d2ad-103">請在要求主體中指定檔案與檔案名稱屬性作為表單資料 (使用 [Postman](https://www.getpostman.com/) 或類似的工具)。</span><span class="sxs-lookup"><span data-stu-id="7d2ad-103">Specify the file and filename properties in the request body as form-data (using [Postman](https://www.getpostman.com/) or a similar tool).</span></span> <span data-ttu-id="7d2ad-104">您可以使用[此範例字串](Base64String.txt)。</span><span class="sxs-lookup"><span data-stu-id="7d2ad-104">You can use [this sample string](Base64String.txt).</span></span> <span data-ttu-id="7d2ad-105">結果會以您指定的檔案名稱儲存在 *wwwroot/images/upload* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="7d2ad-105">The result is saved in the *wwwroot/images/upload* folder with the filename specified.</span></span>

<span data-ttu-id="7d2ad-106">若要測試自訂繫結的範例，請嘗試下列端點：</span><span class="sxs-lookup"><span data-stu-id="7d2ad-106">To test the custom binding example, try the following endpoints:</span></span>

* <span data-ttu-id="7d2ad-107">/api/authors/1</span><span class="sxs-lookup"><span data-stu-id="7d2ad-107">/api/authors/1</span></span>
* <span data-ttu-id="7d2ad-108">/api/authors/2 (找不到)</span><span class="sxs-lookup"><span data-stu-id="7d2ad-108">/api/authors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="7d2ad-109">/api/boundauthors/1</span><span class="sxs-lookup"><span data-stu-id="7d2ad-109">/api/boundauthors/1</span></span>
* <span data-ttu-id="7d2ad-110">/api/boundauthors/2 (找不到)</span><span class="sxs-lookup"><span data-stu-id="7d2ad-110">/api/boundauthors/2 (NOT FOUND)</span></span>
* <span data-ttu-id="7d2ad-111">/api/boundauthors/get/1</span><span class="sxs-lookup"><span data-stu-id="7d2ad-111">/api/boundauthors/get/1</span></span>
* <span data-ttu-id="7d2ad-112">/api/boundauthors/get/2 (NO CONTENT) &ndash; 此動作不會檢查 null，並會傳回 *404 找不到*。</span><span class="sxs-lookup"><span data-stu-id="7d2ad-112">/api/boundauthors/get/2 (NO CONTENT) &ndash; This action doesn't check for null and returns a *404 Not Found*.</span></span>
