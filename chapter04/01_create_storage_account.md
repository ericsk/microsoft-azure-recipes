# 4.1 建立儲存體帳號

要使用 Microsoft Azure 儲存體服務，首先必須建立一個儲存體帳號，有了這個帳號之後，您就可以將 Blob、Table 或者是 Queue 類型的資料儲存在這個帳號下。

一個 Microsoft Azure 訂閱帳戶可以建立多個不同的儲存體帳號。

## 事前準備

* Microsoft Azure 訂閱帳戶。

## 如何操作

跟建立其它服務的方式一樣，首先進入 Microsoft Azure 的管理後台，點擊左下方的 **+新增**，接著選擇 

![建立儲存體帳號](https://skgitbook.blob.core.windows.net/azurerecipestw/4-1-1-create-storage-account.png)

在**URL** 的欄位輸入想要設定的儲存體帳號名稱，儲存體服務也會配發一個 **<帳號名稱>.\*.core.windows.net** 的 URL 供存取 Blob/Table/Queue 的資源，所以這個帳號名稱也不能與其它人重複；**位置/同質群組**則是設定要放儲存體的資料中心位置；而**複寫**的欄位則是讓您選擇資料的複本要備份在相同的資料中心，還是要跨資料中心來備份資料的複本（費用上的差異請參考[官網上的定價說明](http://azure.microsoft.com/zh-tw/pricing/details/storage/)）。最後按下右下角的建立按鈕完成建立儲存體帳號。

儲存體帳號建立完成後，可以在管理頁面中下方的工具列來取得**帳戶金鑰**、**管理網域**或是**刪除儲存體帳號**。

![管理儲存體按鈕](https://skgitbook.blob.core.windows.net/azurerecipestw/4-1-2-manage-storage-account.png)

**管理存取金鑰**中包含了要存取此儲存體帳戶的_帳號名稱_及_金鑰資訊_，當您透過一些管理工具來操作時，需要這個金鑰的資訊，若是金鑰不慎外流，可以點擊**重新產生**的按鈕重新產生金鑰。

![取得存取金鑰資訊](https://skgitbook.blob.core.windows.net/azurerecipestw/4-1-3-access-storage-key.png)

雖然儲存體服務會配發 URL，但有些應用情境會想設定自訂的網域名稱來對應，這時可以按下**管理網域**的按鈕來進行設定，對話盒上就會清楚的說明要如何設定。

![設定自訂網域](https://skgitbook.blob.core.windows.net/azurerecipestw/4-1-4-setting-custom-domain.png)

最後**刪除**的按鈕就是把這個儲存體帳戶整個刪除。

## 注意事項

* 使用儲存體服務因為會有費用產生，除非 Azure 訂閱帳戶有使用優惠（如：第一個月免費用、Azure Pass、MSDN 優惠等），否則必須**移除消費限制**。
* 除了透過 REST API 或是官方提供的 SDK 操作之外，在 MSDN 文件中有推薦一些可以管理儲存體帳戶的工具，可以參考[這頁說明](https://go.microsoft.com/fwLink/?LinkID=296841&clcid=0x7C04)。