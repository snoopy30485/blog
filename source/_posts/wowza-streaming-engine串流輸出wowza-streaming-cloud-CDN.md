---
title: wowza-streaming-engine串流輸出wowza-streaming-cloud-CDN
date: 2018-11-23 11:36:20
tags:
---
### 本文章將介紹如何使用 wowza engine 串流輸出到 wowza cloud CDN

#### 1. 首先登入 wowza cloud 來到 Advanced 頁面

![ ](images/1.png)

#### 2. 再次點擊 Advanced 選擇 Stream Targets

![ ](images/2.png)

#### 3. 點擊 Add Target 選擇 Wowza CDN - HLS 新增 CDN

![ ](images/3.png)

#### 4. 設定名稱其他選項預設，點選 Add 加入

![ ](images/4.png)

#### 5. 下圖是設定好畫面紅框為連接代碼，帶有1的代碼用於將目標連接到 Wowza Streaming Engine

![ ](images/5.png)

#### 6. 再來到 wowza streaming engine → Stream Targets → Add Stream Targers 新增輸出

![ ](images/6.png)

#### . 選擇 wowza streaming cloud 把串流輸出到剛剛 wowza 雲端建好的 cdn

![ ](images/7.png)

#### . 輸入名稱 Stream Target Name，輸入連線代碼 Connection Code ( 連線代碼為在 wowza cloud 建立好 cdn 給的代碼 )

![ ](images/8.png)

#### . 點擊 Check Code 輸入 

https://snoopy30485.github.io/2018/11/02/wowza%E4%BD%BF%E7%94%A8ip-camera%E4%B8%B2%E6%B5%81/