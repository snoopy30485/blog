---
title: GCP-設定DNS網域
date: 2018-06-20 09:51:16
tags: GCP
categories: GCP
---

## 本篇文章降介紹如何在 GCP 設定 DNS 網域

<!-- more -->

### 租好網域後，接下來到 GCP 設定 DNS 網域 ( 本文章是租用 GoDaddy 網域 )

![ ](images/10.png)

### 一、開啟 GCP 導覽選單選擇網路 → Cloud DNS

![ ](images/1.png)

### 二、點選建立區域

![ ](images/2.png)

### 三、輸入區域名稱 (名稱隨意)，DNS 要輸入你租的網域名稱，輸入完點選建立

![ ](images/3.png)

### 四、建立好了之後會產生兩個記錄集，將記錄類行為 NS 的名稱伺服器複製到你租的網域空間那邊的 DNS 設定裡

![ ](images/4.png)

### 點一下右邊鉛筆可以做編輯

![ ](images/6.png)

### ex：GoDaddy 的 DNS 設定

![ ](images/5.png)

### 五、點選新增記錄集，建立新的記錄集

![ ](images/7.png)

### 六、資源類型選 A、IPv4 位址輸入 VM 外網 IP，輸入完後點選建立

![ ](images/8.png)

### 建立完成回到 Cloud DNS 會看到新的記錄集出現，半小時內就會綁定成功

![ ](images/9.png)