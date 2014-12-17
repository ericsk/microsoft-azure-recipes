# 3.2 新增磁碟機到虛擬機器

如果要為虛擬機器增加磁碟機來儲存資料，可以在 BLOB 儲存體上建立一個 Azure 虛擬機器用的磁碟機，然後掛載上去。一個磁碟機僅能掛載到一個虛擬機器上。

## 事前準備

* 瞭解如何建立虛擬機器，可以參考 [3.1 建立虛擬機器](chapter03/01_create_virtual_machine.md)。

## 如何操作

先登入 [Azure 管理後台](https://manage.windowsazure.com)，到虛擬機器的管理畫面上，切換到**儀表板**頁面，在下方的命令列點擊**連接**，然後選擇**連接空的磁碟機**：

![連接空的磁碟機](https://skgitbook.blob.core.windows.net/azurerecipestw/3-2-1-attach-an-empty-disk.png)

接下來會有一個對話盒要建立一個新的磁碟機，這裡要填寫的欄位主要有**磁碟機名稱**、**大小**以及**主機快取**的三個欄位，透過這個方式，建立新的磁碟機預設會放在與虛擬機器主要磁碟相同的儲存體帳號下，如果想要放在不同的儲存體帳號可以再自行修改。

![建立新的磁碟機](https://skgitbook.blob.core.windows.net/azurerecipestw/3-2-2-create-a-new-disk.png)

輸入好建立磁碟機的資料後，按下右下角的勾勾，Microsoft Azure 就會開始在 BLOB 儲存體中建立磁碟機的檔案，然後連接掛載到這台虛擬機器上，連接完成後就可以在儀表板中看到新的磁碟機資訊。

![連接新的磁碟機](https://skgitbook.blob.core.windows.net/azurerecipestw/3-2-3-new-disk-attached.png)

接下來便能連結至虛擬機器中掛載及格式化這顆新的磁碟機來使用了。

## 注意事項
* 新建好的虛擬機器，以 Windows Server 為例，**D 磁碟機**為暫存磁碟機，虛擬機器每次重開機資料便會消失，所以如果要永久存放資料，就必須以本文的方式另外掛載磁碟機來儲存。