# 2.4 部署 ASP.NET 網站應用程式

Microsoft Azure 網站服務的 .NET 執行環境支援 .NET 3.5 及 4.5，底層的伺服器是以 IIS 為基礎開發的，所以只要您的 ASP.NET 應用程式在 .NET 3.5 或 4.5 的環境下執行沒有問題，部署到 Microsoft Azure 網站服務也是很容易的。

## 事前準備

這篇文章的示範環境是使用 Visual Studio 2015 搭配 Azure SDK 2.5，操作時用到的部份相容於以下環境：
* Visual Studio 2012 Professional/Premium/Ultimate
* Visual Studio 2012 Express for Web
* Visual Studio 2013 Community/Professional/Premium/Ultimate
* Visual Studio 2013 Express for Web

## 如何操作

先打開 Microsoft Azure 管理後台的頁面，打開網站實體，在**設定**的頁籤中，可以設定網站要跑 .NET 3.5 或是 4.5 的環境。

![設定 .NET Framework 環境](http://i.imgur.com/YOGXRcq.png)

新增或開啟一個 ASP.NET 的專案（Web Forms, MVC, Web API 皆可），確定執行環境是 .NET 3.5 以上。

![ASP.NET 專案](http://i.imgur.com/6KGRCji.png)

在專案上按右鍵，選擇**發行...**

![直接發行 ASP.NET 專案](http://i.imgur.com/FSMqSWY.png)

接下來，如果有安裝 Azure SDK，其中會安裝與 Visual Studio 的整合工具，這時會看到發行目標中有 **Microsoft Azure Websites** 可以選擇，否則也可以使用**匯入發行設定檔**的方式來進行發行部署。

![發行 ASP.NET 專案](http://i.imgur.com/kei0gmH.png)

* 如果選擇 **Microsoft Azure Websites**，接下來會要你登入 Microsoft 帳戶，登入完畢後會去讀取這個帳戶下所有的 Microsoft Azure 訂閱，接著列出可以部署的網站實體，可以直接選取要部署的網站實體。

  ![選擇要發行的網站實體](http://i.imgur.com/cmSudVR.png)
  
  此外，也可以按下右側的**新增**按鈕，在此新增網站實體，填寫好資料後，就會開始在 Microsoft Azure 網站服務上建立好網站實體。

  ![在 Visual Studio 中新增網站實體](http://i.imgur.com/1W4oV5x.png)

* 如果沒有上述的整合工具，Microsoft Azure 網站服務也提供了發行設定檔可供匯入，回到 Azure 的管理後台網站，點選已經建立好的網站實體，在_開始_（一個雲的圖案）頁籤中，可以找到**下載發行設定檔**的連結：

  ![在開始畫面下載發行設定檔](http://i.imgur.com/iqk8DXR.png)

  或是在_儀表板_中也可以找得到：

  ![在儀表板中找到下載發行設定檔](http://i.imgur.com/E87Zxdd.png)

  點選這些下載連結後就會下載一個 **XXXX.PublishSettings** 的檔案，在發行的對話盒中便可以直接匯入。

  ![匯入發行設定檔](http://i.imgur.com/dY4Hwfk.png)

* 若是較舊的 Visual Studio 版本，在使用 Web Deploy (Web 部署) 時，可以用文字編輯器，打開上述的發行設定檔中找到 **publishUrl**、**userName**、以及 **userPWD** 欄位的設定值，再填入發行時需要的資料。

而不管上面是用哪一種方法來發行網站，接下來就是發行前的準備，首先檢視連線資訊是否都有正確帶入：

![檢查連線資訊](http://i.imgur.com/43x8TjL.png)

確認後按下 **Next（下一步）** 按鈕，再來就是一些設定資訊，你可以視需求勾選一些項目，要注意的是，如果在建立網站實體時同時建立了資料庫，發行設定檔也會將資料庫的連線字串一併代入。

![設定網站發行](http://i.imgur.com/mjGQawz.png)

繼續按 **Next（下一步）** 到最後一步預覽發行的動作，也確認沒問題的話，按下 **Publish（發行）** 的按鈕就會開發部署網站了。

![預覽發行](http://i.imgur.com/tOGCdPx.png)

接著你就會在 Visual Studio 的視窗中看到編譯以及發行的動作，待一切都順利完成後，就會自動開啟瀏覽器，打開部署的網站了。

![發行完成](http://i.imgur.com/VFdcBMD.png)

## 注意事項

* 在建立網站時有一併建立資料庫，發行設定檔才會帶入資料庫的連線字串，而在發行時就可以替換原本 **Web.config** 檔案中的設定。