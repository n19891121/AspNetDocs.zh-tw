---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 資料來源控制項 |Microsoft Docs
author: microsoft
description: DataGrid 控制項在 ASP.NET 1.x 標示為 Web 應用程式中的資料存取的一大進步。 不過，它不是易於使用，可能是...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: ba00024e93beba6eab226dd0d381d8734061e095
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038875"
---
<a name="data-source-controls"></a><span data-ttu-id="64b7d-104">資料來源控制項</span><span class="sxs-lookup"><span data-stu-id="64b7d-104">Data Source Controls</span></span>
====================
<span data-ttu-id="64b7d-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="64b7d-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="64b7d-106">DataGrid 控制項在 ASP.NET 1.x 標示為 Web 應用程式中的資料存取的一大進步。</span><span class="sxs-lookup"><span data-stu-id="64b7d-106">The DataGrid control in ASP.NET 1.x marked a great improvement in data access in Web applications.</span></span> <span data-ttu-id="64b7d-107">不過，它不是因為可能是使用者的易記。</span><span class="sxs-lookup"><span data-stu-id="64b7d-107">However, it wasn't as user-friendly as it could have been.</span></span> <span data-ttu-id="64b7d-108">此外，它仍會需要相當多的程式碼，以從它取得太多有用的功能。</span><span class="sxs-lookup"><span data-stu-id="64b7d-108">It still required a considerable amount of code to obtain much useful functionality from it.</span></span> <span data-ttu-id="64b7d-109">滿足下列條件是所有資料存取工作領域能夠一路順風 1.x 中的模型。</span><span class="sxs-lookup"><span data-stu-id="64b7d-109">Such is the model in all data access endeavors in 1.x.</span></span>


<span data-ttu-id="64b7d-110">DataGrid 控制項在 ASP.NET 1.x 標示為 Web 應用程式中的資料存取的一大進步。</span><span class="sxs-lookup"><span data-stu-id="64b7d-110">The DataGrid control in ASP.NET 1.x marked a great improvement in data access in Web applications.</span></span> <span data-ttu-id="64b7d-111">不過，它不是因為可能是使用者的易記。</span><span class="sxs-lookup"><span data-stu-id="64b7d-111">However, it wasn't as user-friendly as it could have been.</span></span> <span data-ttu-id="64b7d-112">此外，它仍會需要相當多的程式碼，以從它取得太多有用的功能。</span><span class="sxs-lookup"><span data-stu-id="64b7d-112">It still required a considerable amount of code to obtain much useful functionality from it.</span></span> <span data-ttu-id="64b7d-113">滿足下列條件是所有資料存取工作領域能夠一路順風 1.x 中的模型。</span><span class="sxs-lookup"><span data-stu-id="64b7d-113">Such is the model in all data access endeavors in 1.x.</span></span>

<span data-ttu-id="64b7d-114">ASP.NET 2.0 可應付此部分資料來源控制項。</span><span class="sxs-lookup"><span data-stu-id="64b7d-114">ASP.NET 2.0 addresses this with in part with data source controls.</span></span> <span data-ttu-id="64b7d-115">在 ASP.NET 2.0 中的資料來源控制項提供開發人員宣告式模型來擷取資料，顯示資料，並編輯資料。</span><span class="sxs-lookup"><span data-stu-id="64b7d-115">The data source controls in ASP.NET 2.0 provide developers with a declarative model for retrieving data, displaying data, and editing data.</span></span> <span data-ttu-id="64b7d-116">資料來源控制項的用途是提供一致的這些資料來源無關的資料繫結控制項的資料表示法。</span><span class="sxs-lookup"><span data-stu-id="64b7d-116">The purpose of data source controls is to provide a consistent representation of data to data-bound controls regardless of the source of those data.</span></span> <span data-ttu-id="64b7d-117">在 ASP.NET 2.0 中的資料來源控制項的核心是 DataSourceControl 抽象類別。</span><span class="sxs-lookup"><span data-stu-id="64b7d-117">At the heart of the data source controls in ASP.NET 2.0 is the DataSourceControl abstract class.</span></span> <span data-ttu-id="64b7d-118">DataSourceControl 類別提供基底實作 IDataSource 介面和 IListSource 介面，後者可讓您指派為資料繫結控制項 （透過新的 [DataSourceId] 屬性的資料來源的資料來源控制項稍後討論），並公開資料投影為清單。</span><span class="sxs-lookup"><span data-stu-id="64b7d-118">The DataSourceControl class provides a base implementation of the IDataSource interface and the IListSource interface, the latter of which allows you to assign the data source control as the DataSource of a data-bound control (via the new DataSourceId property discussed later) and expose the data therein as a list.</span></span> <span data-ttu-id="64b7d-119">每個資料來源控制項的資料清單會公開為 DataSourceView 物件。</span><span class="sxs-lookup"><span data-stu-id="64b7d-119">Each list of data from a data source control is exposed as a DataSourceView object.</span></span> <span data-ttu-id="64b7d-120">DataSourceView 執行個體的存取是 IDataSource 介面所提供。</span><span class="sxs-lookup"><span data-stu-id="64b7d-120">Access to the DataSourceView instances is provided by the IDataSource interface.</span></span> <span data-ttu-id="64b7d-121">比方說，GetViewNames 方法會傳回相關聯的特定資料來源控制項，可讓您列舉 DataSourceViews ICollection 和 GetView 方法可讓您依名稱存取特定的 DataSourceView 執行個體。</span><span class="sxs-lookup"><span data-stu-id="64b7d-121">For example, the GetViewNames method returns an ICollection that allows you to enumerate the DataSourceViews associated with a particular data source control, and the GetView method allows you to access a particular DataSourceView instance by name.</span></span>

<span data-ttu-id="64b7d-122">資料來源控制項有沒有使用者介面。</span><span class="sxs-lookup"><span data-stu-id="64b7d-122">Data source controls have no user-interface.</span></span> <span data-ttu-id="64b7d-123">它們會實作做為伺服器控制項，讓它們可以支援宣告式語法，並使他們將可以存取頁面狀態，如有需要。</span><span class="sxs-lookup"><span data-stu-id="64b7d-123">They are implemented as server controls so that they can support declarative syntax and so that they have access to page state if desired.</span></span> <span data-ttu-id="64b7d-124">資料來源控制項不呈現到用戶端的任何 HTML 標記。</span><span class="sxs-lookup"><span data-stu-id="64b7d-124">Data source controls do not render any HTML markup to the client.</span></span>

> [!NOTE]
> <span data-ttu-id="64b7d-125">因為您稍後所見，那里要也快取使用資料來源控制項所取得的優點。</span><span class="sxs-lookup"><span data-stu-id="64b7d-125">As you'll see later, there are also caching benefits obtained by using data source controls.</span></span>


## <a name="storing-connection-strings"></a><span data-ttu-id="64b7d-126">將連接字串儲存</span><span class="sxs-lookup"><span data-stu-id="64b7d-126">Storing Connection Strings</span></span>

<span data-ttu-id="64b7d-127">我們看看如何設定資料來源控制項之前，我們應該涵蓋在 ASP.NET 2.0 中有關連接字串的新功能。</span><span class="sxs-lookup"><span data-stu-id="64b7d-127">Before we get into looking at how to configure data source controls, we should cover a new capability in ASP.NET 2.0 concerning connection strings.</span></span> <span data-ttu-id="64b7d-128">ASP.NET 2.0 導入了新的區段，可讓您輕鬆地儲存連接字串，可以在執行階段以動態方式讀取組態檔中。</span><span class="sxs-lookup"><span data-stu-id="64b7d-128">ASP.NET 2.0 introduces a new section in the configuration file that allows you to easily store connection strings that can be read dynamically at runtime.</span></span> <span data-ttu-id="64b7d-129">&lt;ConnectionStrings&gt;  區段可以讓您輕鬆地將連接字串儲存。</span><span class="sxs-lookup"><span data-stu-id="64b7d-129">The &lt;connectionStrings&gt; section makes it easy to store connection strings.</span></span>

