---
title: google-command-SDK安裝
date: 2018-06-27 16:41:22
tags: GCP
categories: GCP
---

### 本文章將介紹安裝 google command SDK

<!-- more -->

#### 1. 首先到官網，點擊 Google Cloud SDK installer 下載安裝檔 [官方下載連結](https://cloud.google.com/sdk/docs/quickstart-windows)

![ ](images/1-1.png)

#### 2. 點擊 GoogleCloudSDKinstaller.exe 開始安裝

![ ](images/2.png)
![ ](images/3.png)

#### 3. 同意條款

![ ](images/4.png)

#### 4. 安裝類型單個用戶或所有用戶，依自己需求選擇

![ ](images/5.png)

#### 5. 選擇安裝地方

![ ](images/6.png)

#### 6. 選擇要安裝組件，依自己需求選擇

![ ](images/7.png)

#### 7. 安裝畫面，安裝好點擊 Next 繼續下一步

![ ](images/8.png)
![ ](images/9.png)

#### 8. 點擊 Finish 是否啟動 SDK、是否建立桌面捷徑等項目，依自己需求選擇

![ ](images/10.png)

#### 9. 登入帳戶

#### 下指令登入帳戶，會取得一串 URL

```
gcloud auth login
```

![ ](images/16.png)

#### 10. 開啟網頁複製貼上 URL，選擇帳戶然後點選允許

![ ](images/17.png)
![ ](images/18.png)

#### 11. 允許後會給一串授權碼，複製貼回 SDK

![ ](images/19.png)
![ ](images/20.png)

#### 12. 貼回 SDK 後會顯示這個帳號有哪些專案，選擇自己想要的專案後會需要再選擇地區和區域，選完設定就結束了

![ ](images/21.png)
![ ](images/22.png)

#### 13. 選擇完後會把設定檔存起來，下指令可以看你有那些設定檔，適合多帳號專案使用

```
gcloud config configurations list
```

![ ](images/23.png)


#### 14. 針對不同的工作可以切換不同的設定檔，正在使用中的設定檔 IS_ACTIVE 會顯示 True

```
gcloud config configurations activate [config name]
```

![ ](images/24.png)

#### 刪除設定檔

```
glcoud config configurations delete [config name]
```

#### 15. 重開設定檔，可重開新的或選擇舊的重新設定

```
gcloud init
```

![ ](images/25.png)