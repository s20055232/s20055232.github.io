---
title: "Key Technologies - Database"
categories:
  - Database
---

總是考慮 JSONB 如果你不用考慮以下問題：

1. JSON 是純文字的完整複製，不會進行預先解析，不會添加索引，如果你可以接受解析較慢，且你使用 JSON 時都是使用整份文字，不需要檢索特定資訊

2. 可以接受空間的浪費，JSONB 會幫你將 JSON 做處理，去掉空格、重複的 key，格式會比較緊湊

3. 你的 key 可以接受跟原本順序不符，JSONB 不會幫你保留原本 JSON 的 key 順序

4. 你的 JSON 非常小，JSONB 幫你做的額外操作顯得沒有必要，直接讀取做使用反而更簡單更快

雖然 JSONB 聽起來很完美，但對於超出數字精度的部分，JSONB 會犧牲其資料精度，而 JSON 不會，這一點取決於系統需求需要被納入考慮。
