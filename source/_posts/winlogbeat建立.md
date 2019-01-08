---
title: winlogbeat建立
date: 2018-07-31 14:49:55
tags:
---

### ELK 建立好了後會需要將 LOG 輸入，本章將使用 winlogbeat 6.2.2 輸入 Windows log

#### 下載網址：https://www.elastic.co/downloads/past-releases

***

#### 一、下載 winlogbeat 並設定 config

#### 將下載的檔案解壓縮並放到自己指定的路徑，本文章放在 D:\service\winlogbeat-6.2.2-windows-x86_64

#### 解壓縮後檔案如圖

![ ](images/1.png)

#### 打開裡面的 winlogbeat.yml 做設定

#### winlogbeat-elasticsearch、kibana 內容

#### https://snoopy30485.github.io/2018/07/31/winlogbeat/

#### winlogbeat-elasticsearch、logstash、kibana 內容

#### https://snoopy30485.github.io/2018/07/31/logstash-winlogbeat/

#### winlogbeat-redis、elasticsearch、logstash、kibana 內容

#### https://snoopy30485.github.io/2018/07/31/Redis-winlogbeat/

#### 二、打開 CMD 做測試

#### cd 進入路徑 D:\service\winlogbeat-6.2.2-windows-x86_64

#### 測試 winlogbeat config 正確會顯示 OK

```
winlogbeat test config
```

#### 啟動 winlogbeat

```
winlogbeat
```

![ ](images/2.png)

#### 會看到資料夾多 2 個檔案就代表開始傳送資料了

![ ](images/3.png)

#### 接著連進 GCP 的 VM

#### 下指令可以檢查 log 是否有確實傳送近來

```
curl -s http://localhost:9200/_cat/indices?v
```

#### 下圖為資料近來後畫面

![ ](images/4.png)

#### 也可以到上篇文章 elasticsearch 指定的路徑看

```
cd /data/elasticsearch/nodes/0/indices/
```

```
ls 或 ll
```

#### 下圖為資料近來畫後面

![ ](images/5.png)
![ ](images/6.png)

***

#### 三、用 powershell 把 winlogbeat 轉服務

#### 當 log 有成功進來後，會把 winlogbeat 轉成服務，這樣每次重開機後都會自行啟動

#### 啟動 windows 內建的 powersfell

![ ](images/7.png)

#### 轉服務指令

#### 指令參數：

#### Executionpolicy：為殼層指定新的執行原則

#### Unrestricted ：任何腳本檔皆可被執行

```
powershell.exe -executionpolicy unrestricted -file.\install-service-winlogbeat.ps1
```

#### 執行一次

```
r (run once)
```

#### 啟動服務

```
net start winlogbeat
```

![ ](images/8.png)

#### 恭喜 winlogbeat 建立完成！