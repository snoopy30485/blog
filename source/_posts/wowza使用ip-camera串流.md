---
title: wowza使用ip-camera串流
date: 2018-11-02 13:41:35
tags:
---

### 本章將講解如何使用 ip camera 串流 wowza

#### 先登入 wowza

![ ](images/1.png)

#### 下圖為登入後畫面，點選上方的 Applications 建立一個新的 live applications

![ ](images/2.png)

#### 輸入名稱

![ ](images/3.png)

#### 進入 Applications 後，點選 Live

![ ](images/4.png)

#### 名稱輸完後會進入設定畫面，下圖紅框部分是允許進入格式，剩下的選項預設 ( 有機會會再做篇文章介紹 )，設定好後點擊 Save 儲存

![ ](images/5.png)

#### 儲存好後會進入下圖畫面，設定隨時都可以更改，左上是建立另一個新 live applications 也可以從這邊點選

![ ](images/6.png)

#### 建立好後 live applications 有2個接 ip camera 的方法

#### 一、 點選左邊 Sources ( Live )，裡面有預設選項讓你選

![ ](images/7.png)

#### 本文章使用 ip camera 牌子是 AXIS

![ ](images/8.png)

#### 點擊後會需要輸入 stream name 和 camera ip address

```
camera ip address 輸入方式為：

ip camera帳號：ip camera密碼@ip camera ip

ex: test:test@1.1.1.1
```

![ ](images/9.png)