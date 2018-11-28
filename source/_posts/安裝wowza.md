---
title: 安裝wowza
date: 2018-10-29 13:36:29
tags:
---

### 一、什麼是 wowza

#### Wowza Streaming Engine 是媒體服務器軟件，提供可靠性強，流暢度高的高質量視頻和音頻到任何設備的傳輸。無論是在雲端還是當前操作，Wowza Streaming Engine 都可以提供組件，讓我們不僅可以保證工作流的流暢性還有安全性。

#### 1. Wowza 是一個不論平台、多格式、多屏幕軟件。它接受任何的視頻格式，一次性轉碼，可靠地進行多格式傳輸，並以最大可能的質量傳輸到任何地方的任何連接設備。

#### 2. Wowza 提供豐富的功能專為流暢的現場內容而設計，包括位碼流暢性，DVR 性能和發布功能。

#### 3. 用融合了其他系統和第三方解決方案的外延軟件，自定義你的流線型作品。平衡軟件強大的組件和 APIs，建立支持你持續發展的工作流的解決方案。

#### 4. Wowza Streaming Engine Manager 可以從一個電腦或者任何的移動設備管理，監察和測量視頻和音頻。

### 二、安裝 wowza for windows

#### 官方下載網址：https://www.wowza.com/pricing/installer

#### 下載下方有安裝需求說明

![ ](images/1.png)

#### 開始安裝

![ ](images/2.png)

#### 輸入金鑰

![ ](images/3.png)

#### 設定 wowza web 登入帳密

![ ](images/4.png)

#### 設定安裝好開啟 web wowza

![ ](images/5.png)

#### 設定安裝位置

![ ](images/6.png)

#### 打開網頁輸入 外網 IP:8088 登入測試 ( 如果是本機 IP 可以輸入 127.0.0.1 或是內網 IP )，出現下圖畫面就是安裝成功了，如果是別台電腦打開 wowza web 防火牆 8088 port 記得開

![ ](images/16.png)

### 三、安裝 wowza for ubuntu 16.04

#### 官方下載網址：https://www.wowza.com/pricing/installer ( 一樣的地方 )

#### 下載下方有安裝指令

![ ](images/7.png)

#### 輸入官方給的指令安裝，接下來會出現條款一直按 Enter 到下一步

```
sudo chmod +x WowzaStreamingEngine-4.7.6-linux-x64-installer.run
```

```
sudo ./WowzaStreamingEngine-4.7.6-linux-x64-installer.run
```

![ ](images/8.png)

#### 讀完條約會出現同意/不同意，輸入 y 同意

![ ](images/9.png)

#### 同意完會出現金鑰輸入，輸入金鑰

![ ](images/10.png)

#### 輸完金鑰，鑰需要輸入帳密 ( 登入 wowza web 用 )，先輸入帳號

![ ](images/11.png)

#### 輸完帳號會問密碼，輸入2次後 OK

![ ](images/12.png)

#### 設定安裝完自動啟動 wowza

![ ](images/13.png)

#### 詢問是否安裝

![ ](images/14.png)

#### 跑完讀條，出現圖文字就是完成了

![ ](images/15.png)

#### 開啟 port

```
sudo ufw allow 22 ( 記得要先開啟 22 再開其他 port )

sudo ufw allow 1935 ( wowza 串流 port )

sudo ufw allow 8088 ( wowza 網頁 port )
```

![ ](images/17.png)

#### 一樣打開網頁測試 ( 在別台電腦開啟網頁輸入 機器外網 IP：8088 )

![ ](images/16.png)