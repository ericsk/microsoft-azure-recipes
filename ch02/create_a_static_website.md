# 架設靜態網站

## 需求

想要架設一個基本的靜態網站，可以自己上傳網站檔案，並且能有公開的網址。

## 事前準備

* 擁有 Microsoft Azure 訂閱帳號。

## 解決方法

### 建立網站空間

使用您擁有 Microsoft Azure 訂閱帳號的 Microsoft 帳號登入 [Microsoft Azure 的管理後台](https://portal.azure.com/)（預覽版本），在左側的面板中找到 **新增** 的按鈕，按下新增按鈕後選擇 _Web + 行動_ > _Web 應用程式_ 準備來建立一個網站空間來放要架設的網站。

![建立 Web 應用程式](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/create_a_webapp.png)
_**圖 1**_. 建立 Web 應用程式

接著是設定網站空間的相關設定，首先是這個網站的名稱，由於 Microsoft Azure 會根據設定的名稱給一組 _名稱.azurewebsites.net_ 的網域用來存取網站，所以輸入名稱時也會檢查這個名稱是不是全球唯一的，如果輸入完看到輸入框最後有綠色的勾勾就是了。

![輸入 Web 應用程式名稱](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/create_a_webapp_name.png)
_**圖 2**_. 輸入 Web 應用程式名稱

接下來是選擇這個網站要歸屬在哪一個訂閱帳號下，因為一個 Microsoft 帳號可以同時有很多不同的訂閱帳號，所以必須要在這裡的下拉式選單中做選擇。

![選擇訂用帳號](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/create_a_webapp_subscription.png)
_**圖 3**_. 選擇訂用帳號

下一步是設定或選擇**資源群組（Resource Group）**，透過這個功能可以將在 Azure 上建立的不同服務放進同一個群組中以方便管理，而通常會將同一個專案中用到的 Azure 服務放在同一個群組中，也有人會將類似用途的服務放在同一個群組，這些都是您可以自行決定的，詳細的資源群組介紹，可以參考[官網上的說明](https://azure.microsoft.com/zh-tw/documentation/articles/resource-group-portal/)。

在這裡我們可以新建一個資源群組（或是選擇您已經建立過的資源群組），名稱只要是同一個訂閱帳號下唯一的就可以了。

![設定或建立資源群組](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/create_a_webapp_resgroup.png)
_**圖 4**_. 設定或建立資源群組

接著是要設定**應用程式服務方案（App Service Plan）**，應用程式服務方案會決定 _欲使用的價格方案_ 以及 _應用程式要擺放的資料中心位置_，您可以將多個網站都套用同一種方案，也可以建立一組新的方案設定，方案名稱設定一個好記的名稱（同一個訂閱帳號下唯一），然後在 _位置_ 欄位選擇這個網站空間要放在 Microsoft Azure 全球的哪一座資料中心，最後選擇價格方案，點擊後會開啟一個面板來選擇，除了會有功能差異的概略描述之外，還會試算若一整個月都使用同一個方案的預估價格，關於價格方案詳細的功能差異及計費模式，可參考[官網上的價格說明](http://azure.microsoft.com/zh-tw/pricing/details/app-service/)。

選擇價格方案後別忘了按下下方的 **選取** 按鈕，確定在方案面板中的價格區間欄位是選擇後的方案。

![設定應用程式服務方案](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/setting_new_app_service_plan.png)
_**圖 5**_. 設定應用程式服務方案

全部都設定好了之後，檢查一下每個欄位是不是都正確無誤。

![檢查一下要建立的網站設定](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/create_a_webapp_finalize.png)
_**圖 6**_. 檢查一下要建立的網站設定

確認無誤後按下 **建立** 的按鈕，Microsoft Azure 便會開始根據設定來建立網站空間，如果在建立時有勾選 _釘選到開始面板_ 那就可以在管理後台的面板上看到這個網站的「磚」。

![]()
_**圖 7**_. 管理後台上的 Web 應用程式磚


### 上傳網站

#### 設定部署認證

在上傳檔案之前，要先設定**部署認證**，其實就是上傳部署網站時（使用 FTP 或 Git 上傳時使用）用到的帳號及密碼。點擊開始面板上剛才建立的 WEB 應用程式磚開始管理，選擇上方工具列的 _設定_ 按鈕，然後選擇 _部署認證_。

![設定部署認證](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/setting_deployment_credentials.png)
_**圖 8**_. 設定部署認證

接著就是設定認證的帳號及密碼（與登入 Microsoft Azure 的帳號不同），而要注意的是，**在同一個訂閱帳號下的部署認證帳號密碼都是同一組（FTP 的帳號會用前置詞區分網站，稍後介紹）**，所以不必每一個 Web 應用程式都重新設定。

![設定部署認證帳號及密碼](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/setting_deployment_credentials_idpwd.png)
_**圖 9**_. 設定部署認證帳號及密碼

#### 使用 FTP 上傳網站

使用 FTP 上傳是最簡單的方式，而且只要上傳完畢，網站內容便會立即更新。首先回到網站應用程式的 _設定_ 面板，然後選擇 _屬性_ 面板，就可以在這個面板中找到 FTP 的帳號及連接的位址。

![FTP 的帳號以及連接位址](https://skgitbook.blob.core.windows.net/azurerecipestw/ch02/webapp_settings_properties.png)
_**圖 10**_. FTP 的帳號以及連接位址

這裡要注意的是，**部署使用者**就是 FTP 連接時的帳號，而這個帳號就是設定部署認證時設定的，並且加上了網站名稱作為前置詞，輸入帳號時不要忘記要加上這個前置詞；而密碼就是設定部署認證時所設定的。而要使用 FTP 或 FTPS 來連接都可以。

   > 上傳網站時，要注意 Microsoft Azure 的 Web 應用程式預設的網站根目錄在 **site\wwwroot** 這個資料夾下，所以上傳檔案時要注意上傳的檔案是不是放到正確的目錄下。
   > 這個部份會在管理網站應用程式的文章另作介紹，若您有興趣，可以在 _應用程式設定_ 的面板最下方找到這個設定。

網站上傳完成後，就可以使用 **http://網站名稱.azurewebsites.net/** 來存取網站。