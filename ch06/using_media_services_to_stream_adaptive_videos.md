# 製作動態位元率的影音串流服務

## 需求

想要提供影音串流的服務，但同時希望能夠根據條件（如：網路傳輸速度）動態調整串流影音的位元率，以提供順暢的播放串流體驗。

## 目標

完成後取得 HLS、MPEG-DASH 或是 SmoothStreaming 的 URL。

## 事前準備

* 擁有 Microsoft Azure 訂閱服務
* 需要串流的影音原始檔案

## 解決方法

### 保留編碼單位

如果我們要透過 Azure 媒體服務來轉檔，而且又是要轉成調適型位元率（adaptive bitrate），那就**一定要保留編碼單位**，因為預設的狀況是用整個服務共享的資源來編碼轉檔，而共享的資源無法處理 adaptive bitrate 的需求，所以需要來設定保留編碼單位，而保留的編碼單位會持續計費，所以不需要轉檔時可以再_把單位數調整為 0_，以確保沒有多花不必要的花費。

在媒體服務的管理介面中，到 _編碼_ 的頁面，選擇希望的保留單位類型，愈高等級代表轉檔編碼的速度愈快；再來就是在 _ENCODING_ 欄位選擇保留單位，如果同一時間只會轉檔一個檔案的話，只要保留一個單位就可以了。

![](https://skgitbook.blob.core.windows.net/azurerecipestw/ch06/reserve_encoding_unit.png)

_**圖 1**_ 保留編碼單位

設定完成，按下方的 _儲存_ 確認保留。

### 上傳影音並開始轉檔

_（下述的操作皆可以 Azure Media Service SDK 以程式完成，這裡介面透過網頁操作介面的方式來完成）_

在媒體服務的管理介面中，切換到 _內容_ 的頁面然後上傳要轉檔的影音檔案，這裡你可以從本機上傳，或者是從儲存體中取出檔案（建立媒體服務時都會要設定搭配的儲存體帳號）來處理，直接在網頁上從本機上傳的話，單檔最多只能 200MB，所以若有更大的檔案要處理，就要先把檔案上傳到儲存體。

最後，在 _內容名稱_ 欄位取一個好記的名稱作為識別。

![](https://skgitbook.blob.core.windows.net/azurerecipestw/ch06/uploading_media_file.png)

_**圖 2**_ 上傳影音檔案

上傳完成後，就可以在 _內容_ 的頁面中看到目錄媒體服務中的媒體內容：

![](https://skgitbook.blob.core.windows.net/azurerecipestw/ch06/media_content.png)

_**圖 3**_ 目前在媒體服務中的媒體檔案


這時點選剛才上傳的內容，然後點擊下方的 **處理序** 按鈕，就會跳出要編碼轉檔的設定，因為我們剛才保留的是標準的編碼單位，所以在**處理器**欄位選擇預設的 _Azure 媒體編碼器_ 就好了；而**編碼設定**就可以挑選不同的類型讓編碼器去轉檔，如果要做到動態調整畫質的服務，就要選擇有 _調適型位元速率_ 名稱的設定。最後，就是設定一個好記的名稱以記得編碼好的內容為何。

![](https://skgitbook.blob.core.windows.net/azurerecipestw/ch06/setting_encoding_job.png)

按下右下角的勾勾後，Azure 媒體服務便會開始啟動轉檔的工作，你可以在管理介面的 _工作_ 頁面觀看轉檔工作的狀態及進度。

![](https://skgitbook.blob.core.windows.net/azurerecipestw/ch06/encoding_job.png)

_**圖 4**_ 觀看目前轉檔編碼工作的狀態

接下來就是等待它編碼轉檔了，如果轉好檔案，你到對應的儲存體容器下就會看到原本一個檔案被壓了很多份不同的位元速率的檔案，但光這樣還不夠，目前還沒有提到動態封裝的機制，也就是稍後會提到的串流單位。

![](https://skgitbook.blob.core.windows.net/azurerecipestw/ch06/multiple_bitrate.png)

_**圖 5**_ 編碼完後產生的多個位元率的影音檔


### 設定串流單位

如果只是一個單一位元率的影音檔案，其實透過 Azure 媒體服務編碼轉檔後，也放在儲存體中，其實直接透過 URL 就能直接（漸進式）下載觀看。在我們使用調適型位元率的方式編碼轉檔完成後，還必須透過**動態封裝**的方式才能提供給播放影音的播放器有動態調整畫質的能力。

要能夠動態封裝，就必須使用**串流單位（streaming unit）**來進行，你可以到 _資料流端點_ 的頁面設定，你可以看到預設就有一個名稱為 _default_ 的端點，不過它的單位是 0，我們可以直接調整它來使用。

![](https://skgitbook.blob.core.windows.net/azurerecipestw/ch06/streaming_endpoint.png)

_**圖 6**_ 資料流端點

進入資料流端點的設定，為了要能動態封裝，至少要保留一個單位，而這個單位也會決定這個串流服務的頻寬大小，所以如果需要較高的頻寬就需要提高資料流單位的數量。

![](https://skgitbook.blob.core.windows.net/azurerecipestw/ch06/datastream_capacity_unit.png)

_**圖 7**_ 設定資料流單位，除了啟用動態封裝之外，也決定了串流的頻寬

決定單位數量後，可以按下下方的 **儲存** 按鈕確認變更。

### 發行內容

在編碼完成也轉好檔、也設定了資料流單位，接下來就是將內容發佈來取得播放的 URL 了。回到 _內容_ 的頁面，選擇編碼後的內容，然後按下下方的 **發行** 按鈕，完成發行後，就可以看到該內容有了 _發行 URL_。

![](https://skgitbook.blob.core.windows.net/azurerecipestw/ch06/publishing_content.png)

_**圖 8**_ 發行影音媒體內容

而這個 URL 所產出的是 SmoothStreaming 格式的串流 URL，如果你的播放器要吃不同的格式，其實只要在這個 URL 後面帶不同的參數即可，注意,都是在最後面加上 ```(format=...)``` 這樣格式的參數

* **SmoothStreaming**: http://gitbooksample.streaming.mediaservices.windows.net/5a61b321-72a4-4926-92e0-7145f38e43a5/WP_20150529_20_54_14_Pro.ism/Manifest
* **HLS (v4)**: http://gitbooksample.streaming.mediaservices.windows.net/5a61b321-72a4-4926-92e0-7145f38e43a5/WP_20150529_20_54_14_Pro.ism/Manifest(format=m3u8-aapl)
* **HLS (v3)**: http://gitbooksample.streaming.mediaservices.windows.net/5a61b321-72a4-4926-92e0-7145f38e43a5/WP_20150529_20_54_14_Pro.ism/Manifest(format=m3u8-aapl-v3)
* **MPEG DASH**: http://gitbooksample.streaming.mediaservices.windows.net/5a61b321-72a4-4926-92e0-7145f38e43a5/WP_20150529_20_54_14_Pro.ism/Manifest(format=mpd-time-csf)


這樣就可以開始提供串流服務了，你可以在 _內容_ 頁面利用下方的 **播放** 按鈕來啟動簡單的播放器測試，如果可以順利播放就表示這個發行沒有問題了。

![](https://skgitbook.blob.core.windows.net/azurerecipestw/ch06/play_adaptive_streaming.png)

_**圖 9**_ 測試串流播放的內容

當然，你隨時都可以取消發行內容。

## 參考資源

你也可以利用 [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) 這個工具來客製一個現成的播放器（而且支援動態調整畫質）；或是使用 [Player Framework](http://playerframework.codeplex.com/) 來自己打造播放器。

