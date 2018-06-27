---
title: 連線進入VM-2
date: 2018-06-22 15:31:25
tags:
---

### 連線進入 VM windows

### 總共有2種方法可以進入 VM 本篇文章將依序作介紹

### 一、 使用 GCP 開啟新視窗連線

### 建立好 VM 後有可能尚未準備好接受 RDP 連接，因為所有 OS 組件都需要一段時間才能初始化

### 要查看服務器是否已準備好進行 RDP 連接，請在 Cloud Shell 終端命令行上運行以下命令 ( 會詢問是否在此區域是非題選對就會繼續下去 )

```
gcloud compute instances get-serial-port-output ( VM 名稱 )
```

### ex：gcloud compute instances get-serial-port-output test

### 重複該命令，直到在命令輸出中看到以下內容，代表 OS 初始化成功

![ ](images/1.png)

### OS 初始化成功後，點擊遠端桌面通訊協定旁的 ▼ ，在點擊設定 Windows 密碼

![ ](images/2.png)

### 設定使用者名稱 ( 使用者預設是帳號，但不建議使用使用同樣使用者名稱會把用同一個名稱的 VM 密碼洗掉換成同一個 )

![ ](images/3.png)

### 複製密碼

![ ](images/4.png)

### 接下來直接點擊遠端桌面通訊協定

![ ](images/5.png)

### 將會開啟新瀏覽器，輸入使用者名稱跟剛剛複製的密碼就可以登入了

![ ](images/6.png)

### 點擊繼續以確認您要連接

![ ](images/7.png)

### 恭喜連線成功！

![ ](images/8.png)

***

### 二、Windows 內建登入

### 取得使用者名稱跟密碼 ( 取得方式跟用 GCP 開啟新視窗連線一樣 )

### 打開搜尋輸入 mstsc 選擇遠端桌面連線

![ ](images/9.png)

### 或是開始鍵 + R 輸入 mstsc

![ ](images/10.png)

### 輸入欲登入 VM 外部 IP

![ ](images/11.png)
![ ](images/12.png)

### 輸入設定好的使用者名稱跟密碼

![ ](images/13.png)

### 選擇是

![ ](images/14.png)

### 恭喜連線成功！

![ ](images/15.png)