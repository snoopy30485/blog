---
title: 安裝AMS_Original_ubuntu
date: 2018-11-08 15:26:58
tags:
---

### AMS_Original 安裝包下載：https://drive.google.com/open?id=1ZoMojUk21mlRwmCl90mylBCVHpClugQ-

#### 將安裝包放入後按照下方指令開始安裝

```
tar -xvf ams-original.tar.gz

cd AMS_5_0_6_r6102/

./installAMS
```

#### 下完指令安裝畫面，按下 Enter 確認安裝 AMS，再按 Enter or Space 鍵直到閱讀完 License

![ ](images/1.png)

#### 是否同意，輸入 y

![ ](images/2.png)

#### 輸入序號

![ ](images/3.png)

#### 安裝目錄 ( /opt/adobe/ams )，直接按 Enter

![ ](images/4.png)

#### 輸入管理員名稱：administrator

![ ](images/5.png)

#### 輸入管理員密碼：xxxxxxxx

![ ](images/6.png)

#### 密碼二次輸入

![ ](images/7.png)

#### 接下來都用預設，Enter

![ ](images/8.png)

#### 完成後總結圖如下，再輸入 y 確認安裝

![ ](images/9.png)

#### 重啟 AMS 服務

```
service ams restart
```

#### 確認 AMS 啟動狀態 ( 有時候會不成功服務需多重起幾次 )，狀態檢查完按 Q 離開

```
service ams status
```

![ ](images/10.png)

#### wowza 是使用 1935 port 記得打開 1935 port

```
sudo ufw allow 22 ( 記得要先開啟 22 再開其他 port )

sudo ufw allow 1935
```

![ ](images/11.png)

#### 進入 /opt/adobe/ams/applications 建立一個資料夾 ( 此資料夾是給 wowza 用的 )

```
cd /opt/adobe/ams/applications
```

![ ](images/12.png)

#### 建立一個資料夾

```
mkdir 隨意資料夾名稱

ex： mkdir test
```

![ ](images/13.png)

#### 調到最高權限

```
chmod 777 資料夾名稱

ex： chmod 777 test 
```

![ ](images/14.png)

#### 到這邊 original 安裝跟設定就完成了