<span data-ttu-id="64b7d-130">下列程式碼片段會新增新的連接字串。</span><span class="sxs-lookup"><span data-stu-id="64b7d-130">The snippet below adds a new connection string.</span></span>

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> <span data-ttu-id="64b7d-131">如同&lt;appSettings&gt;區段中， &lt;connectionStrings&gt;之外的區段會出現&lt;system.web&gt;組態檔中的區段。</span><span class="sxs-lookup"><span data-stu-id="64b7d-131">Just as with the &lt;appSettings&gt; section, the &lt;connectionStrings&gt; section appears outside of the &lt;system.web&gt; section in the configuration file.</span></span>


<span data-ttu-id="64b7d-132">若要使用此連接字串，您可以使用下列語法，設定伺服器控制項的 ConnectionString 屬性時。</span><span class="sxs-lookup"><span data-stu-id="64b7d-132">To use this connection string, you can use the following syntax when setting the ConnectionString attribute of a server control.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

<span data-ttu-id="64b7d-133">&lt;ConnectionStrings&gt;區段也會加密，因此不會公開機密資訊。</span><span class="sxs-lookup"><span data-stu-id="64b7d-133">The &lt;connectionStrings&gt; section can also be encrypted so that sensitive information is not exposed.</span></span> <span data-ttu-id="64b7d-134">在更新版本的模組，將會說明這項功能。</span><span class="sxs-lookup"><span data-stu-id="64b7d-134">That ability will be covered in a later module.</span></span>

## <a name="caching-data-sources"></a><span data-ttu-id="64b7d-135">快取的資料來源</span><span class="sxs-lookup"><span data-stu-id="64b7d-135">Caching Data Sources</span></span>

<span data-ttu-id="64b7d-136">每個 DataSourceControl 會提供四個屬性來設定快取;EnableCaching、 CacheDuration、 CacheExpirationPolicy 和 CacheKeyDependency。</span><span class="sxs-lookup"><span data-stu-id="64b7d-136">Each DataSourceControl provides four properties for configuring caching; EnableCaching, CacheDuration, CacheExpirationPolicy, and CacheKeyDependency.</span></span>

## <a name="enablecaching"></a><span data-ttu-id="64b7d-137">EnableCaching</span><span class="sxs-lookup"><span data-stu-id="64b7d-137">EnableCaching</span></span>

<span data-ttu-id="64b7d-138">EnableCaching 是布林值屬性，決定快取已啟用資料來源控制項。</span><span class="sxs-lookup"><span data-stu-id="64b7d-138">EnableCaching is a Boolean property that determines whether or not caching is enabled for the data source control.</span></span>

## <a name="cacheduration-property"></a><span data-ttu-id="64b7d-139">CacheDuration 屬性</span><span class="sxs-lookup"><span data-stu-id="64b7d-139">CacheDuration Property</span></span>

<span data-ttu-id="64b7d-140">CacheDuration 屬性會設定快取會維持有效狀態的秒數。</span><span class="sxs-lookup"><span data-stu-id="64b7d-140">The CacheDuration property sets the number of seconds that the cache remains valid.</span></span> <span data-ttu-id="64b7d-141">將此屬性設定為**0**會導致要保持有效，直到明確失效的快取。</span><span class="sxs-lookup"><span data-stu-id="64b7d-141">Setting this property to **0** causes the cache to remain valid until explicitly invalidated.</span></span>

## <a name="cacheexpirationpolicy-property"></a><span data-ttu-id="64b7d-142">CacheExpirationPolicy 屬性</span><span class="sxs-lookup"><span data-stu-id="64b7d-142">CacheExpirationPolicy Property</span></span>

<span data-ttu-id="64b7d-143">CacheExpirationPolicy 屬性可以設定為**絕對**或是**滑動**。</span><span class="sxs-lookup"><span data-stu-id="64b7d-143">The CacheExpirationPolicy property can be set to either **Absolute** or **Sliding**.</span></span> <span data-ttu-id="64b7d-144">請將它設定為絕對最大快取的資料的時間量是 CacheDuration 屬性所指定的秒數表示。</span><span class="sxs-lookup"><span data-stu-id="64b7d-144">Setting it to Absolute means that the maximum amount of time that the data will be cached is the number of seconds specified by the CacheDuration property.</span></span> <span data-ttu-id="64b7d-145">藉由將它設定為 滑動，每個作業執行時，會重設到期時間。</span><span class="sxs-lookup"><span data-stu-id="64b7d-145">By setting it to Sliding, the expiration time is reset when each operation is performed.</span></span>

## <a name="cachekeydependency-property"></a><span data-ttu-id="64b7d-146">CacheKeyDependency 屬性</span><span class="sxs-lookup"><span data-stu-id="64b7d-146">CacheKeyDependency Property</span></span>

<span data-ttu-id="64b7d-147">如果 CacheKeyDependency 屬性指定的字串值，ASP.NET 會設定新的快取相依性，該字串為基礎。</span><span class="sxs-lookup"><span data-stu-id="64b7d-147">If a string value is specified for the CacheKeyDependency property, ASP.NET will set up a new cache dependency based on that string.</span></span> <span data-ttu-id="64b7d-148">這可讓您明確地只變更或移除 CacheKeyDependency 確認快取。</span><span class="sxs-lookup"><span data-stu-id="64b7d-148">This allows you to explicitly invalidate the cache by simply changing or removing the CacheKeyDependency.</span></span>

<span data-ttu-id="64b7d-149">**重要**：如果已啟用模擬，且存取的資料來源及/或資料的內容，根據用戶端身分識別，則建議 EnableCaching 設定為 False，則快取停用。</span><span class="sxs-lookup"><span data-stu-id="64b7d-149">**Important**: If impersonation is enabled and access to the data source and/or content of data are based upon client identity, it is recommended that caching be disabled by setting EnableCaching to False.</span></span> <span data-ttu-id="64b7d-150">如果已啟用快取在此案例中，而且非原本要求資料之使用者的使用者發出的要求，不會強制執行資料來源的授權。</span><span class="sxs-lookup"><span data-stu-id="64b7d-150">If caching is enabled in this scenario and a user other than the user who originally requested the data issues a request, authorization to the data source is not enforced.</span></span> <span data-ttu-id="64b7d-151">從快取，將只會提供資料。</span><span class="sxs-lookup"><span data-stu-id="64b7d-151">The data will simply be served from cache.</span></span>

## <a name="the-sqldatasource-control"></a><span data-ttu-id="64b7d-152">SqlDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="64b7d-152">The SqlDataSource Control</span></span>

