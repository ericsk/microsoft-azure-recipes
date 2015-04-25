# 8.1 從 IoT 裝置中蒐集大量的資料

不論您是使用什麼技術或平台開發 IoT 前端裝置，蒐集來的資料總是要找個儲存環境，Microsoft Azure 提供了多種適合於巨量資料的儲存服務，讓開發人員能夠根據資料的特性來選擇要使用儲存體、SQL 資料庫或是 HDInsight（Azure 上的 Hadoop 平台）等。在開始處理這些資料前，必須先瞭解如何蒐集這些從 IoT 裝置送來的資料。

## 使用 Event Hubs 佇列高頻資料

想像一種 IoT 情境 -- 你佈建了很多感測器，而它們不斷傳送大量的資料出來，如果讓這些感測器直接將資料寫入儲存體，I/O 寫入的速度可能追不上資料產生的速度，[Event Hubs](http://azure.microsoft.com/zh-tw/services/event-hubs/) 就是為了能在短時間處理大量資料（如：每秒數百萬計）的佇列（queue）服務，它提供簡單的讀寫操作，而且通用的網路通訊協定（HTTP、AMQP），讓感測器可以很快地將資料先送到 Event Hubs 中（而且還不限前端 IoT 裝置使用何種技術平台），然後在時效之前將這些資料取出寫進（永久）儲存體中，這可以幫助開發人員節省力氣處理資料頻寬的問題。

![Event Hubs](https://skgitbook.blob.core.windows.net/azurerecipestw/8-1-1-send-recv-events.png)


### Event Hubs 的技術

![Event Hubs 與 Service Bus](https://skgitbook.blob.core.windows.net/azurerecipestw/8-1-2-event-hubs-in-service-bus.png)

Event Hubs 是 [Azure Service Bus](http://azure.microsoft.com/zh-tw/services/service-bus/)（服務匯流排）中的一個特殊的佇列服務，連線與身份驗證的部份與 Service Bus 其它的服務一致，但是佇列結構有些不同，在 Event Hubs 中有**分割 (partition)** 的概念，這與 Event Hubs 能處理資料的頻寬有關，愈多的分割區就能提供更高的資料處理頻寬。你可以在 Event Hubs 中建立 8 ~ 32 個分割。

![Event Hubs 的資料分割](https://skgitbook.blob.core.windows.net/azurerecipestw/8-1-3-event-hubs-partitions.png)

### 建立 Event Hubs 服務

在 Microsoft Azure 的管理後台，點擊左下角的_「+ 新增」_，選擇_「應用程式服務」_ » _「服務匯流排」_ » _「事件中心」_ 來快速或自訂建立。

![建立 Event Hubs](https://skgitbook.blob.core.windows.net/azurerecipestw/8-1-4-create-event-hubs.png)

除了輸入**事件中心名稱**、設定所在的資料中心之外，你也可以放在既有的服務匯流排（Service Bus）中或是建立新的服務匯流排。

![自訂建立 Event Hubs](https://skgitbook.blob.core.windows.net/azurerecipestw/8-1-5-creating-event-hub.png)

### 設定存取原則

在使用 Event Hubs 之前，我們可以在管理後台設定不同的存取原則，比方說 IoT、感測器這些裝置若只是要將資料寫入 Event Hubs，那可以給予它們傳送的權限，而後端處理資料的程式也許只需要接收的權限等等，在 Event Hubs 的後台設定存取原則後，每一個原則都配置唯一的存取金鑰，用來進行 Event Hubs 的操作。

![設定 Event Hubs 的存取原則](https://skgitbook.blob.core.windows.net/azurerecipestw/8-1-6-configuring-access-rules.png)

以上圖為例，就是設定了兩個存取原則：**SendRule** 與 **ReceiveRule**，分別只有**傳送**與**接聽**的權限（你也可以設定一個原則是包含_管理_、_傳送_或_接聽_的權限），而不同的原則就會有不同的金鑰，這些金鑰是在操作 Event Hubs 時用來產生_共用存取簽章（SAS, Shared Access Signature）_使用，關於 Azure 服務匯流排產生 SAS 的方式，可以參考[使用服務匯流排的共用存取簽章驗證](https://msdn.microsoft.com/zh-tw/library/azure/dn170477.aspx)這篇文章。


### 將資料送至 Event Hubs 中

若是使用 .NET 進行開發，可以直接使用 Microsoft ServiceBus 函式庫（可透過 NuGet 安裝 **Microsoft Azure Service Bus**）的 ```EventHubClient``` 物件來操作；而若是非 .NET 的程式語言可以使用 **Advanced Message Queuing Protocol (AMQP)** 的通訊協定，或是 [Apache Qpid](http://qpid.apache.org) 這個專案將資料送至 Event Hubs。

每個傳送至 Event Hubs 的單筆資料（single event）大小限制是 **256KB**，你可以一筆一筆資料傳，或是批次處理，不過要注意 Event Hubs 一個單位的頻寬為 _1MB/sec_ 或 _1000 events/sec_。

關於傳送資料到 Event Hubs 的範例，可以參考 [Get started with Event Hubs](http://azure.microsoft.com/documentation/articles/service-bus-event-hubs-csharp-ephcs-getstarted/) 這篇文章。

### 將資料從 Event Hubs 中取出儲存或分析

資料送進 Event Hubs 後只會保存一段時間（可以在管理後台設定），所以不論要分析還是要永遠儲存下來，都還得寫另外一隻程式來取出資料，Event Hubs 會建立_取用者群組（Consumer Group）_來分配分割內的資料，而撰寫的程式就是連接到一個取用者群組（一個取用者群組也只能被一隻程式連結）來讀取放在分割中的資料。

![取出 Event Hubs 分割內的資料](https://skgitbook.blob.core.windows.net/azurerecipestw/8-1-7-consumer-group.png)

而 Event Hubs 讀取的頻寬為 _2MB/sec_。

## 參考資料

* [事件中心概觀](https://msdn.microsoft.com/zh-tw/library/azure/dn836025.aspx)
* [事件中心定價機制](http://azure.microsoft.com/zh-tw/pricing/details/event-hubs/)