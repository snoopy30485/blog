---
title: VXG建立
date: 2018-11-24 15:59:00
tags:
---

### VXG 是跟 wowza 一樣的流媒體服務器，本文章將介紹如何建立起來

#### VXG streaming server 下載方式

#### 進入官網：https://www.videoexpertsgroup.com/

#### 點擊右上角 FREE TRIAL 輸入 email 申請免費30天帳號 ( 此帳號是官網雲端帳號 )

![ ](images/21.png)
![ ](images/22.png)

#### 輸入完 email 後進入 email 點擊 Confirm Email Address 會開啟分頁輸入自己的密碼

![ ](images/23.png)
![ ](images/24.png)

#### 輸入完密碼會回到登入頁面，輸入信箱跟剛剛設定的密碼登入

![ ](images/25.png)

#### 到了登入頁面點擊左邊列表 Downloads，選擇 VXG Streaming Server 下載

![ ](images/26.png)
![ ](images/27.png)

#### 接下來把檔案放到欲安裝機器安裝，本文章使用的是 ubuntu 16.04

#### 更新

```
sudo apt-get update
```
#### 容器安裝

```
sudo apt-get -y install docker.io
```

#### zip 解壓縮安裝

```
sudo apt-get -y install unzip
```

#### 將下載檔案解壓縮

```
sudo unzip VXG.Server-1.3.161_181218.zip
```

![ ](images/1.png)

#### 進入解壓縮資料夾

```
cd 20181218
```

![ ](images/2.png)
![ ](images/3.png)

#### 設置 docker images

```
sudo ./setup.sh
```

![ ](images/4.png)

#### 啟動服務器，看到下圖就是成功，開啟瀏覽器直接輸入安裝 VXG 器 IP 登入，默認登錄帳號密碼：admin / admin

#### 參數介紹：

#### -r：使用本地存儲運行VXG Server以獲取記錄。

#### -h：SERVER_HOST：在早期版本的VXG Server上運行兼容模式。

#### -c：CERTIFICATE_PATH：繼續使用HTTPS證書。

```
sudo ./start.sh -r -h SERVER_HOST -c CERTIFICATE_PATH
```

![ ](images/5.png)

#### 停止 VXG 服務器

```
./stop.sh
```

![ ](images/6.png)

#### 首次啟動需要許可證密要，會需要再度登入官網雲端

#### 打開瀏覽器輸入安裝 VXG 機器 IP 進入 VXG 管理畫面

![ ](images/7.png)


#### 點擊左列 License 複製 UUID

![ ](images/8.png)

#### 接下來來到 VXG 雲端

![ ](images/9.png)

#### 點擊左列 License & Plans，如下圖點擊 SET 把剛剛複製的 UUID 貼上去

![ ](images/10.png)

#### 貼上去後會給你一組 Key 複製下來

![ ](images/11.png)

#### 再回到安裝 VXG 機器 IP 開啟的網頁，把複製的 Key 貼上，接下來就可以正常操作了

![ ](images/12.png)

#### 示範：

#### 點擊左列 Server Admin → 點擊 ADD NEW CHANNEL

![ ](images/13.png)

#### 選擇想要的流方式，本文章是使用 ip camer

![ ](images/14.png)

#### 輸入參數

![ ](images/15.png)

#### 輸完參數會有測試網頁讓你測試，點擊網址開啟分頁觀看

![ ](images/16.png)
![ ](images/17.png)

#### 點擊齒輪圖案可以設定想要觀看格式

![ ](images/18.png)

#### 往下拉會出現 QR code 給手機使用的，手機必須下載 VXG StreamLand 才能用

![ ](images/19.png)

#### 點擊完成後會出現下圖畫面，紅框地方編輯跟刪除

![ ](images/20.png)

#### 到這邊基本操作就結束了！