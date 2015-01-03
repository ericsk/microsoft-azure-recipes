# 1.4 檢視帳單

使用 Azure 雲端服務，因為是_用多少付多少_的概念，所以看懂帳單對於成本的掌控是很重要的一件事，這篇文章將會介紹如何檢視並且瞭解 Microsoft Azure 的帳單。

## 事前準備

* 擁有 Microsoft Azure 訂閱，可以參考 [1.1 建立 Microsoft Azure 訂閱帳戶](chapter01/01_signup.md)來申請訂閱帳號。

## 如何操作

登入 [Microsoft Azure 的管理後台](https://manage.windowsazure.com/)，在右上角的帳號處按下選單，選擇**檢視我的帳單**。

![檢視帳單](https://skgitbook.blob.core.windows.net/azurerecipestw/1-4-1-click-view-bills.png)

點擊後準備進入帳單相關的頁面，因為涉及敏感資訊，所以會要求再驗證身份（再次登入帳號），進入帳單頁面後會列出該帳號下所有的訂閱帳戶，這時便可點擊其中一個訂閱來觀看帳單相關資料。下方的圖示是只有一個訂閱帳號的畫面。

![選擇訂閱帳號以檢視帳單](https://skgitbook.blob.core.windows.net/azurerecipestw/1-4-2-view-bills-by-subscriptions.png)

進入帳單畫面後，若您是第一個月免費試用、Azure Pass、Azure Open、或是擁有 MSDN、Enterprise Agreement 等其它優惠額度，在上方的進度列，或是右側都會顯示目前優惠額度的使用狀況，如下圖：

![優惠額度](https://skgitbook.blob.core.windows.net/azurerecipestw/1-4-3-bill-overview-page-benefit.png)

而若是正式帳號且是隨用即付的訂閱，看到的就是**目前這個帳單週期的預估花費**而不會有進度列，如下圖所示：

![隨用即付](https://skgitbook.blob.core.windows.net/azurerecipestw/1-4-4-bill-overview-page-payg.png)

而若是想要瞭解到底是用了哪些服務造成了多少花費，都可以在左下角的計量列表們看到計價的進度，以下圖為例，因為共享方案的網站服務在這個帳單週期目前已經累積 _633 小時_，所以換算的費用就是_新台幣 196 元_，其它費用以此類推。

![使用量與費用](https://skgitbook.blob.core.windows.net/azurerecipestw/1-4-5-consumption.png)

點擊計量條右側的圓圈就可以看到過去 10 天的記錄：

![使用量的統計資料](https://skgitbook.blob.core.windows.net/azurerecipestw/1-4-6-consumption-detail.png)

而若要更詳細的帳單資訊，可以在右側的功能列表中點選**下載使用情況詳細資料**，就可以得到一份 csv 檔案（可用 Excel 等軟體開啟）裡面詳實記載了這個訂閱帳號的每一筆花費。　

![下載詳細的帳單](https://skgitbook.blob.core.windows.net/azurerecipestw/1-4-7-download-bill-detail.png)

開啟下載的 CSV 檔案後，會看到密密麻麻的資訊，這些都是該訂閱帳號在這個計費週期中使用的每一項 Azure 服務所產生的相關費用，而費用的計算，首先就是在**計費**這一欄決定了每一項服務使用了多少資源（單位可以參考**單位**欄），然後再根據每一項服務的定價規則（也就是**費率**欄位）來計算出帳單費用。

![帳單詳細資料](https://skgitbook.blob.core.windows.net/azurerecipestw/1-4-8-bill.png)

這樣就能隨時掌握用了多少 Azure 服務而累積的花費了。

## 注意事項

* 如果對於帳單或是金額有任何疑問，都可以點選**連絡 Microsoft 支援服務**，然後選擇**帳務**相關問題，這些都是**完全免費**的，而建議您在地區選**台灣**、語言選擇**繁體中文**，您將可以在上班時間由說中文的台灣技術支援工程師來為您服務。