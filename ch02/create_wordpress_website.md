# 架設 WordPress 網站

## 需求

在 Microsoft Azure 上架設 WordPress 網站。

## 事前準備

  * 初步認識 Microsoft Azure 應用程式服務。
  * 瞭解如何[架設靜態網站](create_a_static_website.md)。

## 解決方法

### 建立 WordPress 服務

進入 Microsoft Azure （預覽版）[管理後台](https://portal.azure.com/)，在左側的面板中找到 **新增** 的按鈕，然後選擇 _Marketplace_。

![從 Marketpace 新增服務](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/create_from_marketplace.png)

_**圖 1**_. 從市集建立服務


在市集的搜尋欄位中，搜尋 WordPress 關鍵字，這裡會看到有許多不同版本或社群修改過的 WordPress，如果沒有特定需求，可以先選擇一般的 **WordPress** 就好。

![在 Marketplace 中搜尋 WordPress](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/marketplace_search_wordpress.png)

_**圖 2**_. 搜尋 WordPress

點選由 WordPress 提供的 WordPress 後按下建立，因為這個範本是使用 Azure 應用程式服務來建立，所以也要設定像是名稱、價格方案、資源群組等相關欄位：

![設定應用程式服務來架設 WordPress](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/creating_wordpress_host.png)

_**圖 3**_. 設定應用程式服務來架設 WordPress

大部份的設定欄位可以參考「[架設靜態網站](create_a_static_website.md)」這篇文章的內容介紹，而這裡不同的部份是，因為 WordPress 使用 PHP + MySQL，Azure Web 應用程式本身就支援 PHP 沒有問題，但 MySQL 的部份就要使用 Azure 合作夥伴 ClearDB 提供的服務，而這裡的建立面板就可以直接設定資料庫所在的位置，以及要使用的方案：

![設定 MySQL 的地區及價格](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/setting_mysql_plan.png)

_**圖 4**_. 設定 MySQL 的地區及價格

一切設定完成後（別忘了都要按下下方的 **選取** 按鈕確定設定無誤），因為有用到合作夥伴（ClearDB）的服務，所以要確認一下使用條款，點進去看完條款聲明後按下確認即可。

![接受 ClearDB 的法律條款](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/accept_cleardb_terms.png)

_**圖 5**_. 接受 ClearDB 的法律條款

最後按下 **建立** 的按鈕即可開始部署 WordPress 的服務。

### 設定 WordPress 服務

直接開啟網址，就會進入第一次安裝設定 WordPress 的畫面，順著它的步驟把 WordPress 設定起來。

![設定安裝 WordPress](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/setup_wordpress.png)

_**圖 6**_. 設定安裝 WordPress

如果覺得網站執行速度不是很理想的話，可以回到 Azure 管理後台，然後在這個部落格的網站管理中，調整方案來調整網站的運算資源。

![調整售價方案](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/scaling_blog.png)

_**圖 7**_. 調整售價方案


### 管理 MySQL 資料庫

在（預覽版）管理後台裡也可以打開 MySQL 服務的管理面板，在這裡管理面板中可以看到一些目前 MySQL 資料庫的使用狀況。

![MySQL 管理面板](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/mysql_panel.png)

_**圖 8**_. MySQL 管理面板

而如果要進階的管理，就按下面板上方的 **管理資料庫**，就會開啟 ClearDB 網站的管理畫面來進行管理，你也可以在這裡調整資料庫的價格方案。

![cleardb 的管理畫面](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/cleardb_mgmt.png)

_**圖 9**_. cleardb 的管理畫面

