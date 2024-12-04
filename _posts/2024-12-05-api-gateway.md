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

## API Gateway vs Load Balancer vs Reverse Proxy

### Reverse Proxy

Reverse Proxy 在做的事就是接受所有外部所有的 request，然後再發送給內部的 server 做處理，多一層 proxy 可以讓我們隱藏 server 的 IP、Port 等等資訊，讓使用者不會知道這些細節，這可以避免被針對特定主機的攻擊。

並且因為都會經過 reverse proxy，所以我們也可以快取一些常見資源在 reverse proxy 這邊，這樣甚至不需要經過我們的 server 就可以回應。

為了提高傳輸速度、降低網路頻寬的使用，reverse proxy 通常會對 server 回傳的資料進行壓縮。

Reverse Proxy 所隱藏的 server 可能不只一台，說不定是 10 台，如果這 10 台都要自己處理 TLS 的交互，就會很麻煩，這些 server 也必須同步更新最新的 TLS 憑證，更何況如果導流到不同的 server，那 TLS 就要重新處理，這一來一往就把我們搞死了，所以通常會 client 統一與 reverse proxy 進行 TLS 的交互。

#### 小結

Reverse proxy 的用途是

- 隱藏資訊確保內部 server 安全
- 快取常見資源降低 server 負載
- 壓縮回傳的資訊以提高傳輸速度、降低網路頻寬
- TLS 的加解密

### Load Balancer

剛剛有提到 Reverse Proxy 可以透過快取降低 server 負載，但這樣還不夠，我們還想要更加高效率的分配跟處理負載，此時， load balancer（LB）就可以派上用場。

LB 會依據策略將流量分流給不同 server 做處理，來高效的使用資源，並且發現 server 停止服務時會將流量導向給正常的 server，這稱為「「容錯移轉」」，這可以提高可用性、可靠性。

因為 LB 需要知道哪個 server 正常、哪個不正常，所以通常會有 health check 跟 monitoring 的功能。

#### 小結

- Load Balancer 主要針對負載問題做出優化
- 透過分流策略來高效使用資源，提高可用性
- 監控、確認 server 的健康，並適時進行「容錯移轉」，確保可靠性

### API Gateway

上述的技術可以處理“過去”大部分的需求，但“現在”就有點不夠用了，主要是近幾年微服務架構的興起，如果用上述的技術處理與多個內部微服務的交互，複雜性會大大提升，會遇到的難題像是

- 每個 server 都執行著不同的微服務，LB 要怎麼導流？
- 要怎麼管控權限？ 難道要每個微服務都實現一套各自的權限控管嗎？
- 每個微服務有不同的 protocol，A 用 HTTP/1.1、B 用 gRPC、C 用 HTTP/2，client 根本不知道怎麼用
- 每個微服務都有著不同的職責，我要去哪邊知道總共有哪些 API 可以使用？ 要怎麼測試？

因應微服務時代，我們需要新的工具來處理上述需求，因此有了 API Gateway 這個新類型的工具

#### 小結

API Gateway 是因應微服務架構出現的產物，基於 Reverse Proxy、Load Balancer 之上，又添加了數項功能

- 微服務的流量管理
- 協議轉換，將一種協議轉換成另一種協議
- Developer Portal，一個集合的平台讓開發者方便測試以及查看 API 文檔
- 權限控管，這樣每個微服務就可以專注在自己的 scope，而不用擔心權限問題
