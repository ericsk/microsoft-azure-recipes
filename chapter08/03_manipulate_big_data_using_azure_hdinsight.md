# 8.3 使用 Azure HDInsight 處理巨量資料

在 IoT 的應用情境中，通常蒐集來的不僅是大量的資料，而這些資料通常也有**寫一次、讀取多次（write once; read many times）**的特性，當已經使用 Azure BLOB 儲存體儲存了大量來自 IoT 裝置蒐集來的、或是經由 Azure Stream Analytics 分析後的資料，後續要如何操作（查詢或修改）這些資料？Azure HDInsight 就是需要的工具。

Azure HDInsight 是 Microsoft Azure 與 Horton Networks 公司合作將 Apache Hadoop 專案移植到 Microsoft Azure 上的服務名稱，這意味著使用 Azure HDInsight 就跟操作 Hadoop 是一模一樣的，而且還不用自己架設及管理 Hadoop 的運算叢集，直接在 Microsoft Azure 上建立服務，並根據需要及負擔的價格來選擇運算資源的多寡。而在 Azure HDInsight 上的 Hadoop 版本已經可以直接處理放在 Azure BLOB 儲存體的資料，十分方便。

(圖)


## 建立 Azure HDInsight 服務

文

## 使用 Hive 查詢語法建立資料表

