---
title: 設定wowza-HLS低延遲
date: 2018-11-23 11:36:21
tags: 流媒體服務器
categories: 流媒體服務器
---

### 本文章將介紹如何調整 HLS 低延遲

<!-- more -->

#### 1. 首先在 Applications 選擇想設定低延遲的 Live Applications 點擊 Edit 

![ ](images/1.png)

#### 2. 選擇 Low-latency stream ( ideal for chat applications )

![ ](images/2.png)

#### 3. 設定好後點選 Save 需要重新整理

![ ](images/3.png)

#### 4. 也可以再建立 Live Applications 的時候先設定好

![ ](images/4.png)

#### 5. 設定好 Low-latency stream 點選上面分頁 Properties

![ ](images/5.png)

#### 6. Quick Links 選擇 Cupertino Streaming Packetizer

![ ](images/6.png)

#### 7. 點選 Edit 後開始設定裡面參數 cupertinoChunkDurationTarget 設定 1000 ( 1000毫秒等於1秒 )、cupertinoMaxChunkCount 設定 50、cupertinoPlaylistChunkCount 設定 12

![ ](images/7.png)
![ ](images/8.png)

#### 8. 設定好後一樣要重新整理

![ ](images/9.png)

#### 9. 設定好後回到 Quick Links 選擇 Custom

![ ](images/10.png)

#### 10. 點選 Edit 點選 Add Custom Property 後開始設定參數

![ ](images/11.png)
![ ](images/12.png)

#### 11. 參數為 Path：/Root/Application/LiveStreamPacketizer、Name：cupertinoMinPlaylistChunkCount、Type：Integer、Value：6

![ ](images/13.png)

#### 12. 設定好後一樣要重新整理

![ ](images/9.png)

#### 到這邊就設定完成了