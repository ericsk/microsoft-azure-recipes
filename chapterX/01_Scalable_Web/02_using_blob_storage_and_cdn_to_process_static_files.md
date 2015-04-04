#  X-1-2. 使用 Blob 儲存體及 CDN 處理靜態檔案

Azure WEB 應用程式雖然提供了類似「本機磁碟」的檔案系統（根據不同的價格方案從 1GB 到 250GB 都有），但是在靜態檔案、網站產生的檔案、或是由網站使用者上傳的檔案，一般都建議使用 Azure 儲存體的 Blob 來處理。一來_檔案_與_應用程式_脫勾，不會讓存取本機檔案而造成網站難以延展，而且又可以把檔案全部交給儲存體處理而不佔用 WEB 機器的 CPU 運算資源，更可以結合 CDN 的服務讓使用者更快速地存取這些檔案，這篇文章將會介紹一個網站如何使用 Blob 儲存體，並且結合 CDN 來操作。

## 建立儲存體帳戶

這個部份可以參考這篇文章：
* [4-1. 建立儲存體帳號](../../chapter04/01_create_storage_account.md)
* [4-2. 手動上傳檔案到儲存體（BLOB）](../../chapter04/02_manual_upload_files_to_storage_blob.md)

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

這時可以將 ```/css```、```/img``` 以及 ```/js/``` 目錄下的檔案全部上傳至 Blob 的容器中，假設容器的 URL 為 ```https://gitbooksample.blob.core.windows.net/css```、 ```https://gitbooksample.blob.core.windows.net/img``` 以及  ```https://gitbooksample.blob.core.windows.net/js```，那上面的 HTML 程式碼就可以修改成：

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

## 使用 Azure CDN