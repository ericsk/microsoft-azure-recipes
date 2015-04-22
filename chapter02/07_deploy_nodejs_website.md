# 2.7 部署 Node.js 網站應用程式

Azure App Service - Web 應用程式上的 IIS 環境已經佈建好 [iisnode](https://github.com/Azure/iisnode) 的環境，所以可以直接執行 Node.js 寫成的程式，目前預設支援的 Node.js 版本為 _0.10.32_。

這篇文章將會示範如何將 Node.js 的應用程式部署到 Microsoft Azure 網站服務。

## 事前準備
* 擁有 Microsoft Azure 訂閱帳戶，若沒有可以參考 [1.1 建立 Microsoft Azure 訂閱帳戶](../chapter01/01_signup.md)建立。
* 瞭解如何建立網站服務，可參考 [2.1 建立 Azure App Service - Web 應用程式](01_create_a_website.md)。
* 熟悉 Node.js 程式語言及相關開發技術。
* （選擇性）瞭解 Express 開發框架。

## 如何操作

### 設定 Node.js 版本

在 Microsoft Azure 網站上，設定使用的 Node.js 版本是以環境變數的方式設定，在網站管理後台的**設定**頁面，在**應用程式設定**中設定 ```WEBSITE_NODE_DEFAULT_VERSION``` 的數值來決定。

![設定 Node.js 版本](https://skgitbook.blob.core.windows.net/azurerecipestw/2-7-1-setting-nodejs-version.png)

目前這個數值可以設定的值有 **0.6.2** 及 **0.8.4**。

### 部署 Node.js 應用程式

假設應用程式的進入點是 **app.js**，而內容像是這樣簡單地回應一個 _Hello World_ 的字串：

  ```javascript
  var http = require('http')
  var port = process.env.PORT || 1337;
  http.createServer(function(req, res) {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello World\n');
  }).listen(port);
  ```

接著新增一個 **web.config** 檔案設定 iisnode：

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <configuration>
    <system.webServer>
      <handlers>
        <add name="iisnode" path="app.js" verb="*" modules="iisnode" />
      </handlers>
      <rewrite>
        <rules>
          <clear />
          <rule name="app" enabled="true" patternSyntax="ECMAScript" stopProcessing="true">
            <match url="iisnode.+" negate="true" />
            <conditions logicalGrouping="MatchAll" trackAllCaptures="false" />
            <action type="Rewrite" url="app.js" />
          </rule>
        </rules>
      </rewrite>
    </system.webServer>
  </configuration>
  ```

最後就把 **app.js** 以及 **web.config** 部署上 Azure 網站服務（若是用 FTP 則是放在 _site\wwwroot_ 目錄下）就可以開始運作了。

### 使用自訂的 node 版本

如果要使用特定的 Node.js 版本，自行下載 Windows 版的 node.exe 後，除了將它一併部署到 Microsoft Azure 網站服務上之外（假設放在 **site\wwwroot\bin** 目錄下），還要新增一個 **iisnode.yml** 的檔案來設定，在與 **web.config** 同一層目錄下新增這個檔案，內容設定為：

  ```yaml
  nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"
  ```

來指定要執行應用程式的 node 執行檔，最後部署到 Azure 網站服務的目錄結構應該會像是這樣：

  ```
  site/
    wwwroot/
      bin/
        node.exe
      app.js
      iisnode.yml
      web.config
  ```

這樣一來，應用程式就會使用自帶的 node 執行檔來執行了。

## 注意事項
* 部份原生 node 模組無法在 Microsoft Azure 上執行。
* 可以使用 **package.json** 檔案來管理模組的相依性。
