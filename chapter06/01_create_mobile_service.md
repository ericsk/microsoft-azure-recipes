# 6.1 建立行動服務

要使用 Azure 行動服務平台，首先要先瞭解如何建立 Azure 行動服務的空間。

## 事前準備

* 擁有 Microsoft Azure 訂閱帳號，可參考 [1.1 建立 Microsoft Azure 訂閱帳戶](chapter01/01_signup.md)來建立。
* （選擇性）瞭解 Azure SQL Database 服務，可參考 [SQL Database 服務](chapter05/README.md)。
* （選擇性）瞭解行動平台（如：Windows、iOS、Android 等） app 的開發。

## 如何操作

進入 Microsoft Azure 的管理後台，在下方命令列點擊「_+ 新增_」，選擇 _計算_ » _行動服務_ » _建立_：

![建立行動服務](https://skgitbook.blob.core.windows.net/azurerecipestw/6-1-1-create-mobile-service.png)

接下來會出現建立行動服務的對話盒，在第一部份，首先要在**URL**的欄位讓 app 介接的 URL 位址，這裡要取一個全球唯一的名稱（因為會配一個 _.azure-mobile.net_ 的網域）；接著在**資料庫**的欄位指定這個行動服務要使用的 SQL Database，要使用既有或是建立一個全新的都可以；**地區**的欄位就是這個行動服務要放的 Azure 機房位置；**後端**欄位是選擇要在 Azure 行動服務上撰寫自訂程式時，要採用哪一種程式語言，目前有 _JavaScript_ 及 _.NET_ 可以選擇。**推播設定**的部份稍候再處理。

![建立行動服務 - 步驟一](https://skgitbook.blob.core.windows.net/azurerecipestw/6-1-2-create-mobile-service-step1.png)

如果在第一個步驟時選擇建立新的 SQL 資料庫，對話盒就會出現第二個步驟來建立 SQL Database，可參考 [5.1 建立 SQL Database](chapter05/01_create_sql_database.md)的說明瞭解如何建立 SQL Database。

![建立行動服務 - 步驟二](https://skgitbook.blob.core.windows.net/azurerecipestw/6-1-3-create-mobile-service-step2.png)

一切都設定完成後，按下右下角的勾勾按鈕，Microsoft Azure 便會開始建立 Azure 行動服務了。