# 3.5 建立負載平衡（Load Balanced）的服務端點

使用虛擬機器來架設服務時，很多候我們希望可以使用多台機器來處理服務（如：網頁服務）的需求，這時候我們可以在設定服務端點（endpoint）時可以建立負載平衡集，讓同一個服務可分散到不同的虛擬機器上來處理。

## 事前準備

* 瞭解如何在 Microsoft Azure 上建立虛擬機器，可參考 [3.1 建立虛擬機器](chapter03/01_create_virtual_machine.md)。
* （選擇性）瞭解如何建立高可用性（HA）虛擬機器服務，可參考 [3.4 建立高可用性（HA）的虛擬機器服務](chapter03/04_high_availability.md)。

## 如何操作

首先建立多台虛擬機器，而這些虛擬機器都掛在同一個雲端服務下（對外使用同一個 DNS 名稱 _\*.cloudapp.net_），在建立第二台以後的虛擬機器時要記得選擇同一個域名，要不要建立可用性組（availability set）都可以。

![多台虛擬機器使用相同的雲端服務](https://skgitbook.blob.core.windows.net/azurerecipestw/3-5-2-create-vm-under-the-same-cloud-service.png)

建立完成後，就可以看到多台虛擬機器對應到相同的 DNS 名稱。

![使用相同雲端服務的虛擬機器](https://skgitbook.blob.core.windows.net/azurerecipestw/3-5-3-share-cloud-service.png)

這裡我們以網站服務（HTTP）作為例子，首先我們在 **azurerecipestw1** 機器上建立一個端點的對應，公開的端點設 _80_ 而私用的端點設為 _8080_，並且將**建立負載平衡集**的選項勾選起來。

![建立負載平衡集](https://skgitbook.blob.core.windows.net/azurerecipestw/3-5-4-create-endpoint-and-lb.png)

勾選了負載平衡集後，就會多一個設定的選項來設定負載平衡，

![設定負載平衡名稱](https://skgitbook.blob.core.windows.net/azurerecipestw/3-5-5-config-lb.png)

接下來，再到 **azurerecipestw2** 這台虛擬機器設定處理 HTTP 的服務端點，這時就可以直接選擇剛才建立好的負載平衡集。

![使用負載平衡集](https://skgitbook.blob.core.windows.net/azurerecipestw/3-5-6-add-into-lbset.png)

如此一來，只需要設定 azurerecipestw2 的服務端點名稱即可。

![設定服務端點名稱](https://skgitbook.blob.core.windows.net/azurerecipestw/3-5-7-config-endpoint-name.png)




## 注意事項

* 負載平衡可以分散服務到不同的虛擬機器，不過不同機器間的執行環境、資料的同步等必須要自行處理。