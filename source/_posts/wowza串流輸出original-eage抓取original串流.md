---
title: wowza串流輸出original-edge抓取original串流
date: 2018-11-09 15:29:30
tags:
---

### 如下圖 wowza 串流輸出 original、edge 抓取 original 串流

![ ](images/15.png)

#### 進入 wowza Stream Targets

![ ](images/1.png)

#### 點擊 Enable Stream Targets 開啟

![ ](images/2.png)

#### 這時候 wowza 會要求你重新整理點擊右上 Restart Now 重新整理

![ ](images/3.png)

#### 重新整理過後 Incoming Stream 串流會自己斷掉，要到 Stream Files 重新在串流一次

![ ](images/4.png)
![ ](images/5.png)

#### 串流好了後回到 Stream Targets 點擊 Add Stream Targets

![ ](images/6.png)

#### 選擇一種方式輸出，本文章是使用 RTMP

![ ](images/7.png)

#### 輸入 Stream Targets Name ( 隨意命名 )、Source Stream Name ( Stream Files Name )、Destination Application Name ( Original 串流位置資料夾名稱 )、Destination Host ( Original IP )、Destination Stream Name ( Original 串流輸出名稱 )

![ ](images/8.png)

#### 設定好後如下圖，出現 Active 就是成功輸出了

![ ](images/9.png)

#### 如果設定錯誤會出現 Error

![ ](images/10.png)

#### 如果出現 Waiting 代表串流沒有輸入可以到 Incoming Streams 看

![ ](images/11.png)
![ ](images/12.png)

#### 接下來測試出輸出 original 是否成功，打開撥放器 VLC，輸入串流網址

```
original 串流網址輸入方式為：

格式://original ip:1935/original 輸入串流所創的資料夾/wowza Stream Targets 建立要輸入 original 的名稱 ( Destination Stream Name )

ex：rtmp://35.201.252.199:1935/live-demo/test
```

![ ](images/13.png)

#### #### 如下圖出現畫面就成功了

![ ](images/14.png)

#### 再來是測試 edge 能否抓取 original 的串流，打開撥放器 VLC，輸入串流網址

#### PS.在安裝 edge 文章有介紹指令 sed -i '208c<RouteEntry>*:*;10.140.0.3:1935</RouteEntry>' /opt/adobe/ams/conf/_defaultRoot_/_defaultVHost_/Vhost.xml，此只主要為抓取 original 的串流

```
original 串流網址輸入方式為：

格式://edge ip:1935/original 輸入串流所創的資料夾/wowza Stream Targets 建立要輸入 original 的名稱 ( Destination Stream Name )

ex：rtmp://35.229.145.147:1935/live-demo/test
```

![ ](images/16.png)

#### #### 如下圖出現畫面就成功了

![ ](images/14.png)