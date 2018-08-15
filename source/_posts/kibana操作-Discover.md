---
title: kibana操作-Discover
date: 2018-08-01 17:06:52
tags:
---

### kibana 操作-Discover、版本：5.6.7

### 第一次進入畫面

![ ](images/1.png)

### 設定 index，本文章適用預設所以是 winlogbeat，Time Filter field name 選擇 @timestamp

![ ](images/2.png)

### 設定好後畫面

![ ](images/14.png)

***

### Discover : 做資料查詢，並檢視各索引下的記錄內容及總記錄筆數，本文章分成 5 區將一一作介紹

![ ](images/3.png)

### 1. Index : 純粹看目前所在的 index 是哪一個 ( 不再另外作介紹 )

### 2. Avaliable Fields : 搜索 index 下所包含的欄位

### 3. Timestamp : 資料時間，可用於特定時間區間資料量觀察，直接選取可以查看想要時間範圍內的 log

### 4. source : 也就是我們先前所儲存的資料內容，可以展開查看更詳細內容

### 5. 搜尋條件儲存 : 預設 ”*“ 搜尋 index 下所有紀錄，設定需要 log 時間並儲存

***

### 各區介紹

### 2. Avaliable Fields : 搜索 index 下所包含的欄位

### 可以選擇 add 加入，顯示自己想看的欄位

![ ](images/4.png)

### 點選 Available Fields 的齒輪可以篩選欄位，以更快查詢需要的 log

![ ](images/5.png)

### 如果不需要可以按 remove 移除

![ ](images/6.png)

### 點選放大鏡 + 可以直接在 source 訊息裡顯示你要的欄位

![ ](images/7.png)

### Add a filter 可以加入自己想看的獨欄位的一種條件做 log 查詢

![ ](images/8.png)

### 當加入一個欄位，可以點選 Actions 做欄位的調整

### Enable 啟用、Disable 禁用、Pin 釘選、Unpin 取消釘選、Invert 加入或刪去欄位、Toggle 隱藏、Remove 移除

![ ](images/9.png)

### 左上搜尋條件角滑鼠移上去會顯示圖案，圖案的功能其實跟點選 Actions 後出現的差不多

### 打勾：取消後 source 就不會找出你所設定欄位

### 放大鏡 -：刪去這項欄位

### 圖釘：釘選

### 垃圾桶：刪除

### 框框：編輯欄位

![ ](images/10.png)

***

### 3. Timestamp : 資料時間，可用於特定時間區間資料量觀察，直接選取可以查看想要時間範圍內的 log

![ ](images/11.png)

### 中間下拉式選單，可以選擇時間間隔

### millisecond 毫秒、second 秒、minute 分鐘、hourly 每小時、daily 每日、weekly 每週、monthly 每月、yearly 每年

![ ](images/12.png)

***

### 4. source : 也就是我們先前所儲存的資料內容，可以展開查看更詳細內容

![ ](images/13.png)

***

