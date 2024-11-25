---
title: "System Design Introduction"
categories:
  - System Design
---

80/20 法則，大多數的系統設計面試，主要在考驗你少部分的核心觀念

有四種面試範圍

- OOP Design
- Product Design
- Frontend Design
- Infrastucture

### Product Design

Product Design Interview 是系統設計的一個主要類型，考驗的是如何設計一個符合需求的系統，或是如何達成特定的 use case

- Design a ride-sharing service like uber
- Design the backend for a chat application that supports 1:1 and group chats

### Infrastructure Design

Infrastructure Design 比起 product design 的出現頻率更低，但依然算是常見，這類型的模式會詢問你要怎麼實現一個基礎設施，像是 message broker 或是 rate limiter，並會問及其中的關鍵演算法跟底層觀念

- Design a rate limiter
- Design a message broker
- Design a key-value store

### Object Oriented Design

Object Oriented Design 考驗的是你物件導向設計的能力，你怎麼設計一個物件，合理定義其屬性跟行為、遵守 SOLID，並良好的映射實體，自己沒聽說台灣有考這類面試，美國滿常見的（From Harry）

OOP （封裝、繼承、多型），使用 OOP 概念實現一個物件

Java 考基本繼承觀念，有關物件導向的語法（Instance of）

### Frontend Design

Frontend Design 通常會問的是為特定 APP 設計一個前端

- Design the frontend for a spreadsheet application
- Design the frontend for a video editor

### 面試重點

面試就是一個說服的過程，透過技巧來說服對方是相當有效且重要的

系統設計面試隨著工程師年資的成長，會逐漸的從廣度轉為深度，深入了解平常使用的工具、技術是如何運作的相當重要

分解問題、找出核心問題並解決是面試過程中面試官期望看見的，也是大多數人失敗的地方，通常會落入幾種窘境

- 可以先從 high-level 討論
- 沒有花足夠心力去探索問題跟搜集需求
- 專注在枝微末節的小事上，沒有關注最重要的問題
- 被問題的特定部分卡住而不繼續往前推進

#### High-Level Design

High-Level Design，如何解決每個部分的問題，並且能將解決方案聚合起來成一個整體，這考驗你“核心觀念”的紮實程度。通常會因為以下原因失敗

- 對核心觀念的理解不夠
- 沒有考慮 scaling 跟 performance
- 混亂無章法的設計

#### Technical Excellence

Technical Excellence，要設計一個系統，你需要知道常用的 component 有哪些、使用場景、優缺點為何，並且能夠將他們有系統的組合起來。常犯的問題有

- 對可用的技術不熟悉
- 不知道這些技術的使用場景
- 沒辦法識別常見的使用模式跟最佳實踐

#### Communication and Collaboration

系統設計沒有完美答案，這過程中需要頻繁的討論跟調整設計，這考驗了你如何溝通複雜的概念、應對回饋跟問題。常犯的問題有

- 沒辦法清晰的說明複雜的概念
- 沒辦法良好的應對反饋
- 迷失方向，無法跟面試官一起解決問題
