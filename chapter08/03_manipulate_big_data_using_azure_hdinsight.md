# 8.3 使用 Azure HDInsight 處理巨量資料

在 IoT 的應用情境中，通常蒐集來的不僅是大量的資料，而這些資料通常也有**寫一次、讀取多次（write once; read many times）**的特性，當已經使用 Azure BLOB 儲存體儲存了大量來自 IoT 裝置蒐集來的、或是經由 Azure Stream Analytics 分析後的資料，後續要如何操作（查詢或修改）這些資料？[Azure HDInsight](http://azure.microsoft.com/zh-tw/services/hdinsight/) 服務正好可以來解決這個問題。

Azure HDInsight 是 Microsoft Azure 與 Horton Networks 公司合作將 [Apache Hadoop](http://hadoop.apache.org/) 專案移植到 Microsoft Azure 上的服務名稱，這意味著使用 Azure HDInsight 就跟操作 Hadoop 是一模一樣的，除了既有基於 Hadoop 開發出來的工具（如：[Hive](https://hive.apache.org/), [Pig](https://pig.apache.org/) 等）可以沿用、Azure HDInsight 還加入了一些關於 .NET、ODBC 驅動程式等擴充支援性，還不用自己架設及管理 Hadoop 的運算叢集，直接在 Microsoft Azure 上建立服務，並根據需要及負擔的價格來選擇運算資源的多寡。而在 Azure HDInsight 上的 Hadoop 版本已經可以直接處理放在 Azure BLOB 儲存體的資料，十分方便。

![Azure HDInsight](https://skgitbook.blob.core.windows.net/azurerecipestw/8-3-1-azure-hdinsight.png)

## 建立 Azure HDInsight 服務

在 Microsoft Azure 的管理後台，點擊左下角的_「+ 新增」_，選擇_「資料服務」_ » _「HDINSIGHT」_ » _「HADOOP」_，接著設定**名稱**（用來連結叢集）、**叢集大小**、連結 HDInsight 的**帳號密碼**、以及使用的**儲存體**。

![建立 Azure HDInsight](https://skgitbook.blob.core.windows.net/azurerecipestw/8-3-2-creating-azure-hdinsight.png)


## 使用 Hive 查詢語法建立資料表

## 參考資料

* [開始使用 HDInsight](http://azure.microsoft.com/zh-tw/documentation/articles/hdinsight-get-started/)
* [在 HDInsight 中將 Hadoop 工作的資料上傳](http://azure.microsoft.com/zh-tw/documentation/articles/hdinsight-upload-data/)
* [從 Hadoop 相容的 Blob 儲存體查詢巨量資料，以便在 HDInsight 中分析](http://azure.microsoft.com/zh-tw/documentation/articles/hdinsight-use-blob-storage/)