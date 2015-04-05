# X-1-3. 關閉 Sticky Session 以擴增網站延展性

很多開發人員將應用程式移到雲端平台後，覺得既然可以彈性調整虛擬機器的運算資源及數量，那應該可以永遠擺脫效能瓶頸，隨時能夠應付巨大流量了才是。不過這樣的想法不完全正確，要真正讓程式能夠平順、無縫自由延展，還是得調整一些程式寫法來克服阻礙延展的門檻，這篇文章要談的 Sticky Session 的問題就是其中之一。

## Sticky Session 是什麼

在撰寫網頁程式時，我們常會在伺服器端使用 Session 物件來辨認目前的前端使用者（通常會在前端使用者的 cookie 中存一個 session key 來對應），但是多數的 Web 應用程式，都是用本機檔案來實作 session 物件，這樣的使用情境到了需要使用多台（實體或虛擬）機器來運作 Web 應用程式時，如果不修改程式，要嘛原本在機器 A 存的 session 物件到了機器 B 就找不到對應，不然就是要在伺服器前端的負載平衡器上實作 sticky session 的機制 -- 如果你已經跟機器 A 發生關係，之後負載平衡器就只會把你導向機器 A 而不會到別台機器，這樣的機制通常被稱作 _sticky session_，雖然減輕了程式開發人員的負擔，但可想而知也犧牲了一些延展性（只有新使用者才可能被導向其它台機器處理）。

![IIS ARR](https://skgitbook.blob.core.windows.net/azurerecipestw/x-1-3-1-iis-arr.png)

而 Azure Web 應用程式在預設的情況下，內建的負載平衡器上採用 IIS 的 ARR (Application Request Routing) 的模組，實現了 instance affinity 的機制，也就是前一段提到的，把用戶端跟後面的伺服器機器綁定，所以這篇文章要說明的，就是將這個機制關閉，然後另外處理 session 物件。

## 關閉 ARR 的 Instnace Affinity 機制

前一段說明了 ARR Instnace Affinity 的問題，而要把這個機制關閉也很容易，不論你是使用什麼程式語言，直接在網站的根目錄加上一個 **web.config** 檔案（ASP.NET 的網站應用程式中原本就有這個檔案，把下列內容加入到適當位置即可），內容如下：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <httpProtocol>
      <customHeader>
        <add name="Arr-Disable-Session-Affinity" value="true" />
      </customHeader>
    </httpProtocol>
  </system.webServer>
</configuration>
```

更新部署，重新啟動 Azure WEB 應用程式後，sticky session 的機制就被關閉，接著就必須自己實作 session 的處理方式，不然就會產生 session 物件在機器間不同步，導致程式錯亂的狀況了。

## 重新實作 Session 物件

要重新實作 Session 物件，既然不能使用本機檔案來處理，所以不同的開發團隊會選擇不同的實作方式，有的人會選擇使用儲存體的 Blob 或 Table 來作為 session 物件的存取、也有的人會選擇使用資料庫、或是使用像 memcache、Redis cache 這類 cache store 來實作。以下列出一些參考的例子，協助你選擇或參考重新實作 Session 物件的方式：

### ASP.NET Session State
* [Session State Management in Windows Azure Web Roles](http://blogs.msdn.com/b/cie/archive/2013/05/17/session-state-management-in-windows-azure-web-roles.aspx)
* [使用 Azure Redis Cache 作為 Session State Provider](https://msdn.microsoft.com/zh-tw/library/azure/dn690522.aspx)

### PHP
* 用 Table 儲存體實作 PHP session handler：[Azure Table Session Handler](https://github.com/ericsk/azure-table-sessionhandler-for-php)


## 參考文章
* [Disabling ARR’s Instance Affinity in Windows Azure Web Sites](http://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/)