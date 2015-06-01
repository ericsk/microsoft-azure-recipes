# 7.1 建立媒體服務

要使用媒體服務的功能或平台，就要在 Microsoft Azure 的管理後台建立一個媒體服務的空間來操作。這篇食譜便是介紹一步步建立媒體服務的步驟。

## 事前準備

* 已開通 Microsoft Azure 訂閱，可參考 [1.1 建立 Microsoft Azure 訂閱帳戶](../chapter01/01_signup.md)來建立。
* 瞭解 Azure 儲存體服務。

## 如何操作

登入 Microsoft Azure 的[管理後台](https://manage.windowsazure.com)，點擊左下角的「_+ 新增_」，選擇_應用程式服務_ » _媒體服務_ » _快速建立_：

![建立媒體服務](https://skgitbook.blob.core.windows.net/azurerecipestw/7-1-1-create-media-service.png)

在**名稱**的欄位輸入媒體服務的名稱，由於這個名稱會決定影音串流的 URL 位址，因此也必須是全球唯一的，所以在輸入完畢時會檢查名稱是否可用；在**地區**的欄位選擇要在 Azure 哪座資料中心建置媒體服務；而建立媒體服務時，需要一個儲存體帳戶來儲存多媒體影音檔案（上傳的或是媒體服務產生的），可以選擇既有的儲存體帳戶，或是新建一個。所有欄位都填寫正確後，按下右下角的**建立媒體服務**就會開始建立 Azure 媒體服務了。

看到類似以下的畫面就建立完成了。

![建立媒體服務](https://skgitbook.blob.core.windows.net/azurerecipestw/7-1-2-media-services-created.png)
