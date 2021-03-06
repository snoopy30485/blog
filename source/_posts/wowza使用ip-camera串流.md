---
title: wowza使用ip-camera串流
date: 2018-11-02 13:41:35
tags: 流媒體服務器
categories: 流媒體服務器
---

### 本章將講解如何使用 ip camera 串流 wowza

<!-- more -->

#### 先登入 wowza

![ ](images/1.png)

#### 下圖為登入後畫面，點選上方的 Application 建立一個新的 live Application

![ ](images/2.png)

#### 進入 Application 後，點選 Live

![ ](images/4.png)

#### 輸入名稱

![ ](images/3.png)

#### 進入設定畫面，下圖紅框部分是允許進入格式，剩下的選項預設 ( 有機會會再做篇文章介紹 )，設定好後點擊 Save 儲存

![ ](images/5.png)

#### 儲存好後會進入下圖畫面，設定隨時都可以更改 ( 左上 live Application 點選後會進入到一開始進去畫面 )

![ ](images/6.png)

#### 建立好 live Application 後 ip camera 本文章介紹二個串流輸入的方法

#### 一、 點選左邊 Sources ( Live )，裡面有預設選項讓你選，是依照 ip camera 廠牌做分類，但不是全部廠牌都有沒有要用另一種方法加入

![ ](images/7.png)

#### 本文章使用 ip camera 牌子是 AXIS

![ ](images/8.png)

#### 點擊後會需要輸入 stream name 和 camera ip address

```
camera ip address 輸入方式為：

ip camera 帳號：ip camera 密碼@ip camera ip

ex: test:test@1.1.1.1
```

![ ](images/9.png)

#### 加入好會進入下圖畫面 ( Incoming Streams ) 右邊 Bytes In 顯示數字就是畫面有進 wowza 了 ( 沒有可以點擊 Refresh 刷新一下 ) 點擊 Return to Incoming Streams Page 返回上一頁

![ ](images/10.png)

#### 下圖 Active 代表正在正常運作

![ ](images/11.png)

#### 如果 ip 或是密碼打錯 port 沒開等等問題，就會出現 Waiting for Stream

![ ](images/12.png)

#### 到這邊設定就完成了

#### 二、 第二種串流方法點選左邊的 Stream Files 進入後點選上方的 Add Stream Files 新增

![ ](images/13.png)

#### 輸入 Stream Files name 跟 Stream URI ( URI 如果不知道可以到 ip camera 的官網查 )

```
Stream URI 輸入方式為：

rtsp://ip camera 帳號：ip camera 密碼@ip camera ip/產品型號的 URI

ex: rtsp://test:test@1.1.1.1//axis-media/media.amp
```

![ ](images/14.png)

#### 加入好會進入下圖畫面 ( Stream Files ) 點擊 Return to Stream Files 回上一頁

![ ](images/15.png)

#### 這種方式串流只有建立一個新的 Stream Files，Incoming Stream 不會幫你串流起來，點擊下圖紅框圖案串流

![ ](images/16.png)

#### 點擊後在 MediaCaster Type 選擇你 ip camera 進來的格式，其他選項預設就好

![ ](images/17.png)

#### 出現如下圖紅框文字就是成功了

![ ](images/18.png)

#### 再到 Incoming Streams 確認是否輸入

![ ](images/19.png)

#### 三、 wowza 有測試功能可以看影片是否有串流成功

#### 右上角會有一個 Test Players

![ ](images/20.png)

#### 點擊後會出現一個播放畫面 server：安裝 wowza 機器 ip ( 如果是本機開啟可以用 127.0.0.1 或內網 IP )、Application：live Application Name、Stream：Stream Name.stream

![ ](images/21.png)

#### PS.進入 Incoming Streams 選擇要觀看的 stream 進去後再點 Test Players 數值就會都幫你設定好

![ ](images/22.png)

#### 也可以使用有串流的播放器做測試 ( 本文章使用的是 VLC )

![ ](images/23.png)

#### 點擊媒體 → 開啟網路串流

![ ](images/24.png)

#### 輸入串流網址

```
rtmp://wowza ip:1935/live Application 名稱/Stream Name.stream

ex：rtmp://35.201.252.199:1935/test/test.stream
```

![ ](images/25.png)

#### 如下圖出現畫面就成功了

![ ](images/26.png)

#### PS.到 Incoming Streams stream 點進去可以看到 Bytes Out 輸出 ( 只有直接從 wowza 輸出這邊才會顯示 )

![ ](images/27.png)

#### 到這邊 ip camera 到 wowza 這段就完成了