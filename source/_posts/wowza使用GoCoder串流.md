---
title: wowza使用GoCoder串流
date: 2018-11-15 13:43:22
tags:
---

### 本文章將介紹用手機 GoCoder 串流 wowza

#### 首先進入手機下載 GoCoder

![ ](images/1.jng)

#### 下圖為開啟畫面

![ ](images/2.jng)

#### 點擊右上做設定 ( 串流 wowza engine 只需要設定 Wowza Stream Engine )

![ ](images/3.jng)

#### 進入 wowza webwowza → Source ( Live )，點擊 wowza GoCoder 裡面有一些參數，除了 IP 輸入外網 IP 其他可以對照輸入

![ ](images/4.png)
![ ](images/5.png)

#### 點擊 Wowza Stream Engine 會出現3個需要設定選項

![ ](images/6.jng)

#### 設定 Host：因為是用手機連記得設定外網 IP，Port：1935 wowza 預設串流 port

![ ](images/7.jng)

#### 設定 Application：wowza live application name，Stream Name：GoCoder 預設都是 myStream

![ ](images/8.jng)

#### 手機 GoCoder Source Authentication 要到 wowza Server → Source Authentication → Add Source 新增 Source

![ ](images/10.png)
![ ](images/11.png)

#### 設定 Source Authentication：wowza 所設定的 Source Authentication

![ ](images/9.jng)

#### 點擊右下紅點開始串流

![ ](images/12.jng)

#### 串流後畫面如下圖 ( 一些 GoCoder 其他設定有空會再做文章介紹 )

![ ](images/13.jng)

#### 可以到 Inconing Streams 會發現串流正在在執行 ( 使用 GoCoder 的方式是不會有 Stream Files )

![ ](images/14.png)

#### 設定完後做測試，打開 VLC 輸入串流網址

![ ](images/15.png)

#### 下圖有畫面就是成功了

![ ](images/16.png)

#### PS.手機使用 GoCoder 串流到 wowza 一次只能一台手機使用，下一台手機使用會把上一台畫面蓋掉