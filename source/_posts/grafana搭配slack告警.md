---
title: grafana搭配slack告警
date: 2018-08-03 14:12:11
tags: grafana
categories: grafana
---

## 本篇文章將介紹把告警傳送到 slack

<!-- more -->

### 一、首先先註冊一個 slack 的帳號與下載 slack 的應用程序或 app

![ ](images/1.png)

### 二、slack 點選 channel，創建頻道

![ ](images/2.png)

### 三、為頻道命名

![ ](images/3.png)

### 四、點選 got it 正式啟用頻道

![ ](images/4.png)

### 五、點選 add people to this channel 加入團隊成員到頻道中

![ ](images/5.png)
![ ](images/6.png)

### 六、前往 slack 的a pp Directory 應用程序，登入後右上角選擇要發送告警通知的 channel

### 網址：https://slack.com/apps

![ ](images/7.png)

### 七、在下方搜尋地方輸入 incoming webhooks 搜尋

![ ](images/8.png)
![ ](images/9.png)

### 八、點選 add configuration 申請 channel 的 url

![ ](images/10.png)

### 九、選擇頻道，然後點擊 add incoming webhooks integration

![ ](images/11.png)
![ ](images/12.png)

### 十、申請好就可以看到頻道 url，複製下來 grafana 告警會用到

![ ](images/13.png)

### 沒複製到 url 回到 incoming webhooks 畫面，可以看到你申請好的頻道，點擊右邊鉛筆進入編輯就可以在看到 url

![ ](images/14.png)

### 十一、在來回到 grafana 左邊列表點選鈴鐺，選擇 notification channels

![ ](images/15.png)

### 十二、點擊 add channel 創建告警頻道

![ ](images/22.png)

### 進入畫面

![ ](images/16.png)

### 十三、 type 選擇 slack，url 輸入剛剛在 incoming webhooks 獲得的 url，然後點擊 sent test 會發一個測試訊息到 slack

![ ](images/17.png)
![ ](images/18.png)

### 發送的測試訊息

![ ](images/19.png)

### 發送成功後就點選 save 儲存

![ ](images/20.png)

### 回到 notification channels 會看到設置好的告警頻道

![ ](images/21.png)

### 十四、告警測試，到拉好的圖表設定，選擇分頁的 alert 選擇左列的 alert config 設定成會告警的狀態

![ ](images/23.png)

### 十五、在到左列的 notifications 選擇告警頻道

![ ](images/24.png)

### 十六、告警發送後會發現 slack 只有訊息沒有圖片，下一張將介紹保存告警圖片到 gcs

![ ](images/25.png)