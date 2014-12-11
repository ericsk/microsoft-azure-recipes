# 2.1 建立 Microsoft Azure 網站服務

若要把網站應用程式放在 Microsoft Azure 上運作，首先要建立一個網站的實體（instance），再把網站應用程式部署上來運作。這篇文章將介紹如何使用管理後台建立網站服務。

## 事前準備

* 已擁有 Microsoft Azure 訂閱帳戶。若尚未申請 Microsoft Azure 訂閱帳戶，請參考[這篇文章](../chapter01/01_signup.md)。

## 如何操作

首先開啟瀏覽器，開啟 https://manage.windowsazure.com/ 網頁，使用擁有 Microsoft Azure 訂閱帳戶的 Microsoft 帳號登入。登入成功後可以看到管理後台的畫面。

![Microsoft Azure 管理後台](http://i.imgur.com/IWF6Ddz.png)

接著，點擊左下角的_「新增」_，選_「計算」_ » _「網站」_，在 **URL** 的欄位中填入網站的網域名稱（Microsoft Azure 網站服務會配發一個 **XXX.azurewebsites.net** 的網址，這裡填入的就是 XXX），注意這裡會檢查名稱是否有其它使用者使用過，若出現綠色的勾勾則表示可以建立

![Microsoft Azure 管理後台的新增按鈕](http://i.imgur.com/YBMp7WX.png)

另外，**地區**的欄位可以讓您決定要將網站實體放在 Azure 於全球佈建的任何一個資料中心，而圖示中的_東亞_則是 Microsoft Azure 在香港佈建的機房。

![快速建立網站服務實體](http://i.imgur.com/RO6RF21.png)

最後，按下**建立網站**的按鈕，Microsoft Azure 便會開始建立網站實體，您可以看到下方在顯示進度。

![Microsoft Azure 正在建立網站的進度訊息](http://i.imgur.com/aYJcpL7.png)

建立完成後，您便能在網站服務的頁籤下看到剛才建立完成的網站實體，這樣一來，您便可以開始部署網站應用程式了。

![完成建立網站服務實體](http://i.imgur.com/uyNCzKc.png)


## 注意事項

* 透過這種方式建立的網站實體，預設是採用**免費**的價格方案，關於 Microsoft Azure 網站服務的價格方案，請參考[官網上的頁面](http://azure.microsoft.com/zh-tw/pricing/details/websites/ "Microsoft Azure 網站服務定價機制")。
* 不同的網站可以建立不同的網站實體來運作。
