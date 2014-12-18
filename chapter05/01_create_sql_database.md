# 5.1 建立 SQL Database

就像建立網站服務一樣，不必另外架設伺服器或虛擬機器就能直接建立網站運作的環境，而 SQL Database 服務也能讓您直接有一個 SQL 資料庫來使用，而不必架設 SQL Server。

## 事前準備
* 瞭解基本 SQL 資料庫的運作
* 瞭解 SQL 語法

## 如何操作

### 快速建立

進入 Microsoft Azure 的[管理後台](https://manage.windowsazure.com/)，點擊左下角的_「+新增」_，選_資料服務_ » _SQL 資料庫_» _快速建立_：

![建立 SQL Database 服務](https://skgitbook.blob.core.windows.net/azurerecipestw/5-1-1-create-sql-database.png)

接著在**資料庫名稱**輸入這個資料庫的名稱，接著第一次建立 SQL 資料庫時，需要建立一個 SQL 資料庫伺服器（之後可以自行選擇要不要把不同資料庫建立在相同的 SQL 資料庫伺服器中），在**地區**的欄位選擇想要放資料庫的資料中心，然後輸入這個 SQL 資料庫伺服器的**登入名稱**以及**密碼**，最後按下**建立 SQL 資料庫**的按鈕就可以完成建立。

不用一分鐘，資料庫就準備好可以使用了：

![SQL 資料庫已建立完成](https://skgitbook.blob.core.windows.net/azurerecipestw/5-1-2-sql-database-created.png)

### 自訂建立

在新增時，選擇_自訂建立_會跳出一個對話盒進行比較詳細的建立步驟，會看到這樣的畫面：

![SQL 資料庫已建立完成](https://skgitbook.blob.core.windows.net/azurerecipestw/5-1-3-custom-creation.png)

除了像快速建立時一樣要輸入資料庫名稱、建立或選擇 SQL 資料庫伺服器之外，這裡還可以選擇 SQL 資料庫要使用 **BASIC**、**STANDARD** 還是 *PREMIUM** 等級的服務，而 STANDARD 及 PREMIUM 又還可以說擇不同的效能等級，關於這幾種價格方案的費用及規格的差異，可以參考官網上 [SQL Database 定價頁面](http://azure.microsoft.com/zh-tw/pricing/details/sql-database/)。

## 注意事項

* 由於 SQL 資料庫服務的技術基礎就是 Microsoft SQL Server，所以完全可以使用 SQL Server Management Studio 之類的管理工具來進行管理。