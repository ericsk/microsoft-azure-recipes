# 2.10 不停機部署及過版新網站

當預計要將網站改版更新時，開發人員一定都會想盡辦法測試，以確保新版的程式碼上線時不會發生問題，所以會建立一個與線上（一般稱為 production）環境相同的預備（一般稱為 staging）環境，在網站正式部署上線前，先把新的程式佈到預備環境，確定一切沒問題後才會佈到線上環境。Azure App Service - Web 應用程式內建了這個功能（目前僅提供給**標準**價格方案以上的用戶），在網站服務中可以加入多個部署位置，而其環境都是與線上環境相同，不必自己再花心力去維護預備環境（試想，如果想要有 2 個預備環境，在 Azure App Service - Web 應用程式上僅需按幾個按鍵即可完成，需要再開，不需要就關，如果自行架設預備環境，可以想像會多出多少成本）

![部署到預備環境](https://skgitbook.blob.core.windows.net/azurerecipestw/2-10-1-staging-deployment.png)

在預備環境測試結束後，就可以再輕鬆將預備環境的內容切換到線上環境，不停機上線過版。

## 如何操作

在 Azure App Service - Web 應用程式的管理頁面中，先在**調整規模**頁籤中確定價格方案已經是調整成**標準**以上的方案。

![調整價格方案](https://skgitbook.blob.core.windows.net/azurerecipestw/2-10-2-adjust-pricing-plan.png)

然後回到**儀表板**的頁籤，在右側的快速概覽中點擊**加入新的部署位置**。

![加入新的部署位置](https://skgitbook.blob.core.windows.net/azurerecipestw/2-10-3-dashboard-menu.png)

在對話盒中設定部署位置的名稱，並且可以選擇是否要複製其它部署位置的設定。

![設定加入部署位置的名稱](https://skgitbook.blob.core.windows.net/azurerecipestw/2-10-4-adding-new-deployment-slot.png)

新增完部署位置後，可以發現原本的網站服務會多了一個實體，而且也有它專屬的 URL 可以用來存取測試，下圖是加入了兩個部署位置的狀況：

![新增了兩個部署位置](https://skgitbook.blob.core.windows.net/azurerecipestw/2-10-5-deployment-slots.png)

有了這樣的機制之後，就不必再自行準備預備環境了，直接將新的程式部署到預備環境上，然後用預備環境的 URL 進入測試，確認沒有問題之後，再直接使用管理後台下方的「交換」按鈕，立刻就可以把某一個部署位置的程式與線上環境進行交換，之所以叫交換（swap），就是如果真的上線後發生問題，還是可以再次交換回來，不受影響。這個交換的動作僅需數秒鐘的時間就可以立即生效，所以用這種方式做網站改版完全不需要停機，讓你的網站可以持續運作。

![交換部署位置](https://skgitbook.blob.core.windows.net/azurerecipestw/2-10-6-swap-deployment-slot.png)

有了這樣的功能，將更可以滅少網站換版造成的停機損失、或是測試不完全的問題。

## 參考資源

* [Microsoft Azure 網站上的分段部署](http://azure.microsoft.com/zh-tw/documentation/articles/web-sites-staged-publishing/)