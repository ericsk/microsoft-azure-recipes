# X-1-1 建立網站應用程式及使用 SQL 資料庫

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
