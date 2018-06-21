---
title: 連線進入VM
date: 2018-06-21 14:47:21
tags:
---

# 遠端連線進入 VM 

### 總共有4種方法可以進入 VM 本篇文章將依序作介紹

### 一、 創建好 VM 後直接點擊右邊 SSH 或是 ▼ 在瀏覽器視窗中開啟

![ ](images/1.png)

### 點擊完後會另外再開一個視窗

![ ](images/2.png)
![ ](images/3.png)

### 連進去後在 Compute Engine → 中繼資料 → SSH 金鑰會幫你加金鑰

![ ](images/4.png)
![ ](images/5.png)

### 二、 使用 Cloud Shell 連線

### 打開 Cloud Shell

![ ](images/6.png)

### 使用指令連線進入

```
gcloud compute ssh (VM名稱) --zone (區域) 
```

### ex：gcloud compute ssh test --zone asia-east1-b	

### 輸入 y 繼續

![ ](images/7.png)

### 生成公鑰/私鑰，會輸入密碼點2下 Enter 使用空密碼

![ ](images/8.png)

### 看到使用者改了就是進去了

![ ](images/9.png)
![ ](images/10.png)

### 三、 使用 SDK 連線

### 安裝 SDK 下載和說明：https://cloud.google.com/sdk/

### 打開 SDK 

![ ](images/11.png)

### 如果帳號不對要記得切換帳號

```
gcloud auth login 帳號
```

![ ](images/12.png)

### 可以下指令檢查一下

```
gcloud auth list
```

![ ](images/13.png)

### 切換帳號它會開個網頁讓你選目前想用的帳號

![ ](images/14.png)
![ ](images/15.png)