# 7.2 上傳影音檔案編碼及發行串流

手上的多媒體影音檔案可以藉著 Azure 媒體服務提供的平台來進行針對不同使用情境的編碼作業，並且直接發行成串流播放的形式，或是針對 iOS 裝置產生 HLS 的播放串流資訊等等。

## 事前準備

* 已經建立好 Azure 媒體服務的空間，可參考 [7.1 建立媒體服務](01_create_media_service.md)的說明來建立。
* （選擇性）瞭解 Azure 儲存體服務，並且熟悉上傳檔案至 Blob 儲存體，可參考  [4.2 手動上傳檔案到儲存體（BLOB）](../chapter04/02_manual_upload_files_to_storage_blob.md)的說明。

## 如何操作

進入 Azure 的管理後台，並且開啟已經建立好的 Azure 媒體服務管理介面，點擊下方命令列的**上傳**按鈕來上傳影音檔案。

![上傳影音檔案](https://skgitbook.blob.core.windows.net/azurerecipestw/7-2-1-clicke-upload-command.png)

接下來可以看到上傳的對話盒，可以選擇**從本機**上傳檔案，或者是從（_同一個訂閱帳戶下，**不一定**要跟建立媒體服務時建立的儲存體相同_）儲存體拉檔案進來，因為從本機上傳檔案的大小限制為 **200MB**，所以更大的影音檔案就得先上傳至 Azure 儲存體再拉進來。而支援的影音檔案格式，可以點擊對話盒上的[**深入了解**](https://go.microsoft.com/fwLink/?LinkID=296860&clcid=0x7C04)的連結查詢。

![上傳影音檔案的對話盒](https://skgitbook.blob.core.windows.net/azurerecipestw/7-2-2-upload-media-file.png)

如果選擇**從儲存體**拉檔案，就會顯示另一個對話盒來選擇要從哪個儲存體帳戶來上傳多媒體檔案。

![從儲存體上傳檔案](https://skgitbook.blob.core.windows.net/azurerecipestw/7-2-3-upload-from-storage.png)

選定好要上傳的檔案之後，可以在**內容名稱**的欄位設定這個多媒體影音檔案的名稱，最後按下右下角的勾勾按鈕就可以開始上傳檔案了。**這個檔案就會儲存在建立媒體服務時選擇或新建的儲存體帳戶之中**。

![設定內容名稱](https://skgitbook.blob.core.windows.net/azurerecipestw/7-2-4-ready-to-upload.png)

上傳完畢，如果不需要轉檔就打算直接發行的話，可以直接按下下方命令列的**發行**命令，開始提供這個檔案的串流服務。

![發行媒體內容](https://skgitbook.blob.core.windows.net/azurerecipestw/7-2-5-publish-media-file.png)

發行成功後，就可以在內容列表中取得發行後的 URL，這就可以直接接上播放器來使用。若要取消發行也可以再透過下方命令列的**取消發行**按鈕來操作。

![發行的 URL](https://skgitbook.blob.core.windows.net/azurerecipestw/7-2-6-media-file-published.png)

而如果要將上傳的影音檔案，根據不同的使用情境來重新編碼，可以透過下方命令列的**編碼**命令按鈕來處理，選擇要編碼的檔案，按下編碼的命令，就會出現對話盒要你選擇欲編碼的格式：

![選擇編碼的使用情境](https://skgitbook.blob.core.windows.net/azurerecipestw/7-2-7-encode-media-file.png)

選擇好編碼的格式，也設定好名稱之後，Azure 媒體服務就會開始**排程**來進行編碼轉檔，在預設的狀況下都是由 Azure 媒體服務使用共用的資源、排定時程來轉檔，如果需要更快的轉檔效率或更短的排程，可以在管理介面切換至**編碼**的頁面，來設定保留的編碼服務，這樣 Azure 媒體服務便會保留虛擬機器（可以選擇 Basic, Standard, Premium 三種不同等級的虛擬機器）供您專屬使用，來提升轉檔的效能（當然這也比起使用共用資源需要較多的花費）。

![選擇保留機器來進行編碼](https://skgitbook.blob.core.windows.net/azurerecipestw/7-2-8-reserve-vm-for-encoding.png)

確定要進行編碼後，Azure 媒體服務會立刻產生一個_轉檔工作_，這時可以切換至管理介面的**工作**頁面來檢視進度，一旦工作完成之後，便能對它進行其它操作（例如：發行）。

![檢視工作清單](https://skgitbook.blob.core.windows.net/azurerecipestw/7-2-9-schedule-encoding-task.png)

## 注意事項

* 關於影音編碼時選擇的機器等級及價格差異，可以參考官方的[定價頁面](http://azure.microsoft.com/zh-tw/pricing/details/media-services/)。