<span data-ttu-id="64b7d-153">SqlDataSource 控制項可讓開發人員存取支援 ADO.NET 的任何關聯式資料庫中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="64b7d-153">The SqlDataSource control allows a developer to access data stored in any relational database that supports ADO.NET.</span></span> <span data-ttu-id="64b7d-154">它可用來存取 SQL Server 資料庫、 System.Data.OleDb 提供者、 System.Data.Odbc 提供者或 System.Data.OracleClient 提供者來存取 Oracle System.Data.SqlClient 提供者。</span><span class="sxs-lookup"><span data-stu-id="64b7d-154">It can use the System.Data.SqlClient provider to access a SQL Server database, the System.Data.OleDb provider, the System.Data.Odbc provider, or the System.Data.OracleClient provider to access Oracle.</span></span> <span data-ttu-id="64b7d-155">因此，SqlDataSource 當然不只用於存取 SQL Server 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="64b7d-155">Therefore, the SqlDataSource is certainly not only used for accessing data in a SQL Server database.</span></span>

<span data-ttu-id="64b7d-156">若要使用 SqlDataSource，，只要提供 ConnectionString 屬性的值和指定的 SQL 命令或預存程序。</span><span class="sxs-lookup"><span data-stu-id="64b7d-156">In order to use the SqlDataSource, you simply provide a value for the ConnectionString property and specify a SQL command or stored procedure.</span></span> <span data-ttu-id="64b7d-157">SqlDataSource 控制項負責使用基礎 ADO.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="64b7d-157">The SqlDataSource control takes care of working with the underlying ADO.NET architecture.</span></span> <span data-ttu-id="64b7d-158">它會開啟連接、 查詢資料來源或執行預存程序、 傳回的資料，，然後關閉您的連接。</span><span class="sxs-lookup"><span data-stu-id="64b7d-158">It opens the connection, queries the data source or executes the stored procedure, returns the data, and then closes the connection for you.</span></span>

> [!NOTE]
> <span data-ttu-id="64b7d-159">因為 DataSourceControl 類別會自動關閉您的連線，它應該減少產生的資料庫連線流失的客戶來電數目。</span><span class="sxs-lookup"><span data-stu-id="64b7d-159">Because the DataSourceControl class automatically closes the connection for you, it should reduce the number of customer calls generated by leaking database connections.</span></span>


<span data-ttu-id="64b7d-160">下列程式碼片段中，將繫結 DropDownList 控制項至 SqlDataSource 控制項使用的連接字串儲存在如上所示的組態檔中。</span><span class="sxs-lookup"><span data-stu-id="64b7d-160">The code snippet below binds a DropDownList control to a SqlDataSource control using the connection string that is stored in the configuration file as shown above.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

<span data-ttu-id="64b7d-161">如以上所述，SqlDataSource DataSourceMode 屬性會指定資料來源的模式。</span><span class="sxs-lookup"><span data-stu-id="64b7d-161">As illustrated above, the DataSourceMode property of the SqlDataSource specifies the mode for the data source.</span></span> <span data-ttu-id="64b7d-162">在上述範例中，DataSourceMode 設為 DataReader。</span><span class="sxs-lookup"><span data-stu-id="64b7d-162">In the example above, the DataSourceMode is set to DataReader.</span></span> <span data-ttu-id="64b7d-163">在此情況下，SqlDataSource 會傳回 IDataReader 物件使用順向且唯讀資料指標。</span><span class="sxs-lookup"><span data-stu-id="64b7d-163">In that case, the SqlDataSource will return an IDataReader object using a forward-only and read-only cursor.</span></span> <span data-ttu-id="64b7d-164">傳回物件的指定的型別是由使用提供者控制。</span><span class="sxs-lookup"><span data-stu-id="64b7d-164">The specified type of object that is returned is controlled by the provider that is used.</span></span> <span data-ttu-id="64b7d-165">在此情況下，我使用 System.Data.SqlClient 的提供者中所指定&lt;connectionStrings&gt; web.config 檔案區段。</span><span class="sxs-lookup"><span data-stu-id="64b7d-165">In this case, I'm using the System.Data.SqlClient provider as specified in the &lt;connectionStrings&gt; section of the web.config file.</span></span> <span data-ttu-id="64b7d-166">因此，會傳回的物件將會是類型 SqlDataReader。</span><span class="sxs-lookup"><span data-stu-id="64b7d-166">Therefore, the object that is returned will be of type SqlDataReader.</span></span> <span data-ttu-id="64b7d-167">藉由指定 DataSourceMode 值的資料集，資料可以儲存在伺服器上的資料集。</span><span class="sxs-lookup"><span data-stu-id="64b7d-167">By specifying a DataSourceMode value of DataSet, the data can be stored in a DataSet on the server.</span></span> <span data-ttu-id="64b7d-168">此模式可讓您新增功能，例如排序、 分頁等等。如果我已經資料繫結到 GridView 控制項 SqlDataSource，我會選擇資料集模式。</span><span class="sxs-lookup"><span data-stu-id="64b7d-168">This mode allows you to add features such as sorting, paging, etc. If I had been data-binding the SqlDataSource to a GridView control, I would have chosen the DataSet mode.</span></span> <span data-ttu-id="64b7d-169">不過，在下拉式清單中，DataReader 模式是正確的選擇。</span><span class="sxs-lookup"><span data-stu-id="64b7d-169">However, in the case of a DropDownList, the DataReader mode is the correct choice.</span></span>

> [!NOTE]
> <span data-ttu-id="64b7d-170">當快取 SqlDataSource 或 AccessDataSource DataSourceMode 屬性必須設定資料集。</span><span class="sxs-lookup"><span data-stu-id="64b7d-170">When caching a SqlDataSource or an AccessDataSource, the DataSourceMode property must be set to DataSet.</span></span> <span data-ttu-id="64b7d-171">如果您啟用使用 DataReader DataSourceMode 的快取，則會發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="64b7d-171">An exception will occur if you enable caching with a DataSourceMode of DataReader.</span></span>


## <a name="sqldatasource-properties"></a><span data-ttu-id="64b7d-172">SqlDataSource 屬性</span><span class="sxs-lookup"><span data-stu-id="64b7d-172">SqlDataSource Properties</span></span>

<span data-ttu-id="64b7d-173">以下是一些 SqlDataSource 控制項的屬性。</span><span class="sxs-lookup"><span data-stu-id="64b7d-173">The following are some of the properties of the SqlDataSource control.</span></span>

### <a name="cancelselectonnullparameter"></a><span data-ttu-id="64b7d-174">CancelSelectOnNullParameter</span><span class="sxs-lookup"><span data-stu-id="64b7d-174">CancelSelectOnNullParameter</span></span>

<span data-ttu-id="64b7d-175">布林值，指定是否其中一個參數為 null，是否要取消選取的命令。</span><span class="sxs-lookup"><span data-stu-id="64b7d-175">A Boolean value that specifies whether a select command is canceled if one of the parameters is null.</span></span> <span data-ttu-id="64b7d-176">預設值為 true。</span><span class="sxs-lookup"><span data-stu-id="64b7d-176">True by default.</span></span>

### <a name="conflictdetection"></a><span data-ttu-id="64b7d-177">ConflictDetection</span><span class="sxs-lookup"><span data-stu-id="64b7d-177">ConflictDetection</span></span>

