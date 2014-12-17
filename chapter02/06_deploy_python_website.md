# 2.6 部署 Python 網站應用程式

Microsoft Azure 網站服務目前支援以 WFastCGI 的方式運行 Python 2.7 及 Python 3.4 的執行環境，這篇文章以 [django](https://skgitbook.blob.core.windows.net/azurerecipestw/3-1-7-vm-is-running.png) 開發框架做為部署的示範。

## 事前準備
* 擁有 Microsoft Azure 訂閱帳戶，若沒有可以參考 [1.1 建立 Microsoft Azure 訂閱帳戶](../chapter01/01_signup.md)建立。
* 瞭解如何建立網站服務，可參考 [2.1 建立 Microsoft Azure 網站實體](01_create_a_website.md)。
* 熟悉 Python 程式語言。
* （選擇性）瞭解 django 開發框架。

## 如何操作
### 設定網站服務的 Python 執行環境

在網站管理後台的**設定**頁面，可以選擇要用哪一個版本的 Python （2.7 或 3.4）執行欲部署的網站應用程式，設定完畢後儲存變更。

![選擇 Python 執行環境](https://skgitbook.blob.core.windows.net/azurerecipestw/2-6-1-setting-python-version.png)

### 部署 django 專案

假設您已經有一個 django 專案叫 _MyDjangoApp_，而專案的目錄結構如下：

	MyDjangoApp/
		MyDjangoApp/
		site-packages/
		manage.py

**site-packages** 目錄是放入所有應用程式會用到的 Python 函式庫，**包括 django**也要放進來，這樣在 Microsoft Azure 網站服務上執行時才找得到 django。

首先在你的專案根目錄（跟 **manage.py** 同一層）下新增一個 **handler.fcgi** 的檔案，內容如下：

	""
	
就是兩個雙引號即可。接著再建立一個 **web.config** 檔案，內容指定一些像是 **PYTHON_PATH** 變數或是其它環境設定：

	```xml
	<configuration>
	  <appSettings>
    	<add key="PYTHONPATH" value="D:\home\site\wwwroot;D:\home\site\wwwroot\site-packages" />
    	<add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
    	<add key="DJANGO_SETTINGS_MODULE" value="MyDjangoApp.settings" />
  	  </appSettings>
  	  <system.webServer>
    	<handlers>
      	  <add name="Python_FastCGI"
           path="handler.fcgi"
           verb="*"
           modules="FastCgiModule"
           scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
           resourceType="Either"
           requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Django Application" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
              <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="false" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>
	```
	
這樣一來你的專案下的目錄結構應該會像是這樣：

	MyDjangoApp/
		MyDjangoApp/
		site-packages/
			django/
			...
		handler.fcgi
		manage.py
		web.config
		
最後再把目錄下的東西部署到網站的 **site\wwwroot** 目錄下（如果是用 FTP 部署就要切換資料夾，若是透過 Git 之類的版本控制方式部署，直接就會部署到此目錄下，詳見 [2.3 部署靜態網站](03_deploy_static_website.md)），在 Microsoft Azure 網站服務上的目錄結構就會是這樣：

	site/
		wwwroot/
			MyDjangoApp/
			site-packages/
			handler.fcgi
			manage.py
			web.config
			
部署完成後，重新啟動網站，應該就可以正常執行這個 django 應用程式了。

## 注意事項
* 你可以上傳自行編譯的 Python 直譯器，不過要注意 Microsoft Azure 網站的執行環境是以 Windows Server 為基礎，所以要選用 built for Windows 的版本，同時也要注意網站的環境是設定為 x86 還是 x64 來決定要用什麼版本的 Python 直譯器。
* 目前已知 django 1.7 可能會有的問題是讀不到 django 相關的模組，建議可以先在 ```{APP}/settings.py``` 最後加上
	```python
	...
	import django
	django.setup()
	```
  這個 work around 來解決。