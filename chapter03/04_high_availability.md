# 3.4 建立高可用性的虛擬機器服務

在雲端的虛擬機器服務，幾乎都不可能保證 100% 沒有當機或暫時無法存取的機會，為了要提高放在虛擬機器上的服務盡量不會停機，就必須要用多台虛擬機器相互備援，在其中一台機器暫時無法提供服務或失去連線時，可以自動移轉到其它虛擬機器上繼續提供服務。在 Microsoft Azure 虛擬機器服務中，就要藉著設定**可用性設定組（availability set）**來完成這樣的高可用性架構。

![可用性設定組](https://skgitbook.blob.core.windows.net/azurerecipestw/3-4-1-fault-domain.png)

如上圖顯示，設在同一個可用性設定組（availability set）的虛擬機器會被分配在資料中心的不同機櫃中，一旦有一個虛擬機器或機櫃在維修、或是有問題時，可以無縫地將服務移轉到可用性設定組中的其它機器中，不論要建立 Windows Server、Linux Server 或其它的虛擬機器服務，都可以藉此提高服務的高可用性（HA, High Availability）。

## 事前準備
* 瞭解如何建立虛擬機器，可參考 [3.1 建立虛擬機器](chapter03/01_create_virtual_machine.md)。

## 如何操作

在從組件庫建立虛擬機器時，其中一個步驟便能夠建立**可用性設定組（availability set）**，這時便能建立可用性設定組並且將這個虛擬機器放進這個設定組中。

![建立可用性設定組](https://skgitbook.blob.core.windows.net/azurerecipestw/3-4-2-setting-new-availability-set.png)

有了可用性設定組之後，當再建立新的虛擬機器時，**必須要與其它可用性設定組中的虛擬機器使用同一組雲端服務（cloud service）**（也就是用同一個 _\*.cloudapp.net_ 的 DNS 名稱），這樣才能選擇欲加入的可用性設定組。

![加入可用性設定組](https://skgitbook.blob.core.windows.net/azurerecipestw/3-4-3-adding-availability-set.png)

這樣一來，這些在同一個可用性設定組的虛擬機器便能夠互相備援，建立起高可用性的虛擬機器系統。你可以在虛擬機器管理界面的**設定**頁面看到可用性設定組的狀態。

![可用性設定組的狀態](https://skgitbook.blob.core.windows.net/azurerecipestw/3-4-4-vm-setting.png)


## 注意事項
* 參考 Microsoft Azure 官方網頁上的[服務水準聲明](http://azure.microsoft.com/zh-tw/support/legal/sla/)，其中虛擬機器的說明如下：

	雲端服務、虛擬機器及虛擬網路

	* 對於雲端服務，我們保證當您在不同錯誤網域和升級網域部署兩個以上的角色執行個體時，您的網際網路對向角色將在至少 99.95% 的時間內具有外部連線能力。
	* 對於有兩個以上執行個體部署至相同可用性設定組的所有網際網路對向虛擬機器，我們保證將在至少 99.95% 的時間內具有外部連線能力。
	* 對於虛擬網路，我們保證虛擬網路閘道有 99.9% 的可用性。


* 關於 99.95% 的服務水準，可以參考[維基百科上雲端服務的服務水準的定義](http://en.wikipedia.org/wiki/High_availability)。