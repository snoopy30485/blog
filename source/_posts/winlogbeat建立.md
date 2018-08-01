---
title: winlogbeat建立
date: 2018-07-31 14:49:55
tags:
---

### ELK 建立好了後會需要將 LOG 輸入，本章將使用 winlogbeat 6.2.2 輸入 Windows log

### 下載網址：https://www.elastic.co/downloads/past-releases

***

### 一、下載 wunlogbeat 並設定 config

### 將下載的檔案解壓縮並放到自己指定的路徑，本文章放在 D:\service\winlogbeat-6.2.2-windows-x86_64

### 解壓縮後檔案如圖

![ ](images/1.png)

### 打開裡面的 winlogbeat.yml 做設定

### 37 行 name: 名字 ( 也可以不設定，預設是用本機名稱 )

### 103 行 hosts: ["安裝 ELK 機器的外網 IP:5044"] ( 如果有網域，可把 ip 改成網域 )

```
###################### Winlogbeat Configuration Example ##########################

# This file is an example configuration file highlighting only the most common
# options. The winlogbeat.reference.yml file from the same directory contains all the
# supported options with more comments. You can use it as a reference.
#
# You can find the full configuration reference here:
# https://www.elastic.co/guide/en/beats/winlogbeat/index.html

#======================= Winlogbeat specific options ==========================

# event_logs specifies a list of event logs to monitor as well as any
# accompanying options. The YAML data type of event_logs is a list of
# dictionaries.
#
# The supported keys are name (required), tags, fields, fields_under_root,
# forwarded, ignore_older, level, event_id, provider, and include_xml. Please
# visit the documentation for the complete details of each option.
# https://go.es.io/WinlogbeatConfig
winlogbeat.event_logs:
  - name: Application
    ignore_older: 72h
  - name: Security
  - name: System

#==================== Elasticsearch template setting ==========================

setup.template.settings:
  index.number_of_shards: 3
  #index.codec: best_compression
  #_source.enabled: false

#================================ General =====================================

# The name of the shipper that publishes the network data. It can be used to group
# all the transactions sent by a single shipper in the web interface.
name:

# The tags of the shipper are included in their own field with each
# transaction published.
#tags: ["service-X", "web-tier"]

# Optional fields that you can specify to add additional information to the
# output.
#fields:
#  env: staging


#============================== Dashboards =====================================
# These settings control loading the sample dashboards to the Kibana index. Loading
# the dashboards is disabled by default and can be enabled either by setting the
# options here, or by using the `-setup` CLI flag or the `setup` command.
#setup.dashboards.enabled: false

# The URL from where to download the dashboards archive. By default this URL
# has a value which is computed based on the Beat name and version. For released
# versions, this URL points to the dashboard archive on the artifacts.elastic.co
# website.
#setup.dashboards.url:

#============================== Kibana =====================================

# Starting with Beats version 6.0.0, the dashboards are loaded via the Kibana API.
# This requires a Kibana endpoint configuration.
setup.kibana:

  # Kibana Host
  # Scheme and port can be left out and will be set to the default (http and 5601)
  # In case you specify and additional path, the scheme is required: http://localhost:5601/path
  # IPv6 addresses should always be defined as: https://[2001:db8::1]:5601
  #host: "localhost:5601"

#============================= Elastic Cloud ==================================

# These settings simplify using winlogbeat with the Elastic Cloud (https://cloud.elastic.co/).

# The cloud.id setting overwrites the `output.elasticsearch.hosts` and
# `setup.kibana.host` options.
# You can find the `cloud.id` in the Elastic Cloud web UI.
#cloud.id:

# The cloud.auth setting overwrites the `output.elasticsearch.username` and
# `output.elasticsearch.password` settings. The format is `<user>:<pass>`.
#cloud.auth:

#================================ Outputs =====================================

# Configure what output to use when sending the data collected by the beat.

#-------------------------- Elasticsearch output ------------------------------
#output.elasticsearch:
  # Array of hosts to connect to.
  #hosts: ["35.236.160.168:9200"]

  # Optional protocol and basic auth credentials.
  #protocol: "https"
  #username: "elastic"
  #password: "changeme"

#----------------------------- Logstash output --------------------------------
output.logstash:
  # The Logstash hosts
  hosts: ["33.231.165.122:5044"]

  # Optional SSL. By default is off.
  # List of root certificates for HTTPS server verifications
  #ssl.certificate_authorities: ["/etc/pki/root/ca.pem"]

  # Certificate for SSL client authentication
  #ssl.certificate: "/etc/pki/client/cert.pem"

  # Client Certificate Key
  #ssl.key: "/etc/pki/client/cert.key"

#================================ Logging =====================================

# Sets log level. The default log level is info.
# Available log levels are: error, warning, info, debug
#logging.level: debug

# At debug level, you can selectively enable logging only for some components.
# To enable all selectors use ["*"]. Examples of other selectors are "beat",
# "publish", "service".
#logging.selectors: ["*"]

#============================== Xpack Monitoring ===============================
# winlogbeat can export internal metrics to a central Elasticsearch monitoring
# cluster.  This requires xpack monitoring to be enabled in Elasticsearch.  The
# reporting is disabled by default.

# Set to true to enable the monitoring reporter.
#xpack.monitoring.enabled: false

# Uncomment to send the metrics to Elasticsearch. Most settings from the
# Elasticsearch output are accepted here as well. Any setting that is not set is
# automatically inherited from the Elasticsearch output configuration, so if you
# have the Elasticsearch output configured, you can simply uncomment the
# following line.
#xpack.monitoring.elasticsearch:
```

