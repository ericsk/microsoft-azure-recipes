# 4.3 上傳檔案至 BLOB 儲存體（.NET）

在開發網站或其它應用程式時，可能會想使用 Azure 儲存體服務來儲存檔案，這篇食譜是介紹如何在 .NET 應用程式將檔案上傳至 Blob 儲存體。

## 事前準備

* 建立 Azure 儲存體帳戶，可參考 [4.1 建立儲存體帳號](01_create_storage_account.md)建立。

## 如何上傳

### ASP.NET 網站應用程式

以下以 ASP.NET MVC 為例，假設網頁表單中有一個上傳檔案的欄位（```<input type="file">```），後端程式要如何處理上傳至 Blob 儲存體，首先假設 model 的程式碼如下：

  ```csharp
  using System.Web;

  public class CreateViewModel
  {
    public string Title { get; set; }
    public HttpPostedFileBase Image { get; set; }
  }
  ```

這只是一個很簡單的表單，只有兩個欄位，其中一個是純文字的輸入，而另一個則是上傳檔案的部份。網頁端的程式碼如下所示：

  ```csharp
  @model CreateViewModel

  @using (Html.BeginForm("Bar", "Foo", FormMethod.Post, new { @enctype = "multipart/form-data" }))
  {
    @Html.AntiForgeryToken()

    <p>
      @Html.LabelFor(model => model.Title)
      @Html.EditorFor(model => model.Title)
    </p>
    <p>
      @Html.LabelFor(model => model.Image)
      @Html.TextBoxFor(model => model.Image, new { @type = "file", @accept = "image/*" })
    </p>
    <p>
      <button type="submit">送出</button>
    </p>
  }
  ```

而撰寫處理這個表單上傳的程式碼之前，需要透過 NuGet 安裝 **WindowsAzure.Storage** 的套件：

![透過 NuGet 安裝 WindowsAzure.Storage 套件](https://skgitbook.blob.core.windows.net/azurerecipestw/4-3-1-install-azure-storage-sdk.png)

這樣就可以輕鬆將檔案上傳到 Azure 的儲存體上，程式碼如下：

  ```csharp
  using System;
  using System.Threading.Tasks;
  using System.Web;
  using System.Web.Mvc;
  using Microsoft.WindowsAzure.Storage;
  using Microsoft.WindowsAzure.Storage.Blob;

  public class FooController : Controller
  {
    const string STORAGE_ACCOUNT = "儲存體帳戶名稱";
    const string STORAGE_PRIMARY_KEY = "儲存體金鑰";
    const string BLOB_CONTAINER = "upload";

    ...

    [HttpPost]
    [ValidateAntiForgeryToken]
    public async Task<ActionResult> Bar([Bind(Include = "Title,Image")] CreateViewModel model)
    {
      ...

      if (ModelState.IsValid)
      {
        ...
        var imageUrl = await UploadFileToBlobAsync(model.Image);
        ...
      }
      ...
    }

    private async Task<string> UploadFileToBlobAsync(HttpPostedFileBase file)
    {
      string connectionString = String.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", STORAGE_ACCOUNT, STORAGE_PRIMARY_KEY);
      CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
      CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
      CloudBlobContainer container = blobClient.GetContainerReference(BLOB_CONTAINER);

      string imageName = string.Format("{0}-{1}{2}", id, index, Path.GetExtension(file.FileName));
      CloudBlockBlob blockBlob = container.GetBlockBlobReference(imageName);
      blockBlob.Properties.ContentType = file.ContentType;
      await blockBlob.UploadFromStreamAsync(file.InputStream);

      var uriBuilder = new UriBuilder(blockBlob.Uri);
      string filePath = string.Format("{0}", imageName);

      return filePath;
    }
  }
  ```
