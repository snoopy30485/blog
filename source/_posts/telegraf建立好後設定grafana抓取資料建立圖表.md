---
title: telegraf建立好後設定grafana抓取資料建立圖表
date: 2018-08-03 14:12:10
tags: grafana
categories: grafana
---

## 本文章將介紹 telegraf 收集完資料傳到 influxdb 後 grafana 抓取資料建立圖表

<!-- more -->

### 一、第一次建好登入可以看到首頁 install grafana 顯示打勾圖案，代表那個步驟完成了，所以接下來我們要做下個步驟點擊 add data source，這個步驟是在配置我的數據來源 ex：influxdb、elasticsearch...

![ ](images/1.png)

### 也可以到左邊列表點擊齒輪，選擇 data sources

![ ](images/2.png)

### 二、開始配置 data sources

### 進入畫面

![ ](images/3.png)

### type 選擇 influxdb

![ ](images/4.png)

### http 輸入 http://influxdb:8086，database 輸入你在 telegraf 設定的名稱

![ ](images/5.png)

### 接下來到最下面，點擊 save & test 資料都正確且有抓到右上角就會顯示 datasource added

![ ](images/6.png)

### 回到 data sources 畫面，就會看到已經新增的 data sources

![ ](images/7.png)

### 三、拉圖表測試

### 點擊左邊列表四個方塊，選擇 home 回到首頁

![ ](images/8.png)

### 選擇 new dashboard

![ ](images/9.png)

### 或是左邊列表點擊 + 選擇 dashboard

![ ](images/10.png)

### 選擇想要的圖表類型

![ ](images/11.png)
![ ](images/12.png)

### 點擊 panel title 選擇 edit 編輯圖表

![ ](images/13.png)

### 進入畫面

![ ](images/14.png)

### 在 data source 選擇你建立好的 data source

![ ](images/15.png)

### 如圖下方調整你想看的參數，設定有正確上方就會顯示數據

![ ](images/16.png)

### 記得儲存

![ ](images/17.png)

### 回到 dashborad 就可以看到你拉好的圖表，可以拉好幾個不同種類的圖表，依個人喜好製作自己的監控圖吧

![ ](images/18.png)