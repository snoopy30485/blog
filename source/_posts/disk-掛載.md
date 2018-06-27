---
title: disk-掛載
date: 2018-06-27 09:45:14
tags:
---

### 一、創建硬碟

### 到 Compute Engine → 磁碟創建一個磁碟

![ ](images/1.png)
![ ](images/2.png)
![ ](images/3.png)

### 也可以用指令創建 ( 記得 zone 要設定跟 VM 同區，名稱不能跟 VM 一樣 )

```
gcloud compute disks create (名稱) --size=(容量) --zone (區域)
```

### 輸出畫面

![ ](images/4.png)

### 新增進使用中 VM