<span data-ttu-id="64b7d-178">在其中多個使用者可能會更新資料來源在同一時間的情況下，ConflictDetection 屬性會決定 SqlDataSource 控制項的行為。</span><span class="sxs-lookup"><span data-stu-id="64b7d-178">In a situation where multiple users may be updating a data source at the same time, the ConflictDetection property determines the behavior of the SqlDataSource control.</span></span> <span data-ttu-id="64b7d-179">這個屬性評估為其中一個 ConflictOptions 列舉型別的值。</span><span class="sxs-lookup"><span data-stu-id="64b7d-179">This property evaluates to one of the values of the ConflictOptions enumeration.</span></span> <span data-ttu-id="64b7d-180">這些值為**CompareAllValues**並**OverwriteChanges**。</span><span class="sxs-lookup"><span data-stu-id="64b7d-180">Those values are **CompareAllValues** and **OverwriteChanges**.</span></span> <span data-ttu-id="64b7d-181">如果設為 OverwriteChanges，將資料寫入至資料來源的最後一個人會覆寫任何先前的變更。</span><span class="sxs-lookup"><span data-stu-id="64b7d-181">If set to OverwriteChanges, the last person to write data to the data source overwrites any previous changes.</span></span> <span data-ttu-id="64b7d-182">不過，如果 ConflictDetection 屬性設定為 CompareAllValues，參數會建立 SelectCommand 所傳回的資料行，且參數也會建立來保存每個允許以 sqldatasource 進行的資料行中的原始值判斷值已變更，因為 SelectCommand 執行。</span><span class="sxs-lookup"><span data-stu-id="64b7d-182">However, if the ConflictDetection property is set to CompareAllValues, parameters get created for the columns returned by the SelectCommand and parameters are also created to hold the original values in each of those columns allowing the SqlDataSource to determine whether or not the values have changed since the SelectCommand was executed.</span></span>

### <a name="deletecommand"></a><span data-ttu-id="64b7d-183">DeleteCommand</span><span class="sxs-lookup"><span data-stu-id="64b7d-183">DeleteCommand</span></span>

<span data-ttu-id="64b7d-184">設定或取得從資料庫刪除資料列時使用的 SQL 字串。</span><span class="sxs-lookup"><span data-stu-id="64b7d-184">Sets or gets the SQL string used when deleting rows from the database.</span></span> <span data-ttu-id="64b7d-185">這可以是 SQL 查詢或預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="64b7d-185">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="deletecommandtype"></a><span data-ttu-id="64b7d-186">DeleteCommandType</span><span class="sxs-lookup"><span data-stu-id="64b7d-186">DeleteCommandType</span></span>

<span data-ttu-id="64b7d-187">設定或取得 delete 命令的類型是 SQL 查詢 （文字） 或預存程序 （預存程序）。</span><span class="sxs-lookup"><span data-stu-id="64b7d-187">Sets or gets the type of delete command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="deleteparameters"></a><span data-ttu-id="64b7d-188">DeleteParameters</span><span class="sxs-lookup"><span data-stu-id="64b7d-188">DeleteParameters</span></span>

<span data-ttu-id="64b7d-189">傳回 DeleteCommand SqlDataSourceView 相關聯的物件使用 SqlDataSource 控制項所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="64b7d-189">Returns the parameters that are used by the DeleteCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

### <a name="oldvaluesparameterformatstring"></a><span data-ttu-id="64b7d-190">OldValuesParameterFormatString</span><span class="sxs-lookup"><span data-stu-id="64b7d-190">OldValuesParameterFormatString</span></span>

<span data-ttu-id="64b7d-191">這個屬性用來指定在其中 ConflictDetection 屬性設定為 CompareAllValues 的情況下的原始值參數的格式。</span><span class="sxs-lookup"><span data-stu-id="64b7d-191">This property is used to specify the format of the original value parameters in cases where the ConflictDetection property is set to CompareAllValues.</span></span> <span data-ttu-id="64b7d-192">預設值是{0}表示原始值的參數會與原始的參數同名。</span><span class="sxs-lookup"><span data-stu-id="64b7d-192">The default is {0} which means that original value parameters will take the same name as the original parameter.</span></span> <span data-ttu-id="64b7d-193">換句話說，如果 EmployeeID 欄位名稱，原始的值，參數會是@EmployeeID。</span><span class="sxs-lookup"><span data-stu-id="64b7d-193">In other words, if the field name is EmployeeID, the original value parameter would be @EmployeeID.</span></span>

### <a name="selectcommand"></a><span data-ttu-id="64b7d-194">SelectCommand</span><span class="sxs-lookup"><span data-stu-id="64b7d-194">SelectCommand</span></span>

<span data-ttu-id="64b7d-195">設定或取得用來從資料庫擷取資料的 SQL 字串。</span><span class="sxs-lookup"><span data-stu-id="64b7d-195">Sets or gets the SQL string that is used to retrieve data from the database.</span></span> <span data-ttu-id="64b7d-196">這可以是 SQL 查詢或預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="64b7d-196">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="selectcommandtype"></a><span data-ttu-id="64b7d-197">SelectCommandType</span><span class="sxs-lookup"><span data-stu-id="64b7d-197">SelectCommandType</span></span>

<span data-ttu-id="64b7d-198">設定或取得的 select 命令，類型是 SQL 查詢 （文字） 或預存程序 （預存程序）。</span><span class="sxs-lookup"><span data-stu-id="64b7d-198">Sets or gets the type of select command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="selectparameters"></a><span data-ttu-id="64b7d-199">SelectParameters</span><span class="sxs-lookup"><span data-stu-id="64b7d-199">SelectParameters</span></span>

<span data-ttu-id="64b7d-200">傳回 SelectCommand SqlDataSourceView 相關聯的物件使用 SqlDataSource 控制項所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="64b7d-200">Returns the parameters that are used by the SelectCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

### <a name="sortparametername"></a><span data-ttu-id="64b7d-201">SortParameterName</span><span class="sxs-lookup"><span data-stu-id="64b7d-201">SortParameterName</span></span>

<span data-ttu-id="64b7d-202">取得或設定預存程序參數，以供排序資料擷取時資料來源控制項的名稱。</span><span class="sxs-lookup"><span data-stu-id="64b7d-202">Gets or sets the name of a stored procedure parameter that is used when sorting data retrieved by the data source control.</span></span> <span data-ttu-id="64b7d-203">只有在 SelectCommandType 設為預存程序時，才有效。</span><span class="sxs-lookup"><span data-stu-id="64b7d-203">Valid only when SelectCommandType is set to StoredProcedure.</span></span>

### <a name="sqlcachedependency"></a><span data-ttu-id="64b7d-204">SqlCacheDependency</span><span class="sxs-lookup"><span data-stu-id="64b7d-204">SqlCacheDependency</span></span>

<span data-ttu-id="64b7d-205">以分號分隔的字串，指定的資料庫和 SQL Server 快取相依性中使用的資料表。</span><span class="sxs-lookup"><span data-stu-id="64b7d-205">A semi-colon delimited string specifying the databases and tables used in a SQL Server cache dependency.</span></span> <span data-ttu-id="64b7d-206">（更新版本的模組中會討論 SQL 快取相依性）。</span><span class="sxs-lookup"><span data-stu-id="64b7d-206">(SQL cache dependencies will be discussed in a later module.)</span></span>

### <a name="updatecommand"></a><span data-ttu-id="64b7d-207">UpdateCommand</span><span class="sxs-lookup"><span data-stu-id="64b7d-207">UpdateCommand</span></span>

<span data-ttu-id="64b7d-208">設定或取得更新資料庫中的資料時使用的 SQL 字串。</span><span class="sxs-lookup"><span data-stu-id="64b7d-208">Sets or gets the SQL string that is used when updating data in the database.</span></span> <span data-ttu-id="64b7d-209">這可以是 SQL 查詢或預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="64b7d-209">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="updatecommandtype"></a><span data-ttu-id="64b7d-210">UpdateCommandType</span><span class="sxs-lookup"><span data-stu-id="64b7d-210">UpdateCommandType</span></span>

