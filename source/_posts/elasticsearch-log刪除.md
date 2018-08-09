---
title: elasticsearch-log刪除
date: 2018-08-01 14:22:59
tags:
---

### elasticsearch log 刪除

### 手動刪除指令

### 要按照你 logstash.conf 設定格式才能刪除，\* 是全部刪除如下例子 2018.\* 就是 2018 的 log 全刪除

```
curl -XDELETE 'http://127.0.0.1:9200/( log格式 )'

ex：curl -XDELETE 'http://127.0.0.1:9200/winlogbeat-6.2.2-2018.01.15'

ex：curl -XDELETE 'http://127.0.0.1:9200/winlogbeat-6.2.2-2018.*'
```

### 自動刪除


