---
title: telegraf建立-ubuntu
date: 2018-08-03 14:12:08
tags: grafana
categories: grafana
---

#### 1. 取得 telegraf 安裝包

<!-- more -->

```
wget https://dl.influxdata.com/telegraf/releases/telegraf_1.5.3-1_amd64.deb
```

#### 2. 安裝 telegraf

```
sudo dpkg -i telegraf_1.5.3-1_amd64.deb
```

#### 3. 編輯 telegraf config 檔

```
sudo vi /etc/telegraf/telegraf.conf
```

#### telegraf 內容：https://snoopy30485.github.io/2018/08/03/telegraf-ubuntu/

#### 4. 以上設定完成後存檔並重啟telegraf服務

```
service telegraf restart
```