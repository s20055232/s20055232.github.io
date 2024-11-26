---
title: "Facts to know"
categories:
  - System Design
---

在進行估算時，我們需要一些數字做為起頭，而使用越合理的數字，你得出的結果就越讓人信服，我們可以在得出粗估結果之後再尋求回饋，以下是你應該知道的數字：

| **Power of 1000 (1000^x)** | **Number** | **Prefix** |  
|---|---|---|
| 0 | Unit |  |  
| 1 | Thousand | Kilo |  
| 2 | Million | Mega |  
| 3 | Billion | Giga |  
| 4 | Trillion | Tera |  
| 5 | Quadrillion | Peta |  

## Latencies

以下是一張可愛的圖，闡述電腦的運行時間與我們的認知時間之間的差異

![the scale of computing latencies](/assets/2024-11-26-facts-to-know/the%20scale%20of%20computing%20latencies.png){: data-fancybox="gallery"}

以下是我們常用的操作所耗費的時間

| 操作 | 延遲 | 延遲（μs） | 延遲（ms） | 比較 |  
|---|---|---|---|---|
| L1 緩存引用 | 0\.5 ns |  |  |  |  
| 分支預測錯誤 | 5 ns |  |  |  |  
| L2 緩存引用 | 7 ns |  |  | 14x L1 緩存 |  
| 互斥鎖定/解鎖 | 25 ns |  |  |  |  
| 主內存引用 | 100 ns |  |  | 20x L2 緩存, 200x L1 緩存 |  
| 用 Zippy 壓縮 1K 字節 | 3,000 ns | 3 μs |  |  |  
| 通過 1 Gbps 網絡發送 1K 字節 | 10,000 ns | 10 μs |  |  |  
| 從 SSD 隨機讀取 4K | 150,000 ns | 150 μs |  | \~1GB/秒 SSD |  
| 從內存順序讀取 1 MB | 250,000 ns | 250 μs |  |  |  
| 同一數據中心的往返 | 500,000 ns | 500 μs |  |  |  
| 從 SSD 順序讀取 1 MB | 1,000,000 ns | 1,000 μs | 1 ms | \~1GB/秒 SSD, 4X 內存 |  
| 磁盤尋道 | 10,000,000 ns | 10,000 μs | 10 ms | 20x 數據中心往返 |  
| 從磁盤順序讀取 1 MB | 20,000,000 ns | 20,000 μs | 20 ms | 80x 內存, 20X SSD |  
| 加州到荷蘭再到加州的數據包往返 | 150,000,000 ns | 150,000 μs | 150 ms |  |  

注意：

- 1 ns = 10^-9 秒
- 1 μs = 10^-6 秒 = 1,000 ns
- 1 ms = 10^-3 秒 = 1,000 μs = 1,000,000 ns

SSD 超高速的讀寫速度顛覆了傳統 HDD 的效能瓶頸，一台 server 加上一堆 SSD 可以做到過去一個伺服器集群可以做到的事，你的考官可能沒有意識到這點，你可以適時的提醒他

## Storage

一些常見的檔案所佔用的儲存空間大概如下：

| **Item** | **Size** |  
|---|---|
| A two-hour movie | 7 GB |  
| A 15 mins movie | 1 GB |  
| A small book of plain text | 1 MB |  
| A high-resolution photo | 1 MB |  
| A medium-resolution image (or a site layout graphic) | 100 KB |  

我們這邊用 movie 來展開，雖然你可以直接背下來，但還是知道怎麼算出來的比較好

- 影片長度：2 hours = 120 mins
- 解析度：1080p
- 幀數：24fps ~ 60fps，我們可以使用落於中間的常見格式 30fps（[參考](https://www.hitpaw.tw/video-resources/what-is-the-best-frame-rate-for-youtube.html)）
- 壓縮格式：目前主流是 H.264，後起之秀有 H.266、VP9、AV1，但還沒有普及（編碼解碼吃效能，[參考](https://jacksonlin.net/20221230-how-to-choose-format/)），所以這邊使用 H.264（[參考](https://support.google.com/youtube/answer/1722171?hl=zh-Hant#zippy=%2C%E5%AE%B9%E5%99%A8mp%2C%E9%9F%B3%E8%A8%8A%E8%BD%89%E7%A2%BC%E5%99%A8aac-lc%2C%E5%BD%B1%E6%A0%BC%E9%80%9F%E7%8E%87%2C%E4%BD%8D%E5%85%83%E7%8E%87%2C%E5%BD%B1%E7%89%87%E8%A7%A3%E6%9E%90%E5%BA%A6%E5%92%8C%E9%95%B7%E5%AF%AC%E6%AF%94%2C%E8%89%B2%E5%9F%9F%2C%E5%BD%B1%E7%89%87%E8%BD%89%E7%A2%BC%E5%99%A8h)）

未壓縮的 HD 影片，1920x1080像素、10-bit 色彩深度（有三個 color channel，每個 channel 有 10bits，[參考](https://gist.github.com/YamashitaRen/2dcea6fd5830ecd53236)）

$$
1920 \times 1080 \times 30\ bits \times\ 30\ frames \div 8\ bits = \ 233280000\ bytes \approx 233\ MB
$$

每秒會產生 233 MB，不過通常為了確保觀看畫質與下載速率，透過 H.264 壓縮後，1080p 的影片的 bitrate（位元速率）需要控制在  4 ~ 8 Mbps（1 Mbps 等於 125KB/秒） 左右（[參考](https://simular.co/blog/post/54-%E5%A6%82%E4%BD%95%E5%A3%93%E7%B8%AE%E5%BD%B1%E9%9F%B3%E8%87%B3%E9%81%A9%E5%90%88%E6%92%AD%E6%94%BE%E7%9A%84%E5%A4%A7%E5%B0%8F)），我們取平均為 6 Mbps（750KB/s），重新計算後得知

$$
750\ KB/s \times 60\ secs \times 120\ mins = 5400000\ KB \approx 5.15\ GB
$$

## Business

有些關於領域知識的數字，考官照理來說會提供給你，畢竟工程師可能對這些數字沒有概念，因此你也不用擔心這個數字你抓錯會被扣分

| **Metric** | **Order of Magnitude** |  
|---|---|
| Daily active users of major social networks | O(1b) |  
| Hours of video streamed on Netflix per day | O(100m) |  
| Google searches per second | O(100k) |  
| Size of Wikipedia | O(100gb) |  
