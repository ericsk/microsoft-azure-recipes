# 2.9 自訂網域名稱

建立 Azure App Service - Web 應用程式後，會根據設定的名稱自動配一個 _[名稱].azurewebsites.net_ 的網址使用，假設 Web 應用程式的名稱為 **mywebsite**，那麼就會得到 _mywebsite.azurewebsites.net_ 的網址使用，但 Azure App Service - Web 應用程式還是提供能使用自訂網域的功能（註：免費模式則無法使用自訂網域的功能），這篇文章將介紹如何設定自訂網域。

## 如何操作

首先要將價格方案調整成**共用**以上，才能使用自訂網域的功能。在 Azure App Service - Web 應用程式的管理介面中，選擇**調整規模**頁籤，然後將應用程式服務方案價格區間中調整成**共用**以上的方案。關於方案的計費、功能差異可以參考官網上的[說明頁面](http://azure.microsoft.com/zh-tw/pricing/details/app-service/)。

![設定應用服務價格方案](https://skgitbook.blob.core.windows.net/azurerecipestw/2-9-1-adjust-price-plan.png)

接著到管理你網域設定的頁面（依照購買網域的服務而定），新增一筆 CNAME 記錄來對應配發的 _azurewebsites.net_ 的網域，比方說，如果你自己的 domain 是 _yourweb.com_，而你想要將 _www.yourweb.com_ 對應到 _mywebsite.azurewebsites.net_，就在你管理 _yourweb.com_ 的 DNS 伺服器上新增一筆 CNAME 記錄將 **www** 對應到 **mywebsite.azurewebsites.net**。以下圖為例，這是我將 _blog.ericsk.org_ 對應到 _ericsk-blog.azurewebsites.net_ 的方式（畫面為 GoDaddy 的管理畫面）：

![設定 DNS 的 CNAME 記錄](https://skgitbook.blob.core.windows.net/azurerecipestw/2-9-2-configure-cname-record.png)

設定完 CNAME 記錄之後，回到 Azure App Service - Web 應用程式的管理介面中，選擇**設定**頁籤，拉到下方的**網域名稱**區域，按下**管理網域**的按鈕，

![設定網域](https://skgitbook.blob.core.windows.net/azurerecipestw/2-9-3-setting-domain-names.png)

這時會跳出一個對話視窗，說明如何進行設定，如果 CNAME 記錄已經生效的話，就可以填入你對應的網域名稱，Azure 也會去偵測記錄是否生效，若尚未生效就無法進行設定儲存。另外你也可以在這個對話盒中看到一個 IP，這是提供給你設定 DNS 的 A 記錄所使用的，你也可以用這個 IP 位址來設定 A 記錄。

![設定網域名稱](https://skgitbook.blob.core.windows.net/azurerecipestw/2-9-4-setting-custom-domain.png)

設定完成，按下下方的勾勾按鈕完成設定後，就可以使用這個自訂網域來連接網站了。


## 其它

* 如果想要設定裸網域對應，比方說以上面的例子，想要將 _yourweb.com_ 對應到 _mywebsite.azurewebsites.net_ 的話，首先必須先建立一個 CNAME 記錄，將 _**awverify**.yourweb.com_ 對應到 _**awverify**.mywebsite.azurewebsites.net_ ，然後再在 _yourweb.com_ 新增一筆 A 記錄指到配發的 IP 位址，這樣就可以在管理介面中將裸網域對應到網站了。