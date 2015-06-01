# 4.2 手動上傳檔案到儲存體（BLOB）

這篇文章介紹如何將檔案上傳至 Microsoft Azure 的儲存體服務的 BLOB，同時瞭解如何存取檔案。

## 事前準備

* Microsoft Azure 儲存體帳號，可參考 [4.1 建立儲存體帳號](01_create_storage_account.md) 這篇文章來建立。
* (選擇性) 安裝免費且開源的 [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/) 工具，這篇文章會以此工具作為示範。

## 如何操作

開啟 **Azure Storage Explorer** 之後，按下 **Add Account** 的按鈕來新增 Azure 儲存體帳號以便操作。

![開啟 Azure Storage Explorer](https://skgitbook.blob.core.windows.net/azurerecipestw/4-2-1-azure-storage-explorer.png)

接下來會要求輸入儲存體帳號的資料，主要有兩個欄位要填寫：_Storage account name_ 是填寫儲存體帳號的名稱，而 _Storage account key_ 則是填寫存取金鑰（如果不知道在哪裡查詢這些資料，可以參考 [4.1 建立儲存體帳號](chapter04/01_create_storage_account.md)的內容）；而下方的 **Use HTTPS** 建議勾選起來，而在輸入完成後，可以先按一下 **Test Access** 的按鈕來確認是否連線成功，若確定沒有問題，則可以按下 **Save** 按鈕儲存設定。

![新增 Azure 儲存體帳號](https://skgitbook.blob.core.windows.net/azurerecipestw/4-2-2-setup-azure-storage-account.png)

新增帳號後，在 Azure Storage Explorer 上方的下拉選單選擇加入的帳號來管理，連線成功後，可以看到在左側視窗中有 _Blob Containers_、_Queues_ 以及 _Tables_ 三種資料結構，這就是 Microsoft Azure 儲存體服務提供的基本三種資料結構。

![Azure 儲存體帳號的資料結構](https://skgitbook.blob.core.windows.net/azurerecipestw/4-2-3-manage-storage.png)

而我們要把檔案放在儲存體中，就必須先建立**容器（container）**來放檔案，點選 _Blob Containers_ 上方會出現一個命令列，這時候可以按 **New** 按鈕建立一個新的容器，而建立容器除了要輸入名稱之外，還要決定這個容器的存取權限（Access Level）：

  * **Public Container**: 完全公開的容器，放在這個容器下的所有檔案都可以根據各自的 URL 直接存取。適用的情境像是網站上的靜態檔案如：CSS、JavaScript 或圖檔等，就可以建立一個公開的 Blob 容器來存放。
  * **Public Blob**: 放在此容器下的檔案一樣可以透過 URL 來存取，與 Public Container 的差別在於這個權限無法列舉容器內的所有檔案。適用情境像是讓使用者自行上傳且須公開存取的檔案，可以避免列舉容器內其它內容。
  * **Off (Private)**: 放在此容器下的檔案無法直接透過 URL 存取，必須使用存取金鑰再搭配 Azure Storage REST API 來存取，或是用程式產生_共享存取簽章_（SAS, Shared Access Signature）來存取。

![建立新的 Blob 容器](https://skgitbook.blob.core.windows.net/azurerecipestw/4-2-4-blob-container-access-level.png)

建立好容器後，就可以將檔案上傳至容器中，在 Azure Storage Explorer 的介面中，先在左側選擇欲上傳的容器，然後再到右側點擊 **Upload** 按鈕來上傳檔案。

![上傳檔案到 Blob 容器](https://skgitbook.blob.core.windows.net/azurerecipestw/4-2-5-upload-file-to-container.png)

檔案上傳完成後，可以在 Azure Storage Explorer 中點擊兩下來瀏覽或編輯檔案的相關資訊，像若是上傳圖檔時，可以確定一下 **Content Type** 是否設定正確（如：_image/png_ 或 _image/jpg_ 等）；而若要取得該檔案的 URL，也可以在這個對話盒中的 **Uri** 欄位找到。

![瀏覽檔案的關連資料](https://skgitbook.blob.core.windows.net/azurerecipestw/4-2-6-view-metadata.png)


## 參考連結

* [(MSDN) 限制對容器和 Blob 的存取](http://msdn.microsoft.com/zh-tw/library/azure/dd179354.aspx)

## 注意事項

* 雖然這篇以 Azure Storage Explorer 作示範，但不限定只有此工具可以操作 Azure 儲存體。