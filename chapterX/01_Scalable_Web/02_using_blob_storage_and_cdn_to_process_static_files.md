#  X-1-2. 使用 Blob 儲存體及 CDN 處理靜態檔案

Azure WEB 應用程式雖然提供了類似「本機磁碟」的檔案系統（根據不同的價格方案從 1GB 到 250GB 都有），但是在靜態檔案、網站產生的檔案、或是由網站使用者上傳的檔案，一般都建議使用 Azure 儲存體的 Blob 來處理。一來_檔案_與_應用程式_脫勾，不會讓存取本機檔案而造成網站難以延展，而且又可以把檔案全部交給儲存體處理而不佔用 WEB 機器的 CPU 運算資源，更可以結合 CDN 的服務讓使用者更快速地存取這些檔案，這篇文章將會介紹一個網站如何使用 Blob 儲存體，並且結合 CDN 來操作。

## 建立儲存體帳戶

這個部份可以參考這篇文章：
* [4-1. 建立儲存體帳號](../../chapter04/01_create_storage_account.md)

這裡示範加入前一篇文章中相同的資源群組步驟。首先打開前一篇建立的資源群組管理面板，點擊上方的**新增**按鈕，接著在_新增資源_的面板中選擇 **Storage**。

![在資源群組中新增儲存體](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-2-1-add-storage-into-resource-group.png)

接著在建立時填入儲存體**帳戶名稱**（也會設定搭配 _\*.core.windows.net_ 的 URL）、根據價格及備援考量選擇**定價層**即可。

![在資源群組中新增儲存體](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-2-2-creating-storage-account.png)


## 規劃適用儲存體處理的檔案

一個網站應用程式最適合（也是最快能）使用 Blob 儲存體處理的檔案像是：

* CSS、JavaScript、圖片檔案等這些在網站部署時就不會修改的靜態檔案。
* 由網站產生的檔案，比如說使用者完成交易後的收據（invoice.pdf）、報表檔案等。
* 經由使用者上傳的檔案、圖片或影像等檔案。

### 處理 CSS、JavaScript 或圖片檔等靜態檔案
像 CSS、JavaScript 這些網站部署前就存在的靜態檔案，可以在網站部署時，同時將這些檔案上傳至 Azure 儲存體的 Blob 容器中，接著取得 URL 替換掉原本的存取路徑，比方說原本的 HTML 檔案內容可能像是這樣：

```html 
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    ...
    <link rel="stylesheet" href="/css/site.css">
    <link rel="stylesheet" href="/css/index.css">
  </head>
  <body>
    ...
    <img src="/img/hero-banner.png" alt="Hero banner" width="960" height="550">
    ...
    ...
    <script src="/js/jquery.min.js"></script>
    <script src="/js/index.min.js"></script>
  </body>
</html>
```

這時可以將 ```/css```、```/img``` 以及 ```/js/``` 目錄下的檔案全部上傳至 Blob 的容器中（上傳檔案的部份可以參考 [4-2. 手動上傳檔案到儲存體（BLOB）](../../chapter04/02_manual_upload_files_to_storage_blob.md) 一文），假設容器的 URL 為 ```https://gitbooksample.blob.core.windows.net/css```、 ```https://gitbooksample.blob.core.windows.net/img``` 以及  ```https://gitbooksample.blob.core.windows.net/js```，那上面的 HTML 程式碼就可以將 CSS、JavaScript 以及圖片檔案的路徑修改成：

```html 
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    ...
    <link rel="stylesheet" href="//gitbooksample.blob.core.windows.net/css/site.css">
    <link rel="stylesheet" href="//gitbooksample.blob.core.windows.net/css/index.css">
  </head>
  <body>
    ...
    <img src="//gitbooksample.blob.core.windows.net/img/hero-banner.png" alt="Hero banner" width="960" height="550">
    ...
    ...
    <script src="//gitbooksample.blob.core.windows.net/js/jquery.min.js"></script>
    <script src="//gitbooksample.blob.core.windows.net/js/index.min.js"></script>
  </body>
</html>
```

這樣使用者的瀏覽器在瀏覽這一頁時，就會去 Blob 儲存體中抓取這些檔案，而不必都是對 WEB 應用程式發送存取要求。

### 處理網站產生或是由使用者上傳的檔案

如果網站應用程式中需要產生檔案儲存下來，也可以把產生的檔案先儲存在本機磁碟中，再上傳至儲存體中（如果產生檔案需要較久的時間，建議搭配使用稍後會提到的 WebJobs 的機制），關於如何用程式將檔案上傳至 Azure 儲存體中，可以參考下列文章：

* [4-3. 上傳檔案至 BLOB 儲存體（.NET）](../../chapter04/03_upload_file_to_blob_storage_dotnet.md)

## 使用 Azure CDN

如果已經使用上述的方式將檔案移至 Azure 儲存體中，雖然可以透過 URL 直接存取，但如果想用運用 [Azure CDN](http://azure.microsoft.com/zh-tw/services/cdn/) 更多[在地機房有節點](https://msdn.microsoft.com/library/azure/gg680302.aspx)的好處（以台灣而言，雖然目前最近的資料中心是東亞機房，但 Azure CDN 在高雄有節點），以節省網路傳輸的時間，可以設定一個 Azure CDN 的服務來快取 Azure 儲存體，再透過 Azure CDN 所提供的 URL 來存取檔案。

使用 Azure CDN 非常簡單，只需要在建立 Azure CDN 服務時設定要快取的儲存體帳戶即可，目前要建立 Azure CDN 帳號必須回到[完整的管理後台](https://manage.windowsazure.com/)中進行操作。

![建立 Azure CDN 服務](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-2-3-creating-azure-cdn.png)

完成建立後，Azure CDN 就會配一個網域名稱供你使用（一樣可以自訂網域），在儀表板中找到 CDN 端點的資訊，如果沒有設定自訂網域名稱的話，也可以直接使用這個網域名稱。

![Azure CDN 端點位址](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-2-4-azure-cdn-settings.png)

而這個端點位址的功用就是可以替換 Blob 儲存體中每個 Blob URL 的網域名稱（維持相同的路徑名），這樣就不是直接從資料中心拉資料，而是從 Azure CDN 的節點來存取了。舉例來說，上述的 HTML 檔案在使用 Azure CDN 來快取 Blob 儲存體的話，就可以修改為：

```html 
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    ...
    <link rel="stylesheet" href="//az743383.vo.msecnd.net/css/site.css">
    <link rel="stylesheet" href="//az743383.vo.msecnd.net/css/index.css">
  </head>
  <body>
    ...
    <img src="//az743383.vo.msecnd.net/img/hero-banner.png" alt="Hero banner" width="960" height="550">
    ...
    ...
    <script src="//az743383.vo.msecnd.net/js/jquery.min.js"></script>
    <script src="//az743383.vo.msecnd.net/js/index.min.js"></script>
  </body>
</html>
```

來讓瀏覽器對 Azure CDN 拉資料而不是從資料中心來存取。

