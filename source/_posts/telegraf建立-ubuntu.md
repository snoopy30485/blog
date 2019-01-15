---
title: telegraf建立-ubuntu
date: 2018-08-09 14:09:00
tags:
---

#### 1. 取得 telegraf 安裝包

```
wget https://dl.influxdata.com/telegraf/releases/telegraf_1.5.3-1_amd64.deb
```

#### 2. 安裝 telegraf

```
sudo dpkg -i telegraf_1.5.3-1_amd64.deb
```

#### 3. 編輯 telegraf config 檔

```
vim /etc/telegraf/telegraf.conf
```

#### telegraf 內容：

#### 4. 以上設定完成後存檔並重啟telegraf服務

```
service telegraf restart
```