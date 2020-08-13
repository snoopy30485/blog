---
title: wowza使用GoCoder串流
date: 2018-11-15 13:43:22
tags: 流媒體服務器
categories: 流媒體服務器
---

### 本文章將介紹用手機 GoCoder 串流 wowza

<!-- more -->

#### 首先手機先下載 GoCoder

![ ](images/1.jpg)

#### 下圖為開啟畫面

![ ](images/2.jpg)

#### 點擊右上做設定 ( 串流 wowza engine 只需要設定 Wowza Stream Engine )

![ ](images/3.jpg)

#### 進入 wowza web → Source ( Live )，點擊 wowza GoCoder 裡面有一些參數，除了 IP ( 需要輸入外網 IP ) 其他可以對照輸入

![ ](images/4.png)
![ ](images/5.png)

#### 點擊 Wowza Stream Engine 會出現3個需要設定選項

![ ](images/6.jpg)

#### 設定 Host：輸入外網 IP，Port：1935 ( wowza 預設串流 port )

![ ](images/7.jpg)

#### 設定 Application：wowza live application name，Stream Name：GoCoder 預設都是 myStream ( 更改後 Incoming Streams 會顯示更改後名稱，PS.同樣名稱二支手機會互搶 )

![ ](images/8.jpg)

#### 手機 GoCoder Source Authentication 要到 wowza Server → Source Authentication → Add Source 新增 Source

![ ](images/10.png)
![ ](images/11.png)

#### 設定 Source Authentication：wowza 所設定的 Source Authentication

![ ](images/9.jpg)

#### 點擊右下紅點開始串流

![ ](images/12.jpg)

#### 串流後畫面如下圖 ( 一些 GoCoder 其他設定有空會再做文章介紹 )

![ ](images/13.jpg)

#### 可以到 Inconing Streams 會發現串流正在在執行 ( 使用 GoCoder 的方式是不會有 Stream Files )

![ ](images/14.png)

#### 設定完後做測試，打開 VLC 輸入串流網址

![ ](images/15.png)

#### 下圖有畫面就是成功了

![ ](images/16.png)