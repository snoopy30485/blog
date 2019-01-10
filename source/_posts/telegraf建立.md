---
title: telegraf建立
date: 2018-08-03 14:08:00
tags:
---

#### 1. 下載 telegraf 壓縮檔

#### 下載網址：https://github.com/influxdata/telegraf/releases

#### 2. 將檔案解壓縮後會有 config 與 exe 檔，放到須監控的機器底下的 D:\Service\telegraf\（ 若沒有 D 槽，放在系統槽即可 )

![ ](images/1.png)

#### 3. 打開 telegraf.conf 做設定

#### telegraf 內容：

#### 4. 以系統管理員身份開啟 Command Prompt ( cmd )，輸入指令到 telegraf 的路徑下，進行 telegraf 服務安裝並啟動

![ ](images/2.png)

#### 進入 telegraf 的路徑下

```
D:
cd Service/telegraf
```

#### 安裝成服務

```
telegraf.exe --config D:\Service\telegraf\telegraf.conf --service install
```

#### 啟動也可以到 services.msc 啟動

```
net start telegraf
```

![ ](images/3.png)
![ ](images/4.png)

#### 服務安裝完成後，會在路徑底下多一個剛剛 config 設定的 telegraf.log 檔案

![ ](images/5.png)

#### 恭喜 telegraf 建立完成！