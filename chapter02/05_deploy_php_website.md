# 2.5 部署 PHP 網站應用程式

Microsoft Azure 網站服務目前直接支援 PHP 5.3, 5.4 及 5.5 的執行環境，也可以部署想要使用的 PHP 版本，只要直接把 PHP 網站應用程式的檔案部署到網站空間，幾乎不用調整設定（詳見_注意事項_）就可以直接運行。

## 事前準備
* 擁有 Microsoft Azure 訂閱帳戶。
* 瞭解如何建立Microsoft Azure 網站服務。
* 瞭解 PHP 開發。

## 部署 PHP 網站應用程式

部署 PHP 網站應用程式非常簡單，只要將 PHP 檔案上傳至對應的目錄，如：**site\wwwroot**（詳見[2.3 部署靜態網站](03_deploy_static_website.md)）立刻就可以運作。而若要調整使用的 PHP 的版本，打開網站的管理頁面，切換到**設定**的頁面，可以直接切換 PHP 版本，然後儲存設定，立即生效。

![設定網站的 PHP 版本](https://skgitbook.blob.core.windows.net/azurerecipestw/2-5-1-config-php-versions.png)

## 根據開發框架調整設定

有些 PHP 開發框架，如：Zend Framework、Laravel 等有自己的應用程式目錄結構（例如，根目錄的對應是 **public/**），另外則需要 Web 伺服器做 URL Rewrite 的操作，這樣的特例就需要在設定上做些調整，以下針對 Laravel 的應用程式來介紹設定部署的流程。

  1. 在基於 Laravel 寫成的 PHP 應用程式中，新增一個 **web.config** 檔案在 **public** 目錄下做 URL Rewrite 的設定，檔案內容如下：
  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <configuration>
    <system.webServer>
      <rewrite>
        <rules>
          <rule name="Imported Rule 1" stopProcessing="true">
            <match url="^" ignoreCase="false" />
            <conditions logicalGrouping="MatchAll">
              <add input="{REQUEST_FILENAME}" matchType="IsDirectory" ignoreCase="false" negate="true" />
              <add input="{REQUEST_FILENAME}" matchType="IsFile" ignoreCase="false" negate="true" />
            </conditions>
            <action type="Rewrite" url="index.php" />
          </rule>
        </rules>
      </rewrite>
    </system.webServer>
  </configuration>
  ```

  2. 將基於 Laravel 寫成的 PHP 應用程式的檔案都部署到預設的根目錄 **site\wwwrooot** 目錄下。

  3. 前往網站的管理頁面，到**設定**的頁籤，修改**虛擬應用程式和目錄**的設定，將 **/** 修改成對應到 **site\wwwroot\public**，因為 Laravel 的應用程式根目錄是在 **public**。

    ![設定網站根目錄對應檔案系統的路徑](https://skgitbook.blob.core.windows.net/azurerecipestw/2-5-2-config-virtual-directory.png)

## 使用 PHP 擴充套件（PHP Extensions）

撰寫網站應用程式時，除了 Microsoft Azure 網站服務本來就準備好的 PHP 執行環境、預先編譯好的擴充套件之外，碰到某些狀況可能會想要自行開發或是使用別人已經開發好的 PHP 擴充套件（PHP Extensions），例如要使用 Memcache 作快取時，很多人會使用 [PECL](http://pecl.php.net/) 上的這個 [memcache 擴充套件](http://pecl.php.net/package/memcache)。想要使用 PHP 擴充套件，只要在 Microsoft Azure 網站服務的後台做一些調整就可以了。以下就以 memcache extension 作為示範：

  1. 在取得 PHP 擴充套件時要特別注意，因為 Microsoft Azure 網站服務是以 Windows Server 及 IIS 為基礎，所以**要使用的 PHP 擴充套件必須要是編譯為 Windows 的版本**（也就是 .dll 檔案），目前 Microsoft Azure 網站服務能正確執行的是透過 VC9（Visual C++ 2008）編譯的版本（並且是 non thread safe），至於要使用 32-bit 或是 64-bit 的版本、PHP 的版本，也要看你的網站服務設定使用哪一個環境。

  2. 以上述 memcache 擴充套件為例，到[這個網頁](http://pecl.php.net/package/memcache/3.0.8/windows)，根㯫你的 PHP 版本，下載 **Non Thread Safe (NTS) x86** 的版本，下載後解壓縮後可以得到一個 **php_memcache.dll** 的檔案，這個就是要隨著網站應用程式一併部署到 Microsoft Azure 網站服務上。

  3. 在網站的根目錄下建立一個 **bin** 資料夾_（這個名稱可以自己設定，不一定要 bin）_，然後將 **php_memcache.dll** 檔案放在 **bin\** 目錄下。

  4. 接下來到網站管理介面下的**設定**頁面，在**應用程式設定**裡增加一個 **PHP_EXTENSIONS** 的設定，然後值設成 **bin\php_memcache.dll**（如果有多個 extensions，就用逗號隔開，例如：_bin\a.dll,bin\b.dll_）如下所示：

  ![設定 PHP_EXTENSIONS 常數](https://skgitbook.blob.core.windows.net/azurerecipestw/2-5-3-set-phpextensions-constant.png)

  5. 儲存變更後，你的 PHP 網站就可以使用 php_memcache.dll 這個擴充套件的功能了。

## 使用自訂的 PHP 直譯器

## 注意事項