<span data-ttu-id="64b7d-211">設定或取得更新命令的類型是 SQL 查詢 （文字） 或預存程序 （預存程序）。</span><span class="sxs-lookup"><span data-stu-id="64b7d-211">Sets or gets the type of update command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="updateparameters"></a><span data-ttu-id="64b7d-212">UpdateParameters</span><span class="sxs-lookup"><span data-stu-id="64b7d-212">UpdateParameters</span></span>

<span data-ttu-id="64b7d-213">傳回的 UpdateCommand SqlDataSourceView 相關聯的物件使用 SqlDataSource 控制項所使用的參數。</span><span class="sxs-lookup"><span data-stu-id="64b7d-213">Returns the parameters that are used by the UpdateCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

## <a name="the-accessdatasource-control"></a><span data-ttu-id="64b7d-214">AccessDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="64b7d-214">The AccessDataSource Control</span></span>

<span data-ttu-id="64b7d-215">AccessDataSource 控制項衍生自 SqlDataSource 類別，以及用來資料繫結至 Microsoft Access 資料庫。</span><span class="sxs-lookup"><span data-stu-id="64b7d-215">The AccessDataSource control derives from the SqlDataSource class and is used to data-bind to a Microsoft Access database.</span></span> <span data-ttu-id="64b7d-216">AccessDataSource 控制項上的 ConnectionString 屬性是唯讀屬性。</span><span class="sxs-lookup"><span data-stu-id="64b7d-216">The ConnectionString property for the AccessDataSource control is a read-only property.</span></span> <span data-ttu-id="64b7d-217">而不是使用上的 ConnectionString 屬性，資料檔屬性用來指向 Access 資料庫，如下所示。</span><span class="sxs-lookup"><span data-stu-id="64b7d-217">Instead of using the ConnectionString property, the DataFile property is used to point to the Access Database as shown below.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

<span data-ttu-id="64b7d-218">AccessDataSource 將的基底 SqlDataSource ProviderName 永遠設 System.Data.OleDb，並連接至使用 Microsoft.Jet.OLEDB.4.0 OLE DB 提供者的資料庫。</span><span class="sxs-lookup"><span data-stu-id="64b7d-218">The AccessDataSource will always set the ProviderName of the base SqlDataSource to System.Data.OleDb and connects to the database using the Microsoft.Jet.OLEDB.4.0 OLE DB provider.</span></span> <span data-ttu-id="64b7d-219">您無法使用 AccessDataSource 控制項連接到受密碼保護 Access 資料庫。</span><span class="sxs-lookup"><span data-stu-id="64b7d-219">You cannot use the AccessDataSource control to connect to a password-protected Access database.</span></span> <span data-ttu-id="64b7d-220">如果您有連接到受密碼保護資料庫，您應該使用 SqlDataSource 控制項。</span><span class="sxs-lookup"><span data-stu-id="64b7d-220">If you have to connect to a password protected database, you should use the SqlDataSource control.</span></span>

> [!NOTE]
> <span data-ttu-id="64b7d-221">儲存在網站內的 access 資料庫應該放在應用程式\_資料目錄。</span><span class="sxs-lookup"><span data-stu-id="64b7d-221">Access databases stored within the Web site should be placed in the App\_Data directory.</span></span> <span data-ttu-id="64b7d-222">ASP.NET 不允許所要瀏覽此目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="64b7d-222">ASP.NET does not allow files in this directory to be browsed.</span></span> <span data-ttu-id="64b7d-223">您將需要應用程式的讀取和寫入權限授與處理序帳戶\_使用 Access 資料庫時，資料目錄。</span><span class="sxs-lookup"><span data-stu-id="64b7d-223">You will need to grant the process account Read and Write permissions to the App\_Data directory when using Access databases.</span></span>


## <a name="the-xmldatasource-control"></a><span data-ttu-id="64b7d-224">XmlDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="64b7d-224">The XmlDataSource Control</span></span>

<span data-ttu-id="64b7d-225">XmlDataSource 用來進行資料繫結的 XML 資料的資料繫結控制項。</span><span class="sxs-lookup"><span data-stu-id="64b7d-225">The XmlDataSource is used to data-bind XML data to data-bound controls.</span></span> <span data-ttu-id="64b7d-226">您可以繫結至 XML 檔案中使用的資料檔的屬性，或您可以繫結使用的資料屬性的 XML 字串。</span><span class="sxs-lookup"><span data-stu-id="64b7d-226">You can bind to an XML file using the DataFile property or you can bind to an XML string using the Data property.</span></span> <span data-ttu-id="64b7d-227">XmlDataSource 會公開為可繫結欄位的 XML 屬性。</span><span class="sxs-lookup"><span data-stu-id="64b7d-227">The XmlDataSource exposes XML attributes as bindable fields.</span></span> <span data-ttu-id="64b7d-228">在您要繫結至不會表示為屬性的值的情況下，您必須使用 XSL 轉換。</span><span class="sxs-lookup"><span data-stu-id="64b7d-228">In cases where you need to bind to values that are not represented as attributes, you will need to use an XSL transform.</span></span> <span data-ttu-id="64b7d-229">您也可以使用篩選的 XML 資料的 XPath 運算式。</span><span class="sxs-lookup"><span data-stu-id="64b7d-229">You can also use XPath expressions to filter XML data.</span></span>

<span data-ttu-id="64b7d-230">請考慮下列的 XML 檔案：</span><span class="sxs-lookup"><span data-stu-id="64b7d-230">Consider the following XML file:</span></span>

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

