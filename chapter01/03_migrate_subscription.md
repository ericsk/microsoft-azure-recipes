# 1.3 將試用帳戶或 Azure Pass 轉成正式帳號

不論是自己拿信用卡註冊免費試用帳號，或是使用 Azure Pass 開通的試用帳號，在試用期間快到期時都會提示你轉換成正式訂閱帳戶，因為如果不轉換，在帳號到期後，原本在這個訂閱帳戶的服務就會被中止。所以，如果要讓這些服務繼續延用，建議在試用帳號到期前進行轉換。（**轉換後，原本試用期的優惠金額不會取消，會持續到原本的到期日**）

## 如何操作

在試用帳號到期前，在管理後台的右上角點選帳號，於下拉式選單上選擇**檢視我的帳單**。

![選擇檢視帳單](https://skgitbook.blob.core.windows.net/azurerecipestw/1-3-1-view-my-bill.png)

在試用的訂閱帳戶下，會有一個訊息顯示即將到期的訊息，點擊這個訊息就可以進行轉換。

![升級試用帳戶](https://skgitbook.blob.core.windows.net/azurerecipestw/1-3-2-upgrade-subscription.png)

點擊後，會跳出一個說明的對話盒，確認升級帳戶的選項，也可以修改訂閱帳戶名稱（預設設定為_隨用即付_）。

![確定升級以及設定訂閱帳戶名稱](https://skgitbook.blob.core.windows.net/azurerecipestw/1-3-3-confirm-upgrades.png)

確認升級完成後，如果原本的帳戶下已經建立了需要支付費用的服務，例如：_虛擬機器_、_儲存體_、_SQL 資料庫_等，這時**訂閱帳戶的消費限制是被取消的**，如果想要開啟**消費限制**，則必須先將付費的服務刪除，才能再回到這一頁開啟消費限制。

![如果正在使用付費服務，則無法開啟消費限制](https://skgitbook.blob.core.windows.net/azurerecipestw/1-3-4-spend-limit-disabled.png)

## 注意事項
* 若開啟**消費限制**，Microsoft Azure 不會向您收取任何費用，但相對地，也就不能開啟需要付費的服務，而原本就有免費價格方案的服務（如：網站、行動服務）則不受影響。
