---
title: wowza-stream-engine串流輸出到wowza-streaming-cloud
date: 2018-11-23 11:36:19
tags:
---

### 本文章將介紹 wowza-engine 串流輸出到 wowza-cloud 的基本操作

#### 首先登入 wowza streaming cloud

![ ](images/1.png)

#### 點選 Live Streams

![ ](images/2.png)

#### 點擊左上方或下方的 Add Live Stream 新增直播

![ ](images/3.png)

#### 輸入 live stream 選擇地區

![ ](images/4.png)

#### 選擇輸入進來的方式，本文章使用 wowza streaming engine，下方設定分別為長寬、是否錄製成影片、隱藏字幕類型

![ ](images/5.png)
![ ](images/6.png)

#### 撥放設置依序份別為：撥放瀏覽器選擇、撥放器寬度、直播開始前撥放器顯示時間倒數、撥放前畫面顯示圖片、撥放中顯示圖片、圖片放置位置

![ ](images/7.png)

#### 託管設置依序分別為：是否讓 wowza 託管撥放是頻網頁、標題、託管葉面上放置圖片、說明

![ ](images/8.png)

#### 最後一頁會把你的設置列出來給你看

![ ](images/9.png)

#### 全部設定好會進入下圖畫面，複製紅框代碼

![ ](images/10.png)

#### 接下來到 wowza streaming engine → Stream Targets 選擇 wowza streaming cloud

![ ](images/11.png)

#### 輸入 Stream Target Name、再輸入從 wowza streaming cloud 拿到的代碼，輸入完點擊 Check Code 做確認

![ ](images/12.png)

#### 點擊完 Check Code 會出現 Source Stream Name 輸入你 Incoming Stream 串流的名稱

![ ](images/13.png)

#### 再來回到 wowza streaming cloud → live streams 點選下圖紅框的 Start Live Stream 開始直播

![ ](images/14.png)

#### 點擊 Start Live Stream 會出現下圖提示點擊 Start

![ ](images/15.png)

#### 接下來會跑讀條成功就出現 Ready

![ ](images/16.png)
![ ](images/17.png)

#### 下圖出現畫面直播就開始了，下方紅框為手機使用串流網址

![ ](images/18.png)

#### 也可以點選分頁的 Playback 觀看

![ ](images/19.png)

#### 或是點選 Monitior 下圖點擊紅框圖案會另外開啟一個分頁直播畫面

![ ](images/20.png)
![ ](images/21.png)

#### PS.如果有停止或是重啟動作，會需要再重新輸入一次代碼

![ ](images/22.png)

#### 要到 Video Source and Transcoder 下方 Regenerate Connection Code 重新取得代碼

![ ](images/23.png)
![ ](images/24.png)

#### 到這邊就完成了