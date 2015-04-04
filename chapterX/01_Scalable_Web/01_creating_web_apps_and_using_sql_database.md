# X-1-1. 建立網站應用程式及使用 SQL 資料庫

在開始開發及部署網站之前，得先從最基礎開始：在 Microsoft Azure 建立_Web 應用程式_以及 _SQL 資料庫_。這一篇文章除了介紹如何建立之外，也說明如何調整網站的設定。

本篇提及的 Microsoft Azure 服務有：[Web 應用程式](http://azure.microsoft.com/zh-tw/services/app-service/web/)、[SQL 資料庫](http://azure.microsoft.com/zh-tw/services/sql-database/)。

## 建立 Web 應用程式及 SQL 資料庫

要完成這個工作，你可以先建一個 Web 應用程式，再另外建一個 SQL 資料庫，或者可以透過 [Microsoft Azure 市集](http://azure.microsoft.com/zh-tw/marketplace/)中找到 [**Web app + SQL**](http://azure.microsoft.com/zh-tw/marketplace/partners/microsoft/websitesqldatabase/) 的項目直接建立，以下介紹從市集來建立的步驟。

在 [Microsoft Azure 的管理後台](https://portal.azure.com)中，點選左下角的**+**按鈕，選擇 **Web + 行動**，再選擇 **Azure Marketplace**：

![從 Azure Marketplace 建立服務](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-1-create-from-marketplace.png)

接著再從 **Web 應用程式** 的類別中，找到 **Web app + SQL** 的項目，按下**建立**的按鈕。

![建立 Web app + SQL](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-2-create-web-and-sql.png)

接著進入設定的面板，首先要輸入的是**資源群組（Resource Group）**的名稱，接下來要建立的 Web app 以及 SQL 資料庫都會加入這個資源群組中，方便你在 Azure 管理後台中進行管理、監控各種數值以及花費，所以這裡你可以輸入專案的名稱，以便之後在管理後台中辨識。

![輸入資源群組名稱](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-3-create-blade.png)

### 設定 WEB 應用程式

在設定面板中點選 WEB 應用程式設定，在這個畫面中要設定**網站的名稱**，這同時也決定預設的 URL 位址；**應用程服務方案**可以設定某種「價格 - 資料中心位置」的組合是否要與其它的服務共用，只要設定一個你帳號下唯一的名稱即可（如果之前設定過可以直接選擇）。

![設定 WEB 應用程式的 URL 以及服務方案](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-4-config-web-apps.png)

再來是設定**價格區間**，關於 Web 應用程式不同價格的功能以及計價差異可以參考官網上的[頁面說明](http://azure.microsoft.com/zh-tw/pricing/details/app-service/)。**網站的價格區間是隨時可以調整的**，一開始開發時可以選擇**免費**，上線運作後可以再調整其它的方案使用進階功能或是更好的效能。點擊進入設定時也可以看到一些主要差異的介紹，而預估的價格是假設_整個月都使用同一個價格區間_時的價格：

![設定 WEB 應用程式的價格](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-5-web-apps-prices.png)

最後一個步驟就是選擇要建立 Web 應用程式的資料中心，目前距離台灣最近的是 **East Asia** 的機房。

![設定 WEB 應用程式部署的資料中心](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-6-webapp-location.png)

### 設定 SQL 資料庫

完成 WEB 應用程式的設定後，接著設定資料庫，這裡可以選擇新建、或是從之前建立過的資料庫選擇。

![新建或選擇之前建立的資料庫](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-7-config-sql-database.png)

新建 SQL 資料庫時，首先設定的是**資料庫名稱**。

![設定資料庫名稱](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-8-creating-sql-database.png)

再來是選擇 **SQL 資料庫的價格區間**，關於價格、效能與功能的差異可以參考官網上的[頁面說明](http://azure.microsoft.com/zh-tw/pricing/details/sql-database/)。而建立面板上也會顯示等級的差異：

![SQL 資料庫的價格方案](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-9-sql-database-price-plan.png)

再來是設定**資料庫的定序**，關於定序的詳細說明可以參考[MSDN 上的頁面說明](https://msdn.microsoft.com/zh-tw/library/ms143726.aspx)。這裡可以留在預設的設定就好。最後是運行這個 SQL 資料庫的**伺服器設定**，主要是設定伺服器的帳號密碼，以及它所在的資料中心位置。

![SQL 資料庫的伺服器設定](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-10-config-sql-server.png)


設定完 WEB 應用程式以及 SQL 資料庫後，最後在挑選帳號下的訂閱帳戶，就可以按下**建立**的按鈕開始建立，你也可以勾選**新增至「開始面板」**以方便在管理後台直接進入管理。

![SQL 資料庫的伺服器設定](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-11-create-finally.png)

如果一切都沒有問題，稍待約 1 分鐘左右，就可以看到建立完成的資源群組面板了，這裡你會發現建 WEB 應用程式時也會同步建了一個 Application Insight 的服務，這個我們在稍後的文章中會提到如何使用它。

![SQL 資料庫的伺服器設定](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-12-created-resource-group.png)


## 部署網站及資料庫

完成建立 WEB 應用程式以及資料庫後，接下來就是如何部署應用程式上來了。在開始部署之前，我們先到 WEB 應用程式的設定裡加入 SQL 資料庫的連接字串（connection string），首先在資源群組頁面中，點選建立好的 **SQL Database**，然後在 SQL 資料庫管理面板中點擊**屬性**的區塊，這時便能找到**顯示資料庫連接字串**的連結。

![取得資料庫連接字串](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-13-show-database-connection-string.png)

接著會跳出幾種連接資料庫的連接字串範例，你可以根據你 WEB 應用程式所使用的資料庫連接方式來選擇使用，但要注意的是，**這裡顯示的連接字串內 Password 的值必須自行填入**，以 ADO.NET 的連接字串為例，其中的 ```Password={your_password_here}``` 就要自行替換。

![取得資料庫連接字串](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-14-database-connection-string.png)

取得資料庫連接字串後，回到資源群組的面板，點擊 WEB 應用程式，在點選**設定**，到**應用程式屬性**面板中設定資料庫連接字串。

![設定 WEB 應用程式](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-15-config-web-apps-settings.png)

在應用程式屬性的面板中往下拉到**連接字串**的部份，將**名稱**填入 _DefaultConnection_，然後**值**的部份就貼上剛才取得的連接字串（注意：密碼要確定已經代入），後面的類型就選擇 _SQL Database_ 即可。

![設定資料庫連接字串](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-1-16-setting-database-connection-string.png)

設定完成後，按下面板上方的**儲存**按鈕儲存設定。

關於部署網站的部份可以參考下列文章：
* [2-4. 部署 ASP.NET 網站應用程式](../../chapter02/04_deploy_aspnet_website.md)
* [2-5. 部署 PHP 網站應用程式](../../chapter02/05_deploy_php_website.md)
* [2-6. 部署 Python 網站應用程式](../../chapter02/06_deploy_python_website.md)
* [2-7. 部署 Node.js 網站應用程式](../../chapter02/07_deploy_nodejs_website.md)
* [2-8. 部署 Java 網站應用程式](../../chapter02/08_deploy_java_website.md)