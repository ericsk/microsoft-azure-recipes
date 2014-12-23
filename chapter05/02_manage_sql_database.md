# 5.2 管理 SQL Database

Microsoft Azure 本身提供了一個管理 SQL Database 的 Web 應用程式，除此之外，還能夠使用 Visual Studio 以及 SQL Server Management Studio 這類型的工具來管理放在 Microsoft Azure SQL Database 服務中的 SQL 資料庫。

## 事前準備
* 瞭解如何在 Microsoft Azure SQL Database 服務上建立 SQL 資料庫，可參考 [5.1建立 SQL Database](chapter05/01_create_sql_database.md)。
* （選擇性）瞭解 Visual Studio 的操作，並且有安裝 SQL Database Tooling in Visual Studio。
* （選擇性）瞭解 SQL Server Management Studio 的操作。

## 如何操作
### 透過 SQL Database Web 管理應用程式

進入 Microsoft Azure 管理後台，在 SQL 資料庫的管理頁面下，點擊下方的命令列的**管理**按鈕。

![管理 SQL 資料庫](https://skgitbook.blob.core.windows.net/azurerecipestw/5-2-1-manage-button.png)

因為預設 SQL 資料庫只會開放給 Microsoft Azure 上的服務或應用程式連接，若是第一次點擊管理的按鈕，系統會提示是否要把目前的網路 IP 位址加入 SQL 伺服器的防火牆白名單中，以便存取 SQL 資料庫，你必須加入才能繼續。

![將存取的 IP 位址加入白名單中](https://skgitbook.blob.core.windows.net/azurerecipestw/5-2-2-whitelist.png)

將 IP 位址加入防火牆規則後，就會開啟一個瀏覽器的視窗來執行 Web 版的 SQL Database 管理工具，這裡輸入建立 SQL 伺服器時的帳號密碼，然後登入管理工具。

![登入 SQL Database 管理工具](https://skgitbook.blob.core.windows.net/azurerecipestw/5-2-3-sql-database-management-portal.png)

順利登入之後，就可以使用這工具管理建立在 Microsoft Azure 下的 SQL 資料庫了。

![使用 Web 應用程式管理 SQL 資料庫](https://skgitbook.blob.core.windows.net/azurerecipestw/5-2-4-sql-database-management-webapp.png)

### 透過 Visual Studio 管理

如果要用 Visual Studio 來管理，可以在 SQL 資料庫的管理頁面中，點擊下方命令列的**在 VISUAL STUDIO 中開啟**。

![從 Visual Studio 中管理 SQL 資料庫](https://skgitbook.blob.core.windows.net/azurerecipestw/5-2-5-manage-sql-database-in-visualstudio.png)

點擊後會有訊息提示要使用 _Visual Studio 2013 Update 4 及以後的版本_才能利開啟。

![從 Visual Studio 開啟的提示](https://skgitbook.blob.core.windows.net/azurerecipestw/5-2-6-tips-open-in-visual-studio.png)

按下開啟，並且同意開啟 Visual Studio 之後，SQL Server 工具就會要你連接的資訊，當然也是要事先將操作電腦的 IP 位址加入防火牆規則中才能連線成功。

![連接 SQL Server](https://skgitbook.blob.core.windows.net/azurerecipestw/5-2-7-connect-to-azure-sql-database.png)

連接成功後，在 Visual Studio 中的 SQL Server 物件總管中就可以看到這個 SQL 資料庫，就能對它進行管理及操作。

![在 Visual Studio 中的 SQL Server 物件總管管理 SQL 資料庫](https://skgitbook.blob.core.windows.net/azurerecipestw/5-2-8-connect-to-azure-sql-database.png)

## 注意事項 
* Web 版的 SQL Database 管理工具需要安裝 Silverlight 外掛程式才能啟用。