***

### 二、打開 CMD 做測試

### cd 進入路徑 D:\service\winlogbeat-6.2.2-windows-x86_64

### 測試 wunlogbeat config 正確會顯示 OK

```
winlogbeat test config
```

### 啟動 winlogbeat

```
winlogbeat
```

![ ](images/2.png)

### 會看到資料夾多 2 個檔案就代表開始傳送資料了

![ ](images/3.png)

### 接著連進 GCP 的 VM

### 下指令可以檢查 log 是否有確實傳送近來

```
curl -s http://localhost:9200/_cat/indices?v
```

### 下圖為資料近來後畫面

![ ](images/4.png)

### 也可以到上篇文章 elasticsearch 指定的路徑看

```
cd /data/elasticsearch/nodes/0/indices/
```

```
ls 或 ll
```

### 下圖為資料近來畫後面

![ ](images/5.png)
![ ](images/6.png)

***

### 三、用 powershell 把 winlogbeat 轉服務

### 當 log 有成功進來後，會把 winlogbeat 轉成服務，這樣每次重開機後都會自行啟動

### 啟動 windows 內建的 powersfell

![ ](images/7.png)

### 轉服務指令

### 指令參數：

### Executionpolicy：為殼層指定新的執行原則

### Unrestricted ：任何腳本檔皆可被執行

```
powershell.exe -executionpolicy unrestricted -file.\install-service-winlogbeat.ps1
```

### 執行一次

```
r (run once)
```

### 啟動服務

```
net start winlogbeat
```

![ ](images/8.png)

***

### 四、winlogbeat log 刪除+

### 手動刪除指令

### 要按照你 logstash.conf 設定格式才能刪除，\* 是全部刪除如下例子 2018.\* 就是 2018 的 log 全刪除

```
curl -XDELETE 'http://127.0.0.1:9200/( log格式 )'

ex：curl -XDELETE 'http://127.0.0.1:9200/winlogbeat-6.2.2-2018.01.15'

ex：curl -XDELETE 'http://127.0.0.1:9200/winlogbeat-6.2.2-2018.*'
```

### 自動刪除



### 恭喜 winlogbeat 建立完成！