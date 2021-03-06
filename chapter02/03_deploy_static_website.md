# 2.3 部署靜態網站

要部署靜態網站到 Microsoft Azure 靜態網站，只要把網頁資料上傳到網站服務的根目錄，就可以直接作為網頁空間使用。

## 事前準備

在開始之前，要先在 Azure App Service - Web 應用程式建立網站，建立網站實體的方式可以參考 [2.1 建立 Azure App Service - Web 應用程式實體](01_create_a_website.md)這篇文章。

另一方面，也要先設定好部署認證，設定的方式可以參考 [2.2 設定部署驗證](02_configure_authentication.md)這篇文章。

## 如何操作

### 設定網站根目錄

部署靜態檔案到 Azure App Service - Web 應用程式，首先要知道網站的根目錄是哪一個，這個設定在管理後台中可以看到，打開網站的管理頁面，在**設定**的頁籤，拉到最下面看到虛擬應用程式和目錄:

![設定頁](http://i.imgur.com/OFDsQCH.png)

![設定對應目錄](http://i.imgur.com/H9pGNvm.png)

預設的狀況下，網站的根目錄（**/**）對應到 **site\wwwroot** 目錄，所以網站要上傳時就傳到這個目錄下，當然也可以直接修改設定，或是增加其它網站路徑的對應關係。

### 以 FTP 部署網站為例

這裡以 FTP 部署作示範，在瞭解根目錄的位置後，回到**儀表板**的頁籤，往下捲動，可以在右側找到關於 FTP 連線的相關資訊：

![FTP 連線相關資訊](http://i.imgur.com/92AzIEK.png)

**FTP/FTPS 主機名稱**就是 FTP 連線時的位址； FTP 使用者名稱就是 **網站名稱\使用者名稱** 的格式，注意這裡不能只輸入使用者名稱，必須按照畫面上顯示的全名輸入，以上圖為例就是要輸入 **azurecampdemo\ericsk**，每個網站都不一樣；而密碼的部份，就是在設定部署認證時所輸入的密碼。你可以使用熟悉的 FTP 工具（例如：Windows 下可以使用 FileZilla、Mac 下可使用 Cyberduck 等）來進行連線。

連接上 FTP 主機後，切換到 **site\wwwroot** 目錄（或是您自行設定的目錄路徑）下，再把網站內容上傳上去，就可以完成網站的部署了。

![FileZilla 的連線畫面](http://i.imgur.com/8kwZqDS.png)