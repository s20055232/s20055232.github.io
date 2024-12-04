---
title: "Key Technologies - API Gateway"
categories:
  - System Design
---

## API Gateway

API Gateway 跟 Load balancer 很容易會搞混，因為他們能做到的事有高度的重疊，這時候就必須知道他們的發展脈絡，才能比較好的區隔他們。

API Gateway 是在微服務架構盛行之後所出現的產物，目的是將外部呼叫的 request 可以導流到對應的微服務，而 load balancer 的目的則是將流量均勻的分配的服務，透過上述的文字，你就可以知道差異，一個重點是正確導流到特定服務，一個是均勻分配流量。

| **功能** | **API Gateway** | **Load Balancer** |
|---|---|---|
| 導流和管理 | 將外部呼叫的request導流到對應的微服務 | 平衡流量，均勻分配給多個服務 |
| 安全控制 | 透過API管理、安全控制等功能 | 無 |
| 平衡流量 | 無 | 優化系統效能和可用性 |

因為 API Gateway 是微服務的“警衛室”，所以通常會有 authentication（身份驗證）、authorization（權限管控）的功能，在現今的系統設計面試中，通常 API gateway 是不可或缺的，把它納入你的設計裡面八成沒錯，並且遇到身份管控相關的問題時，你都可以直接說「我的 API gateway 會處理」，可知 API gateway 的重要性

常見的選項有：AWS API Gateway、GCP Apigee、Kong
