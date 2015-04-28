# 8.3 使用 Azure HDInsight 處理巨量資料

在 IoT 的應用情境中，通常蒐集來的不僅是大量的資料，而這些資料通常也有**寫一次、讀取多次（write once; read many times）**的特性，當已經使用 Azure BLOB 儲存體儲存了大量來自 IoT 裝置蒐集來的、或是經由 Azure Stream Analytics 分析後的資料，後續要如何操作（查詢或修改）這些資料？[Azure HDInsight](http://azure.microsoft.com/zh-tw/services/hdinsight/) 服務正好可以來解決這個問題。

Azure HDInsight 是 Microsoft Azure 與 Horton Networks 公司合作將 [Apache Hadoop](http://hadoop.apache.org/) 專案移植到 Microsoft Azure 上的服務名稱，這意味著使用 Azure HDInsight 就跟操作 Hadoop 是一模一樣的，除了既有基於 Hadoop 開發出來的工具（如：[Hive](https://hive.apache.org/), [Pig](https://pig.apache.org/) 等）可以沿用、Azure HDInsight 還加入了一些關於 .NET、ODBC 驅動程式等擴充支援性，還不用自己架設及管理 Hadoop 的運算叢集，直接在 Microsoft Azure 上建立服務，並根據需要及負擔的價格來選擇運算資源的多寡。而在 Azure HDInsight 上的 Hadoop 版本已經可以直接處理放在 Azure BLOB 儲存體的資料，十分方便。

![Azure HDInsight](https://skgitbook.blob.core.windows.net/azurerecipestw/8-3-1-azure-hdinsight.png)

## 建立 Azure HDInsight 服務

在 Microsoft Azure 的管理後台，點擊左下角的_「+ 新增」_，選擇_「資料服務」_ » _「HDINSIGHT」_ » _「HADOOP」_，接著設定**名稱**（用來連結叢集）、**叢集大小**、連結 HDInsight 的**帳號密碼**、以及使用的**儲存體**。

![建立 Azure HDInsight](https://skgitbook.blob.core.windows.net/azurerecipestw/8-3-2-creating-azure-hdinsight.png)

	上述的步驟是建立以 Windows Server 為基礎的 Hadoop 環境，您也可以選擇「LINUX 上的 HADOOP」來建立以 (Ubuntu) Linux 為基礎的 Hadoop 環境。

根據選擇的叢集大小需要一點時間建立服務，建立完成後，就可以直接將需要 Hadoop 執行的工作丟上這個服務上執行（Windows Server 為基礎的 Hadoop 用 PowerShell 來遞交工作；Linux 為基礎的 Hadoop 則用 SSH 來遞交）。

![基於 Windows Server 的 Azure HDInsight](https://skgitbook.blob.core.windows.net/azurerecipestw/8-3-3-hadoop-on-windows-server.png)
_基於 Windows Server 的 Hadoop 環境操作介紹_




## 使用 Web Console 操作 Azure HDInsight

Microsoft Azure 也為 HDInsight 的服務建立了 Web 操作介面（Web Console），方便使用者透過網頁的方式來操作 Hadoop。只要在管理後台，點選服務，都可以在下方的工作列找到 **Web 主控台** 的按鈕（或是直接連結 _https://[名稱].azurehdinsight.net/_）進入

![基於 Windows Server 的 Azure HDInsight](https://skgitbook.blob.core.windows.net/azurerecipestw/8-3-5-web-console-button.png)

輸入帳號（_admin_）及設定的密碼後，就會進入 Web 主控台的介面，可以在左下角切換成正體中文介面。

![Azure HDInsight 的 Web 主控台](https://skgitbook.blob.core.windows.net/azurerecipestw/8-3-6-azure-hdinsight-web-console.png)

有了這樣的介面，你就可以透過網頁來進行範例的練習、執行 Hive 查詢、查看工作記錄、以及瀏覽跟 Azure HDInsight 對應的儲存體內資料。

## 參考資料

* [開始使用 HDInsight](http://azure.microsoft.com/zh-tw/documentation/articles/hdinsight-get-started/)
* [在 HDInsight 中將 Hadoop 工作的資料上傳](http://azure.microsoft.com/zh-tw/documentation/articles/hdinsight-upload-data/)
* [從 Hadoop 相容的 Blob 儲存體查詢巨量資料，以便在 HDInsight 中分析](http://azure.microsoft.com/zh-tw/documentation/articles/hdinsight-use-blob-storage/)