---
title: 設定遠端帳號權限為Remote-Desktop-Users
date: 2018-06-23 12:52:37
tags: windows
categories: windows
---

### 本文章將介紹把帳號設定為 Remote Desktop Users 權限

<!-- more -->

#### 1. 在開始的地方點擊滑鼠右鍵選擇 Computer Management ( 電腦管理 )

![ ](images/1.png)

#### 2. 到 Local Users and Groups ( 本機使用者和群組 ) → Users 可以看到目前有哪些帳號

![ ](images/2.png)

#### 3. 到 Local Users and Groups ( 本機使用者和群組 ) → Groups 會看到很多群組，點擊2下 Remote Desktop Users

![ ](images/3.png)

#### 4. 點擊2下 Remote Desktop Users 點選 Add 後需要設定權限帳號加進去，點選 Check Names 確認是否有這個帳號，點選 ok

![ ](images/4.png)
![ ](images/5.png)
![ ](images/6.png)

#### 5. 點選 Apply 套用，點選 ok

![ ](images/7.png)

#### 6. 再回到 Local Users and Groups ( 本機使用者和群組 ) → Users

![ ](images/2.png)

#### 7. 對剛剛設定好的帳號右鍵點選 Properties ( 內容 )

![ ](images/8.png)

#### 8. 點擊上方分頁 Member Officer ( 成員隸屬 )，點擊 Administrators 在點擊下面 Remove 移除，在點擊 Apply ok 就完成了

![ ](images/9.png)

#### 到這邊就設定完成了