<span data-ttu-id="64b7d-231">請注意，XmlDataSource 使用 XPath 屬性*人/* 若要篩選只&lt;人員&gt;節點。</span><span class="sxs-lookup"><span data-stu-id="64b7d-231">Notice that the XmlDataSource uses an XPath property of *People/Person* in order to filter on just the &lt;Person&gt; nodes.</span></span> <span data-ttu-id="64b7d-232">DropDownList 然後資料繫結至使用 DataTextField 屬性 LastName 屬性。</span><span class="sxs-lookup"><span data-stu-id="64b7d-232">The DropDownList then data-binds to the LastName attribute using the DataTextField property.</span></span>

<span data-ttu-id="64b7d-233">XmlDataSource 控制項主要是用來資料繫結至唯讀的 XML 資料中，您可編輯 XML 資料檔。</span><span class="sxs-lookup"><span data-stu-id="64b7d-233">While the XmlDataSource control is primarily used to data-bind to read-only XML data, it is possible to edit the XML data file.</span></span> <span data-ttu-id="64b7d-234">請注意，在此情況下，自動插入、 更新和刪除的 XML 檔案中的資訊不會自動與其他資料來源控制項所顯示的一樣。</span><span class="sxs-lookup"><span data-stu-id="64b7d-234">Note that in such cases, automatic insertion, updating, and deletion of information in the XML file does not happen automatically as it does with other data source controls.</span></span> <span data-ttu-id="64b7d-235">相反地，您必須撰寫程式碼來手動編輯使用下列方法的 XmlDataSource 控制項的資料。</span><span class="sxs-lookup"><span data-stu-id="64b7d-235">Instead, you will have to write code to manually edit the data using the following methods of the XmlDataSource control.</span></span>

### <a name="getxmldocument"></a><span data-ttu-id="64b7d-236">GetXmlDocument</span><span class="sxs-lookup"><span data-stu-id="64b7d-236">GetXmlDocument</span></span>

<span data-ttu-id="64b7d-237">擷取 XmlDocument 物件，其中包含 XmlDataSource 所擷取的 XML 程式碼。</span><span class="sxs-lookup"><span data-stu-id="64b7d-237">Retrieves an XmlDocument object containing the XML code retrieved by the XmlDataSource.</span></span>

### <a name="save"></a><span data-ttu-id="64b7d-238">儲存</span><span class="sxs-lookup"><span data-stu-id="64b7d-238">Save</span></span>

<span data-ttu-id="64b7d-239">將記憶體中 XmlDocument 儲存回資料來源。</span><span class="sxs-lookup"><span data-stu-id="64b7d-239">Saves the in-memory XmlDocument back to the data source.</span></span>

<span data-ttu-id="64b7d-240">請務必了解下列兩項條件符合時，將只會運作 Save 方法：</span><span class="sxs-lookup"><span data-stu-id="64b7d-240">It's important to realize that the Save method will only work when the following two conditions are met:</span></span>

1. <span data-ttu-id="64b7d-241">XmlDataSource 使用繫結至記憶體中 XML 資料繫結至 XML 檔案而非資料屬性的資料檔屬性。</span><span class="sxs-lookup"><span data-stu-id="64b7d-241">The XmlDataSource is using the DataFile property to bind to an XML file instead of the Data property to bind to in-memory XML data.</span></span>
2. <span data-ttu-id="64b7d-242">任何轉換，並透過 轉換 或 TransformFile 屬性不指定。</span><span class="sxs-lookup"><span data-stu-id="64b7d-242">No transformation is specified via the Transform or TransformFile property.</span></span>

<span data-ttu-id="64b7d-243">也請注意 Save 方法可以產生非預期的結果時同時呼叫多個使用者。</span><span class="sxs-lookup"><span data-stu-id="64b7d-243">Note also that the Save method can yield unexpected results when called by multiple users concurrently.</span></span>

## <a name="the-objectdatasource-control"></a><span data-ttu-id="64b7d-244">ObjectDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="64b7d-244">The ObjectDataSource Control</span></span>

<span data-ttu-id="64b7d-245">截至目前為止，我們已涵蓋的資料來源控制項是絕佳的兩層式應用程式，其中的資料來源控制項與外界溝通的直接資料存放區。</span><span class="sxs-lookup"><span data-stu-id="64b7d-245">The data source controls that we have covered up to this point are excellent choices for two-tier applications where the data source control communicates directly to the data store.</span></span> <span data-ttu-id="64b7d-246">不過，許多真實世界應用程式是多層式應用程式資料來源控制項可能需要進行通訊的通訊與資料層商務物件。</span><span class="sxs-lookup"><span data-stu-id="64b7d-246">However, many real-world applications are multi-tier applications where a data source control might need to communicate to a business object which, in turn, communicates with the data layer.</span></span> <span data-ttu-id="64b7d-247">在這些情況下，ObjectDataSource 會填滿帳單得很好。</span><span class="sxs-lookup"><span data-stu-id="64b7d-247">In these situations, the ObjectDataSource fills the bill nicely.</span></span> <span data-ttu-id="64b7d-248">ObjectDataSource 的運作方式與來源物件搭配使用。</span><span class="sxs-lookup"><span data-stu-id="64b7d-248">The ObjectDataSource works in conjunction with a source object.</span></span> <span data-ttu-id="64b7d-249">ObjectDataSource 控制項將會建立來源物件、 呼叫指定的方法和處置的物件執行個體全部都在範圍內的單一要求的執行個體，如果將物件的執行個體方法，而不是靜態方法 (Visual Basic 中為 Shared)。</span><span class="sxs-lookup"><span data-stu-id="64b7d-249">The ObjectDataSource control will create an instance of the source object, call the specified method, and dispose of the object instance all within the scope of a single request, if your object has instance methods instead of static methods (Shared in Visual Basic).</span></span> <span data-ttu-id="64b7d-250">因此，您的物件必須是無狀態。</span><span class="sxs-lookup"><span data-stu-id="64b7d-250">Therefore, your object must be stateless.</span></span> <span data-ttu-id="64b7d-251">也就是您的物件應該取得和釋放所有必要的資源，在單一要求的範圍內。</span><span class="sxs-lookup"><span data-stu-id="64b7d-251">That is, your object should acquire and release all required resources within the span of a single request.</span></span> <span data-ttu-id="64b7d-252">您可以控制處理 ObjectCreating 事件的 ObjectDataSource 控制項來源物件建立的方式。</span><span class="sxs-lookup"><span data-stu-id="64b7d-252">You can control how the source object is created by handling the ObjectCreating event of the ObjectDataSource control.</span></span> <span data-ttu-id="64b7d-253">您可以建立的來源物件，執行個體，，然後將該執行個體的 ObjectDataSourceEventArgs 類別的 ObjectInstance 屬性。</span><span class="sxs-lookup"><span data-stu-id="64b7d-253">You can create an instance of the source object, and then set the ObjectInstance property of the ObjectDataSourceEventArgs class to that instance.</span></span> <span data-ttu-id="64b7d-254">ObjectDataSource 控制項將使用建立 ObjectCreating 事件，而不是建立在它自己的執行個體中的執行個體。</span><span class="sxs-lookup"><span data-stu-id="64b7d-254">The ObjectDataSource control will use the instance that is created in the ObjectCreating event instead of creating an instance on its own.</span></span>

<span data-ttu-id="64b7d-255">如果 ObjectDataSource 控制項來源物件會公開的公用靜態方法 (Visual Basic 中為 Shared) 可以呼叫以擷取和修改資料，ObjectDataSource 控制項就會直接呼叫這些方法。</span><span class="sxs-lookup"><span data-stu-id="64b7d-255">If the source object for an ObjectDataSource control exposes public static methods (Shared in Visual Basic) that can be called to retrieve and modify data, an ObjectDataSource control will call those methods directly.</span></span> <span data-ttu-id="64b7d-256">如果 ObjectDataSource 控制項必須建立來源物件的執行個體，才能進行方法呼叫，該物件必須包含不接受任何參數的公用建構函式。</span><span class="sxs-lookup"><span data-stu-id="64b7d-256">If an ObjectDataSource control must create an instance of the source object in order to make method calls, the object must include a public constructor that takes no parameters.</span></span> <span data-ttu-id="64b7d-257">ObjectDataSource 控制項來源物件的新執行個體建立時，會呼叫這個建構函式。</span><span class="sxs-lookup"><span data-stu-id="64b7d-257">The ObjectDataSource control will call this constructor when it creates a new instance of the source object.</span></span>

<span data-ttu-id="64b7d-258">如果來源物件不包含不含參數的公用建構函式，您可以建立將由 ObjectCreating 事件中的 ObjectDataSource 控制項來源物件的執行個體。</span><span class="sxs-lookup"><span data-stu-id="64b7d-258">If the source object does not contain a public constructor without parameters, you can create an instance of the source object that will be used by the ObjectDataSource control in the ObjectCreating event.</span></span>

## <a name="specifying-object-methods"></a><span data-ttu-id="64b7d-259">指定物件的方法</span><span class="sxs-lookup"><span data-stu-id="64b7d-259">Specifying Object Methods</span></span>

<span data-ttu-id="64b7d-260">ObjectDataSource 控制項來源物件可以包含任意數目的方法，用於選取、 插入、 更新或刪除資料。</span><span class="sxs-lookup"><span data-stu-id="64b7d-260">The source object for an ObjectDataSource control can contain any number of methods that are used to select, insert, update, or delete data.</span></span> <span data-ttu-id="64b7d-261">使用 ObjectDataSource 控制項的 SelectMethod、 InsertMethod、 UpdateMethod、 或 DeleteMethod 屬性所識別，ObjectDataSource 控制項根據方法的名稱，會呼叫這些方法。</span><span class="sxs-lookup"><span data-stu-id="64b7d-261">These methods are called by the ObjectDataSource control based on the name of the method, as identified by using either the SelectMethod, InsertMethod, UpdateMethod, or DeleteMethod property of the ObjectDataSource control.</span></span> <span data-ttu-id="64b7d-262">來源物件也可以包含選擇性 SelectCount 方法，以使用 SelectCountMethod; 屬性，傳回的資料來源的物件總數計數的 ObjectDataSource 控制項識別。</span><span class="sxs-lookup"><span data-stu-id="64b7d-262">The source object can also include an optional SelectCount method, which is identified by the ObjectDataSource control using the SelectCountMethod property, that returns the count of the total number of objects at the data source.</span></span> <span data-ttu-id="64b7d-263">ObjectDataSource 控制項選取的方法呼叫時，要擷取的資料來源使用的記錄總數分頁之後，會呼叫 SelectCount; 方法。</span><span class="sxs-lookup"><span data-stu-id="64b7d-263">The ObjectDataSource control will call the SelectCount method after a Select method has been called to retrieve the total number of records at the data source for use when paging.</span></span>

## <a name="lab-using-data-source-controls"></a><span data-ttu-id="64b7d-264">使用資料來源控制項的實驗室</span><span class="sxs-lookup"><span data-stu-id="64b7d-264">Lab Using Data Source Controls</span></span>

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a><span data-ttu-id="64b7d-265">練習 1-使用 SqlDataSource 控制項顯示的資料</span><span class="sxs-lookup"><span data-stu-id="64b7d-265">Exercise 1 - Displaying Data with the SqlDataSource Control</span></span>

<span data-ttu-id="64b7d-266">下列練習中使用 SqlDataSource 控制項連接至 Northwind 資料庫。</span><span class="sxs-lookup"><span data-stu-id="64b7d-266">The following exercise uses the SqlDataSource control to connect to the Northwind database.</span></span> <span data-ttu-id="64b7d-267">這裡假設您的 SQL Server 2000 執行個體上有 Northwind 資料庫的存取權。</span><span class="sxs-lookup"><span data-stu-id="64b7d-267">It assumes that you have access to the Northwind database on a SQL Server 2000 instance.</span></span>

1. <span data-ttu-id="64b7d-268">建立新的 ASP.NET 網站。</span><span class="sxs-lookup"><span data-stu-id="64b7d-268">Create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="64b7d-269">加入新的 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="64b7d-269">Add a new web.config file.</span></span>

    1. <span data-ttu-id="64b7d-270">以滑鼠右鍵按一下方案總管] 中的專案，然後按一下 [加入新項目。</span><span class="sxs-lookup"><span data-stu-id="64b7d-270">Right-click on the project in Solution Explorer and click Add New Item.</span></span>
    2. <span data-ttu-id="64b7d-271">從範本清單中選擇 Web 組態檔，並按一下 新增。</span><span class="sxs-lookup"><span data-stu-id="64b7d-271">Choose Web Configuration File from the list of templates and click Add.</span></span>
3. <span data-ttu-id="64b7d-272">編輯&lt;connectionStrings&gt;區段，如下所示：</span><span class="sxs-lookup"><span data-stu-id="64b7d-272">Edit the &lt;connectionStrings&gt; section as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. <span data-ttu-id="64b7d-273">切換到程式碼檢視，並新增的 ConnectionString 屬性，以及 SelectCommand 屬性，來&lt;asp: SqlDataSource&gt;控制，如下所示：</span><span class="sxs-lookup"><span data-stu-id="64b7d-273">Switch to Code view and add a ConnectionString attribute and a SelectCommand attribute to the &lt;asp:SqlDataSource&gt; control as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. <span data-ttu-id="64b7d-274">從 [設計] 檢視中，加入新的 GridView 控制項。</span><span class="sxs-lookup"><span data-stu-id="64b7d-274">From Design view, add a new GridView control.</span></span>
6. <span data-ttu-id="64b7d-275">從 GridView 工作 功能表中選擇資料來源 下拉式清單中，選擇 SqlDataSource1。</span><span class="sxs-lookup"><span data-stu-id="64b7d-275">From the Choose Data Source dropdown in the GridView Tasks menu, choose SqlDataSource1.</span></span>
7. <span data-ttu-id="64b7d-276">以滑鼠右鍵按一下 Default.aspx，並從功能表選擇 在瀏覽器中檢視。</span><span class="sxs-lookup"><span data-stu-id="64b7d-276">Right-click on Default.aspx and choose View in Browser from the menu.</span></span> <span data-ttu-id="64b7d-277">當系統提示您儲存時，請按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="64b7d-277">Click Yes when prompted to save.</span></span>
8. <span data-ttu-id="64b7d-278">GridView 會顯示來自 [產品] 資料表的資料。</span><span class="sxs-lookup"><span data-stu-id="64b7d-278">The GridView displays the data from the Products table.</span></span>

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a><span data-ttu-id="64b7d-279">練習 2-使用 SqlDataSource 控制項的編輯資料</span><span class="sxs-lookup"><span data-stu-id="64b7d-279">Exercise 2 - Editing Data with the SqlDataSource Control</span></span>

<span data-ttu-id="64b7d-280">下列練習示範如何為資料繫結 DropDownList 控制項使用的宣告式語法和可讓您編輯 DropDownList 控制項中顯示的資料。</span><span class="sxs-lookup"><span data-stu-id="64b7d-280">The following exercise demonstrates how to data bind a DropDownList control using the declarative syntax and allows you to edit the data presented in the DropDownList control.</span></span>

1. <span data-ttu-id="64b7d-281">在 [設計] 檢視中，刪除從 Default.aspx 的 GridView 控制項。</span><span class="sxs-lookup"><span data-stu-id="64b7d-281">In Design view, delete the GridView control from Default.aspx.</span></span> 

    <span data-ttu-id="64b7d-282">**重要**：保留網頁上的 SqlDataSource 控制項。</span><span class="sxs-lookup"><span data-stu-id="64b7d-282">**Important**: Leave the SqlDataSource control on the page.</span></span>
2. <span data-ttu-id="64b7d-283">將 DropDownList 控制項新增至 Default.aspx 中。</span><span class="sxs-lookup"><span data-stu-id="64b7d-283">Add a DropDownList control to Default.aspx.</span></span>
3. <span data-ttu-id="64b7d-284">切換至來源檢視。</span><span class="sxs-lookup"><span data-stu-id="64b7d-284">Switch to Source view.</span></span>
4. <span data-ttu-id="64b7d-285">DataSourceId、 DataTextField 和 DataValueField 將屬性新增至&lt;asp: DropDownList&gt;控制，如下所示：</span><span class="sxs-lookup"><span data-stu-id="64b7d-285">Add a DataSourceId, DataTextField, and DataValueField attribute to the &lt;asp:DropDownList&gt; control as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. <span data-ttu-id="64b7d-286">儲存 Default.aspx，並在瀏覽器中檢視它。</span><span class="sxs-lookup"><span data-stu-id="64b7d-286">Save Default.aspx and view it in the browser.</span></span> <span data-ttu-id="64b7d-287">請注意，DropDownList 包含所有的產品，從 Northwind 資料庫。</span><span class="sxs-lookup"><span data-stu-id="64b7d-287">Note that the DropDownList contains all of the products from the Northwind database.</span></span>
6. <span data-ttu-id="64b7d-288">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="64b7d-288">Close the browser.</span></span>
7. <span data-ttu-id="64b7d-289">在 Default.aspx 的來源檢視中，加入新的 TextBox 控制項 DropDownList 控制項下方。</span><span class="sxs-lookup"><span data-stu-id="64b7d-289">In Source view of Default.aspx, add a new TextBox control below the DropDownList control.</span></span> <span data-ttu-id="64b7d-290">將文字方塊的 ID 屬性變更為 txtProductName。</span><span class="sxs-lookup"><span data-stu-id="64b7d-290">Change the ID property of the TextBox to txtProductName.</span></span>
8. <span data-ttu-id="64b7d-291">在 TextBox 控制項中，加入新的按鈕控制項。</span><span class="sxs-lookup"><span data-stu-id="64b7d-291">Under the TextBox control, add a new Button control.</span></span> <span data-ttu-id="64b7d-292">將按鈕的 ID 屬性變更為 btnUpdate 和 Text 屬性**更新產品名稱**。</span><span class="sxs-lookup"><span data-stu-id="64b7d-292">Change the ID property of the Button to btnUpdate and the Text property to **Update Product Name**.</span></span>
9. <span data-ttu-id="64b7d-293">在 Default.aspx 來源檢視，UpdateCommand 屬性和加入兩個新 UpdateParameters SqlDataSource 標記，如下所示：</span><span class="sxs-lookup"><span data-stu-id="64b7d-293">In Source view of Default.aspx, add an UpdateCommand property and two new UpdateParameters to the SqlDataSource tag as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > <span data-ttu-id="64b7d-294">請注意，有兩個更新參數 （「 產品名稱 」 和 「 ProductID 」） 加入此程式碼中。</span><span class="sxs-lookup"><span data-stu-id="64b7d-294">Note that there are two update parameters (ProductName and ProductID) added in this code.</span></span> <span data-ttu-id="64b7d-295">這些參數會對應到 txtProductName 文字方塊的 Text 屬性和 ddlProducts DropDownList SelectedValue 屬性。</span><span class="sxs-lookup"><span data-stu-id="64b7d-295">These parameters are mapped to the Text property of the txtProductName TextBox and the SelectedValue property of the ddlProducts DropDownList.</span></span>
10. <span data-ttu-id="64b7d-296">切換至 [設計] 檢視，並按兩下按鈕控制項加入事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="64b7d-296">Switch to Design view and double-click on the Button control to add an event handler.</span></span>
11. <span data-ttu-id="64b7d-297">將下列程式碼新增至 btnUpdate\_按一下程式碼：</span><span class="sxs-lookup"><span data-stu-id="64b7d-297">Add the following code to the btnUpdate\_Click code:</span></span> 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. <span data-ttu-id="64b7d-298">以滑鼠右鍵按一下 Default.aspx，然後選擇在瀏覽器中檢視它。</span><span class="sxs-lookup"><span data-stu-id="64b7d-298">Right-click on Default.aspx and choose to view it in the browser.</span></span> <span data-ttu-id="64b7d-299">當系統提示您儲存所有變更，請按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="64b7d-299">Click Yes when prompted to save all changes.</span></span>
13. <span data-ttu-id="64b7d-300">ASP.NET 2.0 部份類別允許在執行階段編譯。</span><span class="sxs-lookup"><span data-stu-id="64b7d-300">ASP.NET 2.0 partial classes allow for compilation at runtime.</span></span> <span data-ttu-id="64b7d-301">您不需要建置應用程式以查看程式碼變更，才會生效。</span><span class="sxs-lookup"><span data-stu-id="64b7d-301">It is not necessary to build an application in order to see code changes take effect.</span></span>
14. <span data-ttu-id="64b7d-302">從 DropDownList 中選取產品。</span><span class="sxs-lookup"><span data-stu-id="64b7d-302">Select a product from the DropDownList.</span></span>
15. <span data-ttu-id="64b7d-303">在文字方塊中輸入所選產品的新名稱，然後按一下 [更新] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="64b7d-303">Enter a new name for the selected product in the TextBox and then click the Update button.</span></span>
16. <span data-ttu-id="64b7d-304">在資料庫中更新的產品名稱。</span><span class="sxs-lookup"><span data-stu-id="64b7d-304">The product name is updated in the database.</span></span>

## <a name="exercise-3-using-the-objectdatasource-control"></a><span data-ttu-id="64b7d-305">練習 3 使用 ObjectDataSource 控制項</span><span class="sxs-lookup"><span data-stu-id="64b7d-305">Exercise 3 Using the ObjectDataSource Control</span></span>

<span data-ttu-id="64b7d-306">本練習將示範如何使用 ObjectDataSource 控制項與來源物件與 Northwind 資料庫互動。</span><span class="sxs-lookup"><span data-stu-id="64b7d-306">This exercise will demonstrate how to use the ObjectDataSource control and a source object to interact with the Northwind database.</span></span>

1. <span data-ttu-id="64b7d-307">以滑鼠右鍵按一下方案總管 中的專案，然後按一下加入新項目。</span><span class="sxs-lookup"><span data-stu-id="64b7d-307">Right-click on the project in Solution Explorer and click on Add New Item.</span></span>
2. <span data-ttu-id="64b7d-308">在 [範本] 清單中選取 Web 表單。</span><span class="sxs-lookup"><span data-stu-id="64b7d-308">Select Web Form in the templates list.</span></span> <span data-ttu-id="64b7d-309">將名稱變更為 object.aspx 並按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="64b7d-309">Change the name to object.aspx and click Add.</span></span>
3. <span data-ttu-id="64b7d-310">以滑鼠右鍵按一下方案總管 中的專案，然後按一下加入新項目。</span><span class="sxs-lookup"><span data-stu-id="64b7d-310">Right-click on the project in Solution Explorer and click on Add New Item.</span></span>
4. <span data-ttu-id="64b7d-311">在 [範本] 清單中選取類別。</span><span class="sxs-lookup"><span data-stu-id="64b7d-311">Select Class in the templates list.</span></span> <span data-ttu-id="64b7d-312">將類別名稱變更為 NorthwindData.cs 並按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="64b7d-312">Change the name of the class to NorthwindData.cs and click Add.</span></span>
5. <span data-ttu-id="64b7d-313">按一下 [是] 會將類別新增至應用程式出現提示時\_程式碼資料夾。</span><span class="sxs-lookup"><span data-stu-id="64b7d-313">Click Yes when prompted to add the class to the App\_Code folder.</span></span>
6. <span data-ttu-id="64b7d-314">NorthwindData.cs 檔案中加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="64b7d-314">Add the following code to the NorthwindData.cs file:</span></span> 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. <span data-ttu-id="64b7d-315">將下列程式碼新增至 object.aspx 的來源檢視中：</span><span class="sxs-lookup"><span data-stu-id="64b7d-315">Add the following code to the Source view of object.aspx:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. <span data-ttu-id="64b7d-316">儲存所有檔案，然後瀏覽 object.aspx。</span><span class="sxs-lookup"><span data-stu-id="64b7d-316">Save all files and browse object.aspx.</span></span>
9. <span data-ttu-id="64b7d-317">檢視詳細資料、 編輯員工、 加入員工和刪除員工互動的介面。</span><span class="sxs-lookup"><span data-stu-id="64b7d-317">Interact with the interface by viewing details, editing employees, adding employees, and deleting employees.</span></span>
