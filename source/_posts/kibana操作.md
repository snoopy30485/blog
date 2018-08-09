---
title: kibana操作
date: 2018-08-01 17:06:52
tags:
---

### kibana 操作、版本：5.6.7

### 第一次進入畫面

![ ](images/1.png)

### 設定 index，本文章適用預設所以是 winlogbeat，Time Filter field name 選擇 @timestamp

![ ](images/2.png)

***

### 接下來將以最左邊工具作分類介紹

### 一、 Discover : 做資料查詢，並檢視各索引下的記錄內容及總記錄筆數，本文章分成 5 區將一一作介紹

![ ](images/3.png)

### (1) Index : 純粹看目前所在的 index 是哪一個 ( 不再另外作介紹 )

### (2) Avaliable Fields : 搜索 index 下所包含的欄位

### (3) Timestamp : 資料時間，可用於特定時間區間資料量觀察，直接選取可以查看想要時間範圍內的 log

### (4) source : 也就是我們先前所儲存的資料內容，可以展開查看更詳細內容

### (5) 搜尋條件儲存 : 預設 ”*“ 搜尋 index 下所有紀錄，設定需要 log 時間並儲存

### 各區介紹

### (2) Avaliable Fields : 搜索 index 下所包含的欄位

### 可以選擇 add 加入，顯示自己想看的欄位

![ ](images/4.png)

### 點選 Available Fields 的齒輪可以篩選欄位，以更快查詢需要的 log

![ ](images/5.png)

### 如果不需要可以按 remove 移除

![ ](images/6.png)

### 點選放大鏡 + 可以直接在 source 訊息裡顯示你要的欄位

![ ](images/7.png)