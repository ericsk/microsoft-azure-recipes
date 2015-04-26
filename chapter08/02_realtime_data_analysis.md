# 8.2 即時分析輸入的大量資料

[前一篇](01_collect_data_from_iot_devices.md)介紹了從 IoT 裝置來的大量資料可以藉由 Event Hubs 來佇列傳輸，再由其它的程式將佇列中的資料儲存至其它儲存環境，若希望在資料進 Event Hubs 時就即時地針對這些資料做處理（可能等不及寫入儲存），這時就能利用 [Azure Stream Analytics](http://azure.microsoft.com/zh-tw/services/stream-analytics/) （資料流分析）服務來完成。

![Azure Stream Analytics](https://skgitbook.blob.core.windows.net/azurerecipestw/8-2-1-azure-stream-analytics.png)

## 使用 Azure Stream Analytics (資料流分析)

### 建立 Azure 資料流分析工作

在 Microsoft Azure 管理後台，點擊左下角的_「+ 新增」_，選擇_「資料服務」_ » _「串流分析」_ 就可以設定名稱、選擇資料中心並設定搭配的儲存體帳戶，就能快速建立一個 Azure 資料流分析的工作。

![建立 Azure Stream Analytics](https://skgitbook.blob.core.windows.net/azurerecipestw/8-2-2-creating-stream-analytics.png)

### 新增資料流分析工作監控 Event Hub 內的資料

建立好 Azure 資料流分析後，可以在管理頁面中的**輸入**頁籤加入要監控的資料來源。

![建立 Azure Stream Analytics](https://skgitbook.blob.core.windows.net/azurerecipestw/8-2-3-adding-stream-input.png)

點擊**加入輸入**後會出現一個對話盒，這裡我們選擇加入**資料流（stream）**。

![選擇資料流](https://skgitbook.blob.core.windows.net/azurerecipestw/8-2-4-adding-stream.png)

下一步選擇資料流的來源，這裡因為我們選擇**事件中心（event hubs）**。如果希望 Azure Stream Analytics 服務支援更多的資料流來源，您可以利用下方的 [UserVoice 連結（讓我們知道）](http://feedback.azure.com/forums/270577-azure-stream-analytics)來提出建議。

![選擇資料流來源](https://skgitbook.blob.core.windows.net/azurerecipestw/8-2-5-selecting-stream-source.png)

接著是選擇要監控的 event hubs，以及這個分析工作的名稱，權限及取用者群組的部份就根據需求來設定。

![選擇事件中心](https://skgitbook.blob.core.windows.net/azurerecipestw/8-2-6-selecting-event-hub.png)

最後一步，為了讓 Azure 資料流分析認得傳入 event hub 的資料是什麼_格式_（目前支援 _Avro_、_CSV_ 及 _JSON_）及_字元編碼_，在建立前可以先做設定（事後再到管理頁面修改也可以）。

![設定傳入 event hub 的資料格式](https://skgitbook.blob.core.windows.net/azurerecipestw/8-2-7-configuring-data-format.png)

這些設定完成後就建好了資料流分析工作。

### 設定資料流分析工作的輸出位置

在開始設定分析工作之前，可以先設定好當分析工作結束後要將結果輸出到哪一個儲存環境，在 Azure Stream Analytics 的服務管理頁面，選擇**輸出**的頁籤開始建立輸出位置。

![設定分析工作的輸出位置](https://skgitbook.blob.core.windows.net/azurerecipestw/8-2-8-adding-output.png)

輸出的位置可以選擇 _SQL 資料庫_、_BLOB 儲存體_、_事件中心 (Event Hubs)_ 以及 _Table 儲存體_。如果希望 Azure Stream Analytics 支援更多的輸出位置，可以到下方 [UserVoice 連結（讓我們知道）](http://feedback.azure.com/forums/270577-azure-stream-analytics)提出建議。

![選擇分析工作的輸出位置](https://skgitbook.blob.core.windows.net/azurerecipestw/8-2-9-selecting-output.png)

若選擇 _BLOB 儲存體_就再設定相關的資訊，最後再輸出資料格式以及字元編碼就可以完成建立。

![輸出至 BLOB 儲存體](https://skgitbook.blob.core.windows.net/azurerecipestw/8-2-10-output-to-blob-storage.png)

### 設定查詢工作

Azure Stream Analytics 提供一種類似 SQL 查詢語法的方式讓你設定在資料流的分析工作中，在管理頁面中選擇**查詢**的頁籤就可以設定，然後用 ```INTO``` 子句將結果送到前面設定的輸出位置，用 ```FROM``` 設定資料來源（使用設定的別名）。所以設定的查詢語法可能會像是這樣：

	SELECT 
		DeviceId, HighTemperature 
	INTO 
		output-to-blob 
	FROM
		mydataanalytic

其中 _output-to-blob_ 是剛才設定的輸出位置，而 _mydataanalytic_ 則是資料流來源。（這表示你可以設定多組來源及輸出位置來使用）

![設定資料流分析的查詢](https://skgitbook.blob.core.windows.net/azurerecipestw/8-2-11-configuring-the-query.png)

### 啟動工作

在 Azure Stream Analytics 的管理頁面下方工作列按下**開始**的按鈕便可以啟動資料流分析工作，而要停止時也是在相同的地方按下停止按鈕。而啟動工作後，如果進 Event Hub 的資料符合設定的查詢條件，就會根據設定將資料輸出到設定的位置。

## 參考資料

* [Azure 資料流分析簡介](http://azure.microsoft.com/zh-tw/documentation/articles/stream-analytics-introduction/)
* [開始使用 Azure 資料流分析](http://azure.microsoft.com/zh-tw/documentation/articles/stream-analytics-get-started/)
* [Azure 資料流分析查詢語言參考](https://msdn.microsoft.com/zh-tw/library/dn834998.aspx)