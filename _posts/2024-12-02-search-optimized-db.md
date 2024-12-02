---
title: "Key Technologies - Search Optimized Database"
categories:
  - System Design
---

## Search Optimized Database

當你今天有特殊場景時，一般傳統 DB 提供給你的搜尋可能沒辦法滿足，像是全文搜尋、向量資料、日誌分析，以前你可能需要這樣子下指令，但這樣是 full table scan，既沒效率又沒辦法 scale

```SQL
SELECT * FROM documents WHERE document_text LIKE '%search_term%'
```

你需要一個專門的工具來處理，而這個工具就是 Search Oprimized Database，他內部會對文字進行 indexing、tokenization、stemming（詞幹提取），來加速文字的搜尋跟效率，而這種作法被稱為「Inverted Indexes」（倒排索引）。

使用場景很簡單，當你遇到需要各種文字搜尋的場合，你大概率會需要這類工具來協助你，雖然說 Postgres 也有提供 GIN 這個 indexing 的 type 來給你對該欄位進行倒排索引，不過查詢速度會隨著資料的成長而跟著下滑（不過億級以內的應該感受不大），而且擴展性也沒那麼好，但反過來說，如果你的資料量沒有很大，擴展性需求也不高，你直接 Postgres + GIN 就可以搞定了。

這類 Search Oprimized Database 有以下特性：

- 倒排索引（Inverted Indexes）：倒排索引是一種從單字映射到包含它們的文件的資料結構。這使您可以快速查找包含給定單字的文檔。

- 標記化（Tokenization）：標記化是將一段文字分解為單字的過程，將單字對應到倒排索引中的文件。

- 詞幹提取（Stemming）：詞幹提取是將單字還原為詞根形式的過程，可以匹配同一單字的不同形式。例如，「running」和「runs」都將簡化為「run」。

- 模糊搜尋（Fuzzy Search）：模糊搜尋是找到與給定搜尋字詞相似的結果的能力。大多數搜尋優化資料庫都支援開箱即用的模糊搜尋作為配置選項。簡而言之，這是透過使用可以容忍搜尋字詞中輕微拼字錯誤或變化的演算法來實現的。這是透過編輯距離計算等技術來實現的，編輯距離計算可以測量需要更改、添加或刪除多少個字母才能將一個單字轉換為另一個單字。

- 擴展（Scaling）：就像傳統資料庫一樣，搜尋優化資料庫透過向叢集添加更多節點並跨這些節點分片資料來擴展。

最常見的選項就是 Elasticsearch 沒有之一，他是基於 Apache Lucene 之上，提供 RESTful API，簡單好上手讓他成為大家的首選。
