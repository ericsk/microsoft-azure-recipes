# 2.8 部署 Java 網站應用程式

2014 年 4 月開始 Microsoft Azure 網站應用程式加入了 Java 的支援，目前使用 Java 7 的環境，搭配的 Web 容器則是 Tomcat 7 

## 事前準備

* 擁有 Microsoft Azure 訂閱帳戶。
* 會建立網站服務，可參考 [2.1 建立 Microsoft Azure 網站服務](chapter02/01_create_a_website.md)一文。
* 使用 Java 開發網站應用程式（基於 Tomcat 及 Jetty）。

## 如何操作

### 設定網站的 Java 執行環境

首先建立一個網站服務，接著在**設定**的頁面選擇 Java 的執行版本，並且選擇 Web 容器，目前 Microsoft Azure 的 Java 支援 **jdk1.7.0\_51**，而 Web 容器則是有 **Tomcat** 及 **Jetty** 兩種選擇。

![設定網站服務的 Java 執行環境](https://skgitbook.blob.core.windows.net/azurerecipestw/2-8-1-setting-java-environment.png)

選擇好後儲存變更，就準備好讓這個網站服務能執行 Java 的網站應用程式，以下的示範以 Tomcat 為例。

### 建置 Java 網站應用程式部署包

要將 Java 網站應用程式部署上 Microsoft Azure 網站服務只需要像平時一樣打包成 \*.war 檔案即可（畢竟就是部署到 Tomcat 上）。只是在打包編譯時要注意目標的 Java 版本，以及 Tomcat 的版本都要符合 Microsoft Azure 網站服務支援的部份。

![打包 WAR 檔](https://skgitbook.blob.core.windows.net/azurerecipestw/2-8-2-setting-java-environment.png)

打包 WAR 檔成功之後，可以使用 FTP 將 war 檔案上傳至網站上的 **site\wwwroot\webapps** 目錄下

![上傳至正確的目錄](https://skgitbook.blob.core.windows.net/azurerecipestw/2-8-3-deploy-war.png)

上傳完畢後，等待約 1 分鐘內，等系統解開 WAR 檔後就能開始使用這個 Java 網站應用程式，完